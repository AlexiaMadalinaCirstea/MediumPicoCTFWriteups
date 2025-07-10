
# ReadMyCert – picoCTF Write-up

---

## Description

> Can you take a look at this Certificate Signing Request (CSR) and get the flag from it?

We are given a `.csr` file which is a Certificate Signing Request. It contains information like the subject name, public key, and other relevant metadata typically used when applying for an SSL/TLS certificate.

---

## Solution

We use the `openssl` command-line tool to read the contents of the CSR file.

### Step 1: Run the following command

```bash
openssl req -in readmycert.csr -noout -text
```

This will print the decoded certificate data in a human-readable format.

---

## Decoded CSR Output (Relevant Snippet)

```
Subject: CN = picoCTF{read_mycert_57f58832}, name = ctfPlayer
```

Here, the Common Name (CN) field clearly contains the flag.

---

## Flag

```
picoCTF{read_mycert_57f58832}
```
