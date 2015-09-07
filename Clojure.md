##September 7th 2:38pm

I should probably move faster through this book. I'm still on chapter 2 :). I
think my biggest issue is I like to kind of know the deeper, but I also think
going through each example and then writing a bit about it is going to help me
fully grasp the concepts.

Oh and quick note... I forgot about these, but where I'm at in the book they
mention sets. Well I completely forgot what a set was... on the clojure site it
mentions this

[Data Structures - Sets] (http://clojure.org/data_structures#Data Structures-Sets)

"Sets are collections of unique values."


```clojure
({:a :b :c :d})
```

Notes this map is using unique keywords in each index.



##September 7th 1:53pm
Looking at collection tests. Again I am working through the Living Clojure book. 

One of the first examples I am given is the every? function. It looks like it
takes two arguments. It takes a predicate(?) to test and the collection.

So it looks like this

```clojure
Ex: (every? odd? [1 1 1])
```

Return: true

This checks each value in the vector. If the predicate(?) test returns true then
the function returns true. If any of the items in the collection don't return
true... the function returns false

So again if we check in the Living Clojure book they answer what a predicate is. 

"A predicate is just a function that returns a value used in a logic test."

So i'm thinking that odd? is a function, a built in function but that probably
means we can use our own functions to run tests. 

Because I come from javascript filter comes to mind. For instance in
javascript we could do something like this for an array.


'''javascript
[1,2,3,4].filter( value => { return value % 2 !== 0; })
'''

Its slightly different because the filter only returns the items where this is
true in a new array... and not returning a value but we could do that like so

So javascript actually has a built in method called every and it does pretty
much exactly what our clojure script is doing but were using our own lamdas
(anonymous functions)

It would look like this

'''javascript
[1 1 1].every(item => item % 2 !== 0);
'''

This will return true, anyway using javascript always helps me understanding
other concepts in other languages. Sorry for this digression it just helps me
understand. 


Back to Clojure
We can also write our own predictes (functions that return true or false in a
logic test )

'''clojure
(defn isThisOdd? [x] (not= (rem [x] 2) 0))
'''

I tried to get this to work, the method is created but when I pass a vector into
it... i just get an error

ClassCastException clojure.lang.PersistentVector cannot be cast to
java.lang.Number  clojure.lang.Numbers.remainder (Numbers.java:173)

Which is strange because I thought the every? function didn't pass the vector
but I think that is what is happening. I'll need to look more into it...

But anyway the idea is clear you can pass in functions in this case they're
predicates that return a boolean value.

Of course every? isn't the only "iterable" (?) (didn't see this word used but it
makes sense to me.) function. 


# not-any?
Another one checking for false is not-any?. It can be used like so

```clojure
(not-any? #(= % :drinkme) [:drinkme :poison])
```

Returns: false

So one quick note... this is an example from the living clojure book. It
confused me a t first because what is this new syntax... 

Well it turns out its shorthand for lamda functions.

You could write things in the previous fashion this is just another version.

There is also another function

# some

Another function does something slightly different, it returns the first logical
true value of the predicate, and returns nil if there isn't a true value.

'''Clojure
(some #(> % 3) [1 2 3 4 5])
'''

This will return true because well 4 > 3.


September 7th 1:19pm

I took a few days off from playing with clojure. I dug into some javascript
testing. But I want to spend a little time on clojure today.

There is an empty? function. This is cool reminds me of ruby methods


We can check if a vector is empty by doing soething like this
1. Empty?
'''Clojure
(empty? [:table :door :key])
'''

Return: false

This of course will return false
'''Clojure 
(empty? [])
'''

Return: true
This will return true because the vector is empty

The cool thing is you can actually use this with maps and I think lists but lets
try first.

Yup you can do it with those check these examples out.

'''Clojure
(empty? {})
'''

Return: true

'''Clojure
(empty? '())
'''

Return true

This is cool because it looks like you can use the empty? function with all
the collection types

So Living Clojure page just mentioned something called seq. Apparently under the
hood empty is using it. The example was this

'''Clojure
(defn empty? [col1] (not (seq col1)))
'''

But what is seq. I understand its using a not so lets just look at this from
what we understand right now.

This method takes one argument the col1 argument. Which to me would mean
collection. Then lets check out the expressions from the innermost expression. 

'''Clojure
(seq col1)
'''

