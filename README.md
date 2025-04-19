# Robotics2_IK_Group6_MIDTERM_2025

# CYLINDRICAL
## Trial Values
The group manually assigned values to the trial joint variable in MATLAB, ranging from 0% to 100%. These values were entered into the MATLAB simulation, which then automatically generated the corresponding trial position vector using forward kinematics (FK). This trial position vector was then input into a Python-based calculator developed by the group, which performed inverse kinematics (IK) to compute the actual joint variable. The resulting actual joint variable was recorded in the “Actual JV from Python” table. This value was then re-entered into the MATLAB simulation to obtain the actual position vector. Since both the forward and inverse kinematics produced matching results, the comparison confirms that FK = IK.
![Image](https://github.com/user-attachments/assets/c8251607-d81b-44be-a397-5e77f4cd15c6)

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

### MATLAB Code for Cylindrical Mechanical Manipulator
```matlab
%Clear
clear
clc
close all

disp('Cylindrical')
syms a1 a2 a3

%% Link lengths
a1 = 100;
a2 = 100;
a3 = 100;

%% D-H Parameters [theta, d, r, alpha, offset]  
% if prismatic joint: theta = theta, d = 0, offset = 1, after offset put the value of d
% if revolute joint: theta = 0,offset = 0, after offset put the value of theta

H0_1 = Link([0,a1,0,0,0,0]);
H0_1.qlim = [-pi/2 pi/2];

H1_2 = Link([-pi/2,0,0,-pi/2,1,a2]);
H1_2.qlim = [0 90];

H2_3 = Link([0,0,0,0,1,a3]);
H2_3.qlim = [0 90];

Mid3 = SerialLink([H0_1 H1_2 H2_3], 'name', 'Cylindrical')
Mid3.plot([0 0 0], 'workspace', [-200 200 -200 200 0 500])

figure(1)
Mid3.teach
```

