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

    * [**Solution Pattern - Build an extendable Multi-Channel Messaging Platform**](https://demo.redhat.com/catalog?item=babylon-catalog-prod/community-content.com-multi-channel.prod&utm_source=webapp&utm_medium=share-link)

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

1. Change to the `ansible` directory (in the root project).

    ```sh
    cd sp-multi-channel-messaging-platform/ansible
    ```

    <br/>

1. When running with _Docker_ or _Podman_
    
    1. Configure the `KUBECONFIG` file to use (where kube details are set after login).

        ```sh
        export KUBECONFIG=./kube-demo
        ```

    1. Login into your OpenShift cluster from the `oc` command line.

        ```sh
        oc login --username="admin" --server=https://(...):6443 --insecure-skip-tls-verify=true
        ```

        Replace the `--server` url with your own cluster API endpoint.


    1. Run the Playbook with Docker/Podman

        1. First, read the note below:
        
           > [!IMPORTANT]
           > If your system is SELinux enabled, you'll need to label the project directory to allow docker/podman to access it. Run the command:
           > ```sh     
           > sudo chcon -Rt svirt_sandbox_file_t $PWD
           > ```
           > The error you may get if SELinux blocks the process would be similar to: \
           > `ERROR! the playbook: ./ansible/install.yaml could not be found`
          

        1. Then, to run with Docker:
        
            ```sh
            docker run -i -t --rm --entrypoint /usr/local/bin/ansible-playbook \
            -v $PWD:/runner \
            -v $PWD/kube-demo:/home/runner/.kube/config \
            quay.io/agnosticd/ee-multicloud:v0.0.11  \
            ./playbooks/install.yml
            ```
        
        1. Or, to run with Podman:
        
            ```sh
            podman run -i -t --rm --entrypoint /usr/local/bin/ansible-playbook \
            -v $PWD:/runner \
            -v $PWD/kube-demo:/home/runner/.kube/config \
            quay.io/agnosticd/ee-multicloud:v0.0.11  \
            ./playbooks/install.yml

            ```
    <br/>

1. When running with Ansible Playbook (installed on your machine)

    1. Login into your OpenShift cluster from the `oc` command line.

        For example with: \
        ```sh
        oc login --username="admin" --server=https://(...):6443 --insecure-skip-tls-verify=true
        ```
        (Replace the `--server` url with your own cluster API endpoint)

    1. Ensure you work from the `ansible` directory:
        ```
        cd ansible
        ```
    2. Run Ansible Playbook
        ```sh
        ansible-playbook playbooks/install.yml
        ```

<br/>

### 3. Undeploy the Solution Pattern

If you wish to undeploy the demo, add the following `ACTION` parameter to the command:
 - `./playbooks/install.yml -e ACTION=uninstall`

Instead of just:
 - ~~`./playbooks/install.yml`~~
