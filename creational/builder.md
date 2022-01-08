# Builder

The builder pattern is used to create complex objects with constituent parts that must be created in the same order or using a specific algorithm. An external class controls the construction algorithm.

## Example

```ruby
class Shop
  def build(builder)
    builder.build
  end
end

module VehicleBuilder
  attr_reader :frame
  attr_reader :engine
  attr_reader :wheels
  attr_reader :doors

  def frame=(frame)
    raise "Not implemented"
  end

  def engine=(engine)
    raise "Not implemented"
  end

  def wheels=(wheels)
    raise "Not implemented"
  end

  def doors=(doors)
    raise "Not implemented"
  end

  def build
    raise "Not implemented"
  end
end

class CarBuilder
  include VehicleBuilder

  def frame(frame)
    @frame = frame
    return self
  end

  def engine(engine)
    @engine = engine
    return self
  end

  def wheels(wheels)
    @wheels = wheels
    return self
  end

  def doors(doors)
    @doors = doors
    return self
  end

  def build
    return Vehicle.new(@frame || "", @engine || "", @wheels || 0, @doors || 0)
  end
end

class Vehicle
  def initialize(frame, engine, wheels, doors)
    @frame = frame
    @engine = engine
    @wheels = wheels
    @doors = doors
  end
end
```

### Usage

```ruby
car = CarBuilder.new
  .frame("Frame")
  .engine("Engine")
  .wheels(4)
  .doors(4)
  .build
puts car.inspect
```

### Output

```text
#<Vehicle:0x00007fa8e382feb8 @frame="Frame", @engine="Engine", @wheels=4, @doors=4>
```
