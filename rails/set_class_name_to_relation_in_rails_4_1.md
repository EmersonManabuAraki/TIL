# Set class name to relation in Rails 4.1

Whenever you want to set class_name to relationship in Rails 4.1,
you should put the class name in String

Instead of:

```ruby
class Room
  has_many :windows, class_name: Window
end
```

Should:

```ruby
class Room
  has_many :windows, class_name: 'Window'
end
```
