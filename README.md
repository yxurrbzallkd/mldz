# Зважена лінійна регресія

## Завдання a

Покажіть, що

$J(\theta) = {1\over 2}\sum_{i-1}^m(\omega^{(i)}(\theta^Tx^{(i)}-y^{(i)})^2)$

може бути записана отак

$J(\theta)=(X\theta -\vec y)^TW(X\theta - \vec y)$

Поясніть, що таке матриця W і які її коефіцієнти.

## Розв'язок

Розпишемо цю формулу, я одразу роблю сміливе припущення щодо вмісту матриці W:
$$
(\begin{pmatrix}
x_1\\x_2\\...\\
\end{pmatrix}
\begin{pmatrix}
\theta_1\\\theta_2\\...\\
\end{pmatrix}
-
\begin{pmatrix}
y_1\\y_2\\...\\
\end{pmatrix})
\begin{pmatrix}
\omega_1, 0, 0,\dots\\
0, \omega_2, 0, \dots\\
...\\
\end{pmatrix}
(\begin{pmatrix}
x_1\\x_2\\...\\
\end{pmatrix}
\begin{pmatrix}
\theta_1\\\theta_2\\...\\
\end{pmatrix}
-
\begin{pmatrix}
y_1\\y_2\\...\\
\end{pmatrix})
$$
Перемножимо в дужках:
$$
=
\begin{pmatrix}
x_1\theta_1-y_1\\x_2\theta_2-y_2\\...\\
\end{pmatrix}^T
\begin{pmatrix}
\omega_1, 0, 0,\dots\\
0, \omega_2, 0, \dots\\
...\\
\end{pmatrix}
\begin{pmatrix}
x_1\theta_1-y_1\\x_2\theta_2-y_2\\...\\
\end{pmatrix}
$$
Перемножимо правий вектор і матрицю W:
$$
=
\begin{pmatrix}
x_1\theta_1-y_1\\x_2\theta_2-y_2\\...\\
\end{pmatrix}^T
\begin{pmatrix}
(x_1\theta_1-y_1)\omega_1\\(x_2\theta_2-y_2)\omega_2\\...\\
\end{pmatrix}
$$
Перемножимо вектор справа на "горизонтальний" (транспонований) вектор зліва - перемножити відповідні елементи і додати:
$$
=
(x_1\theta_1-y_1)^2\omega_1+(x_2\theta_2-y_2)^2\omega_2+...\\
$$
Завдання майже зроблено, W це діагональна матриця, елементи діагоналей - коефіцієнти-ваги кожного "рядочка" тренувальних даних - $\omega_i$, ця матриця це матриця зважування.

## Завдання b

Виведіть вираз для знаходження 𝜃 у зваженій лінійній регресії. 
Знайдіть градієнт ∇𝜃
𝐽(𝜃) і, прирівнявши його до нуля, виведіть 
нормальне рівняння для знаходження 𝜃. Вираз буде залежати від 𝑋, 
𝑊 і 𝑦⃗ 

## Розв'язок

$$
{\delta J(\theta)\over \delta \theta} = {\delta ((x_1\theta_1-y_1)^2\omega_1+(x_2\theta_2-y_2)^2\omega_2+...)\over \delta \theta} = 0\\
\equiv  2(x_1\theta_1 - y_1)\omega_1x_1 + 2(x_2\theta_2-y_2)\omega_2x_2 + ... = 0\\
\equiv X^TW(X\theta-\vec y)=0\\
\equiv X^TWX\theta = XW\vec y\\
\equiv \theta = (X^TWX)^{-1}(XW\vec y)
$$

# Регресія Пуассона та сімейство експоненціальних моделей

Ви маєте задачу: передбачити кількість звернень у службу підтримки  вашого сайту в певний день. У службу підтримки за день звертається  цілочисельна кількість людей, яких зазвичай не більше 7–10, тому ви  вирішили використовувати розподіл Пуассона для моделювання таких 
звернень.

## Завдання a

Розподіл імовірностей Пуассона має вигляд:

$P(y, \lambda) = {e^{-\lambda}\lambda^y\over 𝑦!}$
Покажіть, що розподіл Пуассона належить до експоненціального 
сімейства і вкажіть, чому дорівнюють $b(y), \eta, T(\eta), a(\eta)$

## Розв'язок

${1\over y!}e^{y\log\lambda - \lambda}$

$P(Y|\eta) = h(Y)e^{\eta^T T(Y) - a(\eta)}$

$$
b(y) = {1\over y!}\\
\eta = \log\lambda\\
a(\eta) = \lambda\\
T(\eta) = y
$$

## Завдання б

Якою буде канонічна функція відгуку (canonical response 
function) для цього розподілу

## Розв'язок

Для розподілу Пуасона $\mu = e^{\eta}$, $\lambda = e^{\eta}=e^{\log \lambda}$ - правильно

## Завдання с

