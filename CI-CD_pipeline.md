# CI/CD pipeline

- [CI/CD pipeline](#cicd-pipeline)
    - [What?](#what)
    - [Why?](#why)
    - [When?](#when)
    - [How?](#how)
    - [How to create a Jenkins item](#how-to-create-a-jenkins-item)
    - [Creating a Webhook for our Jenkins item](#creating-a-webhook-for-our-jenkins-item)


![alt text](images-cicd/diagram.png)

### What?
A CI/CD (Continuous Integration/Continuous Delivery) pipeline is a set of automated processes that help teams deliver software changes more frequently and reliably. It involves building, testing, and deploying code changes automatically. Here's a quick breakdown:
- Continuous Integration (CI): This part involves automatically building and testing code changes whenever a developer commits code to a shared repository. It helps identify issues early in the development process.
- Continuous Delivery (CD): This part focuses on automating the deployment of tested code to production or staging environments. The goal is to ensure that software can be released quickly, safely, and frequently. <br> <br>

![alt text](images-cicd/what_cicd.png)

### Why?
Implementing a CI/CD pipeline offers several benefits:
- Faster Feedback: Developers receive immediate feedback on code changes, reducing integration issues.
- Consistency: Automated builds and tests ensure consistent quality across different environments.
- Reduced Risk: Automated deployments minimize human error, making releases more reliable and safer.
- Faster Time to Market: Streamlined processes enable quicker delivery of new features and bug fixes. <br> <br>

![alt text](images-cicd/benefits_cicd.png)

![alt text](images-cicd/business-benefits-cicd.png)


### When?
A CI/CD pipeline is beneficial in any software development project, especially in scenarios where:
- Multiple developers are working on the same codebase.
- Rapid deployment of features and bug fixes is essential.
- Consistent and reliable builds are needed across different environments.
- Testing needs to be automated to ensure code quality.

### How?
Implementing a CI/CD pipeline involves several steps:
- Source Control Management: Use version control systems like Git to manage code changes.
- Automated Builds: Set up tools like Jenkins, Travis CI, or GitLab CI to automatically build your application whenever code changes are pushed.
- Automated Testing: Integrate unit tests, integration tests, and other automated tests into your pipeline to ensure code quality.
- Artifact Management: Store build artifacts in a repository like Nexus or Artifactory.
- Continuous Deployment: Automate the deployment process using tools like Kubernetes, Docker, or AWS Lambda to deploy applications to staging or production environments.
- Monitoring and Feedback: Integrate monitoring tools to track application performance and provide feedback to developers.
<br><br>

![alt text](images-cicd/how_cicd.png)

### How to create a Jenkins item
1. Click on new item
![alt text](images-cicd/clicknewproject.PNG)

2. Name your item and specify the project, in this situation we are using a `Freestyle project`. <br>
 ![alt text](images-cicd/name-item.PNG)

3. Provide a description of your item, this should allow other people to understand the reasoning of your item.
4. Click `GitHub project` and supply the URL of your GitHub project.
5. Click `Restrict where this project can be run` and specify `sparta-ubuntu-node` as this will protect the master branch.
![alt text](images-cicd/init-setup.PNG)
6. Click `Git` for `Source Code Management`, specify the repository using the "SSH" link provided on Github. The `Branch` should also be `main`.
![alt text](images-cicd/scm-setup.PNG)
7. To access the GitHub repo, you must provide the private key. To do this, click on the `add` in the picture above, enter the contents of your private key.
8. We are leaving `Build Triggers` alone for now, but click `Provide Node & npm bin/folder to Path`.
9. For the `Build` box, click `execute shell` as this will be how we run our tests. Here, you must enter the following script:
   1.  `cd app`
   2.  `npm install`
   3.  `npm test` 
    
This will be how we conduct our tests, and what we are specifically testing.

![alt text](images-cicd/final-setup.PNG)

### Creating a Webhook for our Jenkins item
1. Navigate to the Github Settings and click Webhooks.
2. Click create new webhook.
3. Enter the url of your Jenkins page in `Payload URL`.
4. The `Content type` should be `application/json`.
5. Click `Let me select individual events` as we wish to be alerted to both push and pulls.

![alt text](images-cicd/wh-pt1.PNG)

![alt text](images-cicd/wh-pt2.PNG)
6. Next, we must navigate to Jenkins and configure our item to collaborate with the webhook.
7. Click the `GitHub hook trigger for GITScm polling` option and you are done! You have successfully created a Webhook for your Jenkins item.
   
   ![alt text](images-cicd/wh-pt3.PNG)