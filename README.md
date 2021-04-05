# Best practices for provisioning Amazon SageMaker Studio

This repository includes reference architecture and cloud formation templates for provisioning SageMaker Studio. We use Service Catalog to set up and provision users. Diagram below showcases two flows that are supported, Cloud Admin and Data Scientist flows.

![Alt Flow Diagram](images/flow_diagram.png?raw=true "Flow Diagram")

If you would like to learn more about how we go about provisioning, please review the sections below. If you would like get started with the setup, please click the button below to create a Service Catalog Product and Product Portfolio which can provision Studio and its associated roles: 

[![Launch in us-west-2](https://raw.githubusercontent.com/awslabs/aws-media-insights-engine/development/docs/assets/images/launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=sagemaker-studio&templateURL=https://studio-provisioning-aggarzo.s3-us-west-2.amazonaws.com/launch.template)

This setup covers two personas:

* *Cloud Admin* – This team is also responsible for building and maintaining the infrastructure for supporting ML services, such as provisioning notebooks for data scientists to use, creating secure buckets for storing data, managing costs for ML from various lines of business (LOBs), and more.

* *Data science COE:* Data scientists within an AI Center of Excellence (COE) or embedded within the LOBs are responsible for building, training, and deploying models. In regulated industries, data scientists need to adhere to the organization’s security boundaries, such as using encrypted buckets for data access, use of private networking for accessing APIs, committing code to source control, ensuring all their experiments and trials are properly logged, enforcing encryption of data in transit, and monitoring deployed models.


Below are the resources the template provisions:

1. Cloud Admin IAM Role
2. Provisioning IAM Role
3. Data Scientist IAM Role
4. Studio Execution IAM Role
5. Three Service Catalog products 
* Create Domain
* Create User
* Attach Image 


## Below are the steps you will go through:

### Populate Sevice Catalog Products

0. You will need an IAM user designated to use for launch product provisioning from Service Catalog. Please attach the **ServiceCartalogEndUserFullAccess** managed policy to the IAM user. Note that, the IAM user used for product provisoning from Service Catalog does not need access to SageMaker. Service Catalog will use a separate role for spinning up SageMaker Studio resources which will be also created along with the Service Catalog products.

Note that, you also can create just an IAM role instead of an IAM user which can be assumed before product provisioning.

1. Click on the Launch button above. Note - by default the template will launch in US-WEST-2 and you can switch to other regions before starting the CNF template.

2. Click next

3. Update the Launch Principal. This can be an IAM user, group or role which grants provisioning access to this product. Use the user you just created during the first step. Click the **Next** button.
 
![Alt Launch Principal](assets/launch_principal.jpg?raw=true "Launch Principal")
  
4. Click the **Next** button. Acknoledge that AWS CloudFormation template will create IAM resources by clicking the checkbox at the bottom of the page. Hit the **Create stack** button.



### Provision SageMaker Studio Domain

4. Go to **AWS Console / Service Catalog / Products**. Launch the **SageMaker Studio** product.

![Alt Step 1](assets/step1.jpg?raw=true "Step 1")

5. Provide a name for the product, your VPC and subenet IDs used for SageMaker communication and hit the Launch Product button

![Alt Step 2](assets/step2.jpg?raw=true "Step 2")

5. Get the domain-id of your newly created SageMaker Domain. Go to the SageMaker Console, and hit on SageMaker studio on the left pane.

![Alt Step 3](assets/step3.jpg?raw=true "Step 3")

6. To provision a user profile, go to service catalog and launch the **SageMaker User Profile** product.

![Alt Step 4](assets/step4.jpg?raw=true "Step 4")

7. Provide the Studio User Profile name along with the SageMaker domain ID in the parameters section. Then hit the Product Launch button.

![Alt Step 5](assets/step5.jpg?raw=true "Step 5")
