# 車輪型移動ロボットのハードウェア構成
## PWNのキャリア周波数
pwm制御はONOFFの割合の平均で電圧を制御する．
そのONOFFの周波数をキャリア周波数という．
逆数にすることで何秒ごとにONOFFしているかわかる．

# オドメトリによる事故位置推定推定の数理モデル
## 実時間
制御に必要な時間内ということ．
## 減速比
モータが何回転して車輪が一回転するかの値
## 角速度の式の意味
$$
\omega = \frac{v_R - v_L}{T}
$$

まず左右の速度の差が回転を生み出す
そして回転する幅が小さいと回りやすく，大きいと回りずらくなるのでTで割っている

## 非ホロノミック拘束
瞬間的に移動できる方向に制限があること

## $\dot{x}\sin\theta-\dot{y}\cos\theta = 0$の理由
移動体の位置が$x, y$で姿勢角が$\theta$のとき
前方向の単位ベクトルは
$$
\begin{bmatrix}
\cos\theta \\
\sin\theta
\end{bmatrix}
$$

横方向の単位ベクトルはそれぞれ90度回転させるので
$$
\begin{bmatrix}
\cos\left(\theta + \frac{\pi}{2}\right)\\
\sin\left(\theta + \frac{\pi}{2}\right)
\end{bmatrix}
$$

つまり
$$
\begin{bmatrix}
-\sin\theta \\
\cos\theta
\end{bmatrix}
$$
になる．
$$
\begin{bmatrix}
\dot{x} \\
\dot{y}
\end{bmatrix}
$$
は移動体の速度ベクトルでありこの二つの内積が移動体の横方向の速度のでありそれが非ホロノミック拘束により0なので
$$
-\dot{x}\sin\theta + \dot{y}\cos\theta = 0
$$
となり，
符号を入れ替えると
$$
\dot{x}\sin\theta-\dot{y}\cos\theta = 0
$$
となる．
式的な意味は横滑りしないということ

# 直線追従制御
## $\omega_{ref}(t+\Delta t) = \omega(t) + \Delta t \left(-K_1 d(t)-K_2 \theta_e(t)-K_3 \omega(t)\right)$なんで右式の二項目全部マイナスなのか
全て誤差を戻す方向に働くから．ばねの働きと一緒

## $$d=(x_{ref}-x_{odm})\sin\theta_{ref}-(y_{ref}-y_{odm})\cos\theta_{ref}$$これ非ホロノミック拘束の式と似てるよね
dは横方向の誤差であり符号が逆なのは移動体の左右どっちを正とするかで変わる．