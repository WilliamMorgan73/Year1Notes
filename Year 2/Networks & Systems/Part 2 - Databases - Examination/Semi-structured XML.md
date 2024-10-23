# Types of data organization
Three characterizations of data
- Structured data
- Semi-structured data (XML)
- Unstructured data

## Structured data
Data represented in a strict format (i.e.., schema)
- The relational data model (tables, tuples, attributes)

The DBMS checks to ensure that the data follows
- The structure (table, attributes, domains)
- The integrity & referential constraints (primary/foreign keys)
That are specified in the schema

## Semi-structured data
data that  
- may be irregular or incomplete and 
- have a structure that may change rapidly / unpredictably  

This data may have some structure, but:  
- not all the parts have the same fixed structure  
- each data object may have different attributes that are not known in advance  

How do we end up with such data?  
- sometimes data is collected ad-hoc  
	- i.e. no predefined structure
	- for instance: details of all research projects  
- not known in advance how it will be stored / managed

Also called self-describing (or schema-less) data:
- Information that normally belongs to a schema, now is contained within the data itself
- The schema information is mixed with the data values

In some cases
- There exists separate schema (or a document type definition - DTD)
- But only places loose constraints on data

## Unstructured data
- Very limited indication of the type/ structure of data
Typical examples:
- A text document with some information within it
- A webpage in HTML that contains some data

Example: a cooking recipe in an HTML document

Flour: 80 cl  
Yeast: 10 grams  
Water: 80 cl (warm)  
Salt: 1 teaspoon  
Attention: Cook for 3 hours

## Semi-structured data
One of the main languages for semi-structured data:
- XML (eXtended Markup Language)
- A language for structuring and exchanging web data

Similarities with HTML
- Hypertext Markup Language
- A language for displaying web pages

Both XML and HTML are "tag" languages

### HTML vs XML
HTML describes the presentation of data
XML describes the content of data (semantics)

### XML data as a graph
XML data have a (directed) tree structure
- Ordering matters
Hierarchical Tree data model

- Internal nodes are elements
- Leafs are raw data (base elements)
- Document node
- Root node


![[Pasted image 20241018165114.png]]

### XML data
XML is self describing
Without a schema
- only the relative position of elements in the tree matters  
•Schema now becomes part of the data  
- it is discovered from the data, not imposed apriori
- Relational schema: person(name, phone) 
- In XML `<person>, <name>, <phone>` are: 
	- part of the data
	- possibly repeated many times (semi-structured data)  

XML is much more flexible

## Why is XML interesting
XML is just syntax for data
- We have no syntax for relational data
- But XML is not relational: semi-structured

This is exciting because we:
- Can translate any data to XML
- can ship XML over the Web  
- can input XML into any application  

easy data sharing & exchange on the Web

### Some advantages of XML

Simplicity:  
- Relatively simple standard, human-legible language and reasonably clear  
Extensibility (unlike HTML):  
- allows users to define their own tags, for their own application requirements  
Platform- and vendor-independent:  
- works with every platform, supports all alphabets  
Separation of content & presentation:
- a “write once – publish anywhere” language
- allows customized view of data (e.g. in browser)  

## Relational data as XML

![[Pasted image 20241018165726.png]]

### XML is semi-structured data
Missing data can be represented with NULLs
Repeated data is impossible in tables
Heterogeneous collections

### Attributes in XML
- a name-value pair with descriptive / identifying information about an element  
- placed inside the start tag of the element  
- attribute value enclosed in quotes “ ”
- an attribute can appear only once within a tag
- but sub-elements can use the same attribute name !
- attributes in XML are not ordered (although elements are):
#### Attributes vs. Sub-elements
Attributes can be replaced by sub-elements

![[Pasted image 20241018170027.png]]

A good rule in practice:
- avoid attributes -> prefer sub-elements 
- unless you need an attribute!  

Disadvantages of attributes:
- cannot contain multiple values (child elements can)
- cannot describe structure (child elements can)  
- more difficult to manipulate by program code 
- not easily expandable (for future changes)  
- not easy to test against a Document-Type-Definition  

Exception to this rule:  
- use attributes to describe metadata
	- (i.e. data about data)

#### Attributes: ID and IDREF
Some attributes can be declared as of type:  
- ID, used as an identifier for the element 
- IDREF, used as a pointer to an element with a specific ID  

If an attribute is explicitly declared as IDREF:  
- its value must be equal to an ID attribute !  

