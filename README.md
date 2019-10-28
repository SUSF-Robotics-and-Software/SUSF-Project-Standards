# SUSF-Project-Standards

## Repo Structure

Each active repository (excluding this one) must have at least 3 branches:

1. master
1. production
1. development
* experimental branches

### branch: master 

Master is always the last stable working version. When starting a new project using a component, it is best to use this one.
It should require no modification to work as intended.

### branch: production

Production is the latest working version, and may introduce a interface modification (calls are different from the master branch).
When this branch replaces master, master should be retired as a legacy version.
It should require minimal/slight modification to work in place of the old master.

### branch: development

Development is the actively developed branch, and frequent changes should be expected before becoming stable enough to be moved production.

### experimental branches

Experimental branches are for learning and/or for experimental/radical redesigns of established branches.

## Project structure

Projects are collections of components, and 'header' files to customise them to the needs of the project. Any 'general use' discovery/expansion, if discovered in the project, should be reflected in the component branch. 

When integrating a component into a project, it should be included as a sub-module:
https://git-scm.com/book/en/v2/Git-Tools-Submodules