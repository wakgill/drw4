---
layout: post
title: Building a Jekyll blog feed with posts AND collections
---

I have several different types of posts on my Jekyll site that could all fit under the "blog" page, but I needed some of them to be 
in their own collection outside of the default <code>_posts</code> collection. 

The problem is, if I use the typical <code>site.posts</code> variable, Jekyll will only display posts in <code>_posts</code> and not in the collections I want displayed on the same page.

I couldn't find a good tutorial on this but by looking through the Jekyll [docs](https://jekyllrb.com/docs/variables/ ) I was able to figure out a good solution for this. Here's the full code if you don't want to read the explanation below.

{% raw %}
```
{% assign documents = site.documents | sort: 'date' | reverse %}

{% for document in documents limit:500 %}
  {% if document.layout == 'post' %}
<div class="post-stub">
       <h2>
      <span class="date hidden-xs">{{ document.date | date: "%Y-%m-%d" }}    </span>
            <span class="title">   <a href="{{ document.url | relative_url }}">{{ document.title }} </a>
         </span> </h2>
       
<p class="p-content"> {{ document.excerpt  }} </p>         
              
 </div> 
  {% endif %}   
  {% endfor %}   
```
{% endraw %}

The code works as follows...

You can use <code>site.documents</code> to render a display of *all* posts and collections on your Jekyll site.

Then you'll need some way to organise the content. If you've got a date set in your collection file frontmatter, you can use a filter to order the documents by date, which looks like <code>assign documents = site.documents | sort: 'date' | reverse </code>.

Here I ran into another problem. I don't actually want all my collections to display with my posts. I only want *some* of them to display. Luckily, we can do that.

It's as simple as creating a filter that meets the parameters you need for the documents you want to display. In my case, I'm using the "post" layout for all the documents I'd want displayed on my blog feed, so 
my code is <code>if document.layout == 'post'</code>.

If you had multiple layouts you were using, you could add all the layouts to the filter, or you could do an exclusion. For example, you could do <code>if document.layout != 'sample'</code>, which would display all documents except those using the 'sample' layout. Or you could add your own custom frontmatter variable like 'group' and do
<code>if document.group == 'blog'</code>.

The thing about Liquid and Jekyll is that there are a ton of ways to accomplish basically the same thing. So far, this works for my site.



