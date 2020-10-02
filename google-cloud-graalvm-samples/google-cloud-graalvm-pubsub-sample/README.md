# Pub/Sub Sample Application with GraalVM

The Pub/Sub sample application demonstrates some common operations with Pub/Sub and is compatible with GraalVM compilation.

## Setup Instructions

1. If you have not already, [create a Google Cloud Platform Project](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project) and [enable the Pub/Sub APIs](https://console.cloud.google.com/apis/api/pubsub.googleapis.com).

2. Install the [Google Cloud SDK](https://cloud.google.com/sdk/) which will allow you to run the sample with your project's credentials.

    Once installed, log in with Application Default Credentials using the following command:
    
    ```
    gcloud auth application-default login
    ```
   
    **Note:** Authenticating with Application Default Credentials is convenient to use during development, but we recommend [alternate methods of authentication](https://cloud.google.com/docs/authentication/production) during production use.
    
3. Install the GraalVM compiler.
    
    You can follow the [official installation instructions](https://www.graalvm.org/docs/getting-started-with-graalvm/#install-graalvm) from the GraalVM website.
    After following the instructions, ensure that you install the Native Image extension installed by running:
    
    ```
    gu install native-image
    ```
   
    Once you finish following the instructions, verify that the default version of Java is set to the Graal version by running `java -version` in a terminal.
    
    You will see something similar to the below output:
    
    ```
    $ java -version
   
    openjdk version "11.0.7" 2020-04-14
    OpenJDK Runtime Environment GraalVM CE 20.1.0 (build 11.0.7+10-jvmci-20.1-b02)
    OpenJDK 64-Bit Server VM GraalVM CE 20.1.0 (build 11.0.7+10-jvmci-20.1-b02, mixed mode, sharing)
    ```

### Run with GraalVM Compilation

Navigate to this directory in a new terminal.

1. Compile the application using the GraalVM Compiler. This step may take a few minutes.

    ```
    mvn package -P graal
    ```
    
2. Run the application:

    ```
    ./target/com.example.pubsubsampleapplication
    ```

3. The application will create a new Pub/Sub topic, send and receive a message from it, and then delete the topic.

    ```
    Created topic: projects/YOUR_PROJECT_ID/topics/graal-pubsub-test-00e72640-4e36-4aff-84d2-13b7569b2289 under project: YOUR_PROJECT_ID
    Created pull subscription: projects/YOUR_PROJECT_ID/subscriptions/graal-pubsub-test-sub2fb5e3f3-cb26-439b-b88c-9cb0cfca9e45
    Published message with ID: 457327433078420
    Received Payload: Pub/Sub Graal Test published message at timestamp: 2020-09-23T19:45:42.746514Z
    Deleted topic projects/YOUR_PROJECT_ID/topics/graal-pubsub-test-00e72640-4e36-4aff-84d2-13b7569b2289
    Deleted subscription projects/YOUR_PROJECT_ID/subscriptions/graal-pubsub-test-sub2fb5e3f3-cb26-439b-b88c-9cb0cfca9e45
    ```