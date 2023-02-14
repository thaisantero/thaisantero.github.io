---
layout: post
title:  "Using ActiveModel translation with PORO"
date:   2023-02-13 10:00:00 -0300
categories: coding rails
---

Coding the [API project] that I talked about in [this post], I wanted to translate the Bmi 
attributes to Portuguese in the validation error message.

So I searched how to use `i18n` to translate the attributes of a PORO.

I discovered I could use [`ActiveModel::Translation`] because it integrates
the object and Rails internationalization (i18n) framework.

To do so, I implemented this line in my code:

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

This configuration is very similar to the [translation using `ActiveRecord`], 
replacing the name `activerecord` with `activemodel`.

So, for example, if you create an instance object with the following parameters:

{% highlight ruby %}
bmi = Bmi.new(height: 0, weight: 76)
{% endhighlight %}

Validating the object the message error will be:

{% highlight ruby %}
bmi.valid? #=> false

bmi.errors.full_messages #=> ["Altura deve ser maior que 0"]
{% endhighlight %}

With the BMI attribute translated.

[`ActiveModel::Translation`]: https://api.rubyonrails.org/classes/ActiveModel/Translation.html
[translation using `ActiveRecord`]: https://guides.rubyonrails.org/i18n.html#translations-for-active-record-models
[API project]: https://github.com/thaisantero/imc-calculator
[this post]: https://thaisantero.github.io/coding/rails/2023/02/02/using-activemodel-validations-in-PORO.html