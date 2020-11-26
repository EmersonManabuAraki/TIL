# Difference between Hash and Struct

Hash and Struct has several differences like:

1: Hash is dynamical, Struct is static

Hash can refer an element that doesn't exist and add elements afterwards. Structure, on the other, can only handle the elements defined at the beginning.

```ruby
# hash
person = {name: "Emerson", age: 22}
person[:tel] # => nil
person[:sex] = "man" # elements added

# struct
Person = Struct.new(:name, :age)
person = Person.new("Emerson", 22)
person.tel # => NameError: undefined method 'tel'
person.sex = "man" # => NameError: undefined method 'sex='
```

2: Equavalent value is different

Structures are no equivalent as Hash, even if they have exactly the same content.

```ruby
Person = Struct.new(:name, :age)
person = Person.new("Emerson", 22)

Robot = Struct.new(:name, :age)
robot = Robot.new("Emerson", 22)

p person == robot # => false.
```

3: Action of `to_a` is different

The Hash will have the array with key-value pair

```ruby
# hash
person.to_a
=> [[:name, "Emerson"], [:age, 22]]

# struct
person.to_a
=> ["Emerson", 22]
```

4: Struct doesn't need attribute name when you create an instance

```ruby
# hash
person1 = {name: "Emerson", age: 20, most_favorite_anime_ever_seen: "Saki"}
person2 = {name: "Manabu", age: 21, most_favorite_anime_ever_seen: "Kyoukai Senjou no Horizon"}
person3 = {name: "Araki", age: 22, most_favorite_anime_ever_seen: "Isekai wa Smartphone to tomo ni"}

# struct
Person = Struct.new(:name, :age, :most_favorite_anime_ever_seen)
person1 = Person.new("Emerson", 20, "Saki")
person2 = Person.new("Manabu", 21, "Kyoukai Senjou no Horizon")
person3 = Person.new("Ara", 22, "Isekai wa Smartphone to tomo ni")
```
