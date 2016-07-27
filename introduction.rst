Introduction
========================================================================

The most prevalent attacks on web applications are achieved by attackers who
misuse the application by 'crafting' input to make the program behave in an
unexpected way.

This experiment aims to demonstrate and explain some of the most common
attacks which target web applications vulnerable to malicious input data.

One significant type of misuse is to add data to a website
that will later be provided to other users and interpreted in their browsers
as a script; this results in an innocent user executing a program which has
been designed by the attacker.

It is important for software developers to understand the importance of
careful input sanitisation, what it means and what is the extent of the
danger when it is done incorrectly.


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
