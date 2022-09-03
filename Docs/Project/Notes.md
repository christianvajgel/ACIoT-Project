# Notes:

- Links:

    https://www.kaggle.com/mnthasi/temperature-of-japanese-room

    https://tecnoblog.net/372161/como-se-calcula-a-sensacao-termica/

    https://www.researchgate.net/publication/335648292_IoT-Based_Smart_Air_Conditioning_Control_for_Thermal_Comfort

    https://stackoverflow.com/a/47970668


- Install Prophet - Anaconda venv

    https://medium.com/data-folks-indonesia/installing-fbprophet-prophet-for-time-series-forecasting-in-jupyter-notebook-7de6db09f93e


- Wind velocity - internal ambiance

    https://www.designingbuildings.co.uk/wiki/Indoor_air_velocity


- Pythermal comfort library AT

    https://pythermalcomfort.readthedocs.io/en/latest/reference/pythermalcomfort.html#apparent-temperature-at


- Digrams maker 

    https://github.com/mingrammer/diagrams


AWS IoT Policy JSON

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "greengrass:*",
                    "iot:*",
                    "iotanalytics:*",
                    "cloud9:*",
                    "lambda:*",
                    "s3:*",
                    "sns:*",
                    "iam:*",
                    "cognito-identity:*",
                    "cognito-sync:*",
                    "cognito-idp:*",
                    "logs:*",
                    "ec2:*",
                    "cloudwatch:*",
                    "kms:ListAliases",
                    "kms:DescribeKey",
                    "cloudformation:DescribeStackResources",
                    "tag:getResources"
                ],
                "Resource": "*"
            }
        ]
    }