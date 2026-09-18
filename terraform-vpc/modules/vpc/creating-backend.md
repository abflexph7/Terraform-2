aws s3api create-bucket \
  --bucket tfstate-devops-$(whoami)-$(date +%Y%m%d) \
  --region eu-west-2 \
  --create-bucket-configuration LocationConstraint=eu-west-2

aws s3api put-bucket-versioning \
  --bucket YOUR-BUCKET-NAME \
  --versioning-configuration Status=Enabled

aws dynamodb create-table \
  --table-name terraform-lock \
  --attribute-definitions AttributeName=LockID,AttributeType=S \
  --key-schema AttributeName=LockID,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST \
  --region eu-west-2

  Terraform state files need to be stored in a safe place so that they are not accidentally tampered with. This shows you how to create an S3 bucket in AWS to store the state file.