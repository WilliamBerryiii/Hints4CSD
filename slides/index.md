- title : Hints for Computer System Design
- description : While technologies, methodologies and abstractions have waxed and waned over the years, Butler Lampson’s ‘Hints for Computer Systems Design’ remains relevant to the current challenges faced in hardware and software  systems engineering.  Drawing against the backdrop of current development practices, we will discuss how Lampson’s hints can still be used, some thirty years later, to implement functionally accurate, high-performing fault-tolerant software systems.
- author : William Berry 
- theme : moon
- transition : default

***

&nbsp;

' -2 take ways
' -Learn something, take tonight as an infection and spread it at work
' -We finish up & know all this. Explain why 30 years later still have these issues
' -Where are the abstractions? 
' -Non-breaking (cant wrap), non-collapsing
' -Sans Serif - Droid Sans Mono by Steve Matteson - consolas,monospace

***
"Design is not what it looks like and feels like. Design is how it works." - Steve Jobs

---
"Science is about knowing; engineering is about doing." - Henry Petroski

---
"The walls between art and engineering exist only in our minds" - Theo Jansen

---
"A good scientist is a person with original ideas. A good engineer is a person who makes a design that works with as few original ideas as possible." - Freeman Dyson

---
"[requirements, architecture, process, techniques]. Of course the goals are in conflict, and engineering is the art of making tradeoffs, for instance among features, speed, cost, dependability, and time to market." - Butler Lampson

***
Hints <span style="font-size:60%">For</span> Computer System Design
----------------------------------------
######- Butler Lampson (1983) -

<div class="fragment">
... or how to engineer less sucky systems
</div>

***
Hardware | Software	

<div class="fragment">
Functionality -> Speed -> Fault Tolerance 
</div>
' top down approach

---
###Industry Status - Hardware
<div class="fragment" style="list-style-type: none;">
Apple - Lisa<br />
Compaq - IBM clone<br />
Gavilan SC - "Laptop" 
</div>

' Compaq 53,000 PCs $111M first year sales same year went public 2nd year in biz

---
<div>

<figure style="display:inline-block;width:250px;">
<img src="images/Apple_Lisa.jpg" alt="Gavilan SC" style="background-color: #fff;height:200px;width:250px;" />
<figcaption style="text-align:center;font-size:xx-small;display:table-caption;caption-side:bottom;width:225px;word-wrap: break-word;">"Apple Lisa". Licensed under CC BY-SA 3.0 via Wikimedia Commons - https://commons.wikimedia.org/wiki/File:Apple_Lisa.jpg#/media/File:Apple_Lisa.jpg</figcaption>
</figure>

<figure class="fragment" style="display:inline-block;width:250px;">
<img src="images/Compaq_portable.jpg" alt="Gavilan SC" style="background-color: #fff;height:200px;width:250px;" />
<figcaption style="text-align:center;font-size:xx-small;display:table-caption;caption-side:bottom;width:225px;word-wrap: break-word;">"Compaq portable". Licensed under Public Domain via Wikimedia Commons - https://commons.wikimedia.org/wiki/File:Compaq_portable.jpg#/media/File:Compaq_portable.jpg</figcaption>
</figure>

<figure class="fragment" style="display:inline-block;width:250px;">
<img src="images/Gavilan_SC.jpg" alt="Gavilan SC" style="background-color: #fff;height:200px;width:250px;" />
<figcaption style="text-align:center;font-size:xx-small;display:table-caption;caption-side:bottom;width:225px;word-wrap: break-word;">"<a href="https://commons.wikimedia.org/wiki/File:Gavilan_SC.jpg#/media/File:Gavilan_SC.jpg">Gavilan SC</a>" by <a href="//commons.wikimedia.org/w/index.php?title=User:Rdc5&amp;action=edit&amp;redlink=1" class="new" title="User:Rdc5 (page does not exist)">Rdc5</a> - <span class="int-own-work" lang="en" xml:lang="en">Own work</span>. Licensed under <a href="http://www.gnu.org/copyleft/fdl.html" title="GNU Free Documentation License">GFDL</a> via <a href="https://commons.wikimedia.org/wiki/">Wikimedia Commons</a>.</figcaption>
</figure>

</div>


---
###Industry Status - Software/Networking
<div class="fragment">
Lotus 1-2-3 - Autocad - MS DOS 2.0 - Word - GNU
</div>
<div class="fragment">
DNS - IEEE 802.3 - Physical Ethernet - MIDI 
</div>

' Visicalc '79 - Xerox Star '81
' DNS by Paul Mockapetris @ UCI 
' Stallman GNU announced, did not start till 1984
' IEEE 802.3 was approved as a standard
' Mouse, Full Size Monitor, laser printer, 2 phase commit, ethernet

***
###But That Was Then ...
<div class="fragment">
Hardware | Software | Peopleware
</div>
<div class="fragment">
Fault Tolerance -> Speed -> Functionality
</div>
' and this is now
' start low level and build toward meta
' paper talked about disk, memory, low level - keep in mind we've raised abstractions

<!---
****
*
* Fault Tolerance Section
*
****
--->

***
Fault Tolerance
==========

---
### End-to-End
Reliability comes with Error Handling

' Commented at application level which raises the question of who is the user? (APIs, Trading systems, etc.)

---
### Log Updates

---
### Transactions

<!---
****
*
* Speed Section
*
****
--->

***
Speed
=====

---
### Split Resources

' when this was written it was about memory and disk
' some times is faster to keep dedicated resources than shared, disk is cheap
' eg. no-sql, where we keep dedicated projections based on the questions of the application

---
### Use Static Analysis 

' that's it. just use it. 

---
### Cache Answers 



--- 
### What's the correct amount of RAM for my SQL box?

<div class="fragment">
<span style="font-size:600%;font-weight:bold;">MORE</span>
</div>

---
### Background Workers

---
### Batch Processing

---
### Safety First

---
### Floatsam & Jetsam

' Load Shedding 
' Packet Loss - the erlang

<!---
****
*
* Functionality
*
****
--->

***
Functionality
========

***
###KIS(S)
Do one thing really well
Interfaces capture minimum requirements of an abstraction
Don't generalize, generalizations are generally wrong

' think about interfaces at each intersection of interaction 
' field/property -> method -> object -> factory -> controller -> service -> website -> user
' unintended consequences, login interface accidentally reveal user emails 

***
###Corollaries
Build basic interfaces that are blazing fast
How do we know it's fast? Telemetry & Logging
"... it is normal for 80% of the time to be spent in 20% of the code, but a priori analysis or intuition usually can’t find the 20% with any certainty." - Lampson

' OData vs WebAPI

---
###Procedure Arguments 
Sort, Filter, Select

' have interface take in a func rather than discrete methods, or special patterning

---
### Make the Client Pay
Unix streaming/piping

' write lots of little programs and compose the parts you need 
' flexibility, extensibility

***
###Continuity
Keep basic interfaces stable 
"When a system grows to more than 250K lines of code the amount of change becomes intolerable; even when there is no doubt about what has to be done, it takes too long to do it. There is no choice but to break the system into smaller pieces related only by interfaces that are stable for years."

Keep a place to stand
' Microservices?


***
###Making Implementations Work



***
-Fin-
===