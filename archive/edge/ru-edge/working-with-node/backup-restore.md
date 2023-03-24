---
id: backup-restore
title: Экземпляр резервного копирования/восстановления нода
description: "Как создать резервную копию и восстановить экземпляр нода Polygon Edge."
keywords:
  - docs
  - polygon
  - edge
  - instance
  - restore
  - directory
  - node
---

## Обзор {#overview}

Руководство подробно описывает создание резервной копии и восстановления экземпляра нода Polygon Edge.  В нем рассказывается о базовых папках, их содержании, а также о том, какие файлы имеют решающее значение для выполнения успешной резервной копии и восстановления.

## Базовые папки {#base-folders}

Polygon Edge использует LevelDB как двигатель хранилища. При запуске нода Polygon Edge в указанной рабочей директории создаются следующие подпапки:
* **блокчейн** — хранение данных блокчейна
* **дерево** — хранение деревьев Меркла (данные о мировом состоянии)
* **хранилище ключей** — хранение приватных ключей для клиента. Это включает приватный ключ libp2p и приватный ключ запечатывания/валидатора
* **консенсус** — хранение любой информации о консенсусе, которая может понадобиться клиенту во время работы. На данный момент он хранит *приватный ключ валидатора* нода

Крайне важно сохранить эти папки, чтобы экземпляр Polygon Edge мог быть запущен без проблем.

## Создание резервной копии из работающего нода и восстановление для нового нода {#create-backup-from-a-running-node-and-restore-for-new-node}

Этот раздел поможет вам создать архивные данные блокчейна на работающем ноде и восстановить их в другом экземпляре.

### Резервное копирование {#backup}

`backup`команда собирает блоки из работающего нода с помощью gRPC и генерирует архивный файл. Если `--from` и `--to` не указаны в команде, это команда будет собирать блоки от генезиса до последнего.

```bash
$ polygon-edge backup --grpc-address 127.0.0.1:9632 --out backup.dat [--from 0x0] [--to 0x100]
```

### Восстановление {#restore}

Сервер импортирует блоки из архива на старте, когда запуск осуществлен с флагом `--restore`. Убедитесь, что для нового нода существует ключ. Более полную информацию об импорте или генерировании ключей можно найти в  разделе [Диспетчеры секретов](/docs/edge/configuration/secret-managers/set-up-aws-ssm).

```bash
$ polygon-edge server --restore archive.dat
```

## Резервная копия / восстановление данных полностью {#back-up-restore-whole-data}

Этот раздел поможет вам создать резервную копию данных, включая данные о состоянии и ключ, а также восстановить в виде нового экземпляра.

### Шаг 1: остановите работающий клиент {#step-1-stop-the-running-client}

Поскольку Polygon Edge использует **LevelDB** для хранения данных, нод необходимо остановить на время резервного копирования, так как **LevelDB** не позволяет одновременный доступ к файлам базы данных.

Кроме того, Polygon Edg также выполняет промывку данных при закрытии.

Первый шаг предполагает остановку работающего клиента (либо через диспетчера служб, либо через другой механизм, посылающий процессу сигнал SIGINT), чтобы он мог вызвать 2 события при изящном завершении работы:
* Выполнение сброса данных на диск
* Освобождение файлов БД от блокировки со стороны LevelDB

### Шаг 2: резервное копирование директории {#step-2-backup-the-directory}

Теперь, когда клиент не работает, данные директории можно резервировать на другой носитель. Не забывайте, что файлы с расширением `.key` содержат данные приватного ключа, которые могут быть использованы для выдачи себя за текущий нод, и они никогда не должны передаваться третьим/неизвестным лицам.

:::info
Создайте резервную копию и восстановите сгенерированный файл `genesis` вручную, чтобы восстановленный нод был полностью работоспособен.
:::

## Восстановление {#restore-1}

### Шаг 1: остановите работающий клиент {#step-1-stop-the-running-client-1}

Если какой-либо экземпляр Polygon Edge запущен, его необходимо остановить, чтобы успешно осуществить шаг 2.

### Шаг 2: скопируйте резервную копию директории данных в нужную папку {#step-2-copy-the-backed-up-data-directory-to-the-desired-folder}

Если клиент не запущен в работу, данные директории, в которой была ранее сделана резервная копия, можно скопировать в нужную папку. Кроме того, восстановите ранее скопированный файл `genesis`.

### Шаг 3: запустите клиент Polygon Edge, указав при этом данные правильной директории {#step-3-run-the-polygon-edge-client-while-specifying-the-correct-data-directory}

Чтобы Polygon Edge использовал восстановленную директорию данных, при запуске пользователю необходимо указать путь к директории данных. Подробнее о флаге `data-dir` см. в разделе [Команды CLI](/docs/edge/get-started/cli-commands).