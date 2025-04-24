Lab 5: Building a Serverless Architecture 
© 2024 Amazon Web Services, Inc. or its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited. All trademarks are the property of their owners. 
Note: Do not include any personal, identifying, or confidential information into the lab environment. Information entered may be visible to others. 
Corrections, feedback, or other questions? Contact us at AWS Training and Certification. 
Lab overview 
AWS solutions architects increasingly adopt event-driven architectures to decouple distributed applications. Often, these events must be propagated in a strictly ordered way to all subscribed applications. Using Amazon Simple Notification Service (Amazon SNS) topics and Amazon Simple Queue Service (Amazon SQS) queues, you can address use cases that require end-to-end message ordering, deduplication, filtering, and encryption. In this lab, you configure an Amazon Simple Storage Service (Amazon S3) bucket to invoke an Amazon SNS notification whenever an object is added to an S3 bucket. You learn how to create and interact with SQS queues, and learn how to invoke an AWS Lambda function using Amazon SQS. This scenario will help you understand how you can architect your application to respond to Amazon S3 bucket events using serverless services such as Amazon SNS, AWS Lambda, and Amazon SQS. 
Objectives 
By the end of this lab, you should be able to do the following: 
• Understand the value of decoupling resources. 
• Understand the potential value of replacing Amazon Elastic Compute Cloud (Amazon EC2) instances with Lambda functions. 
• Create an Amazon SNS topic. 
• Create Amazon SQS queues. 
• Create event notifications in Amazon S3. 
• Create AWS Lambda functions using preexisting code. 
Lab 5: Building a Serverless Architecture 
© 2024 Amazon Web Services, Inc. or its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited. All trademarks are the property of their owners. 
Note: Do not include any personal, identifying, or confidential information into the lab environment. Information entered may be visible to others. 
Corrections, feedback, or other questions? Contact us at AWS Training and Certification. 
Lab overview 
AWS solutions architects increasingly adopt event-driven architectures to decouple distributed applications. Often, these events must be propagated in a strictly ordered way to all subscribed applications. Using Amazon Simple Notification Service (Amazon SNS) topics and Amazon Simple Queue Service (Amazon SQS) queues, you can address use cases that require end-to-end message ordering, deduplication, filtering, and encryption. In this lab, you configure an Amazon Simple Storage Service (Amazon S3) bucket to invoke an Amazon SNS notification whenever an object is added to an S3 bucket. You learn how to create and interact with SQS queues, and learn how to invoke an AWS Lambda function using Amazon SQS. This scenario will help you understand how you can architect your application to respond to Amazon S3 bucket events using serverless services such as Amazon SNS, AWS Lambda, and Amazon SQS. 
Objectives 
By the end of this lab, you should be able to do the following: 
• Understand the value of decoupling resources. 
• Understand the potential value of replacing Amazon Elastic Compute Cloud (Amazon EC2) instances with Lambda functions. 
• Create an Amazon SNS topic. 
• Create Amazon SQS queues. 
• Create event notifications in Amazon S3. 
• Create AWS Lambda functions using preexisting code. 

Task 1: Create a standard Amazon SNS topic 
In this task, you create an Amazon SNS topic, and then subscribe to an Amazon SNS topic. 
3. At the top of the AWS Management Console, in the search box, search for and choose Simple Notification Service. 
4. Expand the navigation menu by choosing the menu icon ☰ in the upper-left corner. 
5. From the left navigation menu, choose Topics. 
6. Choose Create topic. 
The Create topic page is displayed. 
7. On the Create topic page, in the Details section, configure the following: 
• Type: Choose Standard. 
• Name: Enter a unique SNS topic name, such as resize-image-topic-, followed by four random numbers. 
8. Choose Create topic. 
The topic is created and the resize-image-topic-XXXX page is displayed. The topic&apos;s Name, Amazon Resource Name (ARN), (optional) Display name, and topic owner&apos;s AWS account ID are displayed in the Details section. 
9. Copy the topic ARN and Topic owner values to a notepad. You need these values later in the lab. 
 Example: 
ARN example: arn:aws:sns:us-east-2:123456789012:resize-image-topic Topic owner: 123456789123 (12 digit AWS Account ID) 
 Congratulations! You have created an Amazon SNS.

