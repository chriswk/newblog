I work at a company where we use Maven for main build processes, and having a decent archetype to avoid having to setup the common cruft between our projects would help.
This is a documentation of the steps I did to set-up the internal company archetype for framework agnostic webapps (I.e. a maven module with packaging set to war).<br />
Tasks for the archetype
<ul>
<li>Configure logback to have a debug.log written to the ${contextPath}/logs/debug.log.</li>
<li>Set up distribution management section</li>
<li>Set up scm section</li>
<li>Set up JUnit 4.8 dependency</li>
<li>Create a filters subfolder in src/main/filters and src/test/filters</li>
<li>Configure resources plugin to use any filters in src/main/filters folder for filtering</li>
<li>Configure UTF-8 encoding for both resources and compiler</li>
<li>Setup reporting and javadoc creation</li>
</ul>
I'm using maven3 beta 3 for this work
From the<a href="http://maven.apache.org/guides/mini/guide-creating-archetypes.html">documentation</a>:<br />
Use the archetype generation<br />
<pre><code class="bash">
mvn archetype:generate -DgroupId=no.ovitas.archetypes -DartifactId=war-archetype -DarchetypeArtifactId=maven-archetype-archetype<br />
</code></pre>
