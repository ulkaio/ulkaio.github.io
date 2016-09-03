---
layout: docs
title: Data Files
permalink: /datafiles/
---

Example
---
http://example.com
This is an [example link](http://example.com/).

~~Mistaken text.~~

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

Use the `printf()` function.

First Header  | Second Header
------------- | -------------
Content Cell  | Content `Cell`
Content Cell  | Content Cell

Horizontal Rules
Three or more dashes or asterisks:
---

* * *

- - - - 
Manual Line Breaks
End a line with two or more spaces:
Roses are red,   
Violets are blue.


A First Level Header
====================

A Second Level Header
---------------------

Now is the time for all good men to come to
the aid of their country. This is just a
regular paragraph.

The quick brown fox jumped over the lazy
dog's back.

### Header 3

> This is a blockquote.
> 
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote

Some of these words *are emphasized*.
Some of these words _are emphasized also_.

Use two asterisks for **strong emphasis**.
Or, if you prefer, __use two underscores instead__.


List

*   Candy.
*   Gum.
*   Booze.
this:

+   Candy.
+   Gum.
+   Booze.
and this:

-   Candy.
-   Gum.
-   Booze.


Ordered (numbered) lists use regular numbers, followed by periods, as list markers:

1.  Red
2.  Green
3.  Blue

I get 10 times more traffic from [Google][1] than from
[Yahoo][2] or [MSN][3].

[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"

I start my morning with a cup of coffee and
[The New York Times][NY Times].

[ny times]: http://www.nytimes.com/


Inline (titles are optional):

I strongly recommend against using any `<blink>` tags.

I wish SmartyPants used named entities like `&mdash;`
instead of decimal-encoded entites like `&#8212;`.


Find



Find a folder name abc

    find . -type d -name abc

Find filename, exclude permission errors

    find / 2>/dev/null -name nginx.conf

Find with name pattern with time interval

    find . -name 'a.log.*' -mmin -100 -ls
    find . -name '*log*' -print

Find and copy

    sudo find . -name '*log*' -exec cp '{}' . \;

File created within last 5 min

    find . -mmin -5 -ls

Find sort by time

    find . -name "*log*" -printf "%T+\t%p\n" | sort




In addition to the [built-in variables](../variables/) available from Jekyll,
you can specify your own custom data that can be accessed via the [Liquid
templating system](https://wiki.github.com/shopify/liquid/liquid-for-designers).

Jekyll supports loading data from [YAML](http://yaml.org/), [JSON](http://www.json.org/),
and [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) files located in the `_data` directory.
Note that CSV files *must* contain a header row.

This powerful feature allows you to avoid repetition in your templates and to
set site specific options without changing `_config.yml`.

Plugins/themes can also leverage Data Files to set configuration variables.

## The Data Folder

As explained on the [directory structure](../structure/) page, the `_data`
folder is where you can store additional data for Jekyll to use when generating
your site. These files must be YAML, JSON, or CSV files (using either
the `.yml`, `.yaml`, `.json` or `.csv` extension), and they will be
accessible via `site.data`.

## Example: List of members

Here is a basic example of using Data Files to avoid copy-pasting large chunks
of code in your Jekyll templates:

In `_data/members.yml`:

{% highlight yaml %}
- name: Eric Mill
  github: konklone

- name: Parker Moore
  github: parkr

- name: Liu Fengyun
  github: liufengyun
{% endhighlight %}

Or `_data/members.csv`:

{% highlight text %}
name,github
Eric Mill,konklone
Parker Moore,parkr
Liu Fengyun,liufengyun
{% endhighlight %}

This data can be accessed via `site.data.members` (notice that the filename
determines the variable name).

You can now render the list of members in a template:

{% highlight html %}
{% raw %}
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}

## Example: Organizations

Data files can also be placed in sub-folders of the `_data` folder. Each folder
level will be added to a variable's namespace. The example below shows how
GitHub organizations could be defined separately in a file under the `orgs`
folder:

In `_data/orgs/jekyll.yml`:

{% highlight yaml %}
username: jekyll
name: Jekyll
members:
  - name: Tom Preston-Werner
    github: mojombo

  - name: Parker Moore
    github: parkr
{% endhighlight %}

In `_data/orgs/doeorg.yml`:

{% highlight yaml %}
username: doeorg
name: Doe Org
members:
  - name: John Doe
    github: jdoe
{% endhighlight %}

The organizations can then be accessed via `site.data.orgs`, followed by the
file name:

{% highlight html %}
{% raw %}
<ul>
{% for org_hash in site.data.orgs %}
{% assign org = org_hash[1] %}
  <li>
    <a href="https://github.com/{{ org.username }}">
      {{ org.name }}
    </a>
    ({{ org.members | size }} members)
  </li>
{% endfor %}
</ul>
{% endraw %}
{% endhighlight %}

## Example: Accessing a specific author

Pages and posts can also access a specific data item. The example below shows how to access a specific item:

`_data/people.yml`:
{% highlight yaml %}
dave:
    name: David Smith
    twitter: DavidSilvaSmith
{% endhighlight %}

The author can then be specified as a page variable in a post's frontmatter:

{% highlight html %}
{% raw %}
---
title: sample post
author: dave
---

{% assign author = site.data.people[page.author] %}
<a rel="author"
  href="{{ author.twitter }}"
  title="{{ author.name }}">
    {{ author.name }}
</a>

{% endraw %}
{% endhighlight %}
