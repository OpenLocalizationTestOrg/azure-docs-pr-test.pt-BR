---
title: logs de aaaIntegrate do Cofre de chaves do Azure usando os Hubs de eventos | Microsoft Docs
description: "Tutorial que fornece as etapas necessárias de saudação toomake Cofre de chaves logs disponível tooa SIEM usando a integração de Log do Azure"
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
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="aa4e0-103">Tutorial de integração de log do Azure: processar eventos do Azure Key Vault usando Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="aa4e0-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="aa4e0-104">Você pode usar a integração do Azure Log tooretrieve registrado eventos e torná-los disponíveis tooyour segurança informações e eventos (SIEM) sistema de gerenciamento de.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="aa4e0-105">Este tutorial mostra um exemplo de como a integração do Azure Log pode ser usado tooprocess logs adquiridas por meio de Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="aa4e0-106">Use este tutorial tooget familiarizado com como o trabalho de integração de Log do Azure e Hubs de eventos juntos seguindo Olá etapas de exemplo e entender como cada etapa dá suporte à solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="aa4e0-107">Em seguida, você pode executar o que você aprendeu aqui toocreate toosupport suas próprias etapas requisitos exclusivos da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="aa4e0-108">etapas de saudação e os comandos neste tutorial não são toobe pretendido copiados e colados.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="aa4e0-109">Elas são apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-109">They're examples only.</span></span> <span data-ttu-id="aa4e0-110">Não use comandos do PowerShell hello "como está" em seu ambiente dinâmico.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="aa4e0-111">Você deve personalizá-los com base em seu ambiente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="aa4e0-112">Este tutorial orienta você pelo processo de saudação de colocar o hub de eventos de tooan conectado de atividade de Cofre de chaves do Azure e torná-lo disponível como JSON arquivos tooyour SIEM sistema.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="aa4e0-113">Você pode configurar os arquivos JSON de saudação do SIEM sistema tooprocess.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="aa4e0-114">A maioria das etapas neste tutorial Olá envolve configurar cofres de chaves, contas de armazenamento e hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="aa4e0-115">as etapas específicas de integração do Azure Log Olá são final Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="aa4e0-116">Não execute estas etapas em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="aa4e0-117">Elas servem apenas para um ambiente de laboratório.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="aa4e0-118">Você deve personalizar as etapas de saudação antes de usá-los em produção.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="aa4e0-119">As informações fornecidas ao longo de ajuda de maneira Olá que entender motivos Olá atrás de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="aa4e0-120">Artigos de tooother links fornecem mais detalhes sobre determinados tópicos.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="aa4e0-121">Para obter mais informações sobre os serviços de saudação mencionadas neste tutorial, consulte:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="aa4e0-122">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="aa4e0-123">Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="aa4e0-124">Integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="aa4e0-125">Configuração inicial</span><span class="sxs-lookup"><span data-stu-id="aa4e0-125">Initial setup</span></span>