Task 2: Create two Amazon SQS queues 
In this task, you create two Amazon SQS queues each for a specific purpose and then subscribe the queues to the previously created Amazon SNS topic. 
Task 2.1: Create an Amazon SQS queue for the thumbnail image 
10. At the top of the AWS Management Console, in the search box, search for and choose Simple Queue Service. 
11. On the SQS home page, choose Create queue. 
The Create queue page is displayed. 
12. On the Create queue page, in the Details section, configure the following: 
• Type: Choose Standard (the Standard queue type is set by default). 
• Name: Enter thumbnail-queue. 
13. The console sets default values for the queue Configuration parameters. Leave the default values. 
14. Choose Create queue. 
Amazon SQS creates the queue and displays a page with details about the queue. 
15. On the queue&apos;s detail page, choose the SNS subscriptions tab. 
16. Choose Subscribe to Amazon SNS topic. 
A new Subscribe to Amazon SNS topic page opens. 
17. From the Specify an Amazon SNS topic available for this queue section, choose the resize-image-topic SNS topic you created previously under Use existing resource. 
 Note: If the SNS topic is not listed in the menu, choose Enter Amazon SNS topic ARN and then enter the topic&apos;s ARN that was copied earlier. 
18. Choose Save. 
Your SQS queue is now subscribed to the SNS topic named resize-image-topic-XXXX. 
Task 2.2: Create an Amazon SQS queue for the mobile image 
19. On the SQS console, expand the navigation menu on the left, and choose Queues. 
20. Choose Create queue.
The Create queue page is displayed. 
21. On the Create queue page, in the Details section, configure the following: 
• Type: Choose Standard (the Standard queue type is set by default). 
• Name: Enter mobile-queue. 
22. The console sets default values for the queue Configuration parameters. Leave the default values. 
23. Choose Create queue. 
Amazon SQS creates the queue and displays a page with details about the queue. 
24. On the queue&apos;s detail page, choose the SNS subscriptions tab. 
25. Choose Subscribe to Amazon SNS topic. 
A new Subscribe to Amazon SNS topic page opens. 
26. From the Specify an Amazon SNS topic available for this queue section, choose the resize-image-topic SNS topic you created previously under Use existing resource. 
 Note: If the SNS topic is not listed in the menu, choose Enter Amazon SNS topic ARN and then enter the topic&apos;s ARN that was copied earlier. 
27. Choose Save. 
Your SQS queue is now subscribed to the SNS topic named resize-image-topic-XXXX. 
Task 2.3: Verifying the AWS SNS subscriptions 
To verify the result of the subscriptions, publish to the topic and then view the message that the topic sends to the queue. 
28. At the top of the AWS Management Console, in the search box, search for and choose Simple Notification Service. 
29. In the left navigation pane, choose Topics. 
30. On the Topics page, choose resize-image-topic-XXXX. 
31. Choose Publish message. 
The console opens the Publish message to topic page. 
32. In the Message details section, configure the following: 
• Subject - optional:: Enter Hello world. 
33. In the Message body section, configure the following:
For Message structure, select Identical payload for all delivery protocols. 
• For Message body sent to the endpoint, enter Testing Hello world or any message of your choice. 
34. In the Message attributes section, configure the following: 
• For Type, choose String. 
• For Name, enter Message. 
• For Value, enter Hello World. 
35. Choose Publish message . 
The message is published to the topic, and the console opens the topic&apos;s detail page. To investigate the published message, navigate to Amazon SQS. 
36. At the top of the AWS Management Console, in the search box, search for and choose Simple Queue Service. 
37. Choose any queue from the list. 
38. Choose Send and receive messages . 
39. On Send and receive messages page, in the Receive messages section, choose Poll for messages . 
40. Locate the Message section. Choose any ID link in the list to review the Details, Body, and Attributes of the message. 
The Message Details box contains a JSON document that contains the subject and message that you published to the topic. 
41. Choose Done . 
 Congratulations! You have successfully created two Amazon SQS queues and published to a topic that sends notification messages to a queu


