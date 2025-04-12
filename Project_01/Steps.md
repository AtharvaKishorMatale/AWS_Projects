#Project 1: Static Website Hosting using S3,Route 53&CloudFront

In this project, I hosted a static website on AWS using S3, Route 53, and CloudFront. This project helped me understand how static websites work and how AWS services can be used to make websites fast and available all over the world.

#What I Did in This Project:
I created a basic website using HTML and CSS. Then, I hosted it using AWS S3. To connect my domain name to the website, I used Route 53. I also used CloudFront to improve speed and performance of the website.

#Technologies Used:

Amazon S3–for storing and hosting the website files
Route 53–for domain name management
CloudFront–for fast and secure content delivery

#Step-by-Step Process (Performed by Me)

#1.Created an S3 Bucket for Hosting Website
-I went to the S3 service in my AWS account.
-Clicked "Create bucket".
-Gave the bucket a name. Since I was using a domain, I named the bucket exactly like my domain name (i.e-justfacebook.com).
-Chose the AWSRegion close to me.
-Unselected the option "Block all public access" because I wanted my website to be public.
-Clicked on Create bucket.

#2.Enabled Static Website Hosting in the Bucket
-After creating the bucket, I opened it and went to the Properties tab.
-Scrolled to Static website hosting and clicked Edit.
-Selected “Enable”, then chose “Host a static website”.
-Set index.html as the Index document.
-Saved the changes.

#3.Uploaded My Website Files
-I clicked on the bucket, then went to the Objects tab.
-Clicked Upload, then added my index.html and style.css files.
-Uploaded the files.
-Made sure both files were public, so they could load in the browser.

#4.Set Up Route 53 to Link My Domain
-I opened Route 53 and created a Hosted Zone for my domain.
-Added an A record that pointed to my S3 website endpoint.
-If I got the domain from another website like GoDaddy, I changed its settings there to use the Route 53 servers.

#5.Added CloudFront to Speed Up the Website
-I opened the CloudFront service and created a new Distribution.
-Selected my S3 bucket as the origin.
-Enabled HTTPS by choosing Redirect HTTP to HTTPS.
-Entered index.html as the root object.
-Added my domain in Alternate domain name (CNAME).
-After a few minutes, the distribution was active and I could use the CloudFront URL to access my website quickly and securely.
