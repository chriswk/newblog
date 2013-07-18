I'm a big fan of Semantic Versioning, and as such I try to write proper
changelogs when I do a new
release. [Visionmedia's git-extras](https://www.github.com/visionmedia/git-extras)
has a nice git alias for creating a markdown formatted History.md file.

Behind the scenes it works git and bash magic.. So for my own memory I'll
note what the alias actually resolves to here.


<pre><code>
#!/bin/sh

CHANGELOG=`ls | egrep 'change|history' -i`
if test "$CHANGELOG" = ""; then CHANGELOG='History.md'; fi
DATE=`date +'%Y-%m-%d'`
HEAD="\nn.n.n / $DATE \n==================\n"

if test "$1" = "--list"; then
  version=`git for-each-ref refs/tags --sort=-authordate --format='%(refname)'  --count=1 | sed 's/^refs\/tags\///'`
  if test -z "$version"; then
    git log --pretty="format:  * %s"
  else
    git log --pretty="format:  * %s" $version..
  fi
else
  tmp="/tmp/changelog"
  echo $HEAD > $tmp
  git-changelog --list >> $tmp
  echo '' >> $tmp
  if [ -f $CHANGELOG ]; then cat $CHANGELOG >> $tmp; fi
  mv $tmp $CHANGELOG
  test -n "$EDITOR" && $EDITOR $CHANGELOG
fi
</code></pre>


Alternately, just install git-extras, and you won't have to remember that script.


