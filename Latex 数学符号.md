> [!Note] 在Mathjax 在Markdown 下的语法指引

### 上，下标
	$ n^2 $

$$w ^{T} +b =b+\sum_{i=1}^n \alpha_i$$
$$\int_a^b f(x) dx$$




### 数学符号
尽管一些基础的符号可以直接键入，但大多数特殊符号需要使用命令来显示。

本书只是数学符号使用的入门教程，LaTeX Wikibook 的数学符号章节是另一个更好更完整的教程。如果想要了解更多关于数学符号的内容请移步。如果你想找到一个特定的符号，可以使用 [Detexfiy](http://detexify.kirelabs.org/)，它可以识别手写字符。

#### 上标和下标

上标（Powers）使用 `^` 来表示，比如 `$n^2$` 生成的效果为 $n^2$ ![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "n^2")。

下标（Indices）使用 `_` 表示，比如 `$2_a$` 生成的效果为 $2_a$.

如果上标或下标的内容包含多个字符，请使用花括号包裹起来。比如 `$b_{a-2}$` 的效果为 $b_{a-2}$。

#### 分数

分数使用 `\frac{numerator}{denominator}` 命令插入。比如 `$$\frac{a}{3}$$` 的生成效果为$$\frac{a}{3}$$

![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\frac{a}{3}")

分数可以嵌套。比如 `$$\frac{y}{\frac{3}{x}+b}$$` 的生成效果为$$\frac{y}{\frac{3}{x}+b}$$

![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\frac{y}{\frac{3}{x}+b}")

#### 根号

我们使用 `\sqrt{...}` 命令插入根号。省略号的内容由被开根的内容替代。如果需要添加开根的次数，使用方括号括起来即可。

例如 `$$\sqrt{y^2}$$` 的生成效果为$$\sqrt{y^2}$$

![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\sqrt{y^2}")

而 `$$\sqrt[x]{y^2}$$` 的生成效果为$$\sqrt[x]{y^2}$$

![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\sqrt[x]{y^2}")

#### 求和与积分[](https://oi-wiki.org/tools/latex/#%E6%B1%82%E5%92%8C%E4%B8%8E%E7%A7%AF%E5%88%86 "Permanent link")

使用 `\sum` 和 `\int` 来插入求和式与积分式。对于两种符号，上限使用 `^` 来表示，而下限使用 `_` 表示。

`$$\sum_{x=1}^5 y^z$$` 的生成效果为$$\sum_{x=1}^5 y^z$$
![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\sum_{x=1}^5y^z")

而 `$$\int_a^b f(x)$$` 的生成效果为$$\int_a^b f(x)$$

![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7 "\int_a^b f(x)")

#### 希腊字母

我们可以使用反斜杠加希腊字母的名称来表示一个希腊字母。名称的首字母的大小写决定希腊字母的形态。例如

| `$\alpha$`              | $\alpha$              |
| ----------------------- | --------------------- |
| `$\beta$`               | $\beta$               |
| `$\delta, \Delta$`      | $\delta, \Delta$      |
| `$\pi, \Pi$`            | $\pi, \Pi$            |
| `$\sigma, \Sigma$`      | $\sigma, \Sigma$      |
| `$\phi, \Phi, \varphi$` | $\phi, \Phi, \varphi$ |
| `$\psi, \Psi$`          | $\psi, \Psi$          |
| `$\omega, \Omega$`      | $\omega, \Omega$      |
| `$\theta, \Theta$`      | $\theta, \Theta$      |

### 其他
| Command       | Symbol      | Command     | Symbol    |
| ------------- | ----------- | ----------- | --------- |
| `$\infty$`    | $\infty$    | `$\int$`    | $\int$    |
| `$\triangle$` | $\triangle$ | `$oint$`    | $\oint$   |
| `\forall`     | $\forall$   | `$prod`     | $\prod$   |
| `emptyset`    | $\emptyset$ | `$\coprod$` | $\coprod$ |
| `$\exists`    | $\exists$   |             |           |
| `$\neg`       | $\neg$      |             |           |
| `$\mho`       | $\mho$      |             |           |
| `$\nabla$`    | $\nabla$    |             |           |
### 空心符号
| `$\mathbb{M}$` | $\mathbb{M}$ |
| -------------- | ------------ |
| `\mathbb{R}`   | $\mathbb{R}$ |

### 实践

1. $$e = mc^2$$

2. $$\pi = \frac{c}{d}$$


3. $$\frac{d}{dx} e^x = e^x$$
4. $$\frac{d}{dx}\int_0^{\infty} f(x)ds = f(x)$$
5. $$f(x) = \sum_i 0^\infty \frac{f^{(i)}(0)}{i!} x^i$$
6. $$x = \sqrt{\frac{x^i}{z} y}$$
7. $$\mathbb{M}$$
$$\begin{bmatrix}1 & x & x^2 \\1 & y & y^2 \\ 1 & z & z^2 \end{bmatrix}$$

$$\begin {cases}
x = 1 \\
y = 2
\end{cases}
$$


