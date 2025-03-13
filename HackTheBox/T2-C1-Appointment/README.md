## Appointment: HackTheBox Starting Point Walkthrough

**Intro**

What's up, hackers! Welcome back to Ctrl Alt Hack. Today, we're tackling "Appointment," the fifth box in HackTheBox's Starting Point. This box is heavily focused on web applications and introduces us to SQL Injection, a classic and dangerous web vulnerability. We'll learn how attackers can exploit poorly written web applications to bypass normal authentication and access data they shouldn't.

**Enumeration**

As always, we start by checking if our target is alive with a good old `ping`:

```bash
ping <target_IP>
```

Now, let's use `nmap` to scan the target and see what services are running. We'll use the `-sV` flag for version detection:

```bash
sudo nmap -sV <target_IP>
```

This reveals that port 80 is open, running Apache httpd 2.4.38.

**Initial Web App Recon**

Let's navigate to the target IP in our browser. We're greeted with a login page. Now, before we jump to conclusions, it's good to enumerate further.

**Directory Brute-Forcing (Optional)**

Sometimes, there might be hidden directories. Tools like Gobuster can help us discover them. [cite: 64, 65, 66, 67, 68, 69, 70, 88, 89]

First, let’s install Gobuster (if you don’t have it already):

```bash
sudo apt install gobuster -y
```

Now, let's run Gobuster to see if we can find any hidden directories:

```bash
gobuster dir --url http://<target_IP>/ --wordlist /usr/share/wordlists/dirb/wordlist.txt
```

In this case, Gobuster doesn’t reveal anything particularly useful.

**Exploitation: SQL Injection**

Since directory brute-forcing didn't give us much, let's focus on that login form. SQL Injection is a common attack against web applications that use SQL databases. If user input isn't handled carefully, attackers can manipulate SQL queries.

In this case, we can bypass the login using a simple SQL Injection.

Try entering the following in the username field:

```
admin'#
```

And in the password field, you can enter anything you like. [cite: 165, 166]

The payload  `admin'#`  works because the single quote closes the username field in the SQL query, and the `#` comments out the rest of the query (which is the password check). This effectively bypasses the password check.

You should be logged in and see the flag!

**Claiming the Flag**

Copy the flag and submit it on HackTheBox. You’ve pwned Appointment!

**Outro**

And that’s another box down! SQL Injection is a serious vulnerability, and it’s crucial to understand how it works. Remember that input validation is key to preventing these attacks. If you enjoyed this walkthrough, smash that like button, subscribe to Ctrl Alt Hack, and hit the bell icon for more hacking content. Keep those queries secure, and I'll see you in the next video!