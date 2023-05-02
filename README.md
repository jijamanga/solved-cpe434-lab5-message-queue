Download Link: https://assignmentchef.com/product/solved-cpe434-lab5-message-queue
<br>
There are many applications in which processes need to cooperate with each other. This is always the case for a variety of forms of inter-process communication that can be used under LINUX. These support resource sharing, synchronization, connectionless and connection-oriented data exchange or combinations of these.

Message queues are a refined method of inter process communication. As an application, we can implement a printer spooler using message queues. Some form of message passing between processes is now part of many modern operating systems. All messages are stored in the kernel, and have an associated message queue identifier. It is this identifier, which we call an msqid that identifies a particular queue of messages, processes read and write messages to arbitrary queues. Every message on a queue has the following attributes:

Long Integer Type

Length of data portion of message (can be 0)  Data (if length is greater than 0)

For every message queue in the system, the kernel maintains the following structure of information:




<table width="588">

 <tbody>

  <tr>

   <td width="588"># include &lt;sys/types.h&gt;# include &lt;sys/ipc.h&gt; ​/*defines the ipc_perm structure */  stuct msqid_ds{stuct ipc_perm msg_perm​; ​/* opertion permission struct */  struct ​msg ​*​msg_first​; ​/* ptr to first message on q */  struct ​msg ​*​msg _last​; ​/* ptr to last message on q */  ushort msg_cbytes​; ​/* current # bytes on q */  ushort msg_qnum​; ​/* current # of messages on q */  ushort msg_qbytes ​/* max # of bytes allowed on q */  ushort msg_lspid​; ​/* pid of last msgsnd */  ushort msg_lrpid​; ​/* pid of last msgrcv */  time_t msg_stime​; ​/* time of last msgsnd */  time_t msg_rtime​; ​/* time of last msgrcv */  time_t msg_ctime​; ​/* time of last msgct1 (that changed the above) */ ​}</td>

  </tr>

 </tbody>

</table>







<strong>             </strong>

<h1>Assignment</h1>

<strong>Create a Linux Chat Server  </strong>

You will write two applications (named Process A and Process B). Process A should create a message queue and write a message to the queue (read from user through stdin). Process A

should wait for data to be received from Process B. Process B should send some message to Process A using the message queue. The message sent by Process B should be user typed string through stdin. Process A should respond to Process B with another message sent through the

message queue. This is also the message typed by the user in Process A’s stdin. Keep the process of sending messages back and forth until one types “Exit”. The received messages should be displayed to the terminal by both process A and B.

Please make sure to delete the message queue after you are done.

<h1>Topics for Theory</h1>

<strong>int msgget (key_t key, int msgflag); ​</strong>// Functions for Creating and Handling Message Queues  <strong>int msgsnd (int msqid, struct msgbuf *ptr, int length, int flag); ​</strong>//function to send a message, id from above  <strong>int msgrcv (int msqid, struct msgbuf * ptr, int length ,long msgtype, int flag); ​</strong>//function

to Receive Message

<strong>int msgctl(int msqid, int cmd, struct msqid_ds *buff); ​</strong>// provides a variety of control operations on a message queue.

<h1>Coding Hint</h1>

Please find hint on page 11 onwards in the presentation slide uploaded in Shared Memory class. Especially, please go through pages 19 and onwards for hints.

You can use cpp constructs line cin and cout.

Create a shared header that contains the Key information, type information and structure specified in page 19 of ppt.

<strong>Process A:  </strong>

<ol>

 <li>Create a message queue using ​<em>msgget() ​</em>. Use IPC_CREAT flag with 0666 as you did for shared memory</li>

 <li>read user input using scanf/cin function from stdin. Copy this message to data part of the structure object.</li>

 <li>send the message using ​<em>msgsnd() ​</em>function

  <ol>

   <li>if message was ​<strong>Exit​</strong>, break</li>

  </ol></li>

 <li>receive message from Process B using ​<em>msgrcv() ​</em>function

  <ol>

   <li>compare the received message with ​<strong>Exit, ​</strong>if ​<strong>Exit ​</strong>break</li>

   <li>display message received</li>

  </ol></li>

 <li>Continue to Step 2</li>

 <li>Remove the message queue using ​<em>msgctl() ​</em>with IPC_RMID flag.</li>

</ol>

<strong>             </strong>

<strong>Process B:  </strong>

<ol>

 <li>Access the message queue created by Process A using ​<em>msgget() ​</em> You may need to create the same key.</li>

 <li>wait until you receive message from Process A

  <ol>

   <li>if the message was ​<strong>Exit​</strong>, break</li>

   <li>display message received</li>

  </ol></li>

 <li>read from user input</li>

 <li>send the message to Process A using message queue

  <ol>

   <li>if the message was ​<strong>Exit​</strong>, break</li>

  </ol></li>

 <li>Continue to Step 2</li>

 <li>Remove the message queue using ​<em>msgctl() ​</em></li>

</ol>

<h1>Research Online</h1>

<h2>Please include this in your report also</h2>

How do you make a process wait to receive a message and not return immediately?

Message Queue vs Shared Memory (discuss use and differences). Research use of function ​<strong>ftok()​</strong>, what is its use?  <strong>  </strong>

What does IPC_NOWAIT do?




Note: Please see the next page for lab report format.




<h1>Deliverables</h1>

<h2>Lab Report</h2>

The following material in each section is expected:

<ol>

 <li>Cover page with your name, lab number, course name, and dates</li>

 <li>Theory/Background (Material or methods relevant to the lab, a few sentences on each)

  <ol>

   <li>msgget()</li>

   <li>msgsnd()</li>

   <li>msgrcv()</li>

   <li>msgctl()</li>

  </ol></li>

 <li>Observations (Show output demonstrating the two processes can communicate using the message queue)</li>

 <li>Lab Questions (Make sure to answer the following with at least a few sentences)

  <ol>

   <li>How do you make a process wait to receive a message and not return immediately?</li>

   <li>Message Queue vs Shared Memory (discuss use and differences).</li>

   <li>Research use of function ​<strong>ftok()​</strong>, what is its use?</li>

   <li>What does IPC_NOWAIT do?</li>

  </ol></li>

 <li>Conclusion (Did your program work as expected, what can you take away from the lab?)</li>

 <li>Appendix (for source code, submit the text in a table)</li>

</ol>

The report should be submitted as a single pdf document with the source code for your program within it.