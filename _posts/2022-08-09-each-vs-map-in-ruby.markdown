---
layout: post
title:  "Each vs Map"
date:   2022-08-09 16:20:41 -0300
categories: coding ruby
---
When I began to study Ruby, it was a little confusing for me to distinguish [`each`] and [`map`] . 
I even read articles about it more than one time. Using them in different situations helped me 
understand better, and I’d hope I can explain them to someone that is confused as I was.

The main difference that you can find in any article about it is that `each` iterates over a collection
 of values, NOT changing the origin array. So, it’s easy to think that `map` not only iterates over
  a collection of values but also returns a new array containing the return of each iteration.

Example:

{% highlight ruby %}
array = [2, 4, 6, 8]
array.each { |element| element / 2 }
#=> [2, 4, 6, 8] 
{% endhighlight %}

{% highlight ruby %}
array = [2, 4, 6, 8]
array.map { |element| element / 2 }
#=> [1, 2, 3, 4]
{% endhighlight %}

However, I kept asking myself **WHEN** is better to use 'each'. I realized that sometimes you're not
concerned about the iteration return and don't want to allocate memory for it, so in these cases is 
better to use `each`. 

[Array documentation](https://ruby-doc.org/core-2.7.0/Array.html)

[`each`](https://ruby-doc.org/core-2.7.0/Array.html#method-i-each)
[`map`](https://ruby-doc.org/core-2.7.0/Array.html#method-i-map)