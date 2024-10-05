# Review of master thesis: The Impact of Unified Namespace in Industry 4.0

I have read following master thesis:

The Impact of Unified Namespace in Industry 4.0
by Ádám Samuel and Péter Werner 
Lund University
Department of Automatic Control
[link](https://lup.lub.lu.se/student-papers/record/9174552/file/9174561.pdf)


## TLDR

1. There is no clear definition of Unified Namespace (UNS)

2. ISA95 structure and single source of truth are the most useful parts of UNS.

3. MQTT is not always needed, OPC-UA is good enough for small to mid companies. 
Only after 100 connected devices advantages of MQTT will be seen.

## Short summary


Thesis is 138 pages long.
They interviewed 3 manufacturing companies Sweden and also HighByte.
They also made a simulation of Unified namespace (UNS) but unfortunately simulation details are very lacking and no code is given.

First 57 pages and 3 sections should be very familiar to people who are working on Industrial automation and have heard of UNS.
They explain common terms in UNS, IIoT, Artificial Intelligence, MQTT and so on.

Then, interviews are given and companies explain their experience with UNS.
Last, they give their conclusions.

## There is no clear definition of Unified Namespace (UNS)

I have read following thesis [The Impact of Unified Namespace in Industry 4.0](https://lup.lub.lu.se/student-papers/record/9174552/file/9174561.pdf)

Most important thing I learned from reading this thesis is "there is no clear definition of Unified namespace"

In section, 3.3 The Unified Namespace:

> The term Unified namespace was popularized by Walker Reynolds, that created the first UNS project in 2005, and who is an avid supporter and spokesperson for the technology. 


The problem with above sections and UNS is that there is almost nothing to cite academically.
That is apart from some blog posts and videos, there is nothing which defines UNS concretely.
No technical reports, no books, no academic articles that define UNS.
When you look at the references of this thesis, this is clearly observed.


Below sentences actually summarize these very well.


> The exact definition of UNS is still not completely agreed upon, but UNS is a system or methodology where all entities, such as files, data or resources etc. are organized in a centralized repository of structured data. 


> Harrington (from HighByte) says that UNS is an ever-evolving concept. The definition and message that Walker Reynold gave just a few years ago has changed in the past years and will probably continue to do so. 

There is nothing wrong with evolving a definition actually definition should evolve but first a clear definition is needed.


## ISA-95

From the interviews, ISA-95 way of structuring the data is very useful.
Instead of using relational model, using ISA-95 hierarchical model is more intuitive in the Industrial setting.

## MQTT and OPC-UA

A lot of companies are using OPC-UA since it is widely supported and familiar with the factories.
The given reason for MQTT is scalability.
But in my opinion, premature optimization is the root of all evil.
The thesis also confirms this.

> This report concluded that at around 100 connected devices advantages of MQTT will become noticeable. 



