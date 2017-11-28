---
title: "aaaUse proativo de toodo de captura de pacote de rede de monitoramento com alertas e funções do Azure | Microsoft Docs"
description: Este artigo descreve como toocreate um alerta acionado captura de pacote com o observador de rede do Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="c5ac8-103">Usar a captura de pacotes para fazer um monitoramento de rede proativo com alertas e o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c5ac8-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="c5ac8-104">Captura de pacote do Inspetor de rede cria sessões de captura de tráfego tootrack dentro e fora de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="c5ac8-105">Olá captura arquivo pode ter um filtro que é definido tootrack Olá somente o tráfego que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="c5ac8-106">Esses dados, em seguida, são armazenados em um blob de armazenamento ou localmente no computador de convidado hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="c5ac8-107">Esse recurso pode ser iniciado remotamente a partir de outros cenários de automação como o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="c5ac8-108">Fornece de captura de pacote em que Hello capturas de pró-ativo toorun de recurso com base definido anomalias na rede.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="c5ac8-109">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações sobre as invasões de rede, depuração de comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="c5ac8-110">Os recursos implantados no Azure estão em execução 24/7.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="c5ac8-111">Você e sua equipe ativamente não é possível monitorar o status de saudação de todos os recursos 24/7.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="c5ac8-112">Por exemplo, o que acontecerá se ocorrer um problema às 2:00 da manhã?</span><span class="sxs-lookup"><span data-stu-id="c5ac8-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="c5ac8-113">Usando o observador de rede, alertas e funções de em Olá ecossistema do Azure, você pode responder proativamente com problemas de toosolve de dados e ferramentas de saudação em sua rede.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Cenário][scenario]

## <a name="prerequisites"></a><span data-ttu-id="c5ac8-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c5ac8-115">Prerequisites</span></span>

