---
title: Integrar logs do Azure Key Vault usando os Hubs de Eventos | Microsoft Docs
description: "Tutorial que fornece as etapas necessárias para disponibilizar os logs do Key Vault para um SIEM usando a integração de log do Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="b259d-103">Tutorial de integração de log do Azure: processar eventos do Azure Key Vault usando Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="b259d-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="b259d-104">Você pode usar a Integração de Log do Azure para recuperar eventos registrados e disponibilizá-los ao seu SIEM (sistema de informações de segurança e gerenciamento de evento).</span><span class="sxs-lookup"><span data-stu-id="b259d-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="b259d-105">Este tutorial mostra um exemplo de como a Integração de Log do Azure pode ser usada para processar os logs adquiridos por meio de Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b259d-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="b259d-106">Use este tutorial para se familiarizar com a forma como a Integração de Log do Azure e os Hubs de Eventos funcionam juntos, seguindo as etapas de exemplo e assim entender como cada etapa dá suporte à solução.</span><span class="sxs-lookup"><span data-stu-id="b259d-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="b259d-107">Em seguida, você poderá pegar o que aprendeu aqui para criar suas próprias etapas para dar suporte a requisitos exclusivos da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="b259d-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="b259d-108">As etapas e comandos neste tutorial não devem ser copiados e colados.</span><span class="sxs-lookup"><span data-stu-id="b259d-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="b259d-109">Elas são apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="b259d-109">They're examples only.</span></span> <span data-ttu-id="b259d-110">Não use os comandos do PowerShell "no estado em que se encontram" em seu ambiente dinâmico.</span><span class="sxs-lookup"><span data-stu-id="b259d-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="b259d-111">Você deve personalizá-los com base em seu ambiente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b259d-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="b259d-112">Este tutorial orienta você no processo de fazer com que a atividade do Azure Key Vault seja registrada em um hub de eventos e disponibilizada como arquivos JSON para o seu sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="b259d-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="b259d-113">Em seguida, você pode configurar o sistema SIEM para processar os arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="b259d-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="b259d-114">A maioria das etapas deste tutorial envolve a configuração de cofres de chaves, contas de armazenamento e hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="b259d-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="b259d-115">As etapas específicas da integração de log do Azure estão no final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b259d-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="b259d-116">Não execute estas etapas em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b259d-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="b259d-117">Elas servem apenas para um ambiente de laboratório.</span><span class="sxs-lookup"><span data-stu-id="b259d-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="b259d-118">Personalize-as antes de usá-las em produção.</span><span class="sxs-lookup"><span data-stu-id="b259d-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="b259d-119">As informações fornecidas ao longo do processo ajudam você a entender as razões por trás de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="b259d-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="b259d-120">Links para outros artigos fornecem mais detalhes sobre determinados tópicos.</span><span class="sxs-lookup"><span data-stu-id="b259d-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="b259d-121">Para obter mais informações sobre os serviços que este tutorial menciona, consulte:</span><span class="sxs-lookup"><span data-stu-id="b259d-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="b259d-122">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="b259d-123">Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="b259d-124">Integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="b259d-125">Configuração inicial</span><span class="sxs-lookup"><span data-stu-id="b259d-125">Initial setup</span></span>

