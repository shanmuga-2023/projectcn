# projectcn
Ex no. 2	HTTP Web Client Program to download a web page using TCP Sockets




PROGRAM
import java.net.*;
import java.io.*;
public class http
{
public static void main(String args[]) throws Exception
{
URL url=new URL(args[0]);
InputStream is=url.openStream();
DataInputStream dis=new DataInputStream(is);
String s="";
while((s=dis.readLine())!=null)
System.out.println(s);
dis.close();
is.close();
}
}

OUTPUT:

[USER01@telnet ~]$ java http http://www.naanmudhalvan.tn.gov.in
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.18.0 (Ubuntu)</center>
</body>
</html>


Ex_No:3A			ECHO CLIENT AND ECHO SERVER USING TCP SOCKETS




PROGRAM: SERVER
import java.io.*;
import java.net.*;
class echoserver
{
public static void main(String args[])throws Exception
{
ServerSocket ss=new ServerSocket(12543);
Socket s=ss.accept();
DataInputStream dis=new DataInputStream(s.getInputStream());
DataInputStream d=new DataInputStream(System.in);
PrintStream ps=new PrintStream(s.getOutputStream());
String s1=dis.readLine();
System.out.println("message from client:"+s1);
System.out.println("echo from server:"+s1);
ps.println(s1);
ss.close();
s.close();
}
}

PROGRAM:CLIENT
import java.io.*;
import java.net.*;
class echoclient
{
public static void main(String args[]) throws Exception
{
Socket s=new Socket("localhost",12543);
DataInputStream dis=new DataInputStream(s.getInputStream());
DataInputStream d=new DataInputStream(System.in);
PrintStream ps=new PrintStream(s.getOutputStream());
System.out.println("enter the message:");
String s1=d.readLine();
ps.println(s1);
System.out.println("message received from server:");
String s2=dis.readLine();
System.out.println(s2);
s.close();
}
}


OUTPUT FROM SERVER:

[241124@telnet ~]$ java echoserver

message from client:

hi

echo from server:

hi






OUTPUT FROM CLIENT:

[241124@telnet ~]$ java echoclient

enter the message:

hi

message received from server:

hi




Ex_No:3B			CLIENT-SERVER APPLICATION FOR CHAT USING TCP



PROGRAM:SERVER
import java.net.*;
class chatserver
{
public static void main(String args[]) throws Exception
{
ServerSocket ss=new ServerSocket(12501);
Socket s=ss.accept();
DataInputStream dis=new DataInputStream(s.getInputStream());
DataInputStream d=new DataInputStream(System.in);
PrintStream ps=new PrintStream(s.getOutputStream());
String s1="",s2="";
while(!s1.equals("stop")&&!s2.equals("stop"))
{
s1=dis.readLine();
System.out.println("\nclient:"+s1);
System.out.println("\nyou:");
s2=d.readLine();
ps.println(s2);
}
ss.close();
s.close();
}

PROGRAM CLIENT
import java.io.*;
import java.net.*;
class chatclient
{
public static void main(String args[]) throws Exception
{
Socket s=new Socket("LocalHost",12501);

DataInputStream dis=new DataInputStream(s.getInputStream());
DataInputStream d=new DataInputStream(System.in);
PrintStream ps=new PrintStream(s.getOutputStream());
String s1="",s2="";
while(!s1.equals("stop")&&!s2.equals("stop"))
{
System.out.print("\n you:");
s1=d.readLine();
ps.println(s1);

s2=dis.readLine();
System.out.println("\nserver:"+s2);
}
s.close();
}
}

OUTPUT FROM SERVER:

[241124@telnet ~]$ java chatserver

  client: 

  hello

  you:

  world




OUTPUT FROM CLIENT:

[241124@telnet ~]$ java chatclient

   you:

   hello

   server:

