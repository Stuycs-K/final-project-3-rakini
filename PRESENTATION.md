# Cookie Monster's Guide to Stealing Cookies! 

### History of the name 
The name itself was coined by Lou Montulli and is derived from the term 'magic cookie', which referred to a token of data used to communicate between programs, which in itself comes from 'fortune cookie': a cookie with an embedded message. 
 
## What are cookies?
HTTP cookies are small key-value pairs created by a server while browsing a website (their maximum size limited to be 4kb). They help the website store some data for you in order to serve you better, which leads into my next point:

### Sessions 
 When you log in to websites, how do they know you are logged in whenever you reload the page? Or when you get redirected, why does it not immediately log you out? The answer, sessions. They keep track of whether or not the user is logged in AND on the site, which is one of the general security pitfalls of regular HTTP cookies.

### Stateless vs Stateful Cookies  
Cookies could be either stateless or stateful. Now, what does this actually mean? Stateful cookies hold a pointer to the session in the webserver's database while stateless cookies hold the raw data on the client's computer. Both hold it's own pros and cons. 

Pros for Stateful Cookies: 
- More secure since we could validate requests (and wipe invalid ones from the database)
- Slightly better performance as the server takes the client's connection into account 
Cons: 
- Takes more system resources from the server, and hence is limited by the server

Pros for Stateless Cookies: 
- Simplifies the design of the webserver 
- Way more scalable (as it takes resources on the client side) 

Cons: 
- The data is stored client side (which can't be trusted) 
- No easy form of validation 

## How can they be exploited and stolen? 
Cookies in general aren't the most secure, and we know that. Remember the Linus Tech Tips situation a little while ago? Or, even the fact that there were bots hijacking random discord accounts by generating a bunch of random tokens. *Now, as hobbyist hackers? Cybersecurity experts? Mongrels?* How can we exploit them to our own benefit?

### Cookie Hijacking  
First way that comes to mind is pretty simple. You manage to hijack the cookie itself somehow. How, you may ask? Get your imposing victim to click on some malicious link or download some code and steal it directly from their browser. 

Not your cup of tea? Why not apply something we just learned, cross-site scripting or XSS for short. Normally, vulnerabilities like this are patched as soon as they are found but there are quite a lot of amateur site-builders on the web that you can exploit. 

Why not take it straight from the source with a man-in-the-middle attack. Now, there's a couple of ways you could go about this. If you're on the same network, you could just open a packet-sniffer. Or, you can 'pretend' to be the website itself and be the middle-man (hence the name) and get sensitive data from both sides. However, since internet traffic is mostly encrypted nowadays, this has mostly fallen out of favor. 

### Cookie Poisoning 
Now, cookie monster won't exactly approve of this but once we have a hold of those precious cookies, we can 'poison' them by altering or forging them. This is less of an attack on the client usually and more on the server to hijack the session. 

To give some examples, look at this php code: 
``` 
Session("Login") = Request("login") 
Session("Username") = Request("username")
```
Looks fine on paper, right? But if the password for one user checks out, then we can manipulate the response: 
```vulnerable.asp?login=YES&username=BigBird``` 

What is stopping us from changing the user arbitrarily and stealing Elmo's session instead? It puts the entire userbase at risk. 

We could also alter session variables to how we see fit to get more information on either the victim or from the server, if the website didn't take these situations into account. 

## Wrap up 
The internet as we use it now has a reliance on cookies. They're a relatively easy way to store information on a user, which makes them prime target for hackers and for me, cookie monster. It might do you some good to clear your browsing data every once in a while to cut any loose ends, and the obvious of not clicking any suspicious links or whatever (you guys are better than that).




--- 
## Sources 

> https://www.invicti.com/learn/cookie-poisoning/

> https://www.analyticssteps.com/blogs/what-session-hijacking-how-prevent-it 

> https://en.wikipedia.org/wiki/HTTP_cookie  

> https://auth0.com/docs/manage-users/cookies