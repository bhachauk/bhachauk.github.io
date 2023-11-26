---
github: networkviewer_shiny
shiny: networkviewer
---

<kbd class="imgtitle">Contents</kbd>

1. [Objective](#objective)
1. [Pre-requisites](#pre-requisites)
1. [R Libraries](#r-libraries)
1. [Example Scenario](#example-scenario)
1. [Collecting as Graph](#network-details)
1. [R-Code Snippets](#network-viewer---a-simple-tool)
{: .contentBorder .txt-pad}

## Objective
---

The objective of this post is to draw a graph using **R Lanaguage** with data of edges of
the graph. All network data contains the edges list which explains us the Node_connectivity
details and the link details. Here this post discuss with the R packages which does
the work and plotting very beautiful graphs for users.

## Pre-requisites
---

So as I said before you need to have this,

- The Edges list

The edges list should be like this example,

SOURCE,END,LINK
Node_A, Node_B, Link1
Node_B, Node_D, Link2
Node_A, Node_C, Link3
Node_C, Node_B, Link4
{: .output}

###### Description

We know that,

An Edge in a graph, means the link between two nodes or vertices. So here,

- Node_A, Node_B, Node_C and Node_D are the **Vertices**.
- Link1, Link2, Link3 and Link4 are the **Edge Labels**.

## R Libraries
---

These are three libraries used to form and render the graph in front end.

- [IGraph](http://kateto.net/networks-r-igraph){: .link}
- [Network D3](https://christophergandrud.github.io/networkD3){: .link}
- [VisNetwork](https://datastorm-open.github.io/visNetwork){: .link}


## Example Scenario
---

 Initially i am starting with the commercial example, we can call it as **chennai-air-india-flight-network**.
 So here, I am taking a sample data from **Air-India** flight details which shows flight services from chennai.
 
 - View the data source : [Air-India](http://www.airindia.in/time-table.htm){: .link}
 
 The data is like,

ORIGIN,DESTINATION,Flight Number,FREQ,DEPARTURE,ARRIVAL,AIRCRAFT,STOPS
Chennai,Ahmedabad,AI 0981,...4..7,17:20,20:00,A-320, 
Chennai,Bengaluru,AI 0563,1.34567,13:25,14:15,A-319, 
Chennai,Bengaluru,AI 0563,.2.....,14:25,15:20,A-319, 
Chennai,Coimbatore,9I 0561,12345.7,05:40,07:00,ATR-72, 
Chennai,Coimbatore,9I 0561,0.234567,07:20,08:50,ATR-72, 
Chennai,Coimbatore,AI 0429,1234567,13:30,14:20,A-321, 
Chennai,Coimbatore,9I 0553,1234567,18:50,20:15,ATR-72, 
Chennai,Colombo,AI 0273,1234567,05:55,07:20,A-321,
...
{: .output}

Now you can realize the collected data **From: Chennai, To: AnyCity**, which is like **Node_A**, **Node_B** 
edge data as discussed before.

### Collecting as Graph
---

Our ultimate aim is to get the Network paths from the edge list. The network path data should explains
us the Node_connectivity among the network vertices. Each nodes connected by the edges and establishes the connectivity
in directional links. We need to look for these important parameters shown below.

**Parameters :**

 - **vertices**
 - **edges**
 - **link direction**
 - **No of links between nodes**
  
###### Methods Involved
---
 
The important methods to form the Graph using the package **IGraph** is shown below.

- all_simple_paths
- graph_from_data_frame

```R
    all_simple_paths(graph, from, to = V(graph), mode = c("out", "in", "all","total"))
```


Results of link Details :

Chennai-->Ahmedabad 
Chennai-->Bengaluru 
Chennai-->Coimbatore 
Chennai-->Colombo 
Chennai-->Delhi 
Chennai-->Dubai 
Chennai-->Goa 
...
{: .output}
 
Here you can see the it will render you the paths of a network from one vertice. So iterating through
the method with vertices list will give you the all link paths.
 
The iteration will be,

```R
    l <- unlist(lapply(V(graph) , function(x) all_simple_paths(graph, from=x)), recursive = F)
    paths <- lapply(1:length(l), function(x) as_ids(l[[x]]))
``` 

Example Results of Graph Paths :

Chennai-->Ahmedabad-->CityX-->CityY 
Chennai-->Bengaluru-->CityX
...
{: .output}
 
It will render you list of list, you can convert it into the R <mark>data_frame</mark> for further process.

## Network Viewer - A Simple Tool
---

 Using these methods, I 've create a R Web application to make a quick view of the network implemented with,
 
 - Shiny 
 - networkD3 
 - visNetwork 
 - igraph
 
 <br>
 
 [![Demo](/master_navs/myapps/images/networkviewer.gif){: style="width: 75%; border: 2px solid #111;"}](https://bhanuchander.shinyapps.io/networkviewer)
 
 Find the R Source code in my [GitHub](https://github.com/bhachauk/networkviewer_shiny).
 
## References
---
 
- [R Studio](https://shiny.rstudio.com/){: .link}
- [NetworkD3 Plots](https://christophergandrud.github.io/networkD3/){: .link}
- [IGraph Doc](http://igraph.org/r/doc){: .link}