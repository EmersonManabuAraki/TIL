# How to solve `singleton can't be dumped`

When you do caching sometimes you receive `singleton can't be dumped` error.

That ocurres because you are using a singleton object or specific methods,
so you have to use `dup` method to copy and you will be able to dump.

```ruby

user = GitHub.user('my_user')
Rails.cache.write('my_user_cache', user.dup)

```
