---
## Front matter
title: "Отчёт по лабораторной работе №5"
subtitle: "Эмуляция и измерение потерь пакетов в глобальных сетях"
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

Основной целью работы является получение навыков проведения интерактивных экспериментов в среде Mininet по исследованию параметров сети, связанных с потерей, дублированием, изменением порядка и повреждением
пакетов при передаче данных. Эти параметры влияют на производительность протоколов и сетей.

# Выполнение лабораторной работы

1. Запустила виртуальную среду с mininet и исправила права запуска X-соединения.

2. Настройка простейшей топологии и проверка подключение между хостами h1 и h2

![Права запуска X-соединения](image/19.png){width=80% height=80%}

![Информация о сетевом интерфейсе и IP-адресе h1](image/1.png){width=80% height=80%}

![Информация о сетевом интерфейсе и IP-адресе h2](image/2.png){width=80% height=80%}

![Проверка подключение от h1 к h2](image/3.png){width=80% height=80%}

Минимальное, среднее, максимальное и стандартное отклонение $min=0.038, avg=0.332, max=1.631, mdev=0.582$.

![Проверка подключение от h2 к h1](image/4.png){width=80% height=80%}

Минимальное, среднее, максимальное и стандартное отклонение $min=0.039, avg=0.162, max=0.732, mdev=0.254$.

3.  Добавление потери пакетов на интерфейс, подключённый к эмулируемой глобальной сети

![Добавление 10% потери пакетов на хосте h1](image/5.png){width=80% height=80%}

![Проверка подключение](image/6.png){width=80% height=80%}

4. Добавление 10% потери пакетов на хосте h2 и проверка подключение между хостами h1 и h2 используя команду ping с параметром -c 100 с хоста h1: 

![Добавление 10% потери пакетов на хосте h2](image/8.png){width=80% height=80%}

5. Восстановила конфигурацию по умолчанию, удалив все правила и проверила соединения:

![Восстановила конфигурацию](image/9.png){width=80% height=80%}

6. Добавила на интерфейсе узла h1 коэффициент потери пакетов 50% , и каждая последующая вероятность зависит на 50% от последней и проверка подключение между хостами h1 и h2 используя команду ping с параметром -c 50:

![Добавление значения корреляции](image/10.png){width=80% height=80%}

7. Добавила повреждения пакетов в эмулируемой глобальной сети и проверка конфигурацию с помощью инструмента iPerf3:

![ Добавление повреждения пакетов](image/11.png){width=80% height=80%}

8. Добавила переупорядочивания пакетов в интерфейс подключения к эмулируемой глобальной сети проверка подключение между хостами h1 и h2 используя команду ping с параметром -c 20:

![ Добавление переупорядочивания пакетов](image/12.png){width=80% height=80%}

9. Добавила дублирования пакетов в интерфейс подключения к эмулируемой глобальной сети

![Добавление дублирования пакетов](image/13.png){width=80% height=80%}

10. Создала каталог, в который будут размещаться файлы эксперимента: 

![Создание каталогов](image/20.png){width=80% height=80%}

11. Добавление потери пакетов на интерфейс, подключённый к эмулируемой глобальной сети:

- Создала скрипт для эксперимента lab_netem_ii.py, Makefile, ping.py:

![Скрипт lab_netem_ii.py](image/14.png){width=80% height=80%}

![ping.py](image/15.png){width=80% height=80%}

![Makefile](image/16.png){width=80% height=80%}

- Выполнила эксперимент:

![Выполните эксперимент](image/21.png){width=80% height=80%}

![График](image/25.png){width=80% height=80%}

###  Задание для самостоятельной работы

1. Реализовала воспроизводимые эксперименты по добавление значения корреляции:

![Скрипт lab_netem_ii.py для добавление значения корреляции](image/26.png){width=80% height=80%}

![Выполнение эксперимент](image/22.png){width=80% height=80%}

![График](image/28.png){width=80% height=80%}

2. Реализовала воспроизводимые эксперименты по добавление  повреждения пакетов:

![Скрипт lab_netem_ii.py для добавление повреждения пакетов](image/29.png){width=80% height=80%}

![Makefile](image/30.png){width=80% height=80%}

![Выполнение эксперимент](image/32.png){width=80% height=80%}

![Повторная передача](image/31.png){width=80% height=80%}

3. Реализовала воспроизводимые эксперименты по добавление переупорядочивания пакетов:

![Скрипт lab_netem_ii.py для добавление переупорядочивания пакетов](image/dupli.png){width=80% height=80%}

![Выполнение эксперимент](image/33.png){width=80% height=80%}

![График](image/35.png){width=80% height=80%}

4. Реализовала воспроизводимые эксперименты по добавление дублирования пакетов:

![Скрипт lab_netem_ii.py для добавление дублирования пакетов](image/36.png){width=80% height=80%}

![Выполнение эксперимент](image/34.png){width=80% height=80%}

![График](image/37.png){width=80% height=80%}

# Листинги  программы

### Скрипт lab_netem_ii.py 

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

        net = Mininet( controller=Controller, waitConnected=True )

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
        h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem loss 10%' )
        h2.cmdPrint( 'tc qdisc add dev h2-eth0 root netem loss 10%' )

        time.sleep(10) # Wait 10 seconds

        info( '*** Ping\n')
        h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" | 
        awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
        -e \'s/icmp_seq=//g\' > ping.dat' )

        info( '*** Stopping network' )
        net.stop()

