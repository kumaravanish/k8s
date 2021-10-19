Problem 1: Flawed Authorisation Model
 * Granting permissions to the user is intuitive but breaks the controllers.Generally psp is written to keep pods in the mind but no one runs pod directly.
 * Dual Mode weakens security, if someone (cluster admin) provides clusteradmin role with "privileged PSP" (human error) binds through RBAC (rolebinding) to a namespace.
 * Privileged pod can screw up another pod in another namespace.

Problem 2: Difficult to Rollout
* Since this is an admission controller each and every pod will need a policy definition to get scheduled.
  No PSPs means all pods are denied.
* PSPs cannot be enabled by default, user need to add PSP for all the workloads before enabling the feature.There is no audit mode (Bootstrap policy.)

Problem 3: Inconsistent API.
* 2 or more policies to a single user/service/pod can be assigned which often results in privileges esclations.
* Weak prioritisation model which is based on alphabetical order. (Sometime apiserver updates results in unexpected results)
* Many niche usecase requests not supported. Example: No provision to have a policy based labels,scheduling,fine grained volume controls etc.
* Needs understanding of linux security primitives. Example Capabilities.
* Lastly API grown organically with lots of inconsistency which will be difficult to maintain.
