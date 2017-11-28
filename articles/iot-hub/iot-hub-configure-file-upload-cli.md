---
title: Configurar o upload de arquivo para o Hub IoT usando a CLI do Azure (az.py) | Microsoft Docs
description: Como configurar uploads de arquivo para o Hub IoT do Azure usando a CLI 2.0 do Azure (az.py) de plataforma cruzada.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="defe5-103">Configurar uploads de arquivo do Hub IoT usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="defe5-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="defe5-104">Para usar a [funcionalidade de upload de arquivo no Hub IoT][lnk-upload], primeiro associe uma conta de Armazenamento do Azure ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="defe5-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="defe5-105">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="defe5-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="defe5-106">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="defe5-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="defe5-107">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="defe5-107">An active Azure account.</span></span> <span data-ttu-id="defe5-108">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="defe5-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="defe5-109">[CLI do Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="defe5-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="defe5-110">Um Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="defe5-110">An Azure IoT hub.</span></span> <span data-ttu-id="defe5-111">Se você não tiver um Hub IoT, poderá usar o `az iot hub create` [comando][lnk-cli-create-iothub] para criar um ou usar o portal para [Criar um hub IoT][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="defe5-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="defe5-112">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="defe5-112">An Azure Storage account.</span></span> <span data-ttu-id="defe5-113">Se você não tiver uma conta de Armazenamento do Azure, poderá usar a [CLI do Azure 2.0 – Gerenciar contas de armazenamento][lnk-manage-storage] para criar uma ou usar o portal para [Criar uma conta de armazenamento][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="defe5-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="defe5-114">Entre e configure sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="defe5-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="defe5-115">Entre na sua conta do Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="defe5-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="defe5-116">Ao prompt de comando, execute o [comando de logon][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="defe5-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="defe5-117">Siga as instruções de autenticação usando o código e entre em sua conta do Azure por meio de um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="defe5-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="defe5-118">Se você tiver várias assinaturas do Azure, entrar o Azure lhe dará acesso a todas as contas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="defe5-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="defe5-119">Use o seguinte [comando para listar as contas do Azure][lnk-az-account-command] disponíveis para você:</span><span class="sxs-lookup"><span data-stu-id="defe5-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="defe5-120">Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="defe5-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="defe5-121">Você pode usar a ID ou nome da assinatura da saída do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="defe5-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="defe5-122">Recupere os detalhes da sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="defe5-122">Retrieve your storage account details</span></span>

<span data-ttu-id="defe5-123">As etapas a seguir pressupõem que você criou sua conta de armazenamento usando o modelo de implantação do **Resource Manager** e não o modelo de implantação **Clássico**.</span><span class="sxs-lookup"><span data-stu-id="defe5-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="defe5-124">Para configurar os uploads de arquivos dos seus dispositivos, você precisa da cadeia de conexão de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="defe5-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="defe5-125">A conta de armazenamento deve estar nas mesmas região e assinatura que seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="defe5-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="defe5-126">Você também precisa do nome de um contêiner de blob na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="defe5-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="defe5-127">Use o comando a seguir para recuperar as chaves da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="defe5-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="defe5-128">Anote o valor da **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="defe5-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="defe5-129">Ele é necessário nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="defe5-129">You need it in the following steps.</span></span>

<span data-ttu-id="defe5-130">Você pode usar um contêiner de blob existente para os uploads de arquivo ou criar um novo:</span><span class="sxs-lookup"><span data-stu-id="defe5-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="defe5-131">Para listar os contêineres de blob existentes em sua conta de armazenamento, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="defe5-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="defe5-132">Para criar um contêiner de blob em sua conta de armazenamento, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="defe5-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="defe5-133">Upload de arquivos</span><span class="sxs-lookup"><span data-stu-id="defe5-133">File upload</span></span>

<span data-ttu-id="defe5-134">Agora você pode configurar seu Hub IoT para habilitar a [funcionalidade de upload de arquivos][lnk-upload] usando os detalhes da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="defe5-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="defe5-135">A configuração requer os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="defe5-135">The configuration requires the following values:</span></span>

<span data-ttu-id="defe5-136">**Contêiner de armazenamento**: um contêiner de blob em uma conta de armazenamento do Azure na assinatura atual do Azure para associar ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="defe5-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="defe5-137">Você recuperou as informações da conta de armazenamento necessárias na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="defe5-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="defe5-138">O Hub IoT gera automaticamente os URIs de SAS com permissões de gravação para esse contêiner de blob para dispositivos a serem usados ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="defe5-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="defe5-139">**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo.</span><span class="sxs-lookup"><span data-stu-id="defe5-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="defe5-140">**TTL de SAS**: essa configuração é o tempo de vida dos URIs de SAS retornados para o dispositivo pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="defe5-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="defe5-141">Defina como uma hora por padrão.</span><span class="sxs-lookup"><span data-stu-id="defe5-141">Set to one hour by default.</span></span>

<span data-ttu-id="defe5-142">**TTL de configurações de notificação de arquivo padrão**: o tempo de vida de uma notificação de upload de arquivo antes de sua expiração.</span><span class="sxs-lookup"><span data-stu-id="defe5-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="defe5-143">Defina como um dia por padrão.</span><span class="sxs-lookup"><span data-stu-id="defe5-143">Set to one day by default.</span></span>

<span data-ttu-id="defe5-144">**Contagem de entrega máxima de notificação de arquivo**: o número de vezes que o Hub IoT tenta entregar uma notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="defe5-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="defe5-145">Defina como 10 por padrão.</span><span class="sxs-lookup"><span data-stu-id="defe5-145">Set to 10 by default.</span></span>

<span data-ttu-id="defe5-146">Use os seguintes comandos da CLI do Azure para definir as configurações de upload de arquivo no seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="defe5-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="defe5-147">Em um shell de busca, use:</span><span class="sxs-lookup"><span data-stu-id="defe5-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="defe5-148">Em um prompt de comando do Windows, use:</span><span class="sxs-lookup"><span data-stu-id="defe5-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="defe5-149">Você pode examinar a configuração de upload de arquivo em seu hub IoT usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="defe5-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="defe5-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="defe5-150">Next steps</span></span>

<span data-ttu-id="defe5-151">Para saber mais sobre os recursos de upload de arquivo do Hub IoT, consulte [Carregar arquivos de um dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="defe5-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="defe5-152">Para saber mais sobre o gerenciamento do Hub IoT do Azure, siga estes links:</span><span class="sxs-lookup"><span data-stu-id="defe5-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="defe5-153">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="defe5-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="defe5-154">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="defe5-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="defe5-155">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="defe5-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="defe5-156">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="defe5-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="defe5-157">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="defe5-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="defe5-158">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="defe5-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="defe5-159">[Proteger sua solução de IoT desde o início][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="defe5-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create