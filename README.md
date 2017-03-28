## Running Validate

One of the key advantages of the Validate workflow is that it allows for seamless integration into the [Cyverse / TACC](docs/Intro_to_CyVerse.md) infrastructure. Rather than running computationally demanding tasks on your own hardware or struggling with large file management, you can Validate in confidence using high-speed computing systems such as [Stampede](docs/Stampede-guide.md), the Discovery Environment, and [Atmosphere](docs/Validate_on_Atmosphere.md).

Please see [this guide](docs/Account-setup.md) for information on requesting access to these resources.

If you do not have access to any of the above systems, you may nevertheless download the Validate workflow for use on your own machine. Functionally this should be quite similar to working with Validate on Stampede with some command line knowledge.

# Quickstart Guide

The Validate workflow consists of four key stages: Simulation (or importing your own data set), GWAS analysis, comparision of tools via Winnow, and visualization via Demonstrate. Generally, you will want to familiarize yourself with the workflow by following our [tutorial for running the workflow on Stampede using a limited Syngenta data set](docs/syngenta_stampede.md).

From there, you may wish to try [simulating a data set using AlphaSim](docs/alphasim.md).

If you have your own data prepared and in the appropriate format, please see [this tutorial](docs/datastore.md) for accessing the CyVerse data store from the command line.

* 1. Setting up Agave
* [2. Simulation with Alphasim](docs/alphasim.md)
* 3. GWAS tools
* [4. Winnow](docs/Winnow.md)
* [5. Demonstrate](docs/Demonstrate.md)

## Old Workflow Guide:

[Workflow Guide](docs/workflow documentation.md) 

[Working with your own Functions](docs/Your_functions.md)
[Working with your own Simulations](docs/Your_sims.md)

[Further Winnow Development](docs/Winnow_develop.md)
[Docker Tutorial](docs/docker_info/Docker_Tutorial.md)


