# Data Dictionary: ACIoT

## Projeto de Bloco em IoT e Data Science

This is the data dictionary for the ACIoT project.
This application will be delivered as a web application.

- [Source Code](https://github.com/christianvajgel/ACIoT)
- [Christian Vajgel](https://www.linkedin.com/in/christianvajgel/)

## Raw Data Sources:

| Dataset | Original Location | Destination Location | Data Movement Tools / Scripts |
| --------- | ----------- |---------|---------|
| Temperature and humidity of Japanese room | [Kaggle](https://www.kaggle.com/mnthasi/temperature-of-japanese-room) | ```Data/Raw/original_room_dataset.csv``` | ```Code/DataPrep/preprocessing.ipynb```

## Processed Data:

| Dataset | Original Location | Destination Location |  Data Movement Tools / Scripts |
| --------- | ----------- |---------|---------|
| room.csv | ```Data/Raw/original_room_dataset.csv``` | ```Docs/Assets/room.csv``` | ```Code/DataPrep/preprocessing.ipynb``` |

## Dataset:

| Column | Type | Sample's Information | Format |
| --------- | ----------- |---------|---------|
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Timestamp</span> | ```DateTime``` | Date and time separated by 6 hours interval | Date with Hour |
| <span style="text-align: center; color: #0000FF; font-family: 'Courier New';">Temperature_Celsius</span> | ```float``` | Temperature rounded | Celsius degree |
| <span style="text-align: center; color: #795E26; font-family: 'Courier New';">Relative_Humidity</span> | ```float``` | Humidity rounded | 0-100 % |
| <span style="text-align: center; color: #008000; font-family: 'Courier New';">Date</span> | ```DateTime``` | The same of Timestamp for helping on manipulations | Date with Hour |
| <span style="text-align: center; color: #A31515; font-family: 'Courier New';">Season</span> | ```string``` | Representation of date's season | 'winter' or 'spring' |
| <span style="text-align: center; color: #001080; font-family: 'Courier New';">Wind</span> | ```float``` | Wind velocity in the room | 0.15 or 0.10 |
| <span style="text-align: center; color: #008000; font-family: 'Courier New';">ApparentTemperature</span> | ```float``` | Room's apparent temperature sensation | Celsius degree |
