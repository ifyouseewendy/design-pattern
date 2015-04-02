## Decorator

[Specification](http://blog.ifyouseewendy.com/blog/2014/10/17/design-patterns-in-ruby/#the-decorator)

+ Help base class seperate the main responsiblity and decorating logic apart.
+ Works like the Russian dolls.

**Class Diagram**

![decorator](/images/decorator.png)

**Demo**

![pirlo](/images/decorator_eg1.jpg)

```ruby
class Person
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def show
    puts "--> #{name}"
  end
end

class Decorator
  attr_reader :person

  def initialize(person)
    @person = person
  end

  def show
    person.show
  end
end

class RedBlackShirt < Decorator
  def show
    super
    puts "Red Black Shirt"
  end
end

class BlueBlackShirt < Decorator
  def show
    super
    puts "Blue Black Shirt"
  end
end

class WhiteShorts < Decorator
  def show
    super
    puts "White Shorts"
  end
end

class BlackShorts < Decorator
  def show
    super
    puts "Black Shorts"
  end
end

class WhiteShoes < Decorator
  def show
    super
    puts "White Shoes"
  end
end

class BlackShoes < Decorator
  def show
    super
    puts "Black Shoes"
  end
end


pirlo = Person.new('Andrea Pirlo')
WhiteShoes.new( WhiteShorts.new( RedBlackShirt.new(pirlo) ) ).show
BlackShoes.new( BlackShorts.new( BlueBlackShirt.new(pirlo) ) ).show

# --> Andrea Pirlo
# Red Black Shirt
# White Shorts
# White Shoes
# --> Andrea Pirlo
# Blue Black Shirt
# Black Shorts
# Black Shoes
```
