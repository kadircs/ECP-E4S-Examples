![research](https://pantheonscience.github.io/states/research.png)

# Pantheon/E4S workflows

A repository for examples using E4S and Pantheon workflows. 

Build instructions embedded in this workflow are derived from the Ascent build instructions [here](https://ascent.readthedocs.io/en/latest/BuildingAscent.html). This workflow uses **spack** to build all executables, from a specific commit.

This workflow will pull cached builds from a [E4S](https://e4s-project.github.io/) repository, if they exist
to speed up the build/install of requisite applications. If no cached builds are available, it will use
[spack](https://github.com/spack/spack) to build applications.

The workflow does the following:

- Creates a [Pantheon](http://pantheonscience.org/) environment and build location
- Clones a specific commit of [Spack](https://github.com/spack/spack)
- Uses `spack` to build [Ascent](https://ascent.readthedocs.io/en/latest/) and set up a coupled app/in-situ workflow
    - Optionally builds an application, depending on the workflow
- Runs a parallel job that creates a `Cinema` database
- Verifies the `Cinema` database

## Using this repository

First, clone the repository, then:

- Log onto Summit
- In a shell:
```
    git clone git@github.com:pantheonscience/ECP-E4S-Examples.git
    cd ECP-E4S-Examples
    git submodule update --init --recursive
```
- Edit the `bootstrap.env` file to include your summit allocation ID
- Execute the workflow by typing `./execute`

When the workflow is run, the following files will be run in this order:

- `setup/install-deps.sh`
   - `setup/install-app.sh` (called from the above script)
- `run/run.sh` (this submits the job)
- `run/wait_for_completion.sh`
- `postprocessing/postprocessing.sh`
- `validate/validate.sh`
