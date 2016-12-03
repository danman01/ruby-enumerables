# Ruby Enumerables
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
 - The Ruby module that allows searching, traversing, sorting and manipulating collections.

 - Take a look at these examples. Can you describe what is going on in each?
```
[1,3,5].max
=> 5
```

```
toys = {"cars": ["mazda","porsche","subaru"], "bikes": ["schwinn", "GT", "surly"]}
toys.each do |key, value|
  puts "#{key}: #{value}"
end
=> cars: ["mazda", "porsche", "subaru"]
   bikes: ["schwinn", "GT", "surly"]
```
 - acts on a collection ([] and {}, otherwise known as...)
  
 - Use in your classes by `include`ing the module
   - known as a `mixin`
   
### Try it
 - Open your `irb` and create an enumerable
  - What methods are available to your enumerable?
  - `yourEnum.methods`
    - Try sorting this collection. (Hint: there is a `sort` method)
    - Think about how you might return only method names that start with "s" (...we will revisit this)
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
  - A list of any method aliases (i.e `inject` and `reduce`)
  - An example of the method. 
  - At a high level, try to find/think of a use case of this enumerable in the wild. It doesn't have to be the actual code, just conceptually similar.
  
  - The enumerables are:

  1. `each_with_index`
  2. `reject`
  3. `map` 
  
  4. `find`
  5. `select`
  6. `sort_by`
  
  7. `reduce` 
  8. `any?`
  9. `each`
  
  10. `include?` 
  11. `flat_map`
  12. `all`
  

## You Do: Ice Cream Menu

 - Open up your ruby console
 
 - Print out every possible combination of the below ice cream flavors and toppings:
```
flavors = [ "vanilla", "chocolate", "strawberry", "butter pecan", "cookies and cream", "rainbow" ]
toppings = [ "gummi bears", "hot fudge", "butterscotch", "rainbow sprinkles", "chocolate sprinkles" ]
```

>Hint: "nest"

## Learn Together
- Describe what is going on here?
```
[2,5,6,7].reject {|num| num % 2 == 0 }
=> [5,7]
```
```
[2,5,6,7].select {|num| num % 2 == 0 }
=> [2,6]
```

Give me just the names that start with "s":
```
["sam","tim","bob","solomon"].select do | name | 
  name=~/\A(s)/ 
 end
```


## Break!


### Map
 - The Enumerable module contains several methods that allow you to create a new collection out of an existing one. `map` is a popular method that applies code to each item in the original collection and returns a new array.
 
 Consider the following example:
 
 ```
   cars = ["honda","bmw","ford","cadillac"]
   cars.map do |car|
     car.capitalize
   end
```
 - what does `map` act on?
 - what is provided to `map`?
 - what does `map` do to the original array?
 - what is returned?
 
### Reduce
 - `inject` aka `reduce` is used to "accumulate" the elements in a collection to give a final answer.
 - This method performs an operation that combines the current enum with the accumalator value (sometimes denoted as a "memo"). As we loop through the collection, the code in the block acts on each element in the enum and the value returned from the code is used as the starting point for the next round in the loop. The final answer is the accumulation of each round. If you pass a symbol and a method or operator, that method will act upon each enum.
 
 - What does this do? Sometimes it helps to write it out...
```
(5..10).inject { |sum, n| sum + n }  
```
 - The same using the shorthand of providing a symbol and method or operator:
```
(5..10).reduce(:+)
```

 -Find the longest word in a list, without using `reduce`
  ["war","what","is","it","good","forrrr"]
 
 - Now try it with `reduce`

```
longest = %w{ cat sheep bear }.reduce do |memo, word|
   memo.length > word.length ? memo : word
end
longest
```

## Ranges
 - What is a range?
  - A Range represents an interval. It is a set of values with a beginning and an end. Docs: (https://ruby-doc.org/core-2.2.0/Range.html)[https://ruby-doc.org/core-2.2.0/Range.html]
 
 - `1..2` is different from
 `1...10`
 -Is a range enumerable?
 -How do you know?

### Code Together
 - Let's determine grades of the class
 ```
 case grade
   when 0..69
    puts "f"
   when 70..71
    puts "d"
   when 72..79
    puts "c"
   when 80..89
    puts "b"
   when 90..95
    puts "a"
   when 96..100
    puts "a+"
  end
```
### You Try: 
 - Print all of the letters of the alphabet
 - Only print numbers divisible by 3 in the range `1..100`

## Code Together: Write our own class that implements Enumerable
 >The Enumerable mixin provides collection classes with several traversal and searching methods, and with the ability to sort. The class must provide a method each, which yields successive members of the collection. If Enumerable#max, #min, or #sort is used, the objects in the collection must also implement a meaningful <=> operator, as these methods rely on an ordering between members of the collection. - [The Docs](https://ruby-doc.org/core-2.3.3/Enumerable.html)
 
 - So your code to create a class that uses the Enumerable module will have at least four key things:
 - A class definition, so we know it's a class
 - an `include` statement to "mixin" the Enumerable module and gain all of it's superpower
 - an `each` method, which yields successive members of the collection
 - a `<=>` operator if Enumerable#max, #min, or #sort is used
 - How do you show which modules are included within a class?

(More on writing classes in Ruby)[http://rubylearning.com/satishtalim/writing_our_own_class_in_ruby.html]

## BREAK!
 
## Lab & Homework - High Card

How do you compare cards?

Start working with a partner and create and play a few rounds of the popular card game, "High Card!" 

You will:
 - On one users' Git account, fork and clone the project. There will be one submission per pair. Ensure you both have read / write access to the repo.
 - use Ruby enumerable methods to create the game
 - create an algorithm to determine which of two cards, if either, is "greater" than the other.
 - accept input from the command line that your program uses
 - switch off who is typing the code and who is researching methods
 - Talk through your approach, what you discovered or what you struggled with

Go here for the details and to get started: https://github.com/danman01/high_card

-Bonus! Implement the <=> operator in your high card game
 
## Homework:
Finish the High Card game! One submission per pair. Please have at least one commit from each person so we know who worked with who.
https://github.com/danman01/high_card

## Resources
- [GA DC Ruby Enumerables](https://github.com/ga-wdi-lessons/ruby-enumerables)
- [Ruby Docs](https://ruby-doc.org/core-2.3.3/Enumerable.html)
