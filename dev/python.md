

Python is a programming language where you don't need to compile. You can just run it line by line (which is how we can use it in a notebook). **One way to code in Python** is to use a **Jupyter notebook**. This is probably the best way to combine programming, text and images. In a notebook, everything is laid out in cells.

**Ipynb files** are python notebooks that contain the notebook codes, execution results and text elements. you can run cells in a ipython file and see the results and visualization in-place, very good to work with dataframes.

**Py files** are are python files containing plain text (your code). you can easily run and debug your code. very good to write functions and use them in other places.

#### Dynamic typing

Python is **dynamic typing** while C++ is **static typing**

```
Temp = 10
```
this is correct in Python while **we do not specify the type of** **the variable when initializing** 

But in C++ this leads to an error while a variable has a specific type that we have defined when initializing it

```
Type(temp)=string
Str name = ‘Sahel’
```

#### Type hints

Python has support for optional "type hints".
These **"type hints"** or annotations are a special syntax that allow declaring the type of a variable.
By declaring types for your variables, editors and tools can give you better support. 

```
def get_full_name(first_name: str, last_name: str)
```
`
`first_name: str, last_name: str` are type hints in function parameters.

#### Generic types

There are some data structures that can contain other values, like `dict`, `list`, `set` and `tuple`. and the internal values can have their own type too.
These types that have internal types are called "**generic**" types
To declare those types and the internal types, you can use the standard Python module `typing`.

```
def process_items(items: list[str])`

`def process_items(items_t: Tuple[int, int, str], items_s: Set[bytes])`

`def process_items(prices:Dict[str, float])
```

#### Union

You can declare that a variable can be any of **several types**, for example, an `int` or a `str`.
```
def process_item(item: Union[int, str])
```
this means that `item` could be an `int` or a `str`

##### Possibly `None`

You can declare that a value could have a type, like `str`, but that it could also be `None`.
Indexing : index the sequenced characters in a string

```
def say_hi(name: Optional[str] = None)
```

##### Note: 
-  Avoid using `Optional[SomeType]`
- Instead  **use `Union[SomeType, None]`** 

Both are equivalent and underneath they are the same, but I would recommend `Union` instead of `Optional` because the word "**optional**" would seem to imply that the value is optional, and it actually means "it can be `None`", even if it's not optional and is still required.

##### Classes as types

```
def get_person_name(one_person: Person)
```

#### Pydantic models

a Python library to perform data validation. You declare the "shape" of the data as classes with attributes. And each attribute has a type.

Then you create an instance of that class with some values and it will validate the values, convert them to the appropriate type (if that's the case) and give you an object with all the data.

```
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str = "John Doe"
    signup_ts: Union[datetime, None] = None
    friends: List[int] = []

