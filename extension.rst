Extension Challenge
===================

XSS attacks have been used many times in the recent years to attack
important companies and websites, including Tweeter's Tweetdeck in 2004[1] and
MySpace in 2005[2]. Both these attacks had one thing in common: the
Javascript code injected had the ability to replicate itself over
the website:

* Tweetdeck's vulnerability was exploited to retweet the mailicious
  automatically when viewing the tweet.

* MySpace's vulnerability was exploited by an attacker to autmatically add
  to each person's profile the phrase "samy is my hero", plus some code that
  would automatically and silently put the same phrase in the viewer's profile.

**Extend the code used in the last excercise, so that the code will automatically**
**reproduce itself it the user who views the comment is authenticated.**

Hint:
  You can use jQuery's helpers to get the ``<script>`` tag containing the
  code from the code itself:

  .. code:: javascript

    jQuery(this).html();

  Please note that this will only work in the webpage, and can't be used in
  the Javascript Console.

  Also, you can use ``.parent()`` from any element in the DOM tree to get its
  container (parent).


**References**

[1] "Twitter shuts down Tweetdeck after XSS flaw leaves users vulnerable to account hijack"
  Alex Hern, The Guardian. [Online] Available at:  https://www.theguardian.com/technology/2014/jun/11/twitter-tweetdeck-xss-flaw-users-vulnerable
  [Accessed July 2016].
[2] "Samy (Computer worm)"
  Wikipedia. [Online] Avaiable at: https://en.wikipedia.org/wiki/Samy_(computer_worm)
  [Accessed July 2016].
