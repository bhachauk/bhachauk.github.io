---
github: sql
---

<kbd class="imgtitle">Contents</kbd>

- [Overview](#overview)
- [Tables](#example-tables)
- [Convolution](#convolution)
- [Explanation](#explanation)
- [Filtered Convolution](#filtered-convolution---matched)
{: .contentBorder .txt-pad}

### Overview
<hr>

<p class="quickNote">Note : 
If you already know about the basic join mechanism just ignore the post. This practical demo explanation will
give you a basic understanding on joining the tables in databases. If it is not, just ignore :P</p> 

Joining two tables in database using <mark>SQL</mark> is a very easy task. But i would like to share this post to experience the 
table joining through this demo. Enjoy Learning ...!
<br>

### Example Tables
---

Having some tables in database shown below,
###### Table 1 : Months
<hr>

```text
+---------+--------+
| month   | result |
+---------+--------+
| january | 1      |
| March   | 2      |
| April   | 3      |
+---------+--------+
```

###### Table 2 : RefMonths
<hr>

```text
    +-----------+
    | month     |
    +-----------+
    | january   |
    | February  |
    | March     |
    | April     |
    | May       |
    | June      |
    | July      |
    | August    |
    | September |
    | October   |
    | November  |
    | December  |
    +-----------+
```

### Convolution 
---

We know the Join query for <mark>Left Join</mark>. It is easy but when you do the query like shown below,

###### The Query is:
<hr>

```python
    select * from refmonth left join months on 1=1;
```

###### Output :
<hr>

```text
    +-----------+---------+--------+
    | month     | month   | result |
    +-----------+---------+--------+
    | january   | january | 1      |
    | February  | january | 1      |
    | March     | january | 1      |
    | April     | january | 1      |
    | May       | january | 1      |
    | June      | january | 1      |
    | July      | january | 1      |
    | August    | january | 1      |
    | September | january | 1      |
    | October   | january | 1      |
    | November  | january | 1      |
    | December  | january | 1      |
    | january   | March   | 2      |
    | February  | March   | 2      |
    | March     | March   | 2      |
    | April     | March   | 2      |
    | May       | March   | 2      |
    | June      | March   | 2      |
    | July      | March   | 2      |
    | August    | March   | 2      |
    | September | March   | 2      |
    | October   | March   | 2      |
    | November  | March   | 2      |
    | December  | March   | 2      |
    | january   | April   | 3      |
    | February  | April   | 3      |
    | March     | April   | 3      |
    | April     | April   | 3      |
    | May       | April   | 3      |
    | June      | April   | 3      |
    | July      | April   | 3      |
    | August    | April   | 3      |
    | September | April   | 3      |
    | October   | April   | 3      |
    | November  | April   | 3      |
    | December  | April   | 3      |
    +-----------+---------+--------+
```
### Explanation
<hr>

So it will provide output table by doing <mark>convolution</mark> between the tables <mark>months * refmonth</mark>.
Now you can understand what the query <mark>select * from</mark> is doing. So putting SQL the condition <mark>where</mark> is the actual 
area where you achieving the table joining.

So lets continue ...! 
 
### Filtered Convolution - Matched
<hr>

```python
select * from refmonth left join months on months.month = refmonth.month;
```

###### Output:
<hr>

```text
    +-----------+---------+--------+
    | month     | month   | result |
    +-----------+---------+--------+
    | january   | january | 1      |
    | March     | March   | 2      |
    | April     | April   | 3      |
    | February  | NULL    | NULL   |
    | May       | NULL    | NULL   |
    | June      | NULL    | NULL   |
    | July      | NULL    | NULL   |
    | August    | NULL    | NULL   |
    | September | NULL    | NULL   |
    | October   | NULL    | NULL   |
    | November  | NULL    | NULL   |
    | December  | NULL    | NULL   |
    +-----------+---------+--------+
```