Project 6: Build an AWS multi-tier architecture](project6.md)

Lab overview 
Amazon Web Services (AWS) solutions architects must frequently design and build secure, high-performing, resilient, efficient architectures for applications and workloads to deliver content. Amazon CloudFront is a web service that provides a cost-effective way to distribute content with low latency and high data transfer speeds. You can use CloudFront to accelerate static website content delivery, serve video on demand or live streaming video, and even run serverless code at the edge location. In this lab, you configure a CloudFront distribution in front of an Amazon Simple Storage Service (Amazon S3) bucket and secure it using origin access control (OAC) provided by CloudFront. 
Objectives 
After completing this lab, you should be able to do the following: 
• Create an S3 bucket with default security settings. 
• Configure an S3 bucket for public access. 
• Add an S3 bucket as a new origin to an existing CloudFront distribution. 
• Secure an S3 bucket to permit access only through the CloudFront distribution. 
• Configure OAC to lock down security to an S3 bucket. 
• Configure Amazon S3 resource policies for public or OAC access.

Lab Environment 
The lab environment provides you with some resources to get started. There is an Auto Scaling group of EC2 instances being used as publicly accessible web servers. The web server infrastructure is deployed in an Amazon Virtual Private Cloud (Amazon VPC) and configured for multiple Availability Zones. It also uses load balancers. The lab also provides a CloudFront distribution with this load balancer as an origin. 
The following diagram shows the general expected architecture you should have at the end of this lab. During this lab, you create a new S3 bucket for the existing lab environment. You then configure this bucket as a new, secure origin to the existing CloudFront distribution. 
 
Services used in this lab 
Amazon CloudFront 
CloudFront is a content delivery web service. It integrates with other AWS products so that developers and businesses can distribute content to end users with low latency, high data transfer speeds, and no minimum usage commitments. 
You can use CloudFront to deliver your entire website, including dynamic, static, streaming, and interactive content, using a global network of edge locations. CloudFront automatically routes requests for your content to the nearest edge location to deliver content with the best possible performance. CloudFront is optimized to work with other AWS services, like Amazon S3, Amazon Elastic Compute Cloud (Amazon EC2), Elastic Load Balancing (ELB), and Amazon Route 53. CloudFront also works seamlessly with any origin server that doesn&apos;t use AWS, which stores the original, definitive versions of your files.

Amazon Simple Storage Service (Amazon S3) 
Amazon S3 provides developers and information technology teams with secure, durable, highly scalable object storage. Amazon S3 has a simple web services interface to store and retrieve any amount of data from anywhere on the web. 
You can use Amazon S3 alone or together with other AWS services such as Amazon EC2, Amazon Elastic Block Store (Amazon EBS), and Amazon Simple Storage Service Glacier (Amazon S3 Glacier), along with third-party storage repositories and gateways. Amazon S3 provides cost-effective object storage for a wide variety of use cases, including cloud applications, content distribution, backup and archiving, disaster recovery, and big data analytics. 
AWS services not used in this lab 
AWS services not used in this lab are turned off in the lab environment. In addition, the capabilities of the services used in this lab are limited to only what the lab requires. Expect errors when accessing other services or performing actions beyond those provided in this lab guide. 
Task 1: Explore the existing CloudFront distribution 
In this task, you examine the existing CloudFront distribution that was built for web server content. Before making changes to an environment, it is a good practice to understand the existing configuration. If you want to use CloudFront distributions for your personal AWS environments, you need to build and configure the distribution itself first. In later tasks, you add an S3 bucket as a new origin to this CloudFront distribution. 
Task 1.1: Open the CloudFront console 
3. If you have not already opened the console, follow the instructions in the Start Lab section to log in to the console. 
4. At the top of the console, in the search bar, search for and choose CloudFront. 
Task 1.2: Open the existing CloudFront distribution 
5. Choose the ID link for the only available distribution. 
 Note: If you do not find the list of distributions, ensure that you are at the correct page. Choose Distributions from the CloudFront navigation menu located on the left side of the console. 
