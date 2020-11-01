---
id: 263
title: ECS RDF
date: 2010-08-23T22:17:49+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2010/08/23/262-revision/
permalink: /2010/08/23/262-revision/
---
OMG the RDf looks horrible in ECS eprints repo is horrible, I should write a blog post about it &#8230;

I need to mention how the identifiers are odd &#8230;

what is this rdf:_1 job?  
It looks totally horrible

Check to see if the RDF+XML is the RDF+turtle &#8230; and so on and so forth &#8230; NEed to find time to write this blog article ?±?!!?!?!?!?

This is the page which I was looking at :

http://eprints.ecs.soton.ac.uk/16554/

Should write my blog post on this &#8230;.

`<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554#authors> <http://www.w3.org/1999/02/22-rdf-syntax-ns#_1> <http://eprints.ecs.soton.ac.uk/id/x-person/11200> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/6aadb868f6af7a581b985086216d8d28> <http://purl.org/dc/terms/hasPart> <http://eprints.ecs.soton.ac.uk/id/x-org/def9fe13dd2fa504a828c43b23fb336c> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/6aadb868f6af7a581b985086216d8d28> <http://xmlns.com/foaf/0.1/name> "University of Southampton" .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/6aadb868f6af7a581b985086216d8d28> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://xmlns.com/foaf/0.1/Organization> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/def9fe13dd2fa504a828c43b23fb336c> <http://xmlns.com/foaf/0.1/name> "School of Electronics and Computer Science, University of Southampton" .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/def9fe13dd2fa504a828c43b23fb336c> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://xmlns.com/foaf/0.1/Organization> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-org/def9fe13dd2fa504a828c43b23fb336c> <http://purl.org/dc/terms/isPartOf> <http://eprints.ecs.soton.ac.uk/id/x-org/6aadb868f6af7a581b985086216d8d28> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://purl.org/dc/terms/hasPart> <http://eprints.ecs.soton.ac.uk/16554/4/indexcodes.txt> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://eprints.org/ontology/hasFile> <http://eprints.ecs.soton.ac.uk/16554/4/indexcodes.txt> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://eprints.org/ontology/Document> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://eprints.org/relation/isVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://eprints.org/relation/isIndexCodesVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/25158> <http://eprints.org/relation/isVolatileVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<> <http://www.w3.org/2000/01/rdf-schema#comment> "We are still tweaking the RDF, comments, typos, suggestions etc. to cjg@ecs.soton.ac.uk." .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/title> "Who Controls the Past Controls the Future - Life Annotation in Principle and Practice" .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/ontology/bibo/authorList> <http://eprints.ecs.soton.ac.uk/id/eprint/16554#authors> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://purl.org/ontology/bibo/Thesis> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://eprints.org/ontology/EPrint> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://purl.org/ontology/bibo/Article> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/elements/1.1/hasVersion> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/ontology/bibo/abstract> "The fields of the Semantic Web and Ubiquitous Computing are both relatively new fields within the discipline of Computer Science. Yet both are growing and have begun to overlap as people demand ever-smaller computers with persistent access to the internet. The Semantic Web has the potential to become a global knowledge store duplicating the information on the Web, albeit in a machine-readable form. Such a knowledge base combined with truly ubiquitous systems could provide a great benefit for humans. But what of personal knowledge? Information is generally of more use when linked to other information. Sometimes this information must be kept private, so integrating personal knowledge with the Semantic Web is not desirable. Instead, it should be possible for a computer system to collect and store private knowledge while also being able to augment it with public knowledge from the Web, all without the need for user effort.\r\n\r\nThis thesis begins with a review of both fields, indicating the points at which they overlap. It describes the need for semantic annotation and various processes through which it may be achieved. A method for annotating a human\'s life using a combination of personal data collected using an ubiquitous system and public data freely available on the Semantic Web is suggested and conceptually compared to human memory. Context-aware computing is described along with its potential to annotate the life of a human being and the hypothesis that today\'s technology is able to carry out this task is presented.\r\n\r\nThe work then introduces a portable system for automatically logging contextual data and describes a study which used this system to gather life annotations on one specific individual over the course of two years. The implementation of the system and its use is documented and the data collected is presented and evaluated. Finally the thesis offers the conclusion that one type of contextual data is not enough to answer most questions and that multiple forms of data need to be merged in order to get a useful picture of a person\'s life. The thesis concludes with a brief look into the future of the Semantic Web and how it has the potential to assist in achieving better results in this field of study.\r\n"^^<http://www.w3.org/2001/XMLSchema#string> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/isPartOf> <http://eprints.ecs.soton.ac.uk/id/repository> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/issuer> <http://eprints.ecs.soton.ac.uk/id/x-org/def9fe13dd2fa504a828c43b23fb336c> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/issuer> <http://eprints.ecs.soton.ac.uk/id/x-org/6aadb868f6af7a581b985086216d8d28> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/ontology/bibo/status> <http://purl.org/ontology/bibo/status/unpublished> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://eprints.org/ontology/hasAccepted> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/creator> <http://eprints.ecs.soton.ac.uk/id/x-person/11200> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://purl.org/dc/terms/date> "2008-07" .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://eprints.org/ontology/hasDocument> <http://eprints.ecs.soton.ac.uk/id/document/25158> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://eprints.org/ontology/hasDocument> <http://eprints.ecs.soton.ac.uk/id/document/21212> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://eprints.org/ontology/hasDocument> <http://eprints.ecs.soton.ac.uk/id/document/21211> .<br />
<http://eprints.ecs.soton.ac.uk/id/eprint/16554> <http://eprints.org/ontology/hasDocument> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://purl.org/dc/terms/hasPart> <http://eprints.ecs.soton.ac.uk/16554/2/preview.png> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://eprints.org/ontology/hasFile> <http://eprints.ecs.soton.ac.uk/16554/2/preview.png> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://eprints.org/ontology/Document> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://eprints.org/relation/isVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://eprints.org/relation/ispreviewThumbnailVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21211> <http://eprints.org/relation/isVolatileVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://purl.org/dc/terms/hasPart> <http://eprints.ecs.soton.ac.uk/16554/3/fullsize.png> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://eprints.org/ontology/hasFile> <http://eprints.ecs.soton.ac.uk/16554/3/fullsize.png> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://eprints.org/ontology/Document> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://eprints.org/relation/isVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://eprints.org/relation/isfullsizeThumbnailVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/21212> <http://eprints.org/relation/isVolatileVersionOf> <http://eprints.ecs.soton.ac.uk/id/document/7204> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-person/11200> <http://xmlns.com/foaf/0.1/givenname> "Ashley" .<br />
<http://eprints.ecs.soton.ac.uk/id/x-person/11200> <http://www.w3.org/2002/07/owl#sameAs> <http://id.ecs.soton.ac.uk/person/11200> .<br />
<http://eprints.ecs.soton.ac.uk/id/x-person/11200> <http://xmlns.com/foaf/0.1/family_name> "Smith" .<br />
<http://eprints.ecs.soton.ac.uk/id/x-person/11200> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://xmlns.com/foaf/0.1/Person> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/ontology/hasFile> <http://eprints.ecs.soton.ac.uk/16554/1/thesis.pdf> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasfullsizeThumbnailVersion> <http://eprints.ecs.soton.ac.uk/id/document/21212> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://purl.org/ontology/bibo/Document> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://eprints.org/ontology/Document> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasIndexCodesVersion> <http://eprints.ecs.soton.ac.uk/id/document/25158> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://purl.org/dc/terms/hasPart> <http://eprints.ecs.soton.ac.uk/16554/1/thesis.pdf> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVolatileVersion> <http://eprints.ecs.soton.ac.uk/id/document/25158> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVolatileVersion> <http://eprints.ecs.soton.ac.uk/id/document/21212> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVolatileVersion> <http://eprints.ecs.soton.ac.uk/id/document/21211> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/haspreviewThumbnailVersion> <http://eprints.ecs.soton.ac.uk/id/document/21211> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVersion> <http://eprints.ecs.soton.ac.uk/id/document/25158> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVersion> <http://eprints.ecs.soton.ac.uk/id/document/21212> .<br />
<http://eprints.ecs.soton.ac.uk/id/document/7204> <http://eprints.org/relation/hasVersion> <http://eprints.ecs.soton.ac.uk/id/document/21211> .`