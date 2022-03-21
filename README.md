# deadlockAvoidance
In this program I have implemented different activities that are trying to require access to the same resource through different actions. Due to the fact that this process is starved due to resource unavailability, I have implemented a clock / timer, with help from the code in the padlet, to attempt to allow the resources to gain access to the resource once one activity has completed gaining access. If any processes become terminated, due to it timing out, the process will begin again. 
### Timer Usage
The timer usage to solve deadlock situations was useful; however, time consuming. It allowed me to pinpoint which activities were causing the deadlock and allocate resources properly. This solution is scalable to multiple processes and threads in order to achieve the end output.
## Execution Results
The c program implements the scenario as described above that prints the necessary process data which shows a log of activities: which shows the processes that are running, and what resource they are trying to access, and whether the resource is available. Different pthreads were used to correctly allocate the resources and allow each activity to try to gain access to the resource. 
## Analysis 
I was able to determine and grant the following requests to the system given that it remains in the safe state. If the request that was made by the process was less or equal to the max necessary to that process, the request was granted. Following these steps allowed for a sustainable approach to the deadlock resolution.
