# Find and Remove Missing Data, and Remove Duplicate Entries


The goal is to find missing data, remove the missing data and to remove any duplicate entries.

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

In order to explore the data set, this `explore_data()` function was created.  The first paramenter, `dataset`, is designated for the file to be used.  The second and third parameters, `start`and `end`, is to indicate which row to start with and which row to end with (please note the `end` value is the number after the last row you want).  The last parameter, `rows_and_columns`, is assigned as `False`, to indicate the assumption that there are no rows and columns.  
<br>
Inside the `explore data()` function, there are three activities happening: a new variable is assigned using the indicated parameters, a for-loop, and a conditional statement.  The variable, `dataset_slice`, is using the parameters: `dataset`, `start`, and `end`, to create the range of rows.  The for-loop uses `data_slice` to print each row determined by the `start` and `end` value, with a space in between each row. The conditional statement shows that if the parameter, `rows_and_columns`, is "True", then to find and print the number or rows and columns.
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

Below, the header and data rows 1 through 4 are printed for the ios apps.  The `rows_and_columns` were assigned "True" inorder to count the number of columns and rows.



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
Below, the header and data rows 1 through 4 are printed for the Android apps.  The `rows_and_columns` were assigned true inorder to count the number of columns and rows.



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

Below, is a function created to see if any of the rows are missing data.  This allows us to identify the row and delete it for data cleaning.  The function, `missing_data()`, uses to parameters: 1)the dataset header, and 2) the rows of data (not including the header).
<br>
* The function first identifies the length of the header and assigns it to `header_length`.  It then prints a statement that indicated the number of values in the header. The function also prints what information is in the header in order to do a comparison if needed. 
* The function then completes a for-loop inside the `dataset_data` parameter.  In the for-loop, there is a  variable assigned, `row_length`, to find the length of each variable.  A conditional statement is in the loop; if the `row_length` value is not equal to the `header_length` value, then there is a printed statement identifying which index-number row to look at and what information is in that row.
* Outside the for-loop is a final if-stament that says if `row_length` equals `header_length`, then print a statement sying that all other rows apear to be the same length.  This allows to print something incase there are datasets that have all data accounted for in each row. 



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
Below we check to see if there is any missing data in the Android app dataset.  We use the `missing_data()` function that was just created.
<br>
<br>


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
<br>
We see that row 10472 in the Android dataset has missing data.  Please note that index value 10472 is pulled from the dataset that does not include the header.  It appears that the length of this row is 12 while the length of the header is 13.  
<br>




<br>
<br>
Below we check to see if there is any missing data in the ios app dataset.  We use the `missing_data()` function that was just created.
<br>
<br>


```python
missing_data(ios_header, ios_data)

```

    The length of the header is 17
    The information in the header is: 
    ['', 'id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']
    
    
    
    
    All other rows appear to be the same length as header


<br>
<br>
Looking at the results from above, usings the  `missing_data ()` function, we see the statement that all other rows appear to be the same length as the header.  This indicates that all data appears to be accounted for.
<br>
<br>

In order to reconfirm the row with missing that we want to delete, we will print out four rows of the android dataset: `android_header` 10471, 10472, 10473.  This will help us to identify what information is missing and what rows are before and after the targeted row.


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

A `del` key is used to delete the specific row, `android_data[10472]`.  Also the same row numbers are printed again to compare if the correct row was deleted.  Lastly, the number of rows are printed before and after the `del` key in order to see that the row numbers have change.


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


# Removing Duplicate Entries
<br>

###  Part 1 (Finding Duplicate Rows)

When look at the data, we can see there  are duplicate entries for the same apps.  Below is an example of duplicate entries from the android dataset.


```python
print(android_header)
for app in app_data_android:
    name = app[0]
    if name == "Instagram":
        print(app)
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']
    ['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    ['Instagram', 'SOCIAL', '4.5', '66577446', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    ['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    ['Instagram', 'SOCIAL', '4.5', '66509917', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']


Above we see there are four entries for the Instagram apps.  The fourth item in each row, shows the number of reviews that have taken place.  Later on, we are going to keep the row with the highest review and then delete the rest.
<br>
<br>
<br>
Below, a for-loop is created to collect all duplicates.  The `duplicate_apps[]` and `unique_apps[]` are intitially created as empty lists.  A for-loop is created to append to the list of either the duplicate or unique app.  Each row of data goes through the for loop and the app-name is initially added to the `unique_app[]` list if its the first time.  In the for-loop, if a name is already identified as being in the `unique_apps[]` list, then any additional datum that has the same app-name is added to the `duplicate_apps[]` list.  Lastly, there is a print text on the number of duplicates and an example of the first 15 duplicate names.


```python
duplicate_apps_android = []
unique_apps_android = []

