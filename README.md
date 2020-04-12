# Cloudformation
cloudformation templates to do different things

First you need to create a s3 bucket to store the templates for the stacks you want to create

aws s3 mb s3://cfn-$resource-$name

Now you can upload all artifacts to S3:

aws cloudformation package --template-file example.yml --s3-bucket cfn-$resource-$name --output-template-file packaged.yml

Finally, you can create a CloudFormation stack with aws cloudformation deploy:

aws cloudformation deploy --template-file packaged.yml --stack-name ec2-example --capabilities CAPABILITY_IAM