external_data = {
    "id": "123",
    "signup_ts": "2017-06-01 12:22",
    "friends": [1, "2", b"3"],
}
user = User(**external_data)
print(user)
# > User id=123 name='John Doe' signup_ts=datetime.datetime(2017, 6, 1, 12, 22) friends=[1, 2, 3]
print(user.id)
# > 123
```

Indexing: 
‘hello’ -à 1:h  , 2:e

Reverse indexing :    ‘hello’--à  -1:o  (it just returns the last character of a string),

-2:l

Name = “Sahel is a good girl”

Name[1] = ‘s’

Name[-1]= l -à last element is : -1

**Slicing** : grab a subsection of a string

` `[start,stop,step] -à start: starting index  ,  stop: end index but not include  ,  step: step size we take fro start to stop

‘hellos’

[1:5] --à ellos

[1:4:2]àelo

**Len**(hello)= 6

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.002.png)Strings are **immutable =** can not change so string objects doesn’t support item assignment --à a[0]= ‘s’

String concatenation :    ‘2’ + ‘3’ = ‘23’

x=’hallo’ , y=’hi’    --à  X + Y = hellohi

\n à next line

\t à tab

\\--> \

Name.**replace**(‘Sahel’, ‘Ali’) -à replace a part of a string with another string

Name.**find**(‘is’) = 6 à find the first index of a substring

**Arithmetic operations**

7//2 = 3 -à integer division


mystring = ‘sahel is a student’

**Split() :** convert a string to a list

Mystring.split() ----à it returns sahel , is , a , student

myname = ‘Sahel’

print (“hello” **+** myname)

print (“hello {}”**.format**(‘fox’) )

print(“hello {1} my name is {0}”.format(‘Ali’ , ‘Sahel’))

print (“hello {a} my name is {b}”.format(a=’ali’, b= ‘Sahel’))

**Lists**

Ordered sequence of objects with indexes

Can have different type of elements / indexing / slicing

**My\_list = [1, ‘Sahel’,2.5]**

My\_list[1] -à Sahel

My\_list **+** another\_list  (concatenation)

In a list we can change the elsements (mutable) 

mylist[0] = ‘ali’

mylist.**append()**  --à add a element at the end of the list

mylist.**pop() --à** remove an elemnt from the end of a list

mylist.pop(1)   // element in the index = 1

temp = mylist.pop()

\*\*\*\*\*my\_list = [1,2,[3,4,’sahel’]]

\*\*\*\*\*My\_list[2][1] =4

**Sort list** :

My\_list.sort()

Mylist   ---à it gives sorted format of list , it actually changes the list

Sorted(My\_list) ---à it doesn’t change the list just return the sorted format

Mylist= [1,2]

Mylist.extend ([2,3,’hey’]) -à concanteneate the given list with the existing mylist variable -à [1,2,2,3,’hey’]

Mylist.append([‘pop’,1]) -à it just add one element to the list à [1,2,[‘pop’,1]]

Del(mylist[0])--à delete the first element of list à [2]

“sahel is a good girl”.split() -à it splits a string into a list by splitting every group of chracters separated by a space, int an element of list à [‘sahel’, ‘is’,’a’,…]

“sahel,Bloukat”.split(‘,’) à seprate by a specific character ‘,’

Actually a list variable is just a reference to a list

**Aliasing** : when two variable both reference to one single list so when we change the list through variable A the B also changes

**Clone** : we can clone a list to a new element and it is just a copy of the existing list and if we change the existing list the new copied list does not change anymore

A= [1,2,3]

B = A [:]

mylist = [(1,2), (3,4)]

**Dictionaries**

Unordered mapping of objects as **key:value** elements (keys are like indexes in lists)

Keys are immutable and unique

We don’t need to khow the index location to find an element, we just khow the key and find its value

**mydictionary= {‘key1’ : ‘value1’ ,….}**

We can not sort elements in a dictionary

mydictionary[‘key1’] : value1

mydictionary  **=** {key1 : (2,3,4), key2 : [1,2]}

representing a disctionary by a table then à the keys are the first column and the values are the second column

for example in  grocery store we can use dictionaries for grocery pricing

price\_lookup = {‘apple’: 2 , ‘orange’:1.99 ,….}

mydictionary = {**‘k1’** : 1, ‘k2’: [1,2,3]}

we can add a new key:value pair to dictionary by -à  mydictionary[‘A’] **=** 300

delete an element from dictionary à del(mydictionary[‘key1’])

mydictionary.values()

mydictionary.keys() à gives us all the keys

mydictionary.items() /// just show all the key values

‘k1’ **in** mydictionary --à checks if the **a key**  is in the dictionaryà it gives us true or false a sresult

**Tuples**

Are very similar to lists but **immutable**

It means that when an element is assigned to an index position then it can not be changes and reassigned to another element

Mytuple = (1,2,3)

Mylist = [1,2,3]

Mytuple = (‘one’, 2)

Slicing and indexing is allowed    -à     mytuple[1]

Mytuple[1:3] à give me the elements starting from 1 element and until second elemnt (one less thatn the higher number : 3)

mylist=[(‘apple’,200),(‘orange’,300),(‘peach’,400)]            # this is **a list of tuples**

mytuple + (‘two’, 1 ,2) = (‘one’,2,’two’,1,2) -à concantenation of tuples

mytuple = (1,2,’one’, (2,3), (‘two,1’)) à nesting --à  mytuple[4][1] à just pay attention that indexes starts from 0

**tuple unpaccker:**

for  ticker,price   in  mylist:

`      `print(price)

**Sets**

**Unordered** collections of **unique** elements

It means that **it can not be the there two same objects** like two times element 2	

myset = set()

myset**.add** (‘1’)

myset.remove(‘hi’)-à remove an element from a set

‘hello’ **in** myset -à if an element is in a set

Mylist3 = mylist1 & mylist2 à gives us the intersection of two sets

Mylist3 = mylist1.union(mylist2)

Mylist1.issubset(mylist3)

the usefulness of sets is when we want to have a list without repeated elements so we cast the list to a set

**set(mylist)** -à convert list to a set

**Booleans**

**Files IO**

myfile is  a text file that is saved in the same directory of the project

myfile = **open** (myfile.txt)                    // here my file is the name of file

myfile.**read()**                //  just return all that is in the text file

myfile.**read(4)**     // read only the first 4 characters of the file , and keep in mind that in this case cursor will go to the 4<sup>th</sup> character and if we call read again it will start reading from the 4<sup>th</sup> character

![Diagram, timeline

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.003.png)

**important**:

when you once read a file the cursor goes to the end of file so if you read the file for the second time it just returns empty

myfile.**seek**(0)       --à send the cursor again to the start

myfiles.**readline**()           // return the content of text file in terms of different lines 

myfile.readline(10) -à it will return 10 first characters starting from the first line

FileList = myfile.**readlines**() à it will read the file and save it to a list, every element of the list is one line of the file

FileList[0]

myfile = open(“C:\\users\\sahe\\projects\\myfile.text”)

myfile.**close**()

myfile.**mode**() --à r,w,a

**Better way** to open a file and read it :

` `this way , it will close the file automatically, even if the code encounters an exception

**with open**(myfile.txt, **mode** =’r’) **as**  my\_new\_file** (new variable name) **:**

`         `myfile = my\_new\_file.**read()**

mode = ‘r’ , mode = ‘w’ ,    mode = ‘**a**’

**with open**(myfile.txt, **mode** =’r’) **as**  f **:**

`         `print(f.read())

**with open**(myfile.txt, **mode** =’a’) **as**  A **:**

`         `A.write (‘**\n**hi how r u’)	

**with open**(yourfile.txt, **mode** =’w’) **as**  f **:**

`         `f.write(‘hi how r u’)

in **mode = ‘w’**  we just overright a file if it exists **oooor** we create a new file

in **mode = ‘a’**  we append to the end of file (add)

the method **write**() simply works like **readline**() but instead of reading a new line, it writes a new line 


// copy one file to another

with open(**myfile,”r”)** as readfile:

`    `with open (myfile, “w”) as writefile:

`              `for line in readfile:

`                     `writefile.write(line)

It's fairly ineffecient to open the file in **\*\*a\*\*** or **\*\*w\*\*** and then reopening it in **\*\*r\*\*** to read any lines. Luckily we can access the file in the following modes:

\*   **\*\*r+\*\*** : Reading and writing. Cannot truncate the file.

\*   **\*\*w+\*\*** : Writing and reading. Truncates the file.

\*   **\*\*a+\*\*** : Appending and Reading. Creates a new file, if none exists.

Opening the file in **\*\*w\*\*** is akin to opening the .txt file, moving your cursor to the beginning of the text file, writing new text and deleting everything that follows.

Whereas opening the file in **\*\*a\*\*** is similiar to opening the .txt file, moving your **cursor to the very end** and then adding the new pieces of text.

It is often very useful to know where the 'cursor' is in a file and be able to control it. The following methods allow us to do precisely this -

\*   .**tell**() - returns the current position in bytes

\*   .**seek**(offset,from) - changes the position by 'offset' bytes with respect to 'from'. From can take the value of 0,1,2 corresponding to beginning, relative to current position and end

.**seek**(0,0)     // move 0 bytes from beginning.

Finally, a note on the difference between **\*\*w+\*\*** and **\*\*r+\*\***. Both of these modes allow access to read and write methods, however, opening a file in **\*\*w+\*\*** overwrites it and deletes all pre-existing data. 

To work with a file on existing data, use **\*\*r+\*\*** and **\*\*a+\*\***.

**Comparison**

== 	and

!=	or

<	not 1==1 à false

\>

\>=

<=

**Control flow :** control a flow of code in a way that just run the vlock of code that we want

If / else / elif

Indentation (white space ) in control flow is very important

If some\_condition**:**

`    `Then do this

Elif some other condition**:**

`    `Then do this

Else**:**

`    `Do this

**#comment**

#this is a comment

**Loops :** iterate over objects

**For**

Mylist = [1,2,3]

**For** j **in** [1,2,3]**:**
**
`     `Print(j)

For **\_** in [1,2,3] ( **\_** as a variable name)

`     `Print()

mylist = [(1,2), (3,4)]

**for** a,b **in** mylist  //// **for** (a,b) **in** mylist

`     `print(a)

A = {‘k1’:value1 , ‘k2’:value2}

For j in A:

`      `Print(j)  ----à value1

`                                `value2    (it iterates over values)

For j in A.item()

`      `Print(j) --à k1,value1

`                           `K2,value2   (it iterates over the whole item)

**While**

While some\_boolean\_condition:

`            `Do something

`            `……..

`            `……….

Else:

`            `Do something else

**Break,continue,pass**

**Range function**

Range(N) à [0,…,N-1]

For A in range(start,stop,step)

For A in range(10)   ---à 0,1,2,….,9

For A in range(0,10,2) --à 0,2,4,….

**List**(range(0,10,2)) --à [0,2,4,…]      ------à this is a generator that generates list instead of saving them into memory

**Index\_count = 0**

Word = ‘abd’

For item in word

`      `Print(word(index\_count))

`      `**Index\_count += 1** 

For item in **enumerate(**word)

`       `Print(item)-----à function enumerate just return   index,item   value -à (0,a)

**Zip function**

Mylist1 =[1,2,3]

Mylist2 =[4,5,6]

**For** item **in** zip(mylist1,mylist2):

`       `Print(item)  ---à (1,4)

`                                       `(2,5)

List(zip(mylist1,mylist2)) -à [(1,4),(2,5),..]

**In keyword**

2 **in** [1,2,3] --à true

Num **in** range(low,high+1) --à true or false

Mystring= ‘Im not a girl’

Mystring.**replace**(‘ ‘ , ‘’)---à it replaces all the spaces with no space

Mystring = **mystring [: : -1]** --à this just returns the reverse of mystring


**Min**(mylist)

**Max**(mylist)

**Random libarary**

**From** random **import** shuffle --à import shuffle func from library random

Shuffle(mylist) -à shuffle the elemts of a list قر و قاطی کردن

This is inplace function it means it does the shuffle in the list but doesn’t return anyting so we can not save it in a variable

**From** random **import** randint

Randint(lowerlimit, higherlimit)----à produces a random number in this block

**Input** :

` `get an input from the user

**Input**(‘enter a number here’)

Result = input(‘enter the result’)-à this variable result will always be a string/it returns the input as a string

**Casting**

Float(3) = 3

Int(4.2) = 4

Str(2)= ‘2’

Int(True) = 1



**List comprehension**

Mystring = ‘hello’

Mylist =[]

For item in mystring:

`      `mylist.append(item) --à this for loop just put the mystring in the list item by item

another way to do this:

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.004.png)mylist[letter **for** letter **in** mystring] --à [h,e,l,l,o]

`	`this is only a variable name

mylist= [num for num in range(1,10)]	

mylist= [num**\*\*2** for num in range(1,10)  **if** num%2=0]	

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.005.png)	به توان 2

mylist= [num **if** num%2=0 **else** ‘odd’ **for** num **in** range(1,10)]	-à[2,’odd’,4,’odd’]

**for** x in [1,2,3]:

`      `**for** y in [4,5,6]:

`            `mylist.append(x\*y)


**Methods**	this is a function

**help**(mylist.insert)

this help, just helps us to get some information about a function 

L.insert(index,object)

Sum(a,b,c)    --à return the sum of elements

**Functions :** 

blocks of code that can be executed many times, without rewrite, just call the function

**def** name\_of\_function**(**num**):**

`        `**return**  num+num

Name of a function follow the rule of **snake casing :** lowercase letters with underline between words

**def** say\_hello(name = ‘Default’)**:**

`       `print(f ‘hello {name}’)

here of we call the say\_hello function and pass the argument it returns hello… but if don’t pass any argument it returns the value of default

here the argument we pass to the function doesn’t have a specified type , it can be any type (python is dynamic typing)

function can get any type of object as argument, we cal e.g. give a list as the argument to the func

def even\_check(num):

`    `for num in list:

`        `if num%2==0:

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.007.png)             **return** True	this return make it to break out of the function and     

`                                                     `end the function call

`        `else:

`             `**pass**                                       # this pass means don’t do anything

`       `return False                                # this returns false when there is not at all any 

`                                                                `even num in the list

we can also define a variable in a function if it is needed.

**Tuple unpaccking**

\*\*If a function returns tuple then we can do this 

a,b = return(employee , hours)

**\*args**

We can not pass more than 5 parameters to a function and this **\*args** let us to pass an arbitrary number of elements to a function / when the number of argumnets is unknown we also use \*args

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.008.png)

def check( **\*args**):

`       `return sum(\*args)

check(10,20,230,40,40,….)

so args actually **returns back tuples**

**\*\*kwargs**      #keyword arguments

def check (\*\*kwargs):

`       `If ‘fruit’ in kwargs

`           `Return True

Check(fruit =’apple’, veggies = ‘cabbage’ )

If we print kwags  -à  print(kwargs) ---à we get {‘fruit’: ‘apple’, ‘veggies’:’cabbage’}

It actually **returns And get a dictionary**


**Map function:**

This function just map a function that we have earlier defined to every elements of a list

Mylist = [1,2,3]

def check\_even(num):

`       `return  num\*\*2                           

Map(check\_even , mylist)  -à this statement doesnt return anything to us we **should** transform it to  a list 

**List**(map(check\_even,mylist))   ---à[ 1,4,9]

Or use for loop

For item in map(check\_even,mylist):

`       `Print(item)

**Filter function:**

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.009.png)This function filters elements of a list based on a function we have earlier defined

Mylist = [1,2,3,4,5,6]

def  check\_even(num):

`        `return  num%2==0       

list(filter(check\_even,mylist))        --à [2,4,6]        


**Lambda expression:**

One time use function , that we use just one time and never reference again so we do not define a function for that instead we use Lambda expression and we don it give it a name

We here just convert last defined function to lambda expressions

**Lambda** num : num%2==0

**Lambda** num : num\*\*2

We use lambda expressions mostly with map and filter functions

List(map(lambda num:num\*\*2, mylist))

**scope rules:**

**Local namespace**: a variable that is assigned in a function has a local scope and is khown only in the func

**Global** **namespace**: the variable that is assigned at the top level of the file 

**Enclosing namespace**: the variable assigned inside of a function that has in it another function     

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.010.png)def check():

`       `Name = ‘Sahel’ ---à this is enclosing namespace

`       `def add():

`       `print(name)


When we want to find out which variable now we should use we should take a look at namespace rules , **at first** it looks at the **local namespace** and if the variable is assigned there it uses that value **then** it looks at **enclosing namespace** and **at last at global namespace**

If we want to have impact on a global variable in a function we should use:

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.011.png)X = 200

Def check():

`        `**global** x

`        `X=500

`        `Print(x)                     ----à 500  (here we change the global x value from 200 to  

`                                                    `500)

Buuuuut we **shouldn’t use** **global keyword** a lot

**Instead** if we want to change a global variable inside the function we  use **return**

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.012.png)X=400

def check():

`        `X=’Sahel’

`        `Return x

X = check()

This statements just change the global varribale x to sahle while we return the x from the func

**Object oriented programming**

Object-oriented programming (OOP) is a [programming](https://www.udacity.com/course/intro-to-programming-nanodegree--nd000) pattern that consists in defining objects and interacting with them. **An object is a collection of complex variables and functions** and can be used to **represent real entities** like a button, an airplane, or a person.

**To declare, initialize**, and manipulate **objects** in Python, we **use classes**. They serve as **templates**  from which objects are created

**Class** is a blue print for the **objects** of the class, every **instance object** we create from that class just has the same structure as defined in the class.

A **class** defines and structures all of the objects that are created from it. You can view the class as an **object factory**.

` `Classes use **methods and constructors** to create and define objects.

Name of a class has CamelCase structure

Methods are functions within a class that are designed to perform a specific task. Python differentiates between **user-defined methods**, written by the programmer, and **special methods** that are built into the language. 

**Special methods are identified by a double underscore at either side of their name, such as \_\_init\_\_.** Python uses special methods to enhance the functionality of classes. Most of them work in the background and are called automatically when needed by the program.

You cannot call them explicitly. For instance, when you **create a new object**, Python **automatically calls the \_\_new\_\_ method**, which in turn **calls the \_\_init\_\_ method.**

A constructor is a special method that the program calls upon an object’s creation. The constructor is **used in the class to initialize data members** to the object. 

**The \_\_init\_\_ method** is the Python equivalent of the [C++ constructor](https://www.udacity.com/blog/2021/03/what-is-a-constructor-in-c.html?utm_source=rss&utm_medium=rss&utm_campaign=what-is-a-constructor-in-c) in an object-oriented approach. The \_\_init\_\_ method lets the class initialize the object’s attributes and serves no other purpose. 

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.013.png)	This is just the parent class, that here is the class object

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.014.png)**class** Dog (object)**:**

`       `species = ‘mammal’   --à this is a class object **attribute** that is not connected to self or a specific class instance but is true for **any class instance (**مثلا تمام سگ های ک تعریف میکنیم فارق از نوع پستاندار هستند**)**

for class object **attributes** we can say **Dog. Species** instead of **self. Species** while this attribute is the same for all the instances of the class

`       `Def  **\_init\_**  (**self** , att1 = 2, att2):  

`              `**self**.**att1** = att1

`              `self.att2 = att2

`   `---à att1, att2 are **user defined attributes** that are connected to self , a class instance, they are just for user defined attributes while it wants to take the value from user

Self just refers to the current instance of the class 

`     `Def bark(**self** , number): 

`  `Print(“my name is {} and the number is {}”.format(**self**.name , number))

` `--à this number is just an argument that user provided, not related to self or attributes..



**\_init\_**   ---à this **Method** is a constructor for the class that is called automatically when an instance object is created and it takes **user defined attributes** as parameters from the user and assign it to attributes of the class

Self ---à is like **This** in java , it refers to a current instance of the class

Self.name  -à it refers to the name of the current instance of class Dog

my\_dog = Dog(att1,att2)   ---à **creating** an **instance object**

my\_dog.att1 

mydog.bark(number) --à it returns the name of this particular obejct

Difference of **method** and **function :** methods are function defined in a class and it is the action of the object, the way we interact with objects and change them

**Dir**(object name) -à returns a list of methods of the object passed

**Inheritance**

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.015.png)A new class can inherit from a previously defined class 

Class Animal():

`       `Def \_\_init\_\_(self):

`               `Print(“”)

`       `Def eat(self):

`             `Print(“”)

`       `Def who\_am\_i(self):

`  `Print(“”)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.016.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.017.png)	This means that the class Dog inherits from class Animal

Class Dog(**Animal**):

`       `Def \_\_init\_\_(self):

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.018.png)              Animal**.\_\_init\_\_**(self)

`              `Print(“”)	

`	`Here we actually create an instance of animal class when we are creating an instance of Dog class

So when we inherit from another class we can use the methods of that class without need to define them again **and** we can also **override a method** if we want **or** we can add **new methods**

When we define the method again in the new class actually override it , then it uses the new method not the last one in another class

**Polymorphism**

Is one of the key concepts of OOP.

In word it means something happens in different forms

In Programming we have two types of polymorogims : static  / dynamic

- **Static** = method overriding

In a same class we have methods with same name but different parameters and the functionality is similar but have some differences

So we can do an action in different ways

- **Dynamic**

  When we inherits from a previously defined class , we have methods with same name and parameters but different functionality, it means that the methods f superclass has been customized to be used in subclass

  So fore example we have class Animal with subclassed Dog and Cat

  All of these classes have the method animal\_sound() But with different functionality or sound of the specific animal

  **Abstract class**

  An abstract class is never expected to be instantiated or make an instance of the class, actually it is just a base class that other classes can inherit from it and override methods

  Fore example Animal class is an abstract class  and is not expected to be instantiated , is just a base class for other class animals

  Class Animal():

  `         `Def \_\_init\_\_(self):

  `                `Print(“”)

          

  `         `Def speak(self):

  `                 `**Raise NotmplementedError** (“subclass must implement this abstract method”)	

  ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.019.png)actually this method is never

  expected to be instantiated therefore we are not going to define it here, we should inherit this method in a newly defined subclass

  **special** **methods**

  def **\_\_str\_\_**():

  ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.020.png)       return **f** ”{self.title} by {self.writer}”

  this method is a special method that **returns a string representation of the class**

`	`this f is used when we want to replace variables with value in a string

so when we what to print(b) actually print an object of the class it uses the special method of string representation to print it.

def  **\_\_len\_\_**():

`       `return self.pages

**Exception Handling:**

An exception is an error that occurs during the execution of code. This error causes the code to raise an exception and if not prepared to handle it will halt the execution of the code.

A **try except** will allow you to execute code that might raise an exception and in the case of any exception or a specific one we can handle or catch the exception and execute specific code. This will allow us to continue the execution of our program even if there is an exception.

Python tries to execute the code in the **try block**. In this case if there is any exception raised by the code in the try block, it will be caught and the **code block in the except** block will be executed. After that, the **code that comes after the try except** will be executed.

try:

`    `# code to try to execute

except: 

`  `// it is not specific except and will caught any error that will comes

`    `# code to execute if there is an exception



\# code that will still execute if there is an exception

try:

`    `# code to try to execute

except (ZeroDivisionError, NameError):

`    `# code to execute if there is an exception of the given types



\# code that will execute if there is no exception or a one that we are handling

\----------------------------------------------------------------------------

try:

`    `# code to try to execute

except ZeroDivisionError:

`    `# code to execute if there is a ZeroDivisionError

except NameError:

`    `# code to execute if there is a NameError



**else**  allows one to check if there was no exception when executing the try block.

try:

`    `# code to try to execute

except ZeroDivisionError:

`    `# code to execute if there is a ZeroDivisionError

except NameError:

`    `# code to execute if there is a NameError

except:

`    `# code to execute if there is any exception

else:

`    `# code to execute **only if** there is no exception

\# code that will execute if there is no exception or a one that we are handling


**Finally**  allows us to always execute something even if there is an exception or not. This is usually used to signify the end of the try except.

try:

`    `# code to try to execute

except ZeroDivisionError:

`    `# code to execute if there is a ZeroDivisionError

except NameError:

`    `# code to execute if there is a NameError

except:

`    `# code to execute if ther is any exception

else:

`    `# code to execute only if there is no exception

finally:

`    `# code to execute at the end of the try except no matter what



\# code that will execute if there is no exception or a one that we are handling



Most important libraries in machine learning in python :

**Pandas** : library for data analysis

**Numpy**: library for numerical computing

**Matplotlib**: library for visualizsation

**Skicit-learn :**


**Pandas**

Is a popular library for **data analysis**

**Import** panda 

csv\_path = ‘file1.csv’

we should put our data file in our current working directory in order to be able to access it through only its name

but we can also change our current working directoy to the place where our data is located with the function os.chdir()

\*\* os is a nodule in python for interacting with filesystem

To figure out what is our current working directory we can use os.getcwd()

df = Pandas.**read\_csv (**csv\_path**)**                df--à dataframe

dataframe is comprised of rows and columns

A Pandas DataFrame is a 2 dimensional data structure, like a 2 dimensional array, or a table with rows and columnss

we can create a dataframe out of dictionaries 

the keys correspond to column lables and the values correspond to rows

songs = {Album : [‘Thriller’,’back in black’]}

pandas.Dataframe(songs) -à create rows and columns from that dictionary

dataframe has some methods:

len(df) -à number of rows

df.head() -à gives the first 5 rows of file

y = **df**[[‘Artist’,’length’,’type’]] -à it will create a new dataframe from existing, that just contains these three columns

df.tail() shows us the last 5 rows of dataset

df.describe() shows us some brief statistical information(e.g  count,mean,min, max value, ….) for numerical columns 

df.columns() shows the column names of the dataset

we can select an individual column by df [‘column name’] or multiple columns df [[ ‘id’, ‘name’]]

df [‘name’].value\_counts()  shows how many values exists in a column

df.sort\_values(by = ‘Age’)  it sorts dataframe based on the given column


df[‘released’].**unique** -à just returns all of the unique elements in the column of released  /// df here is just the name of our dataframe

df1 = df[df[‘released’]>=1980] à **create a new dataframe** that release dates are > 1980

df.**to\_csv**(‘new songs.csv’) à this method just save our dataframe to a csv file (csv : comma separated file)

**df.ix[0,0]**   à access the first row and column of a dataframe

import pandas

mydataset = {
`  `'cars': ["BMW", "Volvo", "Ford"],
`  `'passings': [3, 7, 2]
}

myvar = pandas.DataFrame(mydataset)

A Pandas Series is like a column in a table.

Create a simple Pandas Series from a list:

import pandas as pd

a = [1, 7, 2]

myvar = pd.Series(a)

print(myvar)

print(myvar[0])

**Loc & iLoc :**

For filtering out the data we use loc and iloc

**Loc** : loc is label-based, which means that we have to specify the name of the rows and columns that we need to filter out.

For example, let’s say we search for the rows whose index is 1, 2 or 100.

So, we can filter the data using the loc function in Pandas even if the indices are not an integer in our dataset.

This method includes the last element of the range passed in it, unlike iloc(). loc() can accept the boolean data unlike iloc() .

**data.loc**[data.age >= 15]

**data.loc**[(data.age >= 12) & (data.gender == 'M')]

**s2.loc**['c':'e']  # all rows lying between 'c' and 'e'

**s2.loc**[1:3]  # all rows lying between 1 , 3



**iLoc** : On the other hand, iloc is integer index-based. So here, we have to specify rows and columns by their integer index.

\# selecting 0th, 2th, 4th, and 7th index rows

display(data.iloc[[0, 2, 4, 7]])

|<p># selecting rows from 1 to 4 and columns from 2 to 4</p><p>display(**data.iloc**[1 : 5, 2 : 5])</p><p>df.loc['c': , :'z']  # rows 'c' and onwards AND columns up to 'z'</p><p></p><p>**df.iloc[:, 3**]        # all rows, but only the column at index location 3</p><p></p>|
| :- |


Pandas use the loc attribute to return one or more specified row(s)

Return row 0:

#refer to the row index:
print(df.loc[0])

Return row 0 and 1:

#use a list of indexes:
print(df.loc[[0, 1]])

When using [], the result is a Pandas DataFrame

**index**

With the **index argument**, you can name your own indexes.

import pandas as pd

data = {
`  `"calories": [420, 380, 390],
`  `"duration": [50, 40, 45]
}

df = pd.DataFrame(data, index = ["day1", "day2", "day3"])

print(df) 

Result: 

`      `Calories    duration

Day1     20             30

Day2      30            70

Load the JSON file into a DataFrame:

import pandas as pd

df = pd.read\_json('data.json')

JSON = Python Dictionary

If your JSON code is not in a file, but in a Python Dictionary, you can load it into a DataFrame directly

Extracting data in different file formats like csv, xml, json using python libraries : 

![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.021.png)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.022.png)![Diagram

Description automatically generated with low confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.023.png)

in order to have the first row of our table as headers, we specify headers in this format**


![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.024.png)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.025.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.026.png)json files are like python dictionaries

panda library does not have an attribute to read xml files so

![Graphical user interface

Description automatically generated with medium confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.027.png)

![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.028.png)



**Merge function** in padas

Df = Pandas.merge(df1 , df2 , how=”left” , on =”key”)

- inner: the default join type in Pandas merge() function and it produces records that have matching values in both DataFrames
- left: produces all records from the left DataFrame and the matched records from the right DataFrame
- right: produces all records from the right DataFrame and the matched records from the left DataFrame
- outer: produces all records when there is a match in either left or right DataFrame


If you want to set the data type for the DataFrame columns

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.029.png)pd.read\_csv('data/data\_7.csv',
**dtype ={
'Name': str,
'Grade': int
}**)

` `Replace a **value** with new values for an **individual** DataFrame column:

df['column name'] = df['column name'].replace(['old value'],'new value')

df['column name'] = df['column name'].replace(['1st old value','2nd old value',...],['1st new value','2nd new value',...])

**Pivot tables** 

Excel pivot tables have 4 sections: Rows, Columns, Values, and Filters. 

When you drag a numerical field to values, Excel defaults to sum of that field. When you drag a word-based field to values Excel counts its quantity.

![Text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.030.png)


![Graphical user interface, application, table

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.031.png)

Pandas **pivot table**:

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.032.png)                                     row

pd.pivot\_table(df,index=["Manager","Rep"],values=["Price"],aggfunc=np.sum)

pd.pivot\_table(df,index=["Manager","Rep"],values=["Price"],

`               `columns=["Product"],aggfunc=[np.sum])

We can also fill missing values using the *fill\_value* parameter.

table = pd.pivot\_table(df, values='D', index=['A', 'B'],

**...**                     columns=['C'], aggfunc=np.sum, fill\_value=0)

pvt.sort\_values(by=('AMOUNT\_EUR', 'Auth'), ascending=False, inplace=True)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.033.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.034.png)

pd.pivot\_table(df[(df['CHARGEBACK\_ORDER']==1)], index='CUSTOMER\_ID', aggfunc={'PSP\_REFERENCE': len, 'AMOUNT\_EUR': np.sum})

reset\_index just simply remove index in pivot table and give us a plain dataframe

pvt.reset\_index

**Data cleaning** 

means fixing bad data in your data set.

Bad data could be:

- Empty cells
- Data in wrong format
- Wrong data
- Duplicates

**NULL values**

NA and Null are both to represent missing or not defined values

**df.isnull**()  -à returns null values **as series** of false and true

- **df[ df.isnull() ]  -à** return dataframe of null values

**df.notnull**() --à return not null values

**df.notna**() -à return not NA values

**Remove null values:**

- **df =** df[ **~** df[‘Age’].isnull() ]![ref1]
- df = df.dropna()

By default, the **dropna()** method **returns a *new* DataFrame**, and will not change the original.

If you want to change the original DataFrame, use the **inplace = True** argument

**Remove all rows with NULL** values:

**df.dropna(inplace = True)**


Another way of dealing with empty cells is to insert a *new* value instead.

The fillna() method allows us to replace empty cells with a value

**Replace NULL values with** the number 130:

**df.fillna(130, inplace = True)**

To **only replace empty values** for one column, specify the *column name* for the DataFrame:

Example

Replace NULL values in the "Calories" columns with the number 130:


**df["Calories"].fillna(130, inplace = True**)

A common way to replace empty cells, is to calculate the mean, median or mode value of the column.

Calculate the MEAN, and replace any empty values with it:
x = df["Calories"].mean()

df["Calories"].fillna(x, inplace = True)



**Replace non-numeric values with NAN :**

First convert all values to numeric , if it is possible replace it with NAN

df[‘age’].apply(**pd.to\_numeric()** , **errors** = ‘coerce’)    -à errors = coerce will replace with NAN in case   

`                                                                                                     `of non possible to convert to numeric

we can use apply to apply a method to the whole dataframe

**enumerate function :**

for **idx, k** in **enumerate**(keys):

df.loc[df["Your main technology / programming language"] == k, "Your main technology / programming language"] = idx


**fix wrong format data:**

Cells with **data of wrong format** can make it difficult, or even impossible, to analyze data.

To fix it, you have two options: remove the rows, or convert all cells in the columns into the same format

Convert to date:

df['Date'] = pd.to\_datetime(df['Date'])

One other way to deal with empty values is simply removing the entire row

Remove rows with a NULL value in the "Date" column:

df.dropna(subset=['Date'], inplace = True)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.036.png)replacing a wrong value in a dataset

Set "Duration" = 45 in row 7:

df.loc[7, 'Duration'] = 45

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.037.png)To replace wrong data for larger data sets you can create some rules

Loop through all values in the "Duration" column.

If the value is higher than 120, set it to 120:

for x in df.index:
`  `if df.loc[x, "Duration"] > 120:
`    `df.loc[x, "Duration"] = 120

Delete rows where "Duration" is higher than 120:

for x in df.index:
`  `if df.loc[x, "Duration"] > 120:
`    `df.drop(x, inplace = True)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.038.png)Returns True for every row that is a duplicate, othwerwise False:

print(df.duplicated())

Remove all duplicates:

df.drop\_duplicates(inplace = True)


![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.039.png)correlation between columns

The corr() method calculates the relationship between each column in your data set.

df.corr()

The Result of the corr() method is a table :

`	    `duration       calories

duration      1.0              0.8

calories       0.9	1.0

1 means that there is a 1 to 1 relationship (a perfect correlation), and for this data set, each time a value went up in the first column, the other one went up as well.

0\.9 is also a good relationship, and if you increase one value, the other will probably increase as well.

-0.9 would be just as good relationship as 0.9, but if you increase one value, the other will probably go down.

0\.2 means NOT a good relationship, meaning that if one value goes up does not mean that the other will. Can not predict

**Numpy**

Is a library for scientific computations

**Numpy array** : is like a list , fixed in size , each element of the same type

Import numpy  (or we can use alias import numpy as np)

We can create an array from a python list or tuple

A = numpy.**array**([1,2,3,4])           1d array

B = numpy.array ([1,2,3] , [3,4,5])              2d array

A[0] = 100 -à change the first element of array

A[0,1]      à second element of first dimention

D = A[1:4] -à slice the nympy array and assign the elements to a new numpy array

A[2:]         à from second until end

A[1,2] = 200,300 à change the values of element index 1 until 2

A[-1]    à gives the last element

**A[0][0:2**]    ---à   Access the element on the first row and first and second columns.


a = [[1,2,3],[2,3,4]]

b = np.array(a)        -à b= [1 2 3     --à 2d array

`                                                `2 3 4]

A[0][0] = 1

A.size à number of elements in array

A.dtype -à type of each element of the array = dtype(‘float64’)

A.ndim à shows the number of dimensions

A.shapeà shows the shape of array    (3,5) = 3\*5

type(A) ànumpy.ndarray 

below we create an array called arr with 15 elements (0,1,2,… 15) and then reshape it into 3\*5 array

arr = numpy.arange(15).reshape(3, 5)

aggregate functions in numpy

numpy.sum(A)

numpy.mean()

numpy.variance()

……….

![ref2]

for n,m in zip(u,v)

z = []

z.append(u+v) -à it just add two lists and put it in list z

![ref2]we can do the above with numpy arrays but it is much faster this way

u= np.array[1,0]

v= np.array[0,1]    ----à numpy arrays are much faster than lists

z = u+v    /  z= u\*v   / z= np.**dot**(u,v)  / z = u+1

u = np.array[0,1]

u.**mean**() -à compute the average pf all elements in the array /// u.**max**()  /// y = np.sin(x)

![ref2]

u= np.array[1,0]

z = 2\* u

**np.random.randint**(0,255)  --à generate a random number between 0 and 255

list = [1 ,2 ,3 , 5, 6]

**np.random.choice**(list , replace = True) -à pick a random number from a list of numbers ,

`                                                                              `the list must be one dimentional

DSS

a dataframe **column** is a **series** , that is actually **a list**

x = x - **np.mean(x)**     --à this will subtract each item of the list from the mean value of the list

**np.dot(x ,y**)    -à **dot product of two lists (vectors)** will be equal to np.sum(x\* y)

**np.sqrt**(x \*\* 2)   --à power of 2 equals to x \*\* 2

**np.sum**(x)   -à it will sum all values of a list together


**Matplotlib**

It is a library for visualization of data

**Plots**

Pandas uses the **plot()** method to create diagrams.

We can use **Pyplot, a submodule of the Matplotlib library** to visualize the diagram on the screen

import pandas as pd
import matplotlib.pyplot as plt

**Plt.plot**([1,2,3,4])            we want to draw this list

**Plt.ylable**(“random numbers”)

**Plt.xlabel**(“here lies the x”)

**Plt.show**()

**Plt.axis**([5,10,6,20])    à specifying min and max for axes  -à xmin,xmax,ymin,ymax

**plot distribution of one column :**

**Histogram:**

- df[‘age’].**plot.hist**(bins = 50)   -à bins is the number of bins

  plt.xlable(‘Age’)

  plt.show()

**Boxplot :**

**With pandas:**

- boxplot\_plt = df[‘Age’].**plot.box**() -à also show outliers in the plot
- df[‘Age’].plot.box ( **showfliers = False** , return\_type = ‘dict’) -à this will not show the outliers in the plot

  plt.show()

**with matplotlib:**

- boxplot\_pd = **plt.boxplot**(df[‘Age’] , showfliers = False)



boxplot\_plt  or boxplot\_pd **returns** us a **dictionary** like below![Text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.041.png)

each of these keys contain **values** consist of **(x,y) data**

**\*get\_xdata** and **get\_ydata** will return us the x and y values of our plot

Now based on this dictionary, we can **get the whiskers value:**

With the whiskers value we can figure out if a value is outlier or not  -à if it is smaller or larger than whiskers

![Text

Description automatically generated with medium confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.042.png)

so the **whiskers are located at 0 and 22** (years)

5 and 12 are quartiles values (Q1 , Q3)

Mathematically : we can calculate whiskers as below

Lower\_limit\_whisker = Q1 – (Q3 – Q1)\* 1.5 ---à here = 0

Upper\_limit\_whisker = Q3 + (Q3 – Q1) \* 1.5   --à here = 22

So inorder to remove outliers we must consider data only between 0 and 22


![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.043.png)**What is a boxplot ?**	



![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.044.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.045.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.046.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.047.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.048.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.049.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.050.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.051.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.052.png)  **![Chart, box and whisker chart

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.053.png)**

Boxplot shows that **50% of our data** are lying in that **box** (in the interval of Q1 and Q2)

When the box is small it means the distribution of the data is dense around one point

It can also shows us how data is skewed to the left , right or it has a normal distributin

**Bar plot   :** is for visualizing categorical data

<a name="_hlk119832059"></a>majors=["mechanical eng.","civil eng.","electrical eng."]

values=[213,178,256]

**plt.bar**(majors, values)

plt.ylabel("majors")

plt.show()

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.054.png)


![ref1]![ref1]**Scatter plot :**

- ` `**df.plot(kind = 'scatter', x = 'Duration', y = 'Calories')**
  ` `plt.show()


- **plt.figure**(figsize=(12, 5))  -àspecify the diagram size (the size of the diagram image )

  **plt.scatter**(df['Total years of experience'] , df['Age'])  (here we are using matplotlib for plotting)

  **plt.xticks**(rotation = 60)  -à rotate x lables

  **plt.ylabe**l("Age"); **plt.xlabel**("Total years of experience")

  **plt.xlim**(0, 100)     --à limit x values to only [0 - 100] interval

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.055.png)

- notes=[1,2,3,4]
- student\_numbers=[22,45,55,34]
- plt.scatter(notes, student\_numbers)
- plt.ylabel("#students")
- plt.xlabel("notes")
- plt.axis([0,5,0,75])
- plt.show()


**value\_counts()7**

df[‘Gender’].**value\_counts()**   --à for a categorical attribute , gives us the number of rows of each category

1. df[‘languages’].**values**   --à return all values of one column

**Pie Chart**

df[‘Gender’].value\_counts()[0:5].**plot(kind = ‘pie’)**    (here we are using pandas for plotting)




**Summary :**

- **using pandas library for plotting**

  df[‘ ’].plot.box()

  df[‘ ’].**value\_counts().**plot(kind = ‘ bar / pie / ..’)

- **using matplotlib library for plotting**

  plt.bar()

  plt.scatter()


**Correlation**

We can compute correlation between two variables with two methods :

- Pearson
- Spearman

- From scipy.stats import **pearsonr , spearmanr**
- corr, p\_value = **pearsonr**( df['Age'], df['Total years of experience'] )
- corr, p\_value = **spearmanr**( df['Age'], df['Total years of experience'] )

these two methods returns us the correlation coefficients

**APIs**

Application program interface

How your weather app get the todays weather forecast? How your tandem app lets you to login through your facebook account?

Actually they talk to other systems / softwares to get data or verify your credentials through APIs

Actually we can not access the internals of a system, we can only talk to the layers of API to get data / APIs just provides us with rules that are needed to interact with another software to get data

APIs are just like waiters in a restaurant , an interface between you and the kitchen

An API lets two pieces of software talk to each other. Just like a function,  you don’t have to know how the API works only its inputs and outputs.

APIs have **End points** that are point of contacts for us to submit our inputs to access data/ endpoints are only URLs that provide the data that we want

[http://vidly.com/**api**/customers](http://vidly.com/api/customers) ---> this is the endpoint to access and work with our customers data

For each endpoint there is some protocols that says which inputs are required and what you will get as a result / if u do not provide the correct inputs , your request will get rejected

You also have to supply an API key , that is a unique ID to identify your app, in this way the system has a record of who is accessing to their inputs

**API key** is unique set of characters that a system use to identify you as a client and through that allow access to the API / in the first call we include the API key / for all of the calls you have the same unique API

**Endpoint** is just the location of the service and is used to find the API on the internet / is like a URL

Your app can interact and communicate with different systems through their APIs

Every API has an End point that specifys what it is providing you, has some inputs that you should provide to access the correct data , and you should provide API key that let the service khow who is accessin their system

in our programs we use APIs to communicate with other softwares through input and output , we should only khow the inputs and outputs and not how an API works

**Pandas are set of software components (library)** that are even not written in python, we use **pandas API / panda is a system that has API** to process our data by communicating to set of softwares

When you create a Pandas object with the Dataframe constructor in API lingo, this is an "instance". The data in the dictionary is passed along to the pandas API. You then use the dataframe to communicate with the API.

![Diagram

Description automatically generated with medium confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.056.png)

When you call the method head the dataframe communicates with the API displaying the first few rows of the dataframe.  df.head()

When you call the method mean,the API will calculate the mean and return the value.

We send a request to the API endpoint through **http message that contains json file** and API just brings us the respond from that software via an http message that contains a **json file** 

this json file contains which operations we want the service to perform 

Most of the apps we work with today are working in the architecture of client and server, the app itself is the client (frontend) and it interacts with the server(backend) to get data. This communication happens using HTTP protocole. The client calls the services on server through a http request.

Via http request we talk to the service through http methods , **Get, Post**(create)**, Put** (update)**, Delete** request

**Rest APIs**

Allow us to communicate through internet to use some resources like storage , access data

Rest API’s function by sending a request,  the request is communicated via HTTP message. The HTTP message usually contains a JSON file. This contains instructions for what operation we would like the service or resource to perform. In a similar manner, API returns a response, via an HTTP message, this response is usually contained within a JSON.

Rest APIs are used to interact web services / applications that we call through internet / your program or application is the client

**Http Protocols** are general protocols for transferring info through web

When you as a client use a webpage , your browser send an http request to the server that hosting this webpage, then the server will send a response as form of http to the client

**URL** = uniform resource locator

Is the most popular way to find a resource on the web

The URL consist of three parts :

1. Scheme : this is the protocol , http:// or https://
1. Internet address or base URL : will be used to find a location , [www.gitlab.com](http://www.gitlab.com)
1. Route : the location on that webserver

   <http://www.ibm.com/images/IDSNlogo.png>

   **http request** :

   When you, the **\*\*client\*\***, use a web page your browser sends an **\*\*HTTP\*\*** request to the **\*\*server\*\*** where the page is hosted. The server tries to find the desired **\*\*resource\*\*** by default index.html. If your request is successful, the server will send the object to the client in an **\*\*HTTP response\*\***. This includes information like the type of the **\*\*resource\*\***, the length of the **\*\*resource\*\***, and other information.

   this tells the server what action to perform.

   ![Text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.057.png)

   ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.058.png)Also http method Get, the location of the resource  /index.html and the HTTP version.

   ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.059.png)![Table

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.060.png)	








   ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.061.png)![ref3]**http response**:	this 200 is the status code

   ![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.063.png)![Table

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.064.png)





This html file is the info that was requested





**Status codes**: ![Table

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.065.png)

Anythingg in 100 means everything is ok so far  / ‘’ In 200 means the request was successful / ‘’ In 400 means bad news

![Table

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.066.png)

**Request module in Python** has some libraries to work with http requests.

**Requests** is a library in python that let us to send http requests

![Graphical user interface, text, application, email

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.067.png)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.068.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.069.png)r is the response object.

This is a dictionary of response headers
![Graphical user interface, text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.070.png)

![Graphical user interface, text, application, email

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.071.png)

**Query string :**

**query string** is a part of a uniform resource locator (URL), this sends other information to the web server. The start of the query is a **?** , followed by a series of parameter and value pairs, as shown in the table below. The first parameter name is **name**  and the value is **Joseph**. The second parameter name is ID and the Value is 123 . Each pair, parameter, and value is separated by an equals sign, **=** .The series of pairs is separated by the ampersand <code>&</code>.

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.072.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.073.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.074.png)![Calendar

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.075.png) this is a get request

To create a Query string, add a dictionary. The keys are the parameter names and the values are the value of the Query string.

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.076.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.077.png)Here  r is the response ---à r = requests.get()

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.078.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.079.png)![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.080.png) 

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.081.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.082.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.083.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.084.png)![ref3]![Text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.085.png)we deal with http response as text
![Text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.086.png) deal with http response as json file format that returns a python dictionary






![ref3]**post request**

r\_post=requests.post(url\_post,data=payload)

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.087.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.088.png)![ref3]![Graphical user interface, text

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.089.png)

**Html**

![ref1]![ref1]![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.090.png)![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.091.png)html** tree  : each tag has children and they form a tree![A piece of paper with writing on it

Description automatically generated with medium confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.092.png)html table


**Webscraping**

Automatically extract data rom a website through request and beautiful soup libraries in python

We can extract info form web pages by webscraping

Html pages composed of html tags 

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.093.png)Each tag  has attributes      <a     href= “”    >    content     </a>

![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.094.png)we make a beautiful soup object and store out html data in this object

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.095.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.096.png)the html data can be stored in a string or can be downloaded via request from web

We can do this by using beautiful soup library

The beautiful soup object represent our htm document as a nested data structure (tree)

With this soup object we can access html tags in our document

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.097.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.098.png)![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.099.png)

![Diagram

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.100.png)

Accessing the upper tag by using parent attribute

Patent\_tag = child\_tag.parent

Accessing a sibling of an object by using sibling attribute

Sibling = tag\_object.next\_sibling

Accessing attributes of a tag

Tag\_object.attrs   à give us all the attributes of a tag as a dictionary

Accessing content of a tag

Tag\_object.string

Find\_all method : it works as a filter on tags

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.101.png)![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.102.png)![Graphical user interface, text, application

Description automatically generated](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.103.png)

Here above table is a soup object and we search for tags with name <tr> in html document and it returns us a list of tr tags

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.104.png)Here we can also access the list elements by table\_row[0]


**Data Engineering**

There are several steps in Data Engineering process.

1\.  **\*\*Extract\*\*** - Data extraction is getting data from multiple sources. Ex. Data extraction from a website using Web scraping or gathering information from the data that are stored in different formats(JSON, CSV, XLSX etc.).

2\.  **\*\*Transform\*\*** - Tarnsforming the data means removing the data that we don't need for further analysis and converting the data in the format that all the data from the multiple sources is in the same format.

3\.  **\*\*Load\*\*** - Loading the data inside a data warehouse. Data warehouse essentially contains large volumes of data that are accessed to gather insights.

In the real world we mostly do not get the data in a tabular neat format, so as  data scientist or data engineer you should be able to handle different file formats.

File format is just a standard way that the info is encoded in the file in that way, and it first of all specifies , whether a file is binary or ASCII and it shows how the info is organized.

We have **.csv** file (comma separated) à tabular data that is stored as plain text, .**xlsx** files, **.json** file.

**CSV** file formats falls under **spreadsheet** file formats.

In spreadsheet file format , the data is stored in cells, and each cell is organized in rows and columns. In CSV each line is an observation or called record , this record can have different fields that are separated with comma.

To **read a csv** file in python :

Df = Pandas .read\_csv (file\_path, header = none)

a file path can be either a URL or a local file address

**selecting columns :**

df[‘risk’]      #selecting one column

df[[‘risk’, ‘amount’]]     #selecting different columns, we pass  a list of columns

**Selecting rows with Loc and iLoc :**

` `loc() is label based data selecting method which means that we have to pass the name of the row or column which we want to select

\# To select the first row

df.loc[0]

\# To select the 0th,1st and 2nd row of "First Name" column only

df.loc[[0,1,2], "First Name" ]

iloc() is a indexed based selecting method which means that we have to **pass integer index** in the method to select specific row/column.\*\*

\# To select the 0th,1st and 2nd row of "First Name" column only

df.iloc[[0,1,2], 0]

**Transfrom function in pandas :**

Python’s Transform function returns a self-produced dataframe with transformed values after applying the function specified in its parameter.

#applying the transform function : add 10 to each element in a dataframe:

df = df.**transform**(func = lambda x : x + 10)

find the square root to each element of the dataframe :

result = df.transform(func = ['sqrt'])

**JSON file format :**

JSON (javascript object notation) is in form of javascript objects.

JSON is built on two structures:

1\.  A collection of name/value pairs. In various languages, this is realized as an object, record, struct, dictionary, hash table, keyed list, or associative array.

2\.  An ordered list of values. In most languages, this is realized as an array, vector, list, or sequenc

Python supports JSON through a built-in package called \*\*json\*\* , so 

Import json

**Writing json to a file :**

This is usually called **\*\*serialization\*\***. It is the process of converting an object into a special format which is suitable for transmitting over the network or storing in file or database.

serialization using dump() function :

**\*\*json.dump()\*\*** method can be used for writing to JSON file.

Syntax: json.dump(dict, file\_pointer)

Parameters:

1\.  **\*\*dictionary\*\*** – name of the dictionary which should be converted to JSON object.

2\.  **\*\*file pointer\*\*** – pointer of the file opened in write or append mode.

with open('person.json', 'w') as f:  # writing JSON object

`    `json.dump(person, f)

serialization using dumps() function :

**\*\*json.dumps()\*\*** that helps in converting a dictionary to a JSON object.

It takes two parameters:

1\.  **\*\*dictionary\*\*** – name of the dictionary which should be converted to JSON object.

2\.  **\*\*indent\*\*** – defines the number of units for indentation

**Reading JSON to a file :**

This process is usually called \*\*Deserialization\*\* - it is the reverse of serialization. It converts the special format returned by the serialization back into a usable object.

\### Using json.load()

The JSON package has json.load() function that loads the json content from a json file into a dictionary.

import json 



\# Opening JSON file 

with open('sample.json', 'r') as openfile: 



`    `# Reading from json file 

`    `json\_object = json.load(openfile) 



print(json\_object) 

print(type(json\_object)) 

![](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.105.png)import json

person = {

`    `'first\_name' : 'Mark',

`    `'last\_name' : 'abc',

`    `'age' : 27,

`    `'address': {

`        `"streetAddress": "21 2nd Street",

`        `"city": "New York",

`        `"state": "NY",

`        `"postalCode": "10021-3100"

`    `}

}

**Writing to a JSON file**

-self.config is a json file and we are writing that json file into another json file\
-Look how we can specify path for the file

with open(**self.perf_output_dir / "config.json"** , "w") as f:
                json.dump(self.config, f , indent= 4)

**XLSX file format** 

Microsoft excel file format that is another type of spreadsheet file formats.

Pd.**read\_excel**(.xlsx)

**XML file format**

\*\*XML is also known as Extensible Markup Language\*\*. As the name suggests, it is a markup language. It has certain rules for encoding data. XML file format is a human-readable and machine-readable file format.

**Save dataset to different file formats**

<h2>Read/Save Other Data Formats</h2>

| Data Formate |        Read       |            Save |

\| ------------ | :---------------: | --------------: |

| csv          |  `pd.read\_csv()`  |   `df.to\_csv()` |

| json         |  `pd.read\_json()` |  `df.to\_json()` |

| excel        | `pd.read\_excel()` | `df.to\_excel()` |

| hdf          |  `pd.read\_hdf()`  |   `df.to\_hdf()` |

| sql          |  `pd.read\_sql()`  |   `df.to\_sql()` |

| ...          |        ...        |             ... |


**Binary file formats**

"Binary" files are any files where the format isn't made up of readable characters. It contain formatting information that only certain applications or processors can understand. While humans can read text files, binary files must be run on the appropriate software or processor before humans can read them.

Binary files can range from image files like JPEGs or GIFs, audio files like MP3s or binary document formats like Word or PDF.

Reading image file :

![A screenshot of a computer

Description automatically generated with low confidence](Aspose.Words.48d29fe6-1156-4f92-bd62-9a2a1c230013.106.png)

**Data Analysis**

Is a bout obtaining necessary insights from a dataset.

Imagine that we have a diabetes dataset and we want to specify if a patient has diabetes or not based on some medical measurements. In the dataset we have some predictor variables (medical measurements like how many pregnancies she had, her IBM, …) and one target variable (label / has diabetes or has not diabetes)

df.info()  -à information about dataset

df.describe() -à statistical details (mean, standard deviation, ..) for numerical columns

df.dtype()  à to check the type of a column 

df.astype()-à to change the type of a column

df.isnull() -à gives us the missing values in a dataset

**Seaborn** and **Matplotlib** are two of the most important libraries in python for visualization

\# import libraries

import matplotlib.pyplot as plt

import seaborn as sns

labels= 'Diabetic','Not Diabetic'

plt.pie(df['Outcome'].value\_counts(),labels=labels,autopct='%0.02f%%')

plt.legend()

plt.show()

**DSS**

**main function()**

In most programming languages, there is a special function which is **executed automatically every time the program is run.** This is nothing but the main function, or **main()** as it is usually denoted. It essentially serves as a **starting point for the execution of a program**.

In most Python programs/scripts, you might see a function definition, followed by a [conditional statement](https://www.edureka.co/blog/loops-in-python/) that looks like the example shown below:

**def main():**

`    `print("Hello, World!")

`    `**if \_\_name\_\_== "\_\_main\_\_" :**

main()

This kind of code pattern is very common when you are dealing with **files that are to be executed as Python scripts**, and/**or to be imported in other modules.**

it’s very necessary to understand that the Python interpreter sets **\_\_name\_\_** depending on the way how the code is executed.f c


oThere are two main ways by which you can tell the Python interpreter to execute the code:

- The most common way is to execute the file as a Python Script.
- By importing the necessary code from one Python file to another.

When we run a program, the interpreter runs the code sequentially and **will not run the main function if imported as a module, but the Main Function gets executed only when it is run as a Python program**.

As a result, programmers write all the necessary functional definitions on the top, and then define main function to execute this previous functions and finally write this statement at the end (**if \_\_name\_\_== "\_\_main\_\_" :** ), to organize the code.

So, if you are running the script directly, Python is going to assign “**\_\_main\_\_**” to **\_\_name\_\_**, i.e., **\_\_name\_\_**= “\_\_main\_\_”. (This happens in the background) and the condition will happen to be true and it will execute the main function, otherwise not.

**def demo(got):**

`        `print("&amp;hellip;Beginning Game Of Thrones Demo1&amp;hellip;n")

`        `new\_got **=** str.split(got)

`        `print("&amp;hellip;Game of Thrones has finished&amp;hellip;n")

`        `**return** new\_got

`    `**def getgot():**

`        `print("&amp;hellip;Getting GOT Data&amp;hellip;n")

`        `got**=**"Bran Stark wins the Iron Throne n"

`        `print("&amp;hellip;GOT Data has been returned&amp;hellip;n")

`        `**return** got

`    `**def main():**

`        `**got= getgot()**

`        `**print(got)**

`        `**new\_got = demo(got)**

`        `**print(new\_got)**

`    `**if \_\_name\_\_ == "\_\_main\_\_":**

`        `**main()**



de pattern is very common when you are dealing with files that are to be executed as Python scripts, and/or to be imported in kind of code pattern is very common when you are dealing with files that are to be executed as Python scripts, and/or to be imported in other modules.



Learning exprience python

- **How to get the current time stamp :**

from datetime import datetime

now = datetime.now()

dt_string = now.strftime("%d_%m_%Y_%H_%M_%S")

print(dt_string)

- **How to create a text file inside an existing directory and write to it :**

file_path = "C:/Users/Sahel Bloukat/Workspace"

with open(file_path + "/" + "Documents" + "/" + "temp.txt", "w") as f:

f.write("Hi, How are you!")

- **How to create a directory and write to a file inside that :**

file_path = "C:/Users/Sahel Bloukat/Workspace"  
<br/>if not os.path.exists(file_path):  
os.makedirs(path)

filename = img_alt + '.jpg'  
with open(os.path.join(file_path, filename), **'wb'**) as temp_file:  
temp_file.write(buff)

‘wb' : opens a write-only file in binary mode



**Threading :**

A thread is a separate flow of execution. This means that your program will have two things happening at once. But for most Python 3 implementations the different threads do not actually execute at the same time: they merely appear to.

The threads may be running on different processors, but they will only be running one at a time. Getting multiple tasks running simultaneously requires a non-standard implementation of Python, writing some of your code in a different language, or using multiprocessing .Because of the way CPython implementation of Python works, threading may not speed up all tasks. Tasks that spend much of their time waiting for external events are generally good candidates for threading.

This is due to interactions with the GIL that essentially limit one Python thread to run at a time. If your threads are written in C they have the ability to release the GIL and run concurrently.

import threading

x = threading.Thread(target=thread_function, args=(1,))  
x.start()

When you create a Thread, you pass it a function and a list containing the arguments to that function. In this case, you’re telling the Thread to run thread_function() and to pass it 1 as an argument.

In computer science, a daemon is a process that runs in the background.

Python threading has a more specific meaning for daemon. A daemon thread will shut down immediately when the program exits. One way to think about these definitions is to consider the daemon thread a thread that runs in the background without worrying about shutting it down.

If a program is running Threads that are not daemons, then the program will wait for those threads to complete before it terminates. Threads that are daemons, however, are just killed wherever they are when the program is exiting.

**How to start multiple Threads :**

- threads = list()  
    for index in range(3):  
    logging.info("Main : create and start thread %d.", index)  
    x = threading.Thread(target=thread_function, args=(index,))  
    threads.append(x)  
    x.start()

<br/>for index, thread in enumerate(threads):  
logging.info("Main : before joining thread %d.", index)  
thread.join()  
logging.info("Main : thread %d done", index)

**Or better**

There’s an easier way to start up a group of threads than the one you saw above. It’s called a ThreadPoolExecutor, and it’s part of the standard library in concurrent.futures (as of Python 3.2).

- with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:  
    executor.map(thread_function, range(3))

The code creates a ThreadPoolExecutor as a context manager, telling it how many worker threads it wants in the pool. It then uses .map() to step through an iterable of things, in your case range(3), passing each one to a thread in the pool.

The end of the with block causes the ThreadPoolExecutor to do a .join() on each of the threads in the pool. It is strongly recommended that you use ThreadPoolExecutor as a context manager when you can so that you never forget to .join() the threads.

# **Assignment vs Shallow Copy vs Deep Copy :**

copying a list in Python might be trickier than you think. There are 3 ways you can do it: simply using the assignment operator (=), making a shallow copy and making a deep copy.

![](data:image/png;)

So, if you edit the new list, changes will be reflected on the original list.

**Shallow copy**

Let’s look at the easy bits first. Here is how you make a shallow copy. In Python 3, you can use list.copy(). However, I prefer the equivalent expression list\[:\] because it works in both Python 2 and 3.

Shallow copy is different from assignment in that **it creates a new object**. So, if you make changes to the new list, such as adding or removing items, it won’t affect the original list.

You might think making a shallow copy is simple, **BUT** here is the tricky part. If the original list is a compound object (e.g. a list of lists), the elements in the new object are **_referenced_** to the original elements. (which is why it is called a shallow copy). So, if you modify the _mutable_ elements like lists, the changes will be reflected on the original elements.

**a = \[\[1, 2\], \[2, 4\]\]**  
**b = a\[:\] ## shallow copy**

The **deep copy** is different from shallow copy in that the copied elements have their own pointers and are not referenced to the original elements. Therefore, **no matter how you modify the deep copy, the changes will NOT be reflected on the original list.**

Creating a deep copy is slower, because you are making new copies for everything. You will need to import copy module to make a deep copy.

**a = \[\[1, 2\], \[2, 4\]\]>> import copy**  
**\>> b = copy.deepcopy(a) ## deep copy**










