# Futures for Crystal
Futures provide a nice way to reason about performing many operations in parallel– in an efficient and non-blocking way. The idea is simple, a Future is a sort of a placeholder object that you can create for a result that does not yet exist. Generally, the result of the Future is computed concurrently and can be later collected. Composing concurrent tasks in this way tends to result in faster, asynchronous, non-blocking parallel code.

** Source : http://docs.scala-lang.org/overviews/core/futures.html

## Usage
```crystal
require "futures"
include Futures

# Create a new future
a = Future.new do
  someTimeConsumingOperation()
end

# Register a callback on successful operation
a.on_success do |val|
  doSomethingWithResult val
end
a.on_failure do |err|
  raise err
end

# Or handle both cases in one callback
a.on_complete do |result|
  try = result.get
  case try
  when Success
    puts try.get
  when Failure
    raise try.error
  end
end

# Or block until future completes
val = a.get

# compose new Futures from existing ones
b = a.map do |val|
  "String : " + val
end

b.get
```

## Documentation
[Link](http://dhruvrajvanshi.github.io/crystal-futures/)
