<!-- TITLE: E Pl Programming -->
<!-- SUBTITLE: A quick summary of E Pl Programming -->

# ePL – Programming
-----

This tutorial is designed for software programmers with a need to understand the ePL programming language starting from scratch. You will gain enough knowledge from where you can take yourself to a higher level of expertise. 

But before we get too deep into the little details, let us start with step one.

-----

Prerequisites
-----
If you want to set up your environment for programming in ePL, you need the following two software tools available on your computer:

* <p> <a href="https://github.com/xel-software/Miner-Mainnet">Xel Miner</a></p>
* <p> <a href="https://github.com/xel-software/xeline">Xeline</a></p>

-----

A Simple Example: Finding Prime Numbers
-----
The example we’ll be looking at is a simple ePL program which is meant to find prime numbers between 10000 – 20000. While it has no real relevance for the real world, it certainly is small enough to help understand how the ePL really works. First of all, let us take a look at the entire code before we start breaking down each line of it:


```java
array_uint 1000;

function main {
    verify();
} 

function primetest {
    u[1] = 0;
    if (u[2] <= 1)  u[1]=0;
    else if (u[2] <= 3) u[1]=0;
    else if (u[2]%2 == 0 || u[2]%3 == 0) u[1]=0;
    else {
        u[3]=5;
        u[1]=1;
        repeat(u[99],20000,20000){
        if (u[2]%u[3] == 0 || u[2]%(u[3]+2) == 0)
        { u[1]=0; break; }
        if(u[3]*u[3] > u[2]) break;
            u[3]+=6;
        }
    }
}

function verify {

    // make prime test
    u[2] = m[0];
    u[1]=0;
    if(m[0]>10000 && m[0]<20000) primetest();
    verify_bty ((m[0]>10000 && m[0]<20000) && (u[1]==1));

    // some randomness for POW function
    u[57] = m[1];
    u[56] = m[2];
    u[55] = m[3];
    u[54] = m[4];

    verify_pow (u[57], u[56], u[55], u[54]);
}
```

An ePL program usually starts with memory allocations which basically describe how the following six arrays are being allocated:



```java
int i[] : signed ints (32 bit)
int u[] : unsigned ints (32 bit)
int l[] : signed longs (64 bit)
int ul[] : unsigned longs (64 bit)
int d[] : doubles
int f[] : floats
```

Your ePL program should have these 6 array initialisers at the beginning, each one telling the VM how many elements it should allocate in which array. In this example it is:


```java
array_int 0;
array_uint 1000;
array_long 0;
array_ulong 0;
array_double 0;
array_float 0;
```

Lines, that allocate 0 elements to an array can be left out – this has been done in our example above. The arrays themselves do not need (and must not be) allocated by the programmer. The command `array_int 1000;` will already make sure that `I[]` is created with 1000 elements in it (indices 0 – 999). Please keep in mind, that there is no such concept as variable scopes, all arrays are global. Later, you will learn that this does not necessarily make it harder to code in ePL – just be a little patient .

In the next part, the body of your ePL program, you can define multiple functions. Functions have the following syntax:


```java
function name {
	...
}
```

Functions neither have arguments nor return values. This is not a big issue though since arguments and return values can be mimicked by simply using the global arrays. Again, later on, you will see how you still can easily and comfortably code in the way you are used to right now.

In our example we have defined three functions: `main`, `verify` and `test_prime`. While you can define as many functions are you like (as long as you stay within the maximum allowed complexity and size allowed for your program), you must have the`main` and the `verify` function.

The functions main and verify are needed both because ePL allows for an asymmetric calculation verification. To understand this a bit better, it is crucial to understand how working nodes are searching for solutions and how the rest of the network verifies these result to make sure that a scientist, who purchases computational power on XEL, actually gets what he has paid for: a correct result. Workers, those nodes who are searching for solutions to other tasks, are executing the main function whereas the verification of a solution to the algorithm is done by executing `verify()`.

This has a very good reason: XEL allows you more complex programs with a fairly longer execution time inside the main function that it does for the verification routine to ensure an easy and light weight verification on the nodes without stalling the network for too long. A good example where this asymmetrical verification could come in handy is an SAT solver. The main() function would carry a complex SAT solving logic, which is more expensive to execute, whereas the verification routine would just assign the result to the boolean formula and check if it evaluates to true. If you want to see an example of how this can be done, feel free to take a look at our SAT solving demo.

 `Important warning: It is the developers responsibility to code the logic in main and verify correctly. Especially, it is important to make sure that the logic (in particular, the verify_bty logic which we will read more about later on) in verify actually evaluates to true whenever the one in main evaluates to true. An incorrect implementation by the developer might cause results to be accepted, that does not really reflect your desired outcome. Or even more importantly, it can cause that valid results found in main are rejected by the Blockchain because they do not pass verify. Surely, this sounds still very abstract to you, but it will make more sense as we dig deeper into this tutorial.`
 
 Anyway, for now, things are very easy: in our particular case, there is no possibility to do an asymmetrical verification as finding primes is as complex as verifying them. To keep the code clean, we therefore add the entire logic into `verify`, and let the `main` function just call `verify():`
 
 
```java
function main {
    verify();
}
```

On we go. Let’s start taking a look at the `verify` function first:


```java
function verify {
    // make prime test
    u[2] = m[0];
    u[1]=0;
    if(m[0]>10000 && m[0]<20000) primetest();
    verify_bty ((m[0]>10000 && m[0]<20000) && (u[1]==1));

    // some randomness for POW function
    u[57] = m[1];
    u[56] = m[2];
    u[55] = m[3];
    u[54] = m[4];

    verify_pow (u[57], u[56], u[55], u[54]);
}
```

