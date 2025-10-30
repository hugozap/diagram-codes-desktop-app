# Class Diagram

![Class diagram](./img/1.png ':size=400')

The main component of the class diagram is the `CLASS` component, `CLASS` components can connect to other class components via different types of connectors.

## Class
Visually each class consists of a display name, a set of attributes, and a set of methods.

To define a class:

```
CLASS "First Class Name" as FirstClass:
"some_attribute"
```

![Class diagram](./img/2_2.png ':size=140')

Where _First Class Name_ is the display name of the class.
_FirstClass_ is the unique identifier of the class and is used as a reference to connect with other classes.

Each class can contain multiple attributes. To define the attributes of the class they should be declared with quotes `""` after the colon `:`, and each attribute should be separated by a new line:

```
CLASS "First Class Name" as FirstClass:
"some_attribute"
"other_attribute"
```

![Class diagram](./img/3_3.png ':size=140')

### Method definition
You can explicitly define methods and attributes inside a class, to do so you need to specify the  `-` symbol when defining an attribute and a `+` symbol when defining a method, you can do it in any order within the class definition, and they will be grouped by method and attributes accordingly.

```
CLASS "First Class Name" as FirstClass:
-"some_attribute"
-"other_attribute"
+"some_method()"
```
![Class diagram](./img/4_4.png ':size=140')

## Class Relationships

To create a relationship with another class we use the _connector_ operator `-`:  
```
CLASS "First Class Name" as FirstClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

CLASS "Second Class Name" as SecondClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

FirstClass-SecondClass
```
![Class diagram](./img/5_5.png ':size=513')


### Class Relations with Explicit Types

You can specify the type of relationship between two classes by following the syntax: 
```
ClassA-ClassB: relationType
```
where _relationType_ defines the type of relation between the two classes.
_relationType_ can be any of the supported relation types (check the table below for reference) for example to define a _dependency_ relation:


```
CLASS "First Class Name" as FirstClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

CLASS "Second Class Name" as SecondClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

FirstClass-SecondClass: dependency
```


![Class diagram](./img/6_6.png ':size=513')


### List of Supported Relation Types:

| Relation Type  | Description  |  Graphic  |
|---|---|---|
| A-B | A and B calls and access to each other |![a](./img/a.png ':size=25') |
|A-B:`association`|   A and B calls and access to each other (same as previous) |![a](./img/a.png ':size=25')|
|A-B:`strict_association`| A calls and access B but not vice versa | ![b](./img/b.png ':size=25') |
|A-B:`composition`| A has a B and B depends on A | ![c](./img/c.png ':size=25')  |
|A-B:`aggregation`| A has B and B can outlive A| ![d](./img/d.png ':size=25') |
|A-B:`dependency`| A depends on B | ![f](./img/f.png ':size=25')|
|A-B:`inheritance`| A inherits B | ![g](./img/g.png ':size=25')|
|A-B:`implementation`| A implements B | ![h](./img/h.png ':size=25')|


### Class Relations with Multiplicity:

You can specify multiplicity at the source and destination points by specifying  `["any_text","any_text"]` after the relation type definition:

```
CLASS "First Class Name" as FirstClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

CLASS "Second Class Name" as SecondClass:
-"some_attribute"
-"other_attribute"
+"some_method()"

FirstClass-SecondClass: composition["0..*","1"]
```
![multiplicity](./img/7_7.png ':size=800')

## Reference Example 

![Class diagram relations](./img/1.png ':size=483')


```
#basic class definition
CLASS "Customer" as Customer:
"name"
"address"
"Customer()"
"EditInfo()"

#basic class definition with field and method grouping
CLASS "Order" as Order:
-"date"
-"status"
+"CalcTax()"
+"CalcTotal()"
+"CalcTotalWeight()"

CLASS "OrderDetail" as OrderDetail:
-"quantity"
-"taxStatus"
+"calcSubTotal()"

CLASS "Item" as Item:
-"shippingWeight"
-"description"
+"getPriceForQuantity()"

CLASS "Payment <<INTERFACE>>" as Payment:
-"ammount"

CLASS "Credit" as Credit:
-"number"
-"type"
+"authorized()"

CLASS "Cash" as Cash:
-"cashTendered"

CLASS "Check" as Check:
-"name"
-"bankId"
+"authorized()"

CLASS "Bill" as Bill:
-"denomination"
-"serial"
+"authorized()"

#class relations reference:
# A-B  (A and B calls and access to each other)  
# A-B: association   (A and B calls and access to each other) (same as previous)
# A-B: strict_association   (A calls and access B but not vice versa)
# A-B: composition   (A has a B and B depends on A)
# A-B: aggregation  (A has B and B can outlive A)
# A-B: dependency    (A depends on B)
# A-B: inheritance   (A inherits B)
# A-B: implementation   (A implements B)

#you can add multiplicity to any relation by adding ["anytext","anytext"] eg:
# A-B: implementation["anytext","anytext"]

#example:
# a simple class relation
Customer-Order

# class relation with explicit type:
Payment-Order: dependency
Credit-Payment: implementation
Cash-Payment: implementation
Check-Payment: implementation

# class relation with explicit type AND multiplicity
Order-OrderDetail: composition["1..*","1"]
Cash-Bill: aggregation["0..*","1"]
OrderDetail-Item: strict_association["0..*","1"]




```

