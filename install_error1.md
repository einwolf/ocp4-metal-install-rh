# Error preventing install completion 1

openshift-install wait-for install-complete times out and errors

It goes to 95%+ installed but console and authentication never finish.
Control plane and workers setup ok otherwise. oc get nodes shows them.
This includes creating and approving certificates.

## Transcript

```bash
# openshift-install wait-for install-complete times out and errors
./openshift-install --dir ./ocp-install1 wait-for install-complete --log-level=debug

# Fails because console and authentication never finish
DEBUG OpenShift Installer 4.13.5                   
DEBUG Built from commit 953477ffa0d19ef8a995258042af8099300a2385 
DEBUG Loading Install Config...                    
DEBUG   Loading SSH Key...                         
DEBUG   Loading Base Domain...                     
DEBUG     Loading Platform...                      
DEBUG   Loading Cluster Name...                    
DEBUG     Loading Base Domain...                   
DEBUG     Loading Platform...                      
DEBUG   Loading Networking...                      
DEBUG     Loading Platform...                      
DEBUG   Loading Pull Secret...                     
DEBUG   Loading Platform...                        
DEBUG Using Install Config loaded from state file  
DEBUG Loading Agent Config...                      
INFO Waiting up to 40m0s (until 5:31PM) for the cluster at https://api.lab.ocp.lan:6443 to initialize... 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 541 of 842 done (64% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 779 of 842 done (92% complete) 
DEBUG Still waiting for the cluster to initialize: Multiple errors are preventing progress: 
DEBUG * Cluster operators authentication, console, image-registry, ingress, insights, monitoring, openshift-controller-manager, openshift-samples are not available 
DEBUG * Could not update role "openshift-console-operator/prometheus-k8s" (759 of 842): resource may have been deleted 
DEBUG * Could not update role "openshift-console/prometheus-k8s" (762 of 842): resource may have been deleted 
DEBUG Still waiting for the cluster to initialize: Multiple errors are preventing progress: 
DEBUG * Cluster operators authentication, console, image-registry, ingress, insights, monitoring, openshift-controller-manager, openshift-samples are not available 
DEBUG * Could not update role "openshift-console-operator/prometheus-k8s" (759 of 842): resource may have been deleted 
DEBUG * Could not update role "openshift-console/prometheus-k8s" (762 of 842): resource may have been deleted 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 2 of 842 done (0% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 17 of 842 done (2% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 52 of 842 done (6% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 64 of 842 done (7% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 65 of 842 done (7% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 607 of 842 done (72% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 607 of 842 done (72% complete) 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console, insights, monitoring are not available 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console, insights are not available 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console are not available 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console are not available 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 11 of 842 done (1% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 53 of 842 done (6% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 54 of 842 done (6% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 612 of 842 done (72% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 613 of 842 done (72% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 614 of 842 done (72% complete) 
DEBUG Still waiting for the cluster to initialize: Working towards 4.13.5: 616 of 842 done (73% complete) 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console are not available 
DEBUG Still waiting for the cluster to initialize: Cluster operators authentication, console are not available 
ERROR Cluster operator authentication Degraded is True with OAuthServerRouteEndpointAccessibleController_SyncError: OAuthServerRouteEndpointAccessibleControllerDegraded: Get "https://oauth-openshift.apps.lab.ocp.lan/healthz": EOF 
ERROR Cluster operator authentication Available is False with OAuthServerRouteEndpointAccessibleController_EndpointUnavailable: OAuthServerRouteEndpointAccessibleControllerAvailable: Get "https://oauth-openshift.apps.lab.ocp.lan/healthz": EOF 
INFO Cluster operator baremetal Disabled is False with :  
INFO Cluster operator cloud-controller-manager CloudConfigControllerAvailable is True with AsExpected: Cloud Config Controller works as expected 
INFO Cluster operator cloud-controller-manager CloudConfigControllerDegraded is False with AsExpected: Cloud Config Controller works as expected 
INFO Cluster operator cloud-controller-manager TrustedCABundleControllerControllerAvailable is True with AsExpected: Trusted CA Bundle Controller works as expected 
INFO Cluster operator cloud-controller-manager TrustedCABundleControllerControllerDegraded is False with AsExpected: Trusted CA Bundle Controller works as expected 
INFO Cluster operator console Progressing is True with SyncLoopRefresh_InProgress: SyncLoopRefreshProgressing: Working toward version 4.13.5, 0 replicas available 
ERROR Cluster operator console Available is False with Deployment_InsufficientReplicas::RouteHealth_FailedGet: DeploymentAvailable: 0 replicas available for console deployment 
ERROR RouteHealthAvailable: failed to GET route (https://console-openshift-console.apps.lab.ocp.lan): Get "https://console-openshift-console.apps.lab.ocp.lan": EOF 
INFO Cluster operator etcd RecentBackup is Unknown with ControllerStarted: The etcd backup controller is starting, and will decide if recent backups are available or if a backup is required 
ERROR Cluster operator ingress Degraded is True with IngressDegraded: The "default" ingress controller reports Degraded=True: DegradedConditions: One or more other status conditions indicate a degraded state: CanaryChecksSucceeding=False (CanaryChecksRepetitiveFailures: Canary route checks for the default ingress controller are failing) 
INFO Cluster operator ingress EvaluationConditionsDetected is False with AsExpected:  
INFO Cluster operator insights ClusterTransferAvailable is False with NoClusterTransfer: no available cluster transfer 
INFO Cluster operator insights Disabled is False with AsExpected:  
INFO Cluster operator insights SCAAvailable is False with NotFound: Failed to pull SCA certs from https://api.openshift.com/api/accounts_mgmt/v1/certificates: OCM API https://api.openshift.com/api/accounts_mgmt/v1/certificates returned HTTP 404: {"code":"ACCT-MGMT-7","href":"/api/accounts_mgmt/v1/errors/7","id":"7","kind":"Error","operation_id":"9463dbba-412b-4d7a-9bc7-8e2ada42fe5f","reason":"The organization (id= 1hClIGEcOn5dvjdhMWOGRqhl78r) does not have any certificate of type sca. Enable SCA at https://access.redhat.com/management."} 
INFO Cluster operator network ManagementStateDegraded is False with :  
ERROR Cluster initialization failed because one or more operators are not functioning properly. 
ERROR The cluster should be accessible for troubleshooting as detailed in the documentation linked below, 
ERROR https://docs.openshift.com/container-platform/latest/support/troubleshooting/troubleshooting-installations.html 
ERROR The 'wait-for install-complete' subcommand can then be used to continue the installation 
ERROR failed to initialize the cluster: Cluster operators authentication, console are not available 

# It looks like ingress is blocking console and authentication due to canary route failure
oc get co
NAME                                       VERSION   AVAILABLE   PROGRESSING   DEGRADED   SINCE   MESSAGE
authentication                             4.13.5    False       False         True       117m    OAuthServerRouteEndpointAccessibleControllerAvailable: Get "https://oauth-openshift.apps.lab.ocp.lan/healthz": EOF
baremetal                                  4.13.5    True        False         False      115m    
cloud-controller-manager                   4.13.5    True        False         False      119m    
cloud-credential                           4.13.5    True        False         False      119m    
cluster-autoscaler                         4.13.5    True        False         False      116m    
config-operator                            4.13.5    True        False         False      117m    
console                                    4.13.5    False       True          False      108m    DeploymentAvailable: 0 replicas available for console deployment...
control-plane-machine-set                  4.13.5    True        False         False      115m    
csi-snapshot-controller                    4.13.5    True        False         False      117m    
dns                                        4.13.5    True        False         False      115m    
etcd                                       4.13.5    True        False         False      115m    
image-registry                             4.13.5    True        False         False      106m    
ingress                                    4.13.5    True        False         True       111m    The "default" ingress controller reports Degraded=True: DegradedConditions: One or more other status conditions indicate a degraded state: CanaryChecksSucceeding=False (CanaryChecksRepetitiveFailures: Canary route checks for the default ingress controller are failing)
insights                                   4.13.5    True        False         False      103m    
kube-apiserver                             4.13.5    True        False         False      113m    
kube-controller-manager                    4.13.5    True        False         False      112m    
kube-scheduler                             4.13.5    True        False         False      113m    
kube-storage-version-migrator              4.13.5    True        False         False      117m    
machine-api                                4.13.5    True        False         False      116m    
machine-approver                           4.13.5    True        False         False      116m    
machine-config                             4.13.5    True        False         False      115m    
marketplace                                4.13.5    True        False         False      115m    
monitoring                                 4.13.5    True        False         False      104m    
network                                    4.13.5    True        False         False      117m    
node-tuning                                4.13.5    True        False         False      116m    
openshift-apiserver                        4.13.5    True        False         False      97m     
openshift-controller-manager               4.13.5    True        False         False      108m    
openshift-samples                          4.13.5    True        False         False      108m    
operator-lifecycle-manager                 4.13.5    True        False         False      116m    
operator-lifecycle-manager-catalog         4.13.5    True        False         False      117m    
operator-lifecycle-manager-packageserver   4.13.5    True        False         False      111m    
service-ca                                 4.13.5    True        False         False      117m    
storage                                    4.13.5    True        False         False      117m    

# The canary routes are getting an empty response.
# (lost event output)

# Reference
# Upgrade process fails in Openshift Container Platform 4 because the Ingress Operator failed: CanaryChecksRepetitiveFailures
# https://access.redhat.com/solutions/5891131
# Steps 1 and 2 pass
# Step 3 fails

# Resolution
# Delete route pods so they can be recreated

[localsysadmin@ocp-svc ocp-install]$ oc get co
NAME                                       VERSION   AVAILABLE   PROGRESSING   DEGRADED   SINCE   MESSAGE
authentication                             4.13.5    False       False         True       117m    OAuthServerRouteEndpointAccessibleControllerAvailable: Get "https://oauth-openshift.apps.lab.ocp.lan/healthz": EOF
baremetal                                  4.13.5    True        False         False      115m    
cloud-controller-manager                   4.13.5    True        False         False      119m    
cloud-credential                           4.13.5    True        False         False      119m    
cluster-autoscaler                         4.13.5    True        False         False      116m    
config-operator                            4.13.5    True        False         False      117m    
console                                    4.13.5    False       True          False      108m    DeploymentAvailable: 0 replicas available for console deployment...
control-plane-machine-set                  4.13.5    True        False         False      115m    
csi-snapshot-controller                    4.13.5    True        False         False      117m    
dns                                        4.13.5    True        False         False      115m    
etcd                                       4.13.5    True        False         False      115m    
image-registry                             4.13.5    True        False         False      106m    
ingress                                    4.13.5    True        False         True       111m    The "default" ingress controller reports Degraded=True: DegradedConditions: One or more other status conditions indicate a degraded state: CanaryChecksSucceeding=False (CanaryChecksRepetitiveFailures: Canary route checks for the default ingress controller are failing)
insights                                   4.13.5    True        False         False      103m    
kube-apiserver                             4.13.5    True        False         False      113m    
kube-controller-manager                    4.13.5    True        False         False      112m    
kube-scheduler                             4.13.5    True        False         False      113m    
kube-storage-version-migrator              4.13.5    True        False         False      117m    
machine-api                                4.13.5    True        False         False      116m    
machine-approver                           4.13.5    True        False         False      116m    
machine-config                             4.13.5    True        False         False      115m    
marketplace                                4.13.5    True        False         False      115m    
monitoring                                 4.13.5    True        False         False      104m    
network                                    4.13.5    True        False         False      117m    
node-tuning                                4.13.5    True        False         False      116m    
openshift-apiserver                        4.13.5    True        False         False      97m     
openshift-controller-manager               4.13.5    True        False         False      108m    
openshift-samples                          4.13.5    True        False         False      108m    
operator-lifecycle-manager                 4.13.5    True        False         False      116m    
operator-lifecycle-manager-catalog         4.13.5    True        False         False      117m    
operator-lifecycle-manager-packageserver   4.13.5    True        False         False      111m    
service-ca                                 4.13.5    True        False         False      117m    
storage                                    4.13.5    True        False         False      117m    

[localsysadmin@ocp-svc ocp-install]$ oc -n openshift-ingress get pods
NAME                              READY   STATUS    RESTARTS       AGE
router-default-57c57cdf5c-hr9tg   1/1     Running   1 (112m ago)   115m
router-default-57c57cdf5c-qz2ft   1/1     Running   1 (112m ago)   115m

[localsysadmin@ocp-svc ocp-install]$ oc -n openshift-ingress delete pod router-default-57c57cdf5c-hr9tg
pod "router-default-57c57cdf5c-hr9tg" deleted
^Z
[1]+  Stopped                 oc -n openshift-ingress delete pod router-default-57c57cdf5c-hr9tg

[localsysadmin@ocp-svc ocp-install]$ bg
[1]+ oc -n openshift-ingress delete pod router-default-57c57cdf5c-hr9tg &

[localsysadmin@ocp-svc ocp-install]$ oc -n openshift-ingress delete pod router-default-57c57cdf5c-qz2ft
pod "router-default-57c57cdf5c-qz2ft" deleted
^Z
[2]+  Stopped                 oc -n openshift-ingress delete pod router-default-57c57cdf5c-qz2ft

[localsysadmin@ocp-svc ocp-install]$ bg
[2]+ oc -n openshift-ingress delete pod router-default-57c57cdf5c-qz2ft &

[localsysadmin@ocp-svc ocp-install]$ oc -n openshift-ingress get pods
NAME                              READY   STATUS        RESTARTS       AGE
router-default-57c57cdf5c-9vcsz   1/1     Running       0              45s
router-default-57c57cdf5c-hr9tg   0/1     Terminating   1 (113m ago)   116m
router-default-57c57cdf5c-qz2ft   1/1     Terminating   1 (113m ago)   116m
router-default-57c57cdf5c-tnszn   1/1     Running       0              21s

[localsysadmin@ocp-svc ocp-install]$ oc -n openshift-ingress get pods
NAME                              READY   STATUS    RESTARTS   AGE
router-default-57c57cdf5c-9vcsz   1/1     Running   0          74s
router-default-57c57cdf5c-tnszn   1/1     Running   0          50s
[1]-  Done                    oc -n openshift-ingress delete pod router-default-57c57cdf5c-hr9tg
[2]+  Done                    oc -n openshift-ingress delete pod router-default-57c57cdf5c-qz2ft

[localsysadmin@ocp-svc ocp-install]$ oc get co
NAME                                       VERSION   AVAILABLE   PROGRESSING   DEGRADED   SINCE   MESSAGE
authentication                             4.13.5    True        False         False      87s     
baremetal                                  4.13.5    True        False         False      118m    
cloud-controller-manager                   4.13.5    True        False         False      122m    
cloud-credential                           4.13.5    True        False         False      122m    
cluster-autoscaler                         4.13.5    True        False         False      118m    
config-operator                            4.13.5    True        False         False      120m    
console                                    4.13.5    True        False         False      79s     
control-plane-machine-set                  4.13.5    True        False         False      118m    
csi-snapshot-controller                    4.13.5    True        False         False      119m    
dns                                        4.13.5    True        False         False      117m    
etcd                                       4.13.5    True        False         False      117m    
image-registry                             4.13.5    True        False         False      109m    
ingress                                    4.13.5    True        False         False      62s     
insights                                   4.13.5    True        False         False      106m    
kube-apiserver                             4.13.5    True        False         False      116m    
kube-controller-manager                    4.13.5    True        False         False      115m    
kube-scheduler                             4.13.5    True        False         False      115m    
kube-storage-version-migrator              4.13.5    True        False         False      119m    
machine-api                                4.13.5    True        False         False      119m    
machine-approver                           4.13.5    True        False         False      119m    
machine-config                             4.13.5    True        False         False      117m    
marketplace                                4.13.5    True        False         False      117m    
monitoring                                 4.13.5    True        False         False      106m    
network                                    4.13.5    True        False         False      119m    
node-tuning                                4.13.5    True        False         False      118m    
openshift-apiserver                        4.13.5    True        False         False      100m    
openshift-controller-manager               4.13.5    True        False         False      111m    
openshift-samples                          4.13.5    True        False         False      111m    
operator-lifecycle-manager                 4.13.5    True        False         False      119m    
operator-lifecycle-manager-catalog         4.13.5    True        False         False      119m    
operator-lifecycle-manager-packageserver   4.13.5    True        False         False      114m    
service-ca                                 4.13.5    True        False         False      120m    
storage                                    4.13.5    True        False         False      120m    

```
