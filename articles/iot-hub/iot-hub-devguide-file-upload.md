---
title: carregamento do arquivo Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - recurso de carregamento de arquivo use saudação do IoT Hub toomanage upload de arquivos de um contêiner de blob de armazenamento do Azure do dispositivo tooan."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="2b095-103">Carregar arquivos com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="2b095-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="2b095-104">Conforme detalhado no hello [pontos de extremidade de IoT Hub] [ lnk-endpoints] artigo, um dispositivo pode iniciar um upload de arquivo enviando uma notificação por meio de um ponto de extremidade voltados para o dispositivo (**/devices/ {deviceId} / arquivos**).</span><span class="sxs-lookup"><span data-stu-id="2b095-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="2b095-105">Quando um dispositivo notifica o IoT Hub que um carregamento for concluído, o IoT Hub envia uma mensagem de notificação de carregamento de arquivo por meio de saudação **/messages/servicebound/filenotifications** voltadas para o serviço de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="2b095-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="2b095-106">Em vez de controle de mensagens por meio de IoT Hub em si, o IoT Hub em vez disso, atua como um dispatcher tooan associados a conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b095-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="2b095-107">Um dispositivo solicita um token de armazenamento do IoT Hub que é específico toohello arquivo hello dispositivo deseja tooupload.</span><span class="sxs-lookup"><span data-stu-id="2b095-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="2b095-108">dispositivo Olá usa Olá URI SAS tooupload Olá arquivo toostorage e quando Olá carregamento for concluído dispositivo Olá envia uma notificação de conclusão tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b095-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="2b095-109">IoT Hub verifica o carregamento do arquivo hello foi concluído e, em seguida, adiciona um arquivo carregamento notificação mensagem toohello voltadas para o serviço arquivo notificação ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="2b095-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="2b095-110">Antes de carregar um arquivo tooIoT Hub de um dispositivo, você deve configurar seu hub por [associando um armazenamento do Azure] [ lnk-associate-storage] tooit de conta.</span><span class="sxs-lookup"><span data-stu-id="2b095-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="2b095-111">Seu dispositivo pode então [inicializar um carregamento] [ lnk-initialize] e, em seguida, [notificar o hub IoT] [ lnk-notify] quando o carregamento de saudação for concluído.</span><span class="sxs-lookup"><span data-stu-id="2b095-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="2b095-112">Opcionalmente, quando um dispositivo notifica o IoT Hub que Olá carregamento for concluído, o serviço de saudação pode gerar um [mensagem de notificação][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="2b095-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="2b095-113">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="2b095-113">When toouse</span></span>

<span data-ttu-id="2b095-114">Usar arquivos de mídia de toosend de carregamento de arquivo e lotes grandes telemetria carregados por dispositivos conectados de maneira intermitente ou a largura de banda de toosave compactado.</span><span class="sxs-lookup"><span data-stu-id="2b095-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="2b095-115">Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] se em dúvida entre usando as propriedades relatadas, mensagens de dispositivo para nuvem ou carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b095-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="2b095-116">Associar uma conta do Armazenamento do Azure com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="2b095-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="2b095-117">funcionalidade de carregamento de arquivo de saudação toouse, primeiro você deve vincular uma conta de armazenamento do Azure toohello IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b095-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="2b095-118">Você pode concluir esta tarefa por meio de saudação [portal do Azure][lnk-management-portal], ou programaticamente por meio de saudação [APIs REST de provedor de recursos do IoT Hub] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="2b095-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="2b095-119">Depois que você tiver associado uma conta de armazenamento do Azure com o IoT Hub, Olá serviço retorna um URI de SAS tooa dispositivo quando o dispositivo de saudação inicia uma solicitação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b095-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="2b095-120">Olá [SDKs do Azure IoT] [ lnk-sdks] automaticamente identificador recuperando Olá URI SAS, carregando o arquivo hello e notificar o IoT Hub de um carregamento concluído.</span><span class="sxs-lookup"><span data-stu-id="2b095-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="2b095-121">Inicializar um upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="2b095-121">Initialize a file upload</span></span>
<span data-ttu-id="2b095-122">IoT Hub tem um ponto de extremidade especificamente para dispositivos toorequest um URI de SAS para um arquivo de tooupload de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2b095-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="2b095-123">processo de carregamento de arquivo de saudação tooinitiate, Olá dispositivo envia uma solicitação POST muito`{iot hub}.azure-devices.net/devices/{deviceId}/files` com hello corpo JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="2b095-124">IoT Hub retorna Olá dados, qual dispositivo Olá usa o arquivo de saudação do tooupload a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="2b095-125">Preterido: inicializar um carregamento de arquivo com um GET</span><span class="sxs-lookup"><span data-stu-id="2b095-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="2b095-126">Esta seção descreve a funcionalidade preterida como tooreceive um URI de SAS do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2b095-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="2b095-127">Use o método de POSTAGEM de saudação descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b095-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="2b095-128">IoT Hub tem dois arquivos de toosupport de pontos de extremidade REST carregar um hello tooget URI SAS para armazenamento e Olá outros hub de IoT Olá toonotify de um carregamento concluído.</span><span class="sxs-lookup"><span data-stu-id="2b095-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="2b095-129">Olá dispositivo inicia o processo de upload de arquivo hello enviando um hub de IoT GET toohello em `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="2b095-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="2b095-130">hub IoT de saudação retorna:</span><span class="sxs-lookup"><span data-stu-id="2b095-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="2b095-131">Um URI de SAS específico toohello toobe de arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="2b095-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="2b095-132">Uma ID de correlação toobe usado após a conclusão do carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b095-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="2b095-133">Notificar o Hub IoT de um upload de arquivo concluído</span><span class="sxs-lookup"><span data-stu-id="2b095-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="2b095-134">dispositivo de saudação é responsável por carregar Olá arquivo toostorage usando Olá SDKs de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b095-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="2b095-135">Quando a saudação carregamento for concluído, o dispositivo de saudação também envia uma solicitação POST`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` com hello corpo JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="2b095-136">Olá valor `isSuccess` é um booleano que representa se o arquivo hello foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="2b095-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="2b095-137">Olá código de status `statusCode` é Olá status de carregamento de saudação do hello arquivo toostorage e Olá `statusDescription` corresponde toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="2b095-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="2b095-138">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="2b095-138">Reference topics:</span></span>

<span data-ttu-id="2b095-139">Olá seguintes tópicos de referência fornecem mais informações sobre como carregar arquivos de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b095-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="2b095-140">Notificações de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="2b095-140">File upload notifications</span></span>

<span data-ttu-id="2b095-141">Opcionalmente, quando um dispositivo de IoT Hub o notifica que um carregamento for concluído, o IoT Hub pode gerar uma mensagem de notificação que contém o nome e o armazenamento local do arquivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="2b095-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="2b095-142">Como explicado em [Pontos de extremidade][lnk-endpoints], o Hub IoT fornece notificações de upload de arquivos por meio de um ponto de extremidade voltado para o serviço (**/messages/servicebound/fileuploadnotifications**) como mensagens.</span><span class="sxs-lookup"><span data-stu-id="2b095-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="2b095-143">Olá semântica de recebimento para notificações de carregamento de arquivo são Olá mesmo para mensagens de nuvem para dispositivos e ter Olá mesmo [ciclo de vida da mensagem][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="2b095-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="2b095-144">Cada mensagem recuperada do ponto de extremidade de notificação de carregamento de arquivo hello é um registro JSON com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="2b095-145">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b095-145">Property</span></span> | <span data-ttu-id="2b095-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b095-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b095-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="2b095-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="2b095-148">O carimbo de hora que indica quando Olá notificação foi criada.</span><span class="sxs-lookup"><span data-stu-id="2b095-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="2b095-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="2b095-149">DeviceId</span></span> |<span data-ttu-id="2b095-150">**DeviceId** do dispositivo Olá que carregou o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2b095-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="2b095-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="2b095-151">BlobUri</span></span> |<span data-ttu-id="2b095-152">URI do arquivo hello carregado.</span><span class="sxs-lookup"><span data-stu-id="2b095-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="2b095-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="2b095-153">BlobName</span></span> |<span data-ttu-id="2b095-154">Nome da saudação arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="2b095-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="2b095-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="2b095-155">LastUpdatedTime</span></span> |<span data-ttu-id="2b095-156">O carimbo de hora que indica quando o arquivo hello foi atualizado pela última.</span><span class="sxs-lookup"><span data-stu-id="2b095-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="2b095-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="2b095-157">BlobSizeInBytes</span></span> |<span data-ttu-id="2b095-158">Tamanho da saudação arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="2b095-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="2b095-159">**Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="2b095-159">**Example**.</span></span> <span data-ttu-id="2b095-160">Este exemplo mostra o corpo de saudação de um arquivo de carregar a mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="2b095-160">This example shows hello body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="2b095-161">Opções de configuração de notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="2b095-161">File upload notification configuration options</span></span>

<span data-ttu-id="2b095-162">Cada hub IoT expõe Olá as opções de configuração para notificações de carregamento de arquivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="2b095-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b095-163">Property</span></span> | <span data-ttu-id="2b095-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b095-164">Description</span></span> | <span data-ttu-id="2b095-165">Intervalo e padrão</span><span class="sxs-lookup"><span data-stu-id="2b095-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b095-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="2b095-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="2b095-167">Controla se as notificações de carregamento de arquivo são gravadas toohello ponto de extremidade de notificações de arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b095-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="2b095-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="2b095-168">Bool.</span></span> <span data-ttu-id="2b095-169">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="2b095-169">Default: True.</span></span> |
| <span data-ttu-id="2b095-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="2b095-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="2b095-171">TTL padrão para notificações de upload de arquivos.</span><span class="sxs-lookup"><span data-stu-id="2b095-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="2b095-172">Intervalo de ISO_8601 a too48H (mínimo 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="2b095-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="2b095-173">Padrão: 1 hora.</span><span class="sxs-lookup"><span data-stu-id="2b095-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="2b095-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="2b095-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="2b095-175">Duração de bloqueio para a fila de notificações de carregamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2b095-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="2b095-176">5 too300 segundos (mínimo 5 segundos).</span><span class="sxs-lookup"><span data-stu-id="2b095-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="2b095-177">Padrão: 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="2b095-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="2b095-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="2b095-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="2b095-179">Contagem máxima de entrega para o arquivo hello carregar fila de notificação.</span><span class="sxs-lookup"><span data-stu-id="2b095-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="2b095-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="2b095-180">1 too100.</span></span> <span data-ttu-id="2b095-181">Padrão: 100.</span><span class="sxs-lookup"><span data-stu-id="2b095-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="2b095-182">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="2b095-182">Additional reference material</span></span>

<span data-ttu-id="2b095-183">Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="2b095-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="2b095-184">[Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2b095-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="2b095-185">[Limitação e cotas] [ lnk-quotas] descreve cotas hello e comportamentos que se aplicam a toohello serviço de IoT Hub de limitação.</span><span class="sxs-lookup"><span data-stu-id="2b095-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="2b095-186">[SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="2b095-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="2b095-187">[Linguagem de consulta de IoT Hub] [ lnk-query] descreve a linguagem de consulta de saudação, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b095-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="2b095-188">[Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="2b095-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b095-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b095-189">Next steps</span></span>

<span data-ttu-id="2b095-190">Agora que você aprendeu como tooupload arquivos de dispositivos usando o IoT Hub, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b095-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="2b095-191">[Gerenciar identidades do dispositivo no Hub IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="2b095-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="2b095-192">[Controlar acesso tooIoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="2b095-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="2b095-193">[Usar configurações e estado do dispositivo twins toosynchronize][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="2b095-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="2b095-194">[Invocar um método direto em um dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="2b095-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="2b095-195">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="2b095-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2b095-196">Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="2b095-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="2b095-197">[Como arquivos de tooupload de toohello de dispositivos de nuvem com o IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="2b095-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
