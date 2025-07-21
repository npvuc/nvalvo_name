

---

# Basic_Document_Manipulation_Using_the_DOM_and_AOM

# Basic Document Manipulation Using the DOM and AOM

This chapter contains a series of brief examples demonstrating basic techniques for manipulating documents and content using the DOM and AOM. The examples cover opening, closing, and saving documents; traversing document trees; inserting text; and locating, selecting, cutting, and pasting content in and between documents.

Most of the sample code in this chapter can be run on the Arbortext XML Docbook sample opened with Arbortext Editor . (Choose File > New , check Sample , select Arbortext XML Docbook V4.0 , and click OK .) Example code that calls openDocument requires access to one or two saved copies of the Arbortext XML Docbook sample.

All of the examples in this chapter are written in JavaScript.



---

# Events

# Events

Arbortext Editor and the Arbortext Publishing Engine implement the W3C DOM Event Model described in the Document Object Model (DOM) Level 2 Events Specification ( www.w3.org/TR/DOM-Level-2-Events ). The DOM Event Model is a generic event system that provides registration of event handlers, describes the flow of events through a tree structure, and defines contextual information for each event.



---

# Line_Numbering_in_Arbortext_Editor_and_Arbortext_Publishing_Engine

# Line Numbering in Arbortext Editor and Arbortext Publishing Engine

Arbortext Editor and the Arbortext Publishing Engine provide a framework for building a custom application to add line numbers to XML documents. Line numbers and page numbers can be displayed in the Editor view as well as composed print output.



---

# Overview_of_Programming_and_Scripting_Techniques

# Overview of Programming and Scripting Techniques

This part of the Programmer's Reference contains information on using Arbortext Editor and the AOM to perform basic and advanced operations. Individual chapters include:

- • Overview — Contains a series of examples demonstrating basic techniques for manipulating documents and content using the DOM and AOM.

- • Overview — Summarizes the DOM Event Model interfaces and the AOM extended event interfaces supported by Arbortext Editor and the Arbortext Publishing Engine .

- • Working with Tables Overview — The AOM contains interfaces that provide access to more than 100 Arbortext Editor table functions. This chapter provides several examples that illustrate the basics of inserting and manipulating tables using the interfaces.

- • Overview — XSL composition refers to Arbortext Editor 's ability to transform a document using XSL or XSL-FO stylesheets. This chapter describes XSL composition and its components, and provides an example of calling the composition pipeline for an HTML file composition.

- • Line Numbering Overview — You can add line numbers to your document, specifying their format using a custom application. This chapter describes the basic line numbering functionality that is available with a Arbortext distributed document type, and detailed instructions for building your own.



---

# Working_with_Tables

# Working with Tables

The AOM contains interfaces that provide access to more than 100 Arbortext Editor table functions. With these interfaces, you can programmatically create and modify tables in any Arbortext Editor document using Java, JavaScript, VB, or VBScript. The entire Arbortext Editor table object model is exposed through the following set of interfaces:

The following three code samples illustrate the basics of inserting and manipulating tables using these interfaces. The sample code is in JavaScript. The code will also work using the Microsoft JScript Engine with the noted modifications.



---

# Working_with_XSL_Composition

# Working with XSL Composition

XSL composition refers to Arbortext Editor 's ability to transform a document using XSL or XSL-FO stylesheets. XSL composition is defined by a composer. A composer is a configurable processor that transforms a document by passing it through one or more SAX filters in a filter pipeline.

Filters are classes written in Java that process an input data stream into an output data stream. The data to be processed is represented as a series of SAX events.

A pipeline is a sequence of filters. Each filter takes inputs and produces outputs that get passed to the next filter in the pipeline. A running pipeline is a closed system with a well-defined input (the source) and a well-defined output (the sink).

You specify the parameters for a composer in a composer configuration file ( .ccf ). The .ccf file defines composer parameters, including filter resources and the processing sequence.

You can create and edit .ccf files using the DCF Editor in Arbortext Architect ( Edit > CCF ). Several .ccf files are distributed with Arbortext Editor . They are located at Arbortext-path \composer .