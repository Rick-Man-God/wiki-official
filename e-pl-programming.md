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



