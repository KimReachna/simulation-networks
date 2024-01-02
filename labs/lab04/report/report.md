---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Эмуляция и измерение задержек в глобальных сетях"
author: "Ким Реачна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Основной целью работы является знакомство с NETEM — инструментом для тестирования производительности приложений в виртуальной сети, а также получение навыков проведения интерактивного и воспроизводимого экспериментов по измерению задержки и её дрожания (jitter) в моделируемой сети в среде Mininet.

# Выполнение лабораторной работы

1. Запустила виртуальную среду с mininet и исправила права запуска X-соединения.

2. Настройка простейшей топологии и проверка соединения между узлами h1 и h2

![Права запуска X-соединения](image/35.png){width=80% height=80%}

![Информация о сетевом интерфейсе и IP-адресе h1](image/1.png){width=80% height=80%}

![Информация о сетевом интерфейсе и IP-адресе h2](image/2.png){width=80% height=80%}

![Проверка соединения от h1 к h2](image/3.png){width=80% height=80%}

Минимальное, среднее, максимальное и стандартное отклонение $min=0.045, avg=0.426, max=2.092, mdev=0.748$.

![Проверка соединения от h1 к h2](image/4.png){width=80% height=80%}

Минимальное, среднее, максимальное и стандартное отклонение $min=0.050, avg=0.315, max=0.918, mdev=0.340$.

3. На хосте h1 добавила задержку в 100 мс и проверила соединения: $min=100.543, avg=100.781, max=101.103, mdev=0.233$

![Добавление задержку в 100 мс на h1](image/5.png){width=80% height=80%}

4. На хосте h2 добавила задержку в 100 мс и проверила соединения: $min=200.392, avg=135.201, max=201.682, mdev=0.449$

![Добавление задержку в 100 мс на h2](image/6.png){width=80% height=80%}

5. Изменила задержку со 100 мс на 50 мс для отправителя h1 и и для получателя h2 и проверила соединения: $min=101.053, avg=101.332, max=101.918, mdev=0.228$

![Добавление задержку в 50 мс на h2](image/8.png){width=80% height=80%}

![Добавление задержку в 50 мс на h1](image/7.png){width=80% height=80%}

6. Восстановила конфигурацию по умолчанию, удалив все правила и проверила соединения: $min=0.050, avg=0.290, max=1.031, mdev=0.346$

![Восстановила конфигурацию по умолчанию для h2](image/10.png){width=80% height=80%}

![Восстановила конфигурацию по умолчанию для h1](image/9.png){width=80% height=80%}

7. Добавила на узле h1 задержку в 100 мс со случайным отклонением 10 мс и проверила соединения: $min=94.499, avg=101.029, max=110.419, mdev=5.781$

![Дрожания задержки](image/11.png){width=80% height=80%}

8. Добавила на интерфейсе хоста h1 задержку в 100 мс с вариацией ±10 мс и значением корреляции в 25% и проверила соединения: $min=96.642, avg=103.190, max=109.136, mdev=5.424$

![Корреляции для джиттера](image/12.png){width=80% height=80%}

9. Установила нормальное распределение задержки на узле h1 в эмулируемой сети и проверила соединения: $min=87.047, avg=98.155, max=108.772, mdev=7.835$

![Распределение задержки в интерфейсе подключения к эмулируемой глобальной сети](image/13.png){width=80% height=80%}

10. Обновила репозитории программного обеспечения на виртуальной машине и установила пакет geeqie и создала каталог, в который будут  размещаться файлы эксперимента: 

![Обновление репозиториев программного обеспечения](image/19.png){width=80% height=80%}

![Установка пакета geeqie](image/20.png){width=80% height=80%}

![Создание каталогов](image/21.png){width=80% height=80%}

11. Провела вопроизводимый эксперимент

![Скрипт lab_netem_i.py](image/14.png){width=80% height=80%}

![Скрипт ping_plot](image/15.png){width=80% height=80%}

![Makefile](image/16.png){width=80% height=80%}

![Выполнение эксперимент](image/24.png){width=80% height=80%}

![График](image/17.png){width=80% height=80%}

