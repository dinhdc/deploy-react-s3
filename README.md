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
