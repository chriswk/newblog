Been using mutt to read crontab status reports, but as long as everything works ok, the interest for the status mails is rather low. This leads to these filling up my mail box.

Found a quick way to delete all mail
<pre><code class="bash">
SHIFT+D (Delete all files matching)
~s (subject matching)
.* (match everything)
{% endhighlight %}
</code></pre>
Worked fine :)
