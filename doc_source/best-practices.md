# Best Practices for Account Administrators<a name="best-practices"></a>

This topic is intended primarily for master account administrators\.

Master account administrators are responsible for explaining some tasks that AWS Control Tower guardrails prevent their member account administrators from doing\. This topic describes some best practices and procedures for transferring this knowledge, and it gives other tips for setting up and maintaining your AWS Control Tower environment efficiently\.

## Explaining Access to Users<a name="explaining-users"></a>

The AWS Control Tower console is available only to users with the master account administrator permissions\. Only these users can perform administrative work within your landing zone\. In accordance with best practices, this means that the majority of your users and member account administrators will never see the AWS Control Tower console\. As a member of the master account administrator group, it's your responsibility to explain the following information to the users and administrators of your member accounts, as appropriate\.
+ Explain which AWS resources that users and administrators have access to within the landing zone\.
+ List the preventive guardrails that apply to each Organizational Unit \(OU\) so that the other administrators can plan and execute their AWS workloads accordingly\.

### Explaining Resource Access<a name="explaining-resource-access"></a>

Some administrators and other users may need an explanation of the AWS resources to which they have access to within your landing zone\. This access can include programmatic access and console\-based access\. Generally speaking, read access and write access for AWS resources is allowed\. To perform work within AWS, your users require some level of access to the specific services they need to do their jobs\.

Some users, such as your AWS developers, may need to know about the resources to which they have access, so they can create engineering solutions\. Other users, such as the end users of the applications that run on AWS services, do not need to know about AWS resources within your landing zone\.

