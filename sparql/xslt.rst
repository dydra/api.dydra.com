.. index:: pair: XSLT; post-processing
.. index:: standards; XPath 2.0
.. index:: standards; XSLT 2.0

XSLT Post-Processing
====================

Dydra's query engine integrates an XSLT 2.0 processor pipeline to enable
server-side post-processing of SPARQL query results based on a user-supplied
XSLT stylesheet.

This feature is currently supported for the RDF/XML output of ``CONSTRUCT``
and ``DESCRIBE`` queries.

Activation Parameter
--------------------

XSLT post-processing is activated by including an ``xsl-stylesheet`` URL
parameter in the :doc:`SPARQL protocol <index>` request. The value of this
parameter must be the URL of the XSLT stylesheet to apply to the RDF/XML
output of the SPARQL query.

Execution Pipeline
------------------

When the query processor receives a SPARQL protocol request that includes a
``xsl-stylesheet`` parameter, it initiates a concurrent HTTP request to
fetch the XSLT stylesheet from the specified URL at the same time as it
begins processing the SPARQL query itself. This means that the stylesheet is
usually available by the time the query results begin streaming out of the
query processor, and can thus be directly applied to those results.

SPARQL Views
------------

XSLT post-processing is also supported for SPARQL views, in a similar
manner. Please refer to the :doc:`../views/index` chapter for particulars.

Known Caveats
-------------

Dydra's XSLT implementation is based on the `XQilla
<http://xqilla.sourceforge.net/>`__ XSLT processor library. While XQilla
supports much of XSLT 2.0 and XPath 2.0, it does have a number of significant `known
limitations <http://xqilla.sourceforge.net/XSLT2>`__ to take into account.

Missing Features
^^^^^^^^^^^^^^^^

The following XSLT 2.0 features are not supported at this time:

* ``xsl:apply-imports``
* ``xsl:attribute-set``
* ``xsl:character-map``
* ``xsl:decimal-format``
* ``xsl:fallback``
* ``xsl:for-each-group``
* ``xsl:import``
* ``xsl:import-schema``
* ``xsl:include``
* ``xsl:key``
* ``xsl:message``
* ``xsl:namespace-alias``
* ``xsl:next-match``
* ``xsl:number``
* ``xsl:output``
* ``xsl:output-character``
* ``xsl:perform-sort``
* ``xsl:preserve-space``
* ``xsl:result-document``
* ``xsl:sort``
* ``xsl:strip-space``
* ``@validation`` & ``@type``
* ``@priority``
