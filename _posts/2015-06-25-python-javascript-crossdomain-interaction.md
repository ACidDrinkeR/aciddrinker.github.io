---
title: "Cross domain solution to execute Python scripts using JS, jQ, AJAX."
layout: post
date: 2015-06-25
---

So I've been learning python scripting, and I've been trying to figure out a 
very simple and trivial question.. how do I run my python scripts online?

Not everyone will have access to a machine with python installed, neither will
everyone wish to install python just to execute scripts. So I wondered if
there was a way to run the python script on a server and obviously there is.
It's also quite easy by using a framework like 'Flask' or 'Bottle' or, if you
dare, 'Django'. But the problem was that they required my whole site to be 
on the same domain.. but that is not what I had in mind.

I currently host my personal site [http://mitesh.ninja](http://mitesh.ninja)
via GitHub Pages, because it's free and natively supports Jekyll (my static
blogging platform of choice). I wanted the input to my scripts taken from the
user/client on this website, which will then be relayed over to my server
which executes the python script with the respective inputs and relays back
the result to my page @mitesh.ninja/&lt;project&gt;.

But wait a minute.. I have absolutely no idea about web development? So I
decided to start with some simple Javascript and read this amazing introduction
by [MDN](). I then realised I need to learn jQuery, AJAX, JSON, HTML headers,
and, Python web frameworks. I was overwhelmed by the sheer amount of information
I was about to soak in the next few days. Instead I just decided to start coding. 

I installed flask `sudo python3 install flask` and quickly got a basic web app
running on localhost. 

<script src="https://gist.github.com/MiteshNinja/e7dc40a099bad92fb752.js"></script>

I could then go to [http://127.0.0.1:8800/2-3](http://127.0.0.1:8800/2-3) and
I would get the following output: 

<samp>Sum of x + y = 5</samp>

So I got my python script running as a webapp. I know had to find a way to get
the input for this script from the user. Like I said, I had no clue about web
development so I started looking at forms. HTML tag `<form>` was a very quick
and easy way to take input from the user and I quickly made a sample html file
with input form for my python script.

<script src="https://gist.github.com/MiteshNinja/660caf1fcf7c4ce284b4.js"></script>

So now I could take input from the user. I somehow had to feed this input into my python script. I first tried doing it via pure javascript alone. A little bit of searching convinced me to instead use AJAX + jQuery. 

I came up with the following solution:

<script src="https://gist.github.com/MiteshNinja/d1208766d38f4e565a2a.js"></script>
}

This would take the answer from my python script and insert it inside the div tag with class ".result", atleast it would in theory.

Having absolutely no knowledge about JS, jQuery or AJAX. It was hard for me to debug my own code. 

There was a particular error which took me quite some time to figure out: 

<samp>XMLHttpRequest cannot load http://127.0.0.1:8800/2-3. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'null' is therefore not allowed access.</samp>

This is when I learned that my sample site was not authorised to transfer/relay data on another server/host. I fixed this by including a header to the respone in my python app.

<script src="https://gist.github.com/MiteshNinja/68f158065f85cec84bde.js"></script>

I included some more CORS code in jQuery/ajax function, but I don't quite understand it completely.

The final result can be seen here: [http://mitesh.ninja/sample](http://mitesh.ninja/sample). 




