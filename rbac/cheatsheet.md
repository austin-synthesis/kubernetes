## 🌱 **Beginner: RBAC Basics**

### Create & View Roles:
```bash
kubectl create role <ROLE_NAME> --verb=<VERBS> --resource=<RESOURCES> --namespace=<NAMESPACE>
kubectl get roles -n <NAMESPACE>
```

### Create & View RoleBindings:
```bash
kubectl create rolebinding <ROLEBINDING_NAME> --role=<ROLE_NAME> --user=<USER_NAME> --namespace=<NAMESPACE>
kubectl get rolebindings -n <NAMESPACE>
```

### Describe Roles & RoleBindings:
```bash
kubectl describe role <ROLE_NAME> -n <NAMESPACE>
kubectl describe rolebinding <ROLEBINDING_NAME> -n <NAMESPACE>
```

---

## 🌊 **Intermediate: Diving Deeper**

### Create & View ClusterRoles & ClusterRoleBindings:
```bash
kubectl create clusterrole <CLUSTERROLE_NAME> --verb=<VERBS> --resource=<RESOURCES>
kubectl get clusterroles
kubectl create clusterrolebinding <CLUSTERROLEBINDING_NAME> --clusterrole=<CLUSTERROLE_NAME> --user=<USER_NAME>
kubectl get clusterrolebindings
```

### Describe ClusterRoles & ClusterRoleBindings:
```bash
kubectl describe clusterrole <CLUSTERROLE_NAME>
kubectl describe clusterrolebinding <CLUSTERROLEBINDING_NAME>
```

### Limiting Access to Specific Resources:
```bash
# Add this to the rules section in the Role or ClusterRole YAML:
resourceNames: ["name1", "name2"]
```

### Save Roles & RoleBindings to Files:
```bash
kubectl get role <ROLE_NAME> -n <NAMESPACE> -o yaml > role.yaml
kubectl get rolebinding <ROLEBINDING_NAME> -n <NAMESPACE> -o yaml > rolebinding.yaml
```

---

## ⚔️ **Advanced: Delving into the Abyss**

### Aggregated ClusterRoles:
```bash
# In the ClusterRole YAML:
aggregationRule:
  clusterRoleSelectors:
  - matchLabels:
      <YOUR_LABEL_KEY>: <YOUR_LABEL_VALUE>
```

### Using RBAC with Non-Resource URLs:
```bash
# In the Role or ClusterRole YAML:
rules:
- nonResourceURLs: ["/<NON_RESOURCE_PATH>"]
  verbs: ["<VERB>"]
```

### External Authentication (Brief overview):
```bash
# Set OIDC options for the Kubernetes API server:
--oidc-issuer-url=<ISSUER_URL>
--oidc-client-id=<CLIENT_ID>
```

---

## ✨ **Expert: Navigating the Labyrinth**

### Dynamic RBAC Generation (Example with kubegen):
```bash
kubegen generate -f <YOUR_CONFIG_PATH>
```

### GitOps with RBAC:

#### ArgoCD:
```bash
argocd app create <APP_NAME> --repo <REPO_URL> --path <PATH_IN_REPO> --dest-server <K8S_API_SERVER> --dest-namespace <DEST_NAMESPACE>
```

#### Flux:
```bash
flux create source git <SOURCE_NAME> --url=<REPO_URL> --branch=<BRANCH>
flux create kustomization <KUSTOMIZATION_NAME> --source=<SOURCE_NAME> --path="./path_in_repo" --prune=true --interval=1h
```

### Customizing RBAC Decisions:
When creating a custom API server, override the RBAC authorizer by implementing the `Authorizer` interface to provide custom decision logic.

### Backup and Restore RBAC Configs:
```bash
kubectl get roles,rolebindings,clusterroles,clusterrolebindings --all-namespaces -o yaml > rbac-backup.yaml
```
To restore:
```bash
kubectl apply -f rbac-backup.yaml
```

---

Remember, the provided commands and setups might require additional configurations and customizations based on the specific environment or needs. Always refer to official documentation and adapt commands as necessary. [Read more about Kubernetes RBAC in the official documentation](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