A page showing the details of the distribution is displayed. 
Task 1.3: Explore the properties of the existing distribution 
In this task, you explore each tab of the distribution to review the existing configuration. In this lab, you are not configuring this CloudFront distribution in great detail. However, it is useful to know where all of the configurations you might need for managing a CloudFront distribution are located. 
6. Examine the contents of the General tab. 
This tab contains the details about the current configuration of this particular CloudFront distribution. It contains the most generally needed information about a distribution. It is also where you configure the common high-level items for the distribution, such as activating the distribution, logging, and certificate settings. 
 
7.  Copy edit: From the Details section, in the General tab, copy the ARN value and save it in a text editor. You need this value for a later task. 
8.  Copy edit: From the Details section, in the General tab, copy the Distribution domain name value. 
The Distribution domain name is also found to the left of these lab instructions under the listing LabCloudFrontDistributionDNS. 
9. Paste the Distribution domain value you copied into a new browser tab. 
A simple web page is loaded displaying the information of the web server from which CloudFront retrieved the content. By requesting content from the Distribution domain value for the CloudFront distribution, you are verifying that the existing cache is working. 
You can close this tab. 
10. Return to the CloudFront console. 
11. Choose the Security tab. 
This tab contains the distribution’s configuration if you need to keep your application secure from the most common web threats using AWS WAF or need to prevent users in specific countries from accessing your content using geographic restrictions. These features are not configured for use in this lab. 
12. Choose the Origins tab. 
This tab contains the details about the current origins that exist for this particular CloudFront distribution. It is also the area of the console you can use to configure new or existing CloudFront origins. A CloudFront Origin defines the location of the definitive, original version of the content that is delivered through the CloudFront distribution. 
 Note: The only origin currently on the distribution is an ELB load balancer. This load balancer is accepting and directing web traffic for the auto scaling web servers in its target group. 
13.  Copy edit: Copy the load balancer&apos;s Domain Name System (DNS) value for this origin from the column labeled Origin dom
16. Choose the Behaviors tab. 
Behaviors define the actions that the CloudFront distribution takes when there is a request for content, such as which origin to serve which content, Time To Live of content in the cache, cookies, and how to handle various headers. 
This tab contains a list of current behaviors defined for the distribution. You configure new or existing behaviors here. Behaviors for the distribution are evaluated in the explicit order in which you define them on this tab. 
Do the following to review or edit the configuration of any single behavior: 
• Select the radio button  in the row next to the behavior you want to modify. 
• Choose Edit. 
• Choose Cancel to close the page and return to the console. 
There is only one behavior currently configured in this lab environment. The behavior accepts HTTP and HTTPS for both GET and HEAD requests to the load balancer origin. 
17. Choose the Error Pages tab. 
This tab details which error page is to be returned to the user when the content requested results in an HTTP 4xx or 5xx status code. You can configure custom error pages for specific error codes here. 
18. Choose the Invalidations tab. 
This tab contains the distribution&apos;s configuration for object invalidation. Invalidated objects are removed from CloudFront edge caches. A faster and less expensive method is to use versioned objects or directory names. There are no invalidations configured for CloudFront distributions by default. 
19. Choose the Tags tab. 
This tab contains the configuration for any tags applied to the distribution. You can view and edit existing tags and create new tags here. Tags help you identify and organize your distributions. 
 Congratulations! You have explored the existing CloudFront distribution.

16. Choose the Behaviors tab. 
Behaviors define the actions that the CloudFront distribution takes when there is a request for content, such as which origin to serve which content, Time To Live of content in the cache, cookies, and how to handle various headers. 
This tab contains a list of current behaviors defined for the distribution. You configure new or existing behaviors here. Behaviors for the distribution are evaluated in the explicit order in which you define them on this tab. 
Do the following to review or edit the configuration of any single behavior: 
• Select the radio button  in the row next to the behavior you want to modify. 
• Choose Edit. 
• Choose Cancel to close the page and return to the console. 
There is only one behavior currently configured in this lab environment. The behavior accepts HTTP and HTTPS for both GET and HEAD requests to the load balancer origin. 
17. Choose the Error Pages tab. 
This tab details which error page is to be returned to the user when the content requested results in an HTTP 4xx or 5xx status code. You can configure custom error pages for specific error codes here. 
18. Choose the Invalidations tab. 
This tab contains the distribution&apos;s configuration for object invalidation. Invalidated objects are removed from CloudFront edge caches. A faster and less expensive method is to use versioned objects or directory names. There are no invalidations configured for CloudFront distributions by default. 
19. Choose the Tags tab. 
This tab contains the configuration for any tags applied to the distribution. You can view and edit existing tags and create new tags here. Tags help you identify and organize your distributions. 
 Congratulations! You have explored the existing CloudFront distribution.

