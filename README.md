# Solution Pattern: Build an extendable Multi-Channel Messaging Platform

This repository contains an implementation demo of the Solution Pattern.

The Solution Pattern proposes a platform that unifies multiple messaging/collaboration systems to address the problem of communication fragmentation where teams and groups, inside and outside large organisations, are affected by communication inefficiencies. 

The unified platform, integrates all systems to behave as one providing new collaboration possibilities and capabilities. The platform has a pluggable architecture that allows new channels to be added in.

This demo showcases the implementation of a multi-channel support service for Globex (a fictitious company) customers that enables clients to chat in real time with support teams.


## Home page

Head to the Solution Pattern's home page to get the full context of this demo sources. You can find it following the link below:

[PENDING]

<!-- - [**Solution Pattern Home Page**](https://redhat-solution-patterns.github.io/solution-pattern-edge-to-cloud-pipelines/solution-pattern-edge-to-core-pipelines/index.html) -->


## Tested with

* RH OpenShift 4.15.14
* Camel K 1.10.6 provided by Red Hat
* AMQ-Streams 2.7.0-0 provided by Red Hat
* AMQ Broker 7.11.6-opr-2 provided by Red Hat
* Data Grid 8.4.15 provided by Red Hat
* Web Terminal 1.10.0 provided by Red Hat
* RH OpenShift GitOps 1.12.3 provided by Red Hat Inc



## Deployment instructions

### 2. Provision an OpenShift environment

1. Provision the following RHDP item:

    * [PENDINIG]

    <!-- * [**Solution Pattern - Edge to Core Data Pipelines for AI/ML**](https://demo.redhat.com/catalog?item=babylon-catalog-prod/community-content.com-edge-to-core.prod&utm_source=webapp&utm_medium=share-link) -->

   <br/>

1. Alternatively, if you don't have access to RHDP, ensure you have an OpenShift environment available, meeting the pre-requisite product version for OpenShift (see '_Tested with_' section to inspect product versions).

<br/>

### 2. Deploy the Solution Pattern

The instructions below assume:
* You either have _Docker_, _Podman_ or `ansible-playbook` installed on your local environment.
* You have provisioned an OCP instance (tested with OCP 4.15), using RHDP, and a bastion server is available.

<br/>


#### Install the demo

1. Clone this GitHub repository:

    ```sh
    git clone https://github.com/brunoNetId/sp-multi-channel-messaging-platform.git
    ```

1. Change to root directory of the project.

    ```sh
    cd sp-multi-channel-messaging-platform
    ```

    <br/>

1. When running with _Docker_ or _Podman_
    
    1. Configure the `KUBECONFIG` file to use (where kube details are set after login).

        ```sh
        export KUBECONFIG=./ansible/kube-demo
        ```

    1. Login into your OpenShift cluster from the `oc` command line.

        ```sh
        oc login --username="admin" --server=https://(...):6443 --insecure-skip-tls-verify=true
        ```

        Replace the `--server` url with your own cluster API endpoint.

    1. Run the Playbook

        1. With Docker:
        
            ```sh
            docker run -i -t --rm --entrypoint /usr/local/bin/ansible-playbook \
            -v $PWD:/runner \
            -v $PWD/ansible/kube-demo:/home/runner/.kube/config \
            quay.io/agnosticd/ee-multicloud:v0.0.11  \
            ./ansible/install.yaml
            ```
        
        1. With Podman:
        
            ```sh
            podman run -i -t --rm --entrypoint /usr/local/bin/ansible-playbook \
            -v $PWD:/runner \
            -v $PWD/ansible/kube-demo:/home/runner/.kube/config \
            quay.io/agnosticd/ee-multicloud:v0.0.11  \
            ./ansible/install.yaml

            ```
    <br/>

1. When running with Ansible Playbook (installed on your machine)

    1. Login into your OpenShift cluster from the `oc` command line.

        For example with: \
        ```sh
        oc login --username="admin" --server=https://(...):6443 --insecure-skip-tls-verify=true
        ```
        (Replace the `--server` url with your own cluster API endpoint)

    1. Set the following property:
        ```
        TARGET_HOST="lab-user@bastion.b9ck5.sandbox1880.opentlc.com"
        ```
    2. Run Ansible Playbook
        ```sh
        ansible-playbook -i $TARGET_HOST,ansible/inventory/openshift.yaml ./ansible/install.yaml
        ```

<br/>

### 3. Undeploy the Solution Pattern

If you wish to undeploy the demo, use the same commands as above, but with:
 - `./uninstall.yaml`

Instead of:
 - ~~`./install.yaml`~~
