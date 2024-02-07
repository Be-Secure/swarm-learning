# <d></d> <img style="float: right;" src="docs/images/GettyImages-1148109728_EAA-graphic-A_112_0_72_RGB.jpg?raw=true"/> SWARM LEARNING

#### Product version: 2.2.0

Swarm Learning is a decentralized, privacy-preserving Machine Learning framework. This framework utilizes the computing power at, or near, the distributed data sources to run the Machine Learning algorithms that train the models. It uses the security of a blockchain platform to share learnings with peers in a safe and secure manner. In Swarm Learning, training of the model occurs at the edge, where data is most recent, and where prompt, data-driven decisions are mostly necessary. In this completely decentralized architecture, only the insights learned are shared with the collaborating ML peers, not the raw data. This tremendously enhances data security and privacy.
<img width="80%" height="70%" src="/docs/User/GUID-899B556F-D33F-42D1-8D0D-37F191715709-high.png">

Swarm Learning framework is made up of various components known as nodes, such as Swarm Learning (SL) nodes, Swarm Network (SN) nodes, Swarm Learning Command Interface (SWCI) nodes, and Swarm Operator (SWOP) nodes. Each node of Swarm Learning is modularized and runs in a separate container. The **nodes represent different Swarm Learning _functionality_ and not physical server nodes**.

-   SL nodes run the core of Swarm Learning. An SL node works in collaboration with all the other SL nodes in the network. It regularly shares its learnings with the other nodes and incorporates their insights. SL nodes act as an interface between the user model application and other Swarm Learning components. SL nodes take care of distributing and merging model weights in a secured way.

-   SN nodes form the blockchain network. The current version of Swarm Learning uses an open-source version of Ethereum as the underlying blockchain platform. The SN nodes interact with each other using this blockchain platform to maintain and track progress. The SN nodes use this state and progress information to co-ordinate the working of the other swarm learning components. Blockchain can be persisted across SN restart to preserve past progress network. User can lookup blockchain and see all history of operations. Users have the flexibility to stop Swarm after training is completed. Once user restarts the SN network, the existing history can be accessed using the `get` or `list` command of SWCI management interface.

    **Sentinel Node** is a special SN node. The Sentinel node is responsible for initializing the blockchain network. This is the first node to start.

<blockquote>
    NOTE: Only metadata is written to the blockchain. The model itself is not stored in the blockchain.
</blockquote>

-   SWOP node is an agent that can manage Swarm Learning operations. SWOP is responsible to execute tasks that are assigned to it. A SWOP node can execute only one task at a time. SWOP helps in executing tasks such as starting and stopping Swarm runs, building and upgrading ML containers, and sharing models for training. For more information about SWOP, see [Swarm Operator node \(SWOP\)](./docs/User/Swarm_Operator_node_(SWOP).md).

-   SWCI node is the command interface tool to the Swarm Learning framework. It is used to monitor the Swarm Learning framework. SWCI nodes can connect to any of the SN nodes in a given Swarm Learning framework to manage the framework. 
For more information on SWCI, see [Swarm Learning Command Interface](./docs/User/Swarm_Learning_Command_Interface.md).

-   SLM-UI node is the GUI management tool to the Swarm Learning framework. It has three functionalities. It is used to [install](./docs/Install/Installing_Swarm_Learning_using_SLM-UI.md) Swarm Learning framework, [deploy](./docs/User/Running_MNIST_example_using_SLM-UI.md) a Swarm training and [monitor](./docs/User/Monitoring_Swarm_Learning_training_using_SLM-UI.md) the progress of the current training and track past training runs to decide the best training. 

