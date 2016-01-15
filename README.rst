*************
api.dydra.com
*************

This is the source repository for the
`Dydra API documentation <http://api.dydra.com/>`__ website.

All materials herein are released into the
`public domain <https://creativecommons.org/publicdomain/zero/1.0/>`__.

Prerequisites
=============

::

   $ pip install -U sphinx
   $ pip install -U sphinx_bootstrap_theme

Building the Manual
===================

::

   $ make html      # HTML output in .build/html/index.html
   $ make latexpdf  # PDF output in .build/latex/dydra-api.pdf

Publishing the Manual
=====================

::

   $ make clean html publish
