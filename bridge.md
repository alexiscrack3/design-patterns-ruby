# Bridge

The bridge pattern is used to separate the abstract elements of a class from the implementation details, providing the means to replace the implementation details without modifying the abstraction.

## Example

```ruby
module Switch
  attr_accessor :appliance

  def turn_on
    raise "Not implemented"
  end

  def turn_off
    raise "Not implemented"
  end
end

class RemoteControl
  include Switch

  def turn_on
    appliance.turn_on
  end

  def turn_off
    appliance.turn_off
  end
end

module Appliance
  def turn_on
    raise "Not implemented"
  end

  def turn_off
    raise "Not implemented"
  end
end

class Lamp
  include Appliance

  def turn_on
    puts "Turning the lamp on"
  end

  def turn_off
    puts "Turning the lamp off"
  end
end

class TV
  include Appliance

  def turn_on
    puts "Turning the tv on"
  end

  def turn_off
    puts "Turning the tv off"
  end
end
```

## Usage

```ruby
remote_control = RemoteControl.new

remote_control.appliance = Lamp.new
remote_control.turn_on

remote_control.appliance = TV.new
remote_control.turn_on
```
