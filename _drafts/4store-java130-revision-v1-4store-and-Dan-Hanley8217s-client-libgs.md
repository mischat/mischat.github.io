---
id: 142
title: '4store and Dan Hanley&#8217;s client libgs'
date: 2009-12-13T21:27:51+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/12/13/130-revision-7/
permalink: /2009/12/13/130-revision-v1/
---
Find below step by step instructions on how to talk to a [4store](http://4store.org/) KB via the [SPARQL-Procotol](http://www.w3.org/TR/rdf-sparql-protocol/) in Java, using [Dan Hanley&#8217;s 4store client libs](http://github.com/danhanley/4store-java-client).

First of all you need to have the following installed :  
4store  
A java compiler (i have [Sun&#8217;s Java SDK 1.6.x](http://java.sun.com/javase/downloads/widget/jdk6.jsp) installed on my laptop)  
[Maven](http://maven.apache.org/) (to compile Dan Hanley&#8217;s 4store client libs). 

I have all of the code needed for this example placed on my site here : <https://mmt.me.uk/blog/examples/4store-java-query-example/> feel free to grab and use it as you wish.

First of all, I should say that I have had to patch the 4store-client-library, as it seems to chomp all of the carriage returns at the end of the lines (&#8220;\n&#8221;). This is fine you are using the [SPARQL-XML-RESULT format](http://www.w3.org/TR/rdf-sparql-XMLres/), by I am a tad lazy and much prefer working with the [tsv](http://en.wikipedia.org/wiki/Delimiter-separated_values) format: tsv requires line breaks.

The git diff of my patch looks like so (and again yes it is a tad dirty) :  
`<br />
diff --git a/src/main/java/uk/co/magus/fourstore/client/Store.java b/src/main/java/uk/co/magus/fourstore/clie<br />
index 6652874..097be43 100644<br />
--- a/src/main/java/uk/co/magus/fourstore/client/Store.java<br />
+++ b/src/main/java/uk/co/magus/fourstore/client/Store.java<br />
@@ -349,7 +349,7 @@ public class Store {<br />
                String response = "";<br />
                String str;<br />
                while (null != ((str = in.readLine()))) {<br />
-                       response += str;<br />
+                       response += str+"\n";<br />
                }<br />
                in.close();<br />
                return response;<br />
~<br />
~<br />
` 

This above [patch](https://mmt.me.uk/blog/examples/4store-java-query-example/patch.txt) allows me to make use of the TSV output as needed. The patch can be grabbed from here : <https://mmt.me.uk/blog/examples/4store-java-query-example/patch.txt>.

Ok, now that I have built the [4store-client.jar](https://mmt.me.uk/blog/examples/4store-java-query-example/4store-client-1.0.jar) file with my patch using the instructions in the [git repo](http://github.com/danhanley/4store-java-client). I create an example RDF file, and some example java code which will query the 4store KB. All the files can be found on my site <https://mmt.me.uk/blog/examples/4store-java-query-example/>.

These are the steps which I have taken to get this little demo up and running :  
**1. Create 4store KB called _lame_**  
`<br />
4s-backend-setup --node 0 --cluster 1 --segments 2 lame<br />
` 

**2. Start _lame_&#8216;s backend (i.e. start the KB)**  
`<br />
4s-backend lame<br />
` 

**3. Import the [example.rdf](https://mmt.me.uk/blog/examples/4store-java-query-example/example.rdf) file into _lame_&#8216;s backend (i.e. start the KB)**  
`<br />
4s-import lame example.rdf<br />
` 

**4. Start HTTPD for the KB named _lame_**  
`<br />
4s-httpd -s -1 lame<br />
` 

**And then I need to compile the [exampleQuery](https://mmt.me.uk/blog/examples/4store-java-query-example/exampleQuery.java) code I knocked together**  
`<br />
javac -cp 4store-client-1.0.jar exampleQuery.java<br />
` 

**Finally, I run the code like so :**  
`<br />
java -cp 4store-client-1.0.jar:. exampleQuery<br />
` 

**Resulting in the following output:**  
`<br />
Am about to query a sparql endpoint<br />
A user name is:"Bob"<br />
A user name is:"Alice"<br />
` 

I hope this helps!