Task 3: Create an Amazon S3 event notification 
In this task, you create an Amazon S3 Event Notification and receive S3 event notifications using the event notification destination as Amazon SNS when certain event happen in the S3 bucket. 
Task 3.1: Configure the Amazon SNS access policy to allow the Amazon S3 bucket to publish to a topic 
42. At the top of the AWS Management Console, in the search box, search for and choose Simple Notification Service. 
43. From the left navigation menu, choose Topics. 
44. Choose the resize-image-topic-XXXX topic. 
45. Choose Edit . 
46. Navigate to the Access policy - optional section and expand it, if necessary 
47. Delete the existing content of the JSON editor panel. 
48. Copy the following code block and paste it into the JSON Editor section. 
{   &quot;Version&quot;: &quot;2008-10-17&quot;,   &quot;Id&quot;: &quot;__default_policy_ID&quot;,   &quot;Statement&quot;: [     {       &quot;Sid&quot;: &quot;__default_statement_ID&quot;,       &quot;Effect&quot;: &quot;Allow&quot;,       &quot;Principal&quot;: {         &quot;AWS&quot;: &quot;*&quot;       },       &quot;Action&quot;: [         &quot;SNS:GetTopicAttributes&quot;,         &quot;SNS:SetTopicAttributes&quot;,         &quot;SNS:AddPermission&quot;,         &quot;SNS:RemovePermission&quot;,         &quot;SNS:DeleteTopic&quot;,         &quot;SNS:Subscribe&quot;,         &quot;SNS:ListSubscriptionsByTopic&quot;,         &quot;SNS:Publish&quot;       ],       &quot;Resource&quot;: &quot;SNS_TOPIC_A
 &quot;Action&quot;: &quot;SNS:Publish&quot;,       &quot;Resource&quot;: &quot;SNS_TOPIC_ARN&quot;,       &quot;Condition&quot;: {         &quot;StringEquals&quot;: {           &quot;AWS:SourceAccount&quot;: &quot;SNS_TOPIC_OWNER&quot;         }       }     }   ] }  
49. Replace the two occurrences of SNS_TOPIC_OWNER with the Topic owner (12-digit AWS Account ID) value that you copied earlier in Task 1. Make sure to leave the double quotes. 
50. Replace the two occurrences of SNS_TOPIC_ARN with the SNS topic ARN value copied earlier in Task 1. Make sure to leave the double quotes. 
51. Choose Save changes . 
Task 3.2: Create a single S3 event notification on uploads to the ingest S3 bucket 
52. At the top of the AWS Management Console, in the search box, search for and choose S3. 
53. On the Buckets page, choose the bucket hyperlink with a name like xxxxx-labbucket-xxxxx. 
54. Choose the Properties tab. 
55. Scroll to the Event notifications section. 
56. Choose Create event notification . 
57. In the General configuration section, do the following: 
• Event name: Enter resize-image-event. 
• Prefix - optional: Enter ingest/. 
 Note: In this lab, you set up a prefix filter so that you receive notifications only when files are added to a specific folder (ingest). 
• Suffix - optional: Enter .jpg. 
 Note: In this lab, you set up a suffix filter so that you receive notifications only when .jpg files are uploaded. 
58. In the Event types section, select ☑ All object create events. 
59. In the Destination section, configure the following: 
ect create events. 
• SNS topic: Choose the resize-image-topic-XXXX SNS topic from the dropdown menu. 
Or, if you prefer to specify an ARN, choose Enter ARN and enter the ARN of the SNS topic copied earlier. 
60. Choose Save changes. 
 Congratulations! You have successfully created an Amazon S3 event notification. 

Task 4: Create and configure two AWS Lambda functions 
In this task, you create two AWS Lambda functions and deploy the respective functionality code to each Lambda function by uploading code and configure each Lambda function to add an SQS trigger. 
Task 4.1: Create a Lambda function to generate a thumbnail image 
In this task, you create an AWS Lambda function with an SQS trigger that reads an image from Amazon S3, resizes the image, and then stores the new image in an Amazon S3 bucket folder. 
61. At the top of the AWS Management Console, in the search box, search for and choose Lambda. 
62. Choose Create function. 
63. In the Create function window, select Author from scratch. 
64. In the Basic information section, configure the following: 
• Function name: Enter CreateThumbnail. 
• Runtime: Choose Python 3.9. 
• Expand the ▶ Change default execution role section. 
• Execution role: Select Use an existing role. 
• Existing role: Choose the role with the name like XXXXX-LabExecutionRole-XXXXX. 
This role provides your Lambda function with the permissions it needs to access Amazon S3 and Amazon SQS. 
⚠ Caution: Make sure to choose Python 3.9 under Other supported runtime. If you choose Python 3.10 or the Latest supported, the code in this lab fails as it is configured specifically for Python 3.9. 
65. Choose Create function. 
At the top of the page there is a message like, Successfully created the function CreateThumbnail. You can now change its code and configuration. To invoke your function with a test event, choose &quot;Test"

