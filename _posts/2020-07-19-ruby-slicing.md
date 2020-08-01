---
layout: index
title: How Ruby slicing works differently
description: If you come from Python or Javascript, it'll perplex you until you see it.

header_classes_index: nav_link
header_classes_problems: nav_link 
header_classes_recommendations: nav_link 
header_classes_articles: nav_link current_page_header

footer_classes_index: footer_li
footer_classes_problems: footer_li 
footer_classes_recommendations: footer_li
footer_classes_articles: footer_li current_page_footer

link_index: index.html
link_problems: problems.html
link_recommendations: recommendations.html
link_articles: articles.html
---
{::options parse_block_html="true" /}

<section>

# How Ruby slicing works differently

**There's a huge insight in slicing** that took me some time to digest that is helpful to anyone who will learn more than one programming language.

Ruby slices differently from languages like Javascript and Python (and if I remember correctly, C).

In these languages, the sliced object is the original object. If I have `i = "hello"`, the sliced object always has a length of 5 (i.e., with indices from 0 to 4). `e` will always be index 1 regardless of the slicing performed.

Yet in Ruby, the sliced object is affected by the starting index in a slice.

For example, in Python

```
i = "hello"
i[1:4]
ell
```

But in Ruby `i[1,4]` outputs `ello` rather than `ell`.

Why is that? **It seems that Python and Ruby slice different objects based on the starting index in a slicing operation**. 

In the above example, Python sliced `i[1:4]` based on `hello`. In contrast, by having a starting index of 1 in `i[1,4]` Ruby operated on `ello`.

**Example Exercise**

Objective: get the subarray starting at the 3rd and ending in the 7th element in a range of 1 to 10.

1. Use a negative index: pick the 3rd item at the start (`-7` is equivalent to `3`) and include every element up to 7 (end index 4)
```
array = (1..10).to_a
array[-7, 4]
```
Interestingly, it seems like we can't use negative indices to mark an end index in slicing.

2. Use positive indices and length
Without length
~~~
array = (1..10).to_a
array[3, 4]
~~~
With length: we need to do `-6` to compensate for i) the elements from 1-3 and ii) the elements from 8-10.
```ruby
array = (1..10).to_a
array[3, (array.length)-6]
```

</section>