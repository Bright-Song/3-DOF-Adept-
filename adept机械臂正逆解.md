Adept机械臂正逆学求解

# 一、正运动学

```matlab
function [x,y,z] = forward_kinematics(theta1,theta2,theta3)

l1 = 100;
l2 = 50;
x = l1*cos(theta1)+l2*cos(theta1+theta2);
y = l1*sin(theta1)+l2*sin(theta1+theta2);
z = theta3 + 150;
```

# 二、逆运动学

几何法求解逆运动学

```matlab
function [theta1,theta2,theta3] = inverse_kinematics(x,y,z)

l1 = 100;
l2 = 50;
beta = atan2(y,x);
theta = acos((x^2+y^2+l1^2-l2^2)/(2*l1*sqrt(x^2+y^2)));
theta1=beta-theta;
theta2 = acos((x^2+y^2-l1^2-l2^2)/(2*l1*l2));
theta3 = z-150;

```



代数法求解逆运动学

```matlab
function [theta1,theta2,theta3] = inverse_kinematics(x,y,z)

l1 = 100;
l2 = 50;

theta2 = acos((x^2+y^2-l1^2-l2^2)/(2*l1*l2));

k1=l1+l2*cos(theta2);
k2=l2*sin(theta2);

theta1=atan2(y,x)-atan2(k2,k1);


theta3 = z-150;
```



