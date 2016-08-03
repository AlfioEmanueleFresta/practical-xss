Conclusion
==========

Summary: Important points
_________________________

As websites and web applications are now extremely common, and most organisations
and many private individuals have a web presence, online accounts become more
and more important and valuable.

Most everyday computer software now has moved,
or is progressively moving, to web applications.
Attacks on web applications have the potential of compromising the privacy of
many users very quickly, significantly more than what was possible with worms
that replicated via email in the 90s.

For these reasons it is more important than ever that those who are
responsible for designing and implementing web applications have a
thorough understanding of security risks and good practices.

XSS is one of the most common attacks on web applications, and can
lead to disastrous consequences for organisations in terms of responsibilities
and costs, but are also very easy to avoid by enforcing good practices
in the development process.

Moreover, web technologies change quickly and significantly. For example,
the HTML standard evolved significantly and new versions of the standard
have many more functionalities that have quickly been be exploited for
new kinds of attacks. It is therefore of uttermost importance for businesses
and development teams to understand and put in place processes for reviewing
the security aspect of applications periodically, and strengthening it if
necessary.


Data sanitisation methods
-------------------------

There are many ways in which data, including both input from the users and
the data persisted in memory or a database, can be sanitised. There are two
opposite methods that can be used to tackle the problem of sanitisation:

* **Whitelisting approach**: analysing the input and only allowing what is
  clearly recognised as non-malicious. For example, in case of HTML sanitisation,
  a website could only allow tags from a list of "good" known tags. This is easy
  to implement, probably the most common and can be safer. The issue with this
  method is that potentially innocuous data, such as new and different tags for
  text manipulation, could be rejected.

* **Blacklisting approach**: analysing the input and trying to recognise
  malicious data, and blocking it. For example, in case of HTML sanitisation,
  a website could block ``<script>``, ``<img>``, and similar tags from a
  list of "bad" known ones. The issue
  with this method is that, as technology evolves quickly and new tags are
  introduced, some may be exploited before they are blacklisted,
  therefore it requires the blacklist to be periodically reviewed and
  updated proactively.

Common web frameworks for most programming languages generally
offer built-in techinques to protect the applications from XSS
attacks, including template engines that require the programmer to
explicitely deactivate HTML escaping. Using these frameworks significantly
reduces the risk of accidental security vulnerabilities in your
applications.

Examples of PHP template
engines with this behaviour are `Smarty <http://www.smarty.net/>`_ and
`Twig <http://twig.sensiolabs.org/>`_. Examples of Python web frameworks
include `Django <https://www.djangoproject.com/>`_ and
`Web2py <http://www.web2py.com/>`_.

Alternatively, most web programming languages include functions to
help you process users' input data. For example, in PHP you should use
`htmlspecialchars() <http://php.net/manual/en/function.htmlspecialchars.php>`_
or `htmlentities() <http://php.net/manual/en/function.htmlentities.php>`_ to
securely excape any HTML input.


OWASP XSS Prevention Cheat Sheet
--------------------------------

OWASP (The Open Web Application Security Project, https://www.owasp.org)
published on its wiki a list of 11 XSS prevention rules.

    * RULE #0 - Never Insert Untrusted Data Except in Allowed Locations
    * RULE #1 - HTML Escape Before Inserting Untrusted Data into HTML Element Content
    * RULE #2 - Attribute Escape Before Inserting Untrusted Data into HTML Common Attributes
    * RULE #3 - JavaScript Escape Before Inserting Untrusted Data into JavaScript Data Values
    * RULE #4 - CSS Escape And Strictly Validate Before Inserting Untrusted Data into HTML Style Property Values
    * RULE #5 - URL Escape Before Inserting Untrusted Data into HTML URL Parameter Values
    * RULE #6 - Sanitize HTML Markup with a Library Designed for the Job
    * RULE #7 - Prevent DOM-based XSS
    * Bonus Rule #1: Use HTTPOnly cookie flag
    * Bonus Rule #2: Implement Content Security Policy
    * Bonus Rule #3: Use an Auto-Escaping Template System
    * Bonus Rule #4: Use the X-XSS-Protection Response Header

You can read more about each of these rules at: https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet.


Ethical Issues
______________

As is common in security teaching, the techniques described here could be
used to attack systems but you must behave responsibly and ethically toward
other people, their data and systems. The writing or use of tools to gain
unauthorised access to systems is a criminal offence.

The Computer Misuse Act (1990) clearly states:

  [...]

  A person is guilty of an offence if—
    (a) he causes a computer to perform any function with intent to secure access to any program or data held in any computer, or to enable any such access to be secured;
    (b) the access he intends to secure, or to enable to be secured, is unauthorised;

  [...]

You can learn more about the Act at http://www.legislation.gov.uk/ukpga/1990/18/contents.


Further Reading and References
______________________________

* **Excess XSS** by Jakob Kallin and Irene Lobo Valbuena is a good starting point
  if you want to learn more about types of XSS attacks. It is freely available online
  at http://excess-xss.com/.

* The **National Vulnerability Database** (https://web.nvd.nist.gov/)
  is the U.S. governement repository
  of standards based vulnerability management data. According to this database,
  XSS represented a significant portion of all vulnerabilities reported.

  .. image:: img-nist.png

  *Cross-Site Scripting Vulnerabilities Matches per Year*

  Source: https://web.nvd.nist.gov/view/vuln/statistics-results?adv_search=true&cves=on&cwe_id=CWE-79&cvss_version=3
