# Ruby Enumerables
The Ruby module that allows searching, traversing and manipulating collections.

Take a look at these examples. Can you describe what is going on in each?
```
[1,3,5].max
=> 5
```
```
[2,5,6,7].select {|num| num % 2 == 0 }
=> [2,6]
```
```
toys = {"cars": ["mazda","porsche","subaru"], "bikes": ["schwinn", "GT", "surly"]}
toys.each do |key, value|
  puts "#{key}: #{value}"
end
=> cars: ["mazda", "porsche", "subaru"]
   bikes: ["schwinn", "GT", "surly"]
```

## Framing
One of the most common things we do as developers is to iterate through data structures.

Whenever we talk about data in Ruby, its important to review how Ruby handles groups of data.

We learned how to work with collections of data in Javascript: looping through data, getting things into and out of arrays and hashes. Now we're going to learn how to work with collections of data in Ruby.

## Objectives
 - Review Ruby Classes, Instances and Modules
 - Learn about Enumerables in Ruby
 - Access the Ruby Docs to find information on methods and modules
 - What are the differences between Javascript and Ruby enumerables?
 - Use enumerables to traverse, search, sort and modify collections.
 - Implement a ruby class that is enumerable
 
## What is an Enumerable?
 - A Ruby Module
  - acts on a collection ([] and {}, otherwise known as...)

 - Allows traversing, sorting, searching and modifying the collection
  
 - Use in your classes by `include`ing the module
   - known as a `mixin`
### Try it
 - Open your `irb` and create an enumerable
  - What methods are available to your enumerable?
  - `yourEnum.methods`
    - Try sorting this collection. (Hint: there is a `sort` method)
    - Try returning only method names that start with "s" (pseudocode is fine...we will revisit this)
  - How does the instance of the class you chose have all of the methods of the Enumerable module available to it?
## Ruby Docs
 - What methods are available in the Enumerable Module? `
 - Does a class have a certain method implemented?
 - View Usage examples
 - View The Docs here: [Enumerable](https://ruby-doc.org/core-2.3.3/Enumerable.html)
 
### Group Exercise: Documentation Dive 

 - Instructions: In your pods, spend 10 minutes using Ruby documentation to look up an assigned enumerable. Prepare the following for your demo:

  - Your own definition of what it does. Make sure to talk about:
    - What arguments can the method take?
    - What is returned?
    - Does it take a block? If so, what happens when a block is given? 
  - An example
  - A list of any method aliases (i.e `inject` and `reduce`)
  - At a high level, try to find/think of a use case of this enumerable in the wild. It doesn't have to be the actual code, just conceptually similar.
  - The enumerables are:

  - `Each With Index`
  - `Reject`
  - `map` 
  
  - `Find`
  - `Select`
  - `Sort By`
  
  - `Reduce` 
  - `any?`
  - `all?`
  
  - `include?` 
  - `flat_map`
  - `grep`
  

## You Do 

 - Open up your ruby console
 
 - Print out every possible combination of the below ice cream flavors and toppings:
```
flavors = [ "vanilla", "chocolate", "strawberry", "butter pecan", "cookies and cream", "rainbow" ]
toppings = [ "gummi bears", "hot fudge", "butterscotch", "rainbow sprinkles", "chocolate sprinkles" ]
```

Hint: "nest"

## More Examples
What does this do?
```
(5..10).inject(1, :*)
```
How about this?

```
longest = %w{ cat sheep bear }.reduce do |memo, word|
   memo.length > word.length ? memo : word
end
longest
```
Back to the earlier example of method names that start with an "s":
`[].methods.select { | meth | meth=~/\A(s)/ }`
What is going on here?

## Break!

### Map
 - `map` is used to create an Array of transformed Enumerable elements
 
 Consider the following example:
 
 ```
   ["honda","bmw","ford","cadillac"].map do |car|
     car.capitalize
   end
```
 - what is given to `map`?
 - what does `map` do to array?
 - what is returned?
 
### Reduce
 - `reduce` is used to "summarize" the elements in an Enumerable
 - The Docs say it well:
 ```
reduce(initial, sym) → obj
reduce(sym) → obj
reduce(initial) { |memo, obj| block } → obj
reduce { |memo, obj| block } → obj
Combines all elements of enum by applying a binary operation, specified by a block or a symbol that names a method or operator.

If you specify a block, then for each element in enum the block is passed an accumulator value (memo) and the element. If you specify a symbol instead, then each element in the collection will be passed to the named method of memo. In either case, the result becomes the new value for memo. At the end of the iteration, the final value of memo is the return value for the method.

If you do not explicitly specify an initial value for memo, then the first element of collection is used as the initial value of memo.

# Sum some numbers
(5..10).reduce(:+)                             #=> 45
# Same using a block and inject
(5..10).inject { |sum, n| sum + n }            #=> 45
# Multiply some numbers
(5..10).reduce(1, :*)                          #=> 151200
# Same using a block
(5..10).inject(1) { |product, n| product * n } #=> 151200
# find the longest word
longest = %w{ cat sheep bear }.inject do |memo, word|
   memo.length > word.length ? memo : word
end
longest                                        #=> "sheep"
```


## Demo: Write our own class that implements Enumerable
 >The Enumerable mixin provides collection classes with several traversal and searching methods, and with the ability to sort. The class must provide a method each, which yields successive members of the collection. If Enumerable#max, #min, or #sort is used, the objects in the collection must also implement a meaningful <=> operator, as these methods rely on an ordering between members of the collection. - [The Docs](https://ruby-doc.org/core-2.3.3/Enumerable.html)
 
 - So your code to create a class that uses the Enumerable module will have at least four key things:
 - A class definition, so we know it's a class
 - an `include` statement to "mixin" the Enumerable module and gain all of it's superpower
 - an `each` method, which yields successive members of the collection
 - a `<=>` operator if Enumerable#max, #min, or #sort is used
 
 > When you design a class, think about the objects that will be created from that class type. Think about the things the object knows and the things the object does.

> Things an object knows about itself are called instance variables. They represent an object's state (the data - for example, the quantity and the product id), and can have unique values for each object of that type.

> Things an object can do are called methods. - [RubyLearning.com](http://rubylearning.com/satishtalim/writing_our_own_class_in_ruby.html)

 - How do you show which modules are included within a class?

## BREAK!

## Ranges
 - What is a range?
 `1..2`
 `1...10`
 -Is a range enumerable?
 -How do you know?
 
## Group exercise - High Card

How do you compare cards?

In your squads, create and play a few rounds of the popular card game, "High Card!" 

You will:
 - use enumerable methods 
 - create an algorithm to determine which of two cards, if either, is "greater" than the other.
 - accept input from the command line that your program uses
 - switch off who is typing the code and who is researching methods
 - Talk through your approach, what you discovered or what you struggled with

Go here for the details and to get started: https://github.com/danman01/high_card

## Code Together:

- Adding the spaceship operator to our custom Card class
- compare cards and find the highest
 
## Homework:
https://github.com/danman01/state_capitals
