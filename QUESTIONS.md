# ArgoCD: GitOps at Scale Questions

#### What is the Apps of Apps pattern?
* A way to group multiple Argo CD applications together

#### How does the Apps of Apps pattern work?
* You create an Argo CD application that points to other applications

#### Where should you deploy an Argo CD application manifest?
* In the same namespace that Argo CD is installed on

#### If you define “self-heal” for a root application that contains other applications...
* Self-heal is enabled only for the parent app

#### How can you use the Apps of Apps pattern?
* For grouping multiple apps together
* For cluster bootstrapping
* For automated application creation via git monitoring

#### How does Argo CD manage Kubernetes clusters?
* You need to install an Argo CD instance on every deployment cluster
* You need a central Argo CD instance that manages all your clusters
* You need multiple Argo CD instances that manage subsets of your clusters

#### When you add an external cluster in Argo CD
* You need a context for the target cluster and the CLI authenticated to the management cluster

#### When you add an external/target cluster in Argo CD...
* The management cluster needs network access to the target cluster

#### It's possible to add an external cluster to Argo CD
* Using the CLI

#### What is the relationship between Application Sets and Apps of Apps?
* Both approaches are independent of each other

#### Can you use Application Sets with App of Apps applications?
* Yes, they can be combined with no limitations

#### For what scenarios can you use Application Sets?
* For installing multiple instances of an application to multiple clusters
* For installing multiple applications on a single cluster
* For installing multiple applications to multiple clusters

#### How do Application Sets work?
* Application Sets are generators for Argo CD applications

#### What source can be used for Application Sets?
* A hardcoded list of applications
* A dynamic list of applications stored in git folders
* A dynamic list of applications defined in Github Pull Requests

#### How can you combine Application Set Generators?
* By using a matrix generator

#### You want an Argo CD application to be deployed as soon as somebody creates a new Github repository with manifests.Which ApplicationSet generator should be used?
* SCM provider Generator

#### You have lots of applications in a single Git repository under c/infra/apps/&lt;app-name&gt;d. The correct ApplicationSet generator to use is
* Git Generator

#### You want to create temporary environments for developers while they create new features on different branches. The correct ApplicationSet generator to use is
* Pull Request Generator

#### How can you model different GitOps environments?
* Use a branch for each environment
* Use a folder for each environment
* Use a git repository for each environment

#### How does Argo Image Updater work?
* It monitors Docker registries for new containers

#### You have a cstagingd container tag that should always be deployed to a staging environment as soon as somebody updates it. The appropriate Argo Image updater strategy is
* digest

#### You have a production environment that gets container images with tags that match only 1.x version. The appropriate Argo Image updater strategy is
* semver

#### You have an application managed by Argo Image Updater with the csemverd strategy. The current image is tagged c1.4d with a constraint to c1.xd releases. You build a new image and push it with tag 1.2.7. This new container
* will not be deployed because 1.4 is newer

#### An Argo CD hook that runs in the PreSync phase has an error and fails. Argo CD will
* Abort the deployment

#### Resource A is marked with Sync wave -1 and Resource B is marked with wave 5.
* We need to check for sync phases before we can answer

#### Argo CD will mark an application as Failed if...
* Any hook fails regardless of its phase

#### If a hook in the SyncFail phase has an error, Argo CD
* will abort the deployment and mark it as failed

#### If a hook in the PostSync phase has an error, Argo CD
* will abort the deployment and mark it as failed

#### Resource A is in the Sync phase and has no Sync wave. Resource B is in the Sync phase and has Sync wave 0
* A and B will be deployed according to the default Resource ordering

#### Can you use sync waves to replace sync phases?
* Yes, but only if you don9t need the SyncFail mechanism

#### What is the relationship between Sync Waves and phases?
* Sync waves and phases can be used on their own or both at once

#### Resource A is in the PreSync phase and Sync wave 10. Resource B is in the Sync phase and has Sync wave 20. Resource C is in the SyncFail phase with sync wave 30
* C will be deployed only if B fails to deploy

#### Resource A is in the PostSync phase and has Sync wave 5. Resource B is in the PostSync phase and has Sync Wave 5. Resource C is in the PostSync phase and has Sync Wave -10
* C will be deployed first and then A and B will be deployed according to default Resource order

#### Resource A is in the PreSync phase with Sync wave 50. Resource B is in the SyncFail phase with Sync Wave -50. Resource C is in the PostSync phase with wave -99
* Resource A will be deployed first, then Resource B (if applicable). Resource C will be deployed last

#### Resource A is in the PreSync phase with Sync wave 50. Resource B is in the Sync phase with Sync Wave -10. Resource C is in the PostSync phase with wave 50
* Resource A will be deployed first then Resource B and finally Resource C

#### When do you need to ignore differences in Argo CD resources?
* When an application has values that should be dynamically modified after manifests are applied.

#### What are Sync Windows used for?
* To disable/enable application deployments for different time periods

#### An application has an callowd sync window for 5pm to 6pm. The time is now 7pm
* You cannot deploy the application because no callowd window is active

#### An application has a cdenyd sync window for 5pm to 6pm. The time is now 7pm
* You can deploy the application because no cdenyd window is active

#### An application has a cdenyd sync window for 5pm to 8pm and an callowd sync window from 6pm to 9pm. The time is now 7pm
* You cannot deploy the application, cdenyd windows override callowd windows

#### An application has a cdenyd sync window for 5pm to 7 pm, an callowd sync window from 4pm to 8pm. The time is now 6pm
* You cannot deploy the application, cdenyd windows override callowd windows

#### An application has a cdenyd sync window for 5pm to 7 pm, an callowd sync window from 4pm to 7pm and an callowd window from 5:30 to 6:30pm. The time is now 6pm
* You cannot deploy the application, cdenyd windows override callowd windows

#### What is the best way according to the GitOps principles to update the container of an application
* Use your CI system to commit a change in the manifest stored in the git repository

#### What is the major disadvantage of disabling cself-heald in an application
* Manual changes in the cluster will no longer be detected and discarded

#### What is the major advantage of using folders as GitOps environments?
* You can promote any change from any environment to any other environment
* The order of commits is no longer relevant for environment promotions
* Handling a large number of environments always results in managing a single git branch

#### What is the major disadvantage of using folders as GitOps environments?
* It is difficult to secure individual folders in a single git repository

#### What is the major advantage of using branches as GitOps environments?
* Developers are already familiar with how git tools work

#### What is the major disadvantage of using branches as GitOps environments?
* Order of commits affects every promotion done by merging

#### What is the best way of modeling your GitOps environments?
* It depends according to the assumptions and limitations of your organization
#### 
