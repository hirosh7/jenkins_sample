Markup Reference
================
That has a paragraph about a main subject and is set when the '='
is at least the same length of the title itself.

Subject Subtitle
----------------
Subtitles are set with '-' and are required to have the same length
of the subtitle itself, just like titles.

Lists can be unnumbered like:

 * Item Foo
 * Item Bar

Or automatically numbered:

 #. Item 1
 #. Item 2

Inline Markup
-------------
Words can have *emphasis in italics* or be **bold** and you can define
code samples with back quotes, like when you talk about a command: ``sudo``
gives you super user powers!That has a paragraph about a main subject and is set when the '='
is at least the same length of the title itself.

Subject Subtitle
----------------
Subtitles are set with '-' and are required to have the same length
of the subtitle itself, just like titles.

Lists can be unnumbered like:

 * Item Foo
 * Item Bar

Or automatically numbered:

 #. Item 1
 #. Item 2

Inline Markup
-------------
Words can have *emphasis in italics* or be **bold** and you can define
code samples with back quotes, like when you talk about a command: ``sudo``
gives you super user powers!

.. code-block:: python
   :emphasize-lines: 3,5

   def some_function():
       interesting = False
       print 'This line is highlighted.'
       print 'This one is not...'
       print '...but this one is.'

.. code-block:: bash
   :linenos:

   ls -lsa
   docker -x file_name

.. code-block:: bash

   ls -lsa
   docker -x file_name

``sudo``

*sudo*

**sudo**

.. tip:: This is a note admonition.
   This is the second line of the first paragraph.

The following admonition directives have been implemented:

    * attention
    * caution
    * danger
    * error
    * hint
    * important
    * note
    * tip
    * warning

.. figure:: images/ballotBoxBot.jpg
    :figclass: align-center

    figure are like images but with a caption