Task 4.2: Configure the CreateThumbnail Lambda function to add an SQS trigger and upload the Python deployment package 
AWS Lambda functions can be initiated automatically by activities such as data being received by Amazon Kinesis or data being updated in an Amazon DynamoDB database. For this lab, you initiate the Lambda function whenever a new object is pushed to your Amazon SQS queue. 
66. Choose + Add trigger, and then configure the following: 
• For Select a source, choose SQS. 
• For SQS Queue, choose thumbnail-queue. 
• For Batch size - optional, enter 1. 
67. Scroll to the bottom of the page, and then choose Add . 
At the top of the page there is a message like, The trigger thumbnail-queue was successfully added to function CreateThumbnail. The trigger is in a disabled state. 
The SQS trigger is added to your Function overview page. Now configure the Lambda function. 
68. Choose the Code tab. 
69. Configure the following settings (and ignore any settings that are not listed): 
70. Copy the CreateThumbnailZIPLocation value that is listed to the left of these instructions 
71. Choose Upload from ▼ , and choose Amazon S3 location. 
72. Paste the CreateThumbnailZIPLocation value you copied from the instructions in the Amazon S3 link URL field. 
73. Choose Save . 
The CreateThumbnail.zip file contains the following code: 
⚠ Caution: Do not copy this code—it is just an example to show what is in the zip file. 
+++Code 
import boto3 import os import sys import uuid from urllib.parse import unquote_plus from PIL import Image import PIL.Image import json  s3_client = boto3.client(&quot;s3&quot;) s3 = boto3.resou
   with Image.open(image_path) as image:         image.thumbnail((128, 128))         image.save(resized_path)   def handler(event, context):     for record in event[&quot;Records&quot;]:         payload = record[&quot;body&quot;]         sqs_message = json.loads(payload)         bucket_name = json.loads(sqs_message[&quot;Message&quot;])[&quot;Records&quot;][0][&quot;s3&quot;][&quot;bucket&quot;][             &quot;name&quot;         ]         print(bucket_name)         key = json.loads(sqs_message[&quot;Message&quot;])[&quot;Records&quot;][0][&quot;s3&quot;][&quot;object&quot;][&quot;key&quot;]         print(key)          download_path = &quot;/tmp/{}{}&quot;.format(uuid.uuid4(), key.split(&quot;/&quot;)[-1])         upload_path = &quot;/tmp/resized-{}&quot;.format(key.split(&quot;/&quot;)[-1])          s3_client.download_file(bucket_name, key, download_path)         resize_image(download_path, upload_path)         s3.meta.client.upload_file(             upload_path, bucket_name, &quot;thumbnail/Thumbnail-&quot; + key.split(&quot;/&quot;)[-1]         )   
