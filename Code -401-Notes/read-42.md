What Are Dunder Methods?
In Python, special methods are a set of predefined methods you can use to enrich your classes. They are easy to recognize because they start and end with double underscores, for example __init__ or __str__.

As it quickly became tiresome to say under-under-method-under-under Pythonistas adopted the term “dunder methods”, a short form of “double under.”

These “dunders” or “special methods” in Python are also sometimes called “magic methods.” But using this terminology can make them seem more complicated than they really are—at the end of the day there’s nothing “magical” about them. You should treat these methods like a normal language feature.

Dunder methods let you emulate the behavior of built-in types. For example, to get the length of a string you can call len('string'). But an empty class definition doesn’t support this behavior out of the box:

class NoLenSupport:
    pass

>>> obj = NoLenSupport()
>>> len(obj)
TypeError: "object of type 'NoLenSupport' has no len()"
To fix this, you can add a __len__ dunder method to your class:

class LenSupport:
    def __len__(self):
        return 42

>>> obj = LenSupport()
>>> len(obj)
42
Another example is slicing. You can implement a __getitem__ method which allows you to use Python’s list slicing syntax: obj[start:stop].

Special Methods and the Python Data Model
This elegant design is known as the Python data model and lets developers tap into rich language features like sequences, iteration, operator overloading, attribute access, etc.

You can see Python’s data model as a powerful API you can interface with by implementing one or more dunder methods. If you want to write more Pythonic code, knowing how and when to use dunder methods is an important step.

For a beginner this might be slightly overwhelming at first though. No worries, in this article I will guide you through the use of dunder methods using a simple Account class as an example.

Enriching a Simple Account Class
Throughout this article I will enrich a simple Python class with various dunder methods to unlock the following language features:

Initialization of new objects
Object representation
Enable iteration
Operator overloading (comparison)
Operator overloading (addition)
Method invocation
Context manager support (with statement)
You can find the final code example here. I’ve also put together a Jupyter notebook so you can more easily play with the examples.

Object Initialization: __init__
Right upon starting my class I already need a special method. To construct account objects from the Account class I need a constructor which in Python is the __init__ dunder:

class Account:
    """A simple account class"""

    def __init__(self, owner, amount=0):
        """
        This is the constructor that lets us create
        objects from this class
        """
        self.owner = owner
        self.amount = amount
        self._transactions = []
The constructor takes care of setting up the object. In this case it receives the owner name, an optional start amount and defines an internal transactions list to keep track of deposits and withdrawals.

This allows us to create new accounts like this:

>>> acc = Account('bob')  # default amount = 0
>>> acc = Account('bob', 10)
Object Representation: __str__, __repr__
It’s common practice in Python to provide a string representation of your object for the consumer of your class (a bit like API documentation.) There are two ways to do this using dunder methods:

__repr__: The “official” string representation of an object. This is how you would make an object of the class. The goal of __repr__ is to be unambiguous.

__str__: The “informal” or nicely printable string representation of an object. This is for the enduser.

Let’s implement these two methods on the Account class:

class Account:
    # ... (see above)

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)
If you don’t want to hardcode "Account" as the name for the class you can also use self.__class__.__name__ to access it programmatically.

If you wanted to implement just one of these to-string methods on a Python class, make sure it’s __repr__.

Now I can query the object in various ways and always get a nice string representation:

>>> str(acc)
'Account of bob with starting amount: 10'

>>> print(acc)
"Account of bob with starting amount: 10"

>>> repr(acc)
"Account('bob', 10)"
Iteration: __len__, __getitem__, __reversed__
In order to iterate over our account object I need to add some transactions. So first, I’ll define a simple method to add transactions. I’ll keep it simple because this is just setup code to explain dunder methods, and not a production-ready accounting system:

def add_transaction(self, amount):
    if not isinstance(amount, int):
        raise ValueError('please use int for amount')
    self._transactions.append(amount)
I also defined a property to calculate the balance on the account so I can conveniently access it with account.balance. This method takes the start amount and adds a sum of all the transactions:

@property
def balance(self):
    return self.amount + sum(self._transactions)
Let’s do some deposits and withdrawals on the account:

>>> acc = Account('bob', 10)

>>> acc.add_transaction(20)
>>> acc.add_transaction(-10)
>>> acc.add_transaction(50)
>>> acc.add_transaction(-20)
>>> acc.add_transaction(30)

>>> acc.balance
80
Now I have some data and I want to know:

How many transactions were there?

Index the account object to get transaction number …

Loop over the transactions

With the class definition I have this is currently not possible. All of the following statements raise TypeError exceptions:

>>> len(acc)
TypeError

>>> for t in acc:
...    print(t)
TypeError

>>> acc[1]
TypeError
Dunder methods to the rescue! It only takes a little bit of code to make the class iterable:

class Account:
    # ... (see above)

    def __len__(self):
        return len(self._transactions)

    def __getitem__(self, position):
        return self._transactions[position]
Now the previous statements work:

>>> len(acc)
5

>>> for t in acc:
...    print(t)
20
-10
50
-20
30

>>> acc[1]
-10
To iterate over transactions in reversed order you can implement the __reversed__ special method:

def __reversed__(self):
    return self[::-1]

>>> list(reversed(acc))
[30, -20, 50, -10, 20]
To reverse the list of transactions I used Python’s reverse list slice syntax. I also had to wrapp the result of reversed(acc) in a list() call because reversed() returns a a reverse iterator, not a list object we can print nicely in the REPL. Check out this tutorial on iterators in Python if you’d like to learn more about how this approach works in detail.

All in all, this account class is starting to look quite Pythonic to me now.

