# hello-ghost

This project consists of a basic hasura project with Ghost with SQLite deployed.

## Quickstart

Follow this section to get the ghost blog working. Before you begin, ensure you have the latest version of [hasura cli tool](https://docs.hasura.io/0.15/manual/install-hasura-cli.html) installed.

### Step 1: Getting the project

```sh
$ hasura quickstart hello-ghost
$ cd hello-ghost
```

The above command does the following:
1. Creates a new folder in the current working directory called `hello-ghost`
2. Creates a new free hasura cluster for you and sets that cluster as the default cluster for this project
3. Initializes `hello-ghost` as a git repository and adds the necessary git remotes.

### Step 2: Getting cluster information

Every hasura project is run on a Hasura cluster. To get details about the cluster this project is running on:

```sh
$ hasura cluster status
```

This will give you your cluster status like so

```sh
INFO Status:
Cluster Name:       h34-excise98-stg
Cluster Alias:      hasura
Kube Context:       h34-excise98-stg
Platform Version:   v0.15.3
Cluster State:      Synced
```

Keep a note of your cluster name. Alternatively, you can also go to your [hasura dashboard](https://dashboard.hasura.io) and see the list of your clusters.

### Step 3: Pushing the project to the cluster

To deploy your app:

```sh
$ git add .
$ git commit -m "First commit"
$ git push hasura master
```
When you push for the first time, it might take sometime. Next time onwards, it is really fast.

Once the above commands are executed successfully, your ghost blog goes live at `https://app.cluster-name.hasura-app.io`

## Files and Directories

The project (a.k.a. project directory) has a particular directory structure and it has to be maintained strictly, else `hasura` cli would not work as expected. A representative project is shown below:

```
.
├── hasura.yaml
├── clusters.yaml
├── conf
│   ├── authorized-keys.yaml
│   ├── auth.yaml
│   ├── ci.yaml
│   ├── domains.yaml
│   ├── filestore.yaml
│   ├── gateway.yaml
│   ├── http-directives.conf
│   ├── notify.yaml
│   ├── postgres.yaml
│   ├── routes.yaml
│   └── session-store.yaml
├── migrations
│   ├── 1504788327_create_table_user.down.yaml
│   ├── 1504788327_create_table_user.down.sql
│   ├── 1504788327_create_table_user.up.yaml
│   └── 1504788327_create_table_user.up.sql
└── microservices
    └── app
        ├── app/
        ├── k8s.yaml
        └── Dockerfile
```

### `hasura.yaml`

This file contains some metadata about the project, namely a name, description and some keywords. Also contains `platformVersion` which says which Hasura platform version is compatible with this project.

### `clusters.yaml`

Info about the clusters added to this project can be found in this file. Each cluster is defined by it's name allotted by Hasura. While adding the cluster to the project you are prompted to give an alias, which is just hasura by default. The `kubeContext` mentions the name of kubernetes context used to access the cluster, which is also managed by hasura. The `config` key denotes the location of cluster's metadata on the cluster itself. This information is parsed and cluster's metadata is appended while conf is rendered. `data` key is for holding custom variables that you can define.

```yaml
- name: h34-ambitious93-stg
  alias: hasura
  kubeContext: h34-ambitious93-stg
  config:
    configmap: controller-conf
    namespace: hasura
  data: null
```
