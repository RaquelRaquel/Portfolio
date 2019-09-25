
# Find and Delete Missing Data


The goal is to find and delete missing data from a given dataset.  This method is to help clean the dataset.
<br> 
<br> 
<br> 
The information for this exercise comes from the following datasets:
<br> 
__[Mobile App Store ( 7200 apps)](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps/downloads/app-store-apple-data-set-10k-apps.zip/7)__  containing data about approximately 7,000 iOS apps from the App Store that was collected in July 20171).
<br>
__[Google Play Store Apps](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps/downloads/app-store-apple-data-set-10k-apps.zip/7)__  containing data about approximately 10,000 Android apps from Google Play that was collected in August 2018.
<br>
<br>



The code below opens, reads, and list data for both files, Google Play and App Store.  


```python
# The ios apps file from Apple Store.
open_file_ios = open("AppleStore.csv")
from csv import reader
read_file_ios = reader(open_file_ios)
app_data_ios = list(read_file_ios)
ios_header = app_data_ios[0]
ios_data = app_data_ios[1:]



#The android apps file from Google Play store.
open_file_android = open("googleplaystore.csv")
from csv import reader
read_file_android = reader(open_file_android)
app_data_android = list(read_file_android)
android_header = app_data_android[0]
android_data = app_data_android[1:]
```

To explore the dataset, we create a function called `explore_data()`.  The first parameter, `dataset`, is the list we will run through the function.  The second and third parameters, `start`and `end`, are to indicate which row to start with and which row to end with (please note the `end` value is the number after the last row you want).  The last parameter, `rows_and_columns`, is assigned as `False`, to indicate the assumption that there are no rows and columns.  
<br>
Inside the `explore data()` function, there are three activities happening: 1) a new variable is assigned using the indicated parameters, 2) a for-loop statement, and 3) a conditional statement.  The variable, `dataset_slice`, is using the parameters: `dataset`, `start`, and `end`, to create the range of rows.  The for-loop uses `data_slice` to print each row determined by the `start` and `end` value, with a space in between each row. The conditional statement shows that if the parameter, `rows_and_columns`, is "True", then to find and print the number of rows and columns.
<br>


```python
def explore_data(dataset, start, end, rows_and_columns=False):
    dataset_slice = dataset[start:end]    
    for row in dataset_slice:
        print(row)
        print('\n') # adds a new (empty) line after each row

    if rows_and_columns:
        print('Number of rows:', len(dataset))
        print('Number of columns:', len(dataset[0]))
```

Below, the header and data records 1 through 4 are printed for the ios apps.  The `rows_and_columns` were assigned "True", in order to count the number of columns and rows.



```python
print(ios_header)
print('\n')

explore_data(ios_data, 0, 5, rows_and_columns=True)

```

    ['', 'id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']
    
    
    ['1', '281656475', 'PAC-MAN Premium', '100788224', 'USD', '3.99', '21292', '26', '4', '4.5', '6.3.5', '4+', 'Games', '38', '5', '10', '1']
    
    
    ['2', '281796108', 'Evernote - stay organized', '158578688', 'USD', '0', '161065', '26', '4', '3.5', '8.2.2', '4+', 'Productivity', '37', '5', '23', '1']
    
    
    ['3', '281940292', 'WeatherBug - Local Weather, Radar, Maps, Alerts', '100524032', 'USD', '0', '188583', '2822', '3.5', '4.5', '5.0.0', '4+', 'Weather', '37', '5', '3', '1']
    
    
    ['4', '282614216', 'eBay: Best App to Buy, Sell, Save! Online Shopping', '128512000', 'USD', '0', '262241', '649', '4', '4.5', '5.10.0', '12+', 'Shopping', '37', '5', '9', '1']
    
    
    ['5', '282935706', 'Bible', '92774400', 'USD', '0', '985920', '5320', '4.5', '5', '7.5.1', '4+', 'Reference', '37', '5', '45', '1']
    
    
    Number of rows: 7197
    Number of columns: 17


The ios data set appears to have 7,197 rows (not including the header) and 17 columns.  For a description of the column-header names, you can go to: __[Mobile App Store ( 7200 apps)](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps/downloads/app-store-apple-data-set-10k-apps.zip/7)__ .

<br>
<br>
Below, the header and data records 1 through 4 are printed for the Android apps.  The `rows_and_columns` were assigned "True", in order to count the number of columns and rows.



