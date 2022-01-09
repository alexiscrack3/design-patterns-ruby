# Singleton

The singleton pattern ensures that only one object of a particular class is ever created. All further references to objects of the singleton class refer to the same underlying instance. There are very few applications, do not overuse this pattern!

## Example

```ruby
module LogLevel
  VERBOSE = 0
  DEBUG = 1
  INFO = 2
  WARNING = 3
  ERROR = 4
end

module LogTag
  OBSERVABLE = "OBSERVABLE"
  MODEL = "MODEL"
  VIEW_MODEL = "VIEW_MODEL"
  VIEW = "VIEW"
end

module Loggable
  def v(tag, message)
    Logger.default.log(LogLevel::VERBOSE, tag, message)
  end

  def d(tag, message)
    Logger.default.log(LogLevel::DEBUG, tag, message)
  end

  def i(tag, message)
    puts "WUT? #{Logger.default}"
    Logger.default.log(LogLevel::INFO, tag, message)
  end

  def w(tag, message)
    Logger.default.log(LogLevel::WARNING, tag, message)
  end

  def e(tag, message)
    Logger.default.log(LogLevel::ERROR, tag, message)
  end
end

class Log
  extend Loggable
end

class Logger
  private_class_method :new
  @default = new

  def self.default
    @default
  end

  def log(level, tag, message)
    puts "#{level}/#{tag}: #{message}"
  end
end
```

### Usage

```swift
Log.i(LogTag::MODEL, "info")
```

### Output

```text
2/MODEL: info
```
