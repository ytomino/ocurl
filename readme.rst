This is my fork of ocurl.
 Yuta Tomino

About ocurl
===========

The OCaml Curl Library (ocurl) is an interface library for the programming
language OCaml to the networking library libcurl_.

The official is `<http://sourceforge.net/projects/ocurl/>`_.

The upstream of this fork is `<https://github.com/ygrek/ocurl>`_.

.. _libcurl: http://curl.haxx.se/libcurl/

About this branch
=================

- The truth is that the configure script of ocurl is unnecessary at all.
  New config.h written with LIBCURL_VERSION_NUM is added.
- The souce files has been moved into ``source`` directory.
- I don't like omake, findlib, Oasis and OPAM.
  The files for them were deleted to be clean.
