---
layout: post
title: Lucene Spellchecking
author: chriswk
published: true
date: 2010-09-10T23:28:28+0200
tags: [lucene, java, spellchecking]
categories: [coding]

---

<p>To run spellchecker against a prebuilt dictionary (the content base) from the command line.</p>
<p>The webapp uses Lucene's improved status methods to figure out whether to use the warmed up searcher, or if we need to release and recreate our searcher.</p>
<p>Below there's some basic Java</p>
<p>
{% highlight java %}
public String[] getSpellingSuggestions(String[] args) {
  String[] results = null;
  ApplicationContext applicationContext = new ClassPathXmlApplicationContext("classpath*:META-INF/spring/*-config.xml");
  SpellCheckingService spellCheck = (SpellCheckingService) applicationContext.getBean("spellCheckingService");
  try {
    results = spellCheck.getSimilarWordsByPopularity(args[1], 10);
  } catch (ParseException parseEx) {
    log.error("Error while parsing: {}", args[1], parseEx);
  }
  return results;
}

{% endhighlight %}
</p>
<p>The SpellCheckingService is an interface which looks like this:<br />

{% highlight java %}
import org.apache.lucene.queryParser.ParseException;
import org.apache.lucene.search.Query;
import org.apache.lucene.store.Directory;

public interface SpellCheckingService {
  public Query getSpellingSuggestion(String queryString, Directory spellIndex, String field) throws ParseException;
  public String[] getSimilarWords(String queryString, Directory spellIndex, int numOfWords) throws ParseException;
  public String[] getSimilarWordsByPopularity(String queryString, Directory spellIndex, int numOfWords) throws ParseException;
  public Query getSpellingSuggestion(String queryString, String field) throws ParseException;
  public String[] getSimilarWords(String queryString, int numOfWords) throws ParseException;
  public String[] getSimilarWordsByPopularity(String queryString, int numOfWords) throws ParseException;
}

{% endhighlight %}

Probably the most interesting method in the implementation (which demonstrates the power of Lucene. I've done nothing here except tell it which dictionary (in this case our content index) to use for suggesting spellings.) is the method which returns an array of suggested words.</p>
<p>
{% highlight java %}
public String[] getSimilarWords(String queryString, Directory spellIndex, int numOfWords) throws ParseException {
  String[] similarWords = null;
  try {
    instantiateSpellChecker(spellIndex);
    if (openChecker.exist(queryString)) {
      similarWords = new String[0];//No suggestion, the word is a correct spelling of something in the index
    } else {
      similarWords = openChecker.suggestSimilar(queryString, numOfWords);
    }
  } catch (IOException ioe) {
    logger.error("IOException when finding similar word", ioe);
    throw new ParseException(ioe.getMessage());
  }
  return similarWords;
}

{% endhighlight %}
</p>
