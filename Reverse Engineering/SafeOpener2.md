# Safe Opener 2 – picoCTF Write-up

---

## Description

> What can you do with this file?  
> I forgot the key to my safe but this file is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

We are given a compiled Java `.class` file. The goal is to decompile it and recover the password hardcoded in the binary.

---

## Provided Decompiled Code

```java
/*
 * Decompiled with CFR 0.152.
 */
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Base64;

public class SafeOpener {
    public static void main(String[] args) throws IOException {
        BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
        Base64.Encoder encoder = Base64.getEncoder();
        String encodedkey = "";
        String key = "";
        for (int i = 0; i < 3; ++i) {
            System.out.print("Enter password for the safe: ");
            key = keyboard.readLine();
            encodedkey = encoder.encodeToString(key.getBytes());
            System.out.println(encodedkey);
            boolean isOpen = SafeOpener.openSafe(encodedkey);
            if (isOpen) break;
            System.out.println("You have  " + (2 - i) + " attempt(s) left");
        }
    }

    public static boolean openSafe(String password) {
        String encodedkey = "picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_5bfbd6f1}";
        if (password.equals(encodedkey)) {
            System.out.println("Sesame open");
            return true;
        }
        System.out.println("Password is incorrect\n");
        return false;
    }
}

```

## Solution
This time, the Base64-encoded "password" is already fully hardcoded as the flag string. No decoding or reverse logic is needed — just decompilation.

We decompiled the .class file using the CFR Java decompiler:
java -jar cfr.jar SafeOpener.class

From the output, we see:
String encodedkey = "picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_5bfbd6f1}";

This is the expected input that the program checks against.

## Flag
picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_5bfbd6f1}
