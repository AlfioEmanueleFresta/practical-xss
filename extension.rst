Extension Challenge
===================

XSS attacks have been used many times in the recent years to attack
important companies and websites, including Tweeter's Tweetdeck in 2004[1],
MySpace in 2005[2] and Facebook in 2011[3]. All these attacks had one thing
in common: the Javascript code injected had the ability to replicate
itself in some way across the website:

* Tweetdeck's vulnerability was exploited to retweet the malicious
  automatically when viewing the tweet.

* MySpace's vulnerability was exploited by an attacker to autmatically add
  to each person's profile the phrase "samy is my hero", plus some code that
  would automatically and silently put the same phrase in the viewer's profile.

* Facebook's vulnerability was exploited by an attacker to automatically send
  a private message to the victim's friends, which included a malicious URL.


**Write a comment containing some Javascript code which will**
**share itself (both the text of the comment and the Javascript code)**
**as a new comment to an article of your choice by the victim.**

**The victim should not**
**be able to notice the attack (i.e. no message should appear, and the webpage**
**should not refresh to reveal the new comment created for the victim).**

Hint:
  Comments can be published by any authenticated users
  by making an HTTP POST request to the
  web application, using the URL ``http://<IP ADDRESS>:12342/?page=comment.php``, with the following
  parameters:

  * ``article_id``: numeric ID of an existing article (you
    can find it in the URL when viewing an article),
  * ``body``: the text of the comment.

  You can use HTML classes and jQuery's helpers to find objects in
  the document.

  .. code:: html

    <div class="my-class">
      Hello <strong>World</strong>
    </div>

  .. code:: javascript

    jQuery(".my-class")
    // This will get all objects with class "my-class". Note that this
    // is an iterable and you should use an index or methods such as
    // .first(), .last() to get a single object.

  Also, you may find useful the documentation of these jQuery methods:

  * jQuery(...):    https://api.jquery.com/jquery/
  * jQuery.post():  https://api.jquery.com/jQuery.post/
  * .parent():      https://api.jquery.com/parent/
  * .html():        https://api.jquery.com/html/


**References**

(1) "Twitter shuts down Tweetdeck after XSS flaw leaves users vulnerable to account hijack", Alex Hern, The Guardian.
  https://www.theguardian.com/technology/2014/jun/11/twitter-tweetdeck-xss-flaw-users-vulnerable
(2) "Samy (Computer worm)", Wikipedia.
  https://en.wikipedia.org/wiki/Samy_(computer_worm)
(3) "Persistent XSS Vulnerability in Facebook", Candid Wueest, Symantec.
  http://www.symantec.com/connect/blogs/persistent-xss-vulnerability-facebook
