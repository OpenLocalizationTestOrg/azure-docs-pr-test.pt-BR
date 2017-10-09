---
title: "exportação de aaaImport de identidades de dispositivo do Azure IoT Hub | Microsoft Docs"
description: "Como toouse hello Azure IoT serviço SDK tooperform operações em relação a saudação tooimport de registro de identidade e exportação em massa identidades de dispositivo. Operações de importação permitem que você toocreate, update e delete identidades de dispositivo em massa."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="9af12-104">Gerenciar identidades de dispositivo do Hub IoT em massa</span><span class="sxs-lookup"><span data-stu-id="9af12-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="9af12-105">Cada hub IoT tem um registro de identidade que você pode usar recursos de cada dispositivo toocreate no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9af12-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="9af12-106">registro de identidade Olá também permite que você toocontrol pontos de extremidade de acesso toohello voltadas para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9af12-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="9af12-107">Este artigo descreve como identidades de dispositivo de tooimport e exportação em massa tooand de um registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="9af12-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="9af12-108">Operações de importação e exportação ocorrem no contexto de saudação do *trabalhos* que permitem operações de serviço tooexecute em massa em relação a um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="9af12-109">Olá **RegistryManager** classe inclui Olá **ExportDevicesAsync** e **ImportDevicesAsync** métodos que usam Olá **trabalho** estrutura.</span><span class="sxs-lookup"><span data-stu-id="9af12-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="9af12-110">Esses métodos permitem que você tooexport, importar e sincronizar a totalidade de saudação de um registro de identidade de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="9af12-111">O que são trabalhos?</span><span class="sxs-lookup"><span data-stu-id="9af12-111">What are jobs?</span></span>

<span data-ttu-id="9af12-112">Operações de registro de identidade usam Olá **trabalho** sistema hello quando a operação:</span><span class="sxs-lookup"><span data-stu-id="9af12-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="9af12-113">Tem um tempo de execução potencialmente longo comparados toostandard operações de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9af12-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="9af12-114">Retorna uma grande quantidade de usuário de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="9af12-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="9af12-115">Em vez de uma única chamada de API aguardando ou bloqueio no resultado de saudação da operação hello, operação Olá cria de maneira assíncrona um **trabalho** do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="9af12-116">operação de saudação e imediatamente retorna um **JobProperties** objeto.</span><span class="sxs-lookup"><span data-stu-id="9af12-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="9af12-117">Olá seguir c# code trecho de código mostra como toocreate um trabalho de exportação:</span><span class="sxs-lookup"><span data-stu-id="9af12-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="9af12-118">Olá toouse **RegistryManager** classe em seu código c#, adicione Olá **Microsoft.Azure.Devices** tooyour de pacote NuGet projeto.</span><span class="sxs-lookup"><span data-stu-id="9af12-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="9af12-119">Olá **RegistryManager** classe está no hello **Microsoft.Azure.Devices** namespace.</span><span class="sxs-lookup"><span data-stu-id="9af12-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="9af12-120">Você pode usar o hello **RegistryManager** classe tooquery estado de saudação do hello **trabalho** usando Olá retornado **JobProperties** metadados.</span><span class="sxs-lookup"><span data-stu-id="9af12-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="9af12-121">Olá seguinte trecho de código c# mostra como toopoll toosee cada cinco segundos se hello trabalho concluiu a execução:</span><span class="sxs-lookup"><span data-stu-id="9af12-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="9af12-122">Exportar dispositivos</span><span class="sxs-lookup"><span data-stu-id="9af12-122">Export devices</span></span>

