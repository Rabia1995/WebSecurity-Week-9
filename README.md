# Project 8 - Pentesting Live Targets

Time spent: **10** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: _______SQL Injection (SQLi)_______

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_blue1.gif" width="800">

In this vulnerability, the user can perform an attack by adding SQLi at the end of the URL. By adding ``` 'OR SLEEP(5)=0' ``` at the end of the URL, it will give an id like 
``` %27OR%20SLEEP(5)=0--%27 ``` Replacing the id of another salesperson with this id gives a different salesperson, indicating that it responded to the SQL injection that was added. 

Vulnerability #2: _____Session Hijacking/Fixation_____

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_blue2.gif" width="800">

Steps:
1. In blue target go to login homepage and input username and password and sumbit(Login should be unsuccessful)
2. Add this ```public/hacktools/change_session_id.php``` in the URL to change the session ID  
3. Go to red/green targets and login-in
4. Use ```public/hacktools/change_session_id.php``` again. The session ID should be different than the blue target 
5. Replace the blue target session ID with green/red target session ID
6. The attacker is now able to access the victims session



## Green

Vulnerability #1: _____User Enumeration_____

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_green1.gif" width="800">


Steps:
1. Go to Login and sign in with a invalid username and password. It will give as error "Login was unsuccessful" but it will not be bolded
2. Using the given username "pperson" a valid username but incorrect password shows the same error "Login was unsuccessful" but in bold

Vulnerability #2: __Cross-Site Scripting (XSS)__

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_green2.gif" width="800">


Steps:
1. On green target go to feedback and input random information
2. In the comment section input ```'<script>alert('Found the XSS!');</script>'```
3. Submit the feedback then login. You will receive the message. 


## Red

Vulnerability #1: ____Insecure Direct Object Reference (IDOR)____

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_red1.gif" width="800">


Steps:
1. Go to salesperson tab in the red target and select any saleperson.
2. The salesperson database can be accessed by change the "id=" tag in the url 
3. By setting the id to 10 and 11 in the red target will not access the salesperson
4. By setting the id to 10 or 11 in the green or the blue target, you will be able to access the salesperson


Vulnerability #2: __Cross-Site Request Forgery (CSRF)__

<img src="https://github.com/Rabia1995/WebSecurity-Week-8/blob/master/Week8_red2.gif" width="800">


Since the red site does not have CSRF protections on the staff area, an attacker can design a form that can submit data to a part of the website that requires admin access.
An attacker can link a hidden form in the feedback that submits data to the edit page for a salesperson. When the admin follows the link, the form is submitted without the knowledge of admin. As a result, the name of the salesperson is changed. 


## Notes

One of the difficulties was actually finding which of the three websites had what vulnerability
