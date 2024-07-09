Adept机械臂轨迹规划

# 一、线性规划

```matlab
function [x,y,z] = time(x_goal,y_goal,z_goal,t)

x_init = 0;
y_init = 0;
z_init = 0;

    if t<10
        x = x_init + (x_goal - x_init) * (t / 10);
        y = y_init + (y_goal - y_init) * (t / 10);
        z = z_init + (z_goal - z_init) * (t / 10);
    else
        x = x_goal;
        y = y_goal;
        z = z_goal;
    end
end
```

其中，x_goal,y_goal,z_goal为指定的转角（通过逆运动学求解得到），x,y,x为当前的转动角度

这是线性插值的方法，较为简单，但在起始点与终点机械臂末端速度不为0



# 二、三次多项式插值

```matlab
function [x,y,z] = time(x_goal,y_goal,z_goal,t)

x_init = 0;
y_init = 0;
z_init = 0;

x = x_init+(3/100)*(x_goal-x_init)*(t^2)-(2/1000)*(x_goal-x_init)*(t^3);
y = y_init+(3/100)*(y_goal-y_init)*(t^2)-(2/1000)*(y_goal-y_init)*(t^3);
z = z_init+(3/100)*(z_goal-z_init)*t^2-(2/1000)*(z_goal-z_init)*(t^3);

end
```

x,y,z的求解运用了三次多项式插值的方式，这样在起始点与终点的速度为0，符合现实条件





