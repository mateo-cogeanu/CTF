## Fawn

**Introduction**

What's up, hackers! Welcome back to Ctrl Alt Hack. In this tutorial, we're tackling the second box in HackTheBox's Starting Point: Fawn. This box focuses on the File Transfer Protocol, or FTP, which is often used for, well, transferring files! But here's the thing: FTP can be risky because it doesn't encrypt data by default. We'll be exploiting a misconfigured FTP service to capture the flag.

**Enumeration**

We start by checking our connection to the target machine using `ping`. This helps confirm that the target is reachable.

```bash
ping <target_IP>
```

Next, we use `nmap` to scan for open ports and services.

```bash
sudo nmap <target_IP>
```

This reveals that port 21 (FTP) is open. To get more information about the FTP service, we use `nmap` with the `-sV` flag for version detection.

```bash
sudo nmap -sV <target_IP>
```

The scan results show that the FTP server is running vsftpd 3.0.3 on a Unix system.

**Exploitation**

We’ll use the `ftp` command to interact with the FTP server. First, ensure that the `ftp` client is installed and up to date.

```bash
sudo apt install ftp -y
```

You can view the help menu for the `ftp` command using:

```bash
ftp -?
```

Now, connect to the target machine's FTP server:

```bash
ftp <target_IP>
```

At the login prompt, we attempt to connect anonymously.

```
Name (<target_IP>:<username>): anonymous
```

We can just simply press enter. anonymous login is allowed, so we will get a "Login successful" message with the response code 230.

Once logged in, we can use the `help` command to list available FTP commands. 

```
ftp> help
```

To list the files on the server, we use the `ls` command.
This reveals a file named `flag.txt`.

We download the file using the `get` command:

```
ftp> get flag.txt
```

Finally, we exit the FTP session with the `exit` command. The downloaded `flag.txt` file will be in your current working directory. You can view its content using `cat`:

```bash
cat flag.txt
```

This will display the flag, which you can submit on the HackTheBox platform.
