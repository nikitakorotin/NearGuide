# Поднимаем ноду Near, Stake Wars III

Статья написана не для того, чтоб ознакомить вас с наградами, которые нам обещает команда проекта. Вы сами можете ознакомиться со всем необходимым на [оффициальной страничке Stake Wars III](https://near.org/stakewars/) или в оффициальных статьях проекта. Цель статьи - подробно описать процесс прохождения заданий с технической стороны.

## Полезные ссылки
- [Оффициальный сайт Near](https://near.org/)
- [Оффициальная страница Stake Wars III](https://near.org/stakewars/)
- [Дискорд проекта для получения поддержки](https://discord.com/invite/UY9Xf2k)
- [Репозиторий с заданиями](https://github.com/near/stakewars-iii/tree/main/challenges)
- [Кошелек Near в Shardnet](https://wallet.shardnet.near.org/)
- [Эксплорер для Shardnet](https://explorer.shardnet.near.org/)

##  Прежде чем начать
Забегая вперед, сразу скажу, что [5ое задание](https://github.com/near/stakewars-iii/blob/main/challenges/005.md) включает в себя написание статьи (на подобие этой) с подробным описанием выполнения заданий 1-4 со скринами и описанием.

По- этому, нам нужно скринить и писать заметки на протяжении всего процесса поднятия ноды, а так же делать это сразу на сервере. Команда предлагает поднимать ноду на слеедующий облачных серверах:
-   Amazon Web Services
-   Google Cloud Platform
-   Microsoft Azure
-   IBM Cloud
-   DigitalOcean
-   Hetzner

Минимальные требования для ноды описаны во [2ом задании](https://github.com/near/stakewars-iii/blob/main/challenges/002.md):
- CPU: 4-Core CPU with AVX support
- RAM: 8GB DDR4
- Storage: 500GB SSD

Я создал сервер на [Hetzner](https://hetzner.cloud/?ref=TwL8pubSjFf8) со спецификациями 4/8/160, в дальнейшем буду расширять память при необходимости (нужно будет постоянно мониторить память), однако это позволит мне сэкономить на ноде. Ребята в коммуне говорят, что понадобится реально 400-500 GB, на [Hetzner](https://hetzner.cloud/?ref=TwL8pubSjFf8) можно в любой момет добавить память.

Для работы с сервером я буду использовать программу [MobaXTerm](https://mobaxterm.mobatek.net/download-home-edition.html).

## Поднимаем сервак
Регистрируемся в [Hetzner](https://hetzner.cloud/?ref=TwL8pubSjFf8), привязываем карту, заходим в Cloud, создаем проект с любым названием и добавляем новый сервер.

![image](_attachments/Pasted%20image%2020220801183304.png)


Выбираем ближайшую до нас локацию, операционную систему (Ubuntu), тип (Standard) и сервер (CPX31 в моем случае, в дальнейшем SSD можно расширить). Все это будет стоить 15 евро в месяц без дополнительной памяти.

![image](_attachments/Pasted%20image%2020220801183512.png)

Если вы хотите сразу добавить недостоющие 340 GB - это вам обойдется еще в 16.46 евро в месяц.

Все остальное я оставляю без изменений (можете дать серверу название).

![image](_attachments/Pasted%20image%2020220801183839.png)

Создаем сервер и ждем его готовности (рядом с сервером загорится зеленая лампочка).

## Коннектимся к серваку
Устанавливаем MobaXTerm. Данные для коннекта к серверу вы получите по почте.

Открываем Moba и жмем кнопку "Session".

![image](_attachments/Pasted%20image%2020220801184301.png)

Жмем кнопку "SSH".

![image](_attachments/Pasted%20image%2020220801193124.png)

В поле "Remote host" вбиваем наш IPv4, ставим галочку в поле "Specify username" и вписываем туда "root", далее жмем "OK".

У нас появится командная строка с запросом пароля, вбиваем туда наш пароль (который мы получили по почте). Символы видны не будут, можно вставлять в терминал что - то из буффера комбинацией клавиш "Shift+Insert". Вставляем пароль и жмем ENTER. Не сохраняем пароль, если нам Moba это предложит.

Так как это временный пароль, нам необходимо будет вбить его еще раз и далее вбить наш новый пароль 2 раза. Делаем.

![image](_attachments/Pasted%20image%2020220801184842.png)

Сервак готов к работе.

![image](_attachments/Pasted%20image%2020220801184938.png)

## Задание 01
Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/001.md).

**Внимание!** в оффициальном гайде вы можете найти все объяснения и теорию в целом (советую читать офф документацию для личного развития). Я буду лаконичен и буду описывать весь процесс без лишних слов, советую использовать этот гайд исключительно как дополнение к оригиналу. Имейте ввиду, что материал, описанный мной, может устареть.

**Цель задания** - создать кошелек на Near и поставить NEAR CLI. Я буду ставить его и ноду на одном сервере.

### Создаем Near кошелек

Переходим на [сайт](https://wallet.shardnet.near.org/) и создаем кошелек в тестовой сети.

![image](_attachments/Pasted%20image%2020220801185632.png)

Выбираем себе ник и жмем синюю кнопку.

В качестве метода защиты я выбрал "Secure Passphrase".

![image](_attachments/Pasted%20image%2020220801185817.png)

Сохраняем сид фразу (никому не показываем ее никогда), жмем "Continue". Далее вставляем слово из нашей сид фразы, которое у нас запросили. В моем случае это слово под номером 3, жмем "Verify & Complete". Этот шаг может потребовать несколько больше времени, просто ждем, если словите ошибку - пробуйте снова.

![image](_attachments/Pasted%20image%2020220801185950.png)

Далее вставляем всю нашу сид фразу в поле и жмем "Find My Account". Процесс тоже займет некоторое время.

![image](_attachments/Pasted%20image%2020220801190123.png)

Если все прошло хорошо - вы не увидите никаких ошибок, создастся аккаунт и на нем будет какое - то количество монет.

![image](_attachments/Pasted%20image%2020220801190220.png)

### Устанавливаем NEAR CLI на сервер

Вбиваем следущие команды по - очереди и ждем полного их выполнения. Я покажу, как выглядит окно терминала после выполнения команд.

```
sudo apt update && sudo apt upgrade -y
```

```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
```

![image](_attachments/Pasted%20image%2020220801190641.png)

```
sudo apt install build-essential nodejs
```

![image](_attachments/Pasted%20image%2020220801190709.png)

Вбиваем "Y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801190758.png)

```
PATH="$PATH"
```

![image](_attachments/Pasted%20image%2020220801190819.png)

```
node -v
```

Должно отбиться в терминале v18.x.x, у меня v18.7.0.

![image](_attachments/Pasted%20image%2020220801190917.png)

```
npm -v
```

Должно отбиться в терминале 8.x.x, у меня 8.15.0.

![image](_attachments/Pasted%20image%2020220801190953.png)

```
sudo npm install -g near-cli
```

![image](_attachments/Pasted%20image%2020220801191033.png)

```
export NEAR_ENV=shardnet
```

![image](_attachments/Pasted%20image%2020220801191101.png)

```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc
```

![image](_attachments/Pasted%20image%2020220801191120.png)

```
echo 'export NEAR_ENV=shardnet' >> ~/.bash_profile
```

![image](_attachments/Pasted%20image%2020220801191137.png)

```
source $HOME/.bash_profile
```

![image](_attachments/Pasted%20image%2020220801191154.png)

### Проверяем, встал ли NEAR CLI на сервер.

```
near proposals
```

Если что - то такое выдает - все ок.

![image](_attachments/Pasted%20image%2020220801191306.png)


## Задание 02

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/002.md).

**Цель задания** - поднимаем ноду Near и активируем ее как валидатора.

### Поднимаем ноду

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```

Вот так должно быть, если сервак подходит под это дело.

![image](_attachments/Pasted%20image%2020220801191518.png)

```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```

![image](_attachments/Pasted%20image%2020220801191651.png)

```
apt-get install containerd=1.3.3-0ubuntu2
```

![image](_attachments/Pasted%20image%2020220801191706.png)

Вбиваем "Y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801191749.png)

```
sudo apt install python3-pip
```

![image](_attachments/Pasted%20image%2020220801191808.png)

Вбиваем "Y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801191825.png)

```
USER_BASE_BIN=$(python3 -m site --user-base)/bin
```

![image](_attachments/Pasted%20image%2020220801191846.png)

```
export PATH="$USER_BASE_BIN:$PATH"
```

![image](_attachments/Pasted%20image%2020220801191900.png)

```
sudo apt install clang build-essential make
```

![image](_attachments/Pasted%20image%2020220801191920.png)

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

![image](_attachments/Pasted%20image%2020220801191946.png)

Вбиваем "y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801191959.png)

Вбиваем "1" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801192036.png)

```
source $HOME/.cargo/env
```

![image](_attachments/Pasted%20image%2020220801192054.png)

```
git clone https://github.com/near/nearcore
```

![image](_attachments/Pasted%20image%2020220801192426.png)

```
cd nearcore
```

![image](_attachments/Pasted%20image%2020220801192437.png)

```
git fetch
```

![image](_attachments/Pasted%20image%2020220801192459.png)

Идем по [ссылке](https://github.com/near/stakewars-iii/blob/main/commit.md) и берем там строчку (вероятно, она может измениться, потому не копируйте мою команду, а перепроверьте).

![image](_attachments/Pasted%20image%2020220801192723.png)

```
git checkout c1b047b8187accbf6bd16539feb7bb60185bdc38
```

![image](_attachments/Pasted%20image%2020220801192843.png)

```
cargo build -p neard --release --features shardnet
```

Тут потребуется минут 10.

![image](_attachments/Pasted%20image%2020220801194224.png)

```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```

![image](_attachments/Pasted%20image%2020220801194402.png)

```
rm ~/.near/config.json
```

![image](_attachments/Pasted%20image%2020220801194453.png)

```
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```

![image](_attachments/Pasted%20image%2020220801194540.png)

```
./target/release/neard --home ~/.near run
```

Запускается нода, начинается что - то вроде синхронизации, ждем 100%.

![image](_attachments/Pasted%20image%2020220801224848.png)

В итоге у нас должен пойти похожий лог. Сверяем текущий блок с [эксплорером](https://explorer.shardnet.near.org/). Должно быть похожее значение.

![image](_attachments/Pasted%20image%2020220801232149.png)

### Активируем валидатора

Нажимаем "CTRL+C" в консоли.

![image](_attachments/Pasted%20image%2020220801232328.png)

```
near login
```

![image](_attachments/Pasted%20image%2020220801232419.png)

Вбиваем "y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220801232510.png)

Полностью копируем ссылку из терминала и вставляем ее в браузер, в котором мы залогинены в наш кошелек.


Жмем "Next".


Жмем "Connect".


Вставляем адрес нашего кошелька в поле и жмем "Confirm". На этом этапе просто ждем, пока появится такая страница.

![image](_attachments/Pasted%20image%2020220801232803.png)

Идем обратно в терминал и вбиваем адрес нашего кошелька, жмем ENTER. Должна появиться инфа о том, что кошелек подключен.

```
cat ~/.near/validator_key.json
```

Если  пишет, что нет такого файла - делаем следующее (у меня нет файла).

![image](_attachments/Pasted%20image%2020220801233156.png)

Придумаем название для нашего пула (pool_id). Я выбрал название как при создании кошелька "mihauman222". Теперь мой пул называется "mihauman222.factory.shardnet.near". Вбиваем команду (замените pool_id на свой), в моем случае:

```
near generate-key mihauman222.factory.shardnet.near
```


Вбиваем команду, предварительно заменив pool_id на ваш собственный.

```
cp ~/.near-credentials/shardnet/mihauman222.factory.shardnet.near.json ~/.near/validator_key.json
```

Так как мы работаем в MobaXTerm, мы можем облегчить себе жизнь при редактировании .json файла, просто переходим в навигаторе (слева) в папку "root -> .near".

![image](_attachments/Pasted%20image%2020220801233923.png)

Открываем наш файл "validator_key.json".

![image](_attachments/Pasted%20image%2020220801234008.png)

Откроется окно с данными, нужно заменить "private_key" на "secret_key". 

![image](_attachments/Pasted%20image%2020220801234124.png)
![image](_attachments/Pasted%20image%2020220801234141.png)

Нужно удостоверится, что тут указан ваш pool_id. Если это не так - редактируем.
у меня mihauman222.factory.shardnet.near

Жмем "CTRL+S". Сохраняем все данные в блокнот, они нам могут пригодиться, будет гораздо удобнее иметь к ним легкий доступ.

Жмем "Yes".

```
target/release/neard run
```

Запускается валидатор, сверяем блоки

![image](_attachments/Pasted%20image%2020220801234759.png)

Жмем "CTRL+C".

![image](_attachments/Pasted%20image%2020220801234834.png)

```
sudo vi /etc/systemd/system/neard.service
```

Открывается редактор, жмем клавишу "i".

Вставляем такой вот скрипт, предварительно подправив имя юзера на свое в путях. Вот как выглядит шаблон от разработчиков (обратите внимание на \<USER>).

```
[Unit]
Description=NEARd Daemon Service

[Service]
Type=simple
User=<USER>
#Group=near
WorkingDirectory=/home/<USER>/.near
ExecStart=/home/<USER>/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

Если ставите ноду на [Hetzner](https://hetzner.cloud/?ref=TwL8pubSjFf8), то, скорее всего, у вас будет как у меня.

```
[Unit]
Description=NEARd Daemon Service

[Service]
Type=simple
User=root
#Group=near
WorkingDirectory=/root/.near
ExecStart=/root/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

Эмем "ESC".


Жмем ":", вписываем "wq" и жмем "ENTER".


```
sudo systemctl enable neard
```

![image](_attachments/Pasted%20image%2020220801235715.png)

```
sudo systemctl start neard
```

![image](_attachments/Pasted%20image%2020220801235735.png)

```
sudo apt install ccze
```

![image](_attachments/Pasted%20image%2020220801235817.png)

Данной командой можем в любой момент чекнуть логи. Чтоб выйти, просто вбиваем "CTRL+C".

```
journalctl -n 100 -f -u neard | ccze -A
```

![image](_attachments/Pasted%20image%2020220802000036.png)



## Задание 03

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/003.md).

**Цель задания** - задеплоить стейкинг пул. Произвести операции делегирования и застейкать Near.

Вот шаблон команды, который надо подправить нашими значениями.

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```

Меняем следующие поля на свои:
- "staking_pool_id": "\<pool id>" - тут меняем \<pool id> на свой (только первая часть названия), я вбиваю сюда "cryptobusher666"
- "owner_id": "\<accountId>" - тут меняем \<accountId> на свой, я вбиваю сюда "cryptobusher666.shardnet.near"
- "stake_public_key": "\<public key>" - тут меняем \<public key> на свой, который можно найти в файле "validator_key.json" (мы сохраняли эти данные в нашем прошлом задании) 
- --accountId="\<accountId>" - тут меняем \<accountId> на свой


![image](_attachments/Pasted%20image%2020220802001334.png)

Можем зайти в [эксплорер](https://explorer.shardnet.near.org/) и проверить, что произошло на нашем аккаунте.  Виден успешный вызов метода и изменение баланса (примерно на 30 Near).

Можете изменить параметры пула (например комиссия), можете использовать следующую команду, однако я этого делать не буду.

```
near call <pool_name> update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId <account_id> --gas=300000000000000
```

Для дополнительных команд (депозит, анстейк и тд) обращайтесь к оффициальному гайду для этого задания.

На сколько я понял, нам нужно некоторое минимальное количество Near для того, чтоб стать валидатором (поправьте, если не прав), однако после данных операций я еще не являюсь валидатором, мне нужно запросить токены в дискорде Near. Для того, чтоб получить токены через дискорд, нужно попасть в proposals. Проверить это можно следующей командой (подставьте название своего пула).

```
 near proposals | grep mihauman222
```

Мне ничего не выдало, должно быть так вообще:

![image](_attachments/Pasted%20image%2020220802003926.png)

Посерфил дискорд и понял, для того, чтоб попасть в proposal нужно застейкать суммарно 56 Near. Где их взять - не особо понятно, но все создают еще один кошелек, чтоб получить дополнительных 50 Near и застейкать их. Не уверен, что это прям понравится команде, но другого выхода я не вижу, потому сделал как все.

Создал аккаунт, получил на него около 50 Near, скинул на основной кошелек.

Вбиваем команду, сменив все значения на свои, вот шаблон команды:

```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
```

У меня команда выглядит так:

```
near call mihauman222.factory.shardnet.near deposit_and_stake --amount 49 --accountId mihauman222.shardnet.near --gas=300000000000000
```

Появились дополнительные токены в пуле.


Проверяем, попали ли мы в proposals:

```
 near proposals | grep mihauman222
```

Ура, попали. Идем в [дискорд Near](https://discord.com/invite/UY9Xf2k), в канал  "stake-wars-tokens_delegation".

![image](_attachments/Pasted%20image%2020220802004740.png)

Просим токены, это может затянуться, так как очередь на раздачу большая, просто терпеливо ждем и иногда напоминаем о себе (не стоит спамить). Пока я не получил токены, иду дальше выполнять задания.



## Задание 04

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/004.md).

**Цель задания** - настроить мониторинг статуса ноды.

Напоминаю, что лог можно посмотреть с помощью команды:

```
journalctl -n 100 -f -u neard | ccze -A
```

Подробное описание значений в логе можно найти в оффициальном гайде по данному заданию.

```
sudo apt install curl jq
```

![image](_attachments/Pasted%20image%2020220802145024.png)

Вбиваем "Y" и жмем ENTER.

![image](_attachments/Pasted%20image%2020220802145112.png)

Готово. В оффициальном гайде по этому заданию перечислены команды для проверки некоторых данных (проверка валидаторов и стейка, причины кика валидатора, информация по блокам). Советую попрактиковаться.

## Задание 05

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/005.md).

**Цель задания** - написать гайд по выполнению первых четырех заданий.

Я говорил об этом в начале статьи. В процессе выполнения первых четырех заданий вам необходимо было документировать весь процесс, скринить все, что считаете нужным (эта статья от части написана для выполнения 5го задания). Подходите к заданию так, как считаете нужным.

Я решил опустить многие пояснения, так как они уже есть в оффициальных гайдах, смысла переписывать это я не вижу. Я решил сделать такой гайд, с помощью которого любой новичек смог бы выполнить первые 4 этапа, описал некоторые тонкости, которые в офф гайдах опущены из - за их очевидности.

## Задание 06

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/006.md).

**Цель задания** - создать cron task для автоматического пинга.

Нам необходимо создать дерикторию "scripts" в папке юзера (в моем случае нет юзера, просто в root), а там уже создать файл "ping.sh".

Вы на данном этапе можете находиться в какой - то директории, отличной от моей, потому го немного теории по навигации.

Вернуться назад можно с помощью этой команды:

```
cd ..
```

Посмотреть список файлов и папок в текущей директории можно с помощью команды:

```
ls
```

Перейти в папку в данной директории можно с помощью команды:

```
cd названиепапки
```

Показать, где я нахожусь сейчас можно с помощью команды:

```
pwd
```

Итак, допустим я нахожусь в папке "nearcore".

![image](_attachments/Pasted%20image%2020220802150225.png)

```
cd ..
```

![image](_attachments/Pasted%20image%2020220802150330.png)

```
pwd
```

![image](_attachments/Pasted%20image%2020220802150349.png)

Я в руте, создаю тут папку "scripts".

```
mkrid scripts
```

Проверяю, создалась ли папка.

```
ls
```

![image](_attachments/Pasted%20image%2020220802150541.png)

Иду в эту папку.

```
cd scripts
```

![image](_attachments/Pasted%20image%2020220802150614.png)

Создаю файл "ping.sh".

```
touch ping.sh
```

Проверяю, создался ли файл.

```
ls
```

![image](_attachments/Pasted%20image%2020220802150709.png)

Открываю файл с помощью vim.

```
vim ping.sh
```


Жму "i".



Вставляю данный скрипт, предварительно изменив пути. Вот так выглядит шаблон.

```
#!/bin/sh
# Ping call to renew Proposal added to crontab

export NEAR_ENV=shardnet
export LOGS=/home/<USER_ID>/logs
export POOLID=<YOUR_POOL_ID>
export ACCOUNTID=<YOUR_ACCOUNT_ID>

echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log
```

Вот так выглядит мой вариант.

```
#!/bin/sh
# Ping call to renew Proposal added to crontab

export NEAR_ENV=shardnet
export LOGS=/root/logs
export POOLID=mihauman222
export ACCOUNTID=mihauman222

echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log
```

Жму "ESC". 


Жму ":" и пишу "wq".

Жму "ENTER".

![image](_attachments/Pasted%20image%2020220802151354.png)

Создаю папку для логов.

```
mkdir $HOME/logs
```

![image](_attachments/Pasted%20image%2020220802151506.png)

Меняем permission для скрипта.

```
chmod +x $HOME/scripts/ping.sh
```

![image](_attachments/Pasted%20image%2020220802151540.png)

Создаем crontab с интервалом в 2 часа.

```
crontab -e
```

![image](_attachments/Pasted%20image%2020220802151627.png)

Я выбрал второй вариант, жму "2" и "ENTER".

Все как обычно, жму "i", вставляю скрипт, предварительно заменив значение на свое, вот шаблон:

```
0 */2 * * * sh /home/<USER_ID>/scripts/ping.sh
```


Жму "ESC", жму ":", пишу "wq" и жму "ENTER".

![image](_attachments/Pasted%20image%2020220802151849.png)

В дальнейшем у нас будут появляться логи, просмотреть их можно с помощью данной команды:

```
cat $HOME/logs/all.log
```

После выполнения данных шагов нам нужно дождаться вызовов метода "ping", заскринить это все в эксплорере и [заполнить форму](https://docs.google.com/forms/d/e/1FAIpQLScp9JEtpk1Fe2P9XMaS9Gl6kl9gcGVEp3A5vPdEgxkHx3ABjg/viewform) с отчетом. Так как у меня этот процесс еще не прошел, я буду сабмитить форму позже, но пример вы можете увидеть на странице с оффициальным гайдом по этому шагу.


## Задание 08

Оффициальный гайд можете найти [тут](https://github.com/near/stakewars-iii/blob/main/challenges/008.md).

**Цель задания** - задеплоить контракт для распределения наград между 2мя аккаунтами.

Нам предлагают поставить cargo и Rust, но мы это делали ранее, на всякий случай прогоню эти 2 команды.

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Прожимаем там "y" и "1" в процессе выполнения, не буду скринить.

```
source $HOME/.cargo/env
```

![image](_attachments/Pasted%20image%2020220802153007.png)

```
rustup target add wasm32-unknown-unknown
```

![image](_attachments/Pasted%20image%2020220802152539.png)

Тут надо склонировать репозиторий из Гитхаба. Для этого я создам директорию "github" в "root".

```
mkdir github
```

![image](_attachments/Pasted%20image%2020220802152652.png)

```
cd github
```

![image](_attachments/Pasted%20image%2020220802152715.png)

```
git clone https://github.com/zavodil/near-staking-pool-owner
```

![image](_attachments/Pasted%20image%2020220802153053.png)

```
cd near-staking-pool-owner/contract
```

![image](_attachments/Pasted%20image%2020220802153119.png)

```
cargo build --target wasm32-unknown-unknown --release
```

![image](_attachments/Pasted%20image%2020220802153231.png)

Вбиваем команду, скорректировав некоторые данные под себя, вот шаблон:

```
NEAR_ENV=shardnet near deploy <OWNER_ID>.shardnet.near --wasmFile target/wasm32-unknown-unknown/release/contract.wasm
```

Вот как выглядит моя команда:

```
NEAR_ENV=shardnet near deploy mihauman222.shardnet.near --wasmFile target/wasm32-unknown-unknown/release/contract.wasm
```

Создаем переменную, вот шаблон команды:

```
CONTRACT_ID=<OWNER_ID>.shardnet.near
```

Моя команда выглядит так:

```
CONTRACT_ID=mihauman222.shardnet.near
```


Тут нам нужен еще один аккаунт для получения наград. Создаем новый аккаунт в Shardnet сети, мы это делали в первом задании, все происходит похожим образом. Я создал новый аккаунт "mihauman222.shardnet.near" (там двойка в конце).

Вбиваем следующую команду, предварительно сменив некоторые значения на свои. Вот шаблон:

```
NEAR_ENV=shardnet near call $CONTRACT_ID new '{"staking_pool_account_id": "<STAKINGPOOL_ID>.factory.shardnet.near", "owner_id":"<OWNER_ID>.shardnet.near", "reward_receivers": [["<SPLITED_ACCOUNT_ID_1>.shardnet.near", {"numerator": 3, "denominator":10}], ["<SPLITED_ACCOUNT_ID_2>.shardnet.near", {"numerator": 70, "denominator":100}]]}' --accountId $CONTRACT_ID
```
Необходимо подождать, пока мы начнем получать реварды и сделать их вывод. Это можно сделать после завершения эпохи, которая длится 12 часов. Ждем и вбиваем команду, скорректировав все своими значениями. Вот шаблон:

```
CONTRACT_ID=<OWNER_ID>.shardnet.near
```

```
NEAR_ENV=shardnet near call $CONTRACT_ID withdraw '{}' --accountId $CONTRACT_ID --gas 200000000000000
```

Вот мой вариант:

```
CONTRACT_ID=mihauman222.shardnet.near
```

```
NEAR_ENV=shardnet near call $CONTRACT_ID withdraw '{}' --accountId $CONTRACT_ID --gas 200000000000000
```

Далее делаем скрин успешного вывода токенов и прикрепляем к [форме](https://docs.google.com/forms/d/e/1FAIpQLScp9JEtpk1Fe2P9XMaS9Gl6kl9gcGVEp3A5vPdEgxkHx3ABjg/viewform) отчета по данному заданию. Больше подробностей об отчете можете найти в оффициальном гайде по данному заданию.



