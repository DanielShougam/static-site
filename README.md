# Daniel Shougam's static site

The website is accessible at:
http://daniel-shougam-static-site-bucket.s3-website-us-east-1.amazonaws.com/

### Notes
#### What I did
This was built using S3 and CodePipeline.
I chose S3 as the requirements only specify that the website must host static text. For this use case S3 is a good choice as it is simple to setup and has high availability and durability.  
  
I chose CodePipeline and linked it to this Github repository so that any future changes can be triggered via `git push` rather than manually updating the files in the bucket.  
  
#### What I would do if I had more time
1. Use Cloudfront to enable TLS for the website
2. Utilise IaC tools such as Cloudfront or Terraform to automate the deployment of the S3 bucket and CodePipeline

#### Alternative Solutions
1. Deploy an EC2 VM and run nginx or nodejs to host the site. I decided against this as this would overcomplicate the solution which requires only to host a static site. In the long term this also creates operational overhead, as a team has to ensure the host and site is up, and regularly patched.  
2. Deploying the website via AWS Amplify. Reading the AWS documentation this is their recommended service for deploying a static site, however I do not have experience with it and decided not to use it.  
  
#### Making it Production Ready
To make the website production grade, I would first utilise CloudFront to distribute the site throughout the AWS CDN, and to enable TLS.  
Secondly, I would utilise IaC to codify the infrastructure resources to remove Click Ops.  
Thirdly, I would utilise stages within CodePipeline to add a test stage, so that changes to the website can be tested before they are pushed to the live site.  
Finally, assuming that the site is developed further with different teams working on different sections, I would utilise IAM roles/policies and Bucket policies to ensure that those teams only modify the objects they are required to. 