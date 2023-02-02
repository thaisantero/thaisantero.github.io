---
layout: post
title:  "Validations in PORO"
date:   2023-02-02 10:00:00 -0300
categories: coding rails
---

I was doing a project that returns the IMC value through an API endpoint. 
So I had the pure ruby class IMC, and I wanted to validate the parameters
sent via API. But, how it was a PORO didn't have the `ActiveRecord` inheritance.

Then I found a simple way to validate: using [`ActiveModel::Validations`]. 
[Here] is the article that I read to use it. 

To do this you have to first add the `ActiveModel` to your `Gemfile`. Like this:

{% highlight ruby %}
gem "activemodel", require: "active_model"
{% endhighlight %}

Then run:

```sh
$ bundle install
```

After this you include the `ActiveModel::Validations` module in your ruby class.
Like I did in my API project:

{% highlight ruby %}
class Imc
  include ActiveModel::Validations

  attr_reader :height, :weight

  def initialize(height:, weight:)
    @height = height
    @weight = weight
  end
{% endhighlight %}

`ActiveModel::Validations` provides you with the full standard validation stack that you know from [`ActiveRecord`].
So, I could include the validations that I wanted, like this:

{% highlight ruby %}
class Imc
  include ActiveModel::Validations

  attr_reader :height, :weight

  validates :height, :weight, presence: true
  validates :height, numericality: {greater_than: 0}
  validates :weight, numericality: {greater_than: 0}

  def initialize(height:, weight:)
    @height = height
    @weight = weight
  end
{% endhighlight %}

The project repo that I used this is: [thaisantero/imc-calculator]

[Here]: https://www.twilio.com/blog/2017/06/validate-ruby-objects-with-active-model-validations.html
[`ActiveModel::Validations`]: https://edgeapi.rubyonrails.org/classes/ActiveModel/Validations.html
[`ActiveRecord`]: https://guides.rubyonrails.org/active_record_validations.html
[thaisantero/imc-calculator]: https://github.com/thaisantero/imc-calculator
