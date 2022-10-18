Denise Rauschendorfer

10/17/2022


# __CSV_Table_to_HTML__

In this repository a function, "<span style="color:red">csv_table_to_html</span>", is defined that transforms any CSV table into a html file.

The following code was executed using Python 3.10.7. 

## __Defining the function__

### __Section 1:__
In order to run the following code, the modules '<span style="color:red">re</span>' and '<span style="color:red">airium</span>' need to be imported.

```
import re
import airium
```


### __Section 2:__
To begin creating the function <span style="color:red">csv_table_to_html</span>...


*Note: All of <span style="color:orange">Sections 2-3</span> are contained within the 'def csv_table_to_html(csv_table_address):'*

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

To accomplish this, the following steps are taken:

```
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
```


## __Using the function__

### __Section 8:__
Now that the function <span style="color:red">creating_folder_paths</span> has been defined, it can be used by specifying the <span style="color:blue">source_file_name</span> of the source code. When defining the <span style="color:blue">source_file_name</span>, each folder should be delineated by either "/", "//", or "\\\\" for <span style="color:blue">source_file_name</span> to be a valid entry in python. 

An example of how to use the function <span style="color:red">creating_folder_paths</span> is shown below. 

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
