Demo environment preperation for Opeshift Virtualization 

Here for demo purposes we are going to deploy virtual machine side by side with containers, take advantage of having Red Hat Openshift Platform, ip addresses , storage, load balancer will be handled by the platform itself.  

We are going to deploy a guestbook application as frontend, in the backend it uses Redis. Redis server is two tier, Redis leader is running in a virtual machine, Redis followers running as containers. 

Prerequisites
- Running Red Hat Openshift Platform 
- On baremetal or nested virtualization enabled if running on virtual environment
- ReadWriteMany storage backend
- Openshift Virtualization enabled, https://docs.openshift.com/container-platform/4.4/cnv/cnv_install/installing-container-native-virtualization.html 


First we need to upload Operating System qcow image file to Red Hat Openshift Platform, so easily we can clone filesystem to have running Virtual Machines. We need a ReadWriteMany storage backend, here I used Red Hat Openshift Container Storage. 

Guestbooktemplate.yaml create template. You can order guestbook application under  Developer →  Add → From  Catalog → Search  in Red Hat Openshift web interface. 


   ```sh

   # oc new-project guestbook 
   # curl -OLJ  https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2
   # virtctl  image-upload --image-path=CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2 --pvc-name=centos8 --access-mode=ReadWriteMany --pvc-size=11G --wait-secs=1800  --insecure --uploadproxy-url https://cdi-uploadproxy-openshift-cnv.apps.as4xy.lp.int
   # oc create -f centosdv.yaml 
   # oc create -f guestbooktemplate.yaml

   ```

Check logs of redis follower, be sure that sync started with redis leader. 
Get the route of guestbook application 

   ```sh
   
   # oc logs -f redisXXXX 
   # oc get route -n guestbook
   
   ```
   
