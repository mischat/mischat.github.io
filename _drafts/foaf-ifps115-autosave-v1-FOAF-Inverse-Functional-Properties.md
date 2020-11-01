---
id: 120
title: FOAF Inverse Functional Properties
date: 2011-05-14T23:17:33+01:00
author: Mischa
layout: revision
guid: http://mmt.me.uk/blog/2009/09/08/115-autosave/
permalink: /2011/05/14/115-autosave-v1/
---
These are the  [Inverse Functional Properties](http://esw.w3.org/topic/InverseFunctionalProperty) of the [FOAF ontology](http://xmlns.com/foaf/0.1/), as per 07/09/2009 :

<pre class="brush:php">4store&gt;select * where { graph &lt;http://xmlns.com/foaf/0.1/&gt; {?a &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#type&gt; &lt;http://www.w3.org/2002/07/owl#InverseFunctionalProperty&gt;}}#EOQ
</pre>

`<br />
?a<br />
<http://xmlns.com/foaf/0.1/homepage><br />
<http://xmlns.com/foaf/0.1/mbox_sha1sum><br />
<http://xmlns.com/foaf/0.1/jabberID><br />
<http://xmlns.com/foaf/0.1/isPrimaryTopicOf><br />
<http://xmlns.com/foaf/0.1/icqChatID><br />
<http://xmlns.com/foaf/0.1/weblog><br />
<http://xmlns.com/foaf/0.1/mbox><br />
<http://xmlns.com/foaf/0.1/aimChatID><br />
<http://xmlns.com/foaf/0.1/msnChatID><br />
<http://xmlns.com/foaf/0.1/yahooChatID><br />
`  
I was wondering what happen to [foaf:openId](http://xmlns.com/foaf/0.1/openID) ? Does anyone know ?