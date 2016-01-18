# Kubernetes for Hubot

Query your Kubernetes resources using Hubot.

## Installation

Add `hubot-kubernetes` to your `package.json` file:

    "dependencies": {
      "hubot": ">= 2.5.1",
      "hubot-scripts": ">= 2.4.2",
      "hubot-kubernetes": ">= 0.0.0"
    }

Then add "hubot-kubernetes" to your `external-scripts.json` file:

    ["hubot-kubernetes"]

Finally, run `npm install hubot-kubernetes` and you're done!

### Configuration

- KUBE_HOST - (REQUIRED) Your Kubernetes apiserver url.
- KUBE_CONTEXT - (OPTIONAL) Default namespace for the queries.
- KUBE_VERSION - (OPTIONAL) Your Kubernetes api version. (By default: v1)
- NODE_TLS_REJECT_UNAUTHORIZED - (OPTIONAL) For https connections, if apiserver is using a self signed certificate, this env variable needs to be set as false.

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

