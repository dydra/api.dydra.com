.. index:: pair: SPARQL; revisioning

Revisioning Support
===================

Revision Identifiers
--------------------

Repository revisions are identified by unique :abbr:`UUIDs (Universally
unique identifiers)`. The revision UUID is automatically assigned by the
system when a transaction is committed.

Revision Designators
--------------------

Repository revisions can also be designated by other means.
Currently supported are the following types of designators:

=============================== ================================================
Designator Syntax               Example of Designator
=============================== ================================================
``HEAD``                        ``HEAD``
``HEAD~``                       ``HEAD~``
``HEAD~<n>``                    ``HEAD~2``
``<uuid>~``                     ``4ed401c3-7c39-46c3-9254-120dbb6000f6~``
``<uuid>~<n>``                  ``4ed401c3-7c39-46c3-9254-120dbb6000f6~3``
``T+<timestamp>Z``              ``T+1454056750Z``
``<y>-<m>-<d>T<h>:<M>:<s>Z``    ``2016-01-29T08:39:10Z``
=============================== ================================================

Tilde Designators
^^^^^^^^^^^^^^^^^

The special designator ``HEAD`` denotes the current repository revision when
the transaction was begun.

It is possible to specify previous revisions relative to the current
``HEAD`` by using the syntax ``HEAD~<n>``, where ``<n>`` is an integer
specifying how many ancestors of the current revision will be traversed.

If ``<n>`` is omitted, it defaults to the integer 1--that is, ``HEAD~`` is
exactly equivalent to ``HEAD~1``, both which designate the parent (i.e.,
previous) revision of the current revision.

As depicted in the previous table, tilde syntax can also be used with
specific revision UUIDs instead of ``HEAD``.

Timestamp Designators
^^^^^^^^^^^^^^^^^^^^^

The designator syntax ``T+<timestamp>Z`` denotes the repository revision (if
any) at ``<timestamp>`` seconds after the `Unix epoch
<https://en.wikipedia.org/wiki/Unix_time>`__ (1970-01-01T00:00:00Z). The
only supported timezone specifier is ``Z``, standing for "Zulu time", so
make sure the timestamp is specified in `UTC
<https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`__.

Timestamps can also be given in `ISO 8601
<https://en.wikipedia.org/wiki/ISO_8601>`__ (aka RFC 3339) syntax; that is,
equivalently to ``xsd:dateTime`` literal syntax. Timezones can be given
either as ``Z`` or as a UTC offset using the standard ``+02:00`` and
``-09:00`` syntax.

See Also
--------

See also the blog post `Repository Revision History
<http://blog.dydra.com/2015/09/02/revision-history>`__.
