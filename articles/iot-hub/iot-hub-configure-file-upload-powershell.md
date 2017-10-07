---
title: carregamento de arquivo aaaUse hello Azure PowerShell tooconfigure | Microsoft Docs
description: "Como toouse hello Azure PowerShell cmdlets tooconfigure seu arquivo de tooenable de hub IoT carregamentos de dispositivos conectados. Inclui informações sobre como configurar a conta de armazenamento do Azure de destino hello."
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
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="d2665-104">Configurar uploads de arquivo do Hub IoT usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2665-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="d2665-105">Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d2665-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="d2665-106">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="d2665-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="d2665-107">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d2665-108">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2665-108">An active Azure account.</span></span> <span data-ttu-id="d2665-109">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d2665-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d2665-110">[Cmdlets do Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="d2665-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="d2665-111">Um Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2665-111">An Azure IoT hub.</span></span> <span data-ttu-id="d2665-112">Se você não tiver um hub IoT, você pode usar o hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate um ou use Olá portal muito[criar um hub IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="d2665-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="d2665-113">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2665-113">An Azure storage account.</span></span> <span data-ttu-id="d2665-114">Se você não tiver uma conta de armazenamento do Azure, você pode usar o hello [cmdlets do PowerShell do armazenamento do Azure] [ lnk-powershell-storage] toocreate um ou use Olá portal muito[criar uma conta de armazenamento] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="d2665-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="d2665-115">Entre e configure sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="d2665-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="d2665-116">Entre no tooyour conta do Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d2665-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="d2665-117">No prompt do PowerShell hello, executar Olá **AzureRmAccount Login** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d2665-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="d2665-118">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="d2665-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="d2665-119">Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="d2665-120">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toomanage seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2665-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="d2665-121">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="d2665-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="d2665-122">Recupere os detalhes da sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d2665-122">Retrieve your storage account details</span></span>

<span data-ttu-id="d2665-123">Olá etapas a seguir pressupõem que você criou sua conta de armazenamento usando Olá **Gerenciador de recursos de** modelo de implantação e não hello **clássico** modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="d2665-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="d2665-124">arquivo tooconfigure carregamentos de seus dispositivos, você precisa de cadeia de caracteres de conexão Olá para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2665-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="d2665-125">conta de armazenamento Olá deve estar no hello mesma assinatura que o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d2665-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="d2665-126">Você também precisa de nome de saudação de um contêiner de blob na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="d2665-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="d2665-127">Use suas chaves de conta de armazenamento de Olá tooretrieve de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="d2665-128">Anote Olá **key1** valor de chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2665-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="d2665-129">Necessário em Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2665-129">You need it in hello following steps.</span></span>

<span data-ttu-id="d2665-130">Você pode usar um contêiner de blob existente para os uploads de arquivo ou criar um novo:</span><span class="sxs-lookup"><span data-stu-id="d2665-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="d2665-131">toolist Olá existente contêineres de blob em sua conta de armazenamento, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="d2665-132">toocreate um contêiner de blob em sua conta de armazenamento, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="d2665-133">Configurar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="d2665-133">Configure your IoT hub</span></span>

<span data-ttu-id="d2665-134">Agora você pode configurar seu tooenable de hub IoT [funcionalidade de carregamento de arquivo] [ lnk-upload] usando os detalhes da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2665-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="d2665-135">configuração de saudação requer Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2665-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="d2665-136">**Contêiner de armazenamento**: um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d2665-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="d2665-137">Você recuperar informações de conta de armazenamento necessários Olá em Olá anterior da seção.</span><span class="sxs-lookup"><span data-stu-id="d2665-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="d2665-138">IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="d2665-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="d2665-139">**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d2665-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="d2665-140">**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2665-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="d2665-141">Definir hora tooone por padrão.</span><span class="sxs-lookup"><span data-stu-id="d2665-141">Set tooone hour by default.</span></span>

<span data-ttu-id="d2665-142">**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="d2665-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="d2665-143">Definir dia tooone por padrão.</span><span class="sxs-lookup"><span data-stu-id="d2665-143">Set tooone day by default.</span></span>

<span data-ttu-id="d2665-144">**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d2665-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="d2665-145">Definir too10 por padrão.</span><span class="sxs-lookup"><span data-stu-id="d2665-145">Set too10 by default.</span></span>

<span data-ttu-id="d2665-146">Use Olá configurações de carregamento do arquivo de saudação do PowerShell cmdlet tooconfigure a seguir em seu hub IoT:</span><span class="sxs-lookup"><span data-stu-id="d2665-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a><span data-ttu-id="d2665-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2665-147">Next steps</span></span>

<span data-ttu-id="d2665-148">Para obter mais informações sobre os recursos de carregamento de arquivo hello IoT Hub, consulte [carregar arquivos de um dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="d2665-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="d2665-149">Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d2665-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="d2665-150">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="d2665-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="d2665-151">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="d2665-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="d2665-152">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="d2665-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="d2665-153">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="d2665-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d2665-154">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d2665-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d2665-155">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d2665-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="d2665-156">[Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="d2665-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md