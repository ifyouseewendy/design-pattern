## Adapter

[Specification](http://blog.ifyouseewendy.com/blog/2014/10/17/design-patterns-in-ruby/#the-adapter)

Uniform the interface.

**Class Diagram**

![adapter](/images/adapter.png)

**Demo**

```ruby
Person = Struct.new(:name, :age, :gender)

class SearchEngine
  def query
    p = Person.new('wendi', 20, 'male')
    {
      name:   p.name,
      age:    p.age,
      gender: p.gender
    }
  end
end

class Google < SearchEngine
  def query
    p = Person.new('wendi', 20, 'male')
    {
      name:   p.name,
      age:    p.age,
      gender: p.gender
    }
  end
end

class Bing < SearchEngine
  def query
    p = Person.new('wendi', 20, 'male')
    [p.name, p.age, p.gender]
  end
end

class BingAdapter < SearchEngine
  def query
    res = Bing.new.query
    {
      name:   res[0],
      age:    res[1],
      gender: res[2]
    }
  end
end

google = Google.new
puts "--> Google returns"
p google.query

bing = Bing.new
puts "--> Bing returns"
p bing.query

puts "--> BingAdapter returns"
bing = BingAdapter.new
p bing.query

# --> Google returns
# {:name=>"wendi", :age=>20, :gender=>"male"}
# --> Bing returns
# ["wendi", 20, "male"]
# --> BingAdapter returns
# {:name=>"wendi", :age=>20, :gender=>"male"}
```
