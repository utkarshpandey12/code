# code
Assumptions 
RDS mysql server is configured and running. 
All the server parameters like host name , username , password etc are passed during deploymnet command and are read as environment variables inside lambda function Names of these variables can be edited from the cloudformation template.


Steps to run the code 
1. Create a S3 bucket in the same region where you want to run the script. Name the bucket: NewsDemoApp

2. git clone https://github.com/utkarshpandey12/code.git 

3. cd code folder 

4. run command
aws cloudformation package
--template-file demo-app-cloudformation-template.sam.yaml
--s3-bucket NewsDemoApp
--output-template-file .demo-app-cloudformation-template.yaml

5  run command after replacing all the relevant details in the command like dbname , username and google news api key etc.Environment and service name as it is




aws cloudformation deploy
--template-file .demo-app-cloudformation-template.yaml
--capabilities CAPABILITY_NAMED_IAM
--stack-name demoapp-news-app
--parameter-overrides
Environment=dev ServiceName=demo-news-app HostName=host_name DataBaseName=db_name PortNumber=p_no UserName=username PassWord=pwd ApiKey=KEY NewsTableName=name

Example url for get request 
https://yourservicename.execute-api.ap-south-1.amazonaws.com/dev/resume?function=fetch-news-db&topic=coronavirus&from=2020-07-24


Example url for post request 
https://yourservicename.execute-api.ap-south-1.amazonaws.com/dev/resume?function=update-news-db

body parameters to be passed in post request
{ 'from':'2020-07-24' , 'topic': 'coronavirus' }


