# Waku

**Разбор проекта Waku + инструкция по установке ноды.**

**План:**
- О проекте;
- Разбор инвесторов;
- Требования к серверу;
- Инструкция по установке ноды;
- Выводы

Waku - это набор протоколов для обмена сообщениями, созданных для децентрализованной сети. Он позволяет пользователям общаться между собой без необходимости использования централизованных посредников, обеспечивая при этом частную и безопасную связь. Важно отметить, что Waku является частью более крупной инициативы по созданию децентрализованного интернета. Его основная цель - дать пользователям больше контроля над своей коммуникацией в онлайн-среде и снизить влияние крупных корпораций на интернет.

Виталик Бутерин признал Waku наследником Whisper, оригинального протокола для обмена сообщениями в сети Ethereum. В своем блоге под названием "Make Ethereum Cypherpunk Again" Виталик обсуждает более широкое технологическое видение, в рамках которого существует Ethereum, и поддерживает Waku как реализацию децентрализованного протокола обмена сообщениями, задуманного Гэвином Вудом.

Бутерин напрямую поддерживает проект, а это уже говорит о многом. Давайте пройдемся по аккаунтам Waku в социальных сетях:
В Twitter на проект подписаны представители таких Tier-1 фондов, как **Delphi Digital(инвестировали в Celestia), Paradigm(инвестировали в Blast, Uniswap), a16z(инвестировали в EigenLayer).** На аккаунт также подписан сам Виталик, что еще раз подтверждает его причастность к проекту. На аккаунт подписано почти 5 тысяч человек(дата написания обзора: 15 марта 2024 г.).

Discord проекта не насчитывает большого количества участников и служит больше платформой для помощи пользователям.

У проекта есть Github, в котором находятся инструкции по установке ноды различными способами и различный материал для разработчиков. Узел nwaku на GitHub продемонстрировал непрерывный прогресс, с 46 релизами с ноября 2020 года, что указывает на постоянные усилия по улучшению от сильной команды разработчиков. Также, Waku имеет красивый и простой сайт, с которым удобно взаимодействовать и который содержит в себе всю необходимую информацию для ознакомления с проектом на английском языке.

**Перейдем к инструкции по установке ноды Waku.**
**Системные требования к VPS серверу:**
- 2 GB RAM или более;
- 2 ядра CPU или более;
- 60 GB SSD или более;
- Ubuntu 20.04

**Также Вам потребуется кошелек, на котором находится как минимум 0.1 Ethereum Sepolia. Это необходимо для обеспечения транзакций в сети. + Зарегистрируйте аккаунт в Alchemy. Для данной ноды настоятельно рекомендую создать новый кошелек и сохранить данные от него в секретном месте.**

**Детальная инструкция по установке ноды:**

- Открываем программу для соединения с Вашим арендованным сервером, подключаемся к нему. Первой командой обновим ПО сервера: ``sudo apt update && sudo apt upgrade -y``


- **Устанавливаем необходимые утилиты:**


-  ``apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y`` 
-  Устанавливаем Docker: ``sudo apt install docker.io`` . В процессе установки все подтверждаем нажатием Y.
-  После установки проверяем версию Docker командой: ``docker --version``. Необходимо, чтобы версия Docker была не ниже версии 24.0.5. 
-  Устанавливаем Docker Compose командой:
- ``sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`` 
-  Выполняем команду: ``sudo chmod +x /usr/local/bin/docker-compose`` 
-  Проверяем версию Docker Compose командой: ``docker-compose --version``. Необходимо, чтобы версия Docker Compose была не ниже версии 2.24.5. 
-  Скачиваем на сервер ПО ноды Waku: ``git clone https://github.com/waku-org/nwaku-compose`` 
-  Меняем директорию: ``cd nwaku-compose`` 

-  **Alchemy**
-  Теперь необходимо зайти в [Alchemy](https://dashboard.alchemy.com/) и создать там новое приложение, с помощью которого мы сможем отслеживать работоспособность ноды. Для этого, авторизуйтесь в Alchemy и перейдите в раздел "Apps" 
-  Создайте новое приложение нажав на кнопку "+ Create new app" 
-  Выберите сеть Ethereum Sepolia. Также задайте название приложения и при необходимости добавьте описание приложению 

 
- Теперь здесь нам нужен следующий параметр: API key -> строчка HTTPS. В будущем мы вставим это в конфиг ноды Waku 
-  Теперь нужно получить тестовые Ethereum Sepolia. Ссылки на краны: [1](https://sepoliafaucet.com/),[2](https://www.infura.io/faucet/sepolia),[3](https://sepolia-faucet.pk910.de/). Переходим в любой удобный кран, получаем Ethereum Sepolia. В [официальной документации](https://docs.waku.org/guides/nwaku/run-docker-compose) по установке ноды Waku указано, что понадобится как минимум 0.1 ETH Sepolia. **ВАЖНО: Как оказалось, большое количество ETH Sepolia не играет роли в работе ноды Waku. Вам просто нужно иметь как минимум 0.1 ETH Sepolia на Вашем кошельке для обеспечения должной работы ноды.** 
-  ETH Sepolia получены, приложение в Alchemy создано. Теперь нам нужно поменять конфиг ноды Waku на сервере. Выполним команду: ``cp .env.example .env``
- Следом выполняем команду: ``nano .env``
-  Устанавливаем новые параметры в конфиге. Перемещаться по файлу можно при помощи стрелочек на клавиатуре. В поле "ETH_CLIENT_ADDRESS" вставьте Вашу ссылку из приложения Alchemy(смотреть пункт 15). В поле "ETH_TESTNET_KEY" укажите приватный ключ Вашего кошелька с Ethereum Sepolia. В поле "RLN_RELAY_CRED_PASSWORD" придумайте и введите пароль. **ВНИМАТЕЛЬНО ЗАПОЛНЯЙТЕ ДАННЫЕ В КОНФИГЕ, НЕ ДОПУСКАЙТЕ ЛИШНИХ КАВЫЧЕК, ПРОБЕЛОВ И ПРОЧИХ СИМВОЛОВ! ** 
-  После того, как внесли изменения в файл .env Вам необходимо его сохранить. Для этого нажимаем комбинацию клавиш CTRL + X, далее жмем Y, после нажимаем Enter на клавиатуре. Изменения должно сохраниться. 
-  Вводим команду: ``./register_rln.sh`` и ждем окончания ее выполнения. Возможна ошибка, не обращайте внимание. Нода все равно должна заработать.
-  Открываем порты. Для этого по очереди введем команды:

``sudo ufw enable``;

``sudo ufw allow 22``    # SSH доступ;

``sudo ufw allow 3000``  # Grafana дэшборд;

``sudo ufw allow 8545``   # Ethereum JSON-RPC;

``sudo ufw allow 8645``   # Waku REST API;

``sudo ufw allow 9005``   # discv5 routine;

``sudo ufw allow 30304``  # libp2p комммуникация

- Финальная команда, запускаем ноду: ``docker-compose up -d`` . Пойдут логи.


- Проверьте Ваше приложение в Alchemy. Там должны отобразиться показатели.

Если Вы все сделали правильно, то Ваша нода Waku должна работать исправно. Вы можете следить за ее работоспособностью в Alchemy в разделе "Apps".

**Выводы:**
- У проекта сильные Tier-1 инвесторы;
- В Twitter'е на проект подписан Виталик Бутерин и вероятнее всего также является инвестором;
- Проект активно взаимодействует с экосистемой Ethereum;
- Практически нет шилла в СНГ;
- Интересная идея, которую реализует проект;
- Разработчики активно работают над проектом(46 обновлений начиная с ноября 2020);
- Дорожная карта на 2024 год указывает на планы по стимулированию операторов, что предполагает инновационный подход к привлечению и расширению сообщества(Возможный насып держателям нод?)






