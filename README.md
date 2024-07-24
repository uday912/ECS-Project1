** **ECS-Project1** **

**Project:** DEPLOYING WEB APPLICATION ON ECS WITH EC2, DOCKER, ECR ALONG WITH LOAD BALANCER

**STEPS TO FOLLOW:**
    **PRE-REQUISITES:-**
          --> AWS EC2 INSTALLATION SETUP
          
          --> DOCKER INSTALLATION
          
          --> ECR FOR STORING DOCKER IMAGE
          
          --> LOAD BALANCER TO CONTROL THE TRAFFIC
          
          --> FINALLY **ECS** FOR ORCHESTRATION AND PROVISIONING OF DOCKER CONTAINERS AND FOR HOST WEB APPLICATION

**EC2 INSTALLATION AND SETUP:**
    First and foremost login into aws account and then search for **ec2** on searchbar
    
      --> click on ec2
    
          --> on ec2 dashoard click on instances and then click on **LAUNCH INSTANCE**
          
               -->  SELECT AND ENTER THE REQUIRED DETAILS: 

                      --> NAME
                      
                      --> AMI
                      
                      --> INSTANCE TYPE
                      
                      --> KEY PAIR - SELECT EXISTING KEY PAIR IF HAVE ANY OR OTHERWISE CREATE A NEW ONE 

                      --> SELECT VPC AND SECURITY GROUPS EITHER DEFAULT ONE'S OR CREATE A NEW ONE'S

                      --> CONFIGURE THE STORAGE AS PER REQUIREMENT OR TAKE DEFAULT

THEN NAVIGATE TO TERMINAL EITHER GITBASH, PUTTY OR MOBAXTERM...

CONNECT WITH THE EC2 INSTANCE USING IP AND PEM KEY..

AFTER SETUP THE TERMINAL, RUN THR FOLLOWING COMMANDS FOR AWS CONFIGURATION AND INSTALLATION OF DOCKER

FOR AWS CONFIGURATION:

    FIRST INSTALL THE AWS CLI, FOR THAT WE NEED, 
    
      **COMMANDS:**
      
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install

   THEN RUN **aws configure**

      FOR AWS CONFIGURATION, WE NEED ACCESS KEY AND SECRET ACCESS KEY ID: FOR THAT

             SEARCH FOR ** IAM ** ON SEARCH BAR
                
                 --> NAVIAGATE TO IAM PAGE AND ON LEFT HAND SIDE THERE IS OPTION CALLED "USER"

                     --> CLICK ON USER AND CREATE A USER IF YOU DON'T HAVE ANY 

                        -->CLICK ON SECURITY CREDENTIALS 

                        --> ON ACCESS KEYS

                          --> CREATE ACCESS KEY

      AFTER CREATING THE KEYS, NAVIAGATE TO TERMINAL AND RUN AWS CONFIGURE COMMAND AND THERE COPY AND PASTE THE ACCESS KEY AND SECRET ACCESS KEY AND REGION TOO.

    **INSTALL THE DOCKER:**

        --> curl -fsSL https://get.docker.com -o get-docker.sh

        --> sudo apt/yum install docker -y

        --> docker --version - to check for the docker version
        

     **ECR SETUP ON AWS:**

      SEARCH FOR ECR:
          
          CLICK ON ELASTIC CONTAINER REGISTRY

             CLICK ON CREATE 

               --> SELECT EITHER PRIVATE OR PUBLIC REPOSITORY OPTION

                 --> FILL THE REPOSITORY NAME

                   --> CLICK ON CREATE REPOSITORY

        AFTER CREATION OF REPO AND ON CREATED REPO DASHBOARD YOU HAVE OPTION CALLED "VIEW PUSH COMMANDS" ON TOP

               FOR AUTHENTICATION AND FOR PUSH THE IMAGES TO ECR WE NEED PERMISSIONS, FOR THAT WE NEED TO CREATE IAM ROLE

              --> NAVIGATE TO IAM 

                  --> CLICK ON ROLE ON LEFT SIDE 

                     --> CREATE A ROLE 

                       -- NAME 

                         -- SELECT REQUIRED ENTITY TYPE {AWS  SERVICE}

                           -- SELECT USE CASE {EC2}

                                  -- ATTACH THE PERMISSION POLICIES AS PER REQUIREMENT AND FINALLY CREATE THE ROLE

       AFTER CREATION, WE NEED TO LOGIN TO ECR FROM AWS CLI, FOR THAT

            NAVIGATE TO ECR, 
                
                -- CLICK ON VIEW PUSH COMMANDS 

                   FROM THERE COPY AND PASTE THE 

                         -- AUTHENTICATE TOKEN COMMAND 

                         -- DOCKER TAG COMMAND AND DOCKER PUSH COMMAND 


        AFTER THAT WE NEED TO CREATE A LOAD BALANCER FOR BETTER ROUTING TRAFFIC ;

             NAVIGATE TO EC2 PAGE 

                 CLICK ON LOAD BALANCING --> LOAD BALANCERS 

                     -- CREATE A LOAD BALANCER

                        -- SELECT THE LOAD BALANCER TYPE [APPLICATION LOAD BALANCER, NETWORK LOAD BALANCER, GATEWAY LOAD BALANCER]

                             FILL AND SELECT THE REQUIRED OPTIONS:

                                 -- LOADBALANCER NAME

                                 -- NETWORK MAPPING

                                      --> VPC
                                      
                                      --> SUBNETS
                                      
                                 -- SECURITY GROUPS 

                                 -- LISTNERS AND ROUTING 

                                     IN LISTNERS 

                                         --> CREATE A TARGET GROUP 

                                                -- CHOOSE TARGET TYPE

                                                -- TARGET GROUP NAME 

                                                -- SELECT THE VPC AS PER REQUIREMENT


