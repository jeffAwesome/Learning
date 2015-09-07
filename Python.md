#Python Notes

Today is August 28th 2015

10:44pm -
  Been running through some python tutorials on codecademy. Mostly just review
of the language syntax. Ran into something interesting.

###Strings
So there are methods you can apply to a string like len()... but that's
interesting is you can apply that to other data types... you use it like so

```python
len("charlie")
```

It would output the length

You also have methods like upper and lower.. .these belong to the String class.
You would call them like so

```python
"Delta".upper()
"Echo".lower()
```


###String Formatting with %

The % operate after a string is used to combine a string with variables. The %
operator will replace a %s in the string with the string variable that comes
after it... FOr example

```python
string_1 = "Camelot"
string_2 = "place"

print "Let's not go to %s. 'Tis a silly %s." % (string_1, string_2)
```

So this string would print as follows

Let's not go to Camelot. Tis a silly place.



### Functions

This is something I always mix up terminology on. 
A parameter is like (n) where n would be the paramter of the function definition
An argument is the value of an argument or put another way
A paramter acts as a variable name for a passed in argument


Functions take arguments but the placeholder in the function declaration or
definition is a paramter


