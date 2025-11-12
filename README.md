Title:-To study Telnet protocol
AIM: Perform Remote login using Telnet server
THEORY:
Telnet protocol allows you to connect to remote hosts over TCP/IP network. Telnet was
developed in 1969. Telnet was initially developed for private use where security was not
primary concern. Telnet protocol has serious security issue. Security expert recommend that
the use of Telnet for remote login should be discontinued under all normal circumstances.

● Telnet Server
● Telnet Client

Telnet Sever
Telnet server software is installed on remote host. You need to configure it before client
can connect with it.

Telnet Client

Telnet client software allows you to connect telnet server. Once telnet client establishes a
connection to the remote host, client becomes a virtual terminal, allowing you to
communicate with the remote host from your computer.
Security issue with Telnet

● Telnet by default does not encrypt any data sent over the connection.
● Anyone who has access to network device located on the network between the two
hosts like router, switch, hub or gateway where Telnet is being used can intercept the
packets

passing by and obtain login, password and whatever else is typed with a packet sniffer
software.

● Telnet protocol have no implementations that would ensure that communication is
carried out between the two hosts is not intercepted in the middle.

● In RHEL Telnet is part of the xinetd daemon.

● Telnet use plain text to transmit password.

● root user is not allowed to connect using Telnet.

● Command-line telnet clients are built into all major operating systems.


### **Procedure: Perform Remote Login Using Telnet Server**

1. **Start the System**
   Power on the computer systems that will act as **Telnet Server** and **Telnet Client**.

2. **Login as Root User**
   On both systems, log in with administrative privileges (root user or sudo access).

3. **Check Telnet Installation**
   On both server and client machines, verify whether Telnet packages are installed using the command:

   ```
   rpm -q telnet telnet-server
   ```

   If not installed, install them using:

   ```
   yum install telnet telnet-server -y
   ```

4. **Start and Enable Telnet Service**
   Start the Telnet service on the **server** using the following commands:

   ```
   systemctl start telnet.socket
   systemctl enable telnet.socket
   ```

   or, in older systems:

   ```
   service xinetd start
   chkconfig telnet on
   ```

5. **Check the Telnet Port (Port 23)**
   Ensure that Telnet service is listening on port 23:

   ```
   netstat -tnlp | grep 23
   ```

6. **Allow Telnet Through Firewall (if required)**
   On the server, open port 23 using the following commands:

   ```
   firewall-cmd --permanent --add-service=telnet
   firewall-cmd --reload
   ```

7. **Find the Server’s IP Address**
   On the server, check its IP address using:

   ```
   ifconfig
   ```

   or

   ```
   ip addr show
   ```

   Note the IP address for client connection.

8. **Connect to Telnet Server from Client**
   On the client system, open the terminal and type:

   ```
   telnet <server_ip_address>
   ```

   Example:

   ```
   telnet 192.168.1.10
   ```

9. **Login to the Remote System**
   When prompted, enter the **username** and **password** of a valid user on the Telnet server (not root).

10. **Verify Remote Access**
    After successful login, you will see the shell prompt of the remote system.
    Run a few basic commands like:

    ```
    hostname
    whoami
    pwd
    ```

    to confirm remote access.

11. **Exit from Telnet Session**
    To disconnect from the remote host, type:

    ```
    exit
    ```

12. **Stop Telnet Service (Optional)**
    For security reasons, stop the Telnet service after testing:

    ```
    systemctl stop telnet.socket
    ```

---

Conclusion –
Telnet is an application protocol used on the Internet or local area networks to provide a
bidirectional interactive text-oriented communication facility using a virtual terminal
connection. However, telnet by default does not encrypt any data sent over the connection
(including passwords), and so it is often feasible to eavesdrop on the communications and
use the password later for malicious purposes.