** ECS SETUP FOR WEB APPLICATION: **

            SEARCH FOR ECS

                -- NAVIGATE TO ECS DASHBOARD

                   --> CLICK ON TASK DEFINITIONS ON LEFT SIDE 

                       --> CREATE A NEW TASK DEFINITION

                           --> FILL THE DETAILS:

                                -- TASK FAMILY NAME

                                -- INFRASTRUCTURE REQUIREMENTS:

                                     -- LAUNCH TYPE : HERE WE USE "FARGATE" - IT'S A SERVERLESS COMPUTE FOR CONTAINERS                                                

                                -- TASK DEFINITION ROLE - A task execution IAM role is used by the container agent to make AWS API requests.

                                      -- CREATE A NEW IAM ROLE AND ATTACH POLICIES THAT IS REQUIRED 

                                                 -- ROLE: POLICIES:- "AMAZONECS TAKE EXECUTION ROLE POLICY"
                                                 
                    --> NAVIGATE AND CLICK ON "CONTAINER SECTION"

                          --> NAME 

                          --> IMAGE URI - COPY AND PASTE THE ECR REPOSITORY URI THAT IS CREATED ON ECR

                   REST OF OPTIONS LEAVE IT AS DEFAULT ONE'S 

                   ** FINALLY TASK DEFINITION IS CREATED....


        ** NAVIGATE TO CLUSTER OPTION ON ECS DASHBOARD:

            --> CLICK ON CREATE CLUSTER

                -- CLUSTER NAME 

                -- INFRASTRUTURE 

                    -- AWS FARGATE- SERVERLESS

             CREATE A CLUSTER....

                THEN NAVIGATE TO CREATED CLUSTER AND AT DOWN HAVE AN OPTION CALLED " SERVICE- MAINTAIN THE EC2 INSTANCES "

                      -- CLICK ON " SERVICE "

                            -- CLICK ON CREATE 

                                 --> SELECT THE TASK DEFINITION- WHICH WE ARE CREATED 

                                 --> SERVICE NAME -

                                 --> DESIRED TASK - 

             
                      -- NETWORKING 

                            --> VPC

                            --> SUBNETS

                            --> SECURITY GROUPS- CREATE A NEW ONE IF REQUIRED:

                                                  -- NAME

                                                  -- TYPE
                       
                       -- LOAD BALANCING 

                          --> SELECT EXISTING CREATED LOAD BALANCER {ALB}

                          --> TARGET GROUP

                             -- NAME 

                             -- PROTOCOL

                             -- EVALUATION ORDER


                        -- AUTO-SCALING 

                          --> DEFAULT ONE 

       AFTER THE SERVICE IS CREATED, NAVIAGATE TO THE SERVICE WHICH IS CREATED AND THERE WE CAN CHECK FOR LOGS, NETWORKING, CONFIGURATION, MONITORING AND HEALTH CHECKS... 
                         
                       
                          

                                
                     


                                  

        
      
          
             

          
          
          
               
                           

          