   world 

EX_NO:4   			Simulation of DNS using UDP



PROGRAM: SERVER
import java.io.*;
import java.net.*;
class server
{
public static void main(String args[])throws Exception
{
System.out.println("\n\n\tDNS Server Using UDP");
DatagramSocket ds=new DatagramSocket(8168);
InetAddressinet=InetAddress.getLocalHost();
String
IP_Address[]={"192.168.100.1","192.168.100.2","192.168.100.3","192.168.100.4","192.168.10
0.5"};
String Host_Name[]={"www.google.com","www.yahoo.com","Saranathan","annauniv","aicte"};
byte b1[]=new byte[100];
DatagramPacket dp1=new DatagramPacket(b1,b1.length);
ds.receive(dp1);
String s1=new String(b1);
System.out.print("\n\nDomain name received : "+s1);
s1=s1.trim();
int Host_Found=-1;
for(int i=0;i<5;i++)
{
if(Host_Name[i].equals(s1))
{
Host_Found=i;
break;
}
}
String host_ip="-1";
if(Host_Found!=-1)
host_ip=IP_Address[Host_Found];
byte[] b2 = host_ip.getBytes();
DatagramPacketdp=new DatagramPacket(b2,b2.length,inet,8167);
ds.send(dp);
}
}

PROGRAM: CLIENT
import java.io.*;
import java.net.*;
class client
{
public static void main(String args[])throws Exception
{
System.out.println("\n\n\tDNS Client using UDP");
byte b[]=new byte[100];
DatagramSocket ds=new DatagramSocket(8167);
InetAddress inet=InetAddress.getLocalHost();
System.out.print("\n\nEnter the Domain Name : ");
DataInputStream dis=new DataInputStream(System.in);
//String str=dis.readLine();
//b=str.getBytes();
System.in.read(b);
DatagramPacket dp=new DatagramPacket(b,b.length,inet,8168);
ds.send(dp);
byte b1[]=new byte[100];
DatagramPacket dp1=new DatagramPacket(b1,b1.length);
ds.receive(dp1);
String s1=new String(b1);
System.out.print("\n\nDomain IP Address : "+s1);
}
}

OUTPUT FROM SERVER:

[241122@telnet ~]$ java user2


        DNS Server Using UDP


Domain name received : www.google.com




OUTPUT FROM CLIENT:

 [241122@telnet ~]$ java user1


        DNS Client using UDP


Enter the Domain Name : www.google.com


Domain IP Address : 192.168.100.1


ExNo:6A  Program for simulating Address Resolution Protocol (ARP) 


PROGRAM: SERVER 
import java.io.*; 
import java.net.*; 
public class arpserver 
{ 
public static void main(String args[]) 
{ 
String 
IP_Address[]={"192.168.100.1","192.168.200.1","192.168.300.1","192.168.400.1","192.168.500.1"}; 
String MAC_Address[]={"57-H348-B2AQ01JY-6","93X-H64L-42AM-WHKY-4","IOV-JK48-2TAB-BEJY-8","89X-IOZ8-6ZLB-DHJY-3","XJH-4U18-3IAP-BPYS-7"}; 
String Send_msg,Recv_msg=""; 
try 
{ 
ServerSocket ss=new ServerSocket(9124); 
System.out.println("server started:\n"+ss); 
Socket s=ss.accept(); 
DataInputStream dis=new DataInputStream(s.getInputStream()); 
DataInputStream d=new DataInputStream(System.in); 
PrintStream ps=new PrintStream(s.getOutputStream()); 
Recv_msg=dis.readLine(); 
System.out.println("Request received is:"+Recv_msg); 
int Host_found=0; 
 for(int i=0;i<5;i++) 
 { 
 if(IP_Address[i].equals(Recv_msg))
 Host_found=i; 
 } 
 if(Host_found!=-1) 
 ps.println(MAC_Address[Host_found]); 
 else 
 ps.println(Host_found); 
 ps.close(); 
 s.close(); 
} 
catch(Exception se) 
{ 
System.out.println("Server Socket Problem"+se.getMessage()); 
}}} 

OUTPUT:
SERVER:
[241124@telnet ~]$ javac arpserver.java
[241124@telnet ~]$ java arpserver
server started:
ServerSocket[addr=0.0.0.0/0.0.0.0,port=0,localport=9124]

PROGRAM: CLIENT 
import java.io.*; 
import java.net.*; 
class arpcli 
{ 
public static void main(String args[]) 
{ 
String Send_msg,Recv_msg=""; 
try 
{ 
InetAddress ip=InetAddress.getLocalHost(); 
Socket s=new Socket(ip,9124); 
PrintStream ps=new PrintStream(s.getOutputStream()); 
DataInputStream dis=new DataInputStream(s.getInputStream()); 
DataInputStream d=new DataInputStream(System.in); 
System.out.println("\n\t\t***implementation of ARP***"); 
System.out.println("enter the ipaddress:"); 
Send_msg=d.readLine(); 
ps.println(Send_msg); 
Recv_msg=dis.readLine(); 
if(!Recv_msg.equals("-1")) 
{ 
System.out.println("MAC Address of given IP Address:"); 
System.out.println(Recv_msg); 
} 
else 
System.out.println("HOST NOT FOUND"); 
ps.close(); 
s.close(); 
} 
catch(Exception se) 
{ 
System.out.println("Exception"+se.getMessage()); 
}}} 

OUTPUT:
CLIENT:
[241124@telnet ~]$ javac arpcli.java
[241124@telnet ~]$ java arpcli

