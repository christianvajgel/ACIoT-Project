# Project Charter: ACIoT

<br>

## Projeto de Bloco em IoT e Data Science

This is the project charter for the ACIoT project.
This application will be delivered as a web application.

- [Source Code](https://github.com/christianvajgel/ACIoT)
- [Christian Vajgel](https://www.linkedin.com/in/christianvajgel/)

<br>

## Mentor

Mentors include:

- [Fernando Guimarães](https://github.com/fernandoferreira-me)

<br>

## Project Purpose

Change the Air Conditioner (AC) temperatue based on IoT sensors (temperature and humidity) reads together with a prediction system.

<br>

## Benefits

Get a more confortable AC temperature based on the actual ambiance thermal conditions.

<br>

## User Roles

This application is used by one type of user.

1. Administrator

<br>

## Pre-requisites:

<br>
This project was tested running in a Conda enviroment with Python version 3.8.12.

<br>
Verify if the packages below are installed if not, run these commands:

<br>

- ```pip3 install awsiotsdk```

- ```pip3 install aws-iot```

- ```pip3 install awsiot```

- ```pip3 install awscrt```

- ```pip3 install AWSIoTPythonSDK```

- ```pip3 install pmdarima```

- ```pip3 install pythermalcomfort```

- ```pip3 install prophet``` <sup>[ 1 ]</sup>

    [ 1 ] - To install ```prophet``` refer to this [link](https://medium.com/data-folks-indonesia/installing-fbprophet-prophet-for-time-series-forecasting-in-jupyter-notebook-7de6db09f93e)

<br>

## Scope

### **Phase 1 - Conception and initiation (Module 1)**
<br>

Phase 1 involves a better comprehension of the data which will be used.

Preprocessing data occurs on this stage with filtering, conversion, rounding and exclusion.

On this stage the result will converted and used on the following stages of the project.

<br>
Deliverables:

- Project charter
- Creation of project structure
- Preprocessed data with required data only

<br>
This phase includes the development of:

- Initial project idea
- Inital project structure
- Code responsible to handle with the raw data

<br>

### **Phase 2 - Connection to AWS Cloud (Module 2)**

<br>

Phase 2 is defined by the stage where processed data is sent to the Cloud Service Provider (CSP), on this case Amazon Web Services (AWS).

```mqtt.ipynb``` is the MQTT notebook responsible to send data to a previously configured AWS Thing.

It is also defined the endpoint, client id and certificate exchange with the CSP.

At the end of this stage it is expected that data is correctly sent to AWS.

<br>

**Dataset attributes sent to AWS:**

*Note:*

* *Refer to ```Docs\DataReport\DataDictionary.md``` for complete a comprehension of the data types.*

<br>

| Column | Type (CSP) | Sample's Information | Format |
| --------- | ----------- |---------|---------|
| <span style="text-align: center; color: #000000; font-family: 'Courier New';">Timestamp</span> | ```JSON (string)``` | Date and time separated by 6 hours interval | Date with Hour |
| <span style="text-align: center; color: #0000FF; font-family: 'Courier New';">Temperature_Celsius</span> | ```JSON (string)``` | Temperature rounded | Celsius degree |
| <span style="text-align: center; color: #795E26; font-family: 'Courier New';">Relative_Humidity</span> | ```JSON (string)``` | Humidity rounded | 0-100 % |
| <span style="text-align: center; color: #008000; font-family: 'Courier New';">Date</span> | ```JSON (string)``` | The same of Timestamp for helping on manipulations | Date with Hour |
| <span style="text-align: center; color: #A31515; font-family: 'Courier New';">Season</span> | ```JSON (string)``` | Representation of date's season | 'winter' or 'spring' |
| <span style="text-align: center; color: #001080; font-family: 'Courier New';">Wind</span> | ```JSON (string)``` | Wind velocity in the room | 0.15 or 0.10 |
| <span style="text-align: center; color: #008000; font-family: 'Courier New';">ApparentTemperature</span> | ```JSON (string)``` | Room's apparent temperature sensation | Celsius degree |


<br>

**Configuration needed to send the payload to AWS:**

<br>

1. Create a thing on AWS (```us-east1```)
   
2. Set IoT Thing's policy in accordance with the file ```Docs/Project/iot-thing-policy.jsonc```
   
3. Connect your IoT Thing to AWS following this [tutorial]('https://us-east-1.console.aws.amazon.com/iot/home?region=us-east-1#/connectdevice/')

4. Confirm that you are receiving message on AWS dashboard and sending them from there
   
5. Extract the zip file generated on the previous step and store the files in a new folder named ```certificates``` under ```Code/DataPrep```

6. Navigate and open the notebook ```Code/Operationalization/mqtt.ipynb```
   
7. Replace the variables below with the desired ones generated on Step 3 and configured on AWS' dashboard:
    - ENDPOINT
    - CLIEND_ID
    - PATH_TO_CERTIFICATE
    - PATH_TO_PRIVATE_KEY
    - PATH_TO_AMAZON_ROOT_CA_1
    - TOPIC
  
8. Go to [MQTT test client]('https://us-east-1.console.aws.amazon.com/iot/home?region=us-east-1#/test') on AWS and subscribe to the TOPIC configured above
   
9.  Run the notebook to send the payload and check the result on the link provided on the Step 8

<br>

### **Phase 3 - Prediction with Prophet (Module 3)**

<br>

Phase 3 is defined by the stage where processed data is predicted for a near period. 

The prediction will take advantage of prediction library [Prophet](https://facebook.github.io/prophet/) from Meta (Facebook).

<br>

*Note:*

* *Refer to the section of ```Pre-requisites``` and ensure everything is already installed in your enviroment.*
* *With the same time period of the prediction it was added a ```red``` line on Prophet's prediction plot containing the real maximum daily temperature in Tokyo for better analysis purposes. It was extracted from [Weather.com](https://weather.com/weather/monthly/l/Minato+ku+Tokyo+Prefecture+Japan?canonicalCityId=88531c440be4859e58ca9bee96a8fef95643429857e3c626542368c9cb3c4815) and added on this project at ```Docs/Assets/real_temperatures_japan.csv```.*

<br>

1. Navigate and open the notebook ```Code/Model/prophet.ipynb```
   
2. Check if desired enviroment is selected and run the notebook to predict.

3. Prediction result is available at ```Docs/Assets/prophet_prediction.csv```

<br>

### **Phase 4 - Perform IoT Shadow on AWS (Module 4)**

<br>

Phase 4 is defined by the stage where the prediction data is sent to AWS to "turn-on" or "turn-off" the AC using AWS IoT Device Shadow service.

<br>

*Note:*

* *Refer to the section of ```Pre-requisites``` and ensure everything is already installed in your enviroment.*

<br>

1. Navigate and open the notebook ```Code/Operationalization/shadow.ipynb```

2. Replace the variables below with the desired ones generated on ```Phase 2 - Connection to AWS Cloud (Module 2) - Configuration needed to send the payload to AWS: Step 3``` and configured on AWS' dashboard:
    - ENDPOINT
    - CLIEND_ID
    - PATH_TO_CERTIFICATE
    - PATH_TO_PRIVATE_KEY
    - PATH_TO_AMAZON_ROOT_CA_1
   
3. Check if desired enviroment is selected and run the notebook to predict.

4. Check the topic ```$aws/things/aciot_test/shadow/update/accepted``` in MQTT section to view the action turning-on/off the AC on AWS.

<br>

## Out of scope

The following items are specifically not included in this scope of work:

- Make the AC correctly change the temperature (the system will send the message to change)


<br>

## Schedule

The following general schedule will be followed:

- TP1: October 25<sup>th</sup>, 2021
- TP3: November 22<sup>th</sup>, 2021
- TP5: December 13<sup>th</sup>, 2021
- TP7: March 28<sup>th</sup>, 2022
- TP9 (Project's deadline): April 11<sup>th</sup>, 2022
- KEYNOTE: April 11<sup>th</sup>, 2022
  