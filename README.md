## Senior Year - 2023-2024 / Module 2
Course: Modeling of data transmission networks

### Laboratory 1 : Introduction to Mininet
Mininet (http://mininet.org/) is a virtual environment that allows
you to develop and test network tools and protocols. Mininet networks
run real Unix/Linux network applications, as well as the real Linux kernel
and network stack.

- The main goal of the work is to deploy in a virtualization system(for example, in VirtualBox) mininet, getting to know the basic commands for working with your computer.-you are connected to Mininet via the command line and through the GUI.
- Getting to know Putty and XLaunch

**Basics of working in Mininet**
- Working with Mininet using the command line
- Building and emulating a network in Mininet using a graphical interface

### Laboratory 2 - iperf3.1 : Measuring and testing network bandwidth. Interactive experiment

Purpose of the work: The main goal of the work is to get acquainted with the tool for measuring
network bandwidth in real time — iPerf3, as well
as to gain skills in conducting an interactive experiment on measuring
the bandwidth of a simulated network in the Mininet environment.

***Preliminary information***:
**iperf3** - It is an open-source cross-platform client-server application that can be used to measure throughput between two end devices.

iPerf3 can work with the TCP, UDP, and SCTP transport protocols:
- TCP and SCTP:- measures throughput;
  - allows you to set the MSS/MTU size;
  - monitors the size of the TCP Congestion Window (CWnd).
    
- UDP:- measures throughput;
  - measures packet loss;
  - measures latency fluctuations (jitter);
  - supports multicast package distribution
 
- The user interacts with iPerf3 using the iperf3 command. The basic
iperf3 syntax used on both the client and server is
as follows: : ```iperf3 [-s| -c] [options]```, where -s(start the server); -c(start the client) and [options] - can be view by entering the ```iperf3 -h``` command.
- iPerf3 allows you to export test results to a file with a lightweight
JSON data exchange format (JavaScript Object Notation), which allows other applications to easily analyze the file
and interpret the results.
- You can use the iperf3_plotter package to visualize the results of an iPerf3 measurement. Repository https://github.com/ekfoury/iperf3_plotter contains the following scripts:
  - preprocessor.sh: converts an iPerf3 JSON file to a split value file-comma-separated files (CSV); uses AWK to format file fields;
  - plot_iperf.sh: accepts the iPerf3 JSON file, calls the preprocessorand gnuplot for creating output PDFs
 
**Task:**
1. Install mininet iPerf3 and additional software for visualization and data processing on the virtual machine.
2. To conduct a series of interactive experiments on measuring bandwidth using iPerf 3 with the construction of graphs.

### Laboratory 3 - iperf3.2 : Measuring and testing network bandwidth. Reproducible experiment
Purpose of the work: The main goal of the work is to get acquainted with the tool for measuring network bandwidth in real time — iPerf3, as well as to gain skills in conducting a reproducible experiment on measuring the bandwidth of a simulated network in the Mininet environment.

***Preliminary information***:
#### API Mininet
- The Application Programming Interface (API — is a special protocol for the interaction of computer programs that allows you to use the functions of one application inside another.
- The Mininet API is built on three main levels:
  - **Low-level API**-consists of base nodes and link classes (such asHost, Switch, Link and their subclasses), which can actually be created separately and used to create a network, but this is a bit
cumbersome.
  - **Mid-level API**-adds a Mininet object that serves as a containerfor nodes and links. It provides a number of methods (addHost (), addSwitch (), addLink()) to add nodes and links to the network, as well as network settings,start and stop operations (start (), stop()).
  - **High-level API**-adds an abstraction of the topology template (Topo class),which provides the ability to create reusable parameterized topology templates. These templates can be passed
to the mn command(via the --custom parameter) and use it from the command line.

The low-level API is used when you want to manage nodes and switches directly. The mid-level API is used when starting and stopping a network (in particular, the Mininet class is used).Full-fledged networks can be created using any of the following levels:-it has an API, but usually you choose either a mid-level API for creating networks(for example, Mininet. add* ()), or a high-level API (Topo. add*())

**Task:**
1. Use the Mininet API to reproduce experiments on measuring missile defense-start-up capacity using iPerf3.
2. Plot graphs based on the experiment performed

### Laboratory 4 - netem-latency : Emulation and measurement of global network latency
Purpose of the work: The main goal of the work is to get acquainted with NETEM, a tool for
testing application performance in a virtual network, as well
as to gain skills in conducting interactive and reproducible
experiments on measuring latency and its jitter (jitter) in a simulated network
in the Mininet environment.

***Preliminary information***:
- NETEM is a Linux network emulator used for testing
the performance of real client-server applications in a virtual network.
The virtual network in this case is a laboratory environment for
reproducing the behavior of a wide Area Network (WAN). NETEM
allows the user to set a number of network parameters, such
as latency, jitter, packet loss rate, packet duplication, and
packet reordering.
- NETEM is implemented in Linux and consists of two parts: a kernel module for
queuing and a command-line utility for configuring it.
A queue with service discipline is created between the IP protocol and the network device
. The queue service discipline is implemented as an object with two
interfaces. One interface queues packets to be sent, and the other
interface sends packets to the network device. Based on
the queue maintenance discipline, decisions are made about which packets to send,
which packets to delay, and which packets to discard.
- Queue processing disciplines can be divided into classless and
class-based ones. Classless disciplines generally receive data, reorder it,
delay it, or destroy it. These disciplines can be used
to specify the entire interface restrictions, without any division
into classes. The most common classless discipline is FIFO(first come, first served). In NETEM and in Linux in general, this disciplinequeue maintenance is used by default
- Class disciplines are widely used in cases where a particular
type of traffic needs to be handled differently. An example of a class
discipline is CBQ-Class Based Queueing (
class-based queue processing discipline). Traffic classes are organized in a tree — each
class has at most one parent; a class can have many descendants.
Classes that don't have parents are called root classes. Classes that
do not have descendants are called branch classes.
- The NETEM module is included in the Linux kernel and is managed using the commandtcfrom the iproute2 package. The tc command performs all necessary actions whenworking with the traffic management system

Basic tc syntax used with NETEM:
```
sudo tc qdisc [add|del|replace|change|show] dev dev_id root netem opts
```
where:
- **sudo**: enable command execution with higher privilegessafety;
- **tc**: command used to interact with NETEM;
- **qdisc**: queue discipline (qdisc), which is a set of rules,defining the order in which packets coming
from the IP protocol output are served.
- **[add / del | replace | change | show] ([add | delete | replace-thread | edit | show])**: indicates that one of the qdisc operations is used (for example, to add a delay on a specific interface , use the add option, and to change or delete a delay on a specific interface, use the change or del option, respectively);
- **dev_id**: parameter specifies the interface to be emulated (in this caseif the root interface is specified — root);
- **opts**: parameter specifies the amount of delay, packet loss, duplication, etc.-damage, etc

**Tasks:**
1. Set the simplest topology consisting of two hosts and a switch with the default mininet network 10.0.0.0/8.
2. Conduct interactive experiments on adding/changing delays, jitter, correlation values for jitter and delay, and delay time distribution in the emulated WAN.
3. Implement a reproducible experiment to set the delay value in an emulated WAN. Build a schedule.
4. Independently implement reproducible experiments to change latency, jitter, correlation values for jitter and delay, and delay time limits in the emulated WAN. Build graphs.

### Laboratory 5 - netem-drop : Emulation and measurement of packet loss in wide area networks

Purpose of the work: The main goal of the work is to gain skills in conducting
interactive experiments in the Mininet environment to study network parameters
related to loss, duplication, reordering, and corruption
of packets during data transmission. These parameters affect the performance
of protocols and networks.

***Preliminary information:***
In addition to latency, many global and local area networks are affectedloss, reordering, corruption, and duplication of packets.
- ***Packet Loss***: a condition that occurs when a packet passing through
the network does not reach its destination. Packet loss can have a big
impact on high-bandwidth and high-latency networks.
A common cause of packet loss is the inability
of routers to hold packets arriving at a rate faster than
the sending speed. Even in cases where high
packet arrival rates are temporary (for example, short-term bursts
of traffic), the router is limited by the amount of buffer memory used for
instant packet storage. When packet loss occurs, TCP
reduces the congestion window and therefore the throughput by half.
- ***Reordering packages***: a condition that occurs when packets
are received in a different order from the one in which they were sent.
Packet reordering (unordered packet delivery) is usually
the result of packets following different routes to
reach their destination. Packet reordering can degrade
the throughput of TCP connections in high
-bandwidth, high-latency networks. For each segment received out of order,
the TCP receiver sends an acknowledgement (ACK) for the last correctly
received segment. As soon as the TCP sender receives three acknowledgements
for the same segment (triple duplicate ACK), the sender considers
that the receiver incorrectly received the packet following the packet that
is acknowledged three times. It then proceeds to reduce the congestion window
and throughput by half.
- ***Package Corruption:*** corruption of the bits that make up the packet can (
mostly) occur at the physical layer. Two adjacent devices
are connected by a physical channel (for example, fiber, twisted pair copper
, etc.). The physical layer receives the raw bit stream and
delivers it to the data link layer. If some bits are damaged they may have values that differ from those originally sent
by the node sender. The recipient node then simply discards the packet. As a result
, the TCP sending process will not receive an acknowledgement for the corresponding
segment and will consider it a lost segment. The TCP sender process
will subsequently reduce the congestion window and throughput
by half.
***Duplicate packages:*** a state where multiple copies of a packet
are present on the network and are received by the destination. Packet duplication
is the result of retransmissions when the sending node
retransmits unacknowledged (NACK) packets.

Problems that occur when packets are lost:
- Outdated information. The effect is noticeable in applications with high sensitivity-It is very slow and requires instant decision-making for certain user actions, such as in video games.
- Slow loading. The effect is noticeable when viewing a multimedia file.online content (social networks, live broadcasts, etc.).
- Interrupting the download. The effect is noticeable when the data transfer rate is lowand stopping the application or resource when loading
some data is not completed.
- Closing connections. Many web resources with no successful completion-If the connection is closed for a long period of time, the connection is closed after
a certain amount of time has elapsed.
- Incomplete information. Web pages that open may displaynot all elements, incomplete images, or even the website's format can
be completely wrong.Some common causes of packet loss:
- damaged equipment (damage to the network card, ports, etc.)-broken connections, faulty routers or switches,
bad wiring);
- limitation of equipment resources (equipment capacity);
- network congestion (network bottlenecks along the packet route);
- interference and noise in wireless networks;
- errors in the software of network devices.

**Tasks:**

1. Set the simplest topology consisting of two hosts and a switch
with the default mininet network 10.0.0.0/8.
2. Conduct interactive experiments to study
network parameters related to loss, duplication, reordering and packet loss during data transmission.
3. Implement a reproducible experiment to add a packet rejection rule in an emulated WAN. Display a summary of the lost packages on the screen.
4. Independently implement reproducible experiments to study network parameters related to loss, reordering and packet corruption during data transmission. Display a summary of the lost packages on the screen.

### Laboratory 6 - tbf : Configuring the global network bandwidth using the Token Bucket Filter
Purpose of the work: The main goal of the work is to get acquainted with the principles of
the Token Bucket Filter queue discipline, which generates incoming / outgoing
traffic to limit bandwidth, as well as to gain skills
in modeling and studying traffic behavior through
interactive and reproducible experiments in Mininet.

***Preliminary information:***


