# Step 1: Create a Table<a name="GettingStarted.Python.01"></a>

In this step, you create a table named `Movies`\. The primary key for the table is composed of the following attributes:
+ `year` – The partition key\. The `AttributeType` is `N` for number\.
+ `title` – The sort key\. The `AttributeType` is `S` for string\.

1. Copy the following program and paste it into a file named `MoviesCreateTable.py`\.

   ```
   #
   #  Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
   #
   #  This file is licensed under the Apache License, Version 2.0 (the "License").
   #  You may not use this file except in compliance with the License. A copy of
   #  the License is located at
   # 
   #  http://aws.amazon.com/apache2.0/
   # 
   #  This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
   #  CONDITIONS OF ANY KIND, either express or implied. See the License for the
   #  specific language governing permissions and limitations under the License.
   #
   from __future__ import print_function # Python 2/3 compatibility
   import boto3
   
   dynamodb = boto3.resource('dynamodb', region_name='us-west-2', endpoint_url="http://localhost:8000")
   
   
   table = dynamodb.create_table(
       TableName='Movies',
       KeySchema=[
           {
               'AttributeName': 'year',
               'KeyType': 'HASH'  #Partition key
           },
           {
               'AttributeName': 'title',
               'KeyType': 'RANGE'  #Sort key
           }
       ],
       AttributeDefinitions=[
           {
               'AttributeName': 'year',
               'AttributeType': 'N'
           },
           {
               'AttributeName': 'title',
               'AttributeType': 'S'
           },
   
       ],
       ProvisionedThroughput={
           'ReadCapacityUnits': 10,
           'WriteCapacityUnits': 10
       }
   )
   
   print("Table status:", table.table_status)
   ```
**Note**  
You set the endpoint to indicate that you are creating the table in the downloadable version of DynamoDB on your computer\.
In the `create_table` call, you specify the table name, primary key attributes, and its data types\.
The `ProvisionedThroughput` parameter is required\. However, the downloadable version of DynamoDB ignores it\. \(Provisioned throughput is beyond the scope of this exercise\.\)
These examples use the Python 3 style `print` function\. The line `from __future__ import print_function` enables Python 3 printing in Python 2\.6 and later\.

1. To run the program, enter the following command\.

   `python MoviesCreateTable.py`

To learn more about managing tables, see [Working with Tables in DynamoDB](WorkingWithTables.md)\.