<span data-ttu-id="b259d-126">Antes de concluir as etapas neste artigo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="b259d-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="b259d-127">Uma assinatura do Azure e uma conta nessa assinatura com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="b259d-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="b259d-128">Se você não tem uma assinatura, você pode criar um [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b259d-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="b259d-129">Um sistema com acesso à Internet que atenda aos requisitos para a instalação da integração de log do Azure.</span><span class="sxs-lookup"><span data-stu-id="b259d-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="b259d-130">O sistema pode estar em um serviço de nuvem ou hospedado localmente.</span><span class="sxs-lookup"><span data-stu-id="b259d-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="b259d-131">[Integração de log do Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalada.</span><span class="sxs-lookup"><span data-stu-id="b259d-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="b259d-132">Para instalá-la:</span><span class="sxs-lookup"><span data-stu-id="b259d-132">To install it:</span></span>

   <span data-ttu-id="b259d-133">a.</span><span class="sxs-lookup"><span data-stu-id="b259d-133">a.</span></span> <span data-ttu-id="b259d-134">Use a Área de Trabalho Remota para conectar-se ao sistema mencionado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="b259d-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="b259d-135">b.</span><span class="sxs-lookup"><span data-stu-id="b259d-135">b.</span></span> <span data-ttu-id="b259d-136">Copie o instalador da integração de log do Azure no sistema.</span><span class="sxs-lookup"><span data-stu-id="b259d-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="b259d-137">Você pode [baixar os arquivos de instalação](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="b259d-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="b259d-138">c.</span><span class="sxs-lookup"><span data-stu-id="b259d-138">c.</span></span> <span data-ttu-id="b259d-139">Inicie o instalador e aceite os Termos de Licença para Software Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b259d-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="b259d-140">d.</span><span class="sxs-lookup"><span data-stu-id="b259d-140">d.</span></span> <span data-ttu-id="b259d-141">Se você vai fornecer informações de telemetria, deixe a caixa de seleção marcada.</span><span class="sxs-lookup"><span data-stu-id="b259d-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="b259d-142">Se você preferir não enviar informações de uso à Microsoft, desmarque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="b259d-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="b259d-143">Para obter mais informações sobre a integração de log do Azure e como instalá-la, consulte [Integração de Log do Azure com log de Diagnóstico do Azure e Encaminhamento de Eventos do Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b259d-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="b259d-144">A versão mais recente do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b259d-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="b259d-145">Se você tem o Windows Server 2016 instalado, você tem, no mínimo, o PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="b259d-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="b259d-146">Se estiver usando outra versão do Windows Server, pode ser que você tenha uma versão anterior do PowerShell instalada.</span><span class="sxs-lookup"><span data-stu-id="b259d-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="b259d-147">Você pode verificar a versão digitando ```get-host``` em uma janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b259d-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="b259d-148">Se você não tiver o PowerShell 5.0 instalado, você poderá [baixá-lo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="b259d-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="b259d-149">Depois de ter pelo menos o PowerShell 5.0, você continuar para instalar a versão mais recente:</span><span class="sxs-lookup"><span data-stu-id="b259d-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="b259d-150">a.</span><span class="sxs-lookup"><span data-stu-id="b259d-150">a.</span></span> <span data-ttu-id="b259d-151">Em uma janela do PowerShell, insira o comando ```Install-Module Azure```.</span><span class="sxs-lookup"><span data-stu-id="b259d-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="b259d-152">Conclua as etapas de instalação.</span><span class="sxs-lookup"><span data-stu-id="b259d-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="b259d-153">b.</span><span class="sxs-lookup"><span data-stu-id="b259d-153">b.</span></span> <span data-ttu-id="b259d-154">Insira o comando ```Install-Module AzureRM```.</span><span class="sxs-lookup"><span data-stu-id="b259d-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="b259d-155">Conclua as etapas de instalação.</span><span class="sxs-lookup"><span data-stu-id="b259d-155">Complete the installation steps.</span></span>

   <span data-ttu-id="b259d-156">Para obter mais informações, consulte [Instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="b259d-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="b259d-157">Criar elementos de suporte da infraestrutura</span><span class="sxs-lookup"><span data-stu-id="b259d-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="b259d-158">Abra uma janela do PowerShell com privilégios elevados e acesse **c:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="b259d-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="b259d-159">Importe os cmdlets do AzLog executando o script LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="b259d-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="b259d-160">Insira o comando `.\LoadAzLogModule.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b259d-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="b259d-161">(Observe o ".\" nesse comando.) Você deverá ver algo assim:</span><span class="sxs-lookup"><span data-stu-id="b259d-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Lista de módulos carregados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="b259d-163">Insira o comando `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="b259d-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="b259d-164">Na janela de logon, insira as informações de credenciais da assinatura que você usará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b259d-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b259d-165">Se esta for a primeira vez que você está fazendo logon no Azure neste computador, você verá uma mensagem sobre permitir que a Microsoft colete dados de uso do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b259d-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="b259d-166">É recomendável que você habilite essa coleta de dados porque ela será usada para melhorar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b259d-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="b259d-167">Após a autenticação bem-sucedida, você estará conectado e verá as informações da seguinte captura de tela.</span><span class="sxs-lookup"><span data-stu-id="b259d-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="b259d-168">Anote a ID da assinatura e o nome da assinatura, porque eles são necessários para concluir etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="b259d-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![Janela do PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="b259d-170">Crie variáveis para armazenar valores que serão usados posteriormente.</span><span class="sxs-lookup"><span data-stu-id="b259d-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="b259d-171">Insira cada uma das seguintes opções nas linhas do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b259d-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="b259d-172">Talvez seja necessário ajustar os valores de acordo com seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="b259d-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="b259d-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (O nome da sua assinatura pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="b259d-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="b259d-174">Você pode ver isso como parte da saída do comando anterior.)</span><span class="sxs-lookup"><span data-stu-id="b259d-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="b259d-175">```$location = 'West US'``` (Essa variável será usada para passar o local em que os recursos devem ser criados.</span><span class="sxs-lookup"><span data-stu-id="b259d-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="b259d-176">Você pode alterar essa variável para qualquer outro local da sua escolha.)</span><span class="sxs-lookup"><span data-stu-id="b259d-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="b259d-177">``` $name = 'azlogtest' + $random``` (O nome pode ser qualquer um, contanto que tenha apenas letras minúsculas e números).</span><span class="sxs-lookup"><span data-stu-id="b259d-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="b259d-178">``` $storageName = $name``` (Essa variável será usada para o nome da conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="b259d-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="b259d-179">```$rgname = $name ``` (Essa variável será usada para o nome do grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="b259d-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="b259d-180">``` $eventHubNameSpaceName = $name``` (Esse é o nome do namespace do hub de eventos).</span><span class="sxs-lookup"><span data-stu-id="b259d-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="b259d-181">Especifique a assinatura com a qual você trabalhará:</span><span class="sxs-lookup"><span data-stu-id="b259d-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="b259d-182">Crie um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b259d-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="b259d-183">Se inserir `$rg` neste momento, você verá uma saída semelhante à essa captura de tela:</span><span class="sxs-lookup"><span data-stu-id="b259d-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Saída após a criação de um grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="b259d-185">Crie uma conta de armazenamento que será usada para manter controle sobre as informações de estado:</span><span class="sxs-lookup"><span data-stu-id="b259d-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="b259d-186">Crie o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="b259d-186">Create the event hub namespace.</span></span> <span data-ttu-id="b259d-187">Isso é necessário para criar um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="b259d-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="b259d-188">Obtenha a ID da regra que será usada com o provedor de informações:</span><span class="sxs-lookup"><span data-stu-id="b259d-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="b259d-189">Obtenha todos os possíveis locais do Azure e adicione os nomes a uma variável que possa ser usada em uma etapa posterior:</span><span class="sxs-lookup"><span data-stu-id="b259d-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="b259d-190">a.</span><span class="sxs-lookup"><span data-stu-id="b259d-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="b259d-191">b.</span><span class="sxs-lookup"><span data-stu-id="b259d-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="b259d-192">Se você inserir `$locations` nesse momento, verá os nomes de local sem as informações adicionais retornadas pelo Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="b259d-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="b259d-193">Criar um perfil de log do Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b259d-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="b259d-194">Para obter mais informações sobre o perfil de log do Azure, consulte [Visão geral do Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b259d-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b259d-195">Você poderá obter uma mensagem de erro ao tentar criar um perfil de log.</span><span class="sxs-lookup"><span data-stu-id="b259d-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="b259d-196">Em seguida, você poderá examinar a documentação para o Get-AzureRmLogProfile e o Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="b259d-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="b259d-197">Se você executar o Get-AzureRmLogProfile, verá as informações sobre o perfil de log.</span><span class="sxs-lookup"><span data-stu-id="b259d-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="b259d-198">Você pode excluir o perfil de log existente inserindo o comando ```Remove-AzureRmLogProfile -name 'Log Profile Name' ```.</span><span class="sxs-lookup"><span data-stu-id="b259d-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Erro de perfil do Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="b259d-200">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="b259d-200">Create a key vault</span></span>

1. <span data-ttu-id="b259d-201">Crie o cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="b259d-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="b259d-202">Configure o registro em log para o cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="b259d-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="b259d-203">Gerar atividade de log</span><span class="sxs-lookup"><span data-stu-id="b259d-203">Generate log activity</span></span>

<span data-ttu-id="b259d-204">As solicitações precisam ser enviados para o Key Vault para gerar a atividade de log.</span><span class="sxs-lookup"><span data-stu-id="b259d-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="b259d-205">Ações como geração de chaves, armazenamento de segredos ou leitura de segredos do Key Vault criarão entradas de log.</span><span class="sxs-lookup"><span data-stu-id="b259d-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="b259d-206">Exibir as chaves de armazenamento atuais:</span><span class="sxs-lookup"><span data-stu-id="b259d-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="b259d-207">Gerar uma nova **key2**:</span><span class="sxs-lookup"><span data-stu-id="b259d-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="b259d-208">Exibir as chaves novamente e ver que **key2** tem um valor diferente:</span><span class="sxs-lookup"><span data-stu-id="b259d-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="b259d-209">Definir e ler um segredo para gerar entradas de log adicionais:</span><span class="sxs-lookup"><span data-stu-id="b259d-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="b259d-210">a.</span><span class="sxs-lookup"><span data-stu-id="b259d-210">a.</span></span> <span data-ttu-id="b259d-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="b259d-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segredo retornado](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="b259d-213">Configurar a integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="b259d-214">Agora que você configurou todos os elementos necessários para que o Key Vault registre em log em um hub de eventos, você precisa configurar a integração de log do Azure:</span><span class="sxs-lookup"><span data-stu-id="b259d-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="b259d-215">Execute o comando AzLog para cada hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="b259d-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="b259d-216">Após um minuto ou mais de execução dos dois últimos comandos, você verá os arquivos JSON sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="b259d-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="b259d-217">Você pode confirmar isso pelo monitoramento do diretório **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="b259d-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b259d-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b259d-218">Next steps</span></span>

- [<span data-ttu-id="b259d-219">Perguntas frequentes sobre a integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="b259d-220">Introdução à integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="b259d-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="b259d-221">Integrar logs de recursos do Azure nos seus sistemas SIEM</span><span class="sxs-lookup"><span data-stu-id="b259d-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