Task 3: Configure the S3 LabBucket for public access 
In this task, you review the default access setting for S3 buckets. Next, you modify the permissions settings to allow public access to the bucket. 
Task 3.1: Configure the LabBucket to allow public policies to be created 
25. Select the link for the newly created LabBucket found in the Buckets section. 
A page with all of the bucket details is displayed. 
26. Choose the Permissions tab. 
27. Locate the Block public access (bucket settings) section. 
28. Choose Edit. 
The Edit Block public access (bucket settings) page is displayed. 
29. Unselect  Block all public access. 
30. Choose Save Changes. 
A message window titled Edit Block public access (bucket settings) is displayed. 
31. In the message field, enter confirm. 
32. Choose Confirm. 
You have removed the block on all public access policies for the LabBucket. You are now able to create access policies for the bucket that allow for public access. The bucket is currently not public, but anyone with the appropriate permissions can grant public access to objects stored within the bucket. 
Task 3.2: Configure a public read policy for the LabBucket 
You now create a public object read policy for this bucket. 
33. On the Permissions tab, locate the Bucket policy section. 
34. Choose Edit. 
The Edit bucket policy page is displayed. 
 
35.  Copy edit: Copy and paste the Bucket ARN value into a text editor to save the information for later. It is a string value like arn:aws:s3:::LabBucket located above the Policy box. 
The ARN value uniquely identifies this S3 bucket. You need this specific ARN value when creating bucket based policies. 
36.  File contents: Copy and paste the following JSON into a text editor. 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Id&quot;: &quot;Policy1621958846486&quot;,     &quot;Statement&quot;: [         {             &quot;Sid&quot;: &quot;OriginalPublicReadPolicy&quot;,             &quot;Effect&quot;: &quot;Allow&quot;,             &quot;Principal&quot;: &quot;*&quot;,             &quot;Action&quot;: [                 &quot;s3:GetObject&quot;,                 &quot;s3:GetObjectVersion&quot;             ],             &quot;Resource&quot;: &quot;RESOURCE_ARN&quot;         }     ] }  
37. Replace the RESOURCE_ARN value in the JSON with the Bucket ARN value you copied in a previous step and append a /* to the end of the pasted Bucket ARN value. 
ⓘ  By appending the /* wildcard to the end of the ARN, the policy definition applies to all objects located in the bucket. 
Here is the example of the updated policy JSON: 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Id&quot;: &quot;Policy1621958846486&quot;,     &quot;Statement&quot;: [         {             &quot;Sid&quot;: &quot;OriginalPublicReadPolicy&quot;,             &quot;Effect&quot;: &quot;Allow&quot;,             &quot;Principal&quot;: &quot;*&quot;,             &quot;Action&quot;: [                 &quot;s3:GetObject&quot;,                 &quot;s3:GetObjectVersion&quot;             ],             &quot;Resource&quot;: &quot;arn:aws:s3:::lab-bucket-1234/*&quot;         }     ] }  
38. Return to the Amazon S3 console. 
39. Paste the completed JSON into the policy box. Save changes.
ⓘ By using the * wildcard as the Principal value, all identities requesting the actions defined in the policy document are allowed to do so. By appending the /* wildcard to the allowed Resources, this policy applies to all objects located in the bucket. 
Note: The policies currently applied to the bucket make the objects in this bucket publicly readable. 
In later lab steps, you configure the bucket to be accessible only from the CloudFront distribution. 
 Congratulations! You have configured an S3 bucket for public read access. 

Task 4: Upload an object into the bucket and testing public access 
In this task, you upload a single object to the LabBucket. You use this object to test access in the remaining lab tasks. 
Task 4.1: Create a new folder in the bucket 
41. Choose the Objects tab. 
42. Choose Create folder. 
43. Enter CachedObjects into the Folder name field. 
44. Leave all other settings on the page at the default values. 
45. Choose Create folder. 
Task 4.2: Upload an object to the bucket 
46. Download the object for these lab instructions by choosing 
logo.png
 and saving it to your local device. 
47. Return to the Amazon S3 Console. 
48. Choose the link for the CachedObjects/ folder that you created previously. 
49. Choose Upload. 
The Upload page is displayed. 
50. Choose Add files. 
51. Choose the logo.png object from your local storage location. 
52. Choose Upload. 
The Upload: status page is displayed. 
A  Upload succeeded message is displayed on top of the screen. 
Task 4.3: Test public access to an object 
53. Choose the logo.png link from the Files and folders section. 
A page with details about the Amazon S3 object is displayed. 
54. Select the link located in the Object URL field. 
Task 4: Upload an object into the bucket and testing public access 
In this task, you upload a single object to the LabBucket. You use this object to test access in the remaining lab tasks. 
Task 4.1: Create a new folder in the bucket 
41. Choose the Objects tab. 
42. Choose Create folder. 
43. Enter CachedObjects into the Folder name field. 
44. Leave all other settings on the page at the default values. 
45. Choose Create folder. 
Task 4.2: Upload an object to the bucket 
46. Download the object for these lab instructions by choosing 
logo.png
 and saving it to your local device. 
47. Return to the Amazon S3 Console. 
48. Choose the link for the CachedObjects/ folder that you created previously. 
49. Choose Upload. 
The Upload page is displayed. 
50. Choose Add files. 
51. Choose the logo.png object from your local storage location. 
52. Choose Upload. 
The Upload: status page is displayed. 
A  Upload succeeded message is displayed on top of the screen. 
Task 4.3: Test public access to an object 
53. Choose the logo.png link from the Files and folders section. 
A page with details about the Amazon S3 object is displayed. 
54. Select the link located in the Object URL field. 


Task 4: Upload an object into the bucket and testing public access 
In this task, you upload a single object to the LabBucket. You use this object to test access in the remaining lab tasks. 
Task 4.1: Create a new folder in the bucket 
41. Choose the Objects tab. 
42. Choose Create folder. 
43. Enter CachedObjects into the Folder name field. 
44. Leave all other settings on the page at the default values. 
45. Choose Create folder. 
Task 4.2: Upload an object to the bucket 
46. Download the object for these lab instructions by choosing 
logo.png
 and saving it to your local device. 
47. Return to the Amazon S3 Console. 
48. Choose the link for the CachedObjects/ folder that you created previously. 
49. Choose Upload. 
The Upload page is displayed. 
50. Choose Add files. 
51. Choose the logo.png object from your local storage location. 
52. Choose Upload. 
The Upload: status page is displayed. 
A  Upload succeeded message is displayed on top of the screen. 
Task 4.3: Test public access to an object 
53. Choose the logo.png link from the Files and folders section. 
A page with details about the Amazon S3 object is displayed. 
54. Select the link located in the Object URL field. 

Task 5: Secure the bucket with Amazon CloudFront and Origin Access Control 
In a previous task, you have confirmed public access to the LabBucket works, but are not utilizing the CloudFront distribution for object access. In this task, you add the lab bucket as an new origin to the CloudFront distribution and make the objects in the LabBucket accessible only from the CloudFront distribution. 
Task 5.1: Update the bucket policy for the LabBucket 
Update the bucket policy to allow read-only access from the CloudFront distribution. 
57. At the top of the console, in the search bar, search for and choose S3. 
58. Select the link for the LabBucket found in the Buckets section. 
A page with all of the bucket details is displayed. 
59. Choose the Permissions tab. 
60. Locate the Bucket policy section. 
61. Choose Edit. 
The Edit bucket policy page is displayed. 
62.  Copy edit: Copy and paste the Bucket ARN value into a text editor to save the information for later. It is a string value like arn:aws:s3:::LabBucket located above the Policy box. 
The ARN value uniquely identifies this S3 bucket. You need this specific ARN value when creating bucket based policies. 
63.  File contents: Copy and paste the following JSON into a text editor. 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Statement&quot;: {         &quot;Sid&quot;: &quot;AllowCloudFrontServicePrincipalReadOnly&quot;,         &quot;Effect&quot;: &quot;Allow&quot;,         &quot;Principal&quot;: {             &quot;Service&quot;: &quot;cloudfront.amazonaws.com&quot;         },         &quot;Action&quot;: [             &quot;s3:GetObject&quot;,             &quot;s3:GetObjectVersion&quot;         ],         &quot;Resource&quot;: &quot;RESOURCE_ARN&qu}
64. Replace the RESOURCE_ARN value in the JSON with the Bucket ARN value you copied in a previous step and append a /* to the end of the pasted Bucket ARN value. 
65. Replace the CLOUDFRONT_DISTRIBUTION_ARN value in the JSON with the ARN value you copied in a previous step. 
Here is the example of the updated policy JSON: 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Id&quot;: &quot;Policy1621958846486&quot;,     &quot;Statement&quot;: [         {             &quot;Sid&quot;: &quot;OriginalPublicReadPolicy&quot;,             &quot;Effect&quot;: &quot;Allow&quot;,             &quot;Principal&quot;: &quot;*&quot;,             &quot;Action&quot;: [                 &quot;s3:GetObject&quot;,                 &quot;s3:GetObjectVersion&quot;             ],             &quot;Resource&quot;: &quot;arn:aws:s3:::lab-bucket-1234/*&quot;         &quot;Condition&quot;: {             &quot;StringEquals&quot;: {                 &quot;AWS:SourceArn&quot;: &quot;arn:aws:cloudfront::123456789:distribution/E3LU8VQUNZACBE&quot;             }         }     } }  
66. Return to the Amazon S3 console. 
67. Paste the completed JSON into the Policy box. 
68. Choose Save changes. 
Task 5.2: Enable the public access blockers 
69. On the Permissions tab, locate the Block public access (bucket settings) section. 
70. Choose Edit. 
The Edit Block public access (bucket settings) page is displayed. 
71. Select ☑ Block all public access.
A  Successfully edited Block Public Access settings for this bucket. message is displayed on top of the screen. 
A page with all the bucket details is displayed. 
 Congratulations! You have edited the S3 bucket policy so that the only principal allowed to read objects CloudFront distribution. 
Task 5.3: Create a new origin with Origin Access Control (OAC) 
In this task, you add the LabBucket as a new origin to the existing CloudFront distribution. 
75. At the top of the console, in the search bar, search for and choose CloudFront. 
76. From the CloudFront Distributions page, choose the ID link for the only available distribution. 
A page showing the details of the distribution is displayed. 
77. Choose the Origins tab. 
78. Choose Create origin. 
The Create Origin page is displayed. 
79. From the Origin domain field, choose the name of your LabBucket from the Amazon S3 section. 
 Note: Recall that the S3 bucket in this lab is never configured as a website. You have only changed the bucket policy regarding who is allowed to perform GetObject API requests against the S3 bucket into an Allow Public read policy. 
80. Leave the entry for Origin path empty. 
 Note: The Origin Path field is optional and configures which directory in the origin CloudFront should forward requests to. In this lab, rather than configuring the origin path, you leave it blank and instead configure a behavior to return only objects matching a specific pattern in the requests. 
81. For Name, enter My Amazon S3 Origin 
82. For Origin access, select  Origin access control settings (recommended). 
83. Choose Create new OAC. 
The console displays the Create new OAC message window. 
84. Leave the default settings and choose Create. 
85. Choose Create origin. 
A Successfully created origin My Amazon S3 Origin message is displayed on top of the screen. 
You can safely ignore any message like, The S3 bucket policy needs to be updated as you completed updating the bucket policy already. 
Task 5.4: Create a new behavior for the Amazon S3 origin 
In this task, you create a new behavior for the Amazon S3 origin so that the distribution has instructions for how to handle incoming requests for the origin. 
86. Choose the Behaviors tab. 
87. Choose Create behavior. 
The Create behavior page is displayed. 
88. In the Path pattern field, enter CachedObjects/*.png 
This field configures which matching patterns of object requests the origin can return. Specifically, in this behavior only .png objects stored in the CachedObjects folder of the Amazon S3 origin can be returned. Unless there is a behavior configured for them, all other requests to the Amazon S3 origin would result in an error being returned to the requester. Typically, users would not be requesting objects directly from the CloudFront distribution URL in this manner; instead, your frontend application would generate the correct object URL to return to the user. 
89. From the Origin and origin groups dropdown menu, choose My Amazon S3 Origin. 
90. From the Cache key and origin requests section, ensure  Cache policy and origin request policy (recommended) is selected. 
91. From the Cache policy dropdown menu, ensure CachingOptimized is selected. 
92. Leave all other settings on the page at the default values. 
93. Choose Create behavior. 
A  Successfully created new cache behavior CachedObjects/*.png. message is displayed on top of the screen. 
 Congratulations! You have created: a new origin for the Amazon S3 bucket, an Origin Access Control, and distribution behavior on a CloudFront distribution for the objects stored in the Amazon S3 bucket for the lab. 

Task 6: Test direct access to a file in the bucket using the Amazon S3 URL 
In this task, you test if the object can still be directly accessed using the Amazon S3 URL. 
94. At the top of the console, in the search bar, search for and choose S3. 
95. Select the link for the LabBucket found in the Buckets section. 
A page with all of the bucket details is displayed. 
96. Choose the Objects tab. 
97. Choose the link for the CachedObjects/ folder. 
98. Choose the link for the logo.png object. 
99. Select the link located in the Object URL field. 
An error message is displayed with Access denied messages. This is expected because the new bucket policy does not allow access to the object directly from Amazon S3 URLs. By denying access to S3 objects directly through Amazon S3, users can no longer bypass the controls provided by CloudFront cache, which can include logging, behaviors, signed URLs, or signed cookies. 
 Congratulations! You have confirmed the object is no longer directly accessible from the Amazon S3 URL. 

Task 7: Test access to the object in the bucket using the CloudFront distribution 
In this task, you confirm that you can access objects in the Amazon S3 origin for the CloudFront distribution. 
100.  Copy edit: Copy the CloudFront distribution&apos;s domain DNS value from the left side of these lab instructions under the listing LabCloudFrontDistributionDNS. 
101. Paste the DNS value into a new browser tab. 
A simple web page is loaded displaying the information of the web server where CloudFront retrieved the content from. 
102. Append /CachedObjects/logo.png to the end of the CloudFront distribution&apos;s domain DNS and press Enter. 
The browser makes a request to the CloudFront distribution and the object is returned from the Amazon S3 origin. 
 Hint: If the CloudFront URL redirects you to the Amazon S3 URL, or if the object isn&apos;t immediately available, the CloudFront distribution might still be updating from your recent changes. Return to the CloudFront console. Select Distributions from the navigation menu. Confirm that the Status column is  Enabled and the Last modified column has a timestamp. You need to wait for this before testing the new origin and behavior. After you have confirmed the status of the distribution, wait a few minutes and try this task again. 
 Congratulations! You have confirmed that the object is returned from a CloudFr

Optional Task 8: Replicate an S3 bucket across AWS Regions 
This optional task is provided to you if you have extra lab time or want to learn something a little more advanced. This task is not necessary to complete. You can end the lab now if you choose by following the steps to end the lab; otherwise, keep reading. 
Cross-Region replication is a feature of Amazon S3 that allows for automatic copying of your data from one bucket to another bucket located in a different AWS Region. It is a useful feature for disaster recovery. After the cross-Region replication feature is enabled for a bucket, every new object that you currently have read permissions for, which is created in the source bucket, is replicated into the destination bucket you define. This means that objects replicated to the destination bucket have the same names. Objects encrypted using an Amazon S3 managed encryption key are encrypted in the same manner as their source bucket. 
To perform Cross-Region replication, you must enable object versioning for both the source and destination buckets. To maintain good data orderliness with versioning enabled, you can deploy lifecycle policies to automatically archive objects to Amazon S3 Glacier or to delete the objects. 
Optional Task 8.1: Enable versioning on your source bucket 
103. Return to the browser tab open to the AWS Management Console. 
104. At the top of the console, in the search bar, search for and choose S3. 
105. Select the link for the LabBucket found in the Buckets section. 
A page with all the bucket details is displayed. 
106. Select the Properties tab. 
107. Locate the Bucket Versioning section. 
108. Choose Edit. 
The Edit Bucket Versioning page is displayed. 
109. Select  Enable for Bucket Versioning. 
110. Choose Save changes. 
Optional Task 8.2: Create a destination bucket for cross-Region replication 
111. From the Amazon S3 navigation menu, choose Buckets. 
112. At the top of the screen, choose the drop-down next to the region you are in and choose the SecondaryRegion value displayed to the left of these instructions. 

This navigates you to the SecondaryRegion to create the bucket. 
113. Choose Create bucket. 
The Create bucket page is displayed. 
114. In the Bucket name field, enter a unique bucket name. 
115. In the Block Public Access settings for this bucket section, unselect ☑ Block all public access. 
116. In the warning message, select ☑ I acknowledge that the current settings might result in this bucket and the objects within becoming public. 
! Caution: You do not need to have public access enabled for your personal buckets to use the cross-Region replication feature. It is enabled in this lab so that you can quickly test if objects are replicated and retrievable using the Amazon S3 URL. 
117. For Bucket Versioning, select  Enable. 
118. Choose Create bucket. 
The Amazon S3 console is displayed. 
The newly created bucket is displayed among the list of all the buckets for the account. 
  Note: To simplify the narrative in this lab, this newly created bucket is referred to as the DestinationBucket in the remainder of instructions. 
Optional Task 8.3: Configure a public read policy for the new destination bucket 
You now create a public object read policy for this bucket. You use the public read policy in this lab to demonstrate during the lab time that objects are replicated and retrievable using the Amazon S3 URL. It is not recommended for most use cases to use bucket policies which allow for public access. 
119. From the Amazon S3 navigation menu, choose Buckets. 
120. Choose the link for the DestinationBucket from the list of buckets. 
121. Choose the Permissions tab. 
122. Locate the Bucket policy section. 
123. Choose Edit. 
The Edit bucket policy page is displayed. 
124.  Copy edit: Copy and paste the Bucket ARN value into a text editor to save the information for later. It is a string value like arn:aws:s3:::LabBucket located above the Policy box. 
The ARN value uniquely identifies this S3 bucket. You need this specific ARN value when creating bucket-based policies. 
125.  File contents: Copy and paste the following JSON into a text editor: 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Id&quot;: &quot;Policy1621958846486&quot;,     &quot;Statement&quot;: [         {             &quot;Sid&quot;: &quot;OriginalPublicReadPolicy&quot;,             &quot;Effect&quot;: &quot;Allow&quot;,             &quot;Principal&quot;: &quot;*&quot;,             &quot;Action&quot;: [                 &quot;s3:GetObject&quot;,                 &quot;s3:GetObjectVersion&quot;             ],             &quot;Resource&quot;: &quot;RESOURCE_ARN&quot;         }     ] }  
126. Replace the RESOURCE_ARN value in the JSON with the Bucket ARN value you copied in a previous step and append a /* to the end of the pasted Bucket ARN value. 
Here is the example of the updated policy JSON: 
{     &quot;Version&quot;: &quot;2012-10-17&quot;,     &quot;Id&quot;: &quot;Policy1621958846486&quot;,     &quot;Statement&quot;: [         {             &quot;Sid&quot;: &quot;OriginalPublicReadPolicy&quot;,             &quot;Effect&quot;: &quot;Allow&quot;,             &quot;Principal&quot;: &quot;*&quot;,             &quot;Action&quot;: [  
Optional Task 8.4: Create a replication rule 
130. From the Amazon S3 navigation menu, choose Buckets. 
131. In the Buckets section, choose the link for the LabBucket. 
132. Choose the Management tab. 
133. Locate the Replication rules section. 
134. Choose Create replication rule. 
The Create replication rule page is displayed. 
135. In the Replication rule name field, enter MyCrossRegionReplication 
136. Verify that LabBucket is set for Source bucket name. If it is not, then you chose the incorrect bucket before choosing the replication rules. 
137. In the Choose a rule scope section, select  Apply to all objects in the bucket. 
138. Locate the Destination section. 
139. Choose  Browse S3. 
140. Select the  DestinationBucket. 
141. Select Choose path. 
142. Locate the IAM Role section. 
143. Select  Create new role. 
144. Leave all other options as their default selection. 
145. Choose Save. 
146. If the Replicate existing objects window is displayed, select   No, do not replicate existing objects then choose Submit. 
The Replication rules page for the LabBucket is displayed. 
A  Replication configuration successfully updated If changes to the configuration aren&apos;t displayed, choose the refresh button. Changes apply only to new objects. To replicate existing objects with this configuration, choose Create replication job. message is displayed on top of the screen. 
All newly created objects in the LabBucket are replicated into the DestinationBucket. 
 Note: It is possible to replicate existing objects between buckets, but that is beyond the scope of this lab. You can find more information about this topic in the document linked in the Appendix sect
Optional Task 8.5: Verify object replication 
147. From the Amazon S3 navigation menu, choose Buckets. You might need to expand the menu by choosing the ☰ menu icon. 
148. In the Buckets section, choose the link for the LabBucket. 
149. Download the object for these lab instructions by right-clicking 
logo2.png
 and saving it to your local device. 
150. Return to the Amazon S3 console. 
151. Choose the link for the CachedObjects/ folder. 
 Note: If you do not find the CachedObjects folder, choose Buckets from the navigation menu located on the left side of the console. Then choose the link for the LabBucket from the list. Finally, choose the Objects tab to ensure that you are at the correct page. 
152. Choose Upload. 
The Upload page is displayed. 
153. Choose Add files. 
154. Choose the logo2.png object from your local storage location. 
155. Choose Upload. 
The Upload: status page is displayed. 
A  Upload succeeded message is displayed on top of the screen. 
156. Choose the link for the logo2.png from the Files and folders section. 
A page with details about the Amazon S3 object is displayed. 
157. In the Object management overview section, examine Replication status and refresh the page periodically until it changes from PENDING to COMPLETED. 
158. From the Amazon S3 navigation menu, select Buckets. 
159. In the Buckets section, choose the link for the DestinationBucket. 
A page with all the bucket details is displayed. 
160. Choose the link for the CachedObjects/ folder. 
161. In the Files and folders section, choose the link for the logo2.png. 
A page with details about the Amazon S3 object is displayed. 
162. In the Object management overview section, examine Replication Status. It displays REPLICA. 
163. Choose the link located in the Object URL field. 
The picture is displayed in a browser tab. 
 Congratulations! You have completed setting up cross-Region replication for all new objects uploaded into the LabBucket. 
Consider these follow-up questions to this optional task: 
• How can you restrict access to objects in the DestinationBucket? 
• What steps are needed to add the DestinationBucket to the CloudFront distribution? 

Conclusion 
 Congratulations! You now have successfully done the following: 
• Created an S3 bucket with default security settings. 
• Configured an S3 bucket for public access. 
• Added an S3 bucket as a new origin to an existing CloudFront distribution. 
• Secured an S3 bucket to allow access only through the CloudFront distribution. 
• Configured OAC to lock down security to an S3 bucket. 
• Configured Amazon S3 resource policies for public or OAC access. 
 
End lab 
Follow these steps to close the console and end your lab. 
164. Return to the AWS Management Console. 
165. At the upper-right corner of the page, choose AWSLabsUser, and then choose Sign out. 
166. Choose End Lab and then confirm that you want to end your lab. 
Additional resources 
• For more information about S3 bucket naming rules, see 
Bucket naming rules
. 
• For more information about serving private content through CloudFront, see 
Serving private content with signed URLs and signed cookies
. 
• For more information about replicating existing objects between buckets, see 
Replicating existing objects between S3 buckets
 in the AWS Storage Blog. 
For more information about AWS Training and Certification, see https://aws.amazon.com/training/. 
Your feedback is welcome and appreciated. If you would like to share any feedback, suggestions, or corrections, please provide the details in our AWS Training and Certification Contact Form. 


