
# Enhance! -picoCTF Write-up


---

## Description
A suspicious SVG (Scalable Vector Graphics) image was provided. The goal was to extract a hidden flag from this file. Since SVG is based on XML, any embedded `<text>` elements could potentially reveal the flag.

---


## Solution

### Step 1: Recognize the File Format
SVG files are just text-based XML documents. This means you can open and read them directly, or parse them with XML tools.

### Step 2: Parse the SVG Using Python

We use Python and BeautifulSoup to extract all the text embedded in the SVG:

```python
from bs4 import BeautifulSoup

# Load and parse the SVG file
with open("drawing.flag.svg", "r", encoding="utf-8") as f:
    svg_content = f.read()

soup = BeautifulSoup(svg_content, "xml")

# Extract all <text> elements
text_elements = soup.find_all("text")
texts = [text.get_text() for text in text_elements if text.get_text().strip()]

# Join the characters to form the flag
flag = ''.join(texts[0].split())  # remove spaces
print(flag)
```

### Step 3: Output

After running the script, we get the following extracted text:

```
p i c o C T F { 3 n h 4 n c 3 d _ 2 4 3 7 4 6 7 5 }
```

Which becomes:

```
picoCTF{3nh4nc3d_24374675}
```

---

## Flag
```
picoCTF{3nh4nc3d_24374675}
```

---

