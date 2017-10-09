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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Gerenciar identidades de dispositivo do Hub IoT em massa

Cada hub IoT tem um registro de identidade que você pode usar recursos de cada dispositivo toocreate no serviço de saudação. registro de identidade Olá também permite que você toocontrol pontos de extremidade de acesso toohello voltadas para o dispositivo. Este artigo descreve como identidades de dispositivo de tooimport e exportação em massa tooand de um registro de identidade.

Operações de importação e exportação ocorrem no contexto de saudação do *trabalhos* que permitem operações de serviço tooexecute em massa em relação a um hub IoT.

Olá **RegistryManager** classe inclui Olá **ExportDevicesAsync** e **ImportDevicesAsync** métodos que usam Olá **trabalho** estrutura. Esses métodos permitem que você tooexport, importar e sincronizar a totalidade de saudação de um registro de identidade de hub IoT.

## <a name="what-are-jobs"></a>O que são trabalhos?

Operações de registro de identidade usam Olá **trabalho** sistema hello quando a operação:

* Tem um tempo de execução potencialmente longo comparados toostandard operações de tempo de execução.
* Retorna uma grande quantidade de usuário de toohello de dados.

Em vez de uma única chamada de API aguardando ou bloqueio no resultado de saudação da operação hello, operação Olá cria de maneira assíncrona um **trabalho** do hub IoT. operação de saudação e imediatamente retorna um **JobProperties** objeto.

Olá seguir c# code trecho de código mostra como toocreate um trabalho de exportação:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> Olá toouse **RegistryManager** classe em seu código c#, adicione Olá **Microsoft.Azure.Devices** tooyour de pacote NuGet projeto. Olá **RegistryManager** classe está no hello **Microsoft.Azure.Devices** namespace.

Você pode usar o hello **RegistryManager** classe tooquery estado de saudação do hello **trabalho** usando Olá retornado **JobProperties** metadados.

Olá seguinte trecho de código c# mostra como toopoll toosee cada cinco segundos se hello trabalho concluiu a execução:

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

## <a name="export-devices"></a>Exportar dispositivos

Saudação de uso **ExportDevicesAsync** método tooexport Olá toda uma tooan de registro de identidade de hub IoT [armazenamento do Azure](../storage/index.md) contêiner de blob usando um [assinatura de acesso compartilhado](../storage/common/storage-security-guide.md#data-plane-security).

Esse método permite backups de toocreate confiáveis de suas informações de dispositivo em um contêiner de blob que você controle.

Olá **ExportDevicesAsync** método requer dois parâmetros:

* Uma *cadeia de caracteres* que contenha um URI de um contêiner de blobs. Esse URI deve conter um token SAS que concede acesso de gravação toohello contêiner. trabalho de saudação cria um blob de bloco nos dados de dispositivo de exportação contêiner toostore Olá serializado. token SAS Olá deve incluir estas permissões:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* Um *booliano* que indica se você deseja que as chaves de autenticação tooexclude de seus dados de exportação. Se for **false**, as chaves de autenticação serão incluídas na saída de exportação. Caso contrário, as chaves serão exportadas como **null**.

Olá seguinte trecho de código c# mostra como tooinitiate um trabalho de exportação que inclui as chaves de autenticação de dispositivo em Olá exportar dados e então sondam conclusão:

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

Olá trabalho armazena sua saída no contêiner de blob Olá fornecido como um blob de bloco com nome hello **Devices**. dados de saída de saudação consistem em dados de dispositivo JSON serializado, com um dispositivo por linha.

Olá, exemplo a seguir mostra os dados de saída de hello:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Se um dispositivo tiver dados de duas, dados de duas Olá também são exportados junto com os dados do dispositivo hello. Olá, exemplo a seguir mostra esse formato. Todos os dados da linha de "twinETag" hello até o término de saudação são dados de duas.

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

Se você precisar acessar dados toothis no código, você pode facilmente desserializar dados usando Olá **ExportImportDevice** classe. Olá seguinte trecho de código c# mostra como informações do dispositivo tooread que foi exportado anteriormente tooa blob de blocos:

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
> Você também pode usar o hello **GetDevicesAsync** método hello **RegistryManager** classe toofetch uma lista de seus dispositivos. No entanto, essa abordagem tem um limite rígido de 1000 no número de saudação de objetos de dispositivo que são retornados. Olá esperado caso de uso para Olá **GetDevicesAsync** método é para depuração de tooaid de cenários de desenvolvimento e não é recomendado para cargas de trabalho de produção.

## <a name="import-devices"></a>Importar dispositivos

Olá **ImportDevicesAsync** método hello **RegistryManager** classe permite que operações de importação e sincronização de em massa de tooperform em um registro de identidade de hub IoT. Como Olá **ExportDevicesAsync** método, Olá **ImportDevicesAsync** usa o método hello **trabalho** framework.

Tome cuidado usar Olá **ImportDevicesAsync** método porque na adição tooprovisioning novos dispositivos em seu registro de identidade, ele também pode atualizar e excluir dispositivos existentes.

> [!WARNING]
> Uma operação de importação não pode ser desfeita. Sempre faça backup dos dados existentes usando Olá **ExportDevicesAsync** tooyour registro de identidade de alterações do contêiner de blob do método tooanother antes de fazer em massa.

Olá **ImportDevicesAsync** método aceita dois parâmetros:

* Um *cadeia de caracteres* que contém um URI de um [armazenamento do Azure](../storage/index.md) blob toouse contêiner como *entrada* toohello trabalho. Esse URI deve conter um token SAS que concede acesso de leitura toohello contêiner. Este contêiner deve conter um blob com nome hello **Devices** que contém Olá serializado tooimport de dados de dispositivo para o registro de identidade. Olá importação de dados deve conter informações do dispositivo no hello JSON mesmo formato que Olá **ExportImportDevice** trabalho usa quando ele cria uma **Devices** blob. token SAS Olá deve incluir estas permissões:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* Um *cadeia de caracteres* que contém um URI de um [armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contêiner como *saída* de trabalho de saudação. Olá trabalho cria um blob de bloco no toostore contêiner qualquer informação de erro de importação de saudação concluída **trabalho**. token SAS Olá deve incluir estas permissões:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> parâmetros de saudação dois podem apontar toohello mesmo contêiner de blob. parâmetros separados Olá simplesmente permitem mais controle sobre os dados como o contêiner de saída Olá requer permissões adicionais.

Olá seguir c# code trecho de código mostra como tooinitiate um trabalho de importação:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Esse método também pode ser usado tooimport Olá dados para duas de dispositivo de saudação. formato Olá Olá entrada de dados é Olá mesmo como formato Olá mostrado Olá **ExportDevicesAsync** seção. Dessa forma, você pode reimportar dados hello exportada. Olá **$metadata** é opcional.

## <a name="import-behavior"></a>Comportamento de importação

Você pode usar o hello **ImportDevicesAsync** seguinte de saudação do método tooperform em massa operações em seu registro de identidade:

* Registro em massa de novos dispositivos
* Exclusões em massa dos dispositivos existentes
* Alterações de status em massa (habilitar ou desabilitar dispositivos)
* Atribuição em massa de novas chaves de autenticação de dispositivo
* Nova geração automática em massa de chaves de autenticação de dispositivo
* Atualização em massa de dados gêmeos

Você pode executar qualquer combinação de saudação anterior de operações em um único **ImportDevicesAsync** chamar. Por exemplo, você pode registrar novos dispositivos e excluir ou atualizar os dispositivos existentes no hello simultaneamente. Quando usada com hello **ExportDevicesAsync** método, você pode migrar completamente todos os dispositivos de um tooanother de hub IoT.

Se o arquivo de importação de saudação inclui duas metadados, metadados substitui os metadados existentes duas hello. Se o arquivo de importação de saudação não inclui duas metadados, em seguida, somente Olá `lastUpdateTime` metadados são atualizados usando Olá hora atual.

Saudação de uso opcional **importMode** propriedade nos dados de serialização de importação Olá para cada dispositivo toocontrol Olá importação processo por dispositivo. Olá **importMode** propriedade tem Olá as opções a seguir:

| importMode | Descrição |
| --- | --- |
| **createOrUpdate** |Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente. <br/>Se já existe um dispositivo Olá, informações existentes serão substituídas pelo Olá fornecido dados de entrada sem levar em consideração toohello **ETag** valor. <br> usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello. etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello. Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log. |
| **create** |Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente. <br/>Se o dispositivo de saudação já existir, um erro será gravado toohello arquivo de log. <br> usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello. etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello. Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log. |
| **atualizar** |Se já existe um dispositivo com hello especificado **id**, as informações existentes sejam substituídas com hello fornecido dados de entrada sem levar em consideração toohello **ETag** valor. <br/>Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log. |
| **updateIfMatchETag** |Se já existe um dispositivo com hello especificado **id**, as informações existentes sejam substituídas com hello fornecido dados de entrada somente se houver um **ETag** corresponder. <br/>Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log. <br/>Se houver um **ETag** incompatibilidade, um erro será gravado toohello arquivo de log. |
| **createOrUpdateIfMatchETag** |Se não existir um dispositivo com hello especificado **id**, ele é registrado recentemente. <br/>Se já existe um dispositivo Olá, informações existentes serão substituídas pelo Olá fornecido dados de entrada somente se houver um **ETag** corresponder. <br/>Se houver um **ETag** incompatibilidade, um erro será gravado toohello arquivo de log. <br> usuário Hello, opcionalmente, pode especificar dados de duas junto com os dados do dispositivo hello. etag do duas Olá, se especificado, será processada independentemente de etag do dispositivo hello. Se houver uma incompatibilidade de etag do duas Olá existente, um erro será gravado toohello arquivo de log. |
| **delete** |Se já existe um dispositivo com hello especificado **id**, ele será excluído sem considerar toohello **ETag** valor. <br/>Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log. |
| **deleteIfMatchETag** |Se já existe um dispositivo com hello especificado **id**, ele é excluído somente se houver um **ETag** corresponder. Se o dispositivo de saudação não existir, um erro será gravado toohello arquivo de log. <br/>Se houver uma incompatibilidade de ETag, um erro será gravado toohello arquivo de log. |

> [!NOTE]
> Se os dados de serialização Olá não definir explicitamente um **importMode** sinalizador para um dispositivo, o padrão é muito**createOrUpdate** Olá durante a operação de importação.

## <a name="import-devices-example--bulk-device-provisioning"></a>Exemplo de importação de dispositivos – provisionamento de dispositivo em massa

Olá c# código exemplo a seguir ilustra como toogenerate várias identidades de dispositivo que:

* Inclua as chaves de autenticação.
* Esse blob de blocos de tooa de informações de dispositivo de gravação.
* Importe dispositivos Olá para registro de identidade de saudação.

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

## <a name="import-devices-example--bulk-deletion"></a>Exemplo de importação de dispositivos – exclusão em massa

Olá exemplo de código a seguir mostra como os dispositivos de saudação toodelete adicionados usando Olá exemplo de código anterior:

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

## <a name="get-hello-container-sas-uri"></a>Obter URI SAS do contêiner Olá

Olá exemplo de código a seguir mostra como toogenerate uma [URI SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) com leitura, gravação e exclusão de permissões para um contêiner de blob:

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

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu como tooperform em massa operações no registro de identidade Olá em um hub IoT. Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:

* [Métricas do Hub IoT][lnk-metrics]
* [Monitoramento de operações][lnk-monitor]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com IoT Edge][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
