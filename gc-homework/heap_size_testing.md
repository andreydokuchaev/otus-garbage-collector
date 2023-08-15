В первой части задания необходимо определить оптимальный размер хипа.

Для этого будем запускать приложение, изменяя размер хипа при помощи параметров,\
пока превышение размера хипа не будет вызывать сокращение времени работы приложения.

Параметры и время работы будем вести в таблице ниже.

| Параметры запуска                                                                                       |              Время работы |
|---------------------------------------------------------------------------------------------------------|--------------------------:|
| -Xms256m -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   |          OutOfMemoryError |
| -Xms280m -Xmx280m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   |  spend msec:20495, sec:20 |
| -Xms2g -Xmx2g -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC       |  spend msec:12829, sec:12 |
| -Xms1g -Xmx1g -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC       |  spend msec:13419, sec:13 |
| -Xms1536m -Xmx1536m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:13107, sec:13 |
| -Xms1792m -Xmx1792m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:12459, sec:12 |
| -Xms1700m -Xmx1700m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:12035, sec:12 |
| -Xms1600m -Xmx1600m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:13178, sec:13 |
| -Xms1650m -Xmx1650m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:13121, sec:13 |
| -Xms1675m -Xmx1675m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:12504, sec:12 |
| -Xms1670m -Xmx1670m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:12909, sec:12 |
| -Xms1665m -Xmx1665m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:12940, sec:12 |
| -Xms1660m -Xmx1660m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC |  spend msec:13624, sec:13 |

Размер хипа равный 1665 мб можно считать оптимальным, так как при дальнейшем увеличении не происходит значительного улучшения быстродействия.

Во второй части задания необходимо оптимизировать работу приложения не изменяя логику работы.

Во время анализа кода мною было обнаружено, что в приложении используется обертка Integer, а не примитив для хранения чисел.\
При этом количество создаваемых объектов достаточно большое. В данном случае можно заменить все обертки на примитивы, не изменяя логику работы.\
После этого количество используемой памяти должно измениться в лучшую сторону.

Проведем анализ используемый памяти, так же как мы это делали в первой части.

| Параметры запуска                                                                                       |           Время работы |
|---------------------------------------------------------------------------------------------------------|-----------------------:|
| -Xms1665m -Xmx1665m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC | spend msec:2980, sec:2 |
| -Xms1536m -Xmx1536m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC | spend msec:2831, sec:2 |
| -Xms1024m -Xmx1024m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC | spend msec:2993, sec:2 |
| -Xms512m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:2891, sec:2 |
| -Xms300m -Xmx300m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:4055, sec:4 |
| -Xms400m -Xmx400m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:3387, sec:3 |
| -Xms450m -Xmx450m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:3335, sec:3 |
| -Xms475m -Xmx475m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:2953, sec:2 |
| -Xms470m -Xmx470m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:3056, sec:3 |
| -Xms256m -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:4119, sec:4 |
| -Xms220m -Xmx220m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./logs/heapdump.hprof -XX:+UseG1GC   | spend msec:4935, sec:4 |

После оптимизации при маленьком размере хипа не появляется OutOfMemoryError. Так же оптимальный размер хипа теперь равен 475 мб,\
что в 3.5 раза меньше, чем раньше. 

Таким образом можно сделать вывод, что оптимизация путем избавления от оберток над примитивами в данном случае помогла значительно\
уменшить размер потребляемой приложением памяти.