Before you can understand what is going on here, it is essential that you understand how randomness is introduced into the execution of your code. ePL has one more array, the so-called `uint m[12];` array – an array which consists of 12 unsigned integers. The first 10 unsigned integers are pseudorandom and provide you with 320 bits of entropy in total. `m[10]`, the 11th unsigned integer, contains the round number and `m[11]`, the 12th unsigned integer, contains the iteration that we are currently in. The concept of iterations will be explained at a later point in time.

To better understand what is going on here, please take a look at the internal C logic that fills this uint `m[12];` array:


```java
// hash32[] is a random hash value which is provided by the XEL protocol
// mult32[] contains a whole bunch of other information such as round and iteration #

// Randomize Inputs m[0]-m[9]
for (i = 0; i < 10; i++) { work->vm_input[i] = swap32(hash32[i % 4]);
  if (i > 4)
    work->vm_input[i] = work-> vm_input[i] ^ work->vm_input[i - 3];
}

// Set m[10] To Round Number
work->vm_input[10] = mult32[1];

// Set Inputs m[11] To Iteration Number
work->vm_input[11] = mult32[2];
```


In our particular example, we will use the first integer `m[0]` to pick our prime candidate. Of course, you can use the entire 320 bit to create potential solution candidates to your algorithm. If you need more than 320 bit, you can even derive an infinite pseudorandom number stream from it:


```java
u[2] = m[0];
u[1]=0;
```

In this part, we basically take over the first random value in `m[0]` and store it in one of our unsigned int array slots `u[0]` – remember, we have defined 1000 of them at the top of our program. Additionally, we initialize `u[1]` with the value `0`: this slot will later hold the result of the prime check.


```java
if(m[0]>10000 && m[0]<20000) primetest();
```

In this part, we want to call the function conducting the prime test. Since we are only interested in primes between 10000 and 20000, we only need to call that function if the value in `m[0]` meets this requirement.


```java
verify_bty ((m[0]>10000 && m[0]<20000) && (u[1]==1));
```

This part actually tells the backend system what to be considered a valid solution to your task/challenge – or a “bounty” how it is called in XEL’s terminology. This basically is a `verify_bty ()`which takes a boolean expression as an argument which should evaluate to true for every valid solution that you want to have reported back. In this case, it is really straight forward: if the number we have stored in `m[0]` is between 10000 and 20000, and the value in `m[1]` equals 1, then consider this a valid solution.

In a next step, we need to specify a condition for “proof-of-work” payments. XEL’s Blockchain works in a way, that every task has two types of payments: the proof-of-work payments and the bounty payments. This has a very simple reason: very often, bounties are very hard to find and only limited to a hand full per job. Imagine you want to find an input to a CNF formula that evaluates it to true: if you are having a bijective relation, there will be only one solution which, depending on the complexity of your formula, is very hard to find. While the discovery of such a solution should be awarded an attractive amount of coins (to keep workers motivated) you also want to keep them motivated by frequent, smaller payments. XEL introduces the concept of proof-of-work solutions to achieve that. These are solutions that do not really solve your problem but which can be submitted by the workers to claim a tiny amount of coins as a reward for ongoing commitment. As you can probably imagine, payments per bounty should be set significantly higher than payments per proof-of-work. However, if you set this value too small, other tasks on the network might seem more lucrative and attract the processing power away from you. Proof-of-work packages, by the way, work on top of a re-targeting mechanism comparable to the block difficulty re-target in Bitcoin: The more processing power the network has, the harder it becomes to find such proof-of-work solutions so that, on average, the total number of proof-of-work solutions in the entire network converges to 10 per minute.

`It is important to point out that it is the developer’s responsibility to provide the verify_pow()function with enough “evidence” that the worker has been actually working on your problem in the form of four unsigned integers. `

In our example here, we use this:


```java
// some randomness for POW function
u[57] = m[1];
u[56] = m[2];
u[55] = m[3];
u[54] = m[4];

verify_pow (u[57], u[56], u[55], u[54]);
```

Now, while it is more than fine for our little demo, it is an example of the worst way to do it for productive use. Here, we just take four integers from our random input entropy and use them to specify the proof-of-work reward condition. In this case, workers who are not really interested in getting the bounty payments but just want to work towards the proof-of-work solutions can basically omit the entire program logic and only check input integers `m[1] ... m[4]` to see if they have found a proof-of-work solution. This gives them a huge advantage over the more honest workers and allows them to get paid without really contributing anything useful to your task. It is always a best practice to use four values which depend “somehow” on the execution on as most of the program’s logic as possible. Then, only people who actually run the entire code can find those bounties. While this still does not guarantee that they will submit any bounty, there is no real reason why they shouldn’t since they have already performed all the work required for a bounty check.

In the last step, we are going to take a look at the actual prime check:


```java
function primetest {
    u[1] = 0;
    if (u[2] <= 1)  u[1]=0;
    else if (u[2] <= 3) u[1]=0;
    else if (u[2]%2 == 0 || u[2]%3 == 0) u[1]=0;
    else {
        u[3]=5;
        u[1]=1;
        repeat(u[99],20000,20000){
        if (u[2]%u[3] == 0 || u[2]%(u[3]+2) == 0)
        { u[1]=0; break; }
        if(u[3]*u[3] > u[2]) break;
            u[3]+=6;
        }
    }
}
```

What you see here is basically a simple trial-division based primality check which works on m[2](we have stored there our prime candidate before) as the input and sets m[1] = 1 if the candidate actually is a prime number, and m[1] = 0 otherwise. This value can be considered the “return value” of our function.

One novelty you have probably notices, is the strange loop construct that you have probably never seen before: