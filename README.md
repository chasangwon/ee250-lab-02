# Lab 2
[Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) this repo and clone it to your machine to get started!

## Team Members
Done individually

## Lab Question Answers

1. What is argc and *argv[]?
Main() receives command-line arguments through argv and argc. Argc is the number of strings pointed to by argv. The parameters can be omitted if main() is not intended to process command line arguments (https://stackoverflow.com/questions/3024197/what-does-int-argc-char-argv-mean)

2. What is a UNIX file descriptor and file descriptor table?
File descriptors are integers assigned to each file that is opened in a single process. File descriptor tables store the file descriptors as their entries. There is one table for each process. (https://stackoverflow.com/questions/5256599/what-are-file-descriptors-explained-in-simple-terms)

3. What is a struct? What's the structure of sockaddr_in?
Structs are a way of grouping related variables with one another. The variables in a struct, members, can be different data types. Sockaddr_in contains a short variable sin_family, an unsigned short variable sin_port, a struct of type in_addr called sin_addr, and a char array called sin_zero. (https://www.gta.ufrj.br/ensino/eel878/sockets/sockaddr_inman.html, https://www.w3schools.com/c/c_structs.php)

4. What are the input parameters and return value of socket()
Input parameters of socket() are three int variables. First is called domain, which specifies a communication domain, selecting the protocol family which will be used for communication. The given code passes on AF_INET, which represents IPv4 Internet protovol. The second input is called type specifying the communication semantics. SOCK_STREAM is passed on, providing reliable bidirectional byte streams. The third input is protocol, specifying the protocol to be used with the socket. 0 is passed on, meaning there is only one protocol to support a particular socket type. Socket() returns a file descriptor or -1. (https://man7.org/linux/man-pages/man2/socket.2.html)

5. What are the input parameters of bind() and listen()?
First input of bind() is sockfd, an int, second is a pointer to a struct of type sockaddr, and the last input is addrlen of type socklen_t. sockfd is a file descriptor that is assigned to addr the pointer. Addrlen specifies the size in bytes of the address struct pointed to by addr. The first input of bind() is an int called sockfd, and an int called backlog. Sockfd is a file descriptor referring to a socket. Backlof defines the max length to which the queue of pending connections for sockfd may grow. (https://man7.org/linux/man-pages/man2/listen.2.html, https://man7.org/linux/man-pages/man2/socket.2.html)

6.  Why use while(1)? Based on the code below, what problems might occur if there are multiple simultaneous connections to handle?
An infinite while loop is used to continue the sequence of sending and receiving data between the server and client, until the program is closed. The buffer may not be big enough to accommodate all inputs coming from multiple connections simultaneously.

7. Research how the command fork() works. How can it be applied here to better handle multiple connections?
Fork() creates a concurrent server that will run in parallel with other client connections. When a new client attempts to connect to the server, you can have an if statement that checks whether a child process was created successfully and send and receive data with the child process.


QA1
The server was not able to receive all numbers sent from the client. The Linux command forced a 50% loss on the packets that were sent. Since UDP doesn’t keep track of lost packets and does not bother to ask the client to resend the data, the server only displays some of the numbers.

QA2
The reliability of TCP was only slightly affected. It did not receive all numbers, but it still managed to receive most of them. Notwithstanding the failsafe mechanisms of TCP, the server was not able to retrieve all of the packets.

QA3
The speed of TCP slowed down significantly. The Linux command forced a 50% loss, and the server keeps track of the packets sent. As a result, when a packet is lost, TCP makes sure the any lost packet is sent again. Thus, it takes the server a longer time to receive input from the client.
