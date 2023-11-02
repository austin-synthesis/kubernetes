**Kubernetes RBAC for Beginners: The Magical Kingdom of Access Control**

🎉 Welcome, brave traveler! 🎉

You've embarked on a journey to the mystical realm of Kubernetes, where clusters of nodes unite, and pods thrive. But, in every realm, there are rules and guards. Today, we'll uncover the secrets of **Role-Based Access Control (RBAC)** - the magical spell that determines who can do what in our kingdom.

### 📜 The Legend:

In the kingdom of Kubernetes, entities (like users & services) are known as **"subjects"**. Every subject wishes to perform actions on resources (like pods & services). But not every subject should be allowed to do everything. And that's where RBAC comes into play!

### 🌟 Your Quest:

Your mission, should you choose to accept it, is to master the art of crafting RBAC rules. By the end of this quest, you will be able to control who gets to do what in our kingdom.

### 🧙‍♂️ The Spells:

**1. Role**: A set of permissions that specify what actions are allowed on which resources. 

```yaml
# role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```

📖 In the above spell, we've crafted a `Role` named "pod-reader" that allows reading (get & list) pods.

**2. RoleBinding**: A magical link that grants the permissions defined in a Role to a subject.

```yaml
# rolebinding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: "janedoe"
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

📖 With this spell, we've granted "janedoe" the permissions of the "pod-reader" Role. She can now read pods!

**3. ClusterRole**: Just like a Role, but with kingdom-wide (cluster-wide) powers.

```yaml
# clusterrole.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-watcher
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list", "watch"]
```

📖 This `ClusterRole` lets one watch over all the nodes in our kingdom.

**4. ClusterRoleBinding**: Grants a `ClusterRole` to a subject across the entire kingdom.

```yaml
# clusterrolebinding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: watch-nodes
subjects:
- kind: User
  name: "janedoe"
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: node-watcher
  apiGroup: rbac.authorization.k8s.io
```

📖 Now, "janedoe" can watch nodes throughout the kingdom!

### 🏰 Tasks in the Castle:

1. **Craft Your First Role**:
   - Open your magical terminal.
   - Craft a Role that lets a subject delete pods.
   - Hint: The verb is "delete".

2. **Bestow the Role Upon a Subject**:
   - Use a RoleBinding to give this power to a new user, "johndoe".

3. **Guard the Kingdom's Gates (Nodes)**:
   - Make a ClusterRole that lets a subject create, get, and update nodes.
   - Bestow this ClusterRole upon "janedoe" using a ClusterRoleBinding.

### 🎉 Celebration:

Congrats, noble guardian of Kubernetes! You've mastered RBAC's basics. The kingdom is safer and more organized, all thanks to you.

Remember, with great power comes great responsibility. Use your RBAC spells wisely, ensuring only those who need access get it. Safe travels on your Kubernetes journey! 🌟🚀🏰

[**Intermediate Guide**](./intermediate.md): Familiar with the basics and ready to dive deeper? Continue your journey here.
