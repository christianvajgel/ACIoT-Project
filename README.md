# :snowflake: ACIoT

Grupo 03 - Christian Vajgel

<br>

    IoT system to predict and set a comfortable temperature for the Air Conditioner (AC).

<br>

## :world_map: The project:

<img src="https://storage.googleapis.com/cv_assets/ACIoT_Architecture_JPG.jpeg" />

<br>

## :deciduous_tree: Project tree:

```
ACIoT
├─ .gitignore
├─ Code
│  ├─ DataPrep
│  │  ├─ preprocessing.ipynb
│  │  └─ preprocessing.py
│  ├─ Model
│  └─ Operationalization
├─ Data
│  └─ Raw
│     └─ original_room_dataset.csv
├─ Docs
│  ├─ DataReport
│  │  ├─ DataDictionary.md
│  │  └─ DQRs.md
│  ├─ Model
│  │  └─ ModelReports.md
│  └─ Project
│     ├─ Charter.md
│     ├─ FinalProjectReport.md
│     └─ Notes.md
└─ README.md
```

<br>

## :gear: Execution guide:

<br>

*Note it is considered that user has already readed, executed, configured and installed each pre-requisite for all stages below listed on ```Docs\Project\Charter.md``` file on the local machine and AWS.*

<br>

### :hammer_and_wrench: **Stage 1: Pre-processing**

1. Navigate to ```Code\DataPrep\preprocessing.ipynb```


2. Execute all cells of the Jupyter notebook mentioned


3. The preprocessed dataset was created at ```Data\Processed\room.csv``` or for convenience it is located an example copy at ```Docs\Assets\room.csv```.

<br>

### :incoming_envelope: **Stage 2: Send data to AWS**

1. Navigate to ```Code\Operationalization\mqtt.ipynb```


2. Create a thing on AWS (```us-east1```)
   
3. Set IoT Thing's policy in accordance with the file ```Docs/Project/iot-thing-policy.jsonc```
   
4. Connect your IoT Thing to AWS following this [tutorial]('https://us-east-1.console.aws.amazon.com/iot/home?region=us-east-1#/connectdevice/')

5. Confirm that you are receiving message on AWS dashboard and sending them from there
   
6. Extract the zip file generated on the previous step and store the files in a new folder named ```certificates``` under ```Code/DataPrep```

7. Navigate and open the notebook ```Code/Operationalization/mqtt.ipynb```
   
8. Replace the variables below with the desired ones generated on Step 3 and configured on AWS' dashboard:
    - ENDPOINT
    - CLIEND_ID
    - PATH_TO_CERTIFICATE
    - PATH_TO_PRIVATE_KEY
    - PATH_TO_AMAZON_ROOT_CA_1
    - TOPIC
  
9.  Go to [MQTT test client]('https://us-east-1.console.aws.amazon.com/iot/home?region=us-east-1#/test') on AWS and subscribe to the TOPIC configured above
   
10.  Run the notebook to send the payload and check the result on the link provided on the Step 9

<br>

### :bar_chart: **Stage 3: Prophet prediction:**

1. Navigate and open the notebook ```Code\Model\prophet.ipynb```
   
2. Check if desired enviroment is selected and run the notebook to predict.

3. Prediction result is available at ```Data\Modeling\prophet_prediction.csv``` or for convenience it is located an example copy at ```Docs\Assets\prophet_prediction.csv```.

<br>

### :zap: **Stage 4: AWS Device Shadow update**

1. Navigate and open the notebook ```Code/Operationalization/shadow.ipynb```

2. Replace the variables below with the desired ones generated on ```Docs\Project\Charter.md - Phase 2 - Connection to AWS Cloud (Module 2) - Configuration needed to send the payload to AWS: Step 3``` and configured on AWS' dashboard:
    - ENDPOINT
    - CLIEND_ID
    - PATH_TO_CERTIFICATE
    - PATH_TO_PRIVATE_KEY
    - PATH_TO_AMAZON_ROOT_CA_1
   
3. Check if desired enviroment is selected and run the notebook to predict.

4. Check the topic ```$aws/things/aciot_test/shadow/update/accepted``` in MQTT section to view the action turning-on/off the AC on AWS.

<br>

## And it is done! :trophy:

<br>

_Last Update: 08ABR22_
