.. index:: pair: XSLT; post-processing

XSLT Post-Processing
====================

Dydra's query engine integrates an XSLT processor pipeline to enable
server-side post-processing of SPARQL query results based on a user-supplied
XSLT stylesheet.

This features is currently supported for the RDF/XML output of ``CONSTRUCT``
and ``DESCRIBE`` queries.

.. todo:: To be detailed.

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
