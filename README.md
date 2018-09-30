### bulk_insert
---
https://github.com/jamis/bulk_insert

```
gem 'bulk_insert'
```

```ruby
class Book < ActiveRecord::Base
end
book_attrs = ...
Book.bulk_insert do |worker|
  book_attrs.each do |attrs|
    worker.add(attrs)
  end
end

book_attrs = ...
Book.bulk_insert values: book_attrs

Book.bulk_insert(:title, :author) do |worker|
  worker.add["...", "..."]
  worker.add title: "...", author: "..."
end

Book.bulk_insert() do |worker|
  worker.add ["...", "...", Time.now, Time.now]
  worker.add ["...", "..."]
end

# create_table :books do |t|
#   t.string "medium", default: "paper"
# end
Book.bulk_insert(:title, :author, :medium) do |worker|
  worker.add title: "...", author: "..."
end
Book.first.medium # => "paper"

Book.bulk_insert do |work|
  worker.add(...)
  worker.add(...)
  worker.save!
  worker.add(...)
end


Book.bulk_insert() do |worker|
end
Book.bulk_insert do |worker|
  worker.set_size = 100
end

destination_columns = [:title, :author]
Book.bulk_insert(*destination_columns, igonre: true) do |worker|
  worker.add(...)
  worker.add(...)
end

# mysql
destination_column = [:title, :author]
Book.bulk_insert(*destination_columns, update_duplicates: true) do |worker|
  worker.add(...)
  worker.add(...)
end

#psgl
worker = Book.bulk_insert(*destination_columns, return_primary_keys: true) do
|worker|
  worker.add(...)
  worker.add(...)
end
worker.result_sets



```

