### To check what all resources the script will create:
`$terraform plan` <br>

### provide values to the variables during run-time:
Syntax: `$terraform plan -var="variable_name=value"` <br>
`$terraform plan -var "username=vinit" -var "age=30"` <br>
`$terraform apply -var="region=us-west-2" -var="instance_type=t2.micro"` <br>

### provide variable values for different environments like prod, dev, test
Syntax: `$terraform plan -var-file=filename.tfvars` <br>
`$terraform apply -var-file=filename.tfvars` <br>
`$terraform plan -var-file=prod-variables.tfvars` <br>
`$terraform apply -var-file=test-variables.tfvars` <br>
NOTE: prod-variables.tfvars and test-variables.tfvars file should be already present in root directory <br>

### to get variable from local .env 
declare variable like this: <br>
export TF_VAR_variablename=value <br>
echo $TF_VAR_variablename <br>
output: value of that variable will be displayed 

### to check the list of providers in terraform script
`$terraform providers` <br>

### to install the plugins and related configuration (shows like creating backend or initalizing backend)
`$terraform init` <br>

### to create the real infra:
`$terraform apply` <br>

### to validate the syntax and configuration file. Not doing anything with cloud. simply checks all the files for syntax errors:
`$terraform validate` <br>

### if you change manually anything in cloud and tfstate file is having something, that time use this command
ex: if description of ec2 is manually changed, but you have not mentioned anything in script and according to script tfstate file is created.
but now it is out of sync. To make it sync use this command <br>
`$terraform refresh`


### to make the indentation correct
`$terraform fmt` <br>

### somethimes the resources created in cloud with script can damange after changing the script. so you make them correct. you mark them as "taint". so that resource will be recreated.
### NOTE: be caustion while taint (bcz it is not recommonded)
Syntax `$terraform taint resourcename`  (resourcename will be found in tfstate file) <br>
`$terraform taint label1.label2` <br>
ex: `$terraform taint aws_instance.label2` <br>
once this command is executed them terraform mark that resource as "tainted". when you do terraform plan or terraform apply command that time, the taint resoruce will be recreated <br>

### workspace (for different envirnoment)
`$terraform workspace list` (all workspace will be shown) <br>
`$terraform workspace new dev` (new dev workspace is created) <br>
`$terraform workspace show` (it will show you are in which workspace) <br>
`$$terraform workspace select dev` (to switch to another workspace) <br>
`$terraform workspace delete dev` (delete the dev workspace. dont be in that workspace while deleting) <br>

### create tfstate file for already created infra
Syntax: `$terraform import <resource_type>.<resource_name> <resource_id>`
ex: `terraform import aws_instance.label2 instance_id`