-   Swarm Learning security and digital identity aspects are handled by X.509 certificates. Communication among Swarm Learning components are secured using X.509 certificates. User can either generate their own certificates or directly use certificates generated by any Standard Security software such as SPIRE. For more information on SPIRE, see [https://thebottomturtle.io/Solving-the-bottom-turtle-SPIFFE-SPIRE-Book.pdf](https://thebottomturtle.io/Solving-the-bottom-turtle-SPIFFE-SPIRE-Book.pdf) and [https://spiffe.io/](https://spiffe.io/).

<blockquote>
    NOTE: Swarm Learning framework does not initialize if certificates are not provided.
</blockquote>

-   Swarm Learning components communicate with each other using a set of TCP/IP ports. For more information on port details that must be opened, see [Exposed Ports](/docs/Install/Exposed_port_numbers.md).
<blockquote>
NOTE: The participating nodes must be able to access each other's ports.
</blockquote>

-   License Server installs and manages the license that is required to run the Swarm Learning framework. The licenses are managed by the AutoPass License Server \(APLS\) container. For more information, see [APLS User Guide](/docs/HPE%20AutoPass%20License%20Server%20User%20Guide.pdf).

Swarm Learning nodes works in collaboration with other Swarm Learning nodes in the network. It regularly shares its learnings with the other nodes and incorporates their insights. This process continues until the Swarm Learning nodes train the model to desired state. 

## User ML components

User can transform any Keras or PyTorch based ML program that is written using Python3 into a Swarm Learning ML program by [making a few simple changes](./docs/User/How_to_Swarm_enable_an_ML_algorithm.md) to the model training code by including the `SwarmCallback` API. For more information, see any of the [examples](/examples/README.md) included with the Swarm Learning package for a sample code.

The transformed user Machine Learning \(user ML node\) program can be run on the host or user can build it as a Docker container.

<blockquote>
NOTE: HPE recommends users to build an ML Docker container.

</blockquote>

The ML node is responsible to train and iteratively update the model. For each ML node, there is a corresponding SL node in the Swarm Learning framework, which performs the Swarm training. Each pair of ML and SL nodes must run on the same host. This process continues until the SL nodes train the model to the desired state.

<blockquote>
NOTE: All the ML nodes must use the same ML platform either Keras (based on TensorFlow 2 backend) or PyTorch. Using Keras for some of the nodes and PyTorch for the other nodes is not supported.
</blockquote>

User can monitor the progress of the current training as shown in the following image. It shows all running Swarm nodes, loss, model metric (for example, accuracy) and overall training progress for each ML-SL pair node. On hovering over the "progress bar", user can view the total number of epochs and the total number of completed epochs.

<img width="80%" height="70%" src="/docs/User/GUID-CB6F59C9-7CD9-4EE8-BA7C-3082F07B8491-high.png">

## Getting Started 
  1. [Prerequisites](/docs/Install/Prerequisites.md) for Swarm Learning
  2. [Upgrading from earlier evaluation versions](/docs/Install/Versioning_and_upgrade.md)
  3. [Download and setup Swarm Learning](/docs/Install/HPE_Swarm_Learning_installation.md) using the SLM-UI installer 
  4. Execute [MNIST example](/examples/mnist/README.md)
  5. [Running MNIST example using SLM-UI](/docs/User/Running_MNIST_example_using_SLM-UI.md)
  6. [Monitoring & Tracking Swarm Learning training using SLM-UI](/docs/User/Monitoring_Swarm_Learning_training_using_SLM-UI.md)
  7. [Frequently Asked Questions](/docs/User/Frequently_asked_questions.md)
  8. [Troubleshooting](/docs/User/Troubleshooting.md)
  9. [Release Notes](/docs/HPE_Swarm_learning_2.1.0_Release_Notes.pdf)

<blockquote>

NOTE: **Accessing Hewlett Packard Enterprise Support** clause and **Concurrent swarm training** feature mentioned in the documentation are applicable for enterprise customers ONLY.

</blockquote>

## Documentation

  - [How Swarm Learning Components interact](/docs/User/Swarm_Learning_component_interactions.md)
  - [Component interactions when using Reverse Proxy](/docs/User/Swarm_Learning_Component_Interactions_using_Reverse_Proxy.md)
  - [Swarm Learning Concepts](/docs/User/Swarm_Learning_concepts.md)
  - [Working of a Swarm Learning node](/docs/User/Working_of_a_Swarm_Learning_node.md)
  - [Adapting ML programs for Swarm Learning](/docs/User/Adapting_an_ML_program_for_Swarm_Learning.md)
  - [Swarm wheels package](/docs/User/Swarm_client_interface-wheels_package.md)
  - [Configuring Swarm Learning components](/docs/Install/Configuring_Swarm_Learning.md) 
  - [Using SWCI](/docs/User/Swarm_Learning_Command_Interface.md)
  - [Using SWOP](/docs/User/Swarm_Operator_node_(SWOP).md)
  - [Running Swarm learning examples using SLM-UI](/docs/Install/Running_Swarm_Learning_examples_using_SLM-UI.md)
  - [Running Swarm Learning using CLI](/docs/Install/Running_Swarm_Learning_using_CLI.md)
  - [Running Swarm Learning with SE Linux](/docs/Install/Running_Swarm_with_SE_Linux.md)
  - [Running Swarm Learning with Podman](/docs/Install/Running_Swarm_Learning_with_Podman.md)
  - [Running Swarm Learning with Spire](/docs/Install/Running_Swarm_Learning_with_Spire.md)
  - [Examples](/examples/README.md)
  - [Swarm Learning diagnostics using CLI](/docs/User/Swarm_Log_Collector.md)
  - [Centralized Swarm diagnostics using SLM-UI](/docs/Install/Centralized_Swarm_diagnostic.md)
  - [Extending Swarm Learning for new ML platforms](/lib/src/README.md)
  - [Merge Methods - Whitepaper](/docs/HPE_Merge_Methods_Whitepaper.pdf)
  - [Uninstalling Swarm Learning using SLM-UI](/docs/Install/Uninstalling_Swarm_Learning_using_SLM-UI.md)
  
## References

  - [Papers](docs/Generic/papers-and-articles.md)
  - [Videos](docs/Generic/videos.md)
  - [URLs](docs/Generic/URL.md)

## Acronyms and Abbreviations
  Refer to [Acronyms and Abbreviations](docs/Generic/acronyms.md) for more information.

## Getting in touch 
  Feedback and questions are appreciated. You can use the issue tracker to report bugs on GitHub.  (Or)
  Join the [HPE Developer Slack Workspace](https://slack.hpedev.io/) and start a discussion in our [#hpe-swarm-learning](https://hpedev.slack.com/archives/C04A5DK9TUK) channel.
  
## Contributing
  Refer to [Contributing](docs/Generic/CONTRIBUTING.md) for more information.

## License
  The distribution of Swarm Learning in this repository is for non-commercial and experimental use under this [license](docs/Generic/LICENSE.md). 
  
  See [ATTRIBUTIONS](docs/Generic/ATTRIBUTIONS.md) and [DATA LICENSE](docs/Generic/DATA_LICENSE.md) for terms and conditions for using the datasets included in this repository.
