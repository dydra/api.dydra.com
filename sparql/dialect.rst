.. index:: pair: SPARQL; functions
.. index:: pair: SPARQL; semantics
.. index:: pair: SPARQL; syntax

Dydra's SPARQL Dialect
======================

Like all SPARQL implementations, Dydra's has some quirks. Unlike all SPARQL
implementations, our canonical description comprises a `BNF
<http://docs.dydra.com/api/sparql_bnf>`__ and `a set of executable tests
<https://github.com/dydra/sparql-tests>`__, written in `RSpec
<http://rspec.info/>`__.

Features
--------

We're always interested in `your feedback <mailto:support@dydra.com>`__
about our feature set.

SPARQL Versions
---------------

Dydra's SPARQL processor supports SPARQL 1.1. Take a look at our `blog
<http://blog.dydra.com/>`__ for further details.

Blank Node Handling
-------------------

Dydra treats blank node identifiers as canonical. When data is imported,
existing blank node identifiers are saved, and new, canonical blank node
identifiers are created for new nodes. In practice, this is quite useful:
the output of one query can be matched with another.

Normalization
-------------

Dydra is a graph store (as opposed to a document store). We store the
semantic representations of numerics, dates, and times. The result is that
several of these formats do not round-trip. For example, data imported as
``"01"^^XSD.integer`` would be returned as ``"1"^^XSD.integer``. See the
`Dydra reference tests <https://github.com/dydra/sparql-tests>`__ for more
detail.

Short Forms
-----------

We support several query variations as a matter of convenience.

Simplified Aggregates
^^^^^^^^^^^^^^^^^^^^^

Our query processor permits a simplified and abbreviated convenience syntax
for aggregates. For example::

   SELECT count(*) WHERE {?s ?p ?o}

is treated as equivalent to::

   SELECT (count(*) AS ?count1) WHERE {?s ?p ?o}

De-duplicated Projection Variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Our query processor removes duplicate projection variable from SELECT forms.
For example::

   SELECT ?s ?p ?o ?s WHERE {?s ?p ?o}

is treated as equivalent to::

   SELECT ?s ?p ?o WHERE {?s ?p ?o}

The Default Graph
-----------------

The default graphs of the default dataset which available when no explicit
dataset is specified comprises exactly the default graph. That is,
``sd:UnionDefaultGraph``` is *not* a SPARQL endpoint feature.

Undefined Variables
-------------------

The query compiler recognizes undefined variables and treats them as an
error. Where an installation is configured to support request parameters,
such formulations can serve to allow optional evaluation depending on which
parameters are bound. Without that, we observe the results are more likely
unintended empty result sets or missing construct elements. Given which, we
have configured this installation to fail such requests.