I'm not quite sure what seq would mean... so lets just assume that's true (?)
not really sure.

Then the not would check the value of the inner expression.. which would negate
whatever value was returned.

so if we do

'''Clojure
(empty? [:3])
'''

Were technically doing 

'''Clojure
(not (seq [:3])
'''

This would return false... so seq [:3] must return true.. and the not would
negate that, so we'd get false back... but anyway lets dig into what seq is.


Abstractions and seq
In clojure there are the collection and sequence abstractions. Collections are a
collection of elements lik in a vector, a map, or a list. These all share
immutable data structure. The collections abstractions share methods like count,
conj, and seq. (ah there is that word again).

So what is seq. Apparently the seq function turns the collection (map, vector,
list) into a sequence. A sequence is a walkable, list abstraction for collection
data structure. Seq (short for sequences) are also persistent and immutable and
provide shared functions like first, rest, and cons.


So the seq function returns a sequence on the collection or returns nil if it is
empty.

So this does actually explain why (seq [:3]) would return truthy since i'm
assuming anything not nil in this instance would not be falsy.


SideNote:

I was reading through more of Clojure Living and so I was curious about
something. (seq []) returns a nil, but (seq [:1 :2 :3]) returns the sequence not
true. Well that's all solved by using the not function. In Clojure Living it
says this.

".. a not of some other value then a logical false, like a string or an integer
will return false."

So for us that's whats happening... were running not on a sequence which returns
false.

whoa that's interesting and a lot to digest but it does make sense

Today is September 2nd 12:00 am

I can't sleep... so i'm going through some closure stuff..

Different types of collections in closure

1. List
'''Clojure
'(:a :b :c)
'''

This is a list with three keywords. (symbols in ruby  :) )
special properties of a list...
You can't access an index directly you have to do so using things like this

'''Clojure
(first '(:a :b :c))
'''

That would return :a

Or you can return b by doing this

'''Clojure
(first (rest '(:a :b :c)))
'''

This will return :b... but wwhy

Its because you call the rest operation which returns everything but the first
item in the list. You then pass that new value in and this time use the first
operation for the list :b :c... it will pull :b


2. Vector 

'''Clojure
[:a :b :c]
'''

This is basically what I think of as an array. You can grab values directly
just like in an array... you just specify the index... 

'''Clojure
(nth [:a :b :c] 1)
'''

This will return :b .. remember all  vectors are 0 based

You can also call first, last, and rest operations

3. Maps

'''Clojure
{:a 'letter A' :b 'letter B' :c 'letter cd'}
'''

This is a map... or hash in ruby or dictionary in python or object in javascript

It consists of a property and a value or key and value pairs

In this case the key is a keyword and the value is a string

You can get values by using the get operation like so


'''Clojure
(get {:a 'letter a' :b 'letter b' :c 'letter c'} :b)
'''

Or you can use the key like so

'''Clojure
(:b {:a 'letter a' :b 'letter b' :c 'letter c'})
'''


You can view all the keys by using the keys operation

'''Clojure
(keys {:a 'letter a' :b 'letter b' :c 'letter c'})
'''









Today is August 28th 2015

10:44pm -
  Been running through some python tutorials on codecademy. Mostly just review
of the language syntax. Ran into something interesting.

###Strings
So there are methods you can apply to a string like len()... but that's
interesting is you can apply that to other data types... you use it like so

'''Python
len("charlie")
'''

It would output the length

You also have methods like upper and lower.. .these belong to the String class.
You would call them like so

'''Python
"Delta".upper()
"Echo".lower()
'''


###String Formatting with %

The % operate after a string is used to combine a string with variables. The %
operator will replace a %s in the string with the string variable that comes
after it... FOr example

'''Python
string_1 = "Camelot"
string_2 = "place"

print "Let's not go to %s. 'Tis a silly %s." % (string_1, string_2)
'''

So this string would print as follows

Let's not go to Camelot. Tis a silly place.



### Functions

This is something I always mix up terminology on. 
A parameter is like (n) where n would be the paramter of the function definition
An argument is the value of an argument or put another way
A paramter acts as a variable name for a passed in argument


Functions take arguments but the placeholder in the function declaration or
definition is a paramter


#August 28th 2015 - 1:13 PM

#Lists

Some intere





Whoa... that's cool
