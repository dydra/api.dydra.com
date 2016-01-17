.. index:: pair: SPARQL; functions

Extension Functions
===================

In addition to the standard SPARQL 1.1 filter functions, the Dydra query
processor also supports several useful extension functions.

The examples employ the following namespace prefix bindings:

+-----------+-------------------------------------------------+
| Prefix    | Base IRI                                        |
+===========+=================================================+
| ``rdf``   | ``http://www.w3.org/1999/02/22-rdf-syntax-ns#`` |
+-----------+-------------------------------------------------+
| ``dydra`` | ``http://dydra.com#``                           |
+-----------+-------------------------------------------------+

----

``dydra:account-name()``
------------------------

This function returns the name of the current query's owning account as a
string value.

``dydra:agent-id()``
--------------------

This function returns the ID of the authenticated agent of the current query
as a string value. If the agent is not authenticated the value is unbound.

``dydra:agent-location()``
--------------------------

This function returns the IP-address location of the authenticated agent of
the current query as a string value. If the agent is not located the value
is unbound.

``dydra:query-uri()``
---------------------

This function returns the IRI of the current query.

``dydra:repository-name()``
---------------------------

This function returns the name of the current query's target repository as a
string value.

``dydra:repository-uri()``
--------------------------

This function returns the URI of the current query's target repository as a
string value.

``dydra:revision-uri()``
--------------------------

This function returns the IRI of the current query's active revision.

``dydra:revision-parent-uri()``
-------------------------------

This function returns the IRI of the current query's active revision's
parent.

``dydra:transaction-uri()``
---------------------------

This function returns the IRI of the current query's active transaction.

``dydra:user-tag()``
--------------------

This function returns the `user query id` tag associated with the current
query as a string value.

``rdf:Seq()``
-------------

This function facilitates the creation of RSS 1.0 feeds using ``CONSTRUCT``
queries. Successive invocations return monotonically increasing integer
values.
