# 实验报告
* 本实验可以分为两部分：针对 ReLU 函数的多项式逼近，以及在密文域下的多项式运算。
## 多项式逼近
* 同态加密的原理是，对于明文 $a,b$ 与加密操作 $Enc$, 解密操作 $Dec$ 有 
$$Dec(Enc(a) + Enc(b)) = a + b$$ 
$$Dec(Enc(a) * Enc(b)) = a * b$$ 
* 但是，$ReLU(a)$ 的操作并不符合同态运算的规律, 因此我们需要用多项式来对 ReLU 进行近似。本实验当中，采取了 泰勒展开式，最小二乘法，Remez 算法对于多项式进行逼近的尝试，其中 Remez 算法的逼近效果最好，在某些最优情况下能够保证整体误差低于 $0.1$, 多数点的误差达到 $0.01$ 量级。
* 对于 Remez 算法的详细过程在这里不进行介绍，可以在以下链接当中找到相关的介绍资料：[1]，[2]。
* 在实验过程中，观察到使用 Remez 算法逼近 ReLU 函数的效果并不好，因此选择逼近其他的能够近似 ReLU 的函数。在本实验中，采用的是 GeLU 函数和 SquarePlus 函数的加权和：
$$f(x) = r * GeLU(x) + (1 - r) * SquarePlus(x)，r \in [0, 1]$$ 
* 其中，
$$GeLU(x) = x * \Phi(x), \Phi(x) = \int_{-\infty}^x \frac{1}{\sqrt{2 \pi }} \exp\left(-\frac{t^2}{2}\right) \, dt,$$
$$SquarePlus(x) = \frac {x + \sqrt{x^2 + b}} 2$$
* 这里的 $b, r$ 都是可调整的参数：见 `Polynomial_Calc/SiLU.h`
### 实验1.1：针对不同多项式逼近算法的逼近效果
对于不同的多项式逼近算法，我们控制其次数相同，控制 $b = 1, r = 0.5$ 的情况下进行实验：




## 参考资料
* [1]: https://www.youtube.com/watch?v=j29rVHCpRUY
* [2]: http://staff.ustc.edu.cn/~tongwh/NA_2023/slides/book.pdf#section.9.6
