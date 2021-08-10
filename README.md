# OpsLyft
 OpsLyft lambda function


#Short description
Note: This example setup is a simple solution. For a more robust solution, use the AWS Instance Scheduler. For more information, see How do I stop and start my instances using the AWS Instance Scheduler?

To stop and start EC2 instances at regular intervals using Lambda, do the following:

1.    Create a custom AWS Identity and Access Management (IAM) policy and execution role for your Lambda function.

2.    Create Lambda functions that stop and start your EC2 instances.

3.    Test  Lambda functions.

##Create an IAM policy and execution role for your Lambda function
2.    Create an IAM role for Lambda.

Important: When attaching a permissions policy to Lambda, make sure that you choose the IAM policy you just created.

#Create Lambda functions that stop and start your EC2 instances
1.    In the AWS Lambda console, choose Create function.

2.    Choose Author from scratch.

3.    Under Basic information, add the following:
For Function name, enter a name that identifies it as the function used to stop your EC2 instances. For example, "StopEC2Instances".
For Runtime, choose Python 3.8.
Under Permissions, expand Choose or create an execution role.
Under Execution role, choose Use an existing role.
Under Existing role, choose the IAM role that you created.

4.    Choose Create function.

5.    Under Function code, copy and paste the following code into the editor pane in the code editor (lambda_function). This code stops the EC2 instances that you identify.

--Example function code—stopping EC2 instances
Important: For region, replace "us-west-1" with the AWS Region that your instances are in. For instances, replace the example EC2 instance IDs with the IDs of the specific instances that you want to stop and start.

6.    Under Basic settings, set Timeout to 10 seconds.
7.    Choose Deploy.


8.    Repeat steps 1-7 to create another function. Do the following differently so that this function starts your EC2 instances:
In step 3, enter a different Function name than the one you used before. For example, "StartEC2Instances".
In step 5, copy and paste the following code into the editor pane in the code editor (lambda_function):

Important: For region and instances , use the same values that you used for the code to stop your EC2 instances.

#Test your Lambda functions
1.    In the AWS Lambda console, choose Functions.

2.    Choose one of the functions that you created.

3.    Choose Test.

4.    In the Configure test event dialog box, choose Create new test event.

5.    Enter an Event name. Then, choose Create.
Note: You don't need to change the JSON code for the test event—the function doesn't use it.

6.    Choose Test to run the function.

7.    Repeat steps 1-6 for the other function that you created.

Tip: You can check the status of your EC2 instances before and after testing to confirm that your functions work as expected.

#Create CloudWatch Events rules that trigger your Lambda functions
1.    Open the Amazon CloudWatch console.

2.    In the left navigation pane, under Events, choose Rules.

3.    Choose Create rule.

4.    Under Event Source, choose Schedule.

5.    Do either of the following:
For Fixed rate of, enter an interval of time in minutes, hours, or days.
For Cron expression, enter an expression that tells Lambda when to stop your instances. For information on expression syntax, see Schedule expressions for rules.
Note: Cron expressions are evaluated in UTC. Make sure that you adjust the expression for your preferred time zone.
6.    Under Targets, choose Add target.

7.    Choose Lambda function.

8.    For Function, choose the function that stops your EC2 instances.

9.    Choose Configure details.

10.    Under Rule definition, do the following:
For Name, enter a name to identify the rule, such as "StopEC2Instances".
(Optional) For Description, describe your rule. For example, "Stops EC2 instances every night at 10 PM."
For State, choose the Enabled check box.

11.    Choose Create rule.
12.    Repeat steps 1-11 to create a rule to start your EC2 instances. Do the following differently:
In step 5, for Cron expression, enter an expression that tells Lambda when to start your instances.
In step 8, for Function, choose the function that starts your EC2 instances.
In step 10, under Rule definition, enter a Name, such as "StartEC2Instances".
(Optional) Enter a Description, such as "Starts EC2 instances every morning at 7 AM."
