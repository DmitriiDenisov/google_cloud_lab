# google_cloud_lab
Видео инструкции по подключению: https://www.youtube.com/watch?v=W-FqRBoyTgw&t=897s

Текстовая инструкция: http://amunategui.github.io/fast-gpu-gcloud/

Можно следовать последовательно по инструкции, но после всего надо будет сделать несколько изменений, а именно: 

### Квоты:

По видео-инструкции неправильный запрос квоты. Для верного запроса квоты надо набрать ‘quotas’ и выбрать следующие фильтры: 


![alt-text-1](https://i.ibb.co/C8F82Mh/1.png "title-1")


### Важно:

При установке по его (и чужим) инструкциям происходит установка не поддерживающих друг друга версий CUDA, Cudnn и tensorflow-gpu. Осторожно смотри на версии устанавливаемых CUDA, Cudnn и tensorflow-gpu. Проблема в том, что они между собой не все совместимы. И если установить несовместимые версии, то при импорте tensorflow (уже внутри питона) будет возникать ошибка libcublas.so.10.0: cannot open shared object
Чтобы её избежать следуй таблице: https://www.tensorflow.org/install/source#tested_build_configurations

При этом я пробовал комбинацию из таблицы: CUDA 8, CUdNN 6, tensorflow_gpu-1.4.0 и все равно не работало 
Итоговая конфигурация, при которой у меня заработало: CUDA 9, cuDNN v7.1.4 Runtime Library for Ubuntu16.04 (Deb), tensorflow_gpu-1.12.0

Ссылка на именно эту версию cudnn https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.1.4/prod/9.0_20180516/Ubuntu16_04-x64/libcudnn7_7.1.4.18-1_cuda9.0_amd64


### Итого: 
1) Проследовать и сделать все инструкции с сайта, при этом устанавливать CUDA 9, cuDNN v7.1.4 Runtime Library for Ubuntu16.04 (Deb)
2) sudo pip3 uninstall tensorflow-gpu
3) sudo pip3 install tensorflow-gpu==1.12.0


### Для локального запуска в terminal’e: 
RSA ключи и тд
https://www.youtube.com/watch?v=R8C66NwMJLs

### Для запуска в PyCharm: 
Скорее всего тут потребуется Professional версия. В добавлении интерпретатора выбрать ssh, порт оставить 22, после чего следовать инструкциям. 

![alt-text-1](https://i.ibb.co/jyZFc6c/2.png "title-1") ![alt-text-2]( "title-2")


### Чтобы проверить GPU:
Запустить файл test_gpu.py из этого репозитория



