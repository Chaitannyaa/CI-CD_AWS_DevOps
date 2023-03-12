# CI-CD_AWS_DevOps
CodePipeline using all AWS services - (AWS CodeCommit + CodeBuild + CodeDeploy + EC2 + S3 + IAM)

# Lets Create CI/CD pipeline in AWS 

- We are going to use AWS CodeCommmit as our code repository (Its similar to GitHub Repos)
- You need IAM user to commit into our CodeCommit repos so create a user
- Microsoft VS code as our editor (You can use editor of your choice)
- AWS CodeBuild will create a build of our code
- Built_code will be stored in Amazon S3
- We need a running EC2 instance to host our app/website/code
- CodeDeploy will use Built-code from S3 to deploy our app/website/code on AWS resources
And
- You can configure a CodePipeline to do all above stuff in an automated fashion..And your every single change in CodeCommit will reflect in our end delivery(App/Website)

So Lets do it >>>>>

![Thank-You](https://user-images.githubusercontent.com/117350787/224546984-b791a2b9-1a3a-4109-bc27-9c2a1a168677.jpeg)
