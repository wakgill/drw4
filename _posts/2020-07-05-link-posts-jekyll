---
layout: post
title: How to create bookmark or link posts in Jekyll
date: 2020-07-05 16:40:03
excerpt: A link post is basically just a post that appears in your regular blog or microblog feed that links to outside content rather than content on your site. That might be a bookmark for an article you want to read later, a link to an piece of content you liked, or something you created yourself.
---

My friend Chuck Grimmett wrote a great article several years ago on [how to create "link" posts in Jekyll.](http://www.cagrimmett.com/til/2016/06/10/external-post-links-jekyll.html)

A link post is basically just a post that appears in your regular blog or microblog feed that links to outside content rather than content on your site. That might be a [bookmark](https://indieweb.org/bookmark) for an article you want to read later, a link to an piece of content you liked, or something you created yourself.

In Chuck's case, he links out to articles he's written on other sites like Quora, Medium or his company blog.

Chuck accomplishes his linkblog by using a custom frontmatter variable and some conditional logic to render the <code>title:</code> variable in files in his <code>_posts</code> folder as an outbound link matching his <code>link:</code> variable. It works great and his [tutorial](http://www.cagrimmett.com/til/2016/06/10/external-post-links-jekyll.html) is, as always, easy to follow.

As I've written before, [there are many ways](https://derykmakgill.github.io/drw/notes/2019/03/01/20190301/) to accomplish the same thing in Jekyll, and after reviewing Chuck's approach, I realised that it wasn't going to work for all the different needs I had on my site for several reasons.

1. I didn't want to clog up my <code>_posts</code> folder with links to external sites. I like to keep different post types more organised. 

2. I wanted to make sure that no permalink page on my site was being rendered and I wasn't sure whether or not Chuck's approach essentially tricked Jekyll but still left a secret page on the site.

3. I wanted more granularity in tagging and categorizations, and keeping things in the same <code>_posts</code> folder seemed limiting.

The solution I settled on involved creating a special Jekyll collection called <code>links</code>.

```
collections:
  links:
    output: false
    permalink: /links/:year/:month/:day/:path/
```

Then I set the <code>output:</code> to <code>false</code> because I don't want a permalink rendered on the site for my link posts right now. In the future, if I want to change that, I can just set it to <code>true</code> and I'll have the permalinks created according the settings I have in my <code>permalink:</code> variable.

I created a layout for my links in my <code>_layouts</code> folder but didn't change anything from the default layout. I like to have seperate layouts for all my post types, even if the layouts are identical, because it gives me easier ability to edit layouts in the future for particular post types if I decide I want to customize it.\

It's at <code>_/layouts/link.html</code>.

```
---
layout: default
---
```

Next I created my <code>_links</code> collection folder in which I'll be posting all my link posts. You can use whatever file structure you want for your link posts in the folder. I like to make mine a copy of the date of the post. For example, a post on 2020-06-16 would be filed as <code>/_links/20200616.md</code>.

The frontmatter I use for the link posts is below. 

```
---
layout: link
date: 2020-06-16 12:36:19
title: The Velocity of Circulation
label: Mises Institute
link: https://mises.org/library/velocity-circulation
---
```

I use the <code>link:</code> variable to tell Jekyll the site my post is linking to. The <code>title:</code> variable is the name of the article or piece of content. The <code>label:</code> variable is the author or site name. The <code>date:</code> variable is the date I posted it can be rendered on the feed page next to the link.

If you want content or commentary on the link you can add content to the file below the frontmatter and we can render it on our feed page. You could also add <code>excerpt:</code> as a variable in the front matter and modify some code to display the excerpt instead of the content.

Next we need a way to display all the link posts on a page in chronological order and the optional content or excerpt. I created a <code>links.html</code> page and wrote the following liquid code for it.

{% raw %}

```
{% assign links = site.links | sort: 'date' | reverse %}
{% for links in links %}

<div class="h-entry note post-stub">
 
 
 <h2 class="post-stub">     <span class="date hidden-xs">{{ links.date | date: "%Y-%m-%d" }}    </span>
  
  <a href="{{ links.url | relative_url }}">
   {{ links.title }} | {{ links.label }} 
   </a> → </h2>

 {% if links.content %}

 
 <p class="p-content"> {{ links.content }}
 </p>
   {% endif %}

 
</div>

{% endfor %}
```
{% endraw %}

We could stop here and have a separate page for our link posts and our regular posts, but one of the advantages of Chuck's original tutorial is that we can display the link posts in the same chronological feed as the other posts on our site. I wanted to the do the same, so I used the <code>side.documents</code> variable instead of the <code>site.links</code> variable and then created a filter based on the layouts I was using.

I wrote a short tutorial about displaying collections AND <code>_posts</code> files on the same feed, which will [walk you through the steps to do this.](https://derykmakgill.github.io/drw/2020/07/04/site-documents.html)

Or you can use the code I've written below for a sample page on my site and adapt it to your needs.

{% raw %}
```

{% assign documents = site.documents | sort: 'date' | reverse %}

{% for document in documents limit:500 %}
  {% if document.layout == "post" or document.layout == "link" %}

<div class="post-stub">
{% if document.layout == "post" %}
<h2>
      <span class="date hidden-xs">{{ document.date | date: "%Y-%m-%d" }}    </span>
             <span class="title">   <a href="{{ document.url | relative_url }}">{{ document.title }} </a>
         </span>
        </h2>
       
    <p class="p-content"> {{ document.excerpt  }} </p>    
  

  
    {% elsif document.layout == "link" %}

<h2>
      <span class="date hidden-xs">{{ document.date | date: "%Y-%m-%d" }}    </span>

<span class="title">   <a href="{{ document.link | relative_url }}"> {{ document.title }} | {{ document.site }} </a>→
         </span>  </h2>
       
        <p class="p-content"> 
   {{ document.content | truncate: 445 }}
 </p>
      {% endif %}  

</div>
  
           
         
        
  {% endif %}   
{% endfor %}

```
{% endraw %}

Using that rough liquid code, you can display both your blog posts in your Jekyll <code>_posts</code> folder and your link collection posts on the same page in chronological order.
