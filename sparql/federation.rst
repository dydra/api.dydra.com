Federation
==========

`Federation
<http://www.w3.org/TR/2012/PR-sparql11-federated-query-20121108/>`__
concerns ways for a query to draw upon diverse data sources and processing
capacity in addition to the immediate dataset and query processor. For
Dydra, its various forms involve an initial query, which is processed by a
first host against an initial repository and a sub-query, which is processed
by a second host against some other repository, with the solutions
incorporated by the first host into the first query's evaluation. The
distinct forms arise due to variations in which hosts play which of the two
roles, which query forms initiate federated processing, and which data
sources are involved.

Federation Request Modes
------------------------

Dydra's production sites support *internal* and *external* federation.
For evaluation accounts, federation is disabled.

Internal federation pertains when the same query processor hosts the
repository to which a sub-query is applied as the host which which executes
the initial query. In this case, the query if executed as a subtask within
the initial host query processor subject to intra-host access and
authorization. External federation pertains when a sub-query is performed
upon request by a remote host processor. In this case, for each such
location, the first processor determines a sparql endpoint, a query request
is made of that endpoint host, and the results are read back and integrated
into the first processor's data-flow. The federation mode none suppresses
federation processing.

The default mode for a query is specified in the initial system
configuration. Each individual query may specify its own mode, subject to
constraints

+--------------------------+-------------------------+--------------------------+
| Mode                     | Effect                  | Permitted Variations     |
+==========================+=========================+==========================+
| ``<urn:dydra:none>``     | Federation is disabled; |                          |
|                          | ``GRAPH`` forms apply   |                          |
|                          | to a repository's named |                          |
|                          | graphs only and any     |                          |
|                          | ``SERVICE`` forms cause |                          |
|                          | an error                |                          |
+--------------------------+-------------------------+--------------------------+
| ``<urn:dydra:internal>`` | Federation is enabled   | ``<urn:dydra:none>``     |
|                          | for references local to |                          |
|                          | the host                |                          |
+--------------------------+-------------------------+--------------------------+
| ``<urn:dydra:external>`` | Federation is enabled   | ``<urn:dydra:none>``,    |
|                          | for both local and      | ``<urn:dydra:internal>`` |
|                          | remote references       |                          |
+--------------------------+-------------------------+--------------------------+

Federation Query Forms
----------------------

`SPARQL 1.1 Federated Query
<http://www.w3.org/TR/sparql11-federated-query/>`__ includes the ``SERVICE``
form, with which a query indicates that a component is to be executed by a
remote host processor. This is explicit federation. SPARQL 1.0, on the other
hand, introduced the possibility to indicate diverse datasets through
``GRAPH`` forms, but the `specification
<http://www.w3.org/TR/rdf-sparql-query/#specifyingDataset>`__ indicates
that, if an IRI is specified in a dataset description, "attempts are made to
obtain an RDF graph associated with the IRI." In other words, it allows just
that the first processor obtain the designated graph and incorporate it into
the local dataset to which it then applies the query. When taken in the
context of the 1.1 federation extension, however, the same results would be
achieved with less data transfer, when the query processor rewrites a
``GRAPH`` form with a remote location into a ``SERVICE`` form and treats it
as in implicit federation request.

Authorization
-------------

When a query specifies either an internal reference to a repository within
another account or a remote repository location, the access must be
authorized. Authorization has two aspects: from the client perspective and
from the service perspective. Each account and each repository allows to
freely specify ``authorized-client-locations``. This takes the form of a
list of regular expressions. A reference from a query is permitted when the
query's initial repository matches one of the regular expressions. This list
is maintained in the account root and managed in the "Authorization" pane of
the account manager ui. Each account and repository system also associates
an additional list of ``authorized-service-locations``, which are drawn from
the system configuration at the time an account or a repository is created.

Examples
--------

Internal Federation
^^^^^^^^^^^^^^^^^^^

If a query enables federation, any ``GRAPH`` forms with a constant IRI name
term which is not present as a named graph in the query repository, but is
local to the query processor host, is executed as a ``SubSelect`` within the
same query processor. References to repositories within the same account are
always permitted, but references to any other repository require
authorization. If either the ``GRAPH`` form name is a variable or the
federation is disabled, then the form denotes a standard
``GroupGraphPattern`` match.

::

   PREFIX federation_mode: <urn:dydra:internal>  # or external
   select *
   where { ?s ?p ?o .
    graph <http://localhost/jhacker/foaf> {
     ?s <http://xmlns.com/foaf/0.1/mbox> ?mbox .
    }
   }

A ``SERVICE`` form which specifies a constant IRI name term, which is local
to the query processor host, behaves similar to the ``GRAPH`` form, above.
It also is executed as a ``SubSelect`` within the same query processor. The
same authorization constraints apply as for implicitly federated ``GRAPH``
forms.

::

   PREFIX federation_mode: <urn:dydra:internal>  # or external
   select *
   where { ?s ?p ?o .
    service <http://localhost/jhacker/foaf> {
     ?s <http://xmlns.com/foaf/0.1/mbox> ?mbox .
    }
   }

External Federation
^^^^^^^^^^^^^^^^^^^

If a query enables external federation, any ``GRAPH`` forms with a constant
IRI name term which is not present as a named graph in the query repository
and is external to the query processor host, is executed as a SPARQL request
to the remote processor. If either the ``GRAPH`` form name is a variable,
then the form denotes a standard ``GroupGraphPattern`` match. All external
requests require authorization to access the respective service.

::

   PREFIX federation_mode: <urn:dydra:external>
   select *
   where { ?s ?p ?o .
    graph <http://w3.org/tbl/foaf.nt> {
     ?s <http://xmlns.com/foaf/0.1/mbox> ?mbox .
    }
   }

A ``SERVICE`` form which specifies a variable IRI name term, which is
external to the query processor host, behaves similar to the ``GRAPH`` form,
above. It also is executed as a SPARQL request to the remote query
processor. All external requests require authorization to access the
respective service.

::

   PREFIX federation_mode: <urn:dydra:external>
   select *
   where { ?s ?p ?o .
    service <http://w3.org/tbl/foaf.nt> {
     ?s <http://xmlns.com/foaf/0.1/mbox> ?mbox .
    }
   }
