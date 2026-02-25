## 🤖 Code Generation Prompt: CSS Tutorial Extractor

**Objective:** Act as a specialized code generator that analyzes Arabic CSS video tutorials (using the provided URLs) and produces perfectly structured, executable HTML and CSS file pairs for each lesson, strictly adhering to all defined file paths, file naming sequences, and formatting templates.

-----

### 1\. Input Data and Analysis

You will be given a list of YouTube URLs. For each URL, you must first process the video transcript and metadata to achieve the following:

1.  **Identify the Core Topic:** Determine the main CSS subject (e.g., "CSS Text Decoration," "CSS Z-Index").
2.  **Extract All Examples from transcript:** Identify all distinct, practical demonstrations of the CSS property and its various values (e.g., `list-style-type: square`, `calc((100% - 50px) / 4)`, `z-index: 10`).

-----

### 2\. File Generation and Naming Rules

For each successfully processed video, you must generate two files: an HTML file and a companion CSS file.

  * **File Sequencing:** File numbering must continue sequentially from the last generated file in the previous chat turn.
      * **Start the next sequence with file number `9`.** The first video processed must result in **`9.html`** and **`css/9.css`**. The next must be **`10.html`** and **`css/10.css`**, and so on.
  * **File Paths:** The HTML file must reside in the root directory, and the companion CSS file must reside inside a **`css/`** subdirectory.

-----

### 3\. Strict Formatting and Template Rules

All generated files **must** strictly comply with the following templates and constraints:

#### **A. Companion CSS File (`css/N.css`) Rules**

  * The file must be clearly divided into two logical sections using comments.
  * **"General Styling":** Includes necessary structural styles (e.g., box widths, borders, clearfixes) that are **not** the main focus of the lesson. **This content must NOT be copied to the HTML `<pre>` tag.**
  * **"Example CSS Rules":** Includes the minimal, essential CSS rules that demonstrate the lesson's concept. **This content MUST be copied verbatim to the HTML `<pre>` tag.**

#### **B. HTML File (`N.html`) Rules**

1.  **CSS Links:** The HTML must link to the companion CSS file (`css/N.css`) and a reference common CSS file (`../css/common.css`).
2.  **Metadata:** The `<title>` and `<h2>` (`#title-main`) elements must dynamically display the extracted **Core Topic**.
3.  **Navigation:** Navigation links (`Previous`, `Next`) must use the corresponding sequential file numbers.
4.  **Content Structure:** The main demonstration content must use numbered `<h4>` headings and descriptive `<p>` tags for each extracted example.
5.  **Critical `<pre>` Block Rule:**
      * The single `<pre id="pre">` tag is reserved exclusively for the CSS code that defines the lesson's main concepts.
      * **The CSS code inside the `<pre>` block must be indented exactly one time** (four spaces or one tab) from the `<pre>` tag.
      * **The CSS code block must start with a single blank newline** immediately after the opening `<pre id="pre">` tag.

-----

### 4\. Required Templates

Use these exact templates for generating the file structure. Replace `N` with the correct sequential file number and placeholder text with the extracted content.

#### **Template 1: Companion CSS File (`css/N.css`)**

```css
/*
 * CSS File for: [Extracted Video Title] - #N - [Extracted Topic]
 * Demonstrating the '[main property]' property.
 */

/* --- General Styling (For visual clarity, not included in the <pre> tag) --- */
/* Add necessary structural/layout styles here */

/* -------------------------------------------------------------------------- */


/* --- Example CSS Rules (Included in the <pre> tag) --- */

[CSS CODE FOR FIRST EXAMPLE]
[CSS CODE FOR SECOND EXAMPLE]
/* ... and so on for all extracted examples */
```

#### **Template 2: HTML File (`N.html`)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="css/N.css"> 
    <link rel="stylesheet" href="../css/common.css">
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            var title = "[Extracted Core Topic]"
            document.title = title;
            document.getElementById("title-main").innerHTML = title;
            document.getElementById("path").innerText = decodeURI(document.location.pathname).split('/')[2] + '/'
        });
    </script>
    <title></title>
</head>
<body>
    
    <section>
        <section class="intro">
            <a href="../../index.html" class="home-button">Go Home</a><br>
            <a href="N-1.html" class="prev-button">Previous</a>
            <a href="N+1.html" class="next-button">Next</a><br>
            
            <br><span id="path"></span><h2 style="display: inline;" id="title-main"></h2>
           
        </section>
        
        <pre id="pre">

    [CSS CODE FOR FIRST EXAMPLE]
    [CSS CODE FOR SECOND EXAMPLE]
    /* ... The entire content of the 'Example CSS Rules' section from N.css */
            
        </pre>
        <section>
            
            <h4>1. [Concept Summary for Example 1]</h4>
            <p>[Detailed explanation of this example]</p>
            <div class="[class-for-example-1]">[HTML element demonstrating the rule]</div>
            <hr>

            <h4>2. [Concept Summary for Example 2]</h4>
            <p>[Detailed explanation of this example]</p>
            <div class="[class-for-example-2]">[HTML element demonstrating the rule]</div>
            <hr>

        </section>
</body>
</html>
```