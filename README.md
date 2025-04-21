# Robotics2_IK_Group6_MIDTERM_2025

## CYLINDRICAL MECHANICAL MANIPULATOR

### Kinematic Diagram
<p align="center">
<img src="https://github.com/user-attachments/assets/d5bd761e-35f8-43fc-9495-4c6ff4f07c99" width=700 height=400>


### Parametric Table

### Homogeneos Transformation Matrices

### Top View and Front View of Inverse Kinematics

### Link Lengths
a1 = 100

a2 = 100

a3 = 100

### Trial No. 1 (0%)
Forward Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/f9970303-2a2b-4199-8e06-2673e76959f4" width=700 height=400>

Inverse Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/c4edae68-4c3a-4789-98bf-22e2591b46da" width=700 height=400>

https://github.com/user-attachments/assets/2ff3b653-d276-4214-ba32-9bf29b4289a8
  
### Trial No.2 (25%)
Forward Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/b75178d8-4a35-4067-a089-c74ff893c777" width=700 height=400>

Inverse Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/19b9c871-bedc-4b12-8932-1f41bfad825c" width=700 height=400>

https://github.com/user-attachments/assets/82051161-9f95-471c-971c-f1e07620b40b

### Trial No.3 (50%)
Forward Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/7bc0f485-315f-466f-8c46-9ba0a206d816" width=700 height=400>

Inverse Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/57ff7645-7d2f-4c08-831a-1b62a106c3fc" width=700 height=400>

https://github.com/user-attachments/assets/c93d7ec4-bda7-4447-9422-729bccf71ebd

### Trial No.4 (75%)
Forward Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/f7ee0502-3991-4672-a434-63e59185723e" width=700 height=400>

Inverse Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/88b7c0a7-73fd-4690-a6b6-77500abeca9a" width=700 height=400>

https://github.com/user-attachments/assets/316b1928-ab05-45fb-b579-741224815a7f

### Trial No.5 (100%)
Forward Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/92b97310-7b4f-4f97-90f1-6a59aeb77b0e" width=700 height=400>

Inverse Kinematics
<p align="center">
<img src="https://github.com/user-attachments/assets/0fa5584c-a5f5-4560-9b53-e0c7606c4a20" width=700 height=400>

https://github.com/user-attachments/assets/b31ea912-6309-45d1-9da4-ec6a48de01a0

## Trial Values
The group manually assigned values to the trial joint variable in MATLAB, ranging from 0% to 100%. These values were entered into the MATLAB simulation, which then automatically generated the corresponding trial position vector using forward kinematics (FK). This trial position vector was then input into a Python-based calculator developed by the group, which performed inverse kinematics (IK) to compute the actual joint variable. The resulting actual joint variable was recorded in the “Actual JV from Python” table. This value was then re-entered into the MATLAB simulation to obtain the actual position vector. Since both the forward and inverse kinematics produced matching results, the comparison confirms that FK = IK.

<p align="center">
<img src="https://github.com/user-attachments/assets/c8251607-d81b-44be-a397-5e77f4cd15c6" width=700 height=900>

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

## Conclusion
This activity focused on analyzing the kinematics of a cylindrical mechanical manipulator using both forward and inverse kinematics. The manipulator, defined by three links of equal length, was modeled in MATLAB using Denavit-Hartenberg parameters and simulated through the Robotics Toolbox. Trial joint variables ranging from 0% to 100% were assigned manually and processed through forward kinematics to determine the end-effector's position. These position vectors were then input into a Python-based inverse kinematics calculator developed by the group to solve for the actual joint variables. Re-entering the inverse kinematics results into MATLAB reproduced the original end-effector positions, confirming that the forward and inverse kinematics are accurately implemented and produce consistent results.
