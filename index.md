---
layout: default
---
## Jekyll categories

Jekyll's posts can have **category** and **categories** variables.

They are different, but they sometimes interfere with each other. So, it can be tricky to play with.

### Setting "categories" and "category"

#### From posts front matter

**categories** variable is an array it can be set like this in posts front matter :

``` yaml
---
categories: [ frontCategories1, frontCategories2 ]
# or
categories:
 - frontCategories1
 - frontCategories2
---
```

**category** variable can be a string, an integer or an array it can be set like this in posts front matter :

``` yaml
---
category: [ frontCategory1, frontCategory2 ] # array
category: frontCategory1                     # string
category: 123                                # integer
 ---
```

**Notes** :

 - Any **category** is added to **categories** array.

 - If **category** is an array, it is merged to **categories**.

 - If **category** is an integer or a string, it is merged to **categories** as a string.


#### From containing folder path

Placing a post in a `_posts/pathCategory0` folder will result in nothing.

Placing a post in a `pathCategory1/_posts` folder will result in the attribution of a `pathCategory1` **categories**, merged to **categories** array

Placing a post in a `pathCategory1/pathCategory2/_posts` folder will result in the attribution of **folderCategory1** and **folderCategory1** **categories**, merged to **categories** array

#### From default configuration

Setting up this defaults rules in `config.yml`

{% highlight yaml %}
defaults:
  -
    scope:
      path: "_posts/default" # for all posts in _post/default
      type: "posts"
    values:
      category: "defaultCategory"
      categories: ["defaultCategories1", "defaultCategories2"]
{% endhighlight %}

Posts present in `_posts/default` folder will have :

 - a default *category* set to `defaultCategory`
 - `defaultCategories1` and `defaultCategories2` added to **categories** array

**Note** :

 - if you set a **category** in front matter, it will override `defaultCategory` value. And this defaultCategory will not be present in **categories** array.

 - any default **categories** is merged to posts **categories** array.

### Listing

{% assign sortedPosts = site.posts | sort:"title" %}
{% for post in sortedPosts %}
<h2><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.path }}</h2>
<p>category : {{ post.category | inspect }}</p>
<p>categories : {% if post.categories %}{{ post.categories | join: ", " }}{% endif %}</p>
{% endfor %}

### Listing by category

{% for c in site.categories %}

#### {{ c[0] }}

post count  {{ c[1] | size }}

{% for p in c[1] %}

post title : {{ p.title }}

{% comment %}
post previous : {{ p.previous | inspect }}
{% endcomment %}
post previous title : {{ p.previous.title | inspect }}

{% endfor %}

{% endfor %}



