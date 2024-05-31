# Аппаратура не биндится с Meteor85
## Описание проблемы
RadioMaster Pocket ELRS 3.3.0. Bind фраза стоит. С этой фразой успешно коннекчусь к Meteor 65pro (ELRS 3.3.0, BetaFlight 4.3.0)

Теперь новый Метеор85 на ELRS. BetaFlight 4.4.0.
Bind фразу вбил в BetaFlight configurator. Ту же самую. По кодам проверил.
По идее, если при включенной аппе включу дрон, должен произойти коннект. Коннект не происходит (на экране аппы не появляются столбики)...

Попытался забиндить через кнопку.  
На дроне нажал кнопку (или в Betaflight нажать кнопку) (быстро стал моргать синей и зеленой лампочкой).  
Зашел в покете в ELRS скрипт и нажал Bind.  
Дрон перестал быстро моргать. Но столбики бинда на экране так и не появились. И в BetaFlight нет реакции на стики.

## Решение
Несовпадение частот работы приемника и передатчика.

Смотрел [видео от Петра](https://www.youtube.com/watch?v=CByA9YKPEJI).  
В нем показано, как через CLI посмотреть на частоту приемника в дроне  
`get expresslrs`
Мое значение  
`expresslrs_rate_index = 1`

На [странице производителя](https://support.betafpv.com/hc/en-us/articles/4403742839705-How-to-Bind-with-F4-Betaflight-FC-SPI-ExpressLRS-Receiver) указано  
`250Hz = 1`  
Захожу в настройки модели на покете. Там зафиксирована частота 1000hz
Запускаю lua script ExpressLRS.  
Там Packet Rate стоит `F1000`, что соответствует 1000Hz.  
![alt text](1_Before_(F1000).jpg)
Меняю на 500Hz  
![alt text](2_After_(500Hz).jpg)
Проверяю в модели. Там тоже частота стала 500Hz  

Возвращаюсь в Betaflight и выставляю из командной строки частоту 500Hz:  
```
set expresslrs_rate_index = 0
Save
```
После перезагрузки аппа что-то выругалась, но появились столбики.  
Итого я забиндил аппу и дрон на частоте 500Hz

Выключаю Метеор85 и включаю Метеор65. Тоже забиндился. То есть частоты совпали.  
К слову в Метеор 65 в Betaflight CLI команды для expresslrs не работают. Наверное потому что приемник по UART подключен.