<span data-ttu-id="9af12-123">Saudação de uso **ExportDevicesAsync** método tooexport Olá toda uma tooan de registro de identidade de hub IoT [armazenamento do Azure](../storage/index.md) contêiner de blob usando um [assinatura de acesso compartilhado](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="9af12-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="9af12-124">Esse método permite backups de toocreate confiáveis de suas informações de dispositivo em um contêiner de blob que você controle.</span><span class="sxs-lookup"><span data-stu-id="9af12-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="9af12-125">Olá **ExportDevicesAsync** método requer dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9af12-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="9af12-126">Uma *cadeia de caracteres* que contenha um URI de um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="9af12-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="9af12-127">Esse URI deve conter um token SAS que concede acesso de gravação toohello contêiner.</span><span class="sxs-lookup"><span data-stu-id="9af12-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="9af12-128">trabalho de saudação cria um blob de bloco nos dados de dispositivo de exportação contêiner toostore Olá serializado.</span><span class="sxs-lookup"><span data-stu-id="9af12-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="9af12-129">token SAS Olá deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="9af12-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="9af12-130">Um *booliano* que indica se você deseja que as chaves de autenticação tooexclude de seus dados de exportação.</span><span class="sxs-lookup"><span data-stu-id="9af12-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="9af12-131">Se for **false**, as chaves de autenticação serão incluídas na saída de exportação.</span><span class="sxs-lookup"><span data-stu-id="9af12-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="9af12-132">Caso contrário, as chaves serão exportadas como **null**.</span><span class="sxs-lookup"><span data-stu-id="9af12-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="9af12-133">Olá seguinte trecho de código c# mostra como tooinitiate um trabalho de exportação que inclui as chaves de autenticação de dispositivo em Olá exportar dados e então sondam conclusão:</span><span class="sxs-lookup"><span data-stu-id="9af12-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="9af12-134">Olá trabalho armazena sua saída no contêiner de blob Olá fornecido como um blob de bloco com nome hello **Devices**.</span><span class="sxs-lookup"><span data-stu-id="9af12-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="9af12-135">dados de saída de saudação consistem em dados de dispositivo JSON serializado, com um dispositivo por linha.</span><span class="sxs-lookup"><span data-stu-id="9af12-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="9af12-136">Olá, exemplo a seguir mostra os dados de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="9af12-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se um dispositivo tiver dados de duas, dados de duas Olá também são exportados junto com os dados do dispositivo hello. Olá, exemplo a seguir mostra esse formato. <span data-ttu-id="9af12-139">Todos os dados da linha de "twinETag" hello até o término de saudação são dados de duas.</span><span class="sxs-lookup"><span data-stu-id="9af12-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="9af12-140">Se você precisar acessar dados toothis no código, você pode facilmente desserializar dados usando Olá **ExportImportDevice** classe.</span><span class="sxs-lookup"><span data-stu-id="9af12-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="9af12-141">Olá seguinte trecho de código c# mostra como informações do dispositivo tooread que foi exportado anteriormente tooa blob de blocos:</span><span class="sxs-lookup"><span data-stu-id="9af12-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="9af12-142">Você também pode usar o hello **GetDevicesAsync** método hello **RegistryManager** classe toofetch uma lista de seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9af12-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="9af12-143">No entanto, essa abordagem tem um limite rígido de 1000 no número de saudação de objetos de dispositivo que são retornados.</span><span class="sxs-lookup"><span data-stu-id="9af12-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="9af12-144">Olá esperado caso de uso para Olá **GetDevicesAsync** método é para depuração de tooaid de cenários de desenvolvimento e não é recomendado para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="9af12-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="9af12-145">Importar dispositivos</span><span class="sxs-lookup"><span data-stu-id="9af12-145">Import devices</span></span>

<span data-ttu-id="9af12-146">Olá **ImportDevicesAsync** método hello **RegistryManager** classe permite que operações de importação e sincronização de em massa de tooperform em um registro de identidade de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="9af12-147">Como Olá **ExportDevicesAsync** método, Olá **ImportDevicesAsync** usa o método hello **trabalho** framework.</span><span class="sxs-lookup"><span data-stu-id="9af12-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="9af12-148">Tome cuidado usar Olá **ImportDevicesAsync** método porque na adição tooprovisioning novos dispositivos em seu registro de identidade, ele também pode atualizar e excluir dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="9af12-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="9af12-149">Uma operação de importação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="9af12-149">An import operation cannot be undone.</span></span> <span data-ttu-id="9af12-150">Sempre faça backup dos dados existentes usando Olá **ExportDevicesAsync** tooyour registro de identidade de alterações do contêiner de blob do método tooanother antes de fazer em massa.</span><span class="sxs-lookup"><span data-stu-id="9af12-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="9af12-151">Olá **ImportDevicesAsync** método aceita dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9af12-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="9af12-152">Um *cadeia de caracteres* que contém um URI de um [armazenamento do Azure](../storage/index.md) blob toouse contêiner como *entrada* toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="9af12-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="9af12-153">Esse URI deve conter um token SAS que concede acesso de leitura toohello contêiner.</span><span class="sxs-lookup"><span data-stu-id="9af12-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="9af12-154">Este contêiner deve conter um blob com nome hello **Devices** que contém Olá serializado tooimport de dados de dispositivo para o registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="9af12-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="9af12-155">Olá importação de dados deve conter informações do dispositivo no hello JSON mesmo formato que Olá **ExportImportDevice** trabalho usa quando ele cria uma **Devices** blob.</span><span class="sxs-lookup"><span data-stu-id="9af12-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="9af12-156">token SAS Olá deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="9af12-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="9af12-157">Um *cadeia de caracteres* que contém um URI de um [armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contêiner como *saída* de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9af12-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="9af12-158">Olá trabalho cria um blob de bloco no toostore contêiner qualquer informação de erro de importação de saudação concluída **trabalho**.</span><span class="sxs-lookup"><span data-stu-id="9af12-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="9af12-159">token SAS Olá deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="9af12-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="9af12-160">parâmetros de saudação dois podem apontar toohello mesmo contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="9af12-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="9af12-161">parâmetros separados Olá simplesmente permitem mais controle sobre os dados como o contêiner de saída Olá requer permissões adicionais.</span><span class="sxs-lookup"><span data-stu-id="9af12-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="9af12-162">Olá seguir c# code trecho de código mostra como tooinitiate um trabalho de importação:</span><span class="sxs-lookup"><span data-stu-id="9af12-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="9af12-163">Esse método também pode ser usado tooimport Olá dados para duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9af12-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="9af12-164">formato Olá Olá entrada de dados é Olá mesmo como formato Olá mostrado Olá **ExportDevicesAsync** seção.</span><span class="sxs-lookup"><span data-stu-id="9af12-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="9af12-165">Dessa forma, você pode reimportar dados hello exportada.</span><span class="sxs-lookup"><span data-stu-id="9af12-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="9af12-166">Olá **$metadata** é opcional.</span><span class="sxs-lookup"><span data-stu-id="9af12-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="9af12-167">Comportamento de importação</span><span class="sxs-lookup"><span data-stu-id="9af12-167">Import behavior</span></span>

<span data-ttu-id="9af12-168">Você pode usar o hello **ImportDevicesAsync** seguinte de saudação do método tooperform em massa operações em seu registro de identidade:</span><span class="sxs-lookup"><span data-stu-id="9af12-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="9af12-169">Registro em massa de novos dispositivos</span><span class="sxs-lookup"><span data-stu-id="9af12-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="9af12-170">Exclusões em massa dos dispositivos existentes</span><span class="sxs-lookup"><span data-stu-id="9af12-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="9af12-171">Alterações de status em massa (habilitar ou desabilitar dispositivos)</span><span class="sxs-lookup"><span data-stu-id="9af12-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="9af12-172">Atribuição em massa de novas chaves de autenticação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="9af12-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="9af12-173">Nova geração automática em massa de chaves de autenticação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="9af12-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="9af12-174">Atualização em massa de dados gêmeos</span><span class="sxs-lookup"><span data-stu-id="9af12-174">Bulk update of twin data</span></span>

<span data-ttu-id="9af12-175">Você pode executar qualquer combinação de saudação anterior de operações em um único **ImportDevicesAsync** chamar.</span><span class="sxs-lookup"><span data-stu-id="9af12-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="9af12-176">Por exemplo, você pode registrar novos dispositivos e excluir ou atualizar os dispositivos existentes no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9af12-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="9af12-177">Quando usada com hello **ExportDevicesAsync** método, você pode migrar completamente todos os dispositivos de um tooanother de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="9af12-178">Se o arquivo de importação de saudação inclui duas metadados, metadados substitui os metadados existentes duas hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="9af12-179">Se o arquivo de importação de saudação não inclui duas metadados, em seguida, somente Olá `lastUpdateTime` metadados são atualizados usando Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="9af12-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="9af12-180">Saudação de uso opcional **importMode** propriedade nos dados de serialização de importação Olá para cada dispositivo toocontrol Olá importação processo por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9af12-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="9af12-181">Olá **importMode** propriedade tem Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="9af12-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="9af12-182">importMode</span><span class="sxs-lookup"><span data-stu-id="9af12-182">importMode</span></span> | <span data-ttu-id="9af12-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="9af12-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9af12-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="9af12-184">**createOrUpdate**</span></span> |<span data-ttu-id="9af12-185">Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="9af12-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9af12-186">Se já existe um dispositivo Olá, informações existentes serão substituídas pelo Olá fornecido dados de entrada sem levar em consideração toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="9af12-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="9af12-187">usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="9af12-188">etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="9af12-189">Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-190">**create**</span><span class="sxs-lookup"><span data-stu-id="9af12-190">**create**</span></span> |<span data-ttu-id="9af12-191">Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="9af12-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9af12-192">Se o dispositivo de saudação já existir, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="9af12-193">usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="9af12-194">etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="9af12-195">Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-196">**atualizar**</span><span class="sxs-lookup"><span data-stu-id="9af12-196">**update**</span></span> |<span data-ttu-id="9af12-197">Se já existe um dispositivo com hello especificado **id**, as informações existentes sejam substituídas com hello fornecido dados de entrada sem levar em consideração toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="9af12-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="9af12-198">Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9af12-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="9af12-200">Se já existe um dispositivo com hello especificado **id**, as informações existentes sejam substituídas com hello fornecido dados de entrada somente se houver um **ETag** corresponder.</span><span class="sxs-lookup"><span data-stu-id="9af12-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="9af12-201">Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="9af12-202">Se houver um **ETag** incompatibilidade, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9af12-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="9af12-204">Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="9af12-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="9af12-205">Se já existe um dispositivo Olá, informações existentes serão substituídas pelo Olá fornecido dados de entrada somente se houver um **ETag** corresponder.</span><span class="sxs-lookup"><span data-stu-id="9af12-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="9af12-206">Se houver um **ETag** incompatibilidade, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="9af12-207">usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="9af12-208">etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9af12-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="9af12-209">Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="9af12-210">**delete**</span></span> |<span data-ttu-id="9af12-211">Se já existe um dispositivo com hello especificado **id**, ele será excluído sem considerar toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="9af12-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="9af12-212">Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="9af12-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="9af12-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="9af12-214">Se já existe um dispositivo com hello especificado **id**, ele é excluído somente se houver um **ETag** corresponder.</span><span class="sxs-lookup"><span data-stu-id="9af12-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="9af12-215">Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="9af12-216">Se houver uma incompatibilidade de ETag, um erro será gravado toohello arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="9af12-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="9af12-217">Se os dados de serialização Olá não definir explicitamente um **importMode** sinalizador para um dispositivo, o padrão é muito**createOrUpdate** Olá durante a operação de importação.</span><span class="sxs-lookup"><span data-stu-id="9af12-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="9af12-218">Exemplo de importação de dispositivos – provisionamento de dispositivo em massa</span><span class="sxs-lookup"><span data-stu-id="9af12-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="9af12-219">Olá c# código exemplo a seguir ilustra como toogenerate várias identidades de dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="9af12-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="9af12-220">Inclua as chaves de autenticação.</span><span class="sxs-lookup"><span data-stu-id="9af12-220">Include authentication keys.</span></span>
* <span data-ttu-id="9af12-221">Esse blob de blocos de tooa de informações de dispositivo de gravação.</span><span class="sxs-lookup"><span data-stu-id="9af12-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="9af12-222">Importe dispositivos Olá para registro de identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9af12-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="9af12-223">Exemplo de importação de dispositivos – exclusão em massa</span><span class="sxs-lookup"><span data-stu-id="9af12-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="9af12-224">Olá exemplo de código a seguir mostra como os dispositivos de saudação toodelete adicionados usando Olá exemplo de código anterior:</span><span class="sxs-lookup"><span data-stu-id="9af12-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="9af12-225">Obter URI SAS do contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="9af12-225">Get hello container SAS URI</span></span>

<span data-ttu-id="9af12-226">Olá exemplo de código a seguir mostra como toogenerate uma [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) com leitura, gravação e exclusão de permissões para um contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="9af12-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="9af12-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9af12-227">Next steps</span></span>

<span data-ttu-id="9af12-228">Neste artigo, você aprendeu como tooperform em massa operações no registro de identidade Olá em um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9af12-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="9af12-229">Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="9af12-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="9af12-230">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="9af12-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="9af12-231">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="9af12-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="9af12-232">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="9af12-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9af12-233">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="9af12-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="9af12-234">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9af12-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
