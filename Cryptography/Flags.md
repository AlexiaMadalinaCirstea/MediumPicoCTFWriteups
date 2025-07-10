# Maritime Flags – picoCTF Write-up

---

## Description

> A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.  
>
> Try a frequency attack  
> Do the punctuation and the individual words help you make any substitutions?

We are provided with what appears to be a ciphertext and later a visual message encoded using **International Maritime Signal Flags** — the nautical communication system where each flag represents a letter or digit.

---

## Solution

We noticed a series of colorful flags in the format:


These flags match the **International Maritime Signal Flags** standard. A quick Google search or reference to the [Wikipedia page](https://en.wikipedia.org/wiki/International_maritime_signal_flags) helped us identify what each flag represents.

---

### Step 1: Identify the Flags

We carefully analyzed each flag from the image and matched them against their official maritime meanings. Here’s a mapping of the sequence:

P I C O C T F { F 1 A G 5 A N D 5 T U F F }


Each flag perfectly maps to a letter or number according to the standard.

---

### Step 2: Read the Flag

Putting all the decoded characters together:

picoCTF{F1AG5AND5TUFF} -> THE FLAG!