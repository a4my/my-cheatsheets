---
title: Asynchronous JavaScript
category: JavaScript
updated: 2021-06-25
intro: |
  A closer look to Promises / Async-Await/ AJAX /
---

# Asynchronous JS

• Most code is synchronous (executed line by line and each line of code waits for the previous line to finish)

👎 Long-running operations block code execution

• Asynchronous code is executed fter a task that runs in the background finishes. Async is non-blocking and the execution doesn't wait for an async task to finish its work. ie setTimeout()

❗ Callback functions alone and event listeners do NOT make code asynchronous!

# AJAX

Stands for Asynchronous JavaScript And XML.

Allows us to communicate with remote web servers in an asynchronous way. With AJAX calls we can request date from web servers dynamically.

XML is a data format which is no longer used, instead we now use JSON data format.

# API

Stands for Application Programming Interface. Piece of software that can be used by another piece of software in order to allow applications to talk to each other and exchange information.