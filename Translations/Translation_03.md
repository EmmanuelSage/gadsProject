# Console and Cloud Shell

## Objectives:
In this lab, you will learn how to perform the following tasks:

- Get access to Google Cloud.

- Create a Cloud Storage bucket using the Cloud Console.

- Create a Cloud Storage bucket using Cloud Shell.

- Become familiar with Cloud Shell features.


## Task 1: Create a bucket using the Cloud Console

Here we create a bucket using

```sh
	gsutil mb gs://<BUCKET_NAME>
 ```

- Ensure <BUCKET_NAME> is a globally unique bucket name


## Task 2: Access Cloud Shell

- This has no commands and basically gives you some background on cloud shell

## Task 3: Create a bucket using Cloud Shell

1. Use the gsutil command to create another bucket. Replace <BUCKET_NAME> with a globally unique name (you can append a 2 to the globally unique bucket name you used previously):

```sh
gsutil mb gs://<BUCKET_NAME>
```

## Task 4: Explore more Cloud Shell features

1. Here we experiment with uploading a file and moving into one of the buckets we created. Ensure the file is in the same directory then run

```sh
gsutil cp [MY_FILE] gs://[BUCKET_NAME]
```

## Task 5: Create a persistent state in Cloud Shell

1. To list available regions, execute the following command:

```sh
gcloud compute regions list
```

2. Select a region from the list and note the value in any text editor. This region will now be referred to as [YOUR_REGION] in the remainder of the lab

### Create and verify an environment variable

1. Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:

```sh
INFRACLASS_REGION=[YOUR_REGION]
```

2. Verify it with echo:
```sh
echo $INFRACLASS_REGION
```

### Append the environment variable to a file

1. Create a subdirectory for materials used in this class:

```sh
mkdir infraclass
```

2. Create a file called `config` in the infraclass directory:

```sh
touch infraclass/config
```

3. Append the value of your Region environment variable to the `config` file:

```sh
echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
```

4. Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the Cloud Console Home page.

```sh
INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID]
```

5. Append the value of your Project ID environment variable to the `config` file:

```sh
echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config
```

6. Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

```
source infraclass/config
```

```sh
echo $INFRACLASS_PROJECT_ID
```

7. Close and re-open Cloud Shell. Then issue the echo command again:

```sh
echo $INFRACLASS_PROJECT_ID
```
- There will be no output because the environment variable no longer exists.

### Modify the bash profile and create persistence

1. Edit the shell profile with the following command:

```sh
nano .profile
```

2. Add the following line to the end of the file:

```sh
source infraclass/config
```

3. Press Ctrl+O, ENTER to save the file, and then press Ctrl+X to exit nano.

4. Use the echo command to verify that the variable is still set:

```sh
echo $INFRACLASS_PROJECT_ID
```
- You should now see the expected value that you set in the config file.


[Return to Readme](../README.md)