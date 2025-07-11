
# Plumbing - PicoCTF Writeup

---

## Description

> Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?  
>
> Connect to `jupiter.challenges.picoctf.org 4427`.

We are asked to connect to a remote server. The server streams output that may contain a flag. We're told to find that flag **without relying on intermediate files** — hinting at the use of **pipes** and real-time processing.

---

## Solution

We begin by connecting to the server using [`nc` (Netcat)](https://linux.die.net/man/1/nc), which allows us to send and receive data over the network:

```bash
nc jupiter.challenges.picoctf.org 4427
```

We observe a stream of repetitive lines like:

```
Not a flag either  
I don't think this is a flag either  
This is definitely not a flag  
```

We scroll through dozens of lines like this.

---

### Step 1: Manually Read Output

We could try to read through it all manually, but the flag is easy to miss in the flood of similar text. We decide to use Unix pipes for a more efficient approach.

---

### Step 2: Use a Pipe to Filter Output

Although we’re asked to think beyond file-based methods, using **pipes** (as covered in the challenge text) is ideal here. With this command:

```bash
nc jupiter.challenges.picoctf.org 4427 | grep picoCTF
```

we connect to the server, then pipe its output directly into `grep` to search for the string `picoCTF`.

> The `grep` utility scans input line-by-line and prints lines that match a pattern—in this case, lines containing the flag format.

---

### Step 3: Capture the Flag

Eventually, the following line appears:

```
picoCTF{digital_plumb3r_5ea1fbd7}
```

That’s our flag!

---

## Final Flag

```
picoCTF{digital_plumb3r_5ea1fbd7}
```

---


