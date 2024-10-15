# AWS_LAB
🌟 Creating an IAM Role for S3 Bucket Access 🌟
Task : create an IAM role that allows an IAM user to list S3 buckets only after switching roles and logging in with the new role. The IAM user should not be able to list S3 buckets when logging in with their regular credentials.
Step 1: Create an IAM Role
Sign in to the AWS Management Console. 🔑

Open the IAM Console:

Navigate to the IAM service in the AWS Management Console. 📂
Create a New Role:

Click on Roles in the left-hand menu.
Click on the Create role button. ➕
Select Trusted Entity:

Choose Another AWS account.
Enter your Account ID in the Account ID field (this allows users in your account to assume the role). 🔄
Set Permissions:

Click on Next: Permissions.
Click on Create policy to define the specific permissions for this role. 📜
Step 2: Define the Policy for the Role
Create Policy:

Select the JSON tab in the policy creation interface.
Enter the following policy JSON, which allows listing S3 buckets:
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "*"
        }
    ]
}
Review and Create the Policy:

Click on Review policy.
Provide a name (e.g., ListS3BucketsPolicy) and a description for your policy.
Click on Create policy. ✅
Attach the Policy to the Role:

Go back to the role creation tab.
Find the policy you just created by searching for ListS3BucketsPolicy.
Check the box next to the policy and click on Next: Tags. 🏷️
Add Tags (Optional):

You can add tags if necessary for organization or tracking.
Click Next: Review.
Review and Create Role:

Provide a role name (e.g., S3ListRole) and a description.
Click on Create role. 🎊
Step 3: Modify the IAM User Policy
Open the Users Section:

Click on Users in the left-hand menu.
Select the user who should assume the new role. 👤
Edit User Permissions:

Go to the Permissions tab.
Click on Add permissions and then Attach policies directly.
Ensure there are no policies that grant S3 permissions. If there are, remove them. ❌
Create a Policy to Allow Role Switching:

Click on Create policy.
Switch to the JSON tab and use the following policy:
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<YOUR_ACCOUNT_ID>:role/S3ListRole"
        }
    ]
}
Replace <YOUR_ACCOUNT_ID> with your actual AWS account ID. 🔧
Attach the Policy to the User:

Review and create this policy.
Attach this policy to the user. 🔗
Step 4: Verify User Permissions
At this point, the IAM user should not have permissions to list S3 buckets directly using their regular credentials. Verify this by doing the following:

Sign in as the IAM User:

Use the IAM user credentials to log into the AWS Management Console. 🖥️
Attempt to List S3 Buckets:

Navigate to the S3 service.
You should receive an Access Denied message when attempting to list buckets. 🚫
Step 5: Switch to the IAM Role
Switch Roles in the Console:

Click on your user name in the top-right corner of the console.
Select Switch Role. 🔄
Enter Role Information:

Fill in the Account ID with your AWS account ID.
Enter the Role Name as S3ListRole.
Optionally, choose a display name and color. 🎨
Switch Role:

Click Switch Role. 🔃
List S3 Buckets:

Now you should have permissions to list the S3 buckets. Navigate to the S3 service again and verify that you can see the buckets. 📊
