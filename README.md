# Jenkins-Terraform-AWS
Create an ec2 instance  with the help of Terraform and Jenkins

## Steps:
1. Create an IAM Role with Administrator previlages in AWS.
2. Get the Access key ID and Secret Access key.
3. Add Credentials in Jenkins with the ID names as below.   
    **AWS_ACCESS_KEY_ID**<br />**AWS_SECRET_ACCESS_KEY**
4. Create a Jenkins Job and select Pipeline.
5. Go to configuration, in the Pipeline section in Definition Select **pipeline script from SCM**.
6. Select Git as the SCM.
7. Provide the Repository URL.(Add Creds if the Repo is private)
8. Specify the **Branch** and the **Script path**.
9. Save and build your pipeline.
