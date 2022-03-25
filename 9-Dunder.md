# Dunder

Special methods are a set of predefined methods you can use to enrich your classes. They are easy to recognize because they start and end with double underscores, for example `__init__` or `__str__`.

Dunder methods let you emulate the behavior of built-in types. For example, to get the length of a string you can call len('string'), you can add a `__len__` dunder method to your class. Another example is slicing. You can implement a __getitem__ method which allows you to use Python’s list slicing syntax: obj[start:stop].

```Python:
class NoLenSupport:
    pass
>>> obj = NoLenSupport()
>>> len(obj)
TypeError: "object of type 'NoLenSupport' has no len()"

class LenSupport:
    def __len__(self):
        return 42
>>> obj = LenSupport()
>>> len(obj)
42
```

<br>

## Common dunders used as methods in classes:

### 1. Object Initialization (constructor): `__init__`

```Python:
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
```

<br>

### 2. Object Representation: `__str__` , `__repr__`

To provide a string representation of your object for the consumer of your class. There are two ways to do this using dunder methods:

1. `__repr__`: The “official” string representation of an object. This is how you would make an object of the class. The goal of `__repr__` is to be unambiguous.
2. `__str__`: The “informal” or nicely printable string representation of an object. This is for the enduser.

```Python:
class Account:
    # ... (see above)

    def __repr__(self):
        return 'Account({!r}, {!r})'.format(self.owner, self.amount)

    def __str__(self):
        return 'Account of {} with starting amount: {}'.format(
            self.owner, self.amount)
```

If you don’t want to hardcode "Account" as the name for the class you can also use `self.__class__.__name__` to access it programmatically.

<br>

### 3. Iteration: `__len__` , `__getitem__` , `__reversed__`:

```Python:
class Account:
    def __init__...

    def add_transaction(self, amount):
        if not isinstance(amount, int):
            raise ValueError('please use int for amount')
        self._transactions.append(amount)
    
    # stage 2 : added after error happend
    def __len__(self):
        return len(self._transactions)

    def __getitem__(self, position):
        return self._transactions[position]

    def __reversed__(self):
        return self[::-1]

    @property
    def balance(self):
        return self.amount + sum(self._transactions)
```

```Python:
# Before adding stage 2
>>> len(acc)
TypeError
>>> for t in acc:
       print(t)
TypeError
>>> acc[1]
TypeError

#after adding stage 2
>>> len(acc)
5
>>> for t in acc:
       print(t)
20
-10
50
-20
30
>>> acc[1]
-10
>>> list(reversed(acc))
[30, -20, 50, -10, 20]
```

<br>

### 4. Operator Overloading for Comparing Accounts: `__eq__` , `__lt__` , `__gt__`:

Used to compare objects with logic operators. in thier methods you can spicefy what is the item that should be compared.

```Python:
    def __eq__(self, other):
        return self.balance == other.balance

    def __lt__(self, other):
        return self.balance < other.balance

>>> acc2 > acc
True
>>> acc2 < acc
False
>>> acc == acc2
False
```

<br>

### 5. Operator Overloading for Merging Accounts: `__add__`:

To spicefy what is the item that should be concatenated when add two object from that type with each other.

Let’s implement `__add__` to be able to merge two accounts. The expected behavior would be to merge all attributes together: the owner name, as well as starting amounts and transactions. To do this we can benefit from the iteration support we implemented earlier:

```Python:
def __add__(self, other):
    owner = '{}&{}'.format(self.owner, other.owner)
    start_amount = self.amount + other.amount
    acc = Account(owner, start_amount)
    for t in list(self) + list(other):
        acc.add_transaction(t)
    return acc

>>> acc3 = acc2 + acc
>>> acc3
Account('tim&bob', 110)
>>> acc3.amount
110
>>> acc3.balance
240
>>> acc3._transactions
[20, 40, 20, -10, 50, -20, 30]
```

If we wanted to ignore historic transactions—fine, you can also implement it like this:

```Python:
def __add__(self, other):
    owner = self.owner + other.owner
    start_amount = self.balance + other.balance
    return Account(owner, start_amount)
```

<br>

### 6. Callable Python Objects: `__call__`:

You can make an object callable like a regular function by adding the `__call__` dunder method. The downside of having a `__call__` method on your objects is that it can be hard to see what the purpose of calling the object is.

```Python:
def __call__(self):
        print('Start amount: {}'.format(self.amount))
        print('Transactions: ')
        for transaction in self:
            print(transaction)
        print('\nBalance: {}'.format(self.balance))

>>> acc()
Start amount: 10
Transactions:
20
-10
50
-20
30
Balance: 80
```

<br>

### 7. Context Manager Support and the With Statement: `__enter__` , `__exit__`:

A context manager is a simple “protocol” (or interface) that your object needs to follow so it can be used with the with statement. Basically all you need to do is add `__enter__` and `__exit__` methods to an object if you want it to function as a context manager.

```Python:
    def __enter__(self):
        print('ENTER WITH: Making backup of transactions for rollback')
        self._copy_transactions = list(self._transactions)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('EXIT WITH:', end=' ')
        if exc_type:
            self._transactions = self._copy_transactions
            print('Rolling back to previous transactions')
            print('Transaction resulted in {} ({})'.format(
                exc_type.__name__, exc_val))
        else:
            print('Transaction OK')
```
<br>

<br>

## [Reference](https://dbader.org/blog/python-dunder-methods)