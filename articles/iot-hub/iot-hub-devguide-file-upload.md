---
title: Entender o upload de arquivo do Hub IoT do Azure | Microsoft Docs
description: "Guia do desenvolvedor ‑ usar o recurso de upload de arquivo do Hub IoT para gerenciar o carregamento de arquivos de um dispositivo para um contêiner de Azure Storage Blob."
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
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="ff43b-103">Carregar arquivos com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="ff43b-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="ff43b-104">Como detalhado no artigo [Pontos de extremidade do Hub IoT][lnk-endpoints], um dispositivo pode iniciar um upload de arquivo enviando uma notificação por meio de um ponto de extremidade voltado para o dispositivo (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="ff43b-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="ff43b-105">Quando um dispositivo notifica o Hub IoT de um upload concluído, o Hub IoT envia uma mensagem de notificação de upload de arquivo por meio do ponto de extremidade voltado para o serviço **/messages/servicebound/filenotifications**.</span><span class="sxs-lookup"><span data-stu-id="ff43b-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="ff43b-106">Em vez da corretagem mensagens por meio do próprio Hub IoT, o Hub IoT age como um dispatcher para uma conta do Armazenamento do Azure associada.</span><span class="sxs-lookup"><span data-stu-id="ff43b-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="ff43b-107">Um dispositivo solicita um token de armazenamento do Hub IoT específico para o arquivo que o dispositivo deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="ff43b-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="ff43b-108">O dispositivo usa o URI de SAS para carregar o arquivo de armazenamento e, quando o upload for concluído, o dispositivo enviará uma notificação de conclusão para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="ff43b-109">O Hub IoT verifica se o upload do arquivo está concluído e então adiciona uma mensagem de notificação de upload de arquivo ao ponto de extremidade de notificação de arquivo voltado para o serviço.</span><span class="sxs-lookup"><span data-stu-id="ff43b-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="ff43b-110">Antes de carregar um arquivo no Hub IoT de um dispositivo, você deve configurar seu hub [associando uma conta do Armazenamento do Azure][lnk-associate-storage] a ele.</span><span class="sxs-lookup"><span data-stu-id="ff43b-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="ff43b-111">Em seguida, seu dispositivo pode [inicializar um carregamento][lnk-initialize] e [notificar o Hub IoT][lnk-notify] após a conclusão do carregamento.</span><span class="sxs-lookup"><span data-stu-id="ff43b-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="ff43b-112">Opcionalmente, quando um dispositivo notifica o Hub IoT de que o carregamento foi concluído, o serviço pode gerar uma [mensagem de notificação][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="ff43b-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="ff43b-113">Quando usar</span><span class="sxs-lookup"><span data-stu-id="ff43b-113">When to use</span></span>

<span data-ttu-id="ff43b-114">Use o carregamento de arquivos para enviar arquivos de mídia e lotes grandes de telemetria carregados por dispositivos conectados de forma intermitente ou compactados para economizar largura de banda.</span><span class="sxs-lookup"><span data-stu-id="ff43b-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="ff43b-115">Veja as[diretrizes de comunicação do dispositivo para a nuvem][lnk-d2c-guidance] se está em dúvida entre o uso de propriedades reportadas, mensagens do dispositivo para a nuvem ou carregamento do arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="ff43b-116">Associar uma conta do Armazenamento do Azure com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="ff43b-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="ff43b-117">Para usar a funcionalidade de upload de arquivos, primeiro você deve vincular uma conta do Armazenamento do Azure para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="ff43b-118">Você pode concluir essa tarefa por meio do [Portal do Azure][lnk-management-portal] ou programaticamente por meio das [APIs REST do provedor de recursos do Hub IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="ff43b-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="ff43b-119">Depois de associar a uma conta do Armazenamento do Azure ao Hub IoT, o serviço retorna um URI de SAS para um dispositivo quando o dispositivo inicia uma solicitação de upload de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="ff43b-120">Os [SDKs do Azure IoT][lnk-sdks] tratam automaticamente da recuperação do URI de SAS, do upload do arquivo e da notificação do Hub IoT de um upload concluído.</span><span class="sxs-lookup"><span data-stu-id="ff43b-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="ff43b-121">Inicializar um upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="ff43b-121">Initialize a file upload</span></span>
<span data-ttu-id="ff43b-122">O Hub IoT tem um ponto de extremidade especificamente para os dispositivos solicitarem um URI SAS para armazenamento a fim de carregar um arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="ff43b-123">Para iniciar o processo de upload de arquivo, o dispositivo envia uma solicitação POST para `{iot hub}.azure-devices.net/devices/{deviceId}/files` com o seguinte corpo JSON:</span><span class="sxs-lookup"><span data-stu-id="ff43b-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="ff43b-124">O Hub IoT retorna os seguintes dados, que são usados pelo dispositivo para carregar o arquivo:</span><span class="sxs-lookup"><span data-stu-id="ff43b-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="ff43b-125">Preterido: inicializar um carregamento de arquivo com um GET</span><span class="sxs-lookup"><span data-stu-id="ff43b-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="ff43b-126">Esta seção descreve a funcionalidade preterida de como receber um URI SAS do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="ff43b-127">Use o método POST descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ff43b-127">Use the POST method described previously.</span></span>

<span data-ttu-id="ff43b-128">O Hub IoT tem dois pontos de extremidade REST para dar suporte ao upload de arquivo, um para obter o URI de SAS para armazenamento e o outro para notificar o hub IoT de um upload concluído.</span><span class="sxs-lookup"><span data-stu-id="ff43b-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="ff43b-129">O dispositivo inicia o processo de upload de arquivo, enviando um GET para o hub IoT em `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="ff43b-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="ff43b-130">O Hub IoT retorna:</span><span class="sxs-lookup"><span data-stu-id="ff43b-130">The IoT hub returns:</span></span>

* <span data-ttu-id="ff43b-131">Um URI de SAS específico para o arquivo a ser carregado.</span><span class="sxs-lookup"><span data-stu-id="ff43b-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="ff43b-132">Uma ID de correlação a ser usada quando o upload for concluído.</span><span class="sxs-lookup"><span data-stu-id="ff43b-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="ff43b-133">Notificar o Hub IoT de um upload de arquivo concluído</span><span class="sxs-lookup"><span data-stu-id="ff43b-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="ff43b-134">O dispositivo é responsável por carregar o arquivo para o armazenamento usando os SDKs do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff43b-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="ff43b-135">Após a conclusão do upload, o dispositivo envia uma solicitação POST para `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` com o seguinte corpo JSON:</span><span class="sxs-lookup"><span data-stu-id="ff43b-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="ff43b-136">O valor de `isSuccess` é um booliano que representa se o arquivo foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ff43b-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="ff43b-137">O código de status para `statusCode` é o status do carregamento do arquivo no armazenamento, e o `statusDescription` corresponde ao `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="ff43b-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="ff43b-138">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="ff43b-138">Reference topics:</span></span>

<span data-ttu-id="ff43b-139">Os tópicos de referência a seguir fornecem a você mais informações sobre como carregar os arquivos de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="ff43b-140">Notificações de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="ff43b-140">File upload notifications</span></span>

<span data-ttu-id="ff43b-141">Opcionalmente, quando um dispositivo notifica o Hub IoT da conclusão de um upload, o Hub IoT pode gerar uma mensagem de notificação com o local de armazenamento e o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="ff43b-142">Como explicado em [Pontos de extremidade][lnk-endpoints], o Hub IoT fornece notificações de upload de arquivos por meio de um ponto de extremidade voltado para o serviço (**/messages/servicebound/fileuploadnotifications**) como mensagens.</span><span class="sxs-lookup"><span data-stu-id="ff43b-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="ff43b-143">A semântica de recebimento das notificações de upload de arquivos é a mesma das mensagens da nuvem para o dispositivo e tem o mesmo [ciclo de vida da mensagem][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="ff43b-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="ff43b-144">Cada mensagem recuperada do ponto de extremidade de notificação de upload de arquivos é um registro JSON com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ff43b-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="ff43b-145">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ff43b-145">Property</span></span> | <span data-ttu-id="ff43b-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="ff43b-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff43b-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ff43b-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="ff43b-148">Carimbo de data/hora que indica quando a notificação foi criada.</span><span class="sxs-lookup"><span data-stu-id="ff43b-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="ff43b-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="ff43b-149">DeviceId</span></span> |<span data-ttu-id="ff43b-150">**DeviceId** do dispositivo que carregou o arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="ff43b-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="ff43b-151">BlobUri</span></span> |<span data-ttu-id="ff43b-152">URI do arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="ff43b-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="ff43b-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="ff43b-153">BlobName</span></span> |<span data-ttu-id="ff43b-154">Nome do arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="ff43b-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="ff43b-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="ff43b-155">LastUpdatedTime</span></span> |<span data-ttu-id="ff43b-156">Carimbo de data/hora que indica quando o arquivo foi atualizado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="ff43b-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="ff43b-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="ff43b-157">BlobSizeInBytes</span></span> |<span data-ttu-id="ff43b-158">Tamanho do arquivo carregado.</span><span class="sxs-lookup"><span data-stu-id="ff43b-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="ff43b-159">**Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="ff43b-159">**Example**.</span></span> <span data-ttu-id="ff43b-160">Este exemplo mostra o corpo de uma mensagem de notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-160">This example shows the body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="ff43b-161">Opções de configuração de notificação de upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="ff43b-161">File upload notification configuration options</span></span>

<span data-ttu-id="ff43b-162">Cada hub IoT expõe as seguintes opções de configuração para notificações de upload de arquivos:</span><span class="sxs-lookup"><span data-stu-id="ff43b-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="ff43b-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ff43b-163">Property</span></span> | <span data-ttu-id="ff43b-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="ff43b-164">Description</span></span> | <span data-ttu-id="ff43b-165">Intervalo e padrão</span><span class="sxs-lookup"><span data-stu-id="ff43b-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff43b-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="ff43b-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="ff43b-167">Controla se as notificações de upload de arquivos serão gravadas no ponto de extremidade de notificações de arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff43b-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="ff43b-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="ff43b-168">Bool.</span></span> <span data-ttu-id="ff43b-169">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="ff43b-169">Default: True.</span></span> |
| <span data-ttu-id="ff43b-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="ff43b-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="ff43b-171">TTL padrão para notificações de upload de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="ff43b-172">Intervalo ISO_8601 de até 48H (mínimo de um minuto).</span><span class="sxs-lookup"><span data-stu-id="ff43b-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="ff43b-173">Padrão: 1 hora.</span><span class="sxs-lookup"><span data-stu-id="ff43b-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="ff43b-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="ff43b-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="ff43b-175">Duração de bloqueio para a fila de notificações de upload de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="ff43b-176">5 a 300 segundos (mínimo de cinco segundos).</span><span class="sxs-lookup"><span data-stu-id="ff43b-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="ff43b-177">Padrão: 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="ff43b-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="ff43b-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="ff43b-179">Contagem máxima de entregas para a fila de notificação de upload de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="ff43b-180">1 a 100.</span><span class="sxs-lookup"><span data-stu-id="ff43b-180">1 to 100.</span></span> <span data-ttu-id="ff43b-181">Padrão: 100.</span><span class="sxs-lookup"><span data-stu-id="ff43b-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="ff43b-182">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="ff43b-182">Additional reference material</span></span>

<span data-ttu-id="ff43b-183">Outros tópicos de referência no Guia do desenvolvedor do Hub IoT incluem:</span><span class="sxs-lookup"><span data-stu-id="ff43b-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="ff43b-184">[Pontos de extremidade do Hub IoT][lnk-endpoints] descreve os vários pontos de extremidade que cada Hub IoT expõe para operações de tempo de execução e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ff43b-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="ff43b-185">[Limitação e cotas][lnk-quotas] descreve as cotas e os comportamentos de limitação que se aplicam ao serviço Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="ff43b-186">[SDKs de dispositivo e serviço IoT do Azure][lnk-sdks] lista os vários SDKs de linguagem que você pode usar no desenvolvimento de aplicativos de dispositivo e de serviço que interagem com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="ff43b-187">A [linguagem de consulta do Hub IoT][lnk-query] descreve a linguagem de consulta que você pode usar para recuperar informações do Hub IoT sobre dispositivos gêmeos e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ff43b-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="ff43b-188">[Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt] fornece mais informações sobre o suporte do Hub IoT para o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="ff43b-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff43b-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff43b-189">Next steps</span></span>

<span data-ttu-id="ff43b-190">Agora que você aprendeu a carregar arquivos de dispositivos usando o Hub IoT, talvez se interesse pelos tópicos a seguir do Guia do desenvolvedor do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="ff43b-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="ff43b-191">[Gerenciar identidades do dispositivo no Hub IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="ff43b-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="ff43b-192">[Controlar o acesso ao Hub IoT][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="ff43b-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="ff43b-193">[Usar dispositivos gêmeos para sincronizar o estado e as configurações][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="ff43b-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="ff43b-194">[Invocar um método direto em um dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="ff43b-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="ff43b-195">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ff43b-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ff43b-196">Se você quiser experimentar alguns dos conceitos descritos neste artigo, talvez se interesse pelo seguinte tutorial de Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="ff43b-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="ff43b-197">[Como carregar arquivos de dispositivos para a nuvem com o Hub IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="ff43b-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