for app in app_data_android:
    name = app[0]
    if name in unique_apps_android:
        duplicate_apps_android.append(name)
    else:
        unique_apps_android.append(name)
    
print('Number of duplicate apps:', len(duplicate_apps_android))
print('\n')
print('Examples of duplicate apps:', duplicate_apps_android[:15])
```

    Number of duplicate apps: 1181
    
    
    Examples of duplicate apps: ['Quick PDF Scanner + OCR FREE', 'Box', 'Google My Business', 'ZOOM Cloud Meetings', 'join.me - Simple Meetings', 'Box', 'Zenefits', 'Google Ads', 'Google My Business', 'Slack', 'FreshBooks Classic', 'Insightly CRM', 'QuickBooks Accounting: Invoicing & Expenses', 'HipChat - Chat Built for Teams', 'Xero Accounting Software']


Based on the results from above, we can see that there are 1,181 duplicate names.  In the example, we can see that the app name, "Box", is shown atleast two times.  
<br>
<br>


### Part 2 (Using a Dictionary)
<br>
Below we created a dictionary to retain all apps with their highest number of reviews (and no duplicates).  To start, we created a empty dictionary called ` review_max `.  A for-loop is created to go through each record for the Android dataset.  Initially, all app-names will be deposited into the `review_max` because they did not exist there before. Afterwards, if the app-name is found in `review_max` dictionary and if the number of reviews for the app (in the dictionary) is less than the number of review being presented in the iteration, than the higher value of number of reviews is updated into the dictionary.  


```python
review_max = {}
for app_name in android_data:
    name = app_name[0]
    n_reviews = float(app_name[3])
    if name in review_max and review_max[name] < n_reviews:
        review_max[name] = n_reviews
    elif name is not review_max:
        review_max[name] = n_reviews
```
To confirm the number of unique apps records that we should have in our dataset, we print the number of apps expected versus the number of apps that actually exist in the dictionary.

```python
print('Expected length after deleting duplicates: ', len(android_data) - len(duplicate_apps_android))
print("Acual length: ", len(review_max))
```

    Expected length after deleting duplicates:  9659
    Acual length:  9659


Above, we see that the numbers match.  Our expectated number of records we have is 9,659 records and the actual number of records in our dictionary is 9,659.
<br>
<br>
Below, we seperate the records to only have the unique apps into a list labelled, `android_clean[]`.  To do this, we create a for-loop that will iterate through the `android_data` dataset. An if-statement is created so that Python can iterate the dataset to determine if the `n_reviews` value is the same as the value listed in the maximum review dictionary.  If so, and if the app `name` does not already exist in the `already_listed` list, then the app record is appended to the `android_clean` list and to the `already_added` list.  The `already_added` list serves as a way to block any duplicates from getting into the `android_clean` list.  


```python
android_clean = []
already_added = []

for app_name in android_data:
    name = app_name[0]
    n_reviews = float(app_name[3])
    if n_reviews == review_max[name] and name not in already_added:
        android_clean.append(app_name)
        already_added.append(name)
```

Below, we explore the `android_clean` list by using the `explore_data`function that was created before.


```python
explore_data(android_clean, 0, 5, rows_and_columns=True)
```

    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    
    
    ['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']
    
    
    ['Pixel Draw - Number Art Coloring Book', 'ART_AND_DESIGN', '4.3', '967', '2.8M', '100,000+', 'Free', '0', 'Everyone', 'Art & Design;Creativity', 'June 20, 2018', '1.1', '4.4 and up']
    
    
    ['Paper flowers instructions', 'ART_AND_DESIGN', '4.4', '167', '5.6M', '50,000+', 'Free', '0', 'Everyone', 'Art & Design', 'March 26, 2017', '1.0', '2.3 and up']
    
    
    Number of rows: 9659
    Number of columns: 13


We can see that the number of rows, 9,659, from the `explore_data` function matches are expectations of how many rows we should have.