```python
print(android_header)
print('\n')
explore_data(android_data, 0, 5, rows_and_columns=True)
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    
    
    ['Coloring book moana', 'ART_AND_DESIGN', '3.9', '967', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    
    
    ['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']
    
    
    ['Pixel Draw - Number Art Coloring Book', 'ART_AND_DESIGN', '4.3', '967', '2.8M', '100,000+', 'Free', '0', 'Everyone', 'Art & Design;Creativity', 'June 20, 2018', '1.1', '4.4 and up']
    
    
    Number of rows: 10841
    Number of columns: 13


The Android app dataset appears to have 10,841 rows (not including the header) and 13 columns.  For a description of the column-header names, you can go to: __[Google Play Store Apps](https://www.kaggle.com/ramamet4/app-store-apple-data-set-10k-apps/downloads/app-store-apple-data-set-10k-apps.zip/7)__ .

### Missing Data Function

A function created to see if any of the rows are missing data.  This allows us to identify the row and delete it.  The function, `missing_data()`, uses two parameters: 1)the dataset header, and 2) the rows of data (not including the header).
<br>
* The function first identifies the length of the header and assigns it to `header_length`.  A print statement is created to indicate the number of values in the header. The function also prints what information is in the header in order to do a comparison. 
* The function completes a for-loop inside the `dataset_data` parameter.  In the for-loop, there is a variable, `row_length`, to find the length of each record.  A conditional statement is in the loop; if the `row_length` value is not equal to the `header_length` value, then there is a printed statement identifying which index-number record to look at and what information is in that record.
* Outside the for-loop is a final if-stament that says if `row_length` equals `header_length`, then print a statement saying that all other rows appear to be the same length.  This allows to print a statement incase there are datasets that have all data accounted for in each row. 


```python
def missing_data(dataset_header, dataset_data):
    header_length = len(dataset_header)
    print ("The length of the header is "+ str(header_length))
    print("The information in the header is: ")
    print(dataset_header)
    
    for row in dataset_data:
        row_length = len(row)
        if row_length != header_length:
            print('\n')
            print("Look at index number of the row: " + str(dataset_data.index(row))+ ". The length of the row is " + str(row_length) +".")
            print('\n')
            print("The information in the index number of row "+ str(dataset_data.index(row)) + " is: " )
            print(row)      
            print('\n')

        
    if row_length == header_length:
            print('\n')
            print('\n')
            print("All other rows appear to be the same length as header") 
            
```

<br>
<br>
Below, we check to see if there is missing data in the Android app dataset.  We use the `missing_data()` function that was just created.



```python
missing_data(android_header, android_data)

```

    The length of the header is 13
    The information in the header is: 
    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    Look at index number of the row: 10472. The length of the row is 12.
    
    
    The information in the index number of row 10472 is: 
    ['Life Made WI-Fi Touchscreen Photo Frame', '1.9', '19', '3.0M', '1,000+', 'Free', '0', 'Everyone', '', 'February 11, 2018', '1.0.19', '4.0 and up']
    
    
    
    
    
    
    All other rows appear to be the same length as header


<br>
In the Android dataset, it appears that row 10472 is missing data.  Please note that index value 10472 is pulled from the dataset that does not include the header.  It appears that the length of this row is 12 while the length of the header is 13.  
<br>


<br>
<br>
Below, we check to see if there is missing data in the ios app dataset.  We use the `missing_data()` function that was just created.


```python
missing_data(ios_header, ios_data)

```

    The length of the header is 17
    The information in the header is: 
    ['', 'id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']
    
    
    
    
    All other rows appear to be the same length as header



Looking at the results from above, we see the statement that all other rows appear to be the same length as the header.  This indicates that all data appears to be accounted for.
<br>
<br>

Before we delete the row with missing information, we will reconfirm the row and print out four rows of the Android dataset: `android_header` 10471, 10472, 10473.  This will help us to identify what information is missing and what rows are before and after the targeted row.


```python
print(android_header)
print('\n')
print(android_data[10471])
print('\n')
print(android_data[10472]) #This is the row that had an issue when first ran missing data function.
print('\n')
print(android_data[10473])
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    
    
    ['Xposed Wi-Fi-Pwd', 'PERSONALIZATION', '3.5', '1042', '404k', '100,000+', 'Free', '0', 'Everyone', 'Personalization', 'August 5, 2014', '3.0.0', '4.0.3 and up']
    
    
    ['Life Made WI-Fi Touchscreen Photo Frame', '1.9', '19', '3.0M', '1,000+', 'Free', '0', 'Everyone', '', 'February 11, 2018', '1.0.19', '4.0 and up']
    
    
    ['osmino Wi-Fi: free WiFi', 'TOOLS', '4.2', '134203', '4.1M', '10,000,000+', 'Free', '0', 'Everyone', 'Tools', 'August 7, 2018', '6.06.14', '4.4 and up']


When taking a closer look at the information in row 10472 and comparing it to the information in the header and the rows before and after, it appears that the data for "Category" is missing.
<br>
<br>

### Deleting Wrong Data

A `del` key is used to delete the specific row, `android_data[10472]`.  Also, the same row numbers are printed again to compare if the correct row was deleted.  Lastly, the number of rows is printed before and after the `del` key in order to see that the row numbers have change.


```python
print("The number of rows prior to deleting the data is: "+ str(len(android_data)))
del android_data[10472]
print(android_data[10471])
print(android_data[10472])
print(android_data[10473])
print("The number of rows after to deleting the data is: "+ str(len(android_data)))
```

    The number of rows prior to deleting the data is: 10841
    ['Xposed Wi-Fi-Pwd', 'PERSONALIZATION', '3.5', '1042', '404k', '100,000+', 'Free', '0', 'Everyone', 'Personalization', 'August 5, 2014', '3.0.0', '4.0.3 and up']
    ['osmino Wi-Fi: free WiFi', 'TOOLS', '4.2', '134203', '4.1M', '10,000,000+', 'Free', '0', 'Everyone', 'Tools', 'August 7, 2018', '6.06.14', '4.4 and up']
    ['Sat-Fi Voice', 'COMMUNICATION', '3.4', '37', '14M', '1,000+', 'Free', '0', 'Everyone', 'Communication', 'November 21, 2014', '2.2.1.5', '2.2 and up']
    The number of rows after to deleting the data is: 10840