<span data-ttu-id="aa4e0-126">Antes de concluir as etapas de saudação neste artigo, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="aa4e0-127">Uma assinatura do Azure e uma conta nessa assinatura com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="aa4e0-128">Se você não tem uma assinatura, você pode criar um [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="aa4e0-129">Um sistema com toohello de acesso à internet que atenda aos requisitos de saudação para a integração do Azure Log de instalação.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="aa4e0-130">sistema Olá pode estar em um serviço de nuvem ou hospedado no local.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="aa4e0-131">[Integração de log do Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalada.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="aa4e0-132">tooinstall-lo:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-132">tooinstall it:</span></span>

   <span data-ttu-id="aa4e0-133">a.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-133">a.</span></span> <span data-ttu-id="aa4e0-134">Use a área de trabalho remota tooconnect toohello sistema mencionado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="aa4e0-135">b.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-135">b.</span></span> <span data-ttu-id="aa4e0-136">Copie o sistema de toohello de instalador de integração do Azure Log hello.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="aa4e0-137">Você pode [baixar arquivos de instalação Olá](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="aa4e0-138">c.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-138">c.</span></span> <span data-ttu-id="aa4e0-139">Iniciar o instalador hello e aceite Olá Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="aa4e0-140">d.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-140">d.</span></span> <span data-ttu-id="aa4e0-141">Se você fornecerá informações de telemetria, deixe a caixa de seleção hello.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="aa4e0-142">Se você preferir enviar não tooMicrosoft de informações de uso, desmarque a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="aa4e0-143">Para obter mais informações sobre a integração do Log do Azure e como tooinstall, consulte [integração de Log do Azure com o log de diagnóstico do Azure e o encaminhamento de eventos do Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="aa4e0-144">versão mais recente do PowerShell Hello.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="aa4e0-145">Se você tem o Windows Server 2016 instalado, você tem, no mínimo, o PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="aa4e0-146">Se estiver usando outra versão do Windows Server, pode ser que você tenha uma versão anterior do PowerShell instalada.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="aa4e0-147">Você pode verificar a versão de hello inserindo ```get-host``` em uma janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="aa4e0-148">Se você não tiver o PowerShell 5.0 instalado, você poderá [baixá-lo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="aa4e0-149">Depois de ter pelo menos PowerShell 5.0, você pode continuar a versão mais recente do tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="aa4e0-150">a.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-150">a.</span></span> <span data-ttu-id="aa4e0-151">Em uma janela do PowerShell, digite Olá ```Install-Module Azure``` comando.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="aa4e0-152">Conclua as etapas de instalação hello.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="aa4e0-153">b.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-153">b.</span></span> <span data-ttu-id="aa4e0-154">Digite hello ```Install-Module AzureRM``` comando.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="aa4e0-155">Conclua as etapas de instalação hello.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="aa4e0-156">Para obter mais informações, consulte [Instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="aa4e0-157">Criar elementos de suporte da infraestrutura</span><span class="sxs-lookup"><span data-stu-id="aa4e0-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="aa4e0-158">Abra uma janela do PowerShell com privilégios elevados e vá muito**C:\Program Files\Microsoft Azure Log integração**.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="aa4e0-159">Importe Olá AzLog cmdlets executando o script hello LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="aa4e0-160">Digite hello `.\LoadAzLogModule.ps1` comando.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="aa4e0-161">(Olá aviso ". \" nesse comando.) Você deverá ver algo assim:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Lista de módulos carregados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="aa4e0-163">Digite hello `Login-AzureRmAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="aa4e0-164">Na janela de logon hello, insira as informações de credencial de Olá para assinatura de saudação que você usará para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="aa4e0-165">Se isso for Olá pela primeira vez que você estiver fazendo o logon em tooAzure desta máquina, você verá uma mensagem sobre a permissão de dados de uso do Microsoft toocollect do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="aa4e0-166">É recomendável que você habilite a coleta de dados porque ele será usado tooimprove PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="aa4e0-167">Após a autenticação bem-sucedida, você está conectado e ver informações Olá Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="aa4e0-168">Anote o nome da assinatura Olá ID e a assinatura, porque eles são necessários toocomplete etapas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Janela do PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="aa4e0-170">Crie variáveis toostore valores que serão usados posteriormente.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="aa4e0-171">Insira cada Olá PowerShell linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="aa4e0-172">Talvez seja necessário tooadjust Olá valores toomatch seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="aa4e0-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (O nome da sua assinatura pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="aa4e0-174">Você poderá ver isso como parte da saída de saudação do comando anterior hello.)</span><span class="sxs-lookup"><span data-stu-id="aa4e0-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="aa4e0-175">```$location = 'West US'```(Essa variável será local de saudação toopass usado onde recursos devem ser criados.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="aa4e0-176">Você pode alterar essa variável toobe qualquer local de sua escolha.)</span><span class="sxs-lookup"><span data-stu-id="aa4e0-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="aa4e0-177">``` $name = 'azlogtest' + $random```(Olá nome pode ser qualquer, mas ele deve conter apenas letras minúsculas e números).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="aa4e0-178">``` $storageName = $name```(Essa variável será usada para o nome de conta de armazenamento hello.)</span><span class="sxs-lookup"><span data-stu-id="aa4e0-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="aa4e0-179">```$rgname = $name ```(Essa variável será usada para o nome do grupo de recursos hello.)</span><span class="sxs-lookup"><span data-stu-id="aa4e0-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="aa4e0-180">``` $eventHubNameSpaceName = $name```(Esse é o nome de saudação do namespace de hub de eventos de saudação).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="aa4e0-181">Especifique a assinatura de saudação que você estará trabalhando com:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="aa4e0-182">Crie um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="aa4e0-183">Se você inserir `$rg` neste ponto, você deve ver a saída de tela de toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Saída após a criação de um grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="aa4e0-185">Crie uma conta de armazenamento que será usado tookeep rastrear informações de estado:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="aa4e0-186">Crie um namespace de hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-186">Create hello event hub namespace.</span></span> <span data-ttu-id="aa4e0-187">Isso é necessário toocreate um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="aa4e0-188">Obter Olá ID da regra que será usado com o provedor de insights hello:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="aa4e0-189">Obter todos os possíveis locais do Azure e adicione a variável de tooa de nomes de saudação que pode ser usado em uma etapa posterior:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="aa4e0-190">a.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="aa4e0-191">b.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="aa4e0-192">Se você inserir `$locations` neste ponto, você verá nomes de local de saudação sem informações adicionais de saudação retornadas por Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="aa4e0-193">Criar um perfil de log do Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="aa4e0-194">Para obter mais informações sobre Olá perfil de registro do Azure, consulte [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e0-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aa4e0-195">Você pode obter uma mensagem de erro ao tentar toocreate um perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="aa4e0-196">Em seguida, você pode revisar documentação Olá para Get-AzureRmLogProfile e remover AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="aa4e0-197">Se você executar Get-AzureRmLogProfile, você pode ver informações sobre o perfil do log de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="aa4e0-198">Você pode excluir o perfil de log existente da saudação inserindo Olá ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Erro de perfil do Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="aa4e0-200">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="aa4e0-200">Create a key vault</span></span>

1. <span data-ttu-id="aa4e0-201">Crie Cofre de chaves de saudação:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="aa4e0-202">Configure o log para o Cofre de chaves hello:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="aa4e0-203">Gerar atividade de log</span><span class="sxs-lookup"><span data-stu-id="aa4e0-203">Generate log activity</span></span>

<span data-ttu-id="aa4e0-204">Solicitações necessário toobe enviado tooKey atividade de log de toogenerate do cofre.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="aa4e0-205">Ações como geração de chaves, armazenamento de segredos ou leitura de segredos do Key Vault criarão entradas de log.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="aa4e0-206">Exibir chaves de armazenamento atual da saudação:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="aa4e0-207">Gerar uma nova **key2**:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="aa4e0-208">Exibir chaves Olá novamente e veja que **key2** contém um valor diferente:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="aa4e0-209">Definir e ler um segredo toogenerate entradas de log adicionais:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="aa4e0-210">a.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-210">a.</span></span> <span data-ttu-id="aa4e0-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Segredo retornado](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="aa4e0-213">Configurar a integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="aa4e0-214">Agora que você configurou o hub de eventos do hello elementos necessários toohave registro de Cofre de chaves tooan todos, é necessário tooconfigure integração do Azure Log:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="aa4e0-215">Execute o comando de AzLog de saudação para cada hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="aa4e0-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="aa4e0-216">Após um minuto ou de execução Olá dois últimos comandos, você deve ver os arquivos JSON que está sendo gerados.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="aa4e0-217">Você pode confirmar que monitoramento Olá diretório **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="aa4e0-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4e0-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa4e0-218">Next steps</span></span>

- [<span data-ttu-id="aa4e0-219">Perguntas frequentes sobre a integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="aa4e0-220">Introdução à integração de log do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4e0-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="aa4e0-221">Integrar logs de recursos do Azure nos seus sistemas SIEM</span><span class="sxs-lookup"><span data-stu-id="aa4e0-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
