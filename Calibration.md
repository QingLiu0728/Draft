内参矩阵：
$$
\begin{bmatrix}
f_x & \beta & u_0 & 0 \\
0 & f_y & v_0 & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
 =
\begin{bmatrix}
\frac 1{dx} & \beta & u_0 \\
0 & \frac 1{dy} & v_0  \\
0 & 0 & 1 
\end{bmatrix}
*
\begin{bmatrix}
f & 0 & 0 & 0 \\
0 & f & 0 & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
$$
内参矩阵由相机的自身物理属性决定，可以根据相机参数推算理论内参。

已知摄像头的焦距为4mm,像片的尺寸大小为640x480，传感器尺寸为5856 μm x 3276 μm，像素大小为3μm x 3μm。
$$
\beta = 0 \\
u_0=\frac {640}{2}=320 \quad v_0=\frac {480}{2}=320 \\
dx = \frac {5.856}{640}=0.00915 \quad dy=\frac {3.276}{480} = 0.006825 \\
fx = \frac f{dx}=\frac 4{0.00915}=437.158 \quad fy = \frac f{dy} = \frac 4{0.006825}=586.081
$$



外参矩阵由摄像机的安装位置决定。

在计算外参矩阵的时候，需要注意左手系和右手系，以及旋转顺序。相同的(roll, yaw, pitch)，在左手系和右手系中，以及不同的旋转顺序下，所得到的旋转矩阵是不相同的。另外，也要注意一些特别的坐标系，比如UE4中的坐标系就是一个非标准的左手系，如果不注意到这一点是无法获得准确的旋转矩阵，投影变换就会出现问题。

左手系和右手系的转换：

调换任意两个坐标轴或者将任意一个坐标轴反向(Interchanging the labels of any two axes reverses the handedness. Reversing the direction of one axis (or of all three axes) also reverses the handedness.)

由旋转矩阵R和平移向量T组成：
$$
\begin{bmatrix}
R & T \\
0^T & 1
\end{bmatrix}
$$

$$
\begin{bmatrix}
X_c \\ Y_c \\ Z_c
\end{bmatrix} 
=
\begin{bmatrix}
R
\end{bmatrix}_{3\times3}
\times
\begin{bmatrix}
X \\ Y \\ Z
\end{bmatrix} 
+
\begin{bmatrix}
T_x \\ T_y \\ T_z
\end{bmatrix}
$$

Given point p in homogeneous coordinates:
$$
\begin{bmatrix}
p_x\\p_y\\p_z\\1
\end{bmatrix}
$$

x, y, z are the basic vectors and the O is the origin. A point in the 3D coordinate system can be descripted with:
$$
P_{xyz}=p_x*x+p_y*y+p_z*z+O
$$



在齐次坐标系(Homogeneous Coordinate)下，向量和点在同一个基下就有了不同的表达：3D向量的第4个代数分量是0，而3D点的第4个代数分量是1

Assuming there are two coordinate systems, xyzo and uvwq. The xyzo coordinated can be expressed w.r.t. to uvwq reference frame:
$$
x = \begin{bmatrix}x_u\\x_v\\x_w\\0\end{bmatrix}
y = \begin{bmatrix}y_u\\y_v\\y_w\\0\end{bmatrix}
z = \begin{bmatrix}z_u\\z_v\\z_w\\0\end{bmatrix}
o = \begin{bmatrix}o_u\\o_v\\o_w\\1\end{bmatrix}
$$
Point p(px,py,pz) in xyzo coordinate system can be expressed in uvwq coordinate system:
$$
p_{uvw}=p_x\begin{bmatrix}x_u\\x_v\\x_w\\0\end{bmatrix}
+p_y\begin{bmatrix}y_u\\y_v\\y_w\\0\end{bmatrix}
+p_z\begin{bmatrix}z_u\\z_v\\z_w\\0\end{bmatrix}
+\begin{bmatrix}o_u\\o_v\\o_w\\1\end{bmatrix}
$$

由相机坐标系$(X_c, Y_c, Z_c)$到图像坐标系$(x,y,1)$, 有个透视变化。假定相机焦距为$f$, 根据相似变化原理：
$$
\frac x{X_c}=\frac f{Z_c} \Rightarrow x=\frac {X_c\times f}{Z_c} \\
\frac y{Y_c}=\frac f{Z_c} \Rightarrow y=\frac {Y_c\times f}{Z_c}
$$


图像坐标系到像素坐标系

像素坐标和图像坐标系都在成像平面上，只是各自的原点和单位不一致。

图像坐标的原点为相机光轴与成像平面的交点，通常为成像平面的中点，单位为mm。

像素坐标系是指可视化后图片的坐标系，约定为左上角为原点，向右向下为坐标系的正向。

图像坐标与像素坐标志坚的转换方程为：
$$
u=\frac x{dx}+u_0 \quad v = \frac y{dy} + v_0
$$


整个转换过程：
$$
Z_c\begin{bmatrix}u \\ v \\1 \end{bmatrix} =
\begin{bmatrix}
\frac 1{dx} & \beta & u_0 \\
0 & \frac 1{dy} & v_0  \\
0 & 0 & 1 
\end{bmatrix}
*
\begin{bmatrix}
f & 0 & 0 & 0 \\
0 & f & 0 & 0 \\
0 & 0 & 1 & 0
\end{bmatrix}
*
\begin{bmatrix}
R & T \\
0^T & 1
\end{bmatrix}
*
\begin{bmatrix}
X_w\\Y_w\\Z_w\\1
\end{bmatrix}
$$
(u, v) 是像素坐标，(x,y)是图像坐标系坐标。$d_x, d_y$是实际像素大小。

