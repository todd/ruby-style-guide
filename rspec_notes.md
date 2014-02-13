# Introduction
This document will serve as a temporary placeholder for RSpec-related style guidelines until they are eventually moved into the completed style guide.

# `describe`
Use `describe` blocks to describe classes and methods. There should only be a single `describe` block for classes, with all method descriptions grouped within it. For methods, prepend `.` for class and `#` for instance method names.

```ruby
# Bad
describe SomeClass, '.some_method' do
  ...
end

describe SomeClass, '#some_other_method' do
  ...
end

# Good
describe SomeClass do
  describe '.some_method' do
    ...
  end
  
  describe '#some_other_method' do
    ...
  end
end
```

# `context`
Use `context` blocks to describe behavior within specific scenarios. Can also be used to describe activity that occurs in ActiveRecord callbacks.

# `it`
As a general rule, strive for only a single assertion per `it` blocks.
