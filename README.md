# <div align="center">Ft_Irc - Internet Relay Chat</div>

### _Summary_

`FT_IRC` is an IRC server project that enables real-time messaging through text-based communication protocol on the Internet. The server is compliant with [RFC 1459](https://www.rfc-editor.org/rfc/rfc1459.html) and allows users to exchange direct messages and join group channels.

### _Introduction_

This project delves into the world of real-time communication protocols by implementing a dedicated IRC server. The Internet Relay Chat (IRC) protocol, defined in RFC 1459, facilitates text-based communication between users. Our server will allow clients to connect, join channels for group discussions, and engage in private messaging. By building this server, we aim to:

* Explore Network Programming: Gain practical experience with network programming concepts like client-server communication and message handling.

* Implement the IRC Protocol: Translate the RFC specifications into working code, understanding the structure and commands that govern IRC interactions.

* Foster Community Building: Provide a platform for users to connect and interact in real-time, replicating the collaborative spirit of the IRC ecosystem.

This project targets developers interested in distributed systems and network protocols, offering a hands-on approach to building a real-world communication tool.

### _General Rules_

The program is designed not to crash in any circumstance, including running out of memory or quitting unexpectedly. A Makefile is included that compiles the source files and includes rules for `$(NAME)`, `all`, `clean`, `fclean`, and `re`. The code is written in C++ 98 and complies with that standard. There are no external libraries or Boost libraries used.

### _Features_

`FT_IRC` server project comes with the following features:

-   Multiple clients can be handled simultaneously without ever hanging
-   Non-blocking I/O operations with only one poll() used to handle all operations (read, write, listen, etc.)
-   Supports authentication, setting a nickname, a username, joining a channel, and sending and receiving private messages
-   Messages sent from one client to a channel are forwarded to every other client that joined the channel
-   Supports operators and regular users
-   Implements commands that are specific to operators
-   Supports [LimeChat] as a reference client for evaluation purposes

### _Getting Started_

Follow these simple steps to get started with the IRC Server Project:

1. Clone the repository to your local machine:

```sh
https://github.com/HYYPNNOSS/Internet-Relay-Chat.git
```

2. Navigate to the project directory:

```sh
cd ft_irc
```

3. Compile the source files by running the make command:

```sh
make
```

4. Start the IRC server:

```sh
./ircserv <port> <password>
```

Replace `<port>` with the port number on which the server will be listening for incoming IRC connections and `<password>` with the connection password.

5. Connect to the server using an IRC client such as [LimeChat] or by using netcat with the following command:

```sh
nc -c localhost <port>
```

6. Authenticate with the server password and set your nickname and username:

```sh
PASS <password>
NICK <nickname>
USER <username> <mode> * :<realname>
```

7. Join or Create a channel:

```sh
JOIN <channel>
```

**Now you can start chatting!**


### _Commands_

Our server supports several commands, conforming to the [BNF] representation specified in RFC1459. Here are the commands and their [BNF] representations:

```bnf
Command: JOIN
Parameters: <channel>{,<channel>} [<key>{,<key>}]
```

The JOIN command is used to join a specific or multiple channels. The `<channel>` parameter specifies the channel to be joined, and the `<key>` parameter provides the channel password, if required.

```bnf
Command: INVITE
Parameters: <nickname> <channel>
```

The INVITE command is used to invite a user to a specific channel. The `<nickname>` parameter specifies the user to be invited, and the `<channel>` parameter specifies the channel to which the user is to be invited.

```bnf
Command: KICK
Parameters: <channel> <user> [ <comment> ]
```

The KICK command is used to kick a user from a specific channel. The `<channel>` parameter specifies the channel from which the user is to be kicked, and the `<user>` parameter specifies the user to be kicked. The `<comment>` parameter provides the reason for the kick.

```bnf
Command: LIST
Parameters: [ <channels> [ <server> ] ]
```

The LIST command is used to list all channels on the server. The `<channels>` parameter specifies the channels to be listed, and the `<server>` parameter specifies the server to be queried. If the `<channels>` and `<server>` parameters are omitted, the server will list all channels on the server.

```bnf
Command: MODE
Parameters: <channel> {[+|-]|o|p|s|i|t|n|b|v} [<limit>] [<user>] [<ban mask>]
```

The MODE command is provided so that channel operators may change the
   characteristics of `their' channel.  It is also required that servers
   be able to change channel modes so that channel operators may be
   created.

   The various modes available for channels are as follows:

           o - give/take channel operator privileges;
           p - private channel flag;
           s - secret channel flag;
           i - invite-only channel flag;
           t - topic settable by channel operator only flag;
           n - no messages to channel from clients on the outside;
           m - moderated channel;
           l - set the user limit to channel;


```bnf
Command: NAMES
Parameters: [<channel>{,<channel>}]
```

The NAMES command is used to list all users in a specific channel or all channels on the server. The `<channels>` parameter specifies the channel(s) to be listed, and the `<server>` parameter specifies the server to be queried. If the `<channels>` and `<server>` parameters are omitted, the server will list all users in all channels on the server.


```bnf
Command: NICK
Parameters: <nickname>
```

The NICK command is used to change a user's nickname. The `<nickname>` parameter specifies the new nickname.

```bnf
Command: NOTICE
Parameters: <nickname> <text>
```

The NOTICE command is used to send a notice message to a specific user. The `<nickname>` parameter specifies the user to whom the notice is to be sent, and the `<text>` parameter specifies the text of the notice.

```bnf
Command: OPER
Parameters: <username> <password>
```

Oper command is used to authenticate a user as an IRC operator or "ircop" (one who manages an IRC network) with a password.

```bnf
Command: PART
Parameters: <channel> [ <comment> ]
```

The PART command is used to leave a specific channel. The `<channel>` parameter specifies the channel to be left, and the `<comment>` parameter provides the reason for leaving the channel.

```bnf
Command: PASS
Parameters: <password>
```

The PASS command is used to provide a password for the connection. The `<password>` parameter specifies the password to be used.

```bnf
Command: PRIVMSG
Parameters: <receiver>{,<receiver>} <text to be sent>
```

PRIVMSG is used to send private messages between users.  <receiver> is the nickname of the receiver of the message.  <receiver> can also be a list of names or channels separated with commas.

```bnf
Command: QUIT
Parameters: [ <reason> ]
```

The QUIT command is used to disconnect from the server. The `<reason>` parameter provides the reason for disconnecting from the server.

```bnf
Command: TOPIC
Parameters: <channel> [ <topic> ]
```

The TOPIC command is used to set or retrieve the topic of a channel.

```bnf
Command: WHOIS
Parameters: <nickname> [ <server> ]
```

The WHOIS command is used to query information about a specific user. The `<nickname>` parameter specifies the nickname of the user to be queried, and the `<server>` parameter specifies the server to be queried.

### _Resources_

* [What is a Socket?](https://www.tutorialspoint.com/unix_sockets/what_is_socket.htm)
* [Unix Socket - Network Addresses](https://www.tutorialspoint.com/unix_sockets/network_addresses.htm)
* [Unix Socket - Core Functions](https://www.tutorialspoint.com/unix_sockets/socket_core_functions.htm)
* [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/html/)
* [The UChicago χ-Projects](http://chi.cs.uchicago.edu/chirc/index.html)
* [Internet Relay Chat Protocol](https://datatracker.ietf.org/doc/html/rfc1459)
* [Internet Relay Chat: Architecture](https://datatracker.ietf.org/doc/html/rfc2810)
* [Internet Relay Chat: Channel Management](https://datatracker.ietf.org/doc/html/rfc2811)
* [Internet Relay Chat: Client Protocol](https://datatracker.ietf.org/doc/html/rfc2812)
* [Internet Relay Chat: Server Protocol](https://datatracker.ietf.org/doc/html/rfc2813)