if __name__ == '__main__':
        setLogLevel( 'info' )
        emptyNet()
```

### Скрипт lab_netem_ii.py для добавление значения корреляции correlation-drop

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

        net = Mininet( controller=Controller, waitConnected=True )

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
        h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem loss 50% 50%' )

        time.sleep(10) # Wait 10 seconds

        info( '*** Ping\n')
        h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" | 
        awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
        -e \'s/icmp_seq=//g\' > ping.dat' )

        info( '*** Stopping network' )
        net.stop()

if __name__ == '__main__':
        setLogLevel( 'info' )
        emptyNet()
```
### Скрипт lab_netem_ii.py для добавление повреждения пакетов corruption-drop:

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

        net = Mininet( controller=Controller, waitConnected=True )

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
        h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem corrupt 0.01%' )

        info( '*** Traffic generation\n' )
        h2.cmdPrint( 'iperf3 -s -D -1' )
        time.sleep(10) # Wait 10 seconds for servers to start
        h1.cmdPrint( 'iperf3 -c', h2.IP(), '-J > iperf_result.json' )

        info( '*** Ping\n')
        h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" | 
        awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
        -e \'s/icmp_seq=//g\' > ping.dat' )

        info( '*** Stopping network' )
        net.stop()

if __name__ == '__main__':
        setLogLevel( 'info' )
        emptyNet()
```
### Скрипт lab_netem_ii.py для добавление переупорядочивания reorder-drop:

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

        net = Mininet( controller=Controller, waitConnected=True )

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
        h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem delay 10ms reorder 25% 25%' )

        time.sleep(10) # Wait 10 seconds

        info( '*** Ping\n')
        h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" | 
        awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
        -e \'s/icmp_seq=//g\' > ping.dat' )

        info( '*** Stopping network' )
        net.stop()

if __name__ == '__main__':
        setLogLevel( 'info' )
        emptyNet()
```

### Скрипт lab_netem_ii.py для добавление дублирования пакетов:

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

        net = Mininet( controller=Controller, waitConnected=True )

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
        h1.cmdPrint( 'tc qdisc add dev h1-eth0 root netem duplicate 50%' )

        time.sleep(10) # Wait 10 seconds

        info( '*** Ping\n')
        h1.cmdPrint( 'ping -c 100', h2.IP(), '| grep "time=" | 
        awk \'{print $5, $7}\' | sed -e \'s/time=//g\' 
        -e \'s/icmp_seq=//g\' > ping.dat'>

        info( '*** Stopping network' )
        net.stop()

if __name__ == '__main__':
        setLogLevel( 'info' )
        emptyNet()
```

### Makefile

```txt
all: ping.dat ping.png ping.check

ping.dat:
        sudo python lab_netem_ii.py
        sudo chown mininet:mininet ping.dat

ping.png: ping.dat
        ./ping_plot

ping.check:
        sudo python ping.py > ping.txt
        cat ping.txt

clean:
        -rm -f *.dat *.txt
```

### Скрипт ping.py для вывода информации о потерянных пакетах

```python
def analyze_results(file_path='ping.dat', total_packets=100):
        with open(file_path, 'r') as f:
                lines = f.readlines()

        received_packets = set(int(line.split()[0]) for line in lines)
        lost_packets = set(range(1, total_packets + 1)) - received_packets

        lost_packets_count = len(lost_packets)
        loss_percentages = (lost_packets_count / total_packets) * 100

        print(f'Total packets: {total_packets}')
        print(f'Lost packets: {lost_packets_count}')
        print(f'Lost packet numbers: {sorted(list(lost_packets))}')
        print(f'Loss percentage: {loss_percentages:.2f}%')

if __name__ == '__main__':
        analyze_results()

def analyze_results(file_path='ping.dat', total_packets=100):
        with open(file_path, 'r') as f:
                lines = f.readlines()

        received_packets = set()
        duplicated_packets = set()
        packet_numbers = []

        for line in lines:
                packet_number = int(line.split()[0])

                if packet_number in received_packets:
                        duplicated_packets.add(packet_number)
                else:
                        received_packets.add(packet_number)

                packet_numbers.append(packet_number)

        lost_packets = set(range(1, total_packets + 1)) - received_packets

        lost_packets_count = len(lost_packets)
        duplicated_packets_count = len(duplicated_packets)
        loss_percentages = (lost_packets_count / total_packets) * 100

        print(f'Total packets: {total_packets}')
        print(f'Lost packets: {lost_packets_count}')
        print(f'Lost packet numbers: {sorted(list(lost_packets))}')
        print(f'Duplicated packets: {duplicated_packets_count}')
        print(f'Duplicated packet numbers: {sorted(list(duplicated_packets))}')
        print(f'Loss percentage: {loss_percentages:.2f}%')

if __name__ == '__main__':
        analyze_results()
```

# Вывод

Получила навыков проведения интерактивных экспериментов в среде Mininet по исследованию параметров сети, связанных с потерей, дублированием, изменением порядка и повреждением пакетов при передаче данных. Эти параметры влияют на производительность протоколов и сетей.