- Из файла ping.dat удалите первую строку и заново постройте график: ```make ping.png```

![График после удаления одной строки из ping.dat](image/18.png){width=80% height=80%}

12. Разработала скрипт для вычисления минимального, среднего, максимального и стандартного отклонения времени приема-передачи на основе данных файла ping.dat, добавила правило запуска скрипта в Makefile. 

![Скрипт с выводом значений](image/23.png){width=80% height=80%}

![Запуск](image/25.png){width=80% height=80%}

###  Задание для самостоятельной работы

1. Реализовала воспроизводимые эксперименты по изменению задержки:

![Скрипт lab_netem_i.py для изменения задержки](image/27.png){width=80% height=80%}

![Выполнение эксперимент](image/26.png){width=80% height=80%}

![График](image/28.png){width=80% height=80%}

2. Реализовала воспроизводимые эксперименты по джиттера, значения корреляции для джиттера и задержки:

![Скрипт lab_netem_i.py для джиттера](image/30.png){width=80% height=80%}

![Выполнение эксперимент](image/29.png){width=80% height=80%}

![График](image/31.png){width=80% height=80%}


3. Реализовала воспроизводимые эксперименты распределение задержки:

![Скрипт lab_netem_i.py для распределения времени задержки в эмулируемой глобальной сети](image/33.png){width=80% height=80%}

![Выполнение эксперимент](image/32.png){width=80% height=80%}

![График](image/34.png){width=80% height=80%}

# Листинги  программы

- Скрипт lab_netem_i.py для simple-delay:

```python
#!/usr/bin/env python

"""
Simple experiment.
Output: ping.dat
"""

from mininet.net import Mininet
from mininet.node import Controller
from mininet.cli import CLI
from mininet.log import setLogLevel, info
import time

def emptyNet():
  "Create an empty network and add nodes to it."

  net = Mininet( controller=Controller,waitConnected=True )

  info( '*** Adding controller\n' )
  net.addController( 'c0' )

  info( '*** Adding hosts\n' )
  h1 = net.addHost( 'h1', ip='10.0.0.1' )
  h2 = net.addHost( 'h2', ip='10.0.0.2' )

  info( '*** Adding switch\n' )
  s1 = net.addSwitch( 's1' )

  info( '*** Creating links\n' )
  net.addLink( h1, s1 )
  net.addLink( h2, s1 )

  info( '*** Starting network\n')
  net.start()

  info( '*** Set delay\n')
  h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem delay 100ms' )
  h2.cmdPrint( 'tc qdisc add dev h2-eth0 root netem delay 100ms' )

  time.sleep(10) # Wait 10 seconds

  info( '*** Ping\n')
  h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" 
  | awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
  -e \'s/icmp_seq=//g\' > ping.dat' )

  info( '*** Stopping network' )
  net.stop()

if __name__ == '__main__':
  setLogLevel( 'info' )
  emptyNet()
```

- Скрипт lab_netem_i.py для изменению задержки:

```python
#!/usr/bin/env python

"""
Simple experiment.
Output: ping.dat
"""

from mininet.net import Mininet
from mininet.node import Controller
from mininet.cli import CLI
from mininet.log import setLogLevel, info
import time

def emptyNet():
  "Create an empty network and add nodes to it."

  net = Mininet( controller=Controller,waitConnected=True )

  info( '*** Adding controller\n' )
  net.addController( 'c0' )

  info( '*** Adding hosts\n' )
  h1 = net.addHost( 'h1', ip='10.0.0.1' )
  h2 = net.addHost( 'h2', ip='10.0.0.2' )

  info( '*** Adding switch\n' )
  s1 = net.addSwitch( 's1' )

  info( '*** Creating links\n' )
  net.addLink( h1, s1 )
  net.addLink( h2, s1 )

  info( '*** Starting network\n')
  net.start()

  info( '*** Set delay\n')
  h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem delay 50ms' )
  h2.cmdPrint( 'tc qdisc add dev h2-eth0 root netem delay 50ms' )

  time.sleep(10) # Wait 10 seconds

  info( '*** Ping\n')
  h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" 
  | awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
  -e \'s/icmp_seq=//g\' > ping.dat' )

  info( '*** Stopping network' )
  net.stop()

if __name__ == '__main__':
  setLogLevel( 'info' )
  emptyNet()
```

