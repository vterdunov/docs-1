# Управление резервными копиями

Вы можете создавать [резервные копии](../concepts/backup.md) и восстанавливать кластеры из имеющихся резервных копий.


## Восстановить кластер из резервной копии {#restore}

Восстанавливая кластер из резервной копии, вы создаете новый кластер с данными из резервной копии. Если в каталоге не хватает [ресурсов](../concepts/limits.md) для создания такого кластера, восстановиться из резервной копии не получится. Средняя скорость восстановления из резервной копии — 10 МБайт/с.

Для нового кластера необходимо задать все параметры, обязательные при создании, кроме типа кластера (резервную копию {{ MG }} не получится восстановить как кластер {{ PG }}).

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmg-name }}**.

  1. Нажмите на имя нужного кластера и выберите вкладку **Резервные копии**.

  1. Нажмите значок ![image](../../_assets/dots.svg) для нужной резервной копии, затем нажмите **Восстановить кластер**.

  1. Задайте настройки нового кластера. В списке **Каталог** можно выбрать каталог для нового кластера.

  1. Нажмите кнопку **Восстановить кластер**.

  {{ mmg-name }} запустит операцию создания кластера из резервной копии.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы восстановить кластер из резервной копии:

  1. Посмотрите описание команды CLI для восстановления кластера {{ MG }}:

      ```
      $ yc managed-mongodb cluster restore --help
      ```

  1. Получите список доступных резервных копий {{ MG }}-кластеров:

      ```
      $ yc managed-mongodb backup list

      +--------------------------+----------------------+----------------------+----------------------+
      |            ID            |      CREATED AT      |  SOURCE CLUSTER ID   |      STARTED AT      |
      +--------------------------+----------------------+----------------------+----------------------+
      | c9qlk4v13uq79r9cgcku:... | 2018-11-02T10:08:38Z | c9qlk4v13uq79r9cgcku | 2018-11-02T10:08:37Z |
      | ...                                                                                           |
      +--------------------------+----------------------+----------------------+----------------------+
      ```

  1. Запросите создание кластера из резервной копии:

      
      ```
      $ yc managed-mongodb cluster restore \
           --backup-id c9q287aqv5rf11isjeql:20181113T133617 \
           --cluster-name mynewmg \
           --environment=PRODUCTION \
           --network-name default \
           --host zone-id=ru-central1-c,subnet-id=b0rcctk2rvtr8efcch63 \
           --mongod-disk-size 20 \
           --mongod-disk-type network-ssd \
           --mongod-resource-preset s2.micro
      ```

     

      В результате будет создан {{ MG }}-кластер со следующими характеристиками:

      

            - С именем `mynewmg`.
      - В окружении `PRODUCTION`.
      - В сети `{{ network-name }}`.
      - С одним хостом класса `{{ host-class }}` в подсети `b0rcctk2rvtr8efcch63`, в зоне доступности `{{ zone-id }}`.
      - С базами данных и пользователями из резервной копии.
      - С быстрым сетевым хранилищем (`{{ disk-type-example }}`) объемом 20 ГБ.

     

{% endlist %}


## Создать резервную копию {#create-backup}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmg-name }}**.

  1. Нажмите на имя нужного кластера и выберите вкладку **Резервные копии**.

  1. Нажмите кнопку **Создать резервную копию**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы создать резервную копию кластера:

  1. Посмотрите описание команды CLI для создания резервной копии {{ MG }}:

      ```
      $ yc managed-mongodb cluster backup --help
      ```

  1. Запросите создание резервной копии, указав имя или идентификатор кластера:

      ```
      $ yc managed-mongodb cluster backup my-mg-cluster
      ```

      Имя и идентификатор кластера можно получить со [списком кластеров](cluster-list.md#list-clusters).

{% endlist %}


## Получить список резервных копий {#list-backups}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmg-name }}**.

  1. Нажмите на имя нужного кластера и выберите вкладку **Резервные копии**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы получить список резервных копий кластеров {{ MG }}, доступных в каталоге по умолчанию, выполните команду:

  ```
  $ yc managed-mongodb backup list

  +----------+----------------------+----------------------+----------------------+
  |    ID    |      CREATED AT      |  SOURCE CLUSTER ID   |      STARTED AT      |
  +----------+----------------------+----------------------+----------------------+
  | c9qv4... | 2018-10-31T22:01:07Z | c9qv4ql6bd4hfo1cgc3o | 2018-10-31T22:01:03Z |
  | c9qpm... | 2018-10-31T22:01:04Z | c9qpm90p3pcg71jm7tqf | 2018-10-31T22:01:04Z |
  +----------+----------------------+----------------------+----------------------+
  ```

{% endlist %}


## Получить информацию о резервной копии {#get-backup}

{% list tabs %}

- Консоль управления

  1. Перейдите на страницу каталога и выберите сервис **{{ mmg-name }}**.

  1. Нажмите на имя нужного кластера и выберите вкладку **Резервные копии**.

- CLI

  {% include [cli-install](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}

  Чтобы получить данные о резервной копии кластера {{ MG }}, выполните команду:

  ```
  $ yc yc managed-mongodb backup get <идентификатор резервной копии>
  ```

  Идентификатор резервной копии можно получить со [списком резервных копий](#list-backups).

{% endlist %}


