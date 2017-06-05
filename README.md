# vois
Vocabulary for Interlinked Streams

# Competency Questions:	
* What is the sGraph of this data stream?
* What are the parts of this data stream?
* What is the timestamp of this iGraph?
* By which affluent was this iGraph streamed?
* What are the capabilities of sensors streaming this iGraph?
* What is the process for publishing this datastream ?
* What parts of this data stream is visible?
* What is the sliding policy of this data stream?
---
# VoIS Core 
VoIS Core module is an extension VoID ontology, introducing basic concepts to annotate RDF data streams with meta-data needed to enable answering queries about the streams.

VoIS expresses general meta-data based on Dublin Core, access meta-data and  structural meta-data based on VoID.
4 classes are introduced, main class vois:DataStream represents a sequence of RDF statement with a temporal annotation.

An RDF Stream is represented with 2 named graphs vois:iGraph and vois:sGraph, where an iGraph represents one stream element, while the sGraph contains the descriptions of the iGraphs. An optional named graph, vois:dGraph, that represents the static/slowly changing information about the iGraph (e.g the capabilities of the stream source, status of the sensors, ..., etc ), it is extremely useful in case the stream is constructed by a merging several smaller streams, by applying a given transformation.

# VoIS Windowing 
VoIS Windowing module introduces the concepts of windowed stream and the visible windows of an RDF Stream. It express the types of windows available for RSP engine to access and process.
This module provides a way to define different types of windows and to represent window technical features important for Stream Consumers.

Some of the main classes defined are, "Window" represents a finite subset of RDF elements extracted from stream. Different types of windows are defined, such "Physical", "TimeBased" and "Semantic" windows, where physical, time based are count based windows on RDF elements and time instance respectively, as for Semantic window, it is a dynamic, non-periodic windows that depends on a defined patterns of events.

Each window is associated with a defined vois:Policy describing the sliding criteria of a window, two types of policy are defined, CountingPolicy for Physical and TimeBased windows and SessionPolicy for Semantic windows.

# VoIS Provenance 
VoIS Provenance module represents the process of stream construction and publication. It uses PROV-O to enrich the ontology with needed meta data about how the stream was constructed. 

An example of the possible process can be 'Replay' static dataset, in which the publisher only annotate the RDF elements with  timestamp, or 'Transform' a live stream, in which publisher consume a live stream and apply some operations, for instance annotation of non RDF stream, constructing a swollen RDF stream from other affluent streams by applying a graph operation such as union, intersection,…,etc, or filtering an existing RDF stream using by applying a contentious query . 

PROV-O ontology is used to represent such process, where the published is considered as subclass of prov:Agent and the process is considered as pipeline of prov:Activity that uses different entities ,e.g. static data set,data stream, ...etc) to generate a processed data stream. 


---
# VoIS Inter-modules interactions  
VoIS core define the basic concept of streams and define all general classes to be used and extended  by VoIS Provenance, VoIS Windowing or others modules.

VoIS core can be seen as an extension of VoID ontology to describe a datastream, without taking into consideration any technical details about the publication process of the stream or how stream is accessed/queried, only information about the content of the stream.

VoIS windowing extends the core module to provide details about the dynamics of the stream's windows, and there technical details, as well as, possibility to access previously streamed window that are no more avaialbe for live usage. It is also possible to express details about the windowing specification and behavior.

VoIS Provenance uses Prov-o to enrich vois:DataStream with information about the activities and agents involved in the Streaming process.
