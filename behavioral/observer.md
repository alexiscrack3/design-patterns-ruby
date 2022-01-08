# Observer

The observer pattern is used to allow an object to publish changes to its state. Other objects subscribe to be immediately notified of any changes.

## Example

```ruby
require "securerandom"

module Observable
  attr_accessor :observers

  def attach=(observer)
    raise "Not implemented"
  end

  def detach=(observer)
    raise "Not implemented"
  end

  def notify
    raise "Not implemented"
  end
end

class Product
  include Observable

  attr_accessor :id

  def initialize
    @observers = []
    @id = SecureRandom.uuid
  end

  def in_stock?
    @in_stock
  end

  def in_stock=(in_stock)
    @in_stock = in_stock
    notify
  end

  def attach(observer)
    @observers.push(observer)
  end

  def deattach(observer)
    index = @observers.index { |x| x == observer }
    if (index != -1)
      @observers.delete_at(index)
    end
  end

  def notify
    @observers.each do |observer|
      observer.get_notification(@in_stock)
    end
  end
end

module Observer
  def get_notification(in_stock)
    raise "Not implemented"
  end
end

class User
  include Observer

  def get_notification(in_stock)
    puts "Is product available? #{in_stock}"
  end
end
```

### Usage

```ruby
foo = User.new
bar = User.new

shorts = Product.new
shorts.attach(foo)
shorts.attach(bar)

shorts.in_stock = true
```

### Output

```text
Is product available? true
Is product available? true
```
