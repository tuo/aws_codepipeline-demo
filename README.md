# AWS SAM CodeBuild & CodeDeploy & Jenkins

smoke test with aws codebuild, codepipeline and codedeploy, so later we could know how to migrate to AWS China with jenkins orchestrating with codebuild/codedeploy since Codepipeline is missing in China region.


---

`Use CodePipeline with CodeBuild to Test Code and Run Builds`: [https://docs.aws.amazon.com/codebuild/latest/userguide/how-to-create-pipeline.html](https://docs.aws.amazon.com/codebuild/latest/userguide/how-to-create-pipeline.html)

`AWS CodeBuild with Jenkins`: [https://docs.aws.amazon.com/codebuild/latest/userguide/jenkins-plugin.html](https://docs.aws.amazon.com/codebuild/latest/userguide/jenkins-plugin.html)


`Create a CodeBuild Service Role`: [https://docs.aws.amazon.com/codebuild/latest/userguide/setting-up.html#setting-up-service-role](https://docs.aws.amazon.com/codebuild/latest/userguide/setting-up.html#setting-up-service-role)

`Tutorial: Create a Four-Stage Pipeline`: [https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-four-stage-pipeline.html](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-four-stage-pipeline.html)

`AWS re:Invent blog`: [https://amazonaws-china.com/blogs/aws/category/events/reinvent/](https://amazonaws-china.com/blogs/aws/category/events/reinvent/) 

`AWS Serverless CI/CD for the enterprise on the AWS Cloud`: [https://github.com/aws-quickstart/quickstart-trek10-serverless-enterprise-cicd](https://github.com/aws-quickstart/quickstart-trek10-serverless-enterprise-cicd)

`Implementing safe AWS Lambda deployments with AWS CodeDeploy`: https://amazonaws-china.com/blogs/compute/implementing-safe-aws-lambda-deployments-with-aws-codedeploy/

https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-lambda-sam.html

https://docs.aws.amazon.com/codebuild/latest/userguide/sample-codedeploy.html


`How to build a CI/CD pipeline for Serverless apps with AWS CodePipeline and CodeBuild`: https://seed.run/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-codepipeline-and-codebuild

## SAM and CodeDeploy

better reference to [AWS Serverless Application Model Document GUide on Deploy](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-deploying.html)

Safe Lambda deployments: https://github.com/awslabs/serverless-application-model/blob/master/docs/safe_lambda_deployments.rst

sam build rebuild everytime: https://github.com/awslabs/aws-sam-cli/issues/805

## Deploy 

 

   * create s3 sbucket for deploy 
        
         aws s3 mb s3://tuo-i18n-serverless-artifact

   * sam upload package
   
         sam package --output-template-file packaged.yaml --s3-bucket tuo-i18n-serverless-artifact

   * sam deploy package 
   
         sam deploy --template-file packaged.yaml --region ap-northeast-1 --capabilities CAPABILITY_IAM --stack-name aws-sam-hello  --s3-bucket tuo-i18n-serverless-artifact --confirm-changeset

## Deploy Pipeline

```
cd pipeline
aws cloudformation create-stack --stack-name aws-sam-hello-pipeline --template-body file://pipeline.yaml --capabilities CAPABILITY_IAM 
```



## TODO:


https://amazonaws-china.com/blogs/devops/building-and-testing-polyglot-applications-using-aws-codebuild/

https://stackoverflow.com/questions/53987204/is-it-possible-recommended-to-use-sam-build-in-aws-codebuild


1. lint your code
2. run unit test before build
3. sam build on build stage (no need run against container)
4. sam package in post build 
 
possible speed up with provisioning with docker.cn registery ?
https://docs.aws.amazon.com/codebuild/latest/userguide/sample-private-registry.html     

![codebuild_phases.png](./screenshots/codebuild_phases.png)
![jenkins](./screenshots/jenkins.png)
![codebuild_log.png](./screenshots/codebuild_log.png)