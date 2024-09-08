# ReLU-encryptor
The summer project for CSNOVA 2024, a homomorphic encryption implementation based on troy-nova for encrypting ReLU function.

## 背景
* 在人工智能领域当中，ReLU 函数是常见的激活函数。有时，出于对数据保护的需求，数据持有者希望在不泄露数据的情况下，计算出持有数据输入激活函数 $f$ 的值 $f(x)$。常见的做法是通过同态加密算法，首先将数据 $x$ 进行同态加密，然后使用可以近似 $f$ 的多项式 $p$ 进行同态加乘运算，最后进行解密得到近似的结果。<br>

* 本项目初步实现了基于 `@Lightbulb(lightbulb128)` 开发的同态加密库 `troy-nova` (https://github.com/lightbulb128/troy-nova.git) 的 ReLU 函数同态加密算法。能够对于区间 $[-5, 5)$ 当中的 $16384$ 个等间距的数进行加密。使用 `<ctime>` 对计算过程进行度量发现，对单个数据进行加密的速度要快于基于同态加密库`heathcliff` 的多方安全计算库 `imp` 的效率。具体的数据将在本文件夹当中的实验报告当中呈现。<br>


## 环境
* 开发环境位于 Ubuntu 22.04 当中，其他的依赖项可以参考 `troy-nova` 的 `readme.md`。

## 使用
* 本实验的目的是探究使用不同次数的多项式逼近下，逼近的效果（精度）以及运行时间（效率）的关系如何。在使用的过程当中，使用者可以自行指定用于逼近 ReLU 函数的多项式次数。
### 演示
* 在本文件夹下运行指令 `./guide.sh`。
* 在命令行当中会出现提示：
```
This is a program that demonstrates how relu function of points evenly distributed between [-5, 5) is calculated.
Input degree for polynomial:
```
* 此时，请输入您希望使用的逼近多项式的次数。请注意，输入的数一定是 $[1, 13]$ 区间的正整数。在不同的机器上，可能会出现过大的正整数导致内存溢出的情况，但该现象还未在实际测试中被观测到。
### 修改运行
* 如果您想修改程序进行测试，请按照以下步骤操作：
    * clone `troy-nova-spu` 至本地：`git clone --branch spu --single-branch git@github.com:lightbulb128/troy-nova.git`
    * 将 `HE_ReLU` 和 `Polynomial_Calc` 防止在 `troy-nova-spu` 下面一级， 即按照下面的文件树：
    * ```
        troy-nova-spu
        ├── HE_ReLU
        └── Polynomial_Calc
        ```
    * 现在，您可以修改代码。修改之后，运行以下指令即可生成可执行程序：
    * ```
        mkdir build
        cd build
        cmake .. -DTROY_RELU=ON
        make troyrelu
        ```
    * 将 `python_script.py` 和 `guide.sh` 放置于 `troy-nova-spu/build/HE_ReLU` 下
    * 运行 `./guide.sh` 即可。
## 更多
* 可以参考 `report`。
