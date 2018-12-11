<!-- TITLE: Support Wiki -->

# Everyone Benefits
We believes that open source is good for everyone. By being open and freely available, it enables and encourages collaboration and the development of technology, solving real world problems.

# Building great open source documentation

Incomplete and confusing documentation is the top complaint about open source software, so technical writers across XEL Community are working together to change that. They'll be sharing what they learn along the way, starting with this brief guide.

<html>
  <head>
    <link rel="stylesheet" href="/path/to/css/btcdonate.css">
  </head>
  <body>

    <h1>My Awesome Web Page</h1>

    <p>Some stuff on your page and <a href="bitcoin:A_BITCOIN_ADDRESS">a donation link</a></p>
    <p>Some more stuff on your page</p>
    <p>
      Even more stuff on your page and
      <a href="bitcoin:ANOTHER_BITCOIN_ADDRESS?amount=0.01">
        another donation link, this time with a suggested amount
      </a>.
    </p>

    <script type="text/javascript" src="/path/to/js/jquery.js"></script>
    <script type="text/javascript" src="/path/to/js/jquery.qrcode.js"></script>
    <script type="text/javascript" src="/path/to/js/btcdonate.js"></script>
    <script>
      btcdonate();
    </script>

  </body>
</html>





