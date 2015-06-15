<header>
2015-06-11 PREFORMA Suppliers meeting
=====================================
</header>

FARO, Brussels (BE)


## Participants

* MediaArea: Ashley, Jerome, Dave (via Skype)
* VeraPDF: Ed, Carl, Boris
* EasyInnova: Miguel, Robert, Xavi
* Preforma: Bert, Erwin, Hilke & Erik

## Agenda

Goals of the meeting:

* Discuss consensus of the 3 projects' different proposals on interoperability
* Use of schematron as an expression of policy set
* Collaboration possibility for what the schematron will test
* Use and structure of the conformance check registry
* Steps towards the standardization of our target formats

---

# Interoperability document
Bert, Benjamin and Erwin, with input from the project partners, prepared a use case document for the common shell. The requirements doc can be found on: <https://docs.google.com/document/d/1wDY4qDPTYRxjLuFRHq6Fis8frbjm_A8Rhdq9YbJEgKo/edit#>. 

VeraPDF indicated that the second minimal requirement [API] for *2.1* is worrying, as we’ll never have a syntax that allows every parameter. The farther you go down, the more you encounter this.

From the discussion, most questions ensue around use case *2.2 Checking embedded resources*. The main question is whether PREFORMA funds some work on involving external / generic checkers. The response is that a standard API should provide a starting point for developers of other checkers who can in turn look for funding, engage developers, etc.

