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

---

## Troubleshooting AWS Elastic Beanstalk Health Degradation

- I've already identified a server-side error, 502 Error Bad Gateway, from the AWS EB web app link.<br><br>

- The next step would be to check the server logs by Selecting last 100 lines and download logs<br><br>
  ![deploy1_10](/images/deploy1_12.png)<br>
  ![deploy1_11](/images/deploy1_13.png)<br><br>

- After a quick review of the logs and I was able to find the following log message:<br><br>

  > Aug 17 01:08:08 ip-172-31-14-228 web\[2687\]: ModuleNotFoundError: No module named 'application'<br><br>

- The _ModuleNotFoundError_ is a python error notice signifying either a missing/uninstalled module that is unable to be imported into the application or an incorrect spelling of a module name. This error consequently is causing the failure of a server worker process which effectively crashes the application.<br><br>

- To confirm the if the application configuration setup is correct I checked the AWS Elastic Beastalk documentation for Python Flask [here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html).<br><br>

- According to the documentation,<br>

> Using application.py as the filename and providing a callable application object (the Flask object, in this case) allows Elastic Beanstalk to easily find your application's code.<br><br>

- This error can be fixed by reviewing the python app.py file and renaming the file to application.py. Moreover, an update to the test_app.py file needed. The test_app.py is dependent on the correct reference to the application.py file allowing for import and testing of the application.<br><br>
  ![deploy1_11](/images/deploy1_14.png)<br>
  ![deploy1_11](/images/deploy1_15.png)<br><br>

- Once the issue was fixed, the updated file was saved and a new application deployment zip file (c4_deployment1_1_v2.zip) was created. All updates and fixes were commit and pushed to github followed by re-running the Jenkins build pipeline.<br><br>
  ![deploy1_11](/images/deploy1_16.png)<br><br>

- In the AWS Elastic Beanstalk service dashboard, the Upload and Deploy option was used to load the _c4_deployment1_1_v2.zip_ file.<br><br>
  ![deploy1_11](/images/deploy1_17.png)<br>
  ![deploy1_11](/images/deploy1_18.png)<br><br>

- I attempted to restart the app server, however, I kept receiving the same error.<br><br>

- Finally, I used the rebuild environment option. Once the environment was rebuilt, the application began to run successfully.<br><br>
  ![deploy1_11](/images/deploy1_19.png)<br>
  ![deploy1_11](/images/deploy1_20.png)<br>
  ![deploy1_11](/images/deploy1_21.png)<br><br>
