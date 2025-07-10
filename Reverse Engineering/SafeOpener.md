# Safe Opener – picoCTF Write-up

---

## Description

> Can you open this safe?  
> I forgot the key to my safe but this program is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

We are given Java source code that performs a Base64 encoding of the user input, and checks it against a hardcoded encoded string.

---

## Provided Code

```java
import java.io.*;
import java.util.*;  
public class SafeOpener {
    public static void main(String args[]) throws IOException {
        BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
        Base64.Encoder encoder = Base64.getEncoder();
        String encodedkey = "";
        String key = "";
        int i = 0;
        boolean isOpen;
        

        while (i < 3) {
            System.out.print("Enter password for the safe: ");
            key = keyboard.readLine();

            encodedkey = encoder.encodeToString(key.getBytes());
            System.out.println(encodedkey);
              
            isOpen = openSafe(encodedkey);
            if (!isOpen) {
                System.out.println("You have  " + (2 - i) + " attempt(s) left");
                i++;
                continue;
            }
            break;
        }
    }
    
    public static boolean openSafe(String password) {
        String encodedkey = "cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz";
        
        if (password.equals(encodedkey)) {
            System.out.println("Sesame open");
            return true;
        }
        else {
            System.out.println("Password is incorrect\n");
            return false;
        }
    }
}

```

## Solution
The check is done on a Base64-encoded value. To reverse it, we decode the hardcoded string.

Using base64 -d in a Linux/WSL terminal:

echo cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz | base64 -d

## Output
pl3as3_l3t_m3_1nt0_th3_saf3

This is the plain-text password expected by the Java program.

## Flag
picoCTF{pl3as3_l3t_m3_1nt0_th3_saf3}
