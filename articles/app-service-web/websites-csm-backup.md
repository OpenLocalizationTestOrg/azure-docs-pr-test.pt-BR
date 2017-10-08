---
title: "aaaUse REST tooback backup e restaurar aplicativos de serviço de aplicativo"
description: "Saiba como toouse API RESTful chama tooback e restauração de um aplicativo no serviço de aplicativo do Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Usar o REST tooback e restaurar aplicativos de serviço de aplicativo
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [API REST](websites-csm-backup.md)
> 
> 

[aplicativos do Serviço de Aplicativo](https://azure.microsoft.com/services/app-service/web/) pode ser feito como blobs no armazenamento do Azure. backup Olá também pode conter os bancos de dados do aplicativo hello. Se o aplicativo hello é nunca acidentalmente excluído, ou se toobe de necessidades de aplicativo hello revertido versão anterior do tooa, podem ser restaurado de qualquer backup anterior. Os backups podem ser realizados a qualquer momento e sob demanda ou podem ser agendados em intervalos adequados.

Este artigo explica como toobackup e restauração de um aplicativo com a API RESTful solicitações. Se deseja toocreate e gerencie os backups de aplicativo graficamente no hello portal do Azure, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Introdução
solicitações de toosend REST, você precisa tooknow seu aplicativo **nome**, **grupo de recursos**, e **id da assinatura**. Essas informações podem ser encontradas clicando em seu aplicativo hello **do serviço de aplicativo** folha de saudação [portal do Azure](https://portal.azure.com). Para obter exemplos de saudação neste artigo, estamos Configurando site Olá **backuprestoreapiexamples.azurewebsites.net**. Ele é armazenado no grupo de recursos padrão-Web-WestUS hello e está em execução em uma assinatura com hello ID 00001111-2222-3333-4444-555566667777.

![Informações do site de exemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Fazer backup e restaurar uma API REST
Agora, abordaremos vários exemplos de como toouse Olá toobackup da API REST e restaurar um aplicativo. Cada exemplo inclui uma URL e um corpo de solicitação HTTP. URL de exemplo Hello contém espaços reservados encapsulados entre chaves, como {id da assinatura}. Substitua espaços reservados de saudação com informações correspondentes de saudação para seu aplicativo. Para referência, aqui está uma explicação de cada espaço reservado que aparece em URLs de exemplo hello.

* id de assinatura – ID do aplicativo de recipiente Olá Olá assinatura do Azure
* Resource-group-name – nome do aplicativo grupo Olá contém recursos Olá
* nome – nome do aplicativo hello
* id de backup – ID do backup do aplicativo hello

Para obter documentação completa de saudação API Olá, incluindo vários parâmetros opcionais que podem ser incluídos na solicitação de saudação HTTP, consulte Olá [Gerenciador de recursos do Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Fazer backup de um aplicativo sob demanda
tooback um aplicativo enviar imediatamente, um **POST** solicitação muito**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backup /**.

Olá URL é semelhante ao seguinte usando nosso site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Forneça um objeto JSON no corpo de saudação do seu toospecify de solicitação que toostore de toouse de conta de armazenamento Olá backup. objeto JSON Olá deve ter uma propriedade chamada **storageAccountUrl**, que mantém um [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) conceder acesso de gravação contêiner de armazenamento do Azure de toohello que contém o blob de backup hello. Se você quiser tooback backup de seus bancos de dados, você também deve fornecer uma lista contendo Olá nomes, tipos e cadeias de caracteres de conexão de saudação toobe de bancos de dados feito backup.

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

Um backup do aplicativo hello começa imediatamente quando a solicitação de saudação é recebida. o processo de backup Olá pode levar um longo tempo toocomplete. Olá resposta HTTP contém uma ID que você pode usar em outra solicitação toosee Olá status de saudação backup. Aqui está um exemplo de corpo de saudação de solicitação de HTTP resposta tooour backup hello.

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> Mensagens de erro podem ser encontradas na propriedade log Olá Olá resposta HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Agendar backups automáticos
Em adição toobacking backup de um aplicativo sob demanda, você também pode agendar um backup toohappen automaticamente.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Configurar um novo agendamento de backup automático
tooset um agendamento de backup, enviar um **colocar** solicitação muito**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config backup/**.

Aqui está a aparência de saudação URL para o site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

corpo da solicitação Olá deve ter um objeto JSON que especifica a configuração de backup hello. Aqui está um exemplo com todos os parâmetros de saudação necessário.

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

Este exemplo configura Olá aplicativo toobe backup automaticamente a cada sete dias. Olá parâmetros **frequencyInterval** e **frequencyUnit** juntos determinar com que frequência hello backups acontecem. Os valores válidos para **frequencyUnit** são **hora** e **dia**. Por exemplo, tooback backup de um aplicativo a cada 12 horas, defina toohour de too12 e frequencyUnit frequencyInterval.

Backups antigos serão removidos automaticamente da conta de armazenamento hello. Você pode controlar Olá quanto tempo os backups podem ser por configuração Olá **retentionPeriodInDays** parâmetro. Se você quiser tooalways ter pelo menos um backup salvo, independentemente de quanto tempo ele é, definido **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Obter o agendamento de backup automático Olá
tooget um aplicativo fazer backup de configuração, envie um **POST** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ {nome} / sites/backup/config/lista**.

URL de saudação do nosso site de exemplo é **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Obter status de saudação de um backup
Dependendo de quão grande aplicativo de saudação é, um backup pode demorar um pouco toocomplete. Os backups também podem falhar, o tempo limite pode ser ultrapassado ou ocorrer parcialmente. toosee Olá status dos backups de todos os do aplicativo, enviar um **obter** toohello URL da solicitação **https://management.azure.com/subscriptions/ {id da assinatura} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.

status de saudação toosee de um backup específico, enviar uma solicitação de GET toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { backup-id}**.

Aqui está a aparência de saudação URL para o site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

corpo da resposta Olá contém um exemplo de toothis JSON objeto semelhante.

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

status de saudação de um backup é um tipo enumerado. Veja abaixo cada estado possível.

* Em andamento 0 –: backup Olá foi iniciada mas ainda não foi concluído.
* 1 – falha: backup Olá teve êxito.
* 2 – êxito: backup de saudação foi concluído com êxito.
* 3 – TimedOut: backup Olá não foi concluída no tempo e foi cancelada.
* 4 – criado: solicitação de backup hello está na fila, mas não foi iniciada.
* 5 – ignorada: backup Olá não possa prosseguir devido a agenda tooa disparo muitos backups.
* 6 – PartiallySucceeded: backup Olá bem-sucedida, mas alguns arquivos não foram feitos porque não pôde ser lido. Isso geralmente ocorre porque um bloqueio exclusivo foi colocado em arquivos de saudação.
* 7 – DeleteInProgress: backup Olá foi solicitado toobe excluído, mas ainda não foi excluído.
* 8 – DeleteFailed: não foi possível excluir o backup de saudação. Isso pode acontecer porque Olá URL de SAS que foi usado toocreate backup de saudação expirou.
* 9 – excluídos: backup Olá foi excluído com êxito.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Restaurar um aplicativo usando um backup
Se seu aplicativo tiver sido excluído ou se você deseja que a versão anterior do aplicativo tooa toorevert, você pode restaurar o aplicativo hello de um backup. tooinvoke uma restauração, enviar um **POST** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backups / {backup-id} / restauração**.

Aqui está a aparência de saudação URL para o site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

No corpo da solicitação de hello, envie um objeto JSON que contém propriedades Olá Olá operação de restauração. Veja um exemplo que contém todas as propriedades necessárias:

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a>Restaurar tooa novo aplicativo
Às vezes, convém toocreate um novo aplicativo quando você restaurar um backup, em vez de substituir um aplicativo já existente. toodo, alteração Olá solicitação URL toopoint toohello novo aplicativo você deseja toocreate e alterar Olá **substituir** propriedade Olá JSON muito**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Excluir um backup de aplicativo
Se você quiser toodelete um backup, envie um **excluir** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / /backups/ {backup-id} de {nome}**.

Aqui está a aparência de saudação URL para o site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Gerenciar a URL de SAS de um backup
Serviço de aplicativo do Azure tentará toodelete o backup do armazenamento do Azure usando Olá URL de SAS que foram fornecidas quando Olá backup foi criado. Se essa URL SAS não é mais válida, Olá backup não é excluído por meio da API REST de saudação. No entanto, você pode atualizar Olá URL SAS associada a um backup, enviando um **POST** toohello URL da solicitação **/resourceGroups/ https://management.azure.com/subscriptions/ {id da assinatura} {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Aqui está a aparência de saudação URL para o site de exemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

No corpo da solicitação de hello, envie um objeto JSON que contém a nova URL de SAS hello. Aqui está um exemplo.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Por motivos de segurança, Olá que URL SAS associada a um backup não é retornado ao enviar uma solicitação GET para um backup específico. Se você desejar Olá tooview URL SAS associada a um backup, envie um toohello de solicitação POST mesma URL acima. Inclua um objeto JSON no corpo da solicitação de saudação. resposta de saudação do servidor de saudação contém todas as informações do backup, incluindo a URL de SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