- Скрипт lab_netem_i.py для джиттера:

```python

#!/usr/bin/env python

"""
Simple experiment.
Output: ping.dat
"""

from mininet.net import Mininet
from mininet.node import Controller
from mininet.cli import CLI
from mininet.log import setLogLevel, info
import time

def emptyNet():
  "Create an empty network and add nodes to it."

  net = Mininet( controller=Controller,waitConnected=True )

  info( '*** Adding controller\n' )
  net.addController( 'c0' )

  info( '*** Adding hosts\n' )
  h1 = net.addHost( 'h1', ip='10.0.0.1' )
  h2 = net.addHost( 'h2', ip='10.0.0.2' )

  info( '*** Adding switch\n' )
  s1 = net.addSwitch( 's1' )

  info( '*** Creating links\n' )
  net.addLink( h1, s1 )
  net.addLink( h2, s1 )

  info( '*** Starting network\n')
  net.start()

  info( '*** Set delay\n')
  h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem delay 100ms 10ms 25%' )
  h2.cmdPrint( 'tc qdisc add dev h2-eth0 root netem delay 100ms' )

  time.sleep(10) # Wait 10 seconds

  info( '*** Ping\n')
  h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" 
  | awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
  -e \'s/icmp_seq=//g\' > ping.dat' )

  info( '*** Stopping network' )
  net.stop()

if __name__ == '__main__':
  setLogLevel( 'info' )
  emptyNet()
```

- Скрипт lab_netem_i.py для распределение задержки: 

```python
#!/usr/bin/env python

"""
Simple experiment.
Output: ping.dat
"""

from mininet.net import Mininet
from mininet.node import Controller
from mininet.cli import CLI
from mininet.log import setLogLevel, info
import time

def emptyNet():
  "Create an empty network and add nodes to it."

  net = Mininet( controller=Controller,waitConnected=True )

  info( '*** Adding controller\n' )
  net.addController( 'c0' )

  info( '*** Adding hosts\n' )
  h1 = net.addHost( 'h1', ip='10.0.0.1' )
  h2 = net.addHost( 'h2', ip='10.0.0.2' )

  info( '*** Adding switch\n' )
  s1 = net.addSwitch( 's1' )

  info( '*** Creating links\n' )
  net.addLink( h1, s1 )
  net.addLink( h2, s1 )

  info( '*** Starting network\n')
  net.start()

  info( '*** Set delay\n')
  h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem delay 100ms 20ms 
  distribution normal' )
  h2.cmdPrint( 'tc qdisc add dev h2-eth0 root netem delay 100ms' )

  time.sleep(10) # Wait 10 seconds

  info( '*** Ping\n')
  h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" 
  | awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
  -e \'s/icmp_seq=//g\' > ping.dat' )

  info( '*** Stopping network' )
  net.stop()

if __name__ == '__main__':
  setLogLevel( 'info' )
  emptyNet()
```

- Скрипт ping_statistic.py:

```python
import statistics

def compute_statistics(ping_data):
    times = [float(line.split()[1]) for line in ping_data]

    min_time = min(times)
    avg_time = statistics.mean(times)
    max_time = max(times)
    std_dev = statistics.stdev(times)
    return min_time, avg_time, max_time, std_dev

def main():
    with open('ping.dat', 'r') as file:
        data = file.readlines()

    min_time, avg_time, max_time, std_dev = compute_statistics(data)

    print(f"Min time: {min_time} ms")
    print(f"Average time: {avg_time} ms")
    print(f"Max time: {max_time} ms")
    print(f"Standard dev: {std_dev} ms")

if __name__ == "__main__":
    main()
```

# Вывод

Я познакомилась с NETEM — инструментом для тестирования производительности приложений в виртуальной сети, а также получение навыков проведения интерактивного и воспроизводимого экспериментов по измерению задержки и её дрожания (jitter) в моделируемой сети в среде Mininet.