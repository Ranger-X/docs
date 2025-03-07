# Отказоустойчивый сайт с балансировкой нагрузки с помощью {{ network-load-balancer-full-name }}

В этом сценарии описано, как настроить веб-сайт на стеке [LAMP](https://ru.wikipedia.org/wiki/LAMP) ([Linux](https://www.linux.org/), [Apache HTTP Server](https://httpd.apache.org/), [MySQL](https://www.mysql.com/), [PHP](https://www.php.net/)) или LEMP (веб-сервер Apache заменяется на [Nginx](https://www.nginx.com/)) с балансировкой нагрузки через [{{ network-load-balancer-full-name }}](../../network-load-balancer/concepts/index.md) между двумя зонами доступности, защищенный от сбоев в одной зоне.

Чтобы настроить отказоустойчивый веб-сайт с балансировкой нагрузки:

1. [Подготовьте облако к работе](#before-you-begin).
1. [Создайте виртуальные машины с предустановленным веб-сервером](#create-vm).
1. [Загрузите файлы веб-сайта](#upload-files).
1. [Создайте целевую группу](#create-target-group).
1. [Создайте сетевой балансировщик](#create-load-balancer).
1. [Протестируйте отказоустойчивость](#test-availability).

Если сайт вам больше не нужен, [удалите все используемые им ресурсы](#clear-out).

## Подготовьте облако к работе {#before-you-begin}

Перед тем, как разворачивать сервер, нужно зарегистрироваться в {{ yandex-cloud }} и создать платежный аккаунт:

{% include [prepare-register-billing](../../_includes/solutions/_common/prepare-register-billing.md) %}

Если у вас есть активный платежный аккаунт, вы можете создать или выбрать каталог, в котором будет работать ваша виртуальная машина, на [странице облака](https://console.cloud.yandex.ru/cloud).

[Подробнее об облаках и каталогах](../../resource-manager/concepts/resources-hierarchy.md).

Убедитесь, что в вашем каталоге есть сеть с подсетями в [зонах доступности](../../overview/concepts/geo-scope.md) `ru-cental1-a` и `ru-central1-b`. Для этого на странице каталога выберите сервис **{{ vpc-name }}**. Если в списке есть сеть — нажмите на нее, чтобы увидеть список подсетей. Если нужной [сети](../../vpc/operations/network-create.md) или [подсетей](../../vpc/operations/subnet-create.md) нет, создайте их.

### Необходимые платные ресурсы {#paid-resources}

В стоимость поддержки веб-сайта входит:

* плата за диски и постоянно запущенные виртуальные машины (см. [тарифы {{ compute-full-name }}](../../compute/pricing.md));
* плата за использование динамических внешних IP-адресов (см. [тарифы {{ vpc-full-name }}](../../vpc/pricing.md));
* плата за сетевые балансировщики и балансировку трафика (см. [тарифы {{ network-load-balancer-full-name}}](../../network-load-balancer/pricing.md)).

## Создайте виртуальные машины {#create-vm}

Создайте две одинаковые виртуальные машины с предустановленным веб-сервером:

1. На странице каталога в [консоли управления]({{ link-console-main }}) нажмите кнопку **Создать ресурс** и выберите **Виртуальная машина**. 
1. В поле **Имя** введите имя виртуальной машины: `lb-tutorial-web-ru-central1-a`.
1. Выберите зону доступности: `ru-central1-a`.
1. Выберите один публичный образ для обеих виртуальных машин в блоке **Выбор образа/загрузочного диска** на вкладке **Cloud Marketplace**:
  
   * [LEMP](https://cloud.yandex.ru/marketplace/products/yc/lemp) для Linux, nginx, MySQL, PHP;
   * [LAMP](https://cloud.yandex.ru/marketplace/products/yc/lamp) для Linux, Apache, MySQL, PHP.

1. В блоке **Вычислительные ресурсы** укажите параметры:
  
   * **Платформа** — Intel Ice Lake.
   * **vCPU** — 2.
   * **Гарантированная доля vCPU** — 20%.
   * **RAM** — 1 ГБ.
  
1. В блоке **Сетевые настройки** укажите, к какой подсети необходимо подключить виртуальную машину при создании.
1. В поле **Публичный адрес** выберите **Автоматически**.
1. Укажите данные для доступа на виртуальную машину:
  
   * В поле **Логин** введите имя пользователя.
   * В поле **SSH-ключ** вставьте содержимое файла открытого ключа. Если у вас еще нет пары SSH-ключей, [создайте их](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys).

   {% note alert %}

   IP-адрес и имя хоста (FQDN) для подключения к ВМ назначается ей при создании. Если вы выбрали вариант **Без адреса** в поле **Публичный адрес**, вы не сможете обращаться к ВМ из интернета.

   {% endnote %}

1. На странице каталога нажмите кнопку **Создать ресурс** и выберите **Виртуальная машина**.  
1. В поле **Имя** введите имя виртуальной машины: `lb-tutorial-web-ru-central1-b`.
1. Выберите зону доступности: `ru-central1-b`.
1. Выберите один публичный образ для обеих виртуальных машин:
  
   * **LEMP** для Linux, nginx, MySQL, PHP;
   * **LAMP** для Linux, Apache, MySQL, PHP.
  
1. В блоке **Вычислительные ресурсы**:
  
   * **Платформа** — Intel Ice Lake.
   * **vCPU** — 2.
   * **Гарантированная доля vCPU** — 20%.
   * **RAM** — 1 ГБ.
  
1. В блоке **Сетевые настройки** выберите, к какой подсети необходимо подключить виртуальную машину при создании.
1. В поле **Публичный адрес** выберите **Автоматически**.
1. Укажите данные для доступа на виртуальную машину:
  
   * В поле **Логин** введите имя пользователя.
   * В поле **SSH-ключ** вставьте содержимое файла открытого ключа. Пару ключей для подключения по [SSH](../../compute/operations/vm-connect/ssh.md) необходимо создать самостоятельно. Для создания ключей используйте сторонние инструменты, например утилиты `ssh-keygen` в Linux и macOS или PuTTYgen в Windows.
  
1. Нажмите кнопку **Создать ВМ**.

1. Аналогичным образом создайте вторую виртуальную машину `lb-tutorial-web-ru-central1-b` в зоне доступности `ru-central1-b`. Виртуальные машины должны быть созданы из одинаковых образов и их характеристики должны совпадать.

Создание виртуальных машин может занять несколько минут. После того, как виртуальные машины перейдут в статус `RUNNING`, вы можете перейти к следующему шагу и [загрузить файлы веб-сайта](#upload-files).

## Загрузите файлы веб-сайта {#upload-files}

Создайте файл `index.html` для вашего сайта с любым текстом, например:

{% cut "Пример файла index.html" %}

```html
<!DOCTYPE html>
<html>
   <head>
      <title>Hello, world!</title>
   </head>
   <body>
      <p>Hello, world!</p>
   </body>
</html>
```

{% endcut %}

Для виртуальных машин `lb-tutorial-web-ru-central1-a` и `lb-tutorial-web-ru-central1-b` выполните следующее:

1. В [консоли управления]({{ link-console-main }}) перейдите в раздел **{{ compute-name }}** и найдите публичный IP-адрес виртуальной машины.
1. [Подключитесь](../../compute/operations/vm-connect/ssh.md) к виртуальной машине по протоколу SSH.
1. Выдайте права на запись для вашего пользователя на директорию `/var/www/html`:
     
   ```bash
   sudo chown -R "$USER":www-data /var/www/html
   ```

1. Загрузите на каждую виртуальную машину файл `index.html` с помощью [протокола SCP](https://ru.wikipedia.org/wiki/SCP).

   {% list tabs %}

   - Linux/macOS
     ```bash
     scp -r <путь до файла index.html> <имя пользователя ВМ>@<IP-адрес виртуальной машины>:/var/www/html
     ```

   - Windows
     
     С помощью программы [WinSCP](https://winscp.net/eng/index.php) скопируйте файл в директорию `/var/www/html` на виртуальной машине.

   {% endlist %}

## Создайте целевую группу {#create-target-group}

1. В [консоли управления]({{ link-console-main }}) откройте раздел **{{ network-load-balancer-short-name }}** в каталоге, где созданы ВМ.
1. Откройте вкладку **Целевые группы**.
1. Нажмите кнопку **Создать целевую группу**.
1. Введите имя целевой группы, например `lb-tg-tutorial-web`.
1. Отметьте виртуальные машины `lb-tutorial-web-ru-central1-a` и `lb-tutorial-web-ru-central1-b` для добавления в целевую группу.
6. Нажмите кнопку **Создать целевую группу**.

## Создайте сетевой балансировщик {#create-load-balancer}

При создании сетевого балансировщика нужно создать обработчик, на котором балансировщик будет принимать трафик, а также настроить проверку состояния ресурсов в подключенной целевой группе.

Чтобы создать сетевой балансировщик:

1. В [консоли управления]({{ link-console-main }}) откройте раздел **{{ network-load-balancer-short-name }}**.
1. Нажмите кнопку **Создать балансировщик**.
1. Задайте имя балансировщика, например `lb-tutorial-web`.
1. В блоке **Обработчики** нажмите кнопку **Добавить обработчик** и укажите параметры:
    * **Имя обработчика** — `lb-tut-listener-1`.
    * **Порт** — `80`.
    * **Целевой порт** — `80`.
1. Нажмите кнопку **Добавить**.
1. Нажмите переключатель **Целевые группы** и выберите созданную ранее целевую группу `lb-tg-tutorial-web`. Если группа одна, она будет выбрана автоматически.
1. В блоке **Проверка состояния** укажите:
    * **Имя** проверки — `health-check-1`.
    * **Тип** — `HTTP`.
    * **Порт** —`80`.
    * **URL** — `/`.
    * **Время ожидания** — `1`.
    * **Интервал** — `2`.
    * **Порог работоспособности** — количество успешных проверок, после которого виртуальная машина будет считаться готовой к приему трафика: `5`.
    * **Порог неработоспособности** — количество проваленных проверок, после которого на виртуальную машину перестанет подаваться трафик: `5`.
1. Нажмите кнопку **Создать балансировщик**.

## Протестируйте отказоустойчивость {#test-availability}

1. В блоке **Сеть** на странице виртуальной машины в [консоли управления]({{ link-console-main }}) найдите публичный IP-адрес виртуальной машины `lb-tutorial-web-ru-central1-a`.
1. [Подключитесь](../../compute/operations/vm-connect/ssh.md) к виртуальной машине по протоколу SSH.
1. Остановите веб-сервис, чтобы имитировать сбой в работе веб-сервера:

   {% list tabs %}

   - LAMP

     ```bash
     sudo service apache2 stop
     ```

   - LEMP

     ```bash
     sudo service nginx stop
     ```
   {% endlist %}

1. В [консоли управления]({{ link-console-main }}) перейдите в раздел **{{ network-load-balancer-name }}** и выберите созданный ранее балансировщик.
1. В блоке **Обработчики** найдите IP-адрес обработчика. Откройте сайт в браузере, используя адрес обработчика. 

   Несмотря на сбой в работе одного из веб-серверов, подключение должно пройти успешно.
1. После завершения проверки снова запустите веб-сервис:

   {% list tabs %}

   - LAMP

     ```bash
     sudo service apache2 start
     ```

   - LEMP
     ```bash
     sudo service nginx start
     ```

   {% endlist %}

## Как удалить созданные ресурсы {#clear-out}

Чтобы перестать платить за развернутые серверы, [удалите](../../compute/operations/vm-control/vm-delete.md) созданные виртуальные машины `dns-lb-tutorial-web-ru-central1-a` и `dns-lb-tutorial-web-ru-central1-b` и [балансировщик](../../network-load-balancer/operations/load-balancer-delete) `lb-tutorial-web`.

Если вы зарезервировали статический публичные IP-адреса для ВМ, [удалите](../../vpc/operations/address-delete.md) их.