ID and IDREF work in a similar way as primary keys and foreign keys in the relational data model  

the tree representation becomes a directed graph (not necessarily acyclic !)

##### IDREFS:  
- an extension of the IDREF attribute type 
- the attribute value is a string consisting of a list of IDs, separated with a whitespace  
- it links the element to a set of elements (i.e. IDs)

## More useful XML
Comments
```
<!-- -->
```

Cdata
- Character data, containing any text
- Will not be parsed by any XML processor

Entity reference in XML
- To refer to reserved symbols and special characters
- Begins with &
- Ends with ;
- When displayed in a browser it will be replaced. e.g, &...; -> ...
- Reserved symbols:
	- &
	- <
	- >
	- '
	- "

## XML validation
Although XML is self-describing data:  
- we can still impose a more rigorous structure
- e.g. for increased business integration between companies (in B2B solutions)  

In particular:  
- list the permissible element names,
- which elements can appear in combination with which other ones, 
- how elements can be nested, 
- what attributes for which element type, …

Document Type Definition (DTD):  
- concrete set of rules for elements and attributes
- allows seamless data exchange between documents with the same DTD
- appropriate for specific applications, e.g. protein structures, menus in a restaurant…  

XML schema:  
- more powerful than DTD
- allows more complex structures

### Types of XML validation
#### Well formed XML document
- single root element  
- matching tags (properly nested)  
- initial XML declaration

#### Type-valid
- must be well formed and
- the elements / attributes must follow the pre-defined structure, described in the DTD
	- DTD (Document Type Definition):
		- in an extra file, or 
		- embedded within the XML file
#### DTD
General Structure of a DTD: 
```
<!DOCTYPE root_name [  
<!ELEMENT elem_name (subElem1, subElem2, …)>  
… more elements …  
]>  
```

In DTD, an element is declared by:  
- its name (i.e. its tag in the XML document)
- the sequence of the names of its sub-elements (placed in parentheses)
- Special case of a sub-element: 
	- (#PCDATA) means that the sub-element is plain text

The sub-elements:  
- are declared by their names (i.e. its tags in XML) 
- appear nested within the element (in XML)  
- they appear in XML in the order specified in the DTD  
- if commas are omitted: arbitrary order  

Multiplicity of a sub-element is specified by:  
1. * = zero or more
2. += one or more
3. ? = zero or one  

In addition: “|” means “or”

##### Example of simple DTD
```
<!DOCTYPE DurhamPUBS [  
<!ELEMENT DurhamPUBS (PUB*)>  
<!ELEMENT PUB (NAME,(BEER | VODKA)+, ADDRESS?)>  
<!ELEMENT NAME (#PCDATA)>  
<!ELEMENT BEER (NAME, PRICE)>  
<!ELEMENT VODKA (NAME, PRICE)>  
<!ELEMENT PRICE (#PCDATA)>  
<!ELEMENT ADDRESS (#PCDATA)>  
]>
```

##### Using the DTD
can either be embeded within the XML file or linked

```
<?XML VERSION = "1.0" STANDALONE = "no"?>  
<!DOCTYPE Bars [  
	<!ELEMENT BARS (BAR*)>  
	<!ELEMENT BAR (NAME, BEER+)>  
	<!ELEMENT NAME (#PCDATA)>  
	<!ELEMENT BEER (NAME, PRICE)>  
	<!ELEMENT PRICE (#PCDATA)>  
]>  
<BARS>  
	<BAR> <NAME> Joe's Bar </NAME>  
		<BEER> <NAME> Bud </NAME> <PRICE> 2.50 </PRICE>  
		</BEER>  
		<BEER> <NAME> Miller </NAME> <PRICE> 3.00 </PRICE>  
		</BEER>  
	</BAR>  
	...  
</BARS>  

or

<?XML VERSION = "1.0" STANDALONE = "no"?>  
<!DOCTYPE Bars SYSTEM "bar.dtd">  
<BARS>  
	<BAR> <NAME> Joe's Bar </NAME>  
		<BEER> <NAME> Bud </NAME>  
			<PRICE> 2.50 </PRICE>  
		</BEER>  
		<BEER> <NAME> Miller </NAME>  
			<PRICE> 3.00 </PRICE>  
		</BEER>  
	</BAR>  
...  
</BARS>
```

#### Schema-valid XML document (stronger)
- must be well formed and 
- conforms to an XML schema

