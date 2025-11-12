Here’s a clear and complete **procedure** for your experiment 👇

---

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

### **Result:**

Successfully performed remote login to a server using the **Telnet protocol** and verified communication between client and server systems.

---

Would you like me to also write **Observations and Result/Conclusion** (the next section after procedure, as per lab record format)?

