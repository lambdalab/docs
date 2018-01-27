# Meta Data

Meta data related APIs provide you the access to read source code static analysis generated data.
The 2 most important concepts of meta data in Insight.io system are `Node` and `Edge`.


### Node

{% method %}
Each symbol (e.g. function, variable, etc.) in your source code is a kind of `Node`. Typically, a `Node` usually has the following fields:

| Field | Description |
|:-:|---|
|`signature`| acts as the id of this node |
|`kind`| the type of this node |
|`range`| the position of this node in the source code |
|`qname`| the query name of this (definition) node |
|`display`| a more readable name of this (definition) node |
|`doc`| The comment of the node |

The `range` of a `Node` has a `start_loc` and `end_loc`, which together defines the range of the
`Node` in the source code. Each of them has the following structure:

| Field | Description |
|:-:|---|
|`line`| the line number on which the position lies |
|`column`| the column number of the position in that line |
|`offset`| the offset in term of the entire file of the position |

The `kind` of the `Node` is an enumeration with the following values:

| Value | Description |
|:-:|---|
|`0`| package |
|`1`| file |
|`2`| class |
|`3`| interface |
|`4`| local variable |
|`5`| field |
|`6`| global variable |
|`7`| method, usually a member of a class |
|`8`| function, which is not a member of any class |
|`9`| usage |
|`10`| decorator |
|`11`| url |
|`12`| eumeration |
|`13`| constructor |
|`14`| type alias |
|`15`| type variable |
|`16`| project |
|`17`| structure |
|`18`| macro |
|`100`| unknown |

{% common %}
**Example**

```json
{
  "signature": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
  "kind": 2,
  "range": {
    "start_loc": {
      "line": 29,
      "column": 13,
      "offset": 1113
    },
    "end_loc": {
      "line": 29,
      "column": 30,
      "offset": 1130
    }
  },
  "qname": "org.apache.hadoop.hdfs.SWebHdfsDtFetcher",
  "display": "SWebHdfsDtFetcher",
  "doc": "  DtFetcher for SWebHdfsFileSystem using the base class HdfsDtFetcher impl.\n"
}
```

{% endmethod %}


### Edge

{% method %}

`Edge` defines the relationship between any 2 `Node`. It has the following fields:

| Field | Description |
|:-:|---|
|`start_id`| The id of the start node |
|`end_id`| The id of the end node |
|`kind`| The type of this edge |

In which, the `kind` is an enumeration with the following values:

| Value | Description |
|:-:|---|
|`0`| reference |
|`1`| referenced at |
|`2`| locate |
|`3`| located at |
|`4`| inherit |
|`5`| inherited by |
|`6`| declare |
|`7`| declared at |
|`8`| has memeber |
|`9`| member of |
|`10`| override |
|`11`| overriden by |
|`12`| has type |
|`13`| type of |
|`14`| call |
|`15`| called at |
|`16`| decorate |
|`17`| decorated by |
|`18`| implement |
|`19`| implemented by |
|`20`| returns |
|`21`| returned by |


{% common %}
**Example**

```json
{
  "start_id": "0X_8smfRb28NmAqJiuyAeA__:1007-1011",
  "end_id": "org.apache.hadoop.io.Text",
  "kind": 0
}
```
{% endmethod %}

This chapter has the following sections:

* [Get Meta Data](./GET_META_DATA.md)
* [Get Node Data](./GET_NODE_DATA.md)
* [Get References](./GET_REFERENCES.md)
