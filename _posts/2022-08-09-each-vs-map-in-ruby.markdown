---
layout: post
title:  "Each vs Map"
date:   2022-08-09 16:20:41 -0300
categories: coding ruby
---
When I was beginning to study Ruby it was a little confusing for me to distinct 'each' and 'map'.
I even read articles about it more than one time.
When I used them in diferente situations I could understand better, and I'd hope I can explain to 
someone that is confused like I was.

The main difference that you can find in any article about it is that 'each' simply interates over a 
collection of values, **NOT** changing the origin array. So, it's easy to think now that 'map' not only 
interates a collection of values but returns a new array by chaging each array element.

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

However, I kept asking myself **WHEN** is better to use 'each' if in my scripts I want to return a
different array or string. So, I realized that sometimes you want to create another array but 
with a different length by accessing 'each' element of the collection, in this case is better
to use 'each'.

Example:

{% highlight ruby %}
string_down = ''
string = 'BanAAna'
string.chars.each do |letter|
  string_down << letter if letter == letter.downcase
end
puts name
#=> "anna"
{% endhighlight %}

If I did this with map, it would return an array with the 'string' length:

{% highlight ruby %}
string = 'BanAAna'
string_down = string.chars.map do |letter|
   letter if letter == letter.downcase
end
puts name
#=> [nil, "a", "n", nil, nil, "n", "a"]
{% endhighlight %}

**Obs.: To use 'each' or 'map' to access each letter of string it's necessary to put '.chars' first!** 

[Array documentation](https://ruby-doc.org/core-2.7.0/Array.html)