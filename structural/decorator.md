# Decorator

The decorator pattern is used to extend or alter the functionality of objects at run- time by wrapping them in an object of a decorator class. This provides a flexible alternative to using inheritance to modify behaviour.

## Example

```ruby
module Element
  def image_path
    raise "Not implemented"
  end
end

class Shape
  include Element

  def image_path
    "shape.png"
  end
end

class Object
  include Element

  def image_path
    "object.png"
  end
end

class ElementDecorator
  include Element

  def initialize(decorated_element)
    @decorated_element = decorated_element
  end

  def image_path
    @decorated_element.image_path
  end
end

class ColorDecorator < ElementDecorator
  def initialize(decorated_element)
    super(decorated_element)
  end

  def image_path
    "color-" + super
  end
end

class SizeDecorator < ElementDecorator
  def initialize(decorated_element)
    super(decorated_element)
  end

  def image_path
    "size-" + super
  end
end
```

### Usage

```ruby
element = Shape.new
puts "Path = #{element.image_path}"
element = ColorDecorator.new(element)
puts "Path = #{element.image_path}"
element = SizeDecorator.new(element)
puts "Path = #{element.image_path}"
```

### Output

```text
Path = shape.png
Path = color-shape.png
Path = size-color-shape.png
```
