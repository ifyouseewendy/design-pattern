## Proxy

[Specification](http://blog.ifyouseewendy.com/blog/2014/10/17/design-patterns-in-ruby/#the-proxy)

+ Protection Proxy, provides controll access, and seperates the concerns.
+ Remote Proxy, hides the complexity behind remote procedure calls.
+ Virtual Proxy, delays the execution(creation).

**Class Diagram**

![proxy](/images/proxy.png)

**Demo**

![proxy demo](/images/proxy_eg1.png)

```ruby
require 'forwardable'

class ClientInsideGFW
  def request(hostname)
    puts "--> Requesting #{hostname}"
    puts "    Sorry, GFW blocks you down."
  end

  def request_with_proxy(hostname)
    Proxy.new.request(hostname)
  end
end

class ClientOutsideGFW
  def request(hostname)
    puts "--> Requesting #{hostname} with proxy"
    puts "    Connected, and f*ck GFW."
  end
end

class Proxy
  extend Forwardable

  def initialize
    @client_outside_gfw = ClientOutsideGFW.new
  end

  def_delegator :@client_outside_gfw, :request
end

client = ClientInsideGFW.new
client.request("twitter.com")
client.request_with_proxy("twitter.com")

# --> Requesting twitter.com
#     Sorry, GFW blocks you down.
# --> Requesting twitter.com with proxy
#     Connected, and f*ck GFW.
```
