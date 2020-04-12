# Cloudformation
cloudformation templates to do different things

First you need to create a s3 bucket to store the templates for the stacks you want to create

aws s3 mb s3://cfn-$resource-$name

Now you can upload all artifacts to S3:

aws cloudformation package --template-file example.yml --s3-bucket cfn-$resource-$name --output-template-file packaged-$resource.yml

Finally, you can create a CloudFormation stack with aws cloudformation deploy:

aws cloudformation deploy --template-file packaged-$resource.yml --stack-name $resource-example --capabilities CAPABILITY_IAM

Creating the stack will take about 10 minutes. You can find information in fields of the outputs:

aws cloudformation describe-stacks --stack-name $resource-example --query "Stacks[0].Outputs"


Don't forget to delete the stack:

aws cloudformation delete-stack --stack-name $resource-example
aws cloudformation wait stack-delete-complete --stack-name $resource-example