Для навчальної вибірки $\{(x^{(i)}, y^{(i)}), i = 1,...,m\}$ логарифмічна функція правдоподібності (log-likelihood) буде: $l(\theta)=\log{P(y^{(i)}|x^{(i)}, \theta)}$ Виведіть похідну ${\delta \over \delta \theta_j}l(\theta)$ та сформулюйте правило оновлення ваги $\theta_j$ методом стохастичного градієнтного підйому, якщо $y$ має розподіл Пуассона та канонічну функцію відгуку.

## Розв'язок


Канонічна функція відгуку длярозподілу Пуасона - $\mu = \lambda$

${d\over d\theta_j}{\ln {e^{-\theta}\theta^x\over x!}} = \\
{\ln {e^{-\theta + x\ln \theta}\over x!}} =\\
{x!\over e^{-\theta+x\ln \theta}}{e^{-\theta + x\ln \theta}\over x!}(-1 + {x\over \theta}) = \\
{x\over \theta}-1
$

Ми маусимізуємо Log-likelyhood, тому правило градієнтного підйому буде $\theta := \theta + ({x\over \theta} - 1)$

# Зважена логістична регресія

Ваша задача – модифікувати логістичну регресію таким чином, щоб вона
передбачала якомога точніше найближчі точки до точки запиту (query
point), аналогічно зваженій лінійній регресії.

Для обрахунку вагових коефіцієнтів ми будемо використовувати таку саму
формулу, яку використовували для зваженої лінійної регресії, записану у
векторній формі:

$\omega^{(i)} = \exp{(-{(x^{(i)}-x)^T(x^{(i)}-x) \over 2\tau^2})}$

### a)

Виведіть формулу функції втрат (cost function) для зваженої логістичної регресії.

hypothesis is $h_{\theta}(x)=g(\theta^Tx)={1\over 1 + e^{-\theta^Tx}}$

objection is to maximize likelihood of data, which, for regular logistic regression is $L(\theta)=\prod_{i}p_i^{y_i}(1-p_i)^{1-y_i}$, $p_i = h_{\theta}(x)$, and for weighted logistic regression it is known to be $L(\theta)=\prod_{i}(p_i^{y_i}(1-p_i)^{1-y_i})^{w_i}$

$J = \ln L(\theta) = \ln(({1\over 1+e^{-\theta^Tx}})^{w_iy_i})+\ln(({1 - {1\over 1+e^{-\theta^Tx}}})^{w_i(1-y_i)}) = w_i (y_i\ln({1\over 1+e^{-\theta^Tx}})+(1-y_i)\ln({1 - {1\over 1+e^{-\theta^Tx}}})$

$\ln({1\over 1+e^{-\theta x}}) =-\ln(1+e^{-\theta x})$

$\ln({1 - {1\over 1+e^{-\theta x}}}) = \\
\ln({e^{-\theta x} \over 1 + e^{-\theta x}}) =\\
\ln (e^{-\theta x}) + \ln (1 + e^{-\theta x}))\\
-\theta x - \ln(1+ e^{-\theta x})
$

$J = -w_iy_i\ln(1+e^{-\theta x}) - \theta xw_i (1-y_i) - w_i(1-y_i)\ln(1+e^{-\theta x}) =\\
\ln(1+e^{-\theta x})w_i (-y_i - 1 + y_i) - \theta xw_i (1-y_i) =\\ -w_i\ln (1 + e^{-\theta x}) - \theta x w_i (1 - y_i)$

But usually this oversimplification is not done, the log's of $h_{\theta}(x)$ and $1-h_{\theta}(x)$ are not simplified further and just left as they are. Also, usuallty in the relevant literature a regularization term is added - ${\lambda \over 2}\theta^T \theta$. And we obtain:

$J(h_{\theta}(x), y) = -{\lambda \over 2}\theta^T\theta+\sum_i w_i(y\ln(h_{\theta}(x)) + (1-y)\ln(1-h_{\theta}(x))) =\\ -{\lambda \over 2}\theta^T\theta+\sum_i-w_iy_i\ln(h_{\theta}(x_i)) - w_i(1-y_i)\ln(1-h_{\theta}(x)) = \\
{\lambda \over 2}\theta^T\theta-\sum_i w_iy_i\ln(h_{\theta}(x_i)) + w_i(1-y_i)\ln(1-h_{\theta}(x)) = \\
{\lambda \over 2}\theta^T\theta-\sum_i w_i[y_i\ln({1\over 1+e^{-\theta x}}) + (1-y_i)\ln(1-{1\over 1+e^{-\theta x}})]$

### b)

Виведіть правило оновлення ваг 𝜃 для зваженої логістичної регресії методом градієнтного спуску.

We need to find derivative of the cost function with respect to $\theta$

$J = w_iy_i\ln ({1\over 1 + e^{-\theta x}}) + w_i(1-y_i)\ln(1 - {1\over 1 + e^{-\theta x}})$