        ***implementation of ARP***
enter the ipaddress:
192.168.200.1
MAC Address of given IP Address:
93X-H64L-42AM-WHKY-4

ExNo:6B			Program for Implementation of Reverse Address Resolution Protocol (RARP)	



PROGRAM:Server

import java.io.*; 
import java.net.*; 
public class arpserver 
{ 
public static void main(String args[]) 
{ 
String 
IP_Address[]={"192.168.100.1","192.168.200.1","192.168.300.1","192.168.400.1","192.168.50
0.1"}; 
String MAC_Address[]={"57-H348-B2AQ01JY-6","93X-H64L-42AM-WHKY-4","IOV-JK48-
2TAB-BEJY-8","89X-IOZ8-6ZLB-DHJY-3","XJH-4U18-3IAP-BPYS-7"}; 
String Send_msg,Recv_msg=""; 
try 
{ 
ServerSocket ss=new ServerSocket(9126); 
System.out.println("server started:\n"+ss); 
Socket s=ss.accept(); 
DataInputStream dis=new DataInputStream(s.getInputStream()); 
DataInputStream d=new DataInputStream(System.in); 
PrintStream ps=new PrintStream(s.getOutputStream()); 
Recv_msg=dis.readLine(); 
System.out.println("Request received is:"+Recv_msg); 
int Host_found=-1; 
 for(int i=0;i<5;i++) 
 { 
 if(MAC_Address[i].equals(Recv_msg))
 Host_found=i; 
 } 
 if(Host_found!=-1) 
 ps.println(IP_Address[Host_found]);
 else 
 ps.println(Host_found); 
 ps.close(); 
 s.close(); 
} 
catch(Exception se) 
{ 
System.out.println("Server Socket Problem"+se.getMessage()); 
}}}







OUTPUT:Server

[241122@telnet ~]$ javac rarpserver.java                                                             
Note: rarpserver.java uses or overrides a deprecated API.                                            
Note: Recompile with -Xlint:deprecation for details.                                               
[241122@telnet ~]$ java rarpserver
server started:                                                                                   
ServerSocket[addr=0.0.0.0/0.0.0.0,port=0,localport=9126]                                            
Request received is:IOV-JK48-2TAB-BEJY-8




PROGRAM:Client

import java.io.*; 
import java.net.*; 
class arpcli 
{ 
public static void main(String args[]) 
{ 
String Send_msg,Recv_msg=""; 
try 
{ 
InetAddress ip=InetAddress.getLocalHost(); 
Socket s=new Socket(ip,9126); 
PrintStream ps=new PrintStream(s.getOutputStream()); 
DataInputStream dis=new DataInputStream(s.getInputStream()); 
DataInputStream d=new DataInputStream(System.in); 
System.out.println("\n\t\t***implementation of RARP***"); 
System.out.println("enter the macaddress:"); 
Send_msg=d.readLine(); 
ps.println(Send_msg); 
Recv_msg=dis.readLine(); 
if(!Recv_msg.equals("-1")) 
{ 
System.out.println("IP Address of given MAC Address:"); 
System.out.println(Recv_msg); 
System.out.println(Recv_msg); 
} 
else 
System.out.println("HOST NOT FOUND"); 
ps.close(); 
s.close(); 
} 
catch(Exception se) 
{ 
System.out.println("Exception"+se.getMessage()); 
}}}







OUTPUT:Client

[241122@telnet ~]$ javac rarpclient.java
[241122@telnet ~]$ java rarpclient

                ***implementation of RARP***
enter the macaddress:
IOV-JK48-2TAB-BEJY-8
IP Address of given MAC Address:
192.168.300.1
192.168.300.1

Exno: 7a Study of Network Simulator using nS2

#Create a simulator object
set ns [new Simulator]

#Open the nam trace file
set nf [open out.nam w]
$ns namtrace-all $nf

#Define a 'finish' procedure
proc finish {} {
        global ns nf
        $ns flush-trace
	#Close the trace file
        close $nf
	#Execute nam on the trace file
        exec nam out.nam &
        exit 0
}

#Create two nodes
set n0 [$ns node]
set n1 [$ns node]

#Create a duplex link between the nodes
$ns duplex-link $n0 $n1 1Mb 10ms DropTail

#Create a UDP agent and attach it to node n0
set udp0 [new Agent/UDP]
$ns attach-agent $n0 $udp0

# Create a CBR traffic source and attach it to udp0
set cbr0 [new Application/Traffic/CBR]
$cbr0 set packetSize_ 500
$cbr0 set interval_ 0.005
$cbr0 attach-agent $udp0

#Create a Null agent (a traffic sink) and attach it to node n1
set null0 [new Agent/Null]
$ns attach-agent $n1 $null0

#Connect the traffic source with the traffic sink
$ns connect $udp0 $null0  

#Schedule events for the CBR agent
$ns at 0.5 "$cbr0 start"
$ns at 4.5 "$cbr0 stop"
#Call the finish procedure after 5 seconds of simulation time
$ns at 5.0 "finish"

#Run the simulation
$ns run

ExNo : 7b Simulation of Congestion Control Algorithm


set ns [new Simulator]   
set f [ open congestion.tr w ]
$ns trace-all $f 
set nf [ open congestion.nam w ]
$ns namtrace-all $nf    

$ns color 1 Red
$ns color 2 Blue
$ns color 3 White
$ns color 4 Green

#to create nodes
set n0 [$ns node]
set n1 [$ns node]
set n2 [$ns node]
set n3 [$ns node]
set n4 [$ns node]
set n5 [$ns node]

# to create the link between the nodes with bandwidth, delay and queue
$ns duplex-link $n0 $n2   2Mb  10ms DropTail
$ns duplex-link $n1 $n2   2Mb  10ms DropTail
$ns duplex-link $n2 $n3 0.3Mb 200ms DropTail
$ns duplex-link $n3 $n4 0.5Mb  40ms DropTail
$ns duplex-link $n3 $n5 0.5Mb  30ms DropTail

# Sending node with agent as Reno Agent
set tcp1 [new Agent/TCP/Reno]
$ns attach-agent $n0 $tcp1
set tcp2 [new Agent/TCP/Reno]
$ns attach-agent $n1 $tcp2
set tcp3 [new Agent/TCP/Reno]
$ns attach-agent $n2 $tcp3
set tcp4 [new Agent/TCP/Reno]
$ns attach-agent $n1 $tcp4

$tcp1 set fid_ 1
$tcp2 set fid_ 2
$tcp3 set fid_ 3
$tcp4 set fid_ 4

# receiving (sink) node
set sink1 [new Agent/TCPSink]
$ns attach-agent $n4 $sink1
set sink2 [new Agent/TCPSink]
$ns attach-agent $n5 $sink2
set sink3 [new Agent/TCPSink]
$ns attach-agent $n3 $sink3
set sink4 [new Agent/TCPSink]
$ns attach-agent $n4 $sink4

# establish the traffic between the source and sink
$ns connect $tcp1 $sink1
$ns connect $tcp2 $sink2
$ns connect $tcp3 $sink3
$ns connect $tcp4 $sink4

# Setup a FTP traffic generator on "tcp"
set ftp1 [new Application/FTP]
$ftp1 attach-agent $tcp1
$ftp1 set type_ FTP

set ftp2 [new Application/FTP]
$ftp2 attach-agent $tcp2
$ftp2 set type_ FTP 

set ftp3 [new Application/FTP]
$ftp3 attach-agent $tcp3
$ftp3 set type_ FTP

set ftp4 [new Application/FTP]
$ftp4 attach-agent $tcp4
$ftp4 set type_ FTP                


# RTT Calculation Using Ping ------------------------------------------------

set p0 [new Agent/Ping]
$ns attach-agent $n0 $p0
set p1 [new Agent/Ping]
$ns attach-agent $n4 $p1

#Connect the two agents
$ns connect $p0 $p1

# Method call from ping.cc file
Agent/Ping instproc recv {from rtt} {
$self instvar node_
puts "node [$node_ id] received ping answer from \
$from with round-trip-time $rtt ms."
}

# ---------------------------------------------------------------------------


# start/stop the traffic
$ns at 0.2 "$p0 send"
$ns at 0.3 "$p1 send"
$ns at 0.5   "$ftp1 start"
$ns at 0.6   "$ftp2 start"
$ns at 0.7 "$ftp3 start"
$ns at 0.8   "$ftp4 start"
$ns at 66.0 "$ftp4 stop"
$ns at 67.0  "$ftp3 stop"
$ns at 68.0 "$ftp2 stop"
$ns at 70.0 "$ftp1 stop"
$ns at 70.1 "$p0 send"
$ns at 70.2 "$p1 send"

# Set simulation end time
$ns at 80.0 "finish"            

# procedure to plot the congestion window
# cwnd_ used from tcp-reno.cc file
proc plotWindow {tcpSource outfile} {
   global ns
   set now [$ns now]
   set cwnd_ [$tcpSource set cwnd_]

# the data is recorded in a file called congestion.xg.
   puts  $outfile  "$now $cwnd_"
   $ns at [expr $now+0.1] "plotWindow $tcpSource  $outfile"
}

set outfile [open  "congestion.xg"  w]
$ns  at  0.0  "plotWindow $tcp1  $outfile"
proc finish {} {
 exec nam congestion.nam &
 exec xgraph congestion.xg -geometry 300x300 &
exit 0
}
# Run simulation 
$ns run

Exno: 8 Study of TCP/UDP Performance Using Simulation Tool

set ns [new Simulator]

#Define different colors for data flows (for NAM)
$ns color 1 Blue
$ns color 2 Red

#Open the Trace files
set file1 [open out.tr w]
set winfile [open WinFile w]
$ns trace-all $file1

#Open the NAM trace file
set file2 [open out.nam w]
$ns namtrace-all $file2

#Define a 'finish' procedure
proc finish {} {
        global ns file1 file2
        $ns flush-trace
        close $file1
        close $file2
        exec nam out.nam &
        exit 0
}

#Create six nodes
set n0 [$ns node]
set n1 [$ns node]
set n2 [$ns node]
set n3 [$ns node]
set n4 [$ns node]
set n5 [$ns node]

#Create links between the nodes
$ns duplex-link $n0 $n2 2Mb 10ms DropTail
$ns duplex-link $n1 $n2 2Mb 10ms DropTail
$ns simplex-link $n2 $n3 0.3Mb 100ms DropTail
$ns simplex-link $n3 $n2 0.3Mb 100ms DropTail
$ns duplex-link $n3 $n4 0.5Mb 40ms DropTail
$ns duplex-link $n3 $n5 0.5Mb 30ms DropTail

#Give node position (for NAM)
$ns duplex-link-op $n0 $n2 orient right-down
$ns duplex-link-op $n1 $n2 orient right-up
$ns simplex-link-op $n2 $n3 orient right
$ns simplex-link-op $n3 $n2 orient left
$ns duplex-link-op $n3 $n4 orient right-up
$ns duplex-link-op $n3 $n5 orient right-down


#Set Queue Size of link (n2-n3) to 10
$ns queue-limit $n2 $n3 20

#Setup a TCP connection
set tcp [new Agent/TCP/Newreno]
$ns attach-agent $n0 $tcp
set sink [new Agent/TCPSink/DelAck]
$ns attach-agent $n4 $sink
$ns connect $tcp $sink
$tcp set fid_ 1
$tcp set window_ 8000
$tcp set packetSize_ 552

#Setup a FTP over TCP connection
set ftp [new Application/FTP]
$ftp attach-agent $tcp
$ftp set type_ FTP


#Setup a UDP connection
set udp [new Agent/UDP]
$ns attach-agent $n1 $udp
set null [new Agent/Null]
$ns attach-agent $n5 $null
$ns connect $udp $null
$udp set fid_ 2

#Setup a CBR over UDP connection
set cbr [new Application/Traffic/CBR]
$cbr attach-agent $udp
$cbr set type_ CBR
$cbr set packet_size_ 1000
$cbr set rate_ 0.01mb
$cbr set random_ false

$ns at 0.1 "$cbr start"
$ns at 1.0 "$ftp start"
$ns at 124.0 "$ftp stop"
$ns at 124.5 "$cbr stop"

# next procedure gets two arguments: the name of the
# tcp source node, will be called here "tcp",
# and the name of output file.

proc plotWindow {tcpSource file} {
global ns
set time 0.1
set now [$ns now]
set cwnd [$tcpSource set cwnd_]
set wnd [$tcpSource set window_]
puts $file "$now $cwnd"
$ns at [expr $now+$time] "plotWindow $tcpSource $file" }
$ns at 0.1 "plotWindow $tcp $winfile"

$ns at 125.0 "finish"
$ns run


Exno:9 Simulation of Distance Vector/Link State Algorithm

set ns [new Simulator]

$ns color 1 Blue
$ns color 2 Red

set nr [open dv.tr w]
set nr1 [open dv1.tr w]
set nr2 [open dv2.tr w]

$ns trace-all $nr
set nf [open dvProgram1.nam w]


$ns namtrace-all $nf

        proc finish { } {
        global ns nr nf
        $ns flush-trace
        close $nf
        close $nr
        exec nam dvProgram1.nam &
 exec xgraph dv1.tr dv2.tr -geometry 800x400 &
	exit 0
        }

proc record {} {
        global sink0 sink1 nr1 nr2
 #Get an instance of the simulator
 set ns [Simulator instance]
 #Set the time after which the procedure should be called again
        set time 0.5
 #How many bytes have been received by the traffic sinks?
        set bw0 [$sink0 set bytes_]
        set bw1 [$sink1 set bytes_]
     #   set bw2 [$sink2 set bytes_]
 #Get the current time
        set now [$ns now]
 #Calculate the bandwidth (in MBit/s) and write it to the files
        puts $nr1 "$now [expr $bw0/$time*8/1000000]"
        puts $nr2 "$now [expr $bw1/$time*8/1000000]"
       # puts $f2 "$now [expr $bw2/$time*8/1000000]"
 #Reset the bytes_ values on the traffic sinks
        $sink0 set bytes_ 0
        $sink1 set bytes_ 0
        #$sink2 set bytes_ 0
 #Re-schedule the procedure
        $ns at [expr $now+$time] "record"
}


for { set i 0 } { $i < 13} { incr i 1 } {
	set n($i) [$ns node]}

for {set i 0} {$i < 6} {incr i} {
$ns duplex-link $n($i) $n([expr $i+1]) 1Mb 10ms DropTail }
$ns duplex-link $n(0) $n(2) 1Mb 10ms DropTail
$ns duplex-link $n(0) $n(3) 1Mb 10ms DropTail
$ns duplex-link $n(0) $n(5) 1Mb 10ms DropTail
$ns duplex-link $n(0) $n(6) 1Mb 10ms DropTail
$ns duplex-link $n(0) $n(4) 1Mb 10ms DropTail
$ns duplex-link $n(1) $n(7) 1Mb 10ms DropTail
$ns duplex-link $n(2) $n(8) 1Mb 10ms DropTail
$ns duplex-link $n(3) $n(9) 1Mb 10ms DropTail
$ns duplex-link $n(4) $n(10) 1Mb 10ms DropTail
$ns duplex-link $n(5) $n(11) 1Mb 10ms DropTail
$ns duplex-link $n(6) $n(12) 1Mb 10ms DropTail
$ns duplex-link $n(6) $n(1) 1Mb 10ms DropTail
$ns duplex-link $n(7) $n(12) 1Mb 10ms DropTail

for {set i 7} {$i < 12} {incr i} {
$ns duplex-link $n($i) $n([expr $i+1]) 1Mb 10ms DropTail }



set tcp0 [new Agent/TCP]
$tcp0 set class_ 2
$ns attach-agent $n(12) $tcp0
set sink0 [new Agent/TCPSink]
$ns attach-agent $n(0) $sink0
$ns connect $tcp0 $sink0

#Attach FTP Application over TCP
set ftp0 [new Application/FTP]
$ftp0 attach-agent $tcp0
$ftp0 set type_ FTP
$ftp0 set packetSize_ 200

set tcp1 [new Agent/TCP]
$tcp1 set class_ 1
$ns attach-agent $n(9) $tcp1
set sink1 [new Agent/TCPSink]
$ns attach-agent $n(0) $sink1
$ns connect $tcp1 $sink1

#Attach FTP Application over TCP
set ftp1 [new Application/FTP]
$ftp1 attach-agent $tcp1
$ftp1 set type_ FTP
$ftp1 set packetSize_ 200


$ns rtproto DV 

$ns rtmodel-at 2.0 down $n(0) $n(6)
$ns rtmodel-at 3.0 down $n(0) $n(5)
$ns rtmodel-at 2.0 down $n(0) $n(1)
$ns rtmodel-at 20.0 up $n(0) $n(6)
$ns rtmodel-at 2.0 down $n(3) $n(9)
$ns rtmodel-at 2.0 down $n(6) $n(12)
$ns rtmodel-at 10.0 up $n(6) $n(12)
$ns rtmodel-at 15.0 up $n(3) $n(9)
$ns rtmodel-at 18.0 up $n(0) $n(1)
$ns rtmodel-at 25.0 up $n(0) $n(5)

$ns at 0.0 "record"

$ns at 0.2 "$ftp0 start"
#$ns at 30.0 "$ftp0 stop"

$ns at 1.0 "$ftp1 start"
#$ns at 30.0 "$ftp1 stop"

$ns at 30.0 "finish"
$ns run


Exno:09 B	Simulation of link state routing algorithm

set ns [new Simulator]
set nr [open thro.tr w]
$ns trace-all $nr
set nf [open thro.nam w]
$ns namtrace-all $nf
proc finish {} {
global ns nr nf
$ns flush-trace
close $nf
close $nr
exec nam thro.nam &
exit 0
}
for { set i 0} { $i <12 } { incr i 1 } {
set n($i) [$ns node]}
for {set i 0} {$i <8} {incr i} {
$ns duplex-link $n($i) $n([expr $i+1]) 1Mb 10ms DropTail}
$ns duplex-link $n(0) $n(8) 1Mb 10ms DropTail
$ns duplex-link $n(1) $n(10) 1Mb 10ms DropTail
$ns duplex-link $n(0) $n(9) 1Mb 10ms DropTail
$ns duplex-link $n(9) $n(11) 1Mb 10ms DropTail
$ns duplex-link $n(10) $n(11) 1Mb 10ms DropTail
$ns duplex-link $n(11) $n(5) 1Mb 10ms DropTail
set udp0 [new Agent/UDP]
$ns attach-agent $n(0) $udp0
set cbr0 [new Application/Traffic/CBR]
$cbr0 set packetSize_ 500
$cbr0 set interval_ 0.005
$cbr0 attach-agent $udp0
set null0 [new Agent/Null]
$ns attach-agent $n(5) $null0
$ns connect $udp0 $null0
set udp1 [new Agent/UDP]
$ns attach-agent $n(1) $udp1
set cbr1 [new Application/Traffic/CBR]
$cbr1 set packet Size_ 500
$cbr1 set interval_ 0.005
$cbr1 attach-agent $udp1
set null0 [new Agent/Null]
$ns attach-agent $n(5) $null0
$ns connect $udp1 $null0
$ns rtproto LS
$ns rtmodel-at 10.0 down $n(11) $n(5)
$ns rtmodel-at 15.0 down $n(7) $n(6)
$ns rtmodel-at 30.0 down $n(11) $n(5)
$ns rtmodel-at 20.0 down $n(7) $n(6)
$udp0 set fid_ 1$udp1 set fid_ 2
$ns color 1 Red
$ns color 2 Green
$ns at 1.0 "$cbr0 start"
$ns at 2.0 "$cbr1 start"
$ns at 45 "finish"
$ns run


ExNo 10: 		Simulation of an Error Correction Code (Like CRC)

import java.io.*;
class CRC
{
	public static void main(String args[])throws IOException
	{
		BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
		System.out.println("Enter Generator:");
		String gen=br.readLine();		
		System.out.println("Enter Data:");
		String data=br.readLine();
		String code=data;	
		while(code.length()<(data.length()+gen.length()-1))
		code=code+"0";
		code=data+div(code,gen);
		System.out.println("The transmitted code word is:"+code);
		System.out.println("Please enter the received code word:");
		String rec=br.readLine();	
		if(Integer.parseInt(div(rec,gen))==0)
		System.out.println("The received code word contains no errors.");
		else
		System.out.println("The received code word contains errors.");
	}
	static String div(String num1,String num2)
	{
		int pointer=num2.length();
		String result=num1.substring(0,pointer);
		String remainder="";
		for(int i=0;i<num2.length();i++)
		{
			if(result.charAt(i)==num2.charAt(i))
			remainder+="0";
			else
			remainder+="1";
		}
		while(pointer<num1.length())
		{
			if(remainder.charAt(0)=='0')
			{
				remainder=remainder.substring(1,remainder.length());
				remainder=remainder+String.valueOf(num1.charAt(pointer));
				pointer++;
			}
			result=remainder;
			remainder="";
			for(int i=0;i<num2.length();i++)
			{
				if(result.charAt(i)==num2.charAt(i))
				remainder+="0";
				else
				remainder+="1";
			}
		}
		return remainder.substring(1,remainder.length());
	}
}


Output :

Enter Generator:1011
Enter Data:1001010
The transmitted Code Word is: 1001010111


Please enter the received Code Word: 1001010111
The received code word contains no errors


Please enter the received Code Word: 
1110110111

The received code word contains errors.

EX5 Experiment: Packet Capturing and Analysis using Wireshark

### **AIM:**

To study and analyze the data packets transmitted over a network using **Wireshark**, a packet sniffing and protocol analysis tool.

THEORY:

Wireshark is a **network protocol analyzer** that captures and displays the data packets flowing through a network interface in real-time. It allows users to inspect each packet’s **source and destination addresses**, **protocols used**, **port numbers**, and **payload data**.

Wireshark uses the **Npcap** (Network Packet Capture) library for packet capturing. When running in **promiscuous mode**, it can capture all the packets on a LAN, not just those addressed to the host system.

Wireshark supports two types of filters:

1. **Capture Filters** – Applied before data is captured (to limit the data being recorded).
2. **Display Filters** – Applied after capture (to analyze specific packets from recorded data).

Common **capture filters** include:

* `host <IP>` – Capture traffic to/from a specific host
* `net <network>` – Capture traffic from/to a subnet
* `port <number>` – Capture traffic on a specific port
* Logical operators such as `and`, `or`, `not` can be used to combine filters

Common **display filters** include:

* `tcp.port == 80` – Displays all TCP packets on port 80 (HTTP traffic)
* `udp.port == 53` – Displays DNS packets
* `ip.src == 192.168.1.5` – Filters packets from a specific source IP
* `http.request.uri contains "login"` – Displays HTTP requests containing “login” in the URI

---

### **PROCEDURE:**

1. **Open Wireshark:** Launch the application with administrator privileges.
2. **Select Interface:** Choose the network interface card (Ethernet/Wi-Fi) on which to capture packets.
3. **Set Capture Filter (Optional):** Define filters such as `host 192.168.1.1` or `port 80` to limit capture data.
4. **Start Capture:** Click on the **Start Capturing Packets** icon.
5. **Generate Network Traffic:**

   * Browse a website, ping a remote system, or transfer files to generate traffic.
6. **Stop Capture:** Click on the **Stop** icon once sufficient data is captured.
7. **Analyze Packets:**

   * The **Top Pane** shows each packet with timestamp, source, destination, protocol, and brief info.
   * The **Middle Pane** shows details of the selected packet (Ethernet, IP, TCP/UDP, etc.).
   * The **Bottom Pane** displays the raw data (in hexadecimal and ASCII).
8. **Apply Display Filters:**

   * Type filters like `tcp`, `udp`, `http`, or `icmp` in the filter bar to focus on specific protocols.
   * Right-click on any field → *Apply as Filter* → choose *Selected / and / or / not* for deeper analysis.
9. **Save or Export Data:** Captured data can be saved as `.pcap` files for further study.

Example Packet Details:

| Source IP      | Destination IP | Protocol | Length | Info                 |
| -------------- | -------------- | -------- | ------ | -------------------- |
| 192.168.1.10   | 172.217.160.78 | TCP      | 74     | HTTP GET request     |
| 172.217.160.78 | 192.168.1.10   | TCP      | 66     | HTTP 200 OK response |



### **APPLICATIONS:**

* Network troubleshooting and debugging
* Security analysis and intrusion detection
* Educational and research purposes
* Monitoring bandwidth usage and network performance
### **RESULT:**

Thus, the **Wireshark tool** was successfully used to capture, filter, and analyze network packets. The experiment helped understand the structure of packets, communication protocols, and network traffic flow.
