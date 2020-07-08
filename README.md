Demo environment preperation for Opeshift Virtualization 
Prerequisite
- Running Red Hat Openshift Platform 
- On baremetal or nested virtualization enabled if running on virtual enviornment
- ReadWriteMany storage
- Openshift Virtualization enabled https://docs.openshift.com/container-platform/4.4/cnv/cnv_install/installing-container-native-virtualization.html 

   ```sh

# oc new-project guestbook 
# cul -OLJ  https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2
# virtctl  image-upload --image-path=CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2 --pvc-name=centos8 --access-mode=ReadOnlyMany --pvc-size=11G --wait-secs=1800  --insecure --uploadproxy-url https://cdi-uploadproxy-openshift-cnv.apps.as4xy.lp.int
# oc create -f centosdv.yaml 
# oc create -f xxxxxx/guestbooktemplate.yaml

   ```
