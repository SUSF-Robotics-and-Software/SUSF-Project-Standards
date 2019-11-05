# Python Standards

## Style

All python code shall follow PEP-8 standards defined in https://www.python.org/dev/peps/pep-0008/.

## Naming Scheme

Follow PEP-8 conventions, generally:

```python
# CamelCase for classes
class ExampleClass:
    pass

# snake_case for function names and variables
example_variable = 42

def example_function:
    pass
```

## Variables

Variable names shall be descriptive and where applicable shall include units and frames to avoid simple mistakes:

```python
# Bad:
#   Doesn't tell us what it is
#   No idea what units or frame it's in
p = [4, 5, 6]

# Good:
#   Tells us exactly what it is (the rover's position)
#   Know exactly the units (metres) and frame (Local Map), where applicable the
#   name should take the form name_unit_Frame
rover_pos_m_Lm = [4, 5, 6]
```
At the first declaration of a variable (for example in a class definition) a comment shall be included describing the variable and it's units/frame.

For units which present problems (like m/s^2) the declaration comment should clarify:
```python
# Bad:
#   Is this m/(s^2) or m * s^2?

rover_speed_ms2_Lm = 4

# Good:
#   Defines the unit and frame well, gives a conscice description of the variable

# Speed of the rover
#    Unit: metres / (second ^2)
#   Frame: Local Map
rover_speed_mss_Lm = 4
```

## Comments

Code shall be well commended and commends shall be meaningful, giving an understanding of why something is being done not just what:

```python
# Bad:
#   Just says what's happening, why is it being done?

# Invert the DCM
rover_att_rot_LmToRb = np.linalg.inv(rover_att_dcm_LmToRb)

# Good:
#   Tells us what's happening and why we're doing it

# Two types of rotation matrix exist, active and passive. The DCM which was 
# calculated earlier is a passive rotation, but we want an active rotation 
# (a rotation matrix), to do this we simply invert the DCM. See 
# https://en.wikipedia.org/wiki/Active_and_passive_transformation for more info.
rover_att_rot_LmToRb = np.linalg.inv(rover_att_dcm_LmToRb)
```

## Notes on numerical protection

When a numerical problem can occur (say a division by zero) you should write a short comment explaining what could go wrong, and what you are doing to prevent that from happening. This is to force you to think about the code you are writing so that we don't get random crashes in the software.

```python
# Bad:
#   No comment and no protection, what if we're at the target already?

time_to_target_s = rover_speed_mss_Lm / target_dist_m_Lm

# Good:
#   Detailed, but not exhaustive description of the problem, and a sensible 
#   protection used

# Numerical protection note:
#   The operation "= ... / targetDist_m_Lm" can result in a division by zero if
#   the rover is at or close to the target. To protect against this we say that
#   if the rover is within the target threshold the time to the target is zero.
#   The threshold has been defined as some value strictly greater than zero, 
#  therfore division by zero cannot occur.
if (target_dist_m_Lm < target_threshold_m_Lm):
    time_to_target_s = 0
else:
    time_to_target_s = rover_speed_mss_Lm / target_dist_m_Lm

```