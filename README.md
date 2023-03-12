# CI-CD_AWS_DevOps
CodePipeline using all AWS services - (AWS CodeCommit + Artifacts + CodeBuild + CodeDeploy + EC2 + S3 + IAM)

# Lets Create CI/CD pipeline in AWS 

- We are going to use AWS CodeCommmit as our code repository (Its similar to GitHub Repos).
- You need IAM user to commit into our CodeCommit repos so create a user.
- Microsoft VS code as our editor (You can use editor of your choice).
- AWS CodeBuild will create a build of our code.
- Built_code will be stored in Amazon S3.
- We need a running EC2 instance to host our app/website/code.
- CodeDeploy will use Built-code from S3 to deploy our app/website/code on AWS resources.
And
- You can configure a CodePipeline to do all above stuff in an automated fashion..And your every single change in CodeCommit will reflect in our end delivery(App/Website).

So Lets do it >>>>>

1) Create IAM user with these permissions-->
   Note User Access key ID and Secret Access key to access AWS services remotely from our local M/c.
    ![Capture](https://user-images.githubusercontent.com/117350787/224547216-b813ffed-f86d-4b79-9dcc-9c2cf25afe0c.PNG)

2) Create a simple index.html, a buildspec.yml and an appspec.yml file-->
   
   - Hosting website using Index.html file will be an output of our pipeline.
     ![Capture2](https://user-images.githubusercontent.com/117350787/224549271-0e6d1f7e-c445-41e5-9fb1-44426dd93337.PNG)
   
   - To create a build of our code we need a buildspec.yml file (blueprint of setup), with this file our CodeBuild service will create the required environment to run.
   We are going to install the Nginx web server to host our website...So provide our *index.html* file to /var/www/html/******  directory path of nginx server.
   Artifacts are our code_data stored on AWS platform as an Artifacts/ S3 object to access by different services 
   (Artifacts:_files:_"**/*"  -->> Includes all your data)
   
   buildspec.yml
   ---------------
   ![Capture1](https://user-images.githubusercontent.com/117350787/224547908-a7717e18-070f-4a37-887c-18712f650117.PNG)
   
   - To create hosting/run environment we need to appspec.yml to tell CodeDeploy to make suitable environment run our website/app on EC2 instance.
   
   appspec.yml
   ---------------
   ![Capture4](https://user-images.githubusercontent.com/117350787/224549811-70a9cd28-d8c4-47b9-89d9-7f7721389c29.PNG)
   
   There two bash scripts used to perform setup for our webserver.
   
   install.sh     and     start.sh
   ---------------------------------
   ![Capture5](https://user-images.githubusercontent.com/117350787/224550174-f4be6b16-030e-4d12-b19f-f88201ed90bd.PNG)
   
  3) Commit all your files to AWS CodeCommit repo from local M/c after signing through your IAM user credentials--->
     [https://docs.aws.amazon.com/codecommit/latest/userguide/how-to-create-file.html]
     Make sure you get all your files in AWS CodeCommit repos.
     ![Capture6](https://user-images.githubusercontent.com/117350787/224550479-0d583109-5535-423a-ae1d-f38a07caa392.PNG)
    
  4) Now create new build project, Start build, Check S3 bucket for created buildname.zip file--->
     ![Capture7](https://user-images.githubusercontent.com/117350787/224551059-0c692bb8-b1eb-413b-9125-cdce1c49fc72.PNG)
     Note your service role must contain AWSs3FullAccess policy attached.
     
     Start build and check S3 for built .zip file.
     ![Capture8](https://user-images.githubusercontent.com/117350787/224551346-eee59ec6-ddbb-48f2-9f51-7ba50dcbcbb9.PNG)
  
  5) Provision an EC2 instance (ubuntu) and Modify IAM role--->
     IAM role must have following policies attached.
     ![Capture10](https://user-images.githubusercontent.com/117350787/224551996-f384eeda-2085-425b-8e6d-f67d7ed37ada.PNG)
  
  6) SSH into EC2 instance and do follow instructions given below to setup CodeDeploy agent on ec2 instance--->
     ![Capture17](https://user-images.githubusercontent.com/117350787/224555697-2deb716b-3963-4650-ba14-db33a63ff83f.PNG)

     
  7) Create Application under CodeDeploy service, create deployment group and start deployment--->
     Note while creating deployment group do select "Never" in "Install AWS CodeDeploy Agent" Because we have already installed AWS codeDeploy agent in previous step.
     ![Capture11](https://user-images.githubusercontent.com/117350787/224552877-f4c4e133-1e97-407d-9e54-796910ff4909.PNG)
     
     Note while creating deployment group you assign/create a service role so it must contain following policies..
     ![Capture9](https://user-images.githubusercontent.com/117350787/224551659-a0679bd0-e90d-4de1-ba3c-eadf91cbcde2.PNG)
     
     Start Deployment...If it shows "Succeeded" then put your EC2 instance public ip address in browser!
     ![Capture12](https://user-images.githubusercontent.com/117350787/224553539-4f95eae9-c773-4cf4-adfa-a91a3bcbe593.PNG)
     
  8) Now create a CodePipeline to automate the CodeCommit>>CodeBuild>>CodeDeploy--->
     Configure pipeline setting.
     Note in AWS CodeCommit stage>>Change detection options --select AWS CodePipeline option.
     ![Capture13](https://user-images.githubusercontent.com/117350787/224554260-0801a948-5241-427f-b17a-501b59192e09.PNG)

    Create and check three stages..You can check error events if any stage fails. Do Correct if needed.
    Click release changes..Its done!
    
  9) Now you just commit any changes you want in your code those changes will reflect in website.
     You can monitor the stages on AWS CodePipeline service console.
     ![Capture14](https://user-images.githubusercontent.com/117350787/224555035-f20936af-3bab-4407-99c3-4845b0eac4dc.PNG)
     ![Capture15](https://user-images.githubusercontent.com/117350787/224555142-41c27924-5497-4ef9-b9f5-3c999867e244.PNG)
     
  10) You can see commit changes on website !
      ![Capture16](https://user-images.githubusercontent.com/117350787/224555278-52657f70-f4b1-4872-a70a-9c6a1b1ce71a.PNG)

Thanks for efforts :sunglasses: and :thumbsup:

     
