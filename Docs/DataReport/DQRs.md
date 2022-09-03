# Data Quality Rules (DQR)

*Note:*

* *For further information about the data refer to ```Docs\DataReport\DataDictionary.md```*
* *Original dataset available at ```Data\Raw\original_room_dataset.csv```*
* *Processed dataset available at ```Docs\Assets\room.csv```*
* *Preprocessing code available at ```Code\DataPrep\preprocessing.ipynb```*

<br>

The dataset was treated with the standard procedure for any downloaded dataset with the libraries *Pandas* and *math*.

DateTime conversion was aplied to the column of ```Timestamp``` to separate data in a 15 minutes regular interval.

Operations for cleaning the dataset from invalid and/or empty row's values from columns and rounding values for columns were performed for a better understanding and data processing.

<br>

### **Used functions for pre-processing data:**

<br>

<div style="text-align:center;">

| File | Function(*parameter*) | Action |  Column | Library used |
| --------- | ----------- |---------|---------|---------|
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Code\DataPrep\preprocessing.ipynb</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">.</span><span style="text-align: center; color: #795E26; font-family: 'Courier New';">resample</span><span style="text-align: center; color: #000000; font-family: 'Courier New';">(</span>```'15min'```<span style="text-align: center; color: #000000; font-family: 'Courier New';">)</span> <br> <span style="text-align: center; color: #795E26; font-family: 'Courier New';">.mean</span><span style="text-align: center; color: #000000; font-family: 'Courier New';">()</span> | ```Perform a resample on the column and separates the periods in a 6 hour interval generating the mean between them``` | <span style="text-align: center; color: #000000; font-family: 'Courier New';">Timestamp</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">Pandas <br> math</span> |
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Code\DataPrep\preprocessing.ipynb</span> | <span style="text-align: center; color: #795E26; font-family: 'Courier New';">remove_empty_observations</span><span style="text-align: center; color: #000000; font-family: 'Courier New';">(x)</span> | ```Check if the value converted to float is NaN if positive remove the row from the dataset``` | <span style="text-align: center; color: #0000FF; font-family: 'Courier New';">Temperature_Celsius</span> <span style="text-align: center; color: #795E26; font-family: 'Courier New';">Relative_Humidity</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">math</span> |
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Code\DataPrep\preprocessing.ipynb</span> | <span style="text-align: center; color: #795E26; font-family: 'Courier New';">round_observations</span><span style="text-align: center; color: #000000; font-family: 'Courier New';">(x)</span> | ```Round the value of the elements on the column to the next closest integer number``` | <span style="text-align: center; color: #0000FF; font-family: 'Courier New';">Temperature_Celsius</span> <span style="text-align: center; color: #795E26; font-family: 'Courier New';">Relative_Humidity</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">math</span> |
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Code\DataPrep\preprocessing.ipynb</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">.</span><span style="text-align: center; color: #795E26; font-family: 'Courier New';">to_csv</span><span style="text-align: center; color: #000000; font-family: 'Courier New';">(</span>```'../../Data/Processed/room.csv'```<span style="text-align: center; color: #000000; font-family: 'Courier New';">)</span> | ```Convert the dataset to a CSV file and save it``` | <span style="text-align: center; color: #000000; font-family: 'Courier New';">Timestamp</span> <span style="text-align: center; color: #0000FF; font-family: 'Courier New';">Temperature_Celsius</span> <span style="text-align: center; color: #795E26; font-family: 'Courier New';">Relative_Humidity</span> | <span style="text-align: center; color: #000000; font-family: 'Courier New';">Pandas</span> |

</div>