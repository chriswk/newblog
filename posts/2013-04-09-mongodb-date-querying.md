Just as a reminder, if you want to delete all Cube entries was not logged at an hour divisible by 4, syntax is
<pre><code class="javascript">
use cube_development;
db.[collection].remote({$where: function () { return object.t.getHours() % 4 != 0}})
</code></pre>