AWS offers tools to identify the scope of a user's AWS resource access\. After you identify the scope of a user's access, you can share that information with the user, in accordance with your organization's information management policies\. For more information about these tools, see the links that follow\. 
+ **AWS access advisor** – The AWS Identity and Access Management \(IAM\) access advisor tool lets you determine the permissions that your developers have by analyzing the last timestamp when an IAM entity, such as a user, role, or group, called an AWS service\. You can audit service access and remove unnecessary permissions, and you can automate the process if needed\. For more information, see [our AWS Security blog post](http://aws.amazon.com/blogs/security/automate-analyzing-permissions-using-iam-access-advisor)\.
+ **IAM policy simulator** – With the IAM policy simulator, you can test and troubleshoot IAM\-based and resource\-based policies\. For more information, see [Testing IAM Policies with the IAM Policy Simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html)\.
+ **AWS CloudTrail logs** – You can review AWS CloudTrail logs to see actions taken by a user, role, or AWS service\. For more information about CloudTrail, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)\.

  Actions taken by CloudTrail landing zone administrators are logged in the landing zone master account\. Actions taken by member account administrators and users are logged in the shared log archive account\.

  You can view a summary table of AWS Control Tower events in the [**Activities** page\.](https://console.aws.amazon.com/)

### Explaining Preventive Guardrails<a name="explaining-preventive-guardrails"></a>

A preventive guardrail ensures that your organization's accounts maintain compliance with your corporate policies\. The status of a preventive guardrail is either **enforced** or **not\-enabled**\. A preventive guardrail prevents policy violations by using service control policies and AWS Lambda functions\. In comparison, a detective guardrail only informs you of various events or states that exist\.

Some of your users, such as AWS developers, may need to know about the preventive guardrails that apply to any accounts and OUs they use, so they can create engineering solutions\. The following procedure offers some guidance on how to provide this information for the right users, according to your organization's information management policies\.

**Note**  
This procedure assumes you've already created at least one child OU within your landing zone, as well as at least one AWS Single Sign\-On user\.

**To show preventive guardrails for users with a need to know**

1. Sign in to the AWS Control Tower console at [https://console\.aws\.amazon\.com/controltower/](https://console.aws.amazon.com/controltower/)\.

1. From the left navigation, choose **Organizational units**\.

1. From the table, choose the **name** of one of the OUs for which your user needs information about the applicable guardrails\.

1. Note the name of the OU and the guardrails that apply to this OU\.

1. Repeat the previous two steps for each OU about which your user needs information\.

For detailed information about the guardrails and their functions, see [Guardrails in AWS Control Tower](guardrails.md)\.

## Administrative Tips for Landing Zone Setup<a name="tips-for-admin-setup"></a>
+ The AWS Region where you do the most work should be your home region\.
+ Set up your landing zone and deploy your Account Factory accounts from within your home region\.
+ If you’re investing in several AWS Regions, be sure that your cloud resources are in the region where you’ll do most of your cloud administrative work and run your workloads\.
+ The audit and other buckets are created in the same AWS Region from which you launch AWS Control Tower\. We recommend that you do not move these buckets\.

## Administrative Tips for Landing Zone Maintenance<a name="tips-for-admin-maint"></a>
+ You can make your own log buckets in the log archive account\. Just be sure to leave the buckets created by AWS Control Tower\. Note that your Amazon S3 access logs must be in the same AWS Region as the source buckets\. 
+ By keeping your workloads and logs in the same AWS Region, you reduce the cost that would be associated with moving and retrieving log information across regions\.
+ The VPC created by AWS Control Tower is limited to the AWS Regions in which AWS Control Tower is available\. Some customers whose workloads run in non\-supported regions may want to disable the VPC that is created with your Account Factory account\. They may prefer to create a new VPC using the AWS Service Catalog portfolio, or to create a custom VPC that runs in only the required regions\.
+  If you delete your default VPC in your home AWS Region, it's best to delete it in all other AWS Regions\. 

## Log in as a Root User<a name="root-login"></a>

Certain administrative tasks require that you must log in as a root user\. You can log in as a root user to an AWS account that was created by account factory in AWS Control Tower\.

**You must log in as a root user to perform the following actions:**
+ Change certain account settings, including the account name, root user password, or email address\. For more information, see [Updating and Moving Account Factory Accounts](account-factory.md#updating-account-factory-accounts)\.
+ To change or enable your [AWS Support plan](https://docs.aws.amazon.com/controltower/latest/userguide/troubleshooting.html#getting-support)\.
+ To [close an AWS Account](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/close-account.html)\.
+ For more information about actions that require root login credentials, please see [AWS Tasks that Require AWS Root Login Credentials](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\.

**Procedure**

1. Open the AWS sign\-in page\.

   If you don't have the email address of the AWS account to which you require access, you can get it from AWS Control Tower\. Open the console for the master account, choose **Accounts**, and look for the email address\.

1. Enter the email address of the AWS account to which you require access, and then choose **Next**\.

1. Choose **Forgot password?** to have password reset instructions sent to the root user email address\.

1.  Open the password reset email message from the root user mailbox, then follow the instructions to reset your password\.

1. Open the AWS sign\-in page, then sign in with your reset password\.

## Recommendations for Setting Up Groups, Roles, and Policies<a name="roles-recommendations"></a>

As you set up your landing zone, it's a good idea to decide ahead of time which users will require access to certain accounts and why\. For example, a security account should be accessible only to the security team, the master account should be accessible only to the cloud administrators' team, and so forth\.

You can restrict the scope of administrative access to your organizations by setting up an IAM role or policy that allows administrators to manage AWS Control Tower actions only\. The recommended approach is to use the IAM Policy `arn:aws:iam::aws:policy/service-role/AWSControlTowerServiceRolePolicy`\. With the `AWSControlTowerServiceRolePolicy` role enabled, an administrator can manage AWS Control Tower only\. Be sure to include appropriate access to AWS Organizations for managing your preventive guardrails, and SCPs, and access to AWS Config, for managing detective guardrails, in each account\. 

When you're setting up the shared audit account in your landing zone, we recommend that you assign the `AWSSecurityAuditors` group to any third\-party auditors of your accounts\. This group gives its members read\-only permission\. An account must not have write permissions on the environment that it is auditing, because it can violate compliance with Separation of Duty requirements for auditors\. 

## Guidance for Creating and Modifying AWS Control Tower Resources<a name="getting-started-guidance"></a>

We recommend the following practices as you create and modify resources in AWS Control Tower\. This guidance might change as the service is updated\.

**General Guidance**
+ Do not modify or delete resources created by AWS Control Tower in the master account or in the shared accounts\. Modification of these resources can require an update to your landing zone\.
+ Do not modify or delete the AWS Identity and Access Management \(IAM\) roles created within the shared accounts in the core organizational unit \(OU\)\. Modification of these roles can require an update to your landing zone\.
+ For more information about the resources created by AWS Control Tower, see [What Are the Shared Accounts?](how-control-tower-works.md#what-shared)

**AWS Organizations Guidance**
+ Do not use AWS Organizations to update service control policies \(SCPs\) that are attached by AWS Control Tower to an AWS Control Tower managed OU\. Doing so could result in the guardrails entering an unknown state, which will require you to re\-enable affected guardrails\.
+ If you use Organizations to create, invite, or move accounts within an organization created by AWS Control Tower, those outside accounts will not be managed by AWS Control Tower and will not appear in the **Accounts** table\.
+ If you use Organizations to create or move OUs within an organization created by AWS Control Tower, those outside OUs will not be managed by AWS Control Tower and will not appear in the **Organizational Units** table\.
+ If you use Organizations to rename or delete an OU that was created by AWS Control Tower, this OU will continue to be displayed by AWS Control Tower using its original name\. You will not be able to provision a new account to this OU using Account Factory\.

**AWS Single Sign\-On Guidance**
+ If you reconfigure your directory in AWS Single Sign\-On to Active Directory, all preconfigured users and groups in AWS SSO will be deleted\.

**Account Factory Guidance**
+ When you use Account Factory to provision new accounts in AWS Service Catalog, do not define `TagOptions`, enable notifications, or create a provisioned product plan\. Doing so can result in a failure to provision a new account\.