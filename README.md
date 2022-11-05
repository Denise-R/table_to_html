Denise Rauschendorfer

10/17/2022


# __Table_to_HTML__

In this repository a function, "<span style="color:red">table_to_html</span>", is defined that transforms any table into a HTML file. This function was originally created to help my brother, James Rauschendorfer, upload supplemental information to a website for his PhD; however, this function may also be a useful way for others to publically share raw data and upload it to a website.

The following code was executed using Python 3.10.7. 

## __Defining the function__

### __Section 1:__
In order to run the following code, the modules '<span style="color:red">re</span>' and '<span style="color:red">airium</span>' need to be imported.

```
import re
import airium
```


### __Section 2:__
To begin creating the function <span style="color:red">table_to_html</span>, the source file needs to be transcribed into a <span style="color:blue">list</span> where each value (separated by commas/tabs/etc.) in the source file is a different element in the <span style="color:blue">list</span>. 


*Note: All of <span style="color:orange">Sections 2-3</span> are contained within the 'def table_to_html(table_address, delineator, filename_html):'*

To accomplish this, the following steps are taken:
1. <span style="color:red">def</span> is used to begin defining the function <span style="color:red">table_to_html</span> with the variables <span style="color:blue">table_address</span>, <span style="color:blue">delineator</span>, and <span style="color:blue">filename_html</span>.
2. The <span style="color:blue">table_address</span> is then opened as <span style="color:blue">table</span> in read (<span style="color:blue">r</span>) mode.
3. An array/nested-list titled <span style="color:blue">list</span> is created.
4. A for loop is created to iterate through each line in the <span style="color:blue">table</span>.
5. Within this for loop, each line of <span style="color:blue">table</span> is divided into separate sections wherever there is a '\n' (new line character). This new list is then saved as <span style="color:blue">x</span>.
6. The first element of <span style="color:blue">x</span> (element that does not include '\n') is then further divided wherever the <span style="color:blue">delineator</span> occurs, and saved as <span style="color:blue">z</span>.
7. The values that were originally separated by the <span style="color:blue">delineator</span> in <span style="color:blue">line</span> of <span style="color:blue">table</span> (<span style="color:blue">z</span>) are then appended to <span style="color:blue">list</span>.
8. Once this process has repeated for every <span style="color:blue">line</span> in <span style="color:blue">table</span>, the for loop is broken and the file <span style="color:blue">table</span> (file specified in <span style="color:blue">table_address</span>) is closed.

```
def table_to_html(table_address, delineator, filename_html):
    table = open(table_address, "r")
    list = []
    for line in table.readlines():
        x = re.split("\\n", line)
        y = str(x[0])
        z = re.split(delineator, y)
        list.append(z)
    table.close()
```


### __Section 3:__
In this section, a HTML file whose title is specified in the variable <span style="color:blue">filename_html</span> is created that contains HTML code to represent the source table (<span style="color:blue">table_address</span>) as a website. 

To accomplish this, the following steps are taken:
1. The function <span style="color:red">Airium</span> from the module <span style="color:red">airium</span> is renamed <span style="color:blue">a</span> for convenience. *Note: <span style="color:blue">a</span> will be used to easily transform python to HTML syntax.*
2. The <span style="color:blue">filename_html</span> is then opened in write (<span style="color:blue">w</span>) mode as <span style="color:blue">f</span>. *Note: write (<span style="color:blue">w</span>) mode will cause the HTML file specified in the variable <span style="color:blue">filename_html</span> to be overwritten every time the function <span style="color:red">table_to_html</span> is run with the same value for <span style="color:blue">filename_html</span>.*
3. The declaration <<span style="color:blue">!DOCTYPE html</span>> is added to <span style="color:blue">a</span>.
4.  Within the HTML <<span style="color:blue">head</span>> tag:
    - "<span style="color:blue">utf-8</span>" is defined as the character set.
    - The HTML contents are formatted to display based on the device width (i.e. phone, tablet, computer).
    - The title of the HTML is set to <span style="color:blue">filename_html</span>.
    - The table headers (<<span style="color:blue">th</span>>) and table data (<<span style="color:blue">td</span>>) are padded by 3 pixels.
    - The HTML function <span style="color:red">hover</span> is used so that every table row (<<span style="color:blue">tr</span>>) the user's mouse hovers over in the HTML website is highlighted light-gray (represented by the hex code: #D3D3D3).
    - A 1 pixel black border is added around the entire <<span style="color:blue">table</span>>, each table header (<<span style="color:blue">th</span>>), and table data (<<span style="color:blue">td</span>>).
    - The function <span style="color:red">border-collapse</span> is set to <span style="color:blue">collapse</span> so that there is no space between each cell of the table.
