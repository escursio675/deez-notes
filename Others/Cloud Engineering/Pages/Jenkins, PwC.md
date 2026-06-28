#personal 
Jenkins is one of the most popular CI/CD servers with great community support.
- Jenkins is built on Java. It is an open-source automation server
- The pipeline includes - continuous integrations, continuous delivery and continuous deployment
- CI/CD is preferred as opposed to nightly builds because it improves the development time by allowing for the early identification and resolution of errors
- A simply Jenkins workflow includes :
	- Commit Source Code
	- Jenkins triggers a build
	- Jenkins runs tests
	- Provides notifications to the developer
- The Jenkins CI server checks and pulls from the source code repository periodically, it then uses a build server to create an executable. A `.jar` file is created and any errors are sent to the developer. Deployment is then done to the test server. If all tests are passed, the application is moved to the production server.
- A Jenkins master-slave architecture can be used to run various pipelines from different codebases such as Node, Java etc.

# Using Jenkins Files
- The Jenkins pipeline description is store in Jenkins file
- The stages are build, test and deployment
- Global environment variables can be used that are accessible from anywhere in the pipeline
- Passwords and credentials can be store in environment variables

# Jenkins Pipeline
- Declarative and scripted syntaxes are used to create a Jenkins file
- Pipelines are durable, pausable, versatile and extensible
- Pipeline, Node, Stage and Step are important parts of the Jenkins Pipeline
- Pipeline is creating using Blue Ocean, Through Classic UI, or through SCM
- Env, Params and currentBuild are the default variables in pipeline

# Running Pipelines
- Multibranch helps in implementing different Jenkins files for different divisions of the same project

