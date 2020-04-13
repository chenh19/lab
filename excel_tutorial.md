# Fast medium-scale data processing with Excel
**When dealing with medium sized datasets (dozens or hundreds of entries), it can be awkward. On the one hand, it might not be worthwhile to specially learn and write an R script for it; on the other hand, it would be very tiresome to do the processing manually. I will introduce herein some handy tools that are perfect for this situation and can expedite the data processing.**  
*Current version: v1.0.0*  

#### Table
- [*Data trimming*](https://github.com/chenh19/lab_training/blob/master/excel_tutorial.md#1-data-trimming)
- [*Data filtering*](https://github.com/chenh19/lab_training/blob/master/excel_tutorial.md#2-data-filtering)
- [*Cross-reference*](https://github.com/chenh19/lab_training/blob/master/excel_tutorial.md#3-cross-reference)
- [*Data exporting*](https://github.com/chenh19/lab_training/blob/master/excel_tutorial.md#4-data-exporting)


## 1. Data trimming
Always do data trimming first. In most cases, data doesn't come neat and uniform. Sometimes you need to combine datasets that have different formatting, sometimes there might be a lot of blank cells or duplicates in a sheet. If the data is not trimmed first, you will very likely lose data entries during analyzing and you won't be able to trace back.

### i. Replace
**Replacing blank cells with "N/A":**  

- Select the entire desired region manually (do not use Ctrl+A because you may miss some cells)  
- Ctrl+H to bring up the "Find and Replace" window  
![](fig/1-1.png)
> Find what: (leave blank)  
> Replace with: N/A  
- Click "Replace All"  
![](fig/1-2.png)

**Uniforming format:**  

- Select the entire column you want to adjust  
- Ctrl+H to bring up the "Find and Replace" window  
![](fig/1-3.png)
> Find what: Dx  
> Replace with: Disease  
- Click "Replace All"  
![](fig/1-4.png)

### ii. Text to columns
- Insert a few blank columns after the column you want to split  
![](fig/1-5.png)
- Select the column you want to split  
- Go to Data > Text to Columns  
![](fig/1-6.png)
- If you want to split by symbols (e.g., " ", "/", "-", "_"), select Delimited; if you want to split by character count, select Fixed Width  
![](fig/1-7.png)
- Next and Finish
![](fig/1-8.png)


### iii. Concatenate columns
- After the columns you want to combine, insert a blank column  
- Input something like this:  
> you can use any delimiter you want, e.g., " ", "/", "-", "_"  
> you may concatenate more than two columns, just use "," to separate the values  

![](fig/1-9.png)
- Autofill the column by dragging  
![](fig/1-10.png)

### iv. Remove duplicates (for manual removing, use highlight)
**Automatic:**  

- Make sure you finished the "1. Replace" step   
- Select the entire data region  
- Go to Data > Remove Duplicates  
- Select only the column you want with unique values  
![](fig/1-12.png)
- Next and Finish  
![](fig/1-13.png)

**Semiautomatic:**  

- Make sure you finished the "1. Replace" step   
- Select the entire data region  
- Go to Home > Sort & Filter > Custom Sort  
- Sort the column you want with unique values  
- Click "OK"  
- Select only the column you want with unique values  
- Go to Home > Conditional formatting > Highlight Cells Rules > Duplicate values (select any color you like)  
![](fig/1-14.png)
- Manually remove the duplicates (sometimes you may need to merge info from two rows)  
![](fig/1-15.png)
![](fig/1-16.png)

## 2. Data filtering
Filtering is the most common and basic procedure to get your interested data entries. In Excel, there is a "Filter" function in the menu, but I personally prefer not to use it. The major reason is that I would like to keep all the filtered out entries in a separate sheet, so that I can always trace back.

- Make sure you finished the "1. Replace" step  
- Select the entire data region  
- Go to Home > Sort & Filter > Custom sort  
- Sort by the column you want to filter by  
![](fig/1-17.png)
- Click "OK"  
- Select only the column you want to filter by  
- Go to Home > Conditional formatting > Highlight Cells Rules > Greater Than (select any color you like)  
![](fig/1-18.png)
- Cut (Ctrl+X) the highlighted rows, paste (Ctrl+V) into a new sheet, annotate why they were filtered out  
![](fig/1-20.png)
- You may need to delete the blank rows in the original sheet  
- If you need to filter by another columns, repeat the whole process in this section  
![](fig/1-19.png)

## 3. Cross-reference
This can be tricky and time consuming for most people, therefore I recommend the vlookup() function in Excel, which can automatically retrieve the related info if the keywords are matched. There is similar function called hlookup(), which works horizontally instead of vertically, but I personally have never used it.

### i. Merge data

- Make sure you finished the "1. Replace" step   
- Prepare the data to be merged  
![](fig/1-21.png)
- In the blank cell of your working sheet that you want to add value, click "fx", search for "vlookup"  
![](fig/1-22.png)
- Click the input box of Lookup_value: select the keyword in both your working sheet (it should also exist in your reference sheet)  
![](fig/1-23.png)
- Click the input box of Table_array: select the entire region of your reference dataset  
- Click the input box of Col_index_num: put 1, 2, 3, etc. The column of the keyword in your reference sheet will be 1, the column after will 2, etc. You can put the number according to the info you want to retrieve  
![](fig/1-24.png)
- Click the input box Range_lookoup: FALSE (I always put FALSE)  
- Click "OK"  
![](fig/1-25.png)
- If you want to retrieve multiple columns of values, you can just repeat the vlookup in the following cells of the same row  
- Select all the cells with vlookup function, autofill the columns by dragging  
![](fig/1-26.png)

### ii. Check missing entries

- Make sure you finished the "1. Replace" step   
- In the blank cell of your reference sheet, click "fx", search for "vlookup"  
- Click the input box of Lookup_value: select the keyword in your reference sheet (it should also exist in your working sheet)  
- Click the input box of Table_array: select only the keyword column your working sheet  
- Click the input box of Col_index_num: 1  
- Click the input box Range_lookoup: FALSE (I always put FALSE)  
![](fig/1-27.png)
- The "#N/A" are the missing entries in your working sheet  
![](fig/1-28.png)

## 4. Data exporting

**Manual check:**  

It's inevitable that you will have to do some manual check when all the above procedures are finished. There might be a few "#N/A" in your working sheet that were not due to the processing procedures, but due to other factors, such as an update from an online database.  

**Paste as value before moving or exporting:**  

To avoid the "#REF!" error, you may just copy everything and paste it as values (note the Paste Options) in a new sheet.  