5. A HTML <<span style="color:blue">body</span>> tag is created with the tags <<span style="color:blue">table</span>> and <<span style="color:blue">tbody</span>> nested inside of it.
6. Within the HTML <<span style="color:blue">tbody</span>> tag:
    - A for loop is created to iterate through each element <span style="color:blue">i</span> in the array/nested-list, <span style="color:blue">list</span>, created in <span style="color:orange">Section 2</span>. *Note: each element <span style="color:blue">i</span> in the array/nested-list, <span style="color:blue">list</span>, represents one row in the original source table.*
    - Within this for loop, a table row is created using the HTML tag <<span style="color:blue">tr</span>>. Within the HTML <<span style="color:blue">tr</span>> tag:
      - A second for loop is created to iterate through each element <span style="color:blue">j</span> in <span style="color:blue">i</span>. *Note: each element <span style="color:blue">j</span> in <span style="color:blue">i</span> represents the values within one row in the original source table.*
      - An if/else statement is used so that the first row of <span style="color:blue">list</span> (<span style="color:blue">i</span> == 0) is nested within the HTML table header tag (<<span style="color:blue">th</span>>) and the background color for every element in that row is set to light grey (style="background-color:#D3D3D3;"). Every other row (<span style="color:blue">i</span> != 0) is nested within the HTML table data tag (<<span style="color:blue">td</span>>).
7. Once this process has repeated for all the values <span style="color:blue">j</span> in every line <span style="color:blue">i</span> of the array/nested-list <span style="color:blue">list</span>, the for loops are broken.
8. All of the HTML code that was added to <span style="color:blue">a</span> is then converted into a string titled <span style="color:blue">html</span>.
9. <span style="color:blue">html</span> is appended to the file <span style="color:blue">f</span> (<span style="color:blue">filename_html</span>) and the file <span style="color:blue">f</span> is closed. 

```
    a = airium.Airium()
    with open(filename_html, 'w') as f:
        a('<!DOCTYPE html>')
        with a.html(lang="pl"):
            with a.head():
                a.meta(charset="utf-8")
                a.meta(name="viewport", content="width=device-width, initial-scale=1.0")
                with a.title():
                    a(filename_html)
                with a.style():
                    a("th, td \n"
                    "\t\t{padding: 3px;}\n"
                    "\ttr:hover \n"
                    "\t\t{background-color: #D3D3D3;}\n"
                    "\ttable, th, td {\n"
                    "\t\tborder: 1px solid black;\n"
                    "\t\tborder-collapse: collapse;}")
            with a.body():
                with a.table():
                    with a.tbody():
                        for i in list:
                            index_i = list.index(i)
                            with a.tr():
                                for j in i:
                                    if index_i == 0:
                                        with a.th(style="background-color:#D3D3D3;"):
                                            a(j)
                                    else:
                                        with a.td():
                                            a(j)
        html = str(a)
        f.write(html)
    f.close()
```


## __Using the function__

### __Section 4:__
Now that the function <span style="color:red">table_to_html</span> has been defined, it can be used by specifying the value of the variables <span style="color:blue">table_address</span>, <span style="color:blue">delineator</span>, and <span style="color:blue">filename_html</span>. When defining the <span style="color:blue">table_address</span>, each folder should be delineated by either "/", "//", or "\\\\" for <span style="color:blue">table_address</span> to be a valid entry in python. 

Examples on how to use the function <span style="color:red">table_to_html</span> with a CSV and TSV source file are shown below: 

```
# TSV Source File
    table_address = "C:\\folder1\\folder2\\folder3\\folder4\\tsv_example.tsv"
    filename_html = "tsv_example.html"
    table_to_html(table_address, "\t", filename_html)

# CSV Source File
    table_address = "C:\\folder1\\folder2\\folder3\\folder4\\csv_example.csv"
    filename_html = "csv_example.html"
    table_to_html(table_address, ",", filename_html)
```


## __Appendix__

### __Compiled Copy of Raw Code:__
```
import re
import airium

def table_to_html(table_address, delineator, filename_html):
    table = open(table_address, "r")
    list = []
    for line in table.readlines():
        x = re.split("\\n", line)
        y = str(x[0])
        z = re.split(delineator, y)
        list.append(z)
    table.close()

    a = airium.Airium()
    with open(filename_html, 'w') as f:
        a('<!DOCTYPE html>')
        with a.html(lang="pl"):
            with a.head():
                a.meta(charset="utf-8")
                a.meta(name="viewport", content="width=device-width, initial-scale=1.0")
                with a.title():
                    a(filename_html)
                with a.style():
                    a("th, td \n"
                    "\t\t{padding: 3px;}\n"
                    "\ttr:hover \n"
                    "\t\t{background-color: #D3D3D3;}\n"
                    "\ttable, th, td {\n"
                    "\t\tborder: 1px solid black;\n"
                    "\t\tborder-collapse: collapse;}")
            with a.body():
                with a.table():
                    with a.tbody():
                        for i in list:
                            index_i = list.index(i)
                            with a.tr():
                                for j in i:
                                    if index_i == 0:
                                        with a.th(style="background-color:#D3D3D3;"):
                                            a(j)
                                    else:
                                        with a.td():
                                            a(j)
        html = str(a)
        f.write(html)
    f.close()


# To use the function:
    # TSV Source File
        table_address = "C:\\folder1\\folder2\\folder3\\folder4\\tsv_example.tsv"
        filename_html = "tsv_example.html"
        table_to_html(table_address, "\t", filename_html)

    # CSV Source File
        table_address = "C:\\folder1\\folder2\\folder3\\folder4\\csv_example.csv"
        filename_html = "csv_example.html"
        table_to_html(table_address, ",", filename_html)
```
