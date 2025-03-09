# Nama : Syahrul Ardi Prasetiyo

# Practice Exercise

## 1.1 What are the three main purposes of an operating system? 

- **Resource Management:**  
  The OS manages hardware resources such as the CPU, memory, storage, and peripheral devices. It ensures efficient allocation and utilization of these resources among multiple applications and users.  
- **Abstraction and Simplification:**  
  The OS provides a simplified interface for users and applications to interact with the hardware. It hides the complexity of hardware operations through abstractions like file systems, device drivers, and system calls.  
- **System Protection and Security:**  
  The OS ensures that different programs and users do not interfere with each other. It enforces security policies, manages user permissions, and protects the system from unauthorized access or malicious activities.  

---

## 1.2 When is it appropriate for the operating system to forsake efficient resource use and "waste" resources? Why is such a system not really wasteful?  

- Operating systems are designed to optimize the use of computing resources, but there are some situations where "wasting" resources is necessary for convenience, security, or reliability. Some examples are Time-Sharing, Graphic interface (GUI), virtualization, security, and background services. This is actually not in vain because the benefits increase ease of use, data protection and system stability.  

---

## 1.3 What is the main difficulty that a programmer must overcome in writing an operating system for a real-time environment?  

- One major difficulty that programmers need to overcome when writing an operating system for a real-time environment is meeting strict timing requirements. In a real-time system, tasks must be completed within specific time constraints to ensure the system functions correctly.  

---

## 1.4 Should the operating system include applications such as web browsers and mail programs? Argue both sides.  

### Why should they be included in the OS?  
- **User Convenience:** Including applications like web browsers eliminates the need for users to download additional software after installing the OS.  
- **Better Integration:** Built-in applications can be optimized to work more smoothly with the OS, improving performance and security.  
- **Consistent User Experience:** Providing standard applications ensures a uniform experience across all devices running the same OS.  

### Why should they not be included in the OS?  
- **The OS Should Focus on Resource Management:** An operating system is designed to manage hardware and software resources, not to provide user applications.  
- **Risk of Bloatware:** Including applications that not all users need can increase system resource usage and reduce flexibility.  
- **Legal and Monopoly Issues:** Bundling certain applications with the OS can lead to legal issues, such as antitrust cases involving major companies.  

---

## 1.5 How does the distinction between kernel mode and user mode function as a rudimentary form of protection (security)?  

The distinction between kernel mode and user mode provides a rudimentary form of protection in the following manner. Certain instructions could be executed only when the CPU is in kernel mode. Similarly, hardware devices could be accessed only when the program is executing in kernel mode.  
- **Kernel Mode:** The OS runs in kernel mode, allowing direct access to hardware and critical system resources.  
- **User Mode:** Applications run in user mode, with restricted access to hardware and sensitive areas of the system.  

---

## 1.6 Which of the following instructions should be privileged?  

a. Set value of timer.  
b. Read the clock.  
c. Clear memory.  
d. Issue a trap instruction.  
e. Turn off interrupts.  
f. Modify entries in device-status table.  
g. Switch from user to kernel mode.  
h. Access I/O device.  

### Non-privileged instructions:  
- **(d) Issue a trap instruction:** This instruction is used to transfer control to the operating system kernel. It is privileged because it allows a user program to request services from the operating system, and these requests need to be carefully managed to prevent unauthorized access or disruption of system operations.  
- **(e) Turn off interrupts:** This instruction is privileged because it can affect the normal operation of the system and needs to be controlled to prevent unauthorized manipulation of system resources.  
- **(g) Switch from user to kernel mode:** This instruction is privileged because it involves a change in the processor's mode of operation, which is a critical operation that should only be allowed under controlled conditions to prevent unauthorized access to system resources.  
- **(h) Access I/O device:** This instruction is privileged because it involves direct interaction with hardware devices, which can impact system stability and security if not properly controlled.  

---

## 1.7 What are two difficulties that could arise from placing the OS in a memory partition that cannot be modified?  

a. **Limited Flexibility:** The OS cannot dynamically adjust its memory usage, making it difficult to handle varying workloads or new features.  
b. **Performance Bottlenecks:** If the OS cannot modify its own memory, it may struggle to optimize performance or respond to system events efficiently.  

---

## 1.8 What are two possible uses of multiple modes of operation in CPUs?  

- One possibility would be to provide different distinctions within kernel code. For example, a specific code would allow USB devices could allow USB devices to driver to run. This would mean that that USB devices could be serviced without having to switch to kernel mode, there by essentially allowing USB device drivers to run in a quasi-user/kernel mode.  
- Second possibility would be to provide different distinctions within user mode. Multiple user modes could be used to provide a finer-grained security policy. Perhaps users belonging to the same group could execute each others code. When the machine was in this mode, a member of the group could run belonging to anyone else in the group.  

---

## 1.9 How could timers be used to compute the current time?  

a. A system timer increments at a fixed frequency (e.g., 1,000 ticks per second).  
b. The OS records the number of ticks since a known start time (e.g., system boot).  
c. By multiplying the tick count by the interval between ticks, the OS can calculate the current time.  

---

## 1.10 Why are caches useful? What problems do they solve and cause? Why not make caches as large as the device they cache?  

- **Reasons caches are useful:**  
  a. **Speed:** Caches provide faster access to frequently used data, reducing latency.  
  b. **Efficiency:** They reduce the load on slower storage devices (e.g., disks) by serving data from faster memory.  
- **Problems they solve:**  
  a. Slow access times for data stored in main memory or secondary storage.  
  b. High latency in fetching data from remote or slow devices.  
- **Problems they cause:**  
  a. **Cache Coherence:** Ensuring consistency between cache and main memory.  
  b. **Cache Pollution:** Storing unnecessary data, reducing effective cache size.  
- **Why not make caches as large as the device they cache?**  
  a. **Cost:** Larger caches are more expensive.  
  b. **Diminishing Returns:** Beyond a certain size, the performance gains do not justify the cost.  

---

## 1.11 Distinguish between the client–server and peer-to-peer models of distributed systems  

The client-server model firmly distinguishes the roles of the client and server. Under this model, the client requests services that are provided by the server. The peer-to-peer model doesn’t have such strict roles. In fact, all nodes in the system are considered peers and thus may act as either clients or servers—or both. A node may request a service from another peer, or the node may in fact provide such a service to other peers in the system.  
For example, let’s consider a system of nodes that share cooking recipes. Under the client-server model, all recipes are stored with the server. If a client wishes to access a recipe, it must request the recipe from the specified server. Using the peer-to-peer model, a peer node could ask other peer nodes for the specified recipe. The node (or perhaps nodes) with the requested recipe could provide it to the requesting node. Notice how each peer may act as both a client (it may request recipes) and as a server (it may provide recipes).  

---