* <span data-ttu-id="c5ac8-116">versão mais recente de saudação do [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="c5ac8-117">Uma instância existente do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="c5ac8-118">Se você ainda não tiver um, [crie uma instância do Observador de Rede](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="c5ac8-119">Uma máquina virtual existente no hello mesma região do observador de rede com hello [extensão Windows](../virtual-machines/windows/extensions-nwa.md) ou [extensão da máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="c5ac8-120">Cenário</span><span class="sxs-lookup"><span data-stu-id="c5ac8-120">Scenario</span></span>

<span data-ttu-id="c5ac8-121">Neste exemplo, a VM estiver enviando mais segmentos TCP que o usual e desejar toobe alertado.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="c5ac8-122">Os segmentos TCP são usados como um exemplo aqui, e você pode utilizar qualquer condição de alerta.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="c5ac8-123">Quando você for alertado, você deseja tooreceive toounderstand de dados de nível de pacote por comunicação aumentou.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="c5ac8-124">Em seguida, você pode adotar medidas comunicação de tooregular tooreturn Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="c5ac8-125">Este cenário pressupõe que você tem uma instância existente do Observador de Rede e um grupo de recursos com uma máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="c5ac8-126">Olá lista a seguir é uma visão geral de fluxo de trabalho Olá ocorre:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="c5ac8-127">Um alerta é disparado em sua VM.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="c5ac8-128">alerta de saudação chama a função do Azure por meio de um webhook.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="c5ac8-129">A função do Azure processa alerta hello e inicia uma sessão de captura de pacote do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="c5ac8-130">captura de pacote de saudação é executado em Olá VM e o tráfego de coleta.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="c5ac8-131">Olá arquivo de captura de pacote é carregado tooa conta de armazenamento para diagnóstico e análise.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="c5ac8-132">tooautomate esse processo, podemos criar e conecte-se um alerta em nosso tootrigger VM quando Olá incidente.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="c5ac8-133">Também criamos uma função toocall em observador de rede.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="c5ac8-134">Este cenário Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-134">This scenario does hello following:</span></span>

* <span data-ttu-id="c5ac8-135">Cria uma função do Azure que inicia uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="c5ac8-136">Cria uma regra de alerta em uma máquina virtual e configura Olá toocall da regra de alerta Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="c5ac8-137">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="c5ac8-137">Create an Azure function</span></span>

<span data-ttu-id="c5ac8-138">Olá primeira etapa é toocreate um alerta de saudação do tooprocess de função do Azure e criar uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="c5ac8-139">Em Olá [portal do Azure](https://portal.azure.com), selecione **novo** > **de computação** > **aplicativo função**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Criar um aplicativo de funções][1-1]

2. <span data-ttu-id="c5ac8-141">Em Olá **aplicativo função** folha, digite Olá valores a seguir e, em seguida, selecione **Okey** toocreate Olá aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="c5ac8-142">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-142">**Setting**</span></span> | <span data-ttu-id="c5ac8-143">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-143">**Value**</span></span> | <span data-ttu-id="c5ac8-144">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="c5ac8-145">**Nome do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-145">**App name**</span></span>|<span data-ttu-id="c5ac8-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="c5ac8-146">PacketCaptureExample</span></span>|<span data-ttu-id="c5ac8-147">nome de saudação do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="c5ac8-148">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-148">**Subscription**</span></span>|<span data-ttu-id="c5ac8-149">[Sua assinatura] Olá assinatura para qual aplicativo de função toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="c5ac8-150">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-150">**Resource Group**</span></span>|<span data-ttu-id="c5ac8-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="c5ac8-151">PacketCaptureRG</span></span>|<span data-ttu-id="c5ac8-152">Olá recurso grupo toocontain Olá função app.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="c5ac8-153">**Plano de hospedagem**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-153">**Hosting Plan**</span></span>|<span data-ttu-id="c5ac8-154">Plano de consumo</span><span class="sxs-lookup"><span data-stu-id="c5ac8-154">Consumption Plan</span></span>| <span data-ttu-id="c5ac8-155">tipo de saudação do plano de seu aplicativo usa de função.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="c5ac8-156">As opções são planos de consumo ou planos do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="c5ac8-157">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-157">**Location**</span></span>|<span data-ttu-id="c5ac8-158">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="c5ac8-158">Central US</span></span>| <span data-ttu-id="c5ac8-159">região de saudação em qual aplicativo de função toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="c5ac8-160">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-160">**Storage Account**</span></span>|<span data-ttu-id="c5ac8-161">{gerado automaticamente}</span><span class="sxs-lookup"><span data-stu-id="c5ac8-161">{autogenerated}</span></span>| <span data-ttu-id="c5ac8-162">conta de armazenamento de saudação que precisa de funções do Azure para armazenamento de uso geral.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="c5ac8-163">Em Olá **PacketCaptureExample função aplicativos** folha, selecione **funções** > **função personalizada**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="c5ac8-164">Selecione **HttpTrigger Powershell**e, em seguida, digite Olá restantes informações.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="c5ac8-165">Por fim, toocreate função hello, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="c5ac8-166">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-166">**Setting**</span></span> | <span data-ttu-id="c5ac8-167">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-167">**Value**</span></span> | <span data-ttu-id="c5ac8-168">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="c5ac8-169">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-169">**Scenario**</span></span>|<span data-ttu-id="c5ac8-170">Experimental</span><span class="sxs-lookup"><span data-stu-id="c5ac8-170">Experimental</span></span>|<span data-ttu-id="c5ac8-171">Tipo de cenário</span><span class="sxs-lookup"><span data-stu-id="c5ac8-171">Type of scenario</span></span>|
    |<span data-ttu-id="c5ac8-172">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-172">**Name your function**</span></span>|<span data-ttu-id="c5ac8-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="c5ac8-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="c5ac8-174">Nome da função hello</span><span class="sxs-lookup"><span data-stu-id="c5ac8-174">Name of hello function</span></span>|
    |<span data-ttu-id="c5ac8-175">**Nível de autorização**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-175">**Authorization level**</span></span>|<span data-ttu-id="c5ac8-176">Função</span><span class="sxs-lookup"><span data-stu-id="c5ac8-176">Function</span></span>|<span data-ttu-id="c5ac8-177">Nível de autorização para a função hello</span><span class="sxs-lookup"><span data-stu-id="c5ac8-177">Authorization level for hello function</span></span>|

![Exemplo de funções][functions1]

> [!NOTE]
> <span data-ttu-id="c5ac8-179">modelo de PowerShell Olá é experimental e não tem suporte completo.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="c5ac8-180">As personalizações são necessárias para este exemplo e são explicadas em Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="c5ac8-181">Adicionar módulos</span><span class="sxs-lookup"><span data-stu-id="c5ac8-181">Add modules</span></span>

<span data-ttu-id="c5ac8-182">toouse cmdlets do PowerShell do Inspetor de rede, carregar o aplicativo hello mais recente do PowerShell módulo toohello função.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="c5ac8-183">Em seu computador local com hello mais recentes do Azure PowerShell módulos instalados, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="c5ac8-184">Isso proporciona exemplo hello caminho local dos seus módulos do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="c5ac8-185">Essas pastas são usadas em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-185">These folders are used in a later step.</span></span> <span data-ttu-id="c5ac8-186">módulos de saudação que são usados neste cenário são:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="c5ac8-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="c5ac8-187">AzureRM.Network</span></span>

    * <span data-ttu-id="c5ac8-188">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="c5ac8-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="c5ac8-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="c5ac8-189">AzureRM.Resources</span></span>

    ![Pastas do PowerShell][functions5]

1. <span data-ttu-id="c5ac8-191">Selecione **configurações do aplicativo de função** > **vá tooApp Editor serviço**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Configurações do aplicativo de funções][functions2]

1. <span data-ttu-id="c5ac8-193">Saudação de atalho **AlertPacketCapturePowershell** pasta e, em seguida, crie uma pasta chamada **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="c5ac8-194">Crie uma subpasta para cada módulo de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-194">Create a subfolder for each module that you need.</span></span>

    ![Pastas e subpastas][functions3]

    * <span data-ttu-id="c5ac8-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="c5ac8-196">AzureRM.Network</span></span>

    * <span data-ttu-id="c5ac8-197">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="c5ac8-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="c5ac8-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="c5ac8-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="c5ac8-199">Saudação de atalho **AzureRM.Network** subpasta e, em seguida, selecione **carregar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="c5ac8-200">Vá tooyour Azure módulos.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="c5ac8-201">No local de saudação **AzureRM.Network** pasta, selecione todos os arquivos de saudação na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="c5ac8-202">Depois, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="c5ac8-203">Repita essas etapas para **AzureRM.Profile** e **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Carregar arquivos][functions6]

1. <span data-ttu-id="c5ac8-205">Depois de concluir, cada pasta deve ter arquivos de módulo do PowerShell Olá em sua máquina local.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Arquivos do PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="c5ac8-207">Autenticação</span><span class="sxs-lookup"><span data-stu-id="c5ac8-207">Authentication</span></span>

<span data-ttu-id="c5ac8-208">cmdlets do PowerShell Olá toouse, você deverá se autenticar.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="c5ac8-209">Configurar a autenticação no aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="c5ac8-210">autenticação tooconfigure, você deve configurar variáveis de ambiente e carregar um aplicativo de função de toohello do arquivo de chave criptografada.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="c5ac8-211">Este cenário fornece apenas um exemplo de como a autenticação tooimplement com funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="c5ac8-212">Existem outra maneiras toodo isso.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="c5ac8-213">Credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="c5ac8-213">Encrypted credentials</span></span>

<span data-ttu-id="c5ac8-214">saudação de script do PowerShell a seguir cria um arquivo de chave chamado **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="c5ac8-215">Ele também fornece uma versão criptografada da senha de saudação que é fornecida.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="c5ac8-216">Essa senha é hello mesma senha que é definida para o aplicativo do Active Directory do Azure hello que é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="c5ac8-217">Olá Editor de aplicativo do serviço de aplicativo de função hello, cria uma pasta chamada **chaves** em **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="c5ac8-218">Em seguida, carregar Olá **PassEncryptKey.key** arquivo criado no exemplo anterior de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Chave de funções][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="c5ac8-220">Recuperar valores de variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="c5ac8-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="c5ac8-221">requisito de final de saudação é tooset variáveis de ambiente de saudação são valores de saudação tooaccess necessário para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="c5ac8-222">Olá lista a seguir mostra as variáveis de ambiente de saudação que são criadas:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="c5ac8-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="c5ac8-223">AzureClientID</span></span>

* <span data-ttu-id="c5ac8-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="c5ac8-224">AzureTenant</span></span>

* <span data-ttu-id="c5ac8-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="c5ac8-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="c5ac8-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="c5ac8-226">AzureClientID</span></span>

<span data-ttu-id="c5ac8-227">ID do cliente Olá é hello ID de um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="c5ac8-228">Se você ainda não tiver um aplicativo toouse, execute um aplicativo para Olá toocreate de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="c5ac8-229">senha de saudação que você usa ao criar o aplicativo hello deveria ser Olá mesma senha que você criou anteriormente ao salvar o arquivo de chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="c5ac8-230">No portal do Azure de Olá, selecione **assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="c5ac8-231">Selecione Olá assinatura toouse e, em seguida, selecione **(IAM) do controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![IAM de funções][functions9]

1. <span data-ttu-id="c5ac8-233">Escolha Olá conta toouse e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="c5ac8-234">Copiar Olá ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-234">Copy hello Application ID.</span></span>

    ![ID do Aplicativo de funções][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="c5ac8-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="c5ac8-236">AzureTenant</span></span>

<span data-ttu-id="c5ac8-237">Obter ID de locatário Olá executando Olá PowerShell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="c5ac8-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="c5ac8-238">AzureCredPassword</span></span>

<span data-ttu-id="c5ac8-239">valor de Olá Olá AzureCredPassword da variável de ambiente é o valor de saudação obtido executando Olá PowerShell de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="c5ac8-240">Este exemplo é Olá mesmo que é mostrada na saudação anterior **credenciais criptografadas** seção.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="c5ac8-241">Olá valor que é necessário Olá de saída de hello `$Encryptedpassword` variável.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="c5ac8-242">Isso é Olá serviço principal senha criptografada usando o script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="c5ac8-243">Variáveis de ambiente de saudação do repositório</span><span class="sxs-lookup"><span data-stu-id="c5ac8-243">Store hello environment variables</span></span>

1. <span data-ttu-id="c5ac8-244">Vá toohello função app.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-244">Go toohello function app.</span></span> <span data-ttu-id="c5ac8-245">Selecione **Configurações do aplicativo de função** > **Definir configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Definir configurações de aplicativo][functions11]

1. <span data-ttu-id="c5ac8-247">Adicionar variáveis de ambiente hello e suas configurações de aplicativo toohello valores e, em seguida, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Configurações do aplicativo][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="c5ac8-249">Adicionar a função do PowerShell toohello</span><span class="sxs-lookup"><span data-stu-id="c5ac8-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="c5ac8-250">Agora é hora toomake chamadas em observador de rede de dentro de Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="c5ac8-251">Dependendo dos requisitos de hello, implementação Olá dessa função pode variar.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="c5ac8-252">No entanto, o fluxo geral de saudação do código de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="c5ac8-253">Processar os parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-253">Process input parameters.</span></span>
2. <span data-ttu-id="c5ac8-254">Pacote existente de consulta de captura tooverify limites e resolver conflitos de nome.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="c5ac8-255">Criar uma captura de pacotes com os devidos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="c5ac8-256">Pesquisar a captura de pacotes periodicamente até concluir.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="c5ac8-257">Notifica o usuário Olá que a sessão de captura de pacote de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="c5ac8-258">Olá, exemplo a seguir é código do PowerShell que pode ser usado na função de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="c5ac8-259">Há valores que precisam toobe substituído para **subscriptionId**, **resourceGroupName**, e **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="c5ac8-260">Recuperar a URL de função hello</span><span class="sxs-lookup"><span data-stu-id="c5ac8-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="c5ac8-261">Depois de criar sua função, configure a URL do hello toocall alerta associado à função hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="c5ac8-262">tooget esse valor, copiar Olá função URL de seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Localizando Olá função URL][functions13]

2. <span data-ttu-id="c5ac8-264">Copie URL de função Olá para seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-264">Copy hello function URL for your function app.</span></span>

    ![Copiar URL da função de saudação][2]

<span data-ttu-id="c5ac8-266">Se você precisar de propriedades personalizadas na carga de saudação de solicitação POST webhook hello, consulte muito[configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="c5ac8-267">Configurar um alerta em uma VM</span><span class="sxs-lookup"><span data-stu-id="c5ac8-267">Configure an alert on a VM</span></span>

<span data-ttu-id="c5ac8-268">Alertas podem ser configurados toonotify indivíduos quando uma métrica específica exceder um limite atribuído tooit.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="c5ac8-269">Neste exemplo, alerta hello está em Olá segmentos TCP que são enviados, mas Olá alerta pode ser acionado para muitas outras métricas.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="c5ac8-270">Neste exemplo, um alerta é configurado toocall uma função de saudação do webhook toocall.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="c5ac8-271">Criar regra de alerta de saudação</span><span class="sxs-lookup"><span data-stu-id="c5ac8-271">Create hello alert rule</span></span>

<span data-ttu-id="c5ac8-272">Vá tooan máquina de virtual existente e, em seguida, adicione uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="c5ac8-273">Mais documentação detalhada sobre como configurar alertas pode ser encontrada em [Criar alertas do Monitor do Azure para serviços do Azure - Portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="c5ac8-274">Digite Olá Olá valores a seguir **regra de alerta** folha e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="c5ac8-275">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-275">**Setting**</span></span> | <span data-ttu-id="c5ac8-276">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-276">**Value**</span></span> | <span data-ttu-id="c5ac8-277">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="c5ac8-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-278">**Name**</span></span>|<span data-ttu-id="c5ac8-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="c5ac8-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="c5ac8-280">Nome da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="c5ac8-281">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-281">**Description**</span></span>|<span data-ttu-id="c5ac8-282">Segmentos TCP enviados limite excedido</span><span class="sxs-lookup"><span data-stu-id="c5ac8-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="c5ac8-283">Descrição de saudação de regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="c5ac8-284">**Métrica**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-284">**Metric**</span></span>|<span data-ttu-id="c5ac8-285">Segmentos TCP enviados</span><span class="sxs-lookup"><span data-stu-id="c5ac8-285">TCP segments sent</span></span>| <span data-ttu-id="c5ac8-286">alerta de saudação do Hello métrica toouse tootrigger.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="c5ac8-287">**Condição**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-287">**Condition**</span></span>|<span data-ttu-id="c5ac8-288">Maior que</span><span class="sxs-lookup"><span data-stu-id="c5ac8-288">Greater than</span></span>| <span data-ttu-id="c5ac8-289">Olá condição toouse ao avaliar a métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="c5ac8-290">**Limite**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-290">**Threshold**</span></span>|<span data-ttu-id="c5ac8-291">100</span><span class="sxs-lookup"><span data-stu-id="c5ac8-291">100</span></span>| <span data-ttu-id="c5ac8-292">valor de saudação da métrica de saudação que dispara um alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="c5ac8-293">Esse valor deve ser definido como tooa o valor válido para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="c5ac8-294">**Período**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-294">**Period**</span></span>|<span data-ttu-id="c5ac8-295">Sobre Olá últimos cinco minutos</span><span class="sxs-lookup"><span data-stu-id="c5ac8-295">Over hello last five minutes</span></span>| <span data-ttu-id="c5ac8-296">Determina o período de saudação na qual toolook para o limite de saudação na métrica hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="c5ac8-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="c5ac8-297">**Webhook**</span></span>|<span data-ttu-id="c5ac8-298">[URL do webhook do aplicativo de funções]</span><span class="sxs-lookup"><span data-stu-id="c5ac8-298">[webhook URL from function app]</span></span>| <span data-ttu-id="c5ac8-299">URL do webhook saudação do aplicativo de função hello criado nas etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="c5ac8-300">métrica de segmentos TCP Olá não está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="c5ac8-301">Saiba mais sobre como as métricas adicionais de tooenable visitando [habilitar o monitoramento e diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="c5ac8-302">Examine os resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="c5ac8-302">Review hello results</span></span>

<span data-ttu-id="c5ac8-303">Depois de critérios de saudação para gatilhos alerta hello, uma captura de pacote é criada.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="c5ac8-304">Vá tooNetwork Inspetor e, em seguida, selecione **captura de pacote**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="c5ac8-305">Nessa página, você pode selecionar Olá captura arquivo link toodownload Olá pacote captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Exibir a captura de pacotes][functions14]

<span data-ttu-id="c5ac8-307">Se o arquivo de captura Olá é armazenado localmente, você pode recuperá-lo ao entrar na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="c5ac8-308">Para obter instruções sobre como baixar os arquivos das contas de armazenamento do Azure, veja [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c5ac8-309">Outra ferramenta que você pode usar é o [Gerenciador de armazenamento](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="c5ac8-310">Depois que a captura for baixada, você poderá exibi-la usando qualquer ferramenta que possa ler um arquivo **.cap**.</span><span class="sxs-lookup"><span data-stu-id="c5ac8-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="c5ac8-311">Estes são links tootwo dessas ferramentas:</span><span class="sxs-lookup"><span data-stu-id="c5ac8-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="c5ac8-312">Analisador de Mensagens da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c5ac8-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="c5ac8-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="c5ac8-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="c5ac8-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5ac8-314">Next steps</span></span>

<span data-ttu-id="c5ac8-315">Saiba como tooview seu pacote captura visitando [análise de captura de pacote com o Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="c5ac8-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