$$
{dJ\over d\theta} = {d\over d\theta}(w_iy_i\ln ({1\over 1 + e^{-\theta x}}) + w_i(1-y_i)\ln(1 - {1\over 1 + e^{-\theta x}})) = \\
-w_iy_i {d\over d\theta}\ln (1+e^{-\theta x}) + w_i(1-y_i){d\over d\theta}\ln({e^{-\theta x}\over 1 + e^{-\theta x}}) = \\
-w_iy_i ({e^{-\theta x}(-x)\over {1+e^{-\theta x}}}) + w_i(1-y_i){d\over d\theta}(\ln(e^{-\theta x}) - \ln(1+e^{-\theta x})) = \\
{w_i y_i e^{-\theta x} x \over 1+e^{-\theta x}} + w_i(1-y_i)(-x) - w_i(1-y_i){e^{-\theta x}(-x)\over 1+e^{-\theta x}} = \\
{w_i y_i e^{-\theta x} x \over 1+e^{-\theta x}}-xw_i(1-y_i) + w_i(1-y_i){xe^{-\theta x}\over 1+e^{-\theta x}} = \\
{xe^{-\theta x}\over 1+e^{-\theta x}}w_i(y_i + 1 - y_i) -xw_i(1-y_i) = \\
xw_i({e^{-\theta x}\over 1 + e^{-\theta x}} - (1-y_i))
$$

therefore, the gradient will be

$$
\nabla J_{\theta} = \sum_{i} (x_iw_i({e^{-\theta x_i}\over 1 + e^{-\theta x_i}} - (1-y_i))) 
\\ \rightarrow\\
{dJ\over d\theta} = {d\over d\theta}(w_iy_i\ln ({1\over 1 + e^{-\theta x}}) + w_i(1-y_i)\ln(1 - {1\over 1 + e^{-\theta x}}))\\
w_+y_i{d\over d\theta}\ln {1\over 1 + e^{-\theta x}} + w_-(1-y_i){d\over d\theta}\ln(1-{1\over 1+e^{-\theta x}})=\\
w_+y_i({xe^{-\theta x} \over 1+e^{-\theta x}}) + w_-(1-y_i)(-x +{xe^{-\theta x} \over 1 + e^{-\theta x}})
{d\over d\theta}(-w_i\ln (1 + e^{-\theta x}) - \theta x w_i (1 - y_i)) = \\
-w_i {xe^{-\theta x}\over 1+e^{-\theta x}} - xw_i(1-y_i) = \\
w_ix({e^{-\theta x}\over 1+e^{-\theta x}} - 1 + y_i) = \\
w_ix(y_i - {1\over 1 + e^{-\theta x}}) \\ \rightarrow \\
\nabla J_{\theta} = X^TW(y - h_{\theta}(x))
$$

### c)

Виведіть рішення зваженої логістичної регресії методом нормальних рівнянь.

set $\nabla J = 0$

$$
\nabla J_{\theta} = X^TW(y - h_{\theta}(X)) = 0\\
X^TW(y - h_{\theta}(X)) = 0\\
X^TWh_{\theta}(X) = X^TWy\\
h_{\theta}(x) = W^{-1}((X^T)^{-1})X^TWy\\
{1\over 1 + e^{-\theta x}} = W^{-1}((X^T)^{-1})X^TWy\\
1+e^{-\theta x} = {1\over W^{-1}((X^T)^{-1})X^TWy}\\
e^{-\theta x} = {1 \over W^{-1}((X^T)^{-1})X^TWy} - 1\\
-X\theta^T = \ln ({1\over W^{-1}((X^T)^{-1})X^TWy} - 1)\\
\theta^T = (-X^{-1})\ln ({1\over W^{-1}((X^T)^{-1})X^TWy} - 1)
$$


# Масштабування ознак в лінійній регресії

Ви побудували лінійну регресію для передбачення витрат палива на 100 км.  шляху. Як ознаки (features) ви використали вагу автомобіля з пасажирами,  об’єм двигуна та швидкість в кілометрах на годину. Після впровадження  моделі у виробництво виявилось, що ознака швидкості приходить не в  кілометрах на годину, а в милях на годину. Ваша модель вже реалізована на  мікросхемі, змінити її чи формат даних, які поступають на вхід, дуже дорого.  Проте, змінити передбачення перед тим, як видавати його користувачу, - просто і дешево. Як можна модифікувати передбачення так, щоб воно було  коректним?



## Розв'язок

Маємо передбачення P - літрів палива на 100 кілометрів

$P = \beta_0 + \beta_1 * weight + \beta_2 * volume + \beta_3 * speed_{km/h}$

Позначимо $l$ - кількість кілометрів у милі

${speed_{m/h} * l} = speed_{km/h}$

Якщо нам відомі всі коефіцієнти моделі, можна відняти неправильно порахований доданок, який містить швидкість і додати правильний, нове передбачення $P'$:

$P' = P - \beta_3 * speed_{m/h} + \beta_3 * {speed_{m/h} * l}$

