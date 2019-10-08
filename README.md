# Домашнее задание № 2
## Реализация методов оптимизации

В задании вы сами реализуете несколько алгоритмов оптимизации и примените их к определению космологических параметров Вселенной: параметра Хаббла и доли темной энергии в составе Вселенной.

**Дедлайн 17 октября в 23:55**

Вы должны реализовать следующие алгоритмы в файле `opt.py`:

1. Метод Гаусса—Ньютона в виде функции `gauss_newton(y, f, j, x0, k=1, tol=1e-4)`, где `y` — это массив с измерениями, `f(*x)` — это функция от неивестных параметров, возвращающая значения, рассчитанные в соответствии с моделью, в виде одномерного массива размера `y.size`, `j(*x)` — это функция от неизвестных параметров, возвращающая якобиан в виде двумерного массива `(y.size, x0.size)`, `x0` — массив с начальными приближениями параметров, `k` — положительное число меньше единицы, параметр метода, `tol` — условие сходимости, параметр метода. Функция должна возвращать объект класса `Result`, реализованного в файле `opt.py`
2. Метод Левенберга—Марквардта в фиде функции `lm(y, f, j, x0, lmbd0=1e-2, nu=2, tol=1e-4)`, где все одноимённые аргументы имеют те же значения, что и для `gauss_newton`, `lmbd0` — начальное значение парметра `lambda` метода, `nu` — мультипликатор для параметра `lambda`. Функция должна возвращать объект класса `Result`

Примените методы 1 и 2 к решению задачи об определении космологиических постоянных.
Вам дан файл `jla_mub.txt`, содержащий две колонки: [красное смещение](http://www.astronet.ru/db/msg/1162269) сверхновых и модуль расстояния до них (см. [заметку](http://www.astronet.ru/db/msg/1162269) о космологическом красном смещении).
Модуль расстояния μ задается следующим соотношением:

![модуль расстояния](mu.png)

Здесь d — это фотометрическое расстояние, c — скорость света, H_0 — постоянная Хаббла (обычно выражается в км/с/Мпк), Ω — доля темной энергии в составе Вселененной (от 0 до 1).
В астрономии расстояние часто измеряется в [парсеках](http://www.astronet.ru/db/msg/1162328) (пк), но вам ничего не нужно в них переводить, просто используйте вторую формулу для расстояния, а постоянную Хаббла подставляйте в единицах км/с/Мпк.
В качестве начального приближения используйте значения H_0 = 50, Ω = 0.5.

Вам нужно будет восстановить параметры модели, используя ваши оптимизаторы, в файле `cosmology.py`:
- Загрузить данные из файла `jla_mub.txt`
- Восстановить параметры, используя ваши оптимизаторы, подберите параметры оптимизаторов, которые хорошо подходят для данной задачи.
- Нанести точки из файла на график зависимости μ от z. Там же построить модельную кривую, используя найденные параметры. Сохраните график в файл `mu-z.png`
- На другом графике построить зависимость функции потерь sum(0.5 * (y-f)^2) от итерационного шага для обоих алгоритмов. Сохраните график в файл `cost.png` 
- Выведите в файл `parameters.json` результаты в виде:

```json
{
  "Gauss-Newton": {"H0": 55, "Omega": 0.55, "nfev": 155},
  "Levenberg-Marquardt": {"H0": 45, "Omega": 0.45, "nfev": 145}
}
```

Для численного взятия интеграла рекомендуется использовать функцию `scipy.integrate.quad`. 

**В этом задании запрещено пользоваться готовыми пакетами для оптимизации, в том числе `scipy.optimize`.**
