# Entity Relationship Diagram

![ER diagram](./img/1.png ':size=400')

The main component of an Entity Relationship diagram is the `TABLE` component, Table components can connect to other tables via different types of connectors.

## Table
Visually, each table consists of a display name and a set of attributes.


To define a table:

```
TABLE "TableNameA" as TableA:
"some_attribute"

TABLE "TableNameB" as TableB:
"some_attribute"

TableA-TableB
```
Where _TableNameA_ is the display name of the first table.
_TableA_ is the unique identifier of the first table and is used as a reference to connect with other tables.

Each table can contain multiple attributes. To define the attributes of a table they should be declared with quotes `""` after the colon `:`, and each attribute should be separated by a new line:

```
TABLE "TableNameA" as TableA:
"some_attribute"
"other_attribute"

TABLE "TableNameB" as TableB:
"some_attribute"
"other_attribute"

TableA-TableB
```

## Table  Relationships

To create a relationship with another table we use the _connector_ operator `-` which represents the simplest relation:  
```
TableA-TableB
```
![ER diagram relations](./img/2_TableRelationships.png ':size=483')


### Relations with Explicit Types

You can specify the type of relations at both ends of the relationship by following the syntax: 
```
TableA-TableB:(relationTypeA,relationTypeB)
```
where relationTypeA is the type of connector at the first table side and relationTypeB is the type of connector at the second table side, relationType can be any of the supported relation types (check the table below for reference) for example:

`TableA-TableB: (One,Many)`

![ER diagram relations](./img/3_TableRelationships.png ':size=483')


### List of Connectors:

| Connector  | Description  |  Graphic  |
|---|---|---|
|`One` | One to One |![One to One](./img/6.png ':size=25') |
|`OneOnlyOne`|   One and only one |![Only One](./img/OneOnlyOne.png ':size=25')|
|`Many`|   Many | ![Many](./img/Many.png ':size=25') |
|`ZeroOrOne`|  Zero or One | ![Zero or One](./img/ZeroOrOne.png ':size=25')  |
|`ZeroOrMany`| Zero or More  | ![Zero or More](./img/ZeroOrMore.png ':size=25') |
|`OneOrMany`| One or More  | ![One or More](./img/OneOrMore.png ':size=25')|

### Table Relationships with Cardinality Labels:

You can specify cardinality on the source and destination connectors by specifying  `["any_text","any_text"]` after the relationship definition:

```
TABLE "TableNameA" as TableA:
"some_attribute"
"other_attribute"

TABLE "TableNameB" as TableB:
"some_attribute"
"other_attribute"

TableA-TableB: (One,Many)["1..","1.."]
```
![ER diagram relations](./img/11.png ':size=483')

### Attributes as Primary Keys or Foreign Keys (PK and FK)

Each attribute can be preceded with the special keyword `PK` or `FK` to declare the attribute as a primary key or a foreign key respectively, this will automatically add a key icon identifier next to the attribute name definition:


```
TABLE "TableNameA" as TableA:
PK"some_attribute"
FK"other_attribute"

TABLE "TableNameB" as TableB:
PK"some_attribute"
FK"other_attribute"

TableA-TableB: (One,Many)["1..","1.."]
```
![ER diagram relations](./img/12.png ':size=483')


## Reference Example 

![ER diagram relations](./img/1.png ':size=483')


```
#table definitions
TABLE "Country" as Country:
PK"country_id"
"name"
"latitude"
"longitude"
"code"

TABLE "Person" as Person:
PK"person_id"
FK"company_id"
FK"country_id"
"dni"
"address"
"firstname"
"secondname"
"lastname"
"birthday"

TABLE "Company" as Company: 
PK"company_id"
"nit"
"name"
"address"
"type"
"location"

TABLE "Product" as Product:
PK"product_id"
FK"product_type"
"product_name"
"available"

TABLE "Product Categories" as ProdCategories:
PK"product_id"
FK"product_type"
"product_name"
"available"

TABLE "Supplier" as Supplier:
PK"company_supplier_id"
"name"
"address"
"type"
"location"


#table relations

# a simple one to one relation
Person-Country

# dual relations
Person-Company: (ZeroOrMany,ZeroOrOne)

# dual relations with cardinality
Supplier-Product: (One,One)["1","1"]
Company-Product: (One,Many)["1","*"]
Product-ProdCategories: (One,OneOrMany)["1","1.."]


```