Use case 2.4 mixes two concepts: both requirements and report should be common for all.
Possible existing formats could be the vocabulary of policy elements from the SCAPE project, which is based on format, or standard PREMIS reporting. VeraPDF could invite a policy expert from SCAPE if useful. MediaArea works closely with Archivematica (as detailed in their design document), who develop a [PolicyRegister](https://www.archivematica.org/wiki/Format_policies) to define policies to characterise different formats to integrate with preseration workflows. VeraPDS indicate an interest in also discussing integration with Archivematica.

Supliers are welcome to discuss the backstory with the technical coordinator of PREFORMA, if there are questions about the nature or level of competition in this phase. The Commission follows closely on the realisation of the project's principles, as it's a new form of project for them.

We discuss whether it makes sens to model the API on the [IIIF](http://www.iiif.org) project. Its API is standard and seems widely used in the image domain.

Indicating the levels of difficulty for realisation, the policy checker might be a good place to start. Most complex is the metadata fixer, which will be distinct per format. 
It was included because it was a requirement from people who needed a checker for TIFF, which has low-level, small problems, but has patent claims to consider. For MKV, fixes are possible but for FFv1 this becomes more difficult. 

Suppliers indicate that the document provides most of the background for the work. All are welcome still to put add comments to the discussion document.

---

# Supplier presentations
Easy Innova presented an overview of its work on interoperablility (see ppt).

EasyInnova indicated that its proposal should be quite easy to implement - the only requirement not taken into account being *2.2 embedded resources*. The conformance checker can ask the shell which the other conformance checkers are. VeraPDF indicated its design was thought up in a similar fashion. Format identification in the shell would work via MIME type or Magic number. MediaArea stressed that it should be able to send binary data instead of the file name direct to the shell server. An important question is whether it can allow memorydump, which is quite essential for the audiovisual aspect.

The GUI was discussed - EasyInnova's GUI is based in Java - and what levels of user expertise should be supported. In EasyInoova's proposal, the GUI has an assistant role - a richer configuration is kept independent. VeraPDF warned about creating a dynamic GUI for new policy documents and wondered whether the effort going into the GUI would be worth it, as it's a rather ambitious goal. It might be more realistic to reuse existing approaches (XML + Schematron).

An agreement is needed on how to configure the policy checker. Idea is to generate a configuration file that can be shared and is as general as possible. Option 1 is to create, option 2 to load an existing policy. 

We agree to go through the Interoperability issues as presented bu EasyInnova (slide #6) and discuss overlaps and work to be done.  We need to define entry points of the resources - defining the exact XML syntax right now is not essential. It’s a two-way process beween the suppliers. Documents will be uploaded to the shared PREFORMA [GitHub account](http://www.github.com/preforma) from where the documents can be further refined.

---

# Six Core topics of interoperability

1. Service discovery
2. Common XML configuration file
    3. Policy checker interoperability
    4. Metadata fixer interoperability
5. Common API
6. Common XML report format   	


## Service Discovery (Service definitions)
There is a common set of necessary elemens that need to be agreed on:
 
- what formats
- what elements to describe
- extensibility around the reporter


VeraPDF is working towards an XML schema for service definitions

MediaArea asked how we create testing conformance on embedded data and fears there will be discrepancy as all making are making different channels. VeraPDF indicates that it goes both ways:

- upstream knowing what you can push out to
- knowing what you push out

With the FFv1 conformance checker however there’s no file format, it's a stream wrapped in other containers. For the AV files it is necessary to be able to process piped data. The same issue exists for PDF, which packs other formats - not a single file type. Validating embedded resources through the shell might not run smoothly - it might be a responsibility for the specific checker to provide plug-in for validation of specific resources.

Identifying file type is a complicated question. Archivematica uses [FIDO](https://www.archivematica.org/wiki/Adding_Format_Identification_Tools), Siegfried, other people browsers. The syntax needs to take that into account

**Actions**

* Syntax is part of EasyInnova's documentation, who will extract a specific document, publish syntax
* Others will extend with revisions, comments



## Common XML configuration file
VeraPDF specified much of this in their technical specs document. EasyInnova also has a proposal ready.

Contains:

* Named policy profile
* Idea of standard service profiles

**Actions**

* Carl & Miguel both to upload syntax

### Policy checker

Discussed the use of Schematron, all in favour. Wellcome Trust has used it in production for exactly the same purposem, which has worked well. 
MediaArea asked a question about the decoding of TIFFs. EasyInnova indicates they only validate, but that the tool needs the flexibility: the grammar should allow content checking. 
VeraPDF will be gathering policy requirements from users in July.

**Actions**

* MediaArea + VeraPDF to upload their preparation doc on policy checking

### Metadata fixer (and reporter)
In itself not particularly difficult, but a major issue for TIFF files, seeing the patent issues. 

**Actions**

* EasyInnova will share their preparatory document.


## Common API
VeraPDF has specified its metadata elements and published them on [Github](https://github.com/verapdf).

Draft API spec from VeraPDF and from EasyInnova. They're basically the same API with a difference in how you call.

Feelings about RESTification? Opportunity to do something elegant with it! Would need to update it to respond to service and resource discovery. 

Using http steams as input data - is supported by all. Shared memory is the only problem, and will be quite complicated, as JAVA runs inside a sandbox / virtual machine. There is currently no scenario for shared memory integration.


## Common XML Report format

We discussed Machine readable vs Human readable reporting formats. In the EasyInnova proposal, a conformance checker would only give a machine-readable format (XML or JSON) while the Shell would be responsable to create a human-readable format. Extra support like localization would be needed, which was considered the only tough issue. Whenever something’s not localized, english becomes default. Shared language packs would be a nice-to-have. The VeraPDF report is human readable in XML format.

All agree to use UTF-8 encoding. Important to foresee enough namespaces. Not all suppliers already have examples ready. 

**Actions**

* Configuration of the reporter 
* Define machine-readable structure of the report


# Remaining use cases
*2.2 Checking embedded resources* is not considered in the current solution and has its own challenges. 
Question is whether this could be postponed until the redesign phase.

# Timeline
A sensible order to tackle the interoperability issues would be:

1. Common XML Report format - implementation checker, policy checker results
    * Need to agree on common structure / schema for the report (top-level part)
2. Agreement on common report structure needed by the end of July
3. Common XML Configuration - Policy checking profiles
4. Common XML Configuration - Metadata fixer (also in profiles? seems simple for PDF)
5. Service discovery
6. Common API 
    * will need a few iterations
    * Sensible in redesign phase

VeraPDF plans its first release in July, so there's a bit of a planning issue with not much action on interoperability possible before, but summer threatening to delay other actions. EasyInnova also indicates that July might be too soon for policy checker

REST API that needs resource added could be figured out before summer

All agree to publish readily available materials on GitHub by 2015-06-15 at the latest and start discussing them asap. Prototypes will be needed by end of September (ideally end of August). 

# Further questions 
## Upcoming meetings

- MediaArea just presentated at EBU workshop: <https://mediaarea.net/Events/2015-06-10_MDN/#/25>
- MediaArea has an IETF working group meeting planned in July (Prague)
- MediaArea will present to the IASA tech committee in September (Paris) in the framework of TC-06
- MediaArea and Sound and Vision to consider presenting at FIAT/IFTA in October (Vienna) (possible with Archivematica)
- MediaArea and Sound and Vision will present to AMIA conference in November (Portland)
- VeraPDF plans to demonstrate at PASIG

One of these venues could possibly serve to have another face-to-face meeting with suppliers before the Stockholm workshop (April 2016).  
**AP** Erwin to discuss possibility of shared events calendar with Claudio 

## Training files
Main needs of training files suppliers would like to receive:

- test files going on github as much as possible
- VeraPDF generates its own controlled examples but would like to receive as much real-world files as possible
- Regional archive in DE allowed testing (300.000 PDF files) only locally - would be interesting for VeraPDF to go local for large test sets

