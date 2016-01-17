.. index:: ! SPARQL; protocol
.. index:: standards; SPARQL 1.1 Graph Store HTTP Protocol
.. index:: standards; SPARQL 1.1 Protocol
.. index:: standards; SPARQL 1.1 Query
.. index:: standards; SPARQL 1.1 Update

*****************************
SPARQL 1.1 Protocol Interface
*****************************

Every Dydra repository is also a SPARQL endpoint. If you're not familiar
with the SPARQL language, we have an `introduction
<http://docs.dydra.com/sparql>`__.

Your repository's SPARQL endpoint is found by appending ``/sparql`` to the
repository's URL. So a user 'jhacker' who created a repository named 'foaf'
would have a SPARQL endpoint located at http://dydra.com/jhacker/foaf/sparql.
A simple query, which specifies a user identifier and returns a statement
count for the 'jhacker/foaf' repository can be done with ``curl``::

   $ curl -H 'Accept: application/sparql-results+json' \
          -H 'Content-Type: application/sparql-query'  \
          -d 'SELECT COUNT(*) WHERE {?s ?p ?o}'        \
          -X POST http://dydra.com/jhacker/foaf/sparql

::

   {
     "head": {
       "vars": [
         "COUNT1"
       ]
     },
     "results": {
       "bindings": [
         {
           "COUNT1": {
             "type": "literal",
             "value": "8631",
             "datatype": "http://www.w3.org/2001/XMLSchema#integer"
           }
         }
       ]
     }
   }

.. toctree::
   :maxdepth: 2

   auth
   dialect
   federation
   xslt

.. _SPARQL 1.0 Protocol: http://www.w3.org/TR/rdf-sparql-protocol/
.. _SPARQL 1.1 Protocol: http://www.w3.org/TR/sparql11-protocol/