+++ 
74. Examine the preceding code. It is performing the following steps: 
• Receives an event, which contains the name of the incoming object (Bucket, Key) 
• Downloads the image to local storage 
• Resizes the image using the Pillow library 
• Creates and uploads the resized image to a new folder 
75. In the Runtime settings section, choose Edit. 
• For Handler, enter CreateThumbnail.handler. 
76. Choose Save. 
At the top of the page there is a message like, Successfully updated the function CreateThumbnail. 
⚠ Caution: Make sure you set the Handler 
79. Choose Edit . 
• For Description, enter Create a thumbnail-sized image. 
Leave the other settings at the default settings. Here is a brief explanation of these settings: 
• Memory defines the resources that are allocated to your function. Increasing memory also increases CPU allocated to the function. 
• Timeout sets the maximum duration for function processing. 
80. Choose Save. 
A message is displayed at the top of the page with text like, Successfully updated the function CreateThumbnail. 
The CreateThumbnail Lambda function has now been configured. 
Task 4.3: Create a Lambda function to generate a mobile image 
In this task, you create an AWS Lambda function with an SQS trigger that reads an image from Amazon S3, resizes the image, and then stores the new image in an Amazon S3 bucket folder. 
81. At the top of the AWS Management Console, in the search box, search for and choose Lambda. 
82. Choose Create function. 
83. In the Create function window, select Author from scratch. 
84. In the Basic information section, configure the following: 
• Function name: Enter CreateMobileImage. 
• Runtime: Choose Python 3.9. 
• Expand the ▶ Change default execution role section. 
• Execution role: Select Use an existing role. 
• Existing role: Choose the role with the name like XXXXX-LabExecutionRole-XXXXX. 
This role provides your Lambda function with the permissions it needs to access Amazon S3 and Amazon SQS. 
⚠ Caution: Make sure to choose Python 3.9 under Other supported runtime. If you choose Python 3.10 or the Latest supported, the code in this lab fails as it is configured specifically for Python 3.9. 
85. Choose Create function. 
At the top of the page there is a message like, Successfully created the function CreateMobile. You can now change its code and configuration. To invoke your function with a test event, choose &quot;Test&quot;. 
Task 4.4: Configure the CreateMobileImage Lambda function to add an SQS trigger and upload the Python deployment package 
AWS Lambda functions can be initiated automatically by activities such as data being received by Amazon Kinesis or data being updated in an Amazon DynamoDB database. For this lab, you initiate the Lambda function whenever a new object is pushed to your Amazon SQS queue. 
86. Choose + Add trigger, and then configure the following: 
• For Select a source, choose SQS. 
• For SQS Queue, choose mobile-queue. 
• For Batch size - optional, enter 1. 
87. Scroll to the bottom of the page, and then choose Add . 
At the top of the page there is a message like, The trigger mobile-queue was successfully added to function CreateMobileImage. The trigger is in a disabled state. 
The SQS trigger is added to your Function overview page. Now configure the Lambda function. 
88. Choose the Code tab. 
89. Configure the following settings (and ignore any settings that are not listed): 
90. Copy the CreateMobileZIPLocation value that is listed to the left of these instructions 
91. Choose Upload from ▼ , and choose Amazon S3 location. 
92. Paste the CreateMobileImageZIPLocation value you copied from the instructions in the Amazon S3 link URL field. 
93. Choose Save . 
The CreateMobileImage.zip file contains the following code: 
⚠ Caution: Do not copy this code—it is just an example to show what is in the zip file. 
+++Code 
import boto3 import os import sys import uuid from urllib.parse import unq
from PIL import Image import PIL.Image import json  s3_client = boto3.client(&quot;s3&quot;) s3 = boto3.resource(&quot;s3&quot;)   def resize_image(image_path, resized_path):     with Image.open(image_path) as image:         image.thumbnail((640, 320))         image.save(resized_path)   def handler(event, context):     for record in event[&quot;Records&quot;]:         payload = record[&quot;body&quot;]         sqs_message = json.loads(payload)         bucket_name = json.loads(sqs_message[&quot;Message&quot;])[&quot;Records&quot;][0][&quot;s3&quot;][&quot;bucket&quot;][             &quot;name&quot;         ]         print(bucket_name)         key = json.loads(sqs_message[&quot;Message&quot;])[&quot;Records&quot;][0][&quot;s3&quot;][&quot;object&quot;][&quot;key&quot;]         print(key)          download_path = &quot;/tmp/{}{}&quot;.format(uuid.uuid4(), key.split(&quot;/&quot;)[-1])         upload_path = &quot;/tmp/resized-{}&quot;.format(key.split(&quot;/&quot;)[-1])          s3_client.download_file(bucket_name, key, download_path)         resize_image(download_path, upload_path)         s3.meta.client.upload_file(             upload_path, bucket_name, &quot;mobile/MobileImage-&quot; + key.split(&quot;/&quot;)[-1]         )   
+++ 
94. In the Runtime settings section, choose Edit. 
• For Handler, enter CreateMobileImage.handler. 
95. Choose Save. 
At the top of the page there is a message like, Successfully updated the function CreateMobileImage. 
⚠ Caution: Make sure you set the Handler field to the preceding value, otherwise the Lambda functi
Leave the other settings at the default settings. Here is a brief explanation of these settings: 
• Memory defines the resources that are allocated to your function. Increasing memory also increases CPU allocated to the function. 
• Timeout sets the maximum duration for function processing. 
99. Choose Save. 
A message is displayed at the top of the page with text like, Successfully updated the function CreateMobileImage. 
The CreateMobileImage Lambda function has now been configured. 
 Congratulations! You have successfully created 2 AWS Lambda functions for the serverless architecture and set the appropriate SQS queue as trigger for their respective functions. 





