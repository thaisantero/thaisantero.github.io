---
layout: post
title:  "Using ActiveModel translation with i18n in PORO"
date:   2023-02-02 10:00:00 -0300
categories: coding rails
---

Coding the API project that I talked about in the last post
I wanted to translate the `Bmi` attributes in the invalid token 
message error to portuguese.

So I searched how to use `i18n` to translate PORO attributes.

And found that I could use [`ActiveModel::Translation`]
because it integrates the object and Rails internationalization (i18n) framework.

To do so I implemented this line in my code:

{% highlight ruby %}
class Bmi
  extend ActiveModel::Translation

{% endhighlight %}

Then, I created the `yml` file `bmi.yml` with
the following configuration:

{% highlight ruby %}
pt-BR:
  activemodel:
      attributes:
        imc:
          height: Altura
          weight: Peso
{% endhighlight %}

This configuration is very similar that the [translation using `ActiveRecord`], 
just replace the name `activerecord` with `activemodel`.

The project repo that I used this: [thaisantero/imc-calculator]

[`ActiveModel::Translation`]: https://api.rubyonrails.org/classes/ActiveModel/Translation.html
[translation using `ActiveRecord`]: https://guides.rubyonrails.org/i18n.html#translations-for-active-record-models