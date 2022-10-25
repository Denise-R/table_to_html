Denise Rauschendorfer

10/17/2022


# __CSV_Table_to_HTML__

In this repository a function, "<span style="color:red">csv_table_to_html</span>", is defined that transforms any CSV table into a html file. This function was originally created to help my brother, James Rauschendorfer, upload supplimental information to a website for his pHD; however, this function may also be a useful way to publically share raw data and upload it to a website.

The following code was executed using Python 3.10.7. 

## __Defining the function__

### __Section 1:__
In order to run the following code, the modules '<span style="color:red">re</span>' and '<span style="color:red">airium</span>' need to be imported.

```
import re
import airium
```


### __Section 2:__
To begin creating the function <span style="color:red">csv_table_to_html</span>, the CSV source file needs to be transcribed into a <span style="color:blue">list</span> where each value (separated by commas) in the CSV file is a different element in the <span style="color:blue">list</span>. 


*Note: All of <span style="color:orange">Sections 2-3</span> are contained within the 'def csv_table_to_html(csv_table_address):'*

To accomplish this, the following steps are taken:
1. <span style="color:red">def</span> is used to begin defining the function <span style="color:red">csv_table_to_html</span> with the variable <span style="color:blue">csv_table_address</span>.
2. The <span style="color:blue">csv_table_address</span> is then opened as <span style="color:blue">csv_table</span> in read (<span style="color:blue">r</span>) mode.
3. A list titled <span style="color:blue">list</span> is created.
4. A for loop is created to iterate through each line in the <span style="color:blue">csv_table</span>.
5. Within this for loop, each line of <span style="color:blue">csv_table</span> is divided into separate sections wherever there is a '\n' (new line character). This new list is then saved as <span style="color:blue">x</span>.
6. The first element of <span style="color:blue">x</span> (not including '\n') is then further divided wherever there is a ',' and saved as <span style="color:blue">z</span>. 
7. The values that were originally separated by commas in <span style="color:blue">line</span> of <span style="color:blue">csv_table</span> (<span style="color:blue">z</span>) are then appended to <span style="color:blue">list</span>.
8. Once this process has repeated for every <span style="color:blue">line</span> in <span style="color:blue">csv_table</span>, the for loop is broken and the file <span style="color:blue">csv_table</span> is closed.

```
def csv_table_to_html(csv_table_address):
    csv_table = open(csv_table_address, "r")
    list = []
    for line in csv_table.readlines():
        x = re.split("\\n", line)
        y = str(x[0])
        z = re.split(",", y)
        list.append(z)
    csv_table.close()
```


### __Section 3:__
In this section, a HTML file titled <span style="color:blue">table.html</span> is created that contains HTML code to represent the CSV table (<span style="color:blue">csv_table_address</span>) on a website. 

To accomplish this, the following steps are taken:
1. The function <span style="color:red">Airium</span> from the module <span style="color:red">airium</span> is remaned <span style="color:blue">a</span> for convience. *Note: the function <span style="color:red">a</span> will be used to easily transform python to HTML syntax.*
2. The file titled "<span style="color:blue">table.html</span>" is created and renamed <span style="color:blue">filename_html</span> within the function. 
3. The <span style="color:blue">filename_html</span> is then opened in write (<span style="color:blue">w</span>) mode as <span style="color:blue">f</span>. *Note: write (<span style="color:blue">w</span>) mode will cause <span style="color:blue">table.html</span> to be overwritten everytime the function <span style="color:red">csv_table_to_html</span> is run.*
4. The declaration <<span style="color:blue">!DOCTYPE html</span>> is added to <span style="color:blue">a</span>.
5.  Within the HTML <<span style="color:blue">head</span>> tag:
    - "<span style="color:blue">utf-8</span>" is defined as the character set.
    - The HTML contents are formatted to display based on the divice width.
    - The title of the HTML is set to "<span style="color:blue">HTML Table Display</span>".
    - The table headers (<<span style="color:blue">th</span>>) and table data (<<span style="color:blue">td</span>>) are padded by 3 pixles.
    - The HTML function <span style="color:red">hover</span> is used so that every table row (<<span style="color:blue">tr</span>>) the user's mouse hovers over in the website is highlighted light grey (represented by the hex code: #D3D3D3).
    - A 1 pixel black border is added around the entire <<span style="color:blue">table</span>>, each table header (<<span style="color:blue">th</span>>), and table data (<<span style="color:blue">td</span>>).
    - The function <span style="color:red">border-collapse</span> is set to <span style="color:blue">collapse</span> so that there is no space between each cell of the table.
6. A HTML'<bodyd>' tag is created with the tags <table> and <tbody> nested inside of it.
7. Within the HTML <<span style="color:blue">tbody</span>> tag:
    - A for loop is created to iterate through each element (<span style="color:blue">i</span>) in the array/nested-list, <span style="color:blue">list</span>, created in <span style="color:orange">Section 2</span>. *Note: each element (<span style="color:blue">i</span>) in the array/nested-list, <span style="color:blue">list</span> repersents one row in the original CSV table.*
    - Within this for loop, a table row is created using the HTML tag <<span style="color:blue">tr</span>>. Within the HTML <<span style="color:blue">tr</span>> tag:
      - A second for loop is created to iterate through each element (<span style="color:blue">j</span>) in <span style="color:blue">i</span>. *Note: each element (<span style="color:blue">j</span>) in <span style="color:blue">i</span> repersents the values within one row in the original CSV table.*
      - An if/else statement is used so that the first row of <span style="color:blue">list</span> (<span style="color:blue">i</span> == 0) is nested within the HTML table header tag (<<span style="color:blue">th</span>>) and every other row (<span style="color:blue">i</span> != 0) is nested within the HTML table data tag (<<span style="color:blue">td</span>>).
8. Once this process has repeated for all the values (<span style="color:blue">j</span>) in every line (<span style="color:blue">i</span>) of the array/nested-list <span style="color:blue">list</span>, the for loops are broken.
9. All of the HTML code that was added to <span style="color:blue">a</span> is then converted into a string titled <span style="color:blue">html</span>.
10. <span style="color:blue">html</span> is appended to the file <span style="color:blue">f</span> ("<span style="color:blue">table.html</span>") and the file <span style="color:blue">f</span> is closed.
11. 

```
    a = airium.Airium()
    filename_html = "table.html"
    with open(filename_html, 'w') as f:
        a('<!DOCTYPE html>')
        with a.html(lang="pl"):
            with a.head():
                a.meta(charset="utf-8")
                a.meta(name="viewport", content="width=device-width, initial-scale=1.0")
                with a.title():
                    a("HTML Table Display")
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
                                        with a.th():
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
Now that the function <span style="color:red">csv_table_to_html</span> has been defined, it can be used by specifying the <span style="color:blue">csv_table_address</span> of the CSV source code. When defining the <span style="color:blue">csv_table_address</span>, each folder should be delineated by either "/", "//", or "\\\\" for <span style="color:blue">csv_table_address</span> to be a valid entry in python. 

An example of how to use the function <span style="color:red">csv_table_to_html</span> is shown below. 

```
csv_table_address = "C:\\folder1\\folder2\\folder3\\folder4\\example.csv"
csv_table_to_html(csv_table_address)
```


## __Appendix__

### __Compiled Copy of Raw Code:__
```
import re
import airium

def csv_table_to_html(csv_table_address):
    csv_table = open(csv_table_address, "r")
    list = []
    for line in csv_table.readlines():
        x = re.split("\\n", line)
        y = str(x[0])
        z = re.split(",", y)
        list.append(z)
    csv_table.close()

    a = airium.Airium()
    filename_html = "demo.html"
    with open(filename_html, 'w') as f:
        a('<!DOCTYPE html>')
        with a.html(lang="pl"):
            with a.head():
                a.meta(charset="utf-8")
                a.meta(name="viewport", content="width=device-width, initial-scale=1.0")
                with a.title():
                    a("HTML Table Display")
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
                                        with a.th():
                                            a(j)
                                    else:
                                        with a.td():
                                            a(j)
        html = str(a)
        f.write(html)
    f.close()

# To use the function:
csv_table_address = "C:\\folder1\\folder2\\folder3\\folder4\\example.csv"
csv_table_to_html(csv_table_address)
```
