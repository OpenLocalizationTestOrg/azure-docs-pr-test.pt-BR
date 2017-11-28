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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="68363-103">Usar o REST tooback e restaurar aplicativos de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="68363-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68363-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68363-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="68363-105">API REST</span><span class="sxs-lookup"><span data-stu-id="68363-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="68363-106">[aplicativos do Serviço de Aplicativo](https://azure.microsoft.com/services/app-service/web/) pode ser feito como blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="68363-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="68363-107">backup Olá também pode conter os bancos de dados do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="68363-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="68363-108">Se o aplicativo hello é nunca acidentalmente excluído, ou se toobe de necessidades de aplicativo hello revertido versão anterior do tooa, podem ser restaurado de qualquer backup anterior.</span><span class="sxs-lookup"><span data-stu-id="68363-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="68363-109">Os backups podem ser realizados a qualquer momento e sob demanda ou podem ser agendados em intervalos adequados.</span><span class="sxs-lookup"><span data-stu-id="68363-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="68363-110">Este artigo explica como toobackup e restauração de um aplicativo com a API RESTful solicitações.</span><span class="sxs-lookup"><span data-stu-id="68363-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="68363-111">Se deseja toocreate e gerencie os backups de aplicativo graficamente no hello portal do Azure, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="68363-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="68363-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="68363-112">Getting Started</span></span>
<span data-ttu-id="68363-113">solicitações de toosend REST, você precisa tooknow seu aplicativo **nome**, **grupo de recursos**, e **id da assinatura**. Essas informações podem ser encontradas clicando em seu aplicativo hello **do serviço de aplicativo** folha de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68363-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="68363-114">Para obter exemplos de saudação neste artigo, estamos Configurando site Olá **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="68363-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="68363-115">Ele é armazenado no grupo de recursos padrão-Web-WestUS hello e está em execução em uma assinatura com hello ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="68363-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informações do site de exemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="68363-117">Fazer backup e restaurar uma API REST</span><span class="sxs-lookup"><span data-stu-id="68363-117">Backup and restore REST API</span></span>
<span data-ttu-id="68363-118">Agora, abordaremos vários exemplos de como toouse Olá toobackup da API REST e restaurar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68363-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="68363-119">Cada exemplo inclui uma URL e um corpo de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="68363-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="68363-120">URL de exemplo Hello contém espaços reservados encapsulados entre chaves, como {id da assinatura}.</span><span class="sxs-lookup"><span data-stu-id="68363-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="68363-121">Substitua espaços reservados de saudação com informações correspondentes de saudação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68363-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="68363-122">Para referência, aqui está uma explicação de cada espaço reservado que aparece em URLs de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="68363-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="68363-123">id de assinatura – ID do aplicativo de recipiente Olá Olá assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="68363-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="68363-124">Resource-group-name – nome do aplicativo grupo Olá contém recursos Olá</span><span class="sxs-lookup"><span data-stu-id="68363-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="68363-125">nome – nome do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68363-125">name – Name of hello app</span></span>
* <span data-ttu-id="68363-126">id de backup – ID do backup do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68363-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="68363-127">Para obter documentação completa de saudação API Olá, incluindo vários parâmetros opcionais que podem ser incluídos na solicitação de saudação HTTP, consulte Olá [Gerenciador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68363-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="68363-128">Fazer backup de um aplicativo sob demanda</span><span class="sxs-lookup"><span data-stu-id="68363-128">Backup an app on demand</span></span>
<span data-ttu-id="68363-129">tooback um aplicativo enviar imediatamente, um **POST** solicitação muito**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backup /**.</span><span class="sxs-lookup"><span data-stu-id="68363-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="68363-130">Olá URL é semelhante ao seguinte usando nosso site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="68363-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="68363-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="68363-132">Forneça um objeto JSON no corpo de saudação do seu toospecify de solicitação que toostore de toouse de conta de armazenamento Olá backup.</span><span class="sxs-lookup"><span data-stu-id="68363-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="68363-133">objeto JSON Olá deve ter uma propriedade chamada **storageAccountUrl**, que mantém um [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) conceder acesso de gravação contêiner de armazenamento do Azure de toohello que contém o blob de backup hello.</span><span class="sxs-lookup"><span data-stu-id="68363-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="68363-134">Se você quiser tooback backup de seus bancos de dados, você também deve fornecer uma lista contendo Olá nomes, tipos e cadeias de caracteres de conexão de saudação toobe de bancos de dados feito backup.</span><span class="sxs-lookup"><span data-stu-id="68363-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

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

<span data-ttu-id="68363-135">Um backup do aplicativo hello começa imediatamente quando a solicitação de saudação é recebida.</span><span class="sxs-lookup"><span data-stu-id="68363-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="68363-136">o processo de backup Olá pode levar um longo tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="68363-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="68363-137">Olá resposta HTTP contém uma ID que você pode usar em outra solicitação toosee Olá status de saudação backup.</span><span class="sxs-lookup"><span data-stu-id="68363-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="68363-138">Aqui está um exemplo de corpo de saudação de solicitação de HTTP resposta tooour backup hello.</span><span class="sxs-lookup"><span data-stu-id="68363-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

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
> <span data-ttu-id="68363-139">Mensagens de erro podem ser encontradas na propriedade log Olá Olá resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="68363-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="68363-140">Agendar backups automáticos</span><span class="sxs-lookup"><span data-stu-id="68363-140">Schedule automatic backups</span></span>
<span data-ttu-id="68363-141">Em adição toobacking backup de um aplicativo sob demanda, você também pode agendar um backup toohappen automaticamente.</span><span class="sxs-lookup"><span data-stu-id="68363-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="68363-142">Configurar um novo agendamento de backup automático</span><span class="sxs-lookup"><span data-stu-id="68363-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="68363-143">tooset um agendamento de backup, enviar um **colocar** solicitação muito**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config backup/**.</span><span class="sxs-lookup"><span data-stu-id="68363-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="68363-144">Aqui está a aparência de saudação URL para o site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="68363-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="68363-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="68363-146">corpo da solicitação Olá deve ter um objeto JSON que especifica a configuração de backup hello.</span><span class="sxs-lookup"><span data-stu-id="68363-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="68363-147">Aqui está um exemplo com todos os parâmetros de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="68363-147">Here is an example with all hello required parameters.</span></span>

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

<span data-ttu-id="68363-148">Este exemplo configura Olá aplicativo toobe backup automaticamente a cada sete dias.</span><span class="sxs-lookup"><span data-stu-id="68363-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="68363-149">Olá parâmetros **frequencyInterval** e **frequencyUnit** juntos determinar com que frequência hello backups acontecem.</span><span class="sxs-lookup"><span data-stu-id="68363-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="68363-150">Os valores válidos para **frequencyUnit** são **hora** e **dia**.</span><span class="sxs-lookup"><span data-stu-id="68363-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="68363-151">Por exemplo, tooback backup de um aplicativo a cada 12 horas, defina toohour de too12 e frequencyUnit frequencyInterval.</span><span class="sxs-lookup"><span data-stu-id="68363-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="68363-152">Backups antigos serão removidos automaticamente da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="68363-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="68363-153">Você pode controlar Olá quanto tempo os backups podem ser por configuração Olá **retentionPeriodInDays** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="68363-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="68363-154">Se você quiser tooalways ter pelo menos um backup salvo, independentemente de quanto tempo ele é, definido **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="68363-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="68363-155">Obter o agendamento de backup automático Olá</span><span class="sxs-lookup"><span data-stu-id="68363-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="68363-156">tooget um aplicativo fazer backup de configuração, envie um **POST** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ {nome} / sites/backup/config/lista**.</span><span class="sxs-lookup"><span data-stu-id="68363-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="68363-157">URL de saudação do nosso site de exemplo é **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="68363-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="68363-158">Obter status de saudação de um backup</span><span class="sxs-lookup"><span data-stu-id="68363-158">Get hello status of a backup</span></span>
<span data-ttu-id="68363-159">Dependendo de quão grande aplicativo de saudação é, um backup pode demorar um pouco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="68363-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="68363-160">Os backups também podem falhar, o tempo limite pode ser ultrapassado ou ocorrer parcialmente.</span><span class="sxs-lookup"><span data-stu-id="68363-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="68363-161">toosee Olá status dos backups de todos os do aplicativo, enviar um **obter** toohello URL da solicitação **https://management.azure.com/subscriptions/ {id da assinatura} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="68363-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="68363-162">status de saudação toosee de um backup específico, enviar uma solicitação de GET toohello URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="68363-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="68363-163">Aqui está a aparência de saudação URL para o site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="68363-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="68363-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="68363-165">corpo da resposta Olá contém um exemplo de toothis JSON objeto semelhante.</span><span class="sxs-lookup"><span data-stu-id="68363-165">hello response body contains a JSON object similar toothis example.</span></span>

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

<span data-ttu-id="68363-166">status de saudação de um backup é um tipo enumerado.</span><span class="sxs-lookup"><span data-stu-id="68363-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="68363-167">Veja abaixo cada estado possível.</span><span class="sxs-lookup"><span data-stu-id="68363-167">Here is every possible state.</span></span>

* <span data-ttu-id="68363-168">Em andamento 0 –: backup Olá foi iniciada mas ainda não foi concluído.</span><span class="sxs-lookup"><span data-stu-id="68363-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="68363-169">1 – falha: backup Olá teve êxito.</span><span class="sxs-lookup"><span data-stu-id="68363-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="68363-170">2 – êxito: backup de saudação foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="68363-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="68363-171">3 – TimedOut: backup Olá não foi concluída no tempo e foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="68363-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="68363-172">4 – criado: solicitação de backup hello está na fila, mas não foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="68363-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="68363-173">5 – ignorada: backup Olá não possa prosseguir devido a agenda tooa disparo muitos backups.</span><span class="sxs-lookup"><span data-stu-id="68363-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="68363-174">6 – PartiallySucceeded: backup Olá bem-sucedida, mas alguns arquivos não foram feitos porque não pôde ser lido.</span><span class="sxs-lookup"><span data-stu-id="68363-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="68363-175">Isso geralmente ocorre porque um bloqueio exclusivo foi colocado em arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="68363-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="68363-176">7 – DeleteInProgress: backup Olá foi solicitado toobe excluído, mas ainda não foi excluído.</span><span class="sxs-lookup"><span data-stu-id="68363-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="68363-177">8 – DeleteFailed: não foi possível excluir o backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="68363-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="68363-178">Isso pode acontecer porque Olá URL de SAS que foi usado toocreate backup de saudação expirou.</span><span class="sxs-lookup"><span data-stu-id="68363-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="68363-179">9 – excluídos: backup Olá foi excluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="68363-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="68363-180">Restaurar um aplicativo usando um backup</span><span class="sxs-lookup"><span data-stu-id="68363-180">Restore an app from a backup</span></span>
<span data-ttu-id="68363-181">Se seu aplicativo tiver sido excluído ou se você deseja que a versão anterior do aplicativo tooa toorevert, você pode restaurar o aplicativo hello de um backup.</span><span class="sxs-lookup"><span data-stu-id="68363-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="68363-182">tooinvoke uma restauração, enviar um **POST** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ backups / {backup-id} / restauração**.</span><span class="sxs-lookup"><span data-stu-id="68363-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="68363-183">Aqui está a aparência de saudação URL para o site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="68363-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="68363-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="68363-185">No corpo da solicitação de hello, envie um objeto JSON que contém propriedades Olá Olá operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="68363-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="68363-186">Veja um exemplo que contém todas as propriedades necessárias:</span><span class="sxs-lookup"><span data-stu-id="68363-186">Here is an example containing all required properties:</span></span>

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

### <a name="restore-tooa-new-app"></a><span data-ttu-id="68363-187">Restaurar tooa novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="68363-187">Restore tooa new app</span></span>
<span data-ttu-id="68363-188">Às vezes, convém toocreate um novo aplicativo quando você restaurar um backup, em vez de substituir um aplicativo já existente.</span><span class="sxs-lookup"><span data-stu-id="68363-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="68363-189">toodo, alteração Olá solicitação URL toopoint toohello novo aplicativo você deseja toocreate e alterar Olá **substituir** propriedade Olá JSON muito**false**.</span><span class="sxs-lookup"><span data-stu-id="68363-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="68363-190">Excluir um backup de aplicativo</span><span class="sxs-lookup"><span data-stu-id="68363-190">Delete an app backup</span></span>
<span data-ttu-id="68363-191">Se você quiser toodelete um backup, envie um **excluir** toohello URL da solicitação **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / /backups/ {backup-id} de {nome}**.</span><span class="sxs-lookup"><span data-stu-id="68363-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="68363-192">Aqui está a aparência de saudação URL para o site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="68363-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="68363-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="68363-194">Gerenciar a URL de SAS de um backup</span><span class="sxs-lookup"><span data-stu-id="68363-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="68363-195">Serviço de aplicativo do Azure tentará toodelete o backup do armazenamento do Azure usando Olá URL de SAS que foram fornecidas quando Olá backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="68363-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="68363-196">Se essa URL SAS não é mais válida, Olá backup não é excluído por meio da API REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="68363-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="68363-197">No entanto, você pode atualizar Olá URL SAS associada a um backup, enviando um **POST** toohello URL da solicitação **/resourceGroups/ https://management.azure.com/subscriptions/ {id da assinatura} {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="68363-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="68363-198">Aqui está a aparência de saudação URL para o site de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="68363-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="68363-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="68363-200">No corpo da solicitação de hello, envie um objeto JSON que contém a nova URL de SAS hello.</span><span class="sxs-lookup"><span data-stu-id="68363-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="68363-201">Aqui está um exemplo.</span><span class="sxs-lookup"><span data-stu-id="68363-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="68363-202">Por motivos de segurança, Olá que URL SAS associada a um backup não é retornado ao enviar uma solicitação GET para um backup específico.</span><span class="sxs-lookup"><span data-stu-id="68363-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="68363-203">Se você desejar Olá tooview URL SAS associada a um backup, envie um toohello de solicitação POST mesma URL acima.</span><span class="sxs-lookup"><span data-stu-id="68363-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="68363-204">Inclua um objeto JSON no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="68363-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="68363-205">resposta de saudação do servidor de saudação contém todas as informações do backup, incluindo a URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="68363-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
