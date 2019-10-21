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

## Coding standards

### Style

All python code shall follow PEP-8 standards defined in https://www.python.org/dev/peps/pep-0008/.

### Variables

Variable names shall be descriptive and where applicable shall include units and frames to avoid simple mistakes:

```python
# Bad:
#   Doesn't tell us what it is
#   No idea what units or frame it's in
p = [4, 5, 6]

# Good:
#   Tells us exactly what it is (the rover's position)
#   Know exactly the units (metres) and frame (Local Map)
roverPos_m_Lm = [4, 5, 6]
```
At the first declaration of a variable (for example in a class definition) a comment shall be included describing the variable and it's units/frame.

For units which present problems (like m/s^2) the declaration comment should clarify:
```python
# Bad:
#   Is this m/(s^2) or m * s^2?

roverSpeed_ms2_Lm = 4

# Good:
#   Defines the unit and frame well, gives a conscice description of the variable

# Speed of the rover
#    Unit: metres / (second ^2)
#   Frame: Local Map
roverSpeed_mss_Lm = 4
```

### Comments

Code shall be well commended and commends shall be meaningful, giving an understanding of why something is being done not just what:

```python
# Bad:
#   Just says what's happening, why is it being done?

# Invert the DCM
roverAtt_rot_LmToRb = np.linalg.inv(roverAtt_dcm_LmToRb)

# Good:
#   Tells us what's happening and why we're doing it

# Two types of rotation matrix exist, active and passive. The DCM which was 
# calculated earlier is a passive rotation, but we want an active rotation 
# (a rotation matrix), to do this we simply invert the DCM. See 
# https://en.wikipedia.org/wiki/Active_and_passive_transformation for more info.
roverAtt_rot_LmToRb = np.linalg.inv(roverAtt_dcm_LmToRb)
```