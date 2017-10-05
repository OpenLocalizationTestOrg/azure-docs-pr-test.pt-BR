---
title: Usar a captura de pacote para fazer o monitoramento de rede proativo com alertas e o Azure Functions | Microsoft Docs
description: Este artigo descreve como criar uma captura de pacotes disparada por alertas com o Observador de Rede do Azure
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
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="37220-103">Usar a captura de pacotes para fazer um monitoramento de rede proativo com alertas e o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="37220-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="37220-104">A captura de pacotes do Observador de Rede permite criar sessões de captura para controlar o tráfego dentro e fora de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="37220-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="37220-105">O arquivo de captura pode ter um filtro que é definido para acompanhar apenas o tráfego que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="37220-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="37220-106">Esses dados são armazenados em um blob de armazenamento ou localmente na máquina convidada.</span><span class="sxs-lookup"><span data-stu-id="37220-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="37220-107">Esse recurso pode ser iniciado remotamente a partir de outros cenários de automação como o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="37220-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="37220-108">A captura de pacotes fornece a capacidade de executar capturas proativas com base nos problemas de rede definidos.</span><span class="sxs-lookup"><span data-stu-id="37220-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="37220-109">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações sobre as invasões de rede, depuração de comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="37220-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="37220-110">Os recursos implantados no Azure estão em execução 24/7.</span><span class="sxs-lookup"><span data-stu-id="37220-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="37220-111">Você e sua equipe não pode monitorar ativamente o status de todos os recursos 24/7.</span><span class="sxs-lookup"><span data-stu-id="37220-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="37220-112">Por exemplo, o que acontecerá se ocorrer um problema às 2:00 da manhã?</span><span class="sxs-lookup"><span data-stu-id="37220-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="37220-113">Usando o Observador de Rede, Alertas e Funções de dentro do ecossistema do Azure, você pode responder proativamente com dados e ferramentas para resolver problemas em sua rede.</span><span class="sxs-lookup"><span data-stu-id="37220-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![Cenário][scenario]

## <a name="prerequisites"></a><span data-ttu-id="37220-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="37220-115">Prerequisites</span></span>

