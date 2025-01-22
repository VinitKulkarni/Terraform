### To check what all resources the script will create:
$terraform plan

### provide values to the variables during run-time:
Syntax: $terraform plan -var="variable_name=value"
$terraform plan -var "username=vinit" -var "age=30"
$terraform apply -var="region=us-west-2" -var="instance_type=t2.micro"

### provide variable values for different environments like prod, dev, test
Syntax: $terraform plan -var-file=filename.tfvars
$terraform apply -var-file=filename.tfvars
$terraform plan -var-file=prod-variables.tfvars
$terraform apply -var-file=test-variables.tfvars
NOTE: prod-variables.tfvars and test-variables.tfvars file should be already present in root directory

### to get variable from local .env 
declare variable like this: 
export TF_VAR_variablename=value
echo $TF_VAR_variablename 
output: value of that variable will be displayed

### to check the list of providers in terraform script
$terraform providers

### to install the plugins and related configuration (shows like creating backend or initalizing backend)
$terraform init

### to create the real infra:
$terraform apply

### to validate the syntax and configuration file. Not doing anything with cloud. simply checks all the files for syntax errors:
$terraform validate

### if you change manually anything in cloud and tfstate file is having something, that time use this command
ex: if description of ec2 is manually changed, but you have not mentioned anything in script and according to script tfstate file is created.
but now it is out of sync. To make it sync use this command
$terraform refresh


### to make the indentation correct
$terraform fmt

### somethimes the resources created in cloud with script can damange after changing the script. so you make them correct. you mark them as "taint". so that resource will be recreated.
### NOTE: be caustion while taint (bcz it is not recommonded)
Syntax $terraform taint resourcename  (resourcename will be found in tfstate file)
$terraform taint label1.label2
ex: $terraform taint aws_instance.label2
once this command is executed them terraform mark that resource as "tainted". when you do terraform plan or terraform apply command that time, the taint resoruce will be recreated

### workspace (for different envirnoment)
$terraform workspace list (all workspace will be shown)
$terraform workspace new dev (new dev workspace is created)
$terraform workspace show (it will show you are in which workspace)
$$terraform workspace select dev (to switch to another workspace)
$terraform workspace delete dev (delete the dev workspace. dont be in that workspace while deleting)

### create tfstate file for already created infra
$terraform import resourcename
