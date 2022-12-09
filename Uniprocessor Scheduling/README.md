<h1 style="text-align:center;color:cyan;">    Uniprocessor Scheduling</h1>



# Scheduling Objectives

1. Share time **fairly** among processes
2. Prevent **starvation** of a process
3. Use the **processor efficiently**
4. Have **low overhead**
5. **Prioritise** processes when necessary (e.g. real time deadlines)


# Types of Scheduling

|Name                                       |Type|
|-------------------------------------------|--------------------------------------------------------------------------------|
|**Long-term scheduling**         	                        |whether to add a new process to the set of processes that are currently active|
|**Medium-term scheduling**	                        |whether to add a process to those that are at partially (or fully) in main memory |
|**Short-term scheduling**                      |actual decision of which ready process to execute next on CPU
 | **I/O scheduling**	                      |Which I/O pending processes shall be handled by the available I/O device                                            |

 <br> 

## Types of Scheduling [States]

![States](imgs/Picture.gif)

<br>                         

## Types of Scheduling [Queues]                  

![States](imgs/Picture4.gif)

<br> 

# [1] Long-Term: 


- Determines which programs are admitted to the system for processing, according to:

> first-come-first-served

> priority

>I/O requirements 

>expected execution time

- Executes **infrequently**

- <font color = "red" > Controls </font> **the degree of  multiprogramming**

- More processes **❱❱** smaller amount of time each process is executed

<br> 

![LT](imgs/Picture5.png)

<br> 

# [2] Medium-Term: 


Part of the swapping function

decision based on the need to <font color = "red" > manage </font> **the degree of  multiprogramming**

Executes **most frequently** 


<br> 

![MT](imgs/Picture6.png)

<br> 

# [3] Short-Term: 


Known as dispatcher

Executes **most frequently** 

Invoked when an event occurs


> Clock interrupts

> I/O interrupts

>Operating system calls


>Signals


<br> 

![ST](imgs/Picture7.gif)

<br> 


# Performance Criteria



| <font color = "cyan"> **User-oriented**<font>   | <font color = "cyan"> **System-oriented**<font>    | 
|---------------------|------------------------|
| behavior of system as perceived by user/        process <br>  <br> Ex: Response Time <br>  " elapsed time between the submission of a request until the response begins to appear as output"| focus on effective and **efficient utilization** of **CPU** <br><br>Ex: Throughput <br>  "number of processes completed per unit of time"|

<br>



| <font color = "cyan"> **performance related**<font>   | <font color = "cyan"> **Non-performance related**<font>      | 
|---------------------|------------------------|
|Quantitative<br><br>Easily measured<br><br> Ex: response time and throughput| Qualitative<br><br> Hard to measure<br><br> Ex: predictability|

<br>

|   |  <font color = "white"> **performance related**<font>     |<font color = "white"> **Non-performance related**<font> | 
|---------------------|------------------------|------------------------|
|<font color = "white"> **User-Oriented**<font>  | Turnaround time<br> Response time<br>Deadlines <br>|Predictability|
|<font color = "white"> **System-Oriented**<font> |Throughput<br> CPU Utilization|Fairness<br> Enforce Priorities<br>Balancing Resources <br>|

<br>

|Name                                       |Defination|
|-------------------------------------------|--------------------------------------------------------------------------------|
|**Turnaround time**         	                        |this is the interval of time between the submission of a process and its completion.<br>Includes actual execution time plus time spent waiting for resources, including the processor. this is an appropriate measue for a batch job.|
|**Medium-term scheduling**	                        |whether to add a process to those that are at partially (or fully) in main memory |
|**Short-term scheduling**                      |actual decision of which ready process to execute next on CPU
 | **I/O scheduling**	                      |Which I/O pending processes shall be handled by the available I/O device                                            |

 <br> 




# Types of Processes



| <font color = "cyan"> **Processor-Bound**<font>   | <font color = "cyan"> **I/O-Bound**<font>      | 
|---------------------|------------------------|
|It mainly performs computational work and occasionally uses I/O devices. <br><br> ![PB](imgs/Picture3.png)|depends primarily on the time spent waiting for I/O operations. <br><br> ![PB](imgs/Picture2.png)|

<br>



----------------------------------------------------------------------------------------------------
# Short-Term Policies

| <font color = "cyan"> **Non-preemptive**<font>   | <font color = "cyan"> **Preemptive**<font>      | 
|---------------------|------------------------|
|process in run state will continue until it terminates or blocks itself for I/O|running process may be interrupted and moved to ready state by the OS <br><br>Preemption may occur when : <br> ❱ new process arrives <br> ❱ on an interrupt <br> ❱ or periodically [clock interrupt]|

<br> 

## Example: 


- consider each process a batch job

- Service time represents total execution time

- **Time now = 0**

### Calculate
1. Finish time
2. Turnaround time & its average
3. Normalized turnaround time & its average
4. Wait time & its average

<br>

   |Process    | Arrival Time  |Service Time   |
   |-----------|---------------|---------------|
   |    A      |       0       |      3        |
   |    B      |       2       |      6        |
   |    C      |       4       |      4        |
   |    D      |       6       |      5        |
   |    E      |       8       |      2        |


<br>

| Rules <br><br> Turnaround time = finish – arrival = service + wait  <br>-----------------------------------------------------------<br>  Normalized turnaround = (finish – arrival) / service <br>-----------------------------------------------------------<br> Wait time = turnaround – service <br>-----------------------------------------------------------<br> CPU Utilization = Time of CPU / Total Time x 100 <br>|
|-----------|

