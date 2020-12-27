变换矩阵的求解与左右手坐标系，旋转顺序以及旋转方向有关。

 For right-hand coordinate system, the rotation matrix is:
$$
R_x(\theta_x)=
\begin{bmatrix} 
1 & 0 & 0 \\
0 & \cos{\theta_x} & -\sin{\theta_x} \\
0 & \sin{\theta_x} & \cos{\theta_x}
\end{bmatrix} \\
R_y(\theta_y)=
\begin{bmatrix}
\cos{\theta_y} & 0 & \sin{\theta_y} \\
0 & 1 & 0 \\
-\sin{\theta_y} & 0 & \cos{\theta_y}
\end{bmatrix}\\
R_z(\theta_z)=
\begin{bmatrix}
\cos{\theta_z} & -\sin{\theta_z} & 0 \\
\sin{\theta_z} & \cos{\theta_z} & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
The final rotation matrix is determined by the rotation sequence. For example, the sequence is ZYX. Then the rotation matrix $R$:
$$
R = R_x*R_y*R_z
\\= 
\begin{bmatrix} 
1 & 0 & 0 \\
0 & \cos{x} & -\sin{x} \\
0 & \sin{x} & \cos{x}
\end{bmatrix} 
* 
\begin{bmatrix}
\cos{y} & 0 & \sin{y} \\
0 & 1 & 0 \\
-\sin{y} & 0 & \cos{y}
\end{bmatrix}
*
\begin{bmatrix}
\cos{z} & \sin{z} & 0 \\
-\sin{z} & \cos{z} & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
For left-handed coordinate system, the rotation matrix is:
$$
R_x(\theta_x)=
\begin{bmatrix} 
1 & 0 & 0 \\
0 & \cos{\theta_x} & \sin{\theta_x} \\
0 & -\sin{\theta_x} & \cos{\theta_x}
\end{bmatrix} \\
R_y(\theta_y)=
\begin{bmatrix}
\cos{\theta_y} & 0 & -\sin{\theta_y} \\
0 & 1 & 0 \\
\sin{\theta_y} & 0 & \cos{\theta_y}
\end{bmatrix}\\
R_z(\theta_z)=
\begin{bmatrix}
\cos{\theta_z} & \sin{\theta_z} & 0 \\
-\sin{\theta_z} & \cos{\theta_z} & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
Maya, OpenGL 使用右手系，DirectX使用左手系

However, the rotation matrix in Unreal Engine 4 is different to the standard rotation matrix:
$$
\begin{bmatrix} 
1 & 0 & 0 \\
0 & \cos{x} & -\sin{x} \\
0 & \sin{x} & \cos{x}
\end{bmatrix} 
* 
\begin{bmatrix}
\cos{y} & 0 & \sin{y} \\
0 & 1 & 0 \\
-\sin{y} & \cos{y} & 0
\end{bmatrix}
*
\begin{bmatrix}
\cos{z} & -\sin{z} & 0 \\
\sin{z} & \cos{z} & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

This is because the design of the coordinate system in Unreal Engine 4 (UE4). The coordinate is not a standard left-hand coordinate system. For a coordinate system, the typical rotation direction is: positive angle yields clockwise rotation about the axis when looking along the axis from origin. However, this rule applies to Pitch (Y) and Roll (X) but Yaw(Z) is on the contrary. Therefore, the rotation matrix for Yaw is different to the standard one. 

The rotation sequence in UE4 Editor is XZY.





​		