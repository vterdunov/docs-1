# Управление доступом

Пользователь Яндекс.Облака может выполнять только те операции над ресурсами, которые разрешены назначенными ему ролями.
Пока у пользователя нет никаких ролей, почти все операции ему запрещены.

Чтобы разрешить доступ к ресурсам сервиса {{ api-gw-name }} (API-шлюзам), назначьте пользователю нужные роли из приведенного ниже списка. На данный момент роль может быть назначена только на родительский ресурс (каталог или облако).

{% note info %}

Подробнее о наследовании ролей читайте в разделе [{#T}](../../resource-manager/concepts/resources-hierarchy.md#access-rights-inheritance) документации сервиса {{ resmgr-full-name }}.

{% endnote %}

## Назначение ролей {#grant-roles}

Чтобы назначить пользователю роль:

{% include [grant-role-console](../../_includes/grant-role-console.md) %}

## Роли {#roles}

Ниже перечислены все роли, которые учитываются при проверке прав доступа в сервисе {{ api-gw-name }}.

### {{ roles-viewer }} {#viewer}

Пользователь с ролью `{{ roles-viewer }}` может просматривать информацию о ресурсах, например, посмотреть список функций или версий и журнал выполнения функции.

### {{ roles-editor }} {#editor}

Пользователь с ролью `{{ roles-editor }}` может управлять функциями и версиями, например, создать или удалить версию или отредактировать информацию о функции.

Помимо этого роль `{{ roles-editor }}` включает в себя все разрешения роли `{{ roles-viewer }}`.

### {{ roles-admin }} {#admin}

Пользователь с ролью `{{ roles-admin }}` может управлять правами доступа к ресурсам, например разрешить другим пользователям запускать функции или работать с версиями.

Помимо этого роль `{{ roles-admin }}` включает в себя все разрешения роли `{{ roles-editor }}`.