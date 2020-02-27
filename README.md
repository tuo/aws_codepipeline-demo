# AWS SAM Codepipeline

smoke test with aws codebuild, codepipeline and codedeploy, so later we could know how to migrate to AWS China with jenkins orchestrating with codebuild/codepipeline since Codepipeline is missing in China region.




###### Use CodePipeline with CodeBuild to Test Code and Run Builds ![https://docs.aws.amazon.com/codebuild/latest/userguide/how-to-create-pipeline.html](https://docs.aws.amazon.com/codebuild/latest/userguide/how-to-create-pipeline.html)

###### Use AWS CodeBuild with Jenkins ![https://docs.aws.amazon.com/codebuild/latest/userguide/jenkins-plugin.html](https://docs.aws.amazon.com/codebuild/latest/userguide/jenkins-plugin.html)


Create a CodeBuild Service Role: https://docs.aws.amazon.com/codebuild/latest/userguide/setting-up.html#setting-up-service-role


#### Deploy 

 

   * create s3 sbucket for deploy 
        
         aws s3 mb s3://tuo-i18n-serverless-artifact

   * sam upload package
   
         sam package --output-template-file packaged.yaml --s3-bucket tuo-i18n-serverless-artifact

   * sam deploy package 
   
         sam deploy --template-file packaged.yaml --region ap-northeast-1 --capabilities CAPABILITY_IAM --stack-name aws-sam-hello  --s3-bucket tuo-i18n-serverless-artifact --confirm-changeset

##### Deploy Pipeline

```
cd pipeline
aws cloudformation create-stack --stack-name aws-sam-hello-pipeline --template-body file://pipeline.yaml --capabilities CAPABILITY_IAM 
```

