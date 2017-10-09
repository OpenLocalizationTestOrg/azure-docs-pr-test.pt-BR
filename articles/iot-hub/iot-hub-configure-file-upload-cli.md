---
title: tooIoT de carregamento de arquivo aaaConfigure Hub usando a CLI do Azure (az.py) | Microsoft Docs
description: "Como tooconfigure fileuploads tooAzure Hub IoT usando Olá plataforma cruzada do Azure CLI 2.0 (az.py)."
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="6ccad-103">Configurar uploads de arquivo do Hub IoT usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6ccad-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="6ccad-104">Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6ccad-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="6ccad-105">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="6ccad-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="6ccad-106">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6ccad-107">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ccad-107">An active Azure account.</span></span> <span data-ttu-id="6ccad-108">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6ccad-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6ccad-109">[CLI do Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="6ccad-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="6ccad-110">Um Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ccad-110">An Azure IoT hub.</span></span> <span data-ttu-id="6ccad-111">Se você não tiver um hub IoT, você pode usar o hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate um ou use Olá portal muito [criar um hub IoT] [hub de portal lnk].</span><span class="sxs-lookup"><span data-stu-id="6ccad-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="6ccad-112">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ccad-112">An Azure Storage account.</span></span> <span data-ttu-id="6ccad-113">Se você não tiver uma conta de armazenamento do Azure, você pode usar o hello [2.0 do CLI do Azure - gerenciar contas de armazenamento] [ lnk-manage-storage] toocreate um ou use Olá portal muito[criar uma conta de armazenamento] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="6ccad-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="6ccad-114">Entre e configure sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="6ccad-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="6ccad-115">Entre no tooyour conta do Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ccad-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="6ccad-116">No prompt de comando do hello, execute Olá [comando login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="6ccad-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="6ccad-117">Siga Olá instruções tooauthenticate usando código hello e entrar tooyour conta do Azure por meio de um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="6ccad-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="6ccad-118">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall Olá associadas com suas credenciais de contas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ccad-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="6ccad-119">Use os seguintes Olá [toolist comando Olá contas do Azure] [ lnk-az-account-command] disponíveis para você toouse:</span><span class="sxs-lookup"><span data-stu-id="6ccad-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="6ccad-120">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ccad-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="6ccad-121">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="6ccad-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="6ccad-122">Recupere os detalhes da sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="6ccad-122">Retrieve your storage account details</span></span>

<span data-ttu-id="6ccad-123">Olá etapas a seguir pressupõem que você criou sua conta de armazenamento usando Olá **Gerenciador de recursos de** modelo de implantação e não hello **clássico** modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="6ccad-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="6ccad-124">arquivo tooconfigure carregamentos de seus dispositivos, você precisa de cadeia de caracteres de conexão Olá para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ccad-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="6ccad-125">conta de armazenamento Olá deve estar no hello mesma assinatura que o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6ccad-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="6ccad-126">Você também precisa de nome de saudação de um contêiner de blob na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="6ccad-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="6ccad-127">Use suas chaves de conta de armazenamento de Olá tooretrieve de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="6ccad-128">Anote Olá **connectionString** valor.</span><span class="sxs-lookup"><span data-stu-id="6ccad-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="6ccad-129">Necessário em Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ccad-129">You need it in hello following steps.</span></span>

<span data-ttu-id="6ccad-130">Você pode usar um contêiner de blob existente para os uploads de arquivo ou criar um novo:</span><span class="sxs-lookup"><span data-stu-id="6ccad-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="6ccad-131">toolist Olá existente contêineres de blob em sua conta de armazenamento, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="6ccad-132">toocreate um contêiner de blob em sua conta de armazenamento, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="6ccad-133">Upload de arquivos</span><span class="sxs-lookup"><span data-stu-id="6ccad-133">File upload</span></span>

<span data-ttu-id="6ccad-134">Agora você pode configurar seu tooenable de hub IoT [funcionalidade de carregamento de arquivo] [ lnk-upload] usando os detalhes da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6ccad-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="6ccad-135">configuração de saudação requer Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="6ccad-136">**Contêiner de armazenamento**: um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6ccad-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="6ccad-137">Você recuperar informações de conta de armazenamento necessários Olá em Olá anterior da seção.</span><span class="sxs-lookup"><span data-stu-id="6ccad-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="6ccad-138">IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="6ccad-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="6ccad-139">**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo.</span><span class="sxs-lookup"><span data-stu-id="6ccad-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="6ccad-140">**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6ccad-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="6ccad-141">Definir hora tooone por padrão.</span><span class="sxs-lookup"><span data-stu-id="6ccad-141">Set tooone hour by default.</span></span>

<span data-ttu-id="6ccad-142">**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="6ccad-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="6ccad-143">Definir dia tooone por padrão.</span><span class="sxs-lookup"><span data-stu-id="6ccad-143">Set tooone day by default.</span></span>

<span data-ttu-id="6ccad-144">**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="6ccad-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="6ccad-145">Definir too10 por padrão.</span><span class="sxs-lookup"><span data-stu-id="6ccad-145">Set too10 by default.</span></span>

<span data-ttu-id="6ccad-146">Use configurações de carregamento de arquivo tooconfigure Olá do CLI do Azure comandos a seguir em seu hub IoT de saudação:</span><span class="sxs-lookup"><span data-stu-id="6ccad-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="6ccad-147">Em um shell de busca, use:</span><span class="sxs-lookup"><span data-stu-id="6ccad-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="6ccad-148">Em um prompt de comando do Windows, use:</span><span class="sxs-lookup"><span data-stu-id="6ccad-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="6ccad-149">Você pode examinar a configuração de carregamento de arquivo hello em seu hub IoT usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ccad-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="6ccad-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ccad-150">Next steps</span></span>

<span data-ttu-id="6ccad-151">Para obter mais informações sobre os recursos de carregamento de arquivo hello IoT Hub, consulte [carregar arquivos de um dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="6ccad-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="6ccad-152">Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="6ccad-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="6ccad-153">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="6ccad-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="6ccad-154">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6ccad-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="6ccad-155">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6ccad-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="6ccad-156">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="6ccad-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6ccad-157">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6ccad-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6ccad-158">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6ccad-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="6ccad-159">[Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="6ccad-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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