# How to ci/cd gitlab with s3?

## Create New Bucket
  

+ step 1: create bucket, uncheck block all

+ step 2: navigate to properties, enable static web hosting

+ step 3: add index.html

+ step 4: edit bucket policy

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadGetObject",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::<YOUR_BUCKET>/*”
		}
	]
}
```
+ step 5: save
## Upload manual

+ step 1: click **Upload** button 
+ step 2: upload all file in build/dist folder 
+ step 3: check link

## ## Set up OpenID Connect in AWS
+ step 1: go to **IAM**
+ step 2: under **Access management** choose **Identity providers**  
+ step 3: choose **Add provider**
+ step 4: select **OpenID Connect**.
+ step 5: For **Provider URL**, enter the address of your GitLab instance, such as `https://gitlab.com` or `https://gitlab.example.com`.

## Create Policy in IAM
+ create Policy with bellow json
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::jw-gl-react"]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject"
      ],
      "Resource": ["arn:aws:s3:::vntel-react-cicd/*"]
    }
  ]
}
```

## Create Role IAM

+ step 1: under  **Access management**  select  **Roles**  
+ step 2: select  **Create role**. Select  **Web identity**.

+ step 3: In the  **Web identity**  section, select the identity provider you created earlier.
+ step 4: in the  **Audience**, select the audience you created earlier.
+ step 5: Select the  **Next**  button to continue.
+ step 6: During the  **Add permissions**  step, select the policy you created and select  **Next**  to continue. Give your role a name and click  **Create role**

## Add gitlab-ci.yml

+ step 1: create ```.gitlab-ci.yml``` in your project
+ step 2: copy from ```sample.yml``` to your ```.gitlab-ci.yml``` 
