---
title: Importar e exportar identidades de dispositivo do Hub IoT do Azure | Microsoft Docs
description: "Como usar o SDK do serviço IoT do Azure para executar operações em massa no Registro de identidade para importar e exportar identidades de dispositivo. As operações de importação permitem criar, atualizar e excluir as identidades de dispositivo em massa."
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
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="8b390-104">Gerenciar identidades de dispositivo do Hub IoT em massa</span><span class="sxs-lookup"><span data-stu-id="8b390-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="8b390-105">Cada hub IoT tem um registro de identidade que você pode usar para criar recursos por dispositivo no serviço.</span><span class="sxs-lookup"><span data-stu-id="8b390-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="8b390-106">O registro de identidade também permite que você controle o acesso aos pontos de extremidade voltados para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="8b390-107">Este artigo descreve como importar e exportar identidades de dispositivo em massa bidirecionalmente em um registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="8b390-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="8b390-108">As operações de importação e exportação ocorrem no contexto de *Trabalhos* , que permitem aos usuários executar operações de serviço em massa em um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8b390-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="8b390-109">A classe **RegistryManager** inclui os métodos **ExportDevicesAsync** e **ImportDevicesAsync** que usam a estrutura **Job**.</span><span class="sxs-lookup"><span data-stu-id="8b390-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="8b390-110">Esses métodos permitem exportar, importar e sincronizar todo o registro de identidade de um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8b390-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="8b390-111">O que são trabalhos?</span><span class="sxs-lookup"><span data-stu-id="8b390-111">What are jobs?</span></span>

<span data-ttu-id="8b390-112">As operações de registro de identidade usam o sistema de **Trabalho** quando a operação:</span><span class="sxs-lookup"><span data-stu-id="8b390-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="8b390-113">Tem um tempo de execução potencialmente longo em comparação com as operações de tempo de execução padrão.</span><span class="sxs-lookup"><span data-stu-id="8b390-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="8b390-114">Retorna uma grande quantidade de dados para o usuário.</span><span class="sxs-lookup"><span data-stu-id="8b390-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="8b390-115">Em vez de ter uma única chamada à API aguardando ou bloqueando o resultado da operação, a operação cria de modo assíncrono um **Trabalho** para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8b390-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="8b390-116">Então, a operação retorna imediatamente um objeto **JobProperties**.</span><span class="sxs-lookup"><span data-stu-id="8b390-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="8b390-117">O trecho de código de C# a seguir mostra como criar um trabalho de exportação:</span><span class="sxs-lookup"><span data-stu-id="8b390-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="8b390-118">Para usar a classe **RegistryManager** no código C#, adicione o pacote NuGet **Microsoft.Azure.Devices** ao projeto.</span><span class="sxs-lookup"><span data-stu-id="8b390-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="8b390-119">A classe **RegistryManager** está no namespace **Microsoft.Azure.Devices**.</span><span class="sxs-lookup"><span data-stu-id="8b390-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="8b390-120">Você pode usar a classe **RegistryManager** para consultar o estado do **Job** usando os metadados de **JobProperties** retornados.</span><span class="sxs-lookup"><span data-stu-id="8b390-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="8b390-121">O trecho de código de C# a seguir mostra como verificar a cada cinco segundos para ver se o trabalho finalizou a execução:</span><span class="sxs-lookup"><span data-stu-id="8b390-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="8b390-122">Exportar dispositivos</span><span class="sxs-lookup"><span data-stu-id="8b390-122">Export devices</span></span>

