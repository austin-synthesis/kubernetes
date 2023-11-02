**Kubernetes RBAC: Intermediate Chronicles – Dive Deeper into the Secrets**

🔥 **The Saga Continues...** 🔥

Bravo! Having mastered the basics of Kubernetes RBAC, you're now ready for a deeper dive. Let the new chapter of our epic tale begin!

### 📜 **The Prologue**:

As our realm expands, so does the complexity of our access controls. We need to deal with not just the basic resources but also with finer aspects, like differentiating between reading a config versus updating it.

### 🌌 **Your New Adventure**:

Venture further into the intricacies of RBAC, unveiling the nuanced controls and patterns that only seasoned knights and mages know about.

### 🧙‍♂️ **Advanced Spells**:

**1. Multiple API Group Access**:
RBAC isn't just limited to the core resources. Extend your influence to other mystical areas like `networking` or `rbac`.

```yaml
# extended-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: extended-permissions
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["networking.k8s.io"]
  resources: ["networkpolicies"]
  verbs: ["create", "update"]
```

📖 This allows subjects to view pods and manage network policies.

**2. ResourceNames - The Fine Guard**:

Limit access to specific instances of a resource, not just the resource type.

```yaml
# specific-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: specific-pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get"]
  resourceNames: ["my-special-pod"]
```

📖 This spell permits reading only `my-special-pod` and no other pod.

**3. Non-Resource URLs**:

Did you know RBAC can control access to non-resource endpoints too? Like `/healthz`?

```yaml
# non-resource-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: health-checker
rules:
- nonResourceURLs: ["/healthz", "/livez", "/readyz"]
  verbs: ["get"]
```

📖 Grant this, and one can monitor the health of the kingdom's gateways!

### 🏞 **Challenges Beyond the Castle**:

1. **Craft an Extended Role**:
   - Write a Role that allows reading `secrets` but only updating `configmaps`.

2. **Guard a Special Treasure (Resource)**:
   - Use `resourceNames` to protect a specific `configmap` named `kingdom-config`. Only selected knights should read it.

3. **Bestow Health Check Access**:
   - Create a `ClusterRoleBinding` that allows a service account named `health-bot` to use the `health-checker` ClusterRole.

### 🎭 **Twists & Turns**:

Remember that `RoleBindings` and `ClusterRoleBindings` can refer to both `Roles` and `ClusterRoles`. This means you can use a `RoleBinding` in a specific namespace to bind a user to a `ClusterRole`. This pattern can be powerful but use it wisely!

### 🌟 **Conclusion of the Chapter**:

Well done, intrepid explorer! You've journeyed further into the RBAC wilderness and uncovered deeper magics. With these new spells at your fingertips, you're well-equipped to protect and manage even the most intricate corners of our Kubernetes realm.

May your paths be clear, and your roles be ever appropriate! Until the next adventure... 🌌🔮🛡

[**Advanced Guide**](./advanced.md): Explore advanced RBAC configurations and master the intricacies.
