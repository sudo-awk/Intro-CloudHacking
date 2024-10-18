## Level 5
url: http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/
<kbd>
![image](https://github.com/user-attachments/assets/ff87639d-72f3-41d7-9a2d-ec12ebd99fc8)
</kbd>
Lab says that the level 6 link can be accessed when we used a proxy, we checked the level 6 link first and sure enough we get access denied
<kbd>
![image](https://github.com/user-attachments/assets/5f8ff2ea-d531-4221-9ca1-d53b90bd027f)
</kbd>
If you notice all three links have a directory `proxy` in it

>- http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/flaws.cloud/
>- http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/summitroute.com/blog/feed.xml
>- http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/neverssl.com/
>
If we  play around with it, the `proxy` redirects us to the a different location, to confirm, notice the results of icanhazip.com it results to my ip, 

![image](https://github.com/user-attachments/assets/bcb95ce7-c823-4484-9828-6e3b5149b34f)

Then we will use this the icanhazip again this time using the our target. 

Notice that the IP address of the target is the one that showed up, this is like a server side request forgery (SSRF) we can issue make commands via the server

![image](https://github.com/user-attachments/assets/f6d0d92f-06c6-4339-972d-f6e4c5f68a35)

With this vulnerability in mind, Aws,Gcp and azure uses the ip address 169.254.169.254 (Magic IP) as their metadata intance address and should only be accessible using the server.

![image](https://github.com/user-attachments/assets/c9b93321-a6a4-455e-aa97-649e59e5eb64)

You can read more about the instances here if you want 


https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html

Since we have access to their server, if they did not disable the ipv4 access, we can get request for the intance using this server.

After trying the said Magic IP we are able to list the instance metadata 

`http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/169.254.169.254/`

<kbd>
![image](https://github.com/user-attachments/assets/aff90250-a6c4-4639-90ff-1be8e50d520b)
</kbd>
And enumerating this vulnerability we found more access to the target 


![image](https://github.com/user-attachments/assets/270e179b-b097-449b-9aad-6a71735f7c70)

