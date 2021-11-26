.. _faq_what_is_proskomma:

########################
FAQ - What is Proskomma?
########################

How does Proskomma compare to other data formats?
=================================================

A short answer might be that Proskomma generates the GraphQL response format. However, Proskomma
is not a format like USFM or OSIS. Proskomma can import several formats, which it converts to an
internal, succinct, binary format. That format can be serialized, but it is not intended to be used
outside of Proskomma.

Proskomma is a Scripture Runtime Engine. In a model-view-controller architecture, Proskomma is a model. It manages
Scripture-related data, and can provide some or all of that data to the view. That data is always formatted as a
GraphQL response, but the 'shape' of that response can vary a lot, depending, on the query, and according to the
needs of the application.

The most fundamental example of this is that canonical text may be chunked up by paragraph, or by verse, or in other,
arbitrary ways. Most Scripture-oriented formats choose either paragraphs or chapter/verse. Both options are extremely
convenient for some use cases, and somewhat awkward for other use cases. An application using Proskomma can choose
a different content structure in each query, regardless of the input format.

Is Proskomma a database?
========================

Yes, in the high-level sense that Proskomma provides a view onto data via a query language.

No, in that it is not designed to handle high levels of concurrency or terabytes of data. Out of the box, Proskomma
does not even persist data between sessions (although there are utilities to implement this).

In use, Proskomma is more like a document-based DBMS such as MongoDB than a table-based DBMS such as MySQL. However,
it provides multiple views of document structure via the GraphQL interface.

Can I use Proskomma without a server?
=====================================

Yes - this is currently the most common way to use Proskomma. The GraphQL interface may be accessed by calling an async
method on the Proskomma instance.

Can I use Proskomma via a server?
=================================

Yes - the Proskomma Node Express project provides proof of concept of this.

Can I use Proskomma with <My Favorite UI Framework>
===================================================

Almost certainly. Most UIs to date have used React, but Proskomma itself is agnostic regarding UI design. The only
requirements are support for modern Javascript and a plan to manage async queries to Proskomma.

Does Proskomma handle verse mapping?
====================================

Yes, via versification files like those used in Paratext.

Does Proskomma handle alignment?
================================

Not specifically, because the Bible-tech world has not agreed on one way to do alignment. However, Proskomma provides
a set of generic tools that have been used to implement alignment.