<span data-ttu-id="8b390-123">Use o método **ExportDevicesAsync** para exportar todo o registro de identidade de um Hub IoT para um contêiner de blobs do [Armazenamento do Azure](../storage/index.md) usando uma [Assinatura de Acesso Compartilhado](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="8b390-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="8b390-124">Esse método permite criar backups confiáveis das informações do dispositivo em um contêiner de blobs controlado por você.</span><span class="sxs-lookup"><span data-stu-id="8b390-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="8b390-125">O método **ExportDevicesAsync** exige dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8b390-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="8b390-126">Uma *cadeia de caracteres* que contenha um URI de um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8b390-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="8b390-127">Esse URI deve conter um token SAS que conceda acesso de gravação ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="8b390-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="8b390-128">O trabalho cria um blob de blocos nesse contêiner para armazenar os dados do dispositivo de exportação serializados.</span><span class="sxs-lookup"><span data-stu-id="8b390-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="8b390-129">O token SAS deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="8b390-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="8b390-130">Um *booliano* que indica se você deseja excluir chaves de autenticação dos dados de exportação.</span><span class="sxs-lookup"><span data-stu-id="8b390-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="8b390-131">Se for **false**, as chaves de autenticação serão incluídas na saída de exportação.</span><span class="sxs-lookup"><span data-stu-id="8b390-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="8b390-132">Caso contrário, as chaves serão exportadas como **null**.</span><span class="sxs-lookup"><span data-stu-id="8b390-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="8b390-133">O seguinte trecho de código em C# mostra como iniciar um trabalho de exportação que inclui chaves de autenticação de dispositivo nos dados de exportação e, em seguida, pesquisar se houve a conclusão:</span><span class="sxs-lookup"><span data-stu-id="8b390-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

<span data-ttu-id="8b390-134">O trabalho armazena sua saída no contêiner de blobs fornecido como um blob de blocos com o nome **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="8b390-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="8b390-135">Os dados da saída consistem em dados de dispositivo serializados JSON, com um dispositivo por linha.</span><span class="sxs-lookup"><span data-stu-id="8b390-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="8b390-136">O exemplo a seguir mostra os dados de saída:</span><span class="sxs-lookup"><span data-stu-id="8b390-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se um dispositivo tiver dados gêmeos, os dados gêmeos também serão exportados junto com os dados do dispositivo. O exemplo a seguir mostra esse formato. <span data-ttu-id="8b390-139">Todos os dados da linha "twinETag" até o final são dados gêmeos.</span><span class="sxs-lookup"><span data-stu-id="8b390-139">All data from the "twinETag" line until the end are twin data.</span></span>

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

<span data-ttu-id="8b390-140">Se precisar de acesso a esses dados no código, você poderá desserializar facilmente esses dados usando a classe **ExportImportDevice** .</span><span class="sxs-lookup"><span data-stu-id="8b390-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="8b390-141">O seguinte trecho de código de C# mostra como ler informações do dispositivo que foram anteriormente exportadas para um blob de blocos:</span><span class="sxs-lookup"><span data-stu-id="8b390-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

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
> <span data-ttu-id="8b390-142">Você também pode usar o método **GetDevicesAsync** da classe **RegistryManager** para buscar uma lista de seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="8b390-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="8b390-143">No entanto, essa abordagem tem um limite rígido de 1.000 no número de objetos de dispositivo que são retornados.</span><span class="sxs-lookup"><span data-stu-id="8b390-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="8b390-144">O caso de uso esperado para o método **GetDevicesAsync** é para cenários de desenvolvimento como auxílio na depuração, não sendo recomendado para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="8b390-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="8b390-145">Importar dispositivos</span><span class="sxs-lookup"><span data-stu-id="8b390-145">Import devices</span></span>

<span data-ttu-id="8b390-146">O método **ImportDevicesAsync** na classe **RegistryManager** permite que você execute operações em massa de importação e sincronização em um registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8b390-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="8b390-147">Assim como ocorre com o método **ExportDevicesAsync**, o método **ImportDevicesAsync** usa a estrutura **Job**.</span><span class="sxs-lookup"><span data-stu-id="8b390-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="8b390-148">Tenha cuidado ao usar o método **ImportDevicesAsync** porque, além de provisionar novos dispositivos no registro de identidade, ele também pode atualizar e excluir os dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="8b390-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="8b390-149">Uma operação de importação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="8b390-149">An import operation cannot be undone.</span></span> <span data-ttu-id="8b390-150">Sempre faça backup de seus dados existentes usando o método **ExportDevicesAsync** em outro contêiner de blobs antes de fazer alterações em massa no registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="8b390-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="8b390-151">O método **ImportDevicesAsync** usa dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8b390-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="8b390-152">Uma *cadeia de caracteres* que contém um URI de um contêiner de blobs do [Armazenamento do Azure](../storage/index.md) como *entrada* para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="8b390-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="8b390-153">Esse URI deve conter um token SAS que conceda acesso de leitura ao contêiner.</span><span class="sxs-lookup"><span data-stu-id="8b390-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="8b390-154">Esse contêiner deve conter um blob com o nome **devices.txt** que contém os dados de dispositivo serializados a serem importados no registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="8b390-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="8b390-155">Os dados de importação devem conter informações do dispositivo no mesmo formato JSON usado pelo trabalho **ExportImportDevice** ao criar um blob **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="8b390-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="8b390-156">O token SAS deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="8b390-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="8b390-157">Uma *cadeia de caracteres* que contém um URI de um contêiner de blobs do [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) como *saída* do trabalho.</span><span class="sxs-lookup"><span data-stu-id="8b390-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="8b390-158">O trabalho cria um blob de blocos nesse contêiner para armazenar quaisquer informações de erro do **Trabalho**de importação concluído.</span><span class="sxs-lookup"><span data-stu-id="8b390-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="8b390-159">O token SAS deve incluir estas permissões:</span><span class="sxs-lookup"><span data-stu-id="8b390-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="8b390-160">Os dois parâmetros podem apontar para o mesmo contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8b390-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="8b390-161">Os parâmetros separados simplesmente permitem mais controle sobre seus dados, pois o contêiner de saída requer permissões adicionais.</span><span class="sxs-lookup"><span data-stu-id="8b390-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="8b390-162">O trecho de código de C# a seguir mostra como iniciar um trabalho de importação:</span><span class="sxs-lookup"><span data-stu-id="8b390-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="8b390-163">Esse método também pode ser usado para importar os dados para o dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="8b390-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="8b390-164">O formato para a entrada de dados é o mesmo mostrado na seção **ExportDevicesAsync**.</span><span class="sxs-lookup"><span data-stu-id="8b390-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="8b390-165">Dessa forma, você pode reimportar os dados exportados.</span><span class="sxs-lookup"><span data-stu-id="8b390-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="8b390-166">O **$metadata** é opcional.</span><span class="sxs-lookup"><span data-stu-id="8b390-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="8b390-167">Comportamento de importação</span><span class="sxs-lookup"><span data-stu-id="8b390-167">Import behavior</span></span>

<span data-ttu-id="8b390-168">É possível usar o método **ImportDevicesAsync** para executar as seguintes operações em massa no registro de identidade:</span><span class="sxs-lookup"><span data-stu-id="8b390-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="8b390-169">Registro em massa de novos dispositivos</span><span class="sxs-lookup"><span data-stu-id="8b390-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="8b390-170">Exclusões em massa dos dispositivos existentes</span><span class="sxs-lookup"><span data-stu-id="8b390-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="8b390-171">Alterações de status em massa (habilitar ou desabilitar dispositivos)</span><span class="sxs-lookup"><span data-stu-id="8b390-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="8b390-172">Atribuição em massa de novas chaves de autenticação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8b390-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="8b390-173">Nova geração automática em massa de chaves de autenticação de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8b390-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="8b390-174">Atualização em massa de dados gêmeos</span><span class="sxs-lookup"><span data-stu-id="8b390-174">Bulk update of twin data</span></span>

<span data-ttu-id="8b390-175">É possível executar qualquer combinação das operações anteriores em uma única chamada **ImportDevicesAsync** .</span><span class="sxs-lookup"><span data-stu-id="8b390-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="8b390-176">Por exemplo, é possível registrar novos dispositivos e excluir ou atualizar dispositivos existentes ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8b390-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="8b390-177">Quando usado com o método **ExportDevicesAsync** , é possível migrar completamente todos os seus dispositivos de um hub IoT para outro.</span><span class="sxs-lookup"><span data-stu-id="8b390-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="8b390-178">Se o arquivo de importação incluir metadados gêmeos, esses metadados substituirão os metadados gêmeos existentes.</span><span class="sxs-lookup"><span data-stu-id="8b390-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="8b390-179">Se o arquivo de importação não inclui metadados gêmeos, somente os metadados `lastUpdateTime` são atualizados usando a hora atual.</span><span class="sxs-lookup"><span data-stu-id="8b390-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="8b390-180">Use a propriedade opcional **importMode** nos dados de serialização de importação para cada dispositivo para controlar o processo de importação por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="8b390-181">A propriedade **importMode** tem as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="8b390-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="8b390-182">importMode</span><span class="sxs-lookup"><span data-stu-id="8b390-182">importMode</span></span> | <span data-ttu-id="8b390-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b390-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b390-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="8b390-184">**createOrUpdate**</span></span> |<span data-ttu-id="8b390-185">Se não houver um dispositivo com a **id**especificada, isso significará que ele foi registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="8b390-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="8b390-186">Se o dispositivo já existir, as informações existentes serão substituídas pelos dados de entrada fornecidos sem considerar o valor de **ETag** .</span><span class="sxs-lookup"><span data-stu-id="8b390-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="8b390-187">Opcionalmente, o usuário pode especificar dados gêmeos junto com os dados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="8b390-188">A etag do gêmeo, se especificada, será processada independentemente da etag do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="8b390-189">Se houver uma incompatibilidade com a etag do gêmeo existente, um erro será registrado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-190">**create**</span><span class="sxs-lookup"><span data-stu-id="8b390-190">**create**</span></span> |<span data-ttu-id="8b390-191">Se não houver um dispositivo com a **id**especificada, isso significará que ele foi registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="8b390-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="8b390-192">Se o dispositivo já existir, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="8b390-193">Opcionalmente, o usuário pode especificar dados gêmeos junto com os dados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="8b390-194">A etag do gêmeo, se especificada, será processada independentemente da etag do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="8b390-195">Se houver uma incompatibilidade com a etag do gêmeo existente, um erro será registrado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-196">**atualizar**</span><span class="sxs-lookup"><span data-stu-id="8b390-196">**update**</span></span> |<span data-ttu-id="8b390-197">Se já existir um dispositivo com a **id** especificada, as informações existentes serão substituídas pelos dados de entrada fornecidos sem considerar o valor de **ETag**.</span><span class="sxs-lookup"><span data-stu-id="8b390-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="8b390-198">Se o dispositivo não existir, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="8b390-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="8b390-200">Se já existir um dispositivo com a **id** especificada, as informações existentes serão substituídas pelos dados de entrada fornecidos somente se houver uma correspondência de **ETag**.</span><span class="sxs-lookup"><span data-stu-id="8b390-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="8b390-201">Se o dispositivo não existir, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="8b390-202">Se não houver uma correspondência de **ETag** , um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="8b390-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="8b390-204">Se não houver um dispositivo com a **id**especificada, isso significará que ele foi registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="8b390-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="8b390-205">Se o dispositivo já existir, as informações existentes serão substituídas pelos dados de entrada fornecidos somente se houver uma correspondência de **ETag** .</span><span class="sxs-lookup"><span data-stu-id="8b390-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="8b390-206">Se não houver uma correspondência de **ETag** , um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="8b390-207">Opcionalmente, o usuário pode especificar dados gêmeos junto com os dados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="8b390-208">A etag do gêmeo, se especificada, será processada independentemente da etag do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8b390-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="8b390-209">Se houver uma incompatibilidade com a etag do gêmeo existente, um erro será registrado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="8b390-210">**delete**</span></span> |<span data-ttu-id="8b390-211">Se já existir um dispositivo com a **id** especificada, ele será excluído sem considerar o valor de **ETag**.</span><span class="sxs-lookup"><span data-stu-id="8b390-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="8b390-212">Se o dispositivo não existir, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="8b390-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="8b390-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="8b390-214">Se já existir um dispositivo com a **id** especificada, ele será excluído somente se houver uma correspondência de **ETag**.</span><span class="sxs-lookup"><span data-stu-id="8b390-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="8b390-215">Se o dispositivo não existir, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="8b390-216">Se não houver uma correspondência de ETag, um erro será gravado no arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8b390-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="8b390-217">Se os dados de serialização não definirem explicitamente um sinalizador **importMode** para um dispositivo, eles usarão **createOrUpdate** como padrão durante a operação de importação.</span><span class="sxs-lookup"><span data-stu-id="8b390-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="8b390-218">Exemplo de importação de dispositivos – provisionamento de dispositivo em massa</span><span class="sxs-lookup"><span data-stu-id="8b390-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="8b390-219">O seguinte exemplo de código C# ilustra como gerar várias identidades de dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="8b390-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="8b390-220">Inclua as chaves de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b390-220">Include authentication keys.</span></span>
* <span data-ttu-id="8b390-221">Grave essas informações de dispositivo em um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="8b390-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="8b390-222">Importe os dispositivos para o registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="8b390-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="8b390-223">Exemplo de importação de dispositivos – exclusão em massa</span><span class="sxs-lookup"><span data-stu-id="8b390-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="8b390-224">O exemplo de código a seguir mostra como excluir os dispositivos que você adicionou usando o exemplo de código anterior:</span><span class="sxs-lookup"><span data-stu-id="8b390-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="8b390-225">Obter o URI de SAS do contêiner</span><span class="sxs-lookup"><span data-stu-id="8b390-225">Get the container SAS URI</span></span>

<span data-ttu-id="8b390-226">O exemplo de código a seguir mostra como gerar um [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) com as permissões de leitura, gravação e exclusão para um contêiner de blobs:</span><span class="sxs-lookup"><span data-stu-id="8b390-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="8b390-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b390-227">Next steps</span></span>

<span data-ttu-id="8b390-228">Neste artigo, você aprendeu a realizar operações em massa no registro de identidade em um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8b390-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="8b390-229">Para saber mais sobre o gerenciamento do Hub IoT do Azure, siga estes links:</span><span class="sxs-lookup"><span data-stu-id="8b390-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="8b390-230">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="8b390-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="8b390-231">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="8b390-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="8b390-232">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="8b390-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8b390-233">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8b390-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8b390-234">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8b390-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
