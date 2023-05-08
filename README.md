Download Link: https://assignmentchef.com/product/solved-prog1970-assignment-4-chat-client-server
<br>
TCP/IP is <strong><u>the most heavily used communications protocol</u></strong> for inter-process communication. It is broadly supported by the socket programming <em>paradigm</em> across multiple platforms. In this assignment, you will write a <strong>chat program</strong> to demonstrate the basics of socket-based TCP/IP communications.

<h1>Objectives</h1>

<ul>

 <li>Practice C Programming techniques for socket-level programming as well as multi-threaded solutions</li>

 <li>Practice the integration and use of a 3<sup>rd</sup> party library (NCURSES)</li>

</ul>

<h1>Requirements</h1>

<ol>

 <li>In this assignment – you are creating a system called CHAT-SYSTEM. This system is comprised of 2 applications – the server (called chat-server) and the client (called chat-client).  These names <u>must</u> be used and reflected in your system development structure. (Please refer to the “<u>Linux Development Project Code Structure</u>” document in the course content)</li>

 <li>Your solution architecture must be a central server model written in ANSI C.

  <ul>

   <li>The server must be multi-threaded. A new thread will be created each time a new user joins the conversation.  This thread will be responsible for accepting incoming messages from that user and broadcasting them to the other chat users. Call the server “chat-server”.</li>

   <li>QUESTION: How will each of the threads learn about all of the other threads and their IP addresses in order to send the message?  Think of a data structure that might be used to hold all client information (IP Address, the user name, etc.) within the server and will be visible and shared among all the communication threads.</li>

   <li>Your client application will be written to make use of the ncurses library in order to facilitate the multiple windows. Call the client program “chat-client”.</li>

   <li>I have provided some sample ncurses programs in the ncurses-samples.tar archive</li>

   <li>You may also want to experiment with threading the client program – one thread to handle the outgoing message window and one thread to handle the incoming messages window.</li>

   <li>The chat functionality must operate across computers that are in the same subnet</li>

  </ul></li>

 <li>Your chat solution must be able to <strong>support at least <u>2 users</u> being able to chat</strong> with each other.

  <ul>

   <li>This means that each person can see the messages in the conversation as it goes back and forth</li>

  </ul></li>

</ol>

– so each user’s message must be <em>tagged</em> with their name (or userID)

<ul>

 <li>Your server design must be able to support a maximum of 10 clients.</li>

</ul>

<ol start="4">

 <li>While running the CHAT-SYSTEM the minimum configuration must be:

  <ul>

   <li>The chat-server application must run on a Linux VM (MACHINE-A)</li>

   <li>One of the chat-client applications must run on a different Linux VM (MACHINE-B)</li>

   <li>The second chat-client application can run on the same Linux VM as the server (MACHINE-A)</li>

   <li>It is recommended that your chat-client application take at least 2 command-line switches as follows:</li>

  </ul></li>

</ol>

chat-client –user&lt;userID&gt; –server&lt;server name&gt;

Please see the section title “Finding the Server’s <em>Name</em>” below for more details and hints …

<ol start="5">

 <li>The chat solution client’s UI only needs to be very basic and simple.

  <ul>

   <li>You will need to incorporate the use of the <strong><em>ncurses</em></strong> library to do this</li>

   <li>The minimum UI requirement is show in Figure 1 at the end of the document. The basic UI consists of a prompt area (to allow a user to input a message) as well as a dedicated area on the screen to display the conversation. The message is sent to the recipient when the carriage return is pressed.</li>

   <li>As you can see by the extra <em>ncurses</em> resource links (at the end of the assignment) – you are also able to draw windows on the screen. You could use this concept to <em>soup up</em> your UI (as shown in Figure 2)</li>

  </ul></li>

 <li>Your solution must enforce and <strong>parcel all messages</strong> being input <strong>at the 40 character boundary</strong> The user should be allowed to enter a message of up to 80 characters. When the user hits the 80 character input boundary – the UI should stop accepting characters for input

  <ul>

   <li>As mentioned, the chat program will parcel up and send the outgoing message into 40 character lengths.</li>

   <li>So if the user happens to enter a message that is 56 characters in length before pressing ENTER (to send) – then one message of length 40 will be sent and another message of length 16 will be sent immediately following it.</li>

   <li>An example of this kind of message is shown in Figure 2 below</li>

   <li>As a usability factor – it would nice for your chat program to break the message at/near the 40 character boundary based on a space character (i.e. between words)</li>

  </ul></li>

