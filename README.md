# Kubernetes for Hubot

Query your Kubernetes resources using Hubot.

## Installation

Add `hubot-kubernetes` to your `package.json` file:

    "dependencies": {
      "hubot": ">= 2.5.1",
      "hubot-scripts": ">= 2.4.2",
      "hubot-redis-brain": "0.0.3",
      "hubot-auth": "^1.2.0",
      "hubot-kubernetes": ">= 0.0.0"
    }

Then add "hubot-kubernetes" to your `external-scripts.json` file:

    ["hubot-kubernetes"]

Finally, run `npm install hubot-kubernetes` and you're done!

### Configuration

- KUBE_HOST - (REQUIRED) Your Kubernetes apiserver url. (By default: https://localhost)
- KUBE_CONTEXT - (OPTIONAL) Default namespace for the queries. (By default: default)
- KUBE_VERSION - (OPTIONAL) Your Kubernetes api version. (By default: v1)
- KUBE_TOKENS - (See Supporting different k8s users section)

#### Self Signed Certificates
For https connections, you need to set one of the following environment variables:
- KUBE_CA - Path of the CA certificate file
- NODE_TLS_REJECT_UNAUTHORIZED - If you don't have a CA certificate file, set this as false for granting access to unauthorized server.

#### Supporting different k8s users
With the assistance of hubot-auth, it is possible to use different basic authentication tokens for each given user role. These are the supported options:
* specify basic auth credentials using KUBE_HOST itself:
  - https://user:password@kubernetes.cluster
* specify a single token using KUBE_TOKENS:
  - export KUBE_TOKENS=user:password
  When you define only a single token in KUBE_TOKENS environment variable, regardless of the users role, it will always use this single token ffor all the requests.
* specify multiple tokens using KUBE_TOKENS:
  - export KUBE_TOKENS=user1:password1,user2:password2
  When you define multiple tokens in KUBE_TOKENS environment variable, it will select a specific token depending on user role. If a token is not defined for a given user role, then it will try to connect to KUBE_HOST url as is. Therefore, if you set basic auth credentials using KUBE_HOST variable, this will be the default access method, for all the undefined user roles.

Caveat:

  If user has multiple roles with corresponding tokens, then first encountered token in the token pool will be used.


### Usage

This extension is used for querying replication controllers, services and pods for the given api server.

 > k8s context

 Returns the current context

 > k8s context test

 Changes the context to test for the user

 > k8s po

 Returns a list of pods for the given context.

 > k8s rc type=front-end

 Returns a list of controllers with label type=front-end for the given context.

