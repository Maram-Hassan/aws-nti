### create solution to send email on every object uploaded on s3 bucket 
![image](https://github.com/user-attachments/assets/bde949e0-0a6f-478c-b2c7-a42264c275bd)
# create sns
![Screenshot from 2024-10-30 21-09-02](https://github.com/user-attachments/assets/02df3f6f-d7bb-4cd5-b042-9c328c784cf2)
# create s3 bucket
![Screenshot from 2024-10-30 21-08-49](https://github.com/user-attachments/assets/3a727d8c-4f38-4a3d-8628-1836bc210ce9)
# create Event notifications 
![Screenshot from 2024-10-30 21-09-23](https://github.com/user-attachments/assets/f0e18d8e-c45d-4b5f-aa31-c70049df319f)
# edit bucket policy
![Screenshot from 2024-10-30 21-09-23](https://github.com/user-attachments/assets/909234bf-3477-407c-914f-4b76dcdb33b3)
# edit acess policy of sns
![Screenshot from 2024-10-30 21-13-22](https://github.com/user-attachments/assets/1203d4e8-6281-4f03-a818-5bc03cce4ae7)
# upload file on s3
![image](https://github.com/user-attachments/assets/81194473-ced7-4c5e-989d-8c930377d03e)
# email notification
![Screenshot from 2024-10-30 21-15-44](https://github.com/user-attachments/assets/ba2b697a-6061-4d9b-83c9-a933fdbd594b)


### create lambda function to make ec2
![Screenshot from 2024-10-31 15-54-51](https://github.com/user-attachments/assets/c40c0820-edc1-4780-a110-1e3c92763afa)

```
import json
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name='us-east-1')  # Specify your AWS region

    # Define instance details
    instance_params = {
        'ImageId': 'ami-0abcdef1234567890',  # Replace with a valid AMI ID
        'InstanceType': 't2.micro',          # Define instance type
        'MinCount': 1,
        'MaxCount': 1,
        'KeyName': 'your-key-pair',          # Replace with your key pair name
        'SecurityGroupIds': ['sg-0123456789abcdef0'],  # Replace with a valid security group
        'SubnetId': 'subnet-0123456789abcdef0'         # Replace with a valid subnet
    }

    # Launch EC2 instance
    try:
        response = ec2.run_instances(**instance_params)
        instance_id = response['Instances'][0]['InstanceId']
        
        return {
            'statusCode': 200,
            'body': json.dumps(f"EC2 instance created with ID: {instance_id}")
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps(f"Error creating EC2 instance: {str(e)}")
        }
```

# iam role to make lambda function has acess to ec2
![Screenshot from 2024-10-31 15-54-34](https://github.com/user-attachments/assets/5e8de308-c2e6-4aa3-bd47-1beaf42a544c)
![Screenshot from 2024-10-31 15-54-38](https://github.com/user-attachments/assets/7ea5cae7-e118-4709-90bc-619c1e4d0a62)

# ec2 done with lambda function
![Screenshot from 2024-10-30 21-16-28](https://github.com/user-attachments/assets/fe335fa0-1761-4d0f-b268-12e9335b0540)

### create cloud watch alarm to send any data to email 

### run system manager document to install any package on ec2
![Screenshot from 2024-10-31 17-28-53](https://github.com/user-attachments/assets/ac93df38-5214-4dc6-a197-9273c4c57a1d)
![Screenshot from 2024-10-31 17-29-00](https://github.com/user-attachments/assets/8190bd33-b593-42b5-bb30-0107b82b340b)
![Screenshot from 2024-10-31 17-29-05](https://github.com/user-attachments/assets/d55103aa-7744-49ae-a11f-1f4319d5a4ce)
![Screenshot from 2024-10-31 17-30-04](https://github.com/user-attachments/assets/cf7be57c-71dc-42f9-8980-45aaf9dd6902)
![Screenshot from 2024-10-31 17-32-01](https://github.com/user-attachments/assets/fd510ecc-5ba7-401c-9a87-acd4debfd38a)




