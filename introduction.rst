Introduction
========================================================================

Software procedures rely on the presence of well-formed input data.
Bad input data can cause programs to behave incorrectly or, in some
occasions, may even lead the software to expose sensitive information
or compromise the state of the system.

It is important for software developers to understand the importance of
careful input sanitisation, what it means and what is the extent of the
danger when it is done incorrectly.

This experiment aims to demonstrate and explain some of the most common
attacks which target web applications vulnerable to malicious input data.


Aims and Objectives
___________________

The objective of this experiment is to:

* Understand the importance of input data sanitisation
* Appreciate the extent of the risk of inadequately sanitised input data being processed by a web application
* Understand the process of XSS attacks (identity theft via session cookie) in web applications.


Prerequisites, Equipment and Software
_____________________________________

A general knowledge of procedural programming languages is required to
complete the worksheet. You should also understand the basics of
HTML markup.

Knowledge of the PHP scripting language and Javascript is preferable but
not necessary, as the exercises only require basic string operations
and constructs, and all of the documentation can be easily found
on the internet together with extensive code examples.

The extension exercise requires some knowledge of Javascript
and access to the jQuery documentation available at https://api.jquery.com/.


Ethical Issues
______________

As is common in security teaching, the techniques described here could be
used to attack systems but you must behave responsibly and ethically toward
other people, their data and systems. The writing or use of tools to gain
unauthorised access to systems is a criminal offence.

The Compure Misuse Act (1990) clearly states:

  [...]

  A person is guilty of an offence if—
    (a) he causes a computer to perform any function with intent to secure access to any program or data held in any computer, or to enable any such access to be secured;
    (b) the access he intends to secure, or to enable to be secured, is unauthorised;

  [...]

You can learn more about the Act at http://www.legislation.gov.uk/ukpga/1990/18/contents.