<br>

--------------------------------------------------------

<font color="Cyan" size="20px" face="WildWest">FCFS</font>
<br>
><font color="white" size="4px" > First Come First Serve</font>
- Each process joins the Ready queue
- Select process with max wait-time
- Non-preemptive

<br>


![FCFS](imgs/Picture9.gif)


 |Process|A | B |C|D|E|Average|
 |-------|--|---|----|-----|--|-----|
 |Finish Time|3|9|13|18|20|
 |Turnaround Time|3|7|9|12|12|8.60 |
 |Normalized turnaround|1.00|1.17|2.25|2.40|6.00|  2.56|         |
   |    Wait Time      | 0|1|5|7|10            |            |
   

<br>


<table>			   
				   	  
<table>
	 <tr>
		 <td> 
          Props
         </td>
		 <td> 
         Concs 
         </td>
	</tr>
    <tr>
		 <td> 
          Simplest  min overhead<br><br>No starvation 
        </td>
		 <td> Bad response time for short process<br>(may have to wait a very long time before it can execute)
<br><br>Favors CPU-bound processes --> inefficient use of I/O<br> (I/O-bound has to wait until all CPU-bound processes complete)
        </td>
 </table>
      

--------------------------------------------
<font color="Cyan" size="20px" face="WildWest">SPN</font>
<br>
><font color="white" size="4px" > Shortest Process Next </font>
- Short process jumps ahead of longer processes

- Select process with shortest expected time

- Non-preemptive

<br>


![SPN](imgs/Picture12.gif)
<br>
<br>

 |Process|A | B |C|D|E|Average|
 |-------|--|---|----|-----|--|-----|
 |Finish Time|3|9|15|20|11|
 |Turnaround Time|3|7|11|14|3|7.60 |
 |Normalized turnaround|1.00|1.17|2.25|2.80|1.50|1.84|         |
   |    Wait Time      | 0|1|7|9|1            |            |
   

<br>


<table>			   
				   	  
<table>
	 <tr>
		 <td> 
          Props
         </td>
		 <td> 
         Concs 
         </td>
	</tr>
    <tr>
		 <td> 
          High throughput<br><br>Good response time for short processes 
        </td>
		 <td> Overhead (to estimate service time)
<br><br>Starvation for long processes<br><br>Bad predictability of longer processes<br><br>inefficient use of I/O devices<br>(I/O bounds need to wait current running CPU-bound)
        </td>
 </table>
                 


-------------------------------------------------------
<font color="Cyan" size="20px" face="WildWest">SRT</font>
<br>
><font color="white" size="4px" >Shortest Remaining Time  </font>
- Preemptive version of SPN


- Preemption on process arrival 


- Select process with min (service – execution)


<br>


![SRT](imgs/Picture14.gif)
<br>
<br>

 |Process|A | B |C|D|E|Average|
 |-------|--|---|----|-----|--|-----|
 |Finish Time|3|15|8|20|10|
 |Turnaround Time|3|13|4|14|2|7.20 |
 |Normalized turnaround|1.00|2.17|1.00|2.80|1.00|1.59|         |
   |    Wait Time      | 0|7|0|9|0            |            |
   

<br>


<table>			   
				   	  
<table>
	 <tr>
		 <td> 
          Props
         </td>
		 <td> 
         Concs 
         </td>
	</tr>
    <tr>
		 <td> 
          High throughput<br><br>Good response time for short processes<br><br>Efficient use of I/O devices<br>(prefer I/O-bounds over CPU-bounds) 
        </td>
		 <td> Overhead (to estimate service time)
<br><br>Starvation for long processes<br><br>Bad predictability of longer processes        </td>
 </table>
                 

---------------------------------------------------------

<font color="Cyan" size="20px" face="WildWest">RR</font>
<br>
><font color="white" size="4px" >Round Robin  </font>

- Preemptive version of FCFS

- Clock interrupt is generated at periodic intervals 
 
- each process is given a slice of time (quantum) before being preempted

- No need to know remaining time of the process



<br>


![RR](imgs/Picture15.gif)
<br>
<br>

 |Process|A | B |C|D|E|Average|
 |-------|--|---|----|-----|--|-----|
 |Finish Time|4|18|17|20|15|
 |Turnaround Time|4|16|13|14|7|10.80 |
 |Normalized turnaround|1.33|2.67|3.25|2.80|3.50|2.71|         |
   |    Wait Time      | 1|10|9|9|5            |            |
   

<br>


<table>			   
				   	  
<table>
	 <tr>
		 <td> 
          Props
         </td>
		 <td> 
         Concs 
         </td>
	</tr>
    <tr>
		 <td> 
          Independent on service time<br><br>Good response time for short processes
        </td>
		 <td>   Favors CPU-bound processes --> inefficient use of I/O devices <br>(I/O bounds need to wait all CPU-bounds in the queue)
<br><br>Context-switch overhead<br><br>  Affect the cache usage
     </td>
 </table>

<br>

<font color="gree" size="6px" face="s">  Solution </font> <font color="White" size="5px">  of   I/O Bound Problem </font> 

## Virtual Round Robin

> <font color="White"> Produce fair treatment for I/O-bound
 </font> 

> <font color="White"> Use auxiliary queue with high priority over ready Q
  </font> 

> <font color="White"> Process from auxiliary Q allowed for a single quantum only
 </font> 



<br>

-------------------------------------------------------