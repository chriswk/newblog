---
layout: post
title: Creating archetypes  for Maven
author: chriswk
published: true
date: 2010-09-14T13:53:12+0200
tags: [archetype, coding, hints, maven ]
categories: [coding]

---

<p>I wanted to create an archetype to simplify maven project creation in-house.<br />
Wanted a couple of extra properties to be checked so updated the<br />
{% highlight bash %}
src/main/resources/META-INF/archetype-metadata.xml
{% endhighlight %}
To include the</p>
<p>
{% highlight xml %}
 <requiredProperties>
	<requiredProperty key="javaVersion"></requiredProperty>
	<requiredProperty key="customer"></requiredProperty>
	<requiredProperty key="projectName"></requiredProperty>
     </requiredProperties>
{% endhighlight %}
</p>
<p>We use a git project policy where the connection is [gitdetails]:[customer]/[projectname].git<br />
This failed to build several times complaining about missing required properties in the test.</p>
<p>Turns out the archetype project when you create a new archetype project
configures a test in src/test for you, and the</p>
<p>
{% highlight bash %}
src/test/resources/projects/basic/archetype.properties
{% endhighlight %}
</p>
<p>needs to be updated with your added requiredProperties otherwise your build of the archetype will fail with a</p>
<p>
{% highlight bash %}
[INFO] Test basic failed
[Ljava.lang.StackTraceElement;@66200db9
org.apache.maven.archetype.exception.ArchetypeNotConfigured: Archetype no.ovitas.archetypes:jar-archetype:1.1.1-SNAPSHOT is not configured
	Property projectName is missing.
{% endhighlight %}
</p>
<p>Give your required properties a value in the archetype.properties file, and everything is fine again.</p>
