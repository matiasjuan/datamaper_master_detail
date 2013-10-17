Datamapper example
====
In this example we can see how to generate an XML file with master-detail relationships (nodes and subnodes).
The source data is stored in the same table; each record contains fields for the parent and fields for the child.

Input
----

JSon input example
```
[
  {
  	"patientid": 2,
  	"lab_name": "lab1",
  	"date": "2013/04/20",
  	"result": "ok"
  },
  {
  	"patientid": 2,
  	"lab_name": "lab2",
  	"date": "2013/04/22",
  	"result": "failed"
  },
  {
  	"patientid": 2,
  	"lab_name": "lab3",
  	"date": "2013/04/25",
  	"result": "unknown"
  }
]
```

Output
----

XML output example
```
<?xml version="1.0" encoding="UTF-8"?>
<patient_lab>
  <id>2</id>
  <labs>
    <lab>
      <name>lab1</name>
      <date>2013/04/20</date>
      <result>ok</result>
    </lab>
    <lab>
      <name>lab2</name>
      <date>2013/04/22</date>
      <result>failed</result>
    </lab>
    <lab>
      <name>lab3</name>
      <date>2013/04/25</date>
      <result>unknown</result>
    </lab>
  </labs>
</patient_lab>
```

How it works
====
2 element mappings

*  array to patient: this will map each record to one record of the root
*  array to lab: this will map each record to one lab node

Array to patient mapping:
----
Edit the script, and change
```
output.__id = input.__id;
```
by this
```
output.__id = input.patientid;
```

Edit the condition and put 1 in the condition.

Array to lab mapping:
----

Edit the script and change this

```
output.__id = input.__id;
```

by this
```
output.__id = input.__id;
output.__parent_id = input.patientid;
```

