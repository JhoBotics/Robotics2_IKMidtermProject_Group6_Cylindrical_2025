# Robotics2_IK_Group6_MIDTERM_2025

# CYLINDRICAL

### Calculator Code in Python
```Python
import numpy as np

#Inverse Kinematics Using Graphical Method
a1 = float(input("a1 = "))
a2 = float(input("a2 = "))
a3 = float(input("a3 = "))

#Position Vector
xe = float(input("X = "))
ye = float(input("Y = "))
ze = float(input("Z = "))

#Solve for TH1
TH1_rad = np.arctan(ye/xe)

# Convert to degrees
TH1 = np.degrees(TH1_rad)

#Solve for D3
D3 = np.sqrt(xe**2 + ye**2) - a3 

#Solve for D2
D2 = ze - a1 - a2

print("TH1 = ", np.around(TH1,3))
print("D2 = ", np.around(D2,3))
print("D3 = ", np.around(D3,3))
```

### MATLAB Code for Cylindrical Robotic Arm
