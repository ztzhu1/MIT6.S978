讲义: https://mit-6s978.github.io/assets/pdfs/lec2_vae.pdf (lec2_vae.pdf)

要优化的似然函数为

$$
\begin{align}
{\rm argmax}_{\theta}\sum_x p_{\rm data}(x)\log p_{\theta}(x)
\end{align}
$$

在推导时往往会把$\Sigma_x$省略掉，先研究$\log p_{\theta}(x)$的性质，在这样的情况下ELBO被写成了第20页忽略求和符号的形式。由于$q(z)$可以随便取, 自然也可以写成$q_\phi(z|x)$, 在实际应用中, $q_{\phi}$就是神经网络构成的encoder, $\phi$就是encoder神经网络的参数, $x$是给定的输入, $z$是encoder的输出。另外$p_{\theta}(x|z)$也是神经网络构成的decoder, $\theta$是decoder神经网络的参数。PPT 21页的替换自然成立。

另外作业题Problem 2也比较直接
$$
\begin{align}
{\rm ELBO} &= \sum_{x, z}p_{\rm data}(x)q_{\phi}(z|x)\log \frac{p(x|z)p(z)}{q_{\phi}(z|x)}\\
&= \sum_{x, z}p_{\rm data}(x)q_{\phi}(z|x)\log \frac{p(xz)}{q_{\phi}(z|x)}\\
\end{align}
$$

在应用时, ELBO从Eq. (2)改成了Problem 2下面那种求和的形式，发现$p_{\rm data}(x)$和$q_{\phi}(z|x)$没有了, 这是因为对每一个$x_i$, 都可以确定一个$q_{\phi}(z|x_i)$, 简单起见我们认为$z$服从正态分布, $x_i$确定的是正态分布的均值和方差, 再从这个分布中采样出很多$z_{i,j}$，这样在计算后面的求和时, $p_{\rm data}(x)$和$q_{\phi}(z|x)$的分布就天然存在于取数据$x_i$和采样$z_{i,j}$的过程中, 这是蒙特卡洛法模拟中常见的方法。