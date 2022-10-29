---
layout: post
title:  "Change Column Name Migration - Part2"
date:   2022-10-25 16:20:41 -0300
categories: coding ruby
---
In the article [Change-Column-Name-Migration-Part1] I talked about creating two migrations
to rename a column name of a model.

However, by studying and coding more, I learned that creating only one migration which renames it is possible. Which looks like this:

```bash
rails g migration change_column_name
```

And generated the following ruby file:

{% highlight ruby %}
class ChangeColumnName < ActiveRecord::Migration
 def change
 end
end
{% endhighlight %}

I had to include this line with the table name, old column name, and new column name that I wanted to rename it for.
So, in the end my migration looked like this:

{% highlight ruby %}
class ChangeColumnName < ActiveRecord::Migration
 def change
  rename_column :warehouses, :codi, :code
 end
end
{% endhighlight %}

OBS.: If needed to change more than one column name you
could repeat this line, like this:

{% highlight ruby %}
rename_column :table_name, :old_column1, :new_column1
rename_column :table_name, :old_column2, :new_column2
...
{% endhighlight %}

But, in this case, is best to use [change_table] that would look like this:

{% highlight ruby %}
class ChangeColumnsNames < ActiveRecord::Migration
 def change
    change_table :table_name do |t|
      t.rename :old_column1, :new_column1
      t.rename :old_column2, :new_column2
      ...
    end
  end
end
{% endhighlight %}

OBS.: Change_table can be used to make different 
changes in one table, like rename, change column type, remove...
[Example]

[Example]: https://guides.rubyonrails.org/active_record_migrations.html#changing-tables
[change_table]: https://api.rubyonrails.org/v7.0.4/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-change_table
[Change-Column-Name-Migration-Part1]: https://thaisantero.github.io/coding/ruby/2022/09/16/change-column-name-migration-pt1.html