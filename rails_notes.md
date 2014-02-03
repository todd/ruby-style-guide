# Introduction
This document will serve as a temporary placeholder for Rails-related style guidelines until they are eventually moved into the completed style guide.

# Models
* Always put `include` and `extend` statements immediately after the class definition. These take precedence over all other information as they are inherently tied to the class.
```Ruby
# bad
class Car < ActiveRecord::Base
  self.table_name = 'some_cars'
  
  include SomeModule

  # your code here
end

# good
class Car < ActiveRecord::Base
  include SomeModule
  
  self.table_name = 'some_cars'
  
  # your code here
end
```

* Important meta information (if any) about the model should come immediately after `include` and `extend` statements.
  * Examples of such information are: `self.table_name`, `default_scope`
```Ruby
class Car < ActiveRecord::Base
  include SomeModule
  
  self.table_name = 'some_cars'
  default_scope { order('make') }
end
```

* Logically group associations together.
```Ruby
# bad
has_one :driver
has_many :wheels
has_one :garage

# good
has_one :driver
has_one :garage

has_many :wheels
```

* Logically group scopes together.
  * Avoid use of `default_scope`.
  * Break up long scope definitions by method on each line.
```Ruby
# bad
scope :with_accidents, -> { joins(:accidents).where('accidents.crashed_at IS NULL').includes(accidents: :insurer) }

# bad
scope :with_load_errors, -> {
                                joins(
                                  :accidents
                                ).where(
                                  'accidents.crashed_at IS NULL'
                                ).includes(accidents: :insurer)
                              }

# good
scope :with_load_errors, -> {
  joins(:accidents)
  .where('accidents.crashed_at IS NULL')
  .includes(accidents: :insurer)
}
```
