---
layout: blog-detail
title:  "Suspicious USB Stick"
date:   april 7, 2021
categories: jekyll update
tag: something
titleimage: btlo.png
permalink: /blog/:title
excerpt_separator:  <!-- excerpt-end -->
---


### Challenge Description


→<!-- excerpt-start --> One of our clients informed us they recently suffered an employee data breach. As a startup company, they had a constrained budget allocated for security and employee  <!-- excerpt-end --> training. I visited them and spoke with the relevant stakeholders. I also collected some suspicious emails and a USB drive an employee found on their premises. While I am analyzing the suspicious emails, can you check the contents on the USB drive?


&nbsp;
&nbsp;
&nbsp;

**1. What file is the autorun.inf running?**

→ README.pdf


![autorun ><](/assets/img/blog1/1.png){: .center }


autorun.inf - It's a text file that can be used to automatically run some applications or load when some media like usb,cd/dvd is inserted.

![autorun ><](/assets/img/blog1/1p2.png){: .left }

For more info you can visit this link. [Click Here ](https://www.samlogic.net/articles/autorun-commands.htm)

&nbsp;
&nbsp;


**2. Does the pdf file pass virustotal scan? (No malicious results returned)**

→ False

As it also scans pdfs which is obvious.

![scan ><](/assets/img/blog1/2.png){: .left }

The pdf is utterly suspected as malicious.

![virtustotalscan ><](/assets/img/blog1/3.png){: .left }

&nbsp;
&nbsp;


**3. Does the file have the correct magic number?**

→ True

To check the signature , visit here: [Click Here](https://en.wikipedia.org/wiki/List_of_file_signatures)
![ signature ><](/assets/img/blog1/4.png){: .left }
The magic bytes matches with pdf magic bytes so the file has correct magic number.



Let's first analyze the pdf file with a tool pdfid.
https://blog.didierstevens.com/programs/pdf-tools

&nbsp;

<!-- <pre>
<b style="color:black;" > -->
```
/Page - the number of pages in pdf

/Encrypt - stipulates a password need to be read

/ObjStm - object streams

/Js - pdf file may contains js code which could be malicious to open

/AA and /OpenAction - action that will carried out automatically when we open a pdf file. Could automatically launch malicious js commands

/AcroForm - pdf form authored with Adobe Acrobat Pro/Standard

/JBIG2Decode - indicates pdf uses JBIG2Decode compression

/RichMedia - use to embed files,videos etc on pdf

/Launch - to lauch some actions

/EmbeddedFile - contains some external files

/XFA - XML Forms Architecture

/URI - Url to access
```
<!-- </b> 
</pre> -->

![ pdfidresult ><](/assets/img/blog1/5.png){: .left }


As we see it has some js contents which will automatically open on opening the pdf file and that seems particularly malicious.
The same type of result can be obtained via peepdf tool.
Here is the link: [Click Here](https://eternal-todo.com/tools/peepdf-pdf-analysis-tool) tut for this tool. You can also download the tool if you want. :) Btw it only runs in python2.
![ peepdf ><](/assets/img/blog1/6.png){: .left }



"pdf-parser - This tool will parse a PDF document to identify the fundamental elements used in the analyzed file. It will not render a PDF document."
On checking each objects , the object 28 seems rather interesting than other.
This is just my guess could be wrong.

 /F - indicates file

 /D - indicates directory

 /P - indicates path

![ peepdf ><](/assets/img/blog1/7.png){: .left }


&nbsp;
&nbsp;

**4. What OS type can the file exploit? (Linux, MacOS, Windows, etc)**

→ Windows

&nbsp;
&nbsp;


**5. A Windows executable is mentioned in the pdf file, what is it?**

→ cmd.exe


&nbsp;
&nbsp;

**6. How many suspicious /OpenAction elements does the file have?**

→ 1

&nbsp;
&nbsp;

Thank You :)

