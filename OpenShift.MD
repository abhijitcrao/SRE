# Let's Explore the way we can Monitor OpenShift Infra via Geneos

Prep work:
- We are using _OCI CLI_ command line i.e. OC commands to interact and share the output to Geneos.
- To work we need a communication link between your OC commandline host to OpenShift Infra, usually this will be your UAT or lower Environment
- Once you have host identified, kindly download the _OC cli_ on this host and try testing basic OC commands
- To connect to OpenShift project's you need to copy **Login Command** from _OpenShift Console_
** We recommend to use service account for OCI command line interaction as it's token doesn't expire **
- Once you try using oc login with token an entry is made under your user home dir under folder .kube/config
- For script to run without userid each time, edit the _config_ under _.kube_ and enter userid and token details.

PFB the basic command line's that can be used to interact and share output back to Geneos

Get Quota Details of the project

_**oc get quota | sed -r 's/ {2,}/,g' | cut -d ',' -f-4**_

Get Deployment Descriptor of project

_**oc get deployment | sed -r 's/ {2,}/,g'**_

Get POD details along with Restart counters

_**oc get pods -o wide | sed -r 's/ {2,}/,g**_

Get Events (this is important to know the current operations going on under OpenShift)

_**oc get event -o wide  | sed -r 's/ {2,}/,g'**_

Sample script can be created here so to make it more useful

`````#!/bin/bash
#Name: <scriptName>
#author: Abhijit Rao
#Useage:

#We will be passing parameter for the OC commands here
object=$1
#we are checking here if the request is for Quota 
if [[$1 == "quota"]]
then
    oc get quota | sed -r 's/ {2,}/,g' | cut -d ',' -f-4
elseif [[ $1 =="deployment" ]]
then
    oc get deployment | sed -r 's/ {2,}/,g'
else
    oc get $object | sed -r 's/ {2,}/,g'
fi`````
