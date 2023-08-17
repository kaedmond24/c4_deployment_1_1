# Deployment using Jenkins and AWS Elastic Beanstalk

1. Log into the Jenkins server using your _username_ and _password_
   ![deploy1_1](/images/deploy1_1.png)<br><br>

2. On the Jenkins dashboard, select a _new item_ to setup the pipeline
   ![deploy1_2](/images/deploy1_2.png)<br><br>

3. Create a name, then select the _Pipeline_ option
   ![deploy1_3](/images/deploy1_3.png)<br><br>

4. Define a pipeline script using the ‘Pipeline script from SCM’ option<br><br>

5. Enter the Github repository link for the project
   ![deploy1_4](/images/deploy1_4.png)<br><br>

6. Select _Add_ to setup your Github credentials

- [How to setup Github access token](https://docs.github.com/en/enterprise-server@3.8/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)<br>
  ![deploy1_6](/images/deploy1_6.png)<br><br>

7. Select your Github credentials<br><br>

8. Set _Branch Specifier_ to _\*/main_ branch<br><br>

9. Apply and Save
   ![deploy1_7](/images/deploy1_7.png)<br><br>

10. Select _Build Now_ option
    ![deploy1_8](/images/deploy1_8.png)<br><br>

11. Wait for _SCM Checkout_, _Build_, and _Test_ stages to complete
    ![deploy1_9](/images/deploy1_9.png)<br><br>

12. Upon Successful completion, package application files into a zip file in preparation for deployment to AWS Elastic Beanstalk<br><br>

13. Login into AWS console<br><br>

14. Create IAM roles for needed services

    - [How to Create an AWS IAM Role for Elastic Beanstalk and EC2](https://scribehow.com/shared/How_to_Create_an_AWS_IAM_Role_for_Elastic_Beanstalk_and_EC2__kTg4B7zRRxCp-aYTJc-WLg)<br><br>

15. Setup AWS Elastic Beanstalk

    - [Create and Deploy a Python URL Shortener on AWS Elastic Beanstalk](https://scribehow.com/shared/How_to_Create_and_Deploy_a_Python_URL_Shortener_on_AWS_Elastic_Beanstalk__MS9pB8lfRaGFiKAq2FU-cw)<br><br>

16. Test application access using the domain link provided by AWS Elastic Beanstalk
    ![deploy1_10](/images/deploy1_10.png)<br>
    ![deploy1_11](/images/deploy1_11.png)<br><br>

## Troubleshooting
