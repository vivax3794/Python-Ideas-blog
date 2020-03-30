This is how you avoid using lambdas in python!

# What are lambdas?
Lambdas are [anonymous functions](https://book.pythontips.com/en/latest/lambdas.html) they are useful when you don't want to define a new function just for that little `map` function.

# Why not to use them!
They can look ugly and make what is part of the lambda and what is part of the rest of the expression.
Let's take the example from the previous link:
```python
a.sort(key=lambda x: x[1])
```
Well, this is not the worst, but there is no clear border around the lambda.

It is worse in a map function, since there the lambda is the first argument.
```python
map(lambda x: x[0], some_list)
```
Again, this might not be that bad. But the only real indication that the lambda has ended is a `,`.
But some lambdas call functions them self, so just hitting a `,` does not mean the lambda is done.
this can make things confusing fast!

# But what should I do instead?
There are 2 ways to avoid lambdas.
* Define the function normally with `def`.
* Use functions from the standard lib instead!
	* Yes, the standard lib has many nice functions for this, mainly you might be interested [operator](https://docs.python.org/3/library/operator.html) 

Let's take that first example again:
```pytohn
a.sort(key=lambda x: x[1])
```
And look at the 2 methods on how to use something else!

## Using normal def
this is a easy fix.
```python
def get_index_1(some_list):
	return some_list[1]

a.sort(key=get_indedx_1)
```
You might see this and thing, "What a waste of a function and lines!"
And you are right, this is not the best option, but I will argue that this is still better than lambdas.
But let's now look at the standard lib and see if it can help us!

## The standard lib
here [operator](https://docs.python.org/3/library/operator.html) is out friend, specifically [operator.itemgetter](https://docs.python.org/3/library/operator.html#operator.itemgetter) is the tool we need!
> Return a callable object that fetches item from its operand using the operand’s __getitem__() method.

This sounds like exactly what we need! now let's see how this can be used to remove that pesky lambda:
```python
import operator

a.sort(key=operator.itemgetter(1))
```
Much clearer don't you agree?