* <span data-ttu-id="37220-116">A versão mais recente do [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="37220-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="37220-117">Uma instância existente do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="37220-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="37220-118">Se você ainda não tiver um, [crie uma instância do Observador de Rede](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="37220-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="37220-119">Uma máquina virtual existente na mesma região que o Observador de Rede com a [extensão Windows](../virtual-machines/windows/extensions-nwa.md) ou [extensão de máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="37220-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="37220-120">Cenário</span><span class="sxs-lookup"><span data-stu-id="37220-120">Scenario</span></span>

<span data-ttu-id="37220-121">Neste exemplo, sua VM está enviando mais segmentos TCP que o usual e você quer ser alertado.</span><span class="sxs-lookup"><span data-stu-id="37220-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="37220-122">Os segmentos TCP são usados como um exemplo aqui, e você pode utilizar qualquer condição de alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="37220-123">Quando você for alertado, você deseja receber dados de nível de pacote para entender por que aumentou a comunicação.</span><span class="sxs-lookup"><span data-stu-id="37220-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="37220-124">Em seguida, você pode tomar medidas para retornar a máquina virtual para comunicação regular.</span><span class="sxs-lookup"><span data-stu-id="37220-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="37220-125">Este cenário pressupõe que você tem uma instância existente do Observador de Rede e um grupo de recursos com uma máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="37220-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="37220-126">A lista a seguir é uma visão geral do fluxo de trabalho que ocorre:</span><span class="sxs-lookup"><span data-stu-id="37220-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="37220-127">Um alerta é disparado em sua VM.</span><span class="sxs-lookup"><span data-stu-id="37220-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="37220-128">O alerta chama sua Função do Azure por meio de um webhook.</span><span class="sxs-lookup"><span data-stu-id="37220-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="37220-129">A função do Azure processa o alerta e inicia uma sessão de captura de pacotes do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="37220-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="37220-130">A captura de pacotes é executada na VM e coleta o tráfego.</span><span class="sxs-lookup"><span data-stu-id="37220-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="37220-131">O pacote de captura é carregado em uma conta de armazenamento para um diagnóstico e análise.</span><span class="sxs-lookup"><span data-stu-id="37220-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="37220-132">Para automatizar esse processo, criamos e conectamos um Alerta em nossa VM para disparar quando ocorre o incidente.</span><span class="sxs-lookup"><span data-stu-id="37220-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="37220-133">Também criamos uma função a ser chamada no Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="37220-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="37220-134">Esse cenário faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37220-134">This scenario does the following:</span></span>

* <span data-ttu-id="37220-135">Cria uma função do Azure que inicia uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="37220-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="37220-136">Cria uma regra de alerta em uma máquina virtual e configura a regra de alerta para chamar a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="37220-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="37220-137">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="37220-137">Create an Azure function</span></span>

<span data-ttu-id="37220-138">A primeira etapa é criar uma função do Azure para processar o alerta e criar uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="37220-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="37220-139">No [Portal do Azure](https://portal.azure.com), selecione **Novo** > **Computação** > **Aplicativo de Funções**.</span><span class="sxs-lookup"><span data-stu-id="37220-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Criar um aplicativo de funções][1-1]

2. <span data-ttu-id="37220-141">Na folha **Aplicativo de funções**, insira os seguintes valores e selecione **OK** para criar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="37220-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="37220-142">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="37220-142">**Setting**</span></span> | <span data-ttu-id="37220-143">**Valor**</span><span class="sxs-lookup"><span data-stu-id="37220-143">**Value**</span></span> | <span data-ttu-id="37220-144">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="37220-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="37220-145">**Nome do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="37220-145">**App name**</span></span>|<span data-ttu-id="37220-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="37220-146">PacketCaptureExample</span></span>|<span data-ttu-id="37220-147">O nome do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-147">The name of the function app.</span></span>|
    |<span data-ttu-id="37220-148">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="37220-148">**Subscription**</span></span>|<span data-ttu-id="37220-149">[Sua assinatura]A assinatura na qual a criar o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="37220-150">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="37220-150">**Resource Group**</span></span>|<span data-ttu-id="37220-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="37220-151">PacketCaptureRG</span></span>|<span data-ttu-id="37220-152">O nome do grupo de recursos para conter o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="37220-153">**Plano de hospedagem**</span><span class="sxs-lookup"><span data-stu-id="37220-153">**Hosting Plan**</span></span>|<span data-ttu-id="37220-154">Plano de consumo</span><span class="sxs-lookup"><span data-stu-id="37220-154">Consumption Plan</span></span>| <span data-ttu-id="37220-155">O tipo de plano de que seu aplicativo de funções usa.</span><span class="sxs-lookup"><span data-stu-id="37220-155">The type of plan your function app uses.</span></span> <span data-ttu-id="37220-156">As opções são planos de consumo ou planos do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="37220-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="37220-157">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="37220-157">**Location**</span></span>|<span data-ttu-id="37220-158">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="37220-158">Central US</span></span>| <span data-ttu-id="37220-159">A região na qual um aplicativo de funções será criado.</span><span class="sxs-lookup"><span data-stu-id="37220-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="37220-160">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="37220-160">**Storage Account**</span></span>|<span data-ttu-id="37220-161">{gerado automaticamente}</span><span class="sxs-lookup"><span data-stu-id="37220-161">{autogenerated}</span></span>| <span data-ttu-id="37220-162">A conta de armazenamento que o Azure Functions usa para armazenamento de finalidade geral.</span><span class="sxs-lookup"><span data-stu-id="37220-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="37220-163">Na folha **Aplicativos do Functions PacketCaptureExample**, selecione **Functions** > **Função personalizada** >**+**.</span><span class="sxs-lookup"><span data-stu-id="37220-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="37220-164">Selecione **HttpTrigger-Powershell** e, em seguida, insira as informações restantes.</span><span class="sxs-lookup"><span data-stu-id="37220-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="37220-165">Finalmente, para criar a função, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="37220-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="37220-166">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="37220-166">**Setting**</span></span> | <span data-ttu-id="37220-167">**Valor**</span><span class="sxs-lookup"><span data-stu-id="37220-167">**Value**</span></span> | <span data-ttu-id="37220-168">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="37220-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="37220-169">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="37220-169">**Scenario**</span></span>|<span data-ttu-id="37220-170">Experimental</span><span class="sxs-lookup"><span data-stu-id="37220-170">Experimental</span></span>|<span data-ttu-id="37220-171">Tipo de cenário</span><span class="sxs-lookup"><span data-stu-id="37220-171">Type of scenario</span></span>|
    |<span data-ttu-id="37220-172">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="37220-172">**Name your function**</span></span>|<span data-ttu-id="37220-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="37220-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="37220-174">Nome da função</span><span class="sxs-lookup"><span data-stu-id="37220-174">Name of the function</span></span>|
    |<span data-ttu-id="37220-175">**Nível de autorização**</span><span class="sxs-lookup"><span data-stu-id="37220-175">**Authorization level**</span></span>|<span data-ttu-id="37220-176">Função</span><span class="sxs-lookup"><span data-stu-id="37220-176">Function</span></span>|<span data-ttu-id="37220-177">Nível de autorização para a função</span><span class="sxs-lookup"><span data-stu-id="37220-177">Authorization level for the function</span></span>|

![Exemplo de funções][functions1]

> [!NOTE]
> <span data-ttu-id="37220-179">O modelo do PowerShell é experimental e não tem suporte completo.</span><span class="sxs-lookup"><span data-stu-id="37220-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="37220-180">As personalizações são necessárias para este exemplo e explicadas nas seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="37220-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="37220-181">Adicionar módulos</span><span class="sxs-lookup"><span data-stu-id="37220-181">Add modules</span></span>

<span data-ttu-id="37220-182">Para usar os cmdlets do PowerShell no Observador de Rede, faça upload do último módulo do PowerShell no aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="37220-183">No computador local com os módulos mais recentes do Azure PowerShell instalados, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37220-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="37220-184">Esse exemplo fornece o caminho local dos módulos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37220-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="37220-185">Essas pastas são usadas em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="37220-185">These folders are used in a later step.</span></span> <span data-ttu-id="37220-186">Os módulos usados neste cenário são:</span><span class="sxs-lookup"><span data-stu-id="37220-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="37220-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="37220-187">AzureRM.Network</span></span>

    * <span data-ttu-id="37220-188">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="37220-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="37220-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="37220-189">AzureRM.Resources</span></span>

    ![Pastas do PowerShell][functions5]

1. <span data-ttu-id="37220-191">Selecione **Configurações do Aplicativo de funções** > **Ir para o Editor do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="37220-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![Configurações do aplicativo de funções][functions2]

1. <span data-ttu-id="37220-193">Clique com o botão direito do mouse na pasta **AlertPacketCapturePowershell** e crie uma pasta chamada **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="37220-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="37220-194">Crie uma subpasta para cada módulo de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="37220-194">Create a subfolder for each module that you need.</span></span>

    ![Pastas e subpastas][functions3]

    * <span data-ttu-id="37220-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="37220-196">AzureRM.Network</span></span>

    * <span data-ttu-id="37220-197">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="37220-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="37220-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="37220-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="37220-199">Clique com o botão direito do mouse na subpasta **AzureRM.Network** e selecione **Fazer Upload de Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="37220-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="37220-200">Vá para os módulos do Azure.</span><span class="sxs-lookup"><span data-stu-id="37220-200">Go to your Azure modules.</span></span> <span data-ttu-id="37220-201">Na pasta **AzureRM.Network** local, selecione todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="37220-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="37220-202">Depois, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="37220-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="37220-203">Repita essas etapas para **AzureRM.Profile** e **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="37220-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Carregar arquivos][functions6]

1. <span data-ttu-id="37220-205">Ao concluir, cada pasta deve ter os arquivos de módulo do PowerShell do seu computador local.</span><span class="sxs-lookup"><span data-stu-id="37220-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![Arquivos do PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="37220-207">Autenticação</span><span class="sxs-lookup"><span data-stu-id="37220-207">Authentication</span></span>

<span data-ttu-id="37220-208">Para usar os cmdlets do PowerShell, você deve se autenticar.</span><span class="sxs-lookup"><span data-stu-id="37220-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="37220-209">Configure a autenticação no aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-209">You configure authentication in the function app.</span></span> <span data-ttu-id="37220-210">Para configurar a autenticação, você deverá configurar as variáveis de ambiente e carregar um arquivo de chave criptografado no aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="37220-211">Esse cenário fornece apenas um exemplo de como implementar a autenticação com o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="37220-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="37220-212">Há outras maneiras de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="37220-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="37220-213">Credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="37220-213">Encrypted credentials</span></span>

<span data-ttu-id="37220-214">O seguinte script do PowerShell cria um arquivo de chave chamado **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="37220-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="37220-215">Ele também fornece uma versão criptografada da senha fornecida.</span><span class="sxs-lookup"><span data-stu-id="37220-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="37220-216">Essa senha é a mesma senha que é definida para o Aplicativo do Azure Active Directory que é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="37220-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

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

<span data-ttu-id="37220-217">No Editor do Serviço de Aplicativo do aplicativo de funções, crie uma pasta chamada **chaves** em **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="37220-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="37220-218">Em seguida, carregue o arquivo **PassEncryptKey.key** criado no exemplo anterior do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37220-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![Chave de funções][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="37220-220">Recuperar valores de variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="37220-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="37220-221">O requisito final é instalar as variáveis de ambiente necessárias para acessar os valores de autenticação.</span><span class="sxs-lookup"><span data-stu-id="37220-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="37220-222">A seguinte lista mostra as variáveis de ambiente criadas:</span><span class="sxs-lookup"><span data-stu-id="37220-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="37220-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="37220-223">AzureClientID</span></span>

* <span data-ttu-id="37220-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="37220-224">AzureTenant</span></span>

* <span data-ttu-id="37220-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="37220-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="37220-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="37220-226">AzureClientID</span></span>

<span data-ttu-id="37220-227">A ID do cliente é a ID de um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37220-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="37220-228">Caso ainda não tenha um aplicativo a ser usado, execute o exemplo a seguir para criar um.</span><span class="sxs-lookup"><span data-stu-id="37220-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="37220-229">A senha que você usa ao criar o aplicativo deve ser a mesma senha criada anteriormente ao salvar o arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="37220-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="37220-230">No Portal do Azure, selecione **Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="37220-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="37220-231">Selecione a assinatura para usar e, em seguida, selecione **Controle de Acesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="37220-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![IAM de funções][functions9]

1. <span data-ttu-id="37220-233">Escolha a conta a ser usada e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="37220-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="37220-234">Copie a ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37220-234">Copy the Application ID.</span></span>

    ![ID do Aplicativo de funções][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="37220-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="37220-236">AzureTenant</span></span>

<span data-ttu-id="37220-237">Obtenha a ID do locatário com a execução do seguinte exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37220-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="37220-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="37220-238">AzureCredPassword</span></span>

<span data-ttu-id="37220-239">O valor da variável de ambiente AzureCredPassword é o valor que você obtém executando o exemplo a seguir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37220-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="37220-240">Esse é o mesmo exemplo mostrado na seção anterior, **Credenciais criptografadas**.</span><span class="sxs-lookup"><span data-stu-id="37220-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="37220-241">O valor necessário é a saída da variável `$Encryptedpassword`.</span><span class="sxs-lookup"><span data-stu-id="37220-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="37220-242">Essa é a senha da entidade de serviço que você criptografou usando o script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37220-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

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

### <a name="store-the-environment-variables"></a><span data-ttu-id="37220-243">Armazenar as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="37220-243">Store the environment variables</span></span>

1. <span data-ttu-id="37220-244">Vá para o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-244">Go to the function app.</span></span> <span data-ttu-id="37220-245">Selecione **Configurações do aplicativo de função** > **Definir configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="37220-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Definir configurações de aplicativo][functions11]

1. <span data-ttu-id="37220-247">Adicione as variáveis de ambiente e seus valores às configurações do aplicativo e selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="37220-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![Configurações do aplicativo][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="37220-249">Adicione o PowerShell para a função</span><span class="sxs-lookup"><span data-stu-id="37220-249">Add PowerShell to the function</span></span>

<span data-ttu-id="37220-250">Agora é hora de fazer chamadas no Observador de Rede de dentro da função do Azure.</span><span class="sxs-lookup"><span data-stu-id="37220-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="37220-251">Dependendo dos requisitos, a implementação dessa função pode variar.</span><span class="sxs-lookup"><span data-stu-id="37220-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="37220-252">No entanto, o fluxo geral do código é assim:</span><span class="sxs-lookup"><span data-stu-id="37220-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="37220-253">Processar os parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="37220-253">Process input parameters.</span></span>
2. <span data-ttu-id="37220-254">Consultar as capturas de pacotes existentes para verificar os limites e resolver os conflitos de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="37220-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="37220-255">Criar uma captura de pacotes com os devidos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="37220-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="37220-256">Pesquisar a captura de pacotes periodicamente até concluir.</span><span class="sxs-lookup"><span data-stu-id="37220-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="37220-257">Notificar o usuário que a sessão de captura de pacotes foi concluída.</span><span class="sxs-lookup"><span data-stu-id="37220-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="37220-258">O exemplo a seguir é o código do PowerShell que pode ser usado na função.</span><span class="sxs-lookup"><span data-stu-id="37220-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="37220-259">Há valores que precisam ser substituídos em **subscriptionId**, **resourceGroupName** e **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="37220-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
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


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="37220-260">Recuperar a URL da função</span><span class="sxs-lookup"><span data-stu-id="37220-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="37220-261">Depois de criar sua função, configure o alerta para chamar a URL associada à função.</span><span class="sxs-lookup"><span data-stu-id="37220-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="37220-262">Para obter esse valor, copie a URL da função a partir de seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-262">To get this value, copy the function URL from your function app.</span></span>

    ![Localizando a URL da função][functions13]

2. <span data-ttu-id="37220-264">Copie a URL da função para seu Aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="37220-264">Copy the function URL for your function app.</span></span>

    ![Copiando a URL da função][2]

<span data-ttu-id="37220-266">Se você precisar de propriedades personalizadas no conteúdo da solicitação POST do webhook, confira [Configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="37220-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="37220-267">Configurar um alerta em uma VM</span><span class="sxs-lookup"><span data-stu-id="37220-267">Configure an alert on a VM</span></span>

<span data-ttu-id="37220-268">Os alertas podem ser configurados para notificar as pessoas quando uma métrica específica cruza um limite atribuído a ela.</span><span class="sxs-lookup"><span data-stu-id="37220-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="37220-269">Neste exemplo, o alerta está nos segmentos TCP enviados, mas o alerta pode ser disparado para muitas outras métricas.</span><span class="sxs-lookup"><span data-stu-id="37220-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="37220-270">No exemplo, um alerta é configurado para chamar um webhook para chamar a função.</span><span class="sxs-lookup"><span data-stu-id="37220-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="37220-271">Criar a regra de alerta</span><span class="sxs-lookup"><span data-stu-id="37220-271">Create the alert rule</span></span>

<span data-ttu-id="37220-272">Vá até uma máquina virtual existente e adicione uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="37220-273">Mais documentação detalhada sobre como configurar alertas pode ser encontrada em [Criar alertas do Monitor do Azure para serviços do Azure - Portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37220-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="37220-274">Insira os seguintes valores na folha **Regra de alerta** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="37220-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="37220-275">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="37220-275">**Setting**</span></span> | <span data-ttu-id="37220-276">**Valor**</span><span class="sxs-lookup"><span data-stu-id="37220-276">**Value**</span></span> | <span data-ttu-id="37220-277">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="37220-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="37220-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="37220-278">**Name**</span></span>|<span data-ttu-id="37220-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="37220-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="37220-280">Nome da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="37220-281">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="37220-281">**Description**</span></span>|<span data-ttu-id="37220-282">Segmentos TCP enviados limite excedido</span><span class="sxs-lookup"><span data-stu-id="37220-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="37220-283">A descrição para a regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="37220-284">**Métrica**</span><span class="sxs-lookup"><span data-stu-id="37220-284">**Metric**</span></span>|<span data-ttu-id="37220-285">Segmentos TCP enviados</span><span class="sxs-lookup"><span data-stu-id="37220-285">TCP segments sent</span></span>| <span data-ttu-id="37220-286">A métrica para usar para disparar o alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="37220-287">**Condição**</span><span class="sxs-lookup"><span data-stu-id="37220-287">**Condition**</span></span>|<span data-ttu-id="37220-288">Maior que</span><span class="sxs-lookup"><span data-stu-id="37220-288">Greater than</span></span>| <span data-ttu-id="37220-289">A condição para usar ao avaliar a métrica.</span><span class="sxs-lookup"><span data-stu-id="37220-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="37220-290">**Limite**</span><span class="sxs-lookup"><span data-stu-id="37220-290">**Threshold**</span></span>|<span data-ttu-id="37220-291">100</span><span class="sxs-lookup"><span data-stu-id="37220-291">100</span></span>| <span data-ttu-id="37220-292">O valor da métrica que dispara o alerta.</span><span class="sxs-lookup"><span data-stu-id="37220-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="37220-293">Esse valor deve ser definido como um valor válido para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="37220-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="37220-294">**Período**</span><span class="sxs-lookup"><span data-stu-id="37220-294">**Period**</span></span>|<span data-ttu-id="37220-295">Nos últimos cinco minutos</span><span class="sxs-lookup"><span data-stu-id="37220-295">Over the last five minutes</span></span>| <span data-ttu-id="37220-296">Determina o período no qual procurar o limite na métrica.</span><span class="sxs-lookup"><span data-stu-id="37220-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="37220-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="37220-297">**Webhook**</span></span>|<span data-ttu-id="37220-298">[URL do webhook do aplicativo de funções]</span><span class="sxs-lookup"><span data-stu-id="37220-298">[webhook URL from function app]</span></span>| <span data-ttu-id="37220-299">A URL de webhook do aplicativo de funções que foi criada nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="37220-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="37220-300">A métrica de segmentos TCP não está habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="37220-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="37220-301">Saiba mais sobre como habilitar outras métricas visitando [Habilitar o monitoramento e o diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="37220-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="37220-302">Revise os resultados</span><span class="sxs-lookup"><span data-stu-id="37220-302">Review the results</span></span>

<span data-ttu-id="37220-303">Após os critérios para os gatilhos de alerta, uma captura de pacote será criada.</span><span class="sxs-lookup"><span data-stu-id="37220-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="37220-304">Vá para Observador de Rede e, em seguida, selecione **Captura de pacote**.</span><span class="sxs-lookup"><span data-stu-id="37220-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="37220-305">Nesta página, você pode selecionar o link de arquivo de captura de pacote para baixar a captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="37220-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![Exibir a captura de pacotes][functions14]

<span data-ttu-id="37220-307">Se o arquivo de captura for armazenado localmente, você poderá recuperá-lo entrando na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="37220-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="37220-308">Para obter instruções sobre como baixar os arquivos das contas de armazenamento do Azure, veja [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="37220-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="37220-309">Outra ferramenta que você pode usar é o [Gerenciador de armazenamento](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="37220-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="37220-310">Depois que a captura for baixada, você poderá exibi-la usando qualquer ferramenta que possa ler um arquivo **.cap**.</span><span class="sxs-lookup"><span data-stu-id="37220-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="37220-311">Os links para duas dessas ferramentas são:</span><span class="sxs-lookup"><span data-stu-id="37220-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="37220-312">Analisador de Mensagens da Microsoft</span><span class="sxs-lookup"><span data-stu-id="37220-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="37220-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="37220-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="37220-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37220-314">Next steps</span></span>

<span data-ttu-id="37220-315">Saiba como exibir as capturas de pacotes visitando [Análise da captura de pacotes com o Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="37220-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


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
