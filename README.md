# useful-scripts

Sum up EC2 instance type counts in each region
~~~
 for region in `aws ec2 describe-regions --output text | cut -f3`; 
 do   echo -e "\nListing Instances in region:'$region'...";  
 aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,InstanceType]' --filters "Name=instance-state-code,Values=16" --region $region  --output text | awk '{++map[$2]}END{ for( i in map ){print i,map[i] } }'; done
~~~


select instance ID by security group
~~~
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId]' --filters "Name=instance.group-id,Values=sg-3e89f577" --output text
~~~

