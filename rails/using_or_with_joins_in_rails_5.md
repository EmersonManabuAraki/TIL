# Using `or` with `joins` in Rails 5.x

Before we have to prepare the model:

```ruby
class Anime < ApplicationRecord
  has_many :characters
end
```

```ruby
class Character < ApplicationRecord
  belongs_to :anime
  
  enum gender: { male: 1, female: 2 }
end
```

When you do a joins(INNER JOIN) like this example below:

```ruby
Character
  .joins(:anime)
  .merge(Anime.where(title: 'One Piece'))
  .or(Character.where(gender: :male))
```

It will cause the next error:

```
ArgumentError: Relation passed to #or must be structurally compatible. Imcompatible values: [:joins]
```

So you have to fix your code to:

```ruby
relation = Character.joins(:anime)
relation
  .merge(Anime.where(title: 'One Piece'))
  .or(relation.where(gender: :male))
```