</ol>

<table width="0">

 <tbody>

  <tr>

   <td colspan="3" width="598">QUESTION:  Is this parceling best handled by the originating client sending the message? Or</td>

  </tr>

  <tr>

   <td colspan="2" width="554">by the central server before it broadcasts to all clients? Or on the client receiving the</td>

   <td rowspan="2" width="44"> </td>

  </tr>

  <tr>

   <td width="92">message end?</td>

   <td width="462"> </td>

  </tr>

  <tr>

   <td width="92"></td>

   <td width="462"></td>

   <td width="44"></td>

  </tr>

 </tbody>

</table>

<ul>

 <li></li>

</ul>

<ol start="7">

 <li>The client’s incoming message window of your UI:

  <ul>

   <li>Should display each of the incoming messages in a specific format. This format is detailed in the <em>Incoming Message Formatting</em> section below and as well is also shown in the sample screenshots.</li>

  </ul></li>

</ol>

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="601">HINT: The fact that there are starting and stopping positions for fields in the message output</td>

  </tr>

  <tr>

   <td width="308">should indicate the potential solution for you …</td>

   <td width="293"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li></li>

</ul>

<ol start="8">

 <li>The client’s incoming message window should be able to show the history of <u>at most</u> the last 10</li>

</ol>

“lines” from the messages sent and received.  Please note that a message is allowed to take up 2

“lines” in the output window (i.e. one line for each of the 40 character messages) … this requirement indicates that a <u>maximum of 10 lines of output</u> are present in the message window before being scrolled …

<ol start="9">

 <li>Your solution should be architected such that messages should be received as soon as they are sent. And as well, if a message is received when the user is typing another message, it must not interrupt the message being currently composed.</li>

 <li>When the user enters the message “&gt;&gt;bye&lt;&lt;” – their client application will shut down properly.

  <ul>

   <li>The server can end the thread that is connected to this client and as well clean up any information dealing with the client.</li>

   <li>When the number of threads reaches zero in the server, it may shutdown properly</li>

  </ul></li>

 <li>There should be no debugging messages being printed to the screen in your final client and server programs.</li>

 <li>Your solution must be programmed to handle any and all errors gracefully.</li>

 <li>Your solution must be programmed to handle any and all shutdowns gracefully.</li>

 <li>If there are command line parameters available in either your client or server programs then make sure that a <strong><em>usage</em></strong> message appears if the parameters are incorrect or missing.</li>

 <li>Include the completed <u>A-04: Test Report</u> in your submission

  <ul>

   <li>This document does not have to be part of your cleaned, submitted TAR file</li>

  </ul></li>

 <li>Make sure to submit your commented, cleaned TAR file to the appropriate drop-box by the due date and time</li>

</ol>




<strong><u>What About the Message?</u></strong>

You need to think about what needs to be sent in the message and how it will be formatted.  When you are using sockets (or any low-level communication mechanism) one of the most exciting things is that you are in control of the messaging protocol!  You get to create the format of, program and enforce your own communication scheme.  So let’s consider what needs to be placed in the actual message – what pieces of information need to be sent between the chatting parties?

<ul>

 <li>The IP address of the incoming message can be gotten through the accept() function call– or you could include it in your message</li>

 <li>What about the name (5 characters) of the person sending the message?</li>

 <li>What about the actual message contents? Should it be parceled on the client before the original send? Or on the server before broadcasting?</li>

