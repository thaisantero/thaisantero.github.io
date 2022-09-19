---
layout: post
title:  "Change Column Name Migration - Part1"
date:   2022-09-16 16:20:41 -0300
categories: coding ruby
---
One thing that I found very useful in Rails is when we are
creating a migration in terminal we can write in a certain [pattern] that the migration have the right format when created. 

I can give one example, I was generating a migration to create a model, but, by a miswriting I created a column with the wrong name and run it. So, I had to change the column name.

If you are starting to learn Rails you can think this is an easy fix:
just go in the migration file, change the column name and run again.
Here you are mistaken!!! Like I was. 
Rails just run a migration once and don't run it again.

So, I had to create two migrations, one to delete and another to create a new column.

To create a migration that delete the column in the model you can use this format:

```bash
rails generate migration RemoveFieldNameFromTable
```

OBS: You can use 'g' for 'generate' in terminal

I used this code line in terminal (codi is the wrong column name):

```bash
rails g migration RemoveCodiFromWarehouse
```

And generated the following ruby file:

{% highlight ruby %}
class RemoveCodigoFromWarehouses < ActiveRecord::Migration[7.0]
  def change
    remove_column :warehouses, :codi, :string
  end
end
{% endhighlight %}

To create a migration that add the column in the model you can use this format:

```bash
rails g migration AddFieldnameToTablename fieldname:fieldtype
```

OBS: If the field type is a string you can just give the fieldname at the end, 
Rails understand the string type as default

I used this code line in terminal:

```bash
rails g migration AddCodeToWarehouse code
```

And generated the following ruby file:

{% highlight ruby %}
class AddCodeToWarehouses < ActiveRecord::Migration[7.0]
  def change
    add_column :warehouses, :code, :string
  end
end
{% endhighlight %}

[pattern]: https://edgeguides.rubyonrails.org/active_record_migrations.html
