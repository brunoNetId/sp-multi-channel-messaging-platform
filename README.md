# Solution Pattern: Event-Driven Multi-Channel Support Service

Any organisation nowadays generally has a support team to attend customer queries or/and resolve problems. In an effort to get closer to the customer, companies could offer a variety of channels for users to choose from when contacting the Support team. For example, a customer enquiring about a certain product, could do so by using the official portal's chat window, or via a dedicated App from their handsets, or by using an Instant Message application such as WhatsApp.

The Multi-Channel Support Service is a platform that allows customers to choose between different channels to contact the support team. The platform has a pluggable architecture that allows new channels to be added in.

This solution pattern showcases the implementation of a multi-channel support service for Globex (a fictitious company) customers that will enable clients to chat in real time with a team of agents.


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
    git clone https://github.com/brunoNetId/sp-multi-channel-support-service.git
    ```

1. Change to root directory of the project.

    ```sh
    cd sp-multi-channel-support-service
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