</ul>

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="704">Please document your messaging scheme and data structure used to manage the multiple client connections</td>

  </tr>

  <tr>

   <td width="277"><strong>in your server code file header comments</strong>.</td>

   <td width="427"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Make sure to include where/how the server will gain knowledge of the client IP and client’s user name</li>

 <li>Be sure to include documentation on how the server will handle the &gt;&gt;bye&lt;&lt; message and shutdown / clean-up after the client. And as well clean-up after itself (when all clients are gone)</li>

 <li>Also ensure to indicate how your server data structure is managing the list of all clients – do this by describing the structure / elements / values being stored for each client</li>

</ul>




<h1>ncurses Resources</h1>

Here are a couple of extra resources that you can use to do more in-depth research on the functionality and capabilities of the ncurses library.

<ul>

 <li><u><a href="https://www.cyberciti.biz/faq/linux-install-ncurses-library-headers-on-debian-ubuntu-centos-fedora/">Installing ncurses on Your Own Linux Installation</a></u></li>

 <li><u><a href="http://tldp.org/HOWTO/NCURSES-Programming-HOWTO/">Programmer’s Guide to ncurses</a></u></li>

 <li><u><a href="http://www.c-for-dummies.com/ncurses/">Another Programmer’s Guide (of sorts) </a><a href="http://www.c-for-dummies.com/ncurses/">– </a><a href="http://www.c-for-dummies.com/ncurses/">but with sample programs</a></u></li>

 <li><u><a href="https://edlinuxeditor.blogspot.ca/p/ncurses-library-tutorial.html">Simple “Hello World” Tutorial</a></u></li>

</ul>

<h1>Incoming Message Formatting</h1>

Here is the layout of each of the chat messages being sent from and/or received by your program – as well, an explanation of the format follows.

0               1       2  2                                        6 1               7       5  8                                        9

XXX.XXX.XXX.XXX_[AAAAA]_&gt;&gt;_aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa_(HH:MM:SS) — IP ADDR —  -USER     —————MESSAGE——————  –TIME–

<ul>

 <li>Should display the IP address of the message’s source</li>

 <li>in positions 1 through 15 of the output line</li>

 <li>Positions 16, 24, 27 and 68 should be spaces (as highlighted above)</li>

 <li>Should show the name of the person sending the message (max 5 characters) enclosed in square brackets (“[“ and “]”)</li>

 <li>in positions 17 through 23 (including the brackets)</li>

 <li>Should show the directionality of the message (i.e. &gt;&gt; for outgoing, &lt;&lt; for incoming)</li>

 <li>in positions 25 and 26</li>

 <li>you should see &gt;&gt; on your client if you sent the message</li>

 <li>you should see &lt;&lt; on your client if the message came from another client</li>

 <li>Should show the actual message (again max 40 characters)</li>

 <li>in positions 28 to 67</li>

 <li>Should show the a 24-hour clock received timestamp on the message enclosed in round brackets (“(“ and “)”)</li>

 <li>in positions 69 to 78 (including the brackets)</li>

 <li>this should reflect the time that the client received the message from the server</li>

</ul>

<strong> </strong>

<h1>Finding the Server’s <em>Name</em></h1>

As was discussed during the Module on <u>Sockets</u>, the underlying TCP/IP protocol being used in this solution works by knowing the name / identity or address of the computer you are trying to communicate with.




As you learned in OSF – computers can be given names (e.g. B03-213) and computers can be networked and be made part of a domain (e.g. conestogac.on.ca).  If we were trying to communicate with this computer within the domain then – we could open a TCP/IP communication to B03-213.conestogac.on.ca – and we would find ourselves talking to that computer!




You also learned in OSF that each computer on a network is assigned an IP address (IPv4 and IPv6).  This IP address also serves as the <em><u>name</u></em> of the computer when talking across any of the TCP/IP protocols.  In Windows, you learned about the ipconfig command which allows you to find the computer’s IP address.  In Linux the comparable command if ifconfig.




It is recommended that when constructing and running the CHAT-SYSTEM you find the server’s name by choosing the IPv4 address (referred to as the inet address (not inet6)) of the networking devices shown in the ifconfig command.  This command will show you many networking devices – the ethernet networking connection device will most likely be called something like eth0.

<h1></h1>

<strong> </strong>