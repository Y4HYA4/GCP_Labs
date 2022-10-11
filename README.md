# Create and Manage Cloud Resources: Challenge Lab
Hey, so here are the commands I made to complete this Google Cloud Lab.
<br>
You can find this and more in https://www.cloudskillsboost.google/

# Task 1
For the first, I strongly advise you to select everything from the UI to obtain the full gcloud command. The entire lab is designed to familiarize you with the command line. Create your essay by creating this simple elastic compute configuration. and conclude the remaining tasks solely through the use of the Google terminal. <br>
**Name of instance:** nucleus-jumphost-161

```
gcloud compute instances create nucleus-jumphost-161 \
          --network nucleus-vpc \
          --zone us-east1-b  \
          --machine-type f1-micro  \
          --image-project debian-cloud \
          --scopes cloud-platform \
          --no-address
```
Tried this one but didnt work.
`gcloud compute instances create nucleus-jumphost-161 --zone=us-east1-b" --machine-type="f1-micro" --boot-disk-size=10GB `

I ended up doing it through the platform UI and then using the Google command snipet in cloudshell.

# Task2
----
`gcloud config set compute/zone us-east1-b`

----

`gcloud container clusters create nucleus-webserver1`

----

`gcloud container clusters get-credentials nucleus-webserver1`


---

`kubectl create deployment hello-app --image=gcr.io/google-samples/hello-app:2.0`

---

`kubectl expose deployment hello-app --type=LoadBalancer --port 8080`


---

`kubectl get service `





# Task 3

Update packages.

-----

`gcloud compute instance-templates create nginx-template --metadata-from-file startup-script=startup.sh`

---

`gcloud compute target-pools create nginx-pool --region=us-east1`

----

`gcloud compute instance-groups managed create nginx-group --base-instance-name nginx --size 2 --template nginx-template --target-pool nginx-pool`

----
`gcloud compute firewall-rules create accept-tcp-rule-826 --allow tcp:80`

----

`gcloud compute forwarding-rules create nginx-lb --region us-east1 --ports=80 --target-pool nginx-pool `


---


`gcloud compute http-health-checks create http-basic-check`

---


`gcloud compute instance-groups managed set-named-ports nginx-group --named-ports http:80`

---


`gcloud compute backend-services create nginx-backend --protocol HTTP --http-health-checks http-basic-check --global`

---

`gcloud compute backend-services add-backend nginx-backend --instance-group nginx-group --instance-group-zone us-east1-b --global `

---


`gcloud compute url-maps create web-map --default-service nginx-backend`


----

`gcloud compute target-http-proxies create http-lb-proxy --url-map web-map`


---

`gcloud compute forwarding-rules create http-content-rule --global --target-http-proxy http-lb-proxy --ports 80`









