node-n-element
=======

### 20210507

``node`` 와 ``element`` 의 차이점에 대하여 기록한 내용이다.

``getElementsBy`` 와 ``querySelector`` 의 차이에 대해서 알기 위해선 ``node`` 와 ``element`` 의 차이를 이해하여야 한다.

<br>

```
The Node object is the primary data type for the entire DOM.

A node can be an element node, an attribute node, a text node,

or any other of the node types explained in the "Node types" chapter.

An XML element is everything from (including) the element's start tag to (including) the element's end tag.
```
출처: https://stackoverflow.com/questions/132564/whats-the-difference-between-an-element-and-a-node-in-xml

<br>

__``element`` 는 ``node`` 의 타입 중 하나이다.__

<br>

``node`` 는 다양한 타입이 있다.

Different W3C specifications define different sets of "Node" types.

Thus, the DOM spec defines the following types of nodes:

- Document -- Element (maximum of one), ProcessingInstruction, Comment, DocumentType
- DocumentFragment -- Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference
- DocumentType -- no children
- EntityReference -- Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference
- Element -- Element, Text, Comment, ProcessingInstruction, CDATASection, EntityReference
- Attr -- Text, EntityReference
- ProcessingInstruction -- no children
- Comment -- no children
- Text -- no children
- CDATASection -- no children
- Entity -- Element, ProcessingInstruction, Comment, Text, CDATASection, EntityReference
- Notation -- no children

https://www.w3.org/TR/1998/REC-DOM-Level-1-19981001/level-one-core.html#ID-1590626202
