Extension Challenge
===================

XSS attacks have been used many times in the recent years to attack
important companies and websites, including Tweeter's Tweetdeck in 2004[1],
MySpace in 2005[2] and Facebook in 2011[3]. All these attacks had one thing
in common: the Javascript code injected had the ability to replicate
itself over the website:

* Tweetdeck's vulnerability was exploited to retweet the mailicious
  automatically when viewing the tweet.

* MySpace's vulnerability was exploited by an attacker to autmatically add
  to each person's profile the phrase "samy is my hero", plus some code that
  would automatically and silently put the same phrase in the viewer's profile.

**Extend the code used in the last excercise, so that the code will automatically**
**reproduce itself it the user who views the comment is authenticated.**

Hint:
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

  * jQuery(...):  http://api.jquery.com/jquery/
  * .parent():    https://api.jquery.com/parent/
  * .html():      http://api.jquery.com/html/


**References**

[1] "Twitter shuts down Tweetdeck after XSS flaw leaves users vulnerable to account hijack"
  Alex Hern, The Guardian. [Online] Available at:  https://www.theguardian.com/technology/2014/jun/11/twitter-tweetdeck-xss-flaw-users-vulnerable
  [Accessed July 2016].
[2] "Samy (Computer worm)"
  Wikipedia. [Online] Avaiable at: https://en.wikipedia.org/wiki/Samy_(computer_worm)
  [Accessed July 2016].
[3] "Persistent XSS Vulnerability in Facebook",
  Candid Wueest, Symantec. [Online] Available at: http://www.symantec.com/connect/blogs/persistent-xss-vulnerability-facebook
  [Accessed July 2016].
