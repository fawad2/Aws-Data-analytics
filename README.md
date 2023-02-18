# Aws-Data-Analytics

Goal: Analyze the Data in QuickSight BI Service provided by AWS

Note: My data is already located in S3 bucket(csv format) 


So let's Go!

I will follow this Diagram.
![image](https://user-images.githubusercontent.com/51129966/219843908-dc55706b-4029-48a2-acf2-5ba072e4b7a1.png)


Creating a clawer in AWS GLUE to

![image](https://user-images.githubusercontent.com/51129966/219844291-38cd6bd9-fde5-4e92-8d1e-911fe70a137d.png)

Adding a Data Source as you know my data is located in s3
We can select a single file to crawl but I'm crawling all the files in my bucket.
![image](https://user-images.githubusercontent.com/51129966/219844386-f0696fd3-13e8-477e-bc22-a32c0ef1bf00.png)

Create IAM role to access to Crawl s3 bcucket
![image](https://user-images.githubusercontent.com/51129966/219844529-f4b5bc60-0355-41cf-9a8d-e838b8b9dcca.png)

Crawler Schedule is set for on-Demand
![image](https://user-images.githubusercontent.com/51129966/219844610-6d527eef-2823-45be-aa72-62200da2f2af.png)

Now you need a database to store crawled data
if you haven't created yet you can create on from AWS GLUE -> Database
and target the data base in Crawler Properties 

![image](https://user-images.githubusercontent.com/51129966/219844674-402abee4-3fac-4ea2-99e0-86eb19c15638.png)
So my crawler is created and my table is created in database the output which i choose.
AWS -> Database -> you can see your crawled table here.

![image](https://user-images.githubusercontent.com/51129966/219844936-63d9b925-71be-4375-91dd-291c073b50e7.png)


Step 2: Move the Crawled Data to Redshift but first we need to create a table in redshift.

Creating a Cluster in Redshift

![image](https://user-images.githubusercontent.com/51129966/219844165-5a938b4f-152d-42cd-bd66-ee64c9894ba5.png)

Now open a Querry editor and Connect to a Dev Database

Creating a new Database 

Write in Querry Editor

CREATE database myfirstdatabase; 
after running the command
My Database is Created

I will change my connection to switch from dev data to myfirstdatabase

and creating a table in Querry Editor (change data-type according to your data)

Create TABLE myfirstdatabase
(
  show_id     bigint,
  type        VARCHAR,
  title        VARCHAR,
  director    VARCHAR,
  cast1        VARCHAR,
  country       VARCHAR,
  date_added        VARCHAR,
  release_year        bigint,
  rating   VARCHAR,
  duration VARCHAR,
  listed_in VARCHAR,
  description VARCHAR
  
);

My table is created
![image](https://user-images.githubusercontent.com/51129966/219845345-87510b51-4b23-412e-b0a7-9a04f4b31519.png)


Now repeat the process 
Create a crawler in AWS GLUE for redshift crawler and choose the output in Database once the data is crawled,

Create a Job which can transfer Craweled s3 data into redshift Table.
Once job complete preview Data in Redshift.

Make you redshift Public

So quicksight can use the Data

Open Quciksight and Create Dataset -> New Dataset -> Redshift
![image](https://user-images.githubusercontent.com/51129966/219845666-ded3c8c2-3593-42fe-916d-506df9ab1085.png)

Redshift DataSource
![image](https://user-images.githubusercontent.com/51129966/219845768-17c2919f-ffee-4621-b4aa-b79e0353fc71.png)

Now data is loaded in to quicksight
Now you can Visualize Data,



Thanks for Reading


