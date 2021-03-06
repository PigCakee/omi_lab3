# Лабораторная работа #3
## 1. С использованием техники обучения Transfer Learning обучить нейронную сеть EfficientNet-B0 (предварительно обученную на базе изображений imagenet) для решения задачи классификации изображений Food-101 с использованием фиксированных темпов обучения 0.01, 0.001, 0.0001

### Результаты обучения
https://tensorboard.dev/experiment/ROO8TdtZSM2GYgJ6bhEqWQ/#scalars

При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_1_(0001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_1_(0001).svg">

При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.
#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_1_(001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_1_(001).svg">

### Анализ результатов:

При темпе обучения 0.0001 наблюдается максимальная точность ~68%, однако график потерь свидетельствует о том, что сеть еще можно обучать дальше (график за 50 эпох не успел пойти вверх). При темпе обучения 0.001 максимальная точность составляет ~67.5%, однако график после 10 эпохи начал идти на убыль, а график функции потерь, в свою очередь, расти. Это свидетельствует о переобучаемости сети. Из вышеперечисленного можно сделать вывод, что наибольшая точность на 50 эпохах была достигнута в случае темпа обучения равного 0.0001. В случае, если увеличивать это значение, то сеть очень быстро начинает переобучаться. В случае с темпом обучения в 0.01 можо ожидать еще большего ухудшения результатов, что подтвердится с следюущих экспериментах.

## 2. Реализовать и применить в обучении следующие политики изменения темпа обучения, а также определить оптимальные параметры для каждой политики
# А. Косинусное затухание (Cosine Decay)
https://tensorboard.dev/experiment/DpDvXmBIRkyrWkuqbPw6Pw/#scalars
В ходе выполнения данного задания проверялся параметр темпа обучения (initial_learning_rate)

При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_2_(0001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_2_(0001).svg">

При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_2_(001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_2_(001).svg">

При темпе обучения 0.01 розовая кривая отображает обучающую выборку, зеленая - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_2_(01).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_2_(01).svg">

**Описание архитектуры:**
 
* Косинусное затухание (Cosine Decay)
```
tf.keras.experimental.CosineDecay(
    initial_learning_rate, decay_steps, alpha=0.0
)
```

* Параметры
```
initial_learning_rate - темп обучения
decay_steps - число шагов затухания, выбрано значение 1000 по примеру https://www.tensorflow.org/api_docs/python/tf/keras/experimental/CosineDecay#example_usage
alpha - ограничение шагов
```
### Анализ результатов
Результаты в ходе выполнения этого эксперимента практически идентичны с результатами прошлого эксперимента. Единственное отличие в значениях: При темпе обучения 0.0001 максимальная точность за 50 эпох достигла ~67.5%, при 0.001 - ~67%, при 0.01 - ~60% (график потерь в этом случае начал расти практически в самом начале обучения, а точность оставалась на примерно одном и том же уровне).

# В. Косинусное затухание с перезапусками (Cosine Decay with restarts)
https://tensorboard.dev/experiment/ZPDGUeu5RimQ714RJ6UDZQ/#scalars
В ходе выполнения данного задания проверялся параметр темпа обучения (initial_learning_rate)

При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_3_(0001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_3_(0001).svg">

При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_3_(001).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_3_(001).svg">

При темпе обучения 0.01 розовая кривая отображает обучающую выборку, зеленая - валидационную.

#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_3_(01).svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_3_(01).svg">

**Описание архитектуры:**
 
* Косинусное затухание с перезапусками (Cosine Decay with restarts)
```
tf.keras.experimental.CosineDecayRestarts(
    initial_learning_rate, first_decay_steps, t_mul=2.0, m_mul=1.0, alpha=0.0,
    name=None
)
```

* Параметры
```
initial_learning_rate - темп обучения
first_decay_steps - число шагов затухания, выбрано значение 1000 по примеру https://www.tensorflow.org/api_docs/python/tf/keras/experimental/CosineDecayRestarts#example_usage
alpha - ограничение шагов
t_mul - количество итераций в i-м периоде
m_mul - начальная скорость обучения i-го периода
```
### Анализ результатов
Результаты в ходе выполнения этого эксперимента практически идентичны с результатами прошлых экспериментов. Единственное отличие в значениях: При темпе обучения 0.0001 максимальная точность за 50 эпох достигла ~68.2%, при 0.001 - ~67.5%, при 0.01 - ~60% (график потерь в этом случае начал расти практически в самом начале обучения, а точность оставалась на примерно одном и том же уровне). Общий вывод таков: наибольший успех касательно максимальной точности показал третий эксперимент с темпом обучения 0.0001, однако разница между экспериментами совсем небольшая. Между темпами обучения 0.0001 и 0.001 разница заключается в максимальной точности и в том факте, что в первом случае максимальная точность за 50 эпох не достигнута, сеть можно обучать и дальше, а во втором случае сеть начала переобучаться. В третьем же случае с темпом обучения 0.01 результаты плачевны: график потерь моментально устремился вверх, а точность на протяжении всех 50 эпох варьировалась вокруг одного и того же значения. 

## Дополнение: графики изменения темпов обучения (объединение в группы предыдущих графиков)
1. Фиксированные темпы:
При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.
При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.
#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_1.svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_1.svg">

2.А. Косинусное затухание
При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.
При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.
При темпе обучения 0.01 розовая кривая отображает обучающую выборку, зеленая - валидационную.
#### epoch_categorical_accuracy
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_2.svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_2.svg">

2. В. Косинусное затухание с перезапусками
При темпе обучения 0.0001 оранжевая кривая отображает обучающую выборку, синяя - валидационную.
При темпе обучения 0.001 красная кривая отображает обучающую выборку, голубая - валидационную.
При темпе обучения 0.01 розовая кривая отображает обучающую выборку, зеленая - валидационную.
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_categorical_accuracy_3.svg">

#### epoch_loss
<img src="https://raw.githubusercontent.com/PigCakee/omi_lab3/main/epoch_loss_3.svg">
