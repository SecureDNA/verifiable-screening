<!-- SPDX-License-Identifier: MIT OR Apache-2.0 -->

# Verifiable screening tokens

[![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-informational?style=flat-square)](COPYRIGHT.md)

This repo holds public verifiable screening tokens, for use in later verifying auditable `synthclient` API returns when verifiable screening was requested.

Every time a new token signature is generated, we check it in here; tokens have the Unix epoch time as part of their pathname.

In addition, when each database server acknowledges reloading its configuration to incorporate this token, it appends a single line to `updates.log`.  Each line consists of:
* The Unix epoch timestamp when the database acknowledged the reload
* The domain name of the database server in question
* The Unix epoch timestamp when the token was generated; this is extracted from the pathname of the most-recent signed token

If a server is unavailable or otherwise cannot reload the token promptly, the first timestamp on the line might be arbitrarily delayed compared to the second, but in general, they should match within a few seconds.
