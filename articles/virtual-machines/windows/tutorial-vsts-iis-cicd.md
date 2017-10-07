---
title: aaaCreate um pipeline de CI/CD no Azure com o Team Services | Microsoft Docs
description: "Saiba como pipeline de toocreate Visual Studio Team Services para integração contínua e entrega que implanta um tooIIS de aplicativo web em uma VM do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="dcfc7-103">Criar um pipeline de integração contínua com o Visual Studio Team Services e o IIS</span><span class="sxs-lookup"><span data-stu-id="dcfc7-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="dcfc7-104">compilação de saudação tooautomate, teste e as fases de implantação de desenvolvimento de aplicativos, você pode usar uma integração contínua e pipeline de implantação (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="dcfc7-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="dcfc7-105">Neste tutorial, você cria um pipeline de CI/CD usando o Visual Studio Team Services e uma VM (máquina virtual) do Windows no Azure que executa o IIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="dcfc7-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcfc7-107">Publicar um projeto do Team Services do tooa de aplicativo da web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dcfc7-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="dcfc7-108">Criar uma definição de build disparada por confirmações de código</span><span class="sxs-lookup"><span data-stu-id="dcfc7-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="dcfc7-109">Instalar e configurar o IIS em uma máquina virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="dcfc7-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="dcfc7-110">Adicionar grupo de implantação Olá IIS instância tooa no Team Services</span><span class="sxs-lookup"><span data-stu-id="dcfc7-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="dcfc7-111">Criar uma versão de definição toopublish nova web implantar pacotes tooIIS</span><span class="sxs-lookup"><span data-stu-id="dcfc7-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="dcfc7-112">Pipeline de CI/CD de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="dcfc7-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="dcfc7-113">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="dcfc7-114">Executar `Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="dcfc7-115">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="dcfc7-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="dcfc7-116">Criar o projeto no Team Services</span><span class="sxs-lookup"><span data-stu-id="dcfc7-116">Create project in Team Services</span></span>
<span data-ttu-id="dcfc7-117">O Visual Studio Team Services facilita a colaboração e o desenvolvimento sem manter uma solução de gerenciamento de código local.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="dcfc7-118">O Team Services oferece compilação, código de testes e Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="dcfc7-119">Você pode escolher um repositório de controle de versão e o IDE que melhor se adapta a seu desenvolvimento de código.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="dcfc7-120">Para este tutorial, você pode usar uma conta gratuita toocreate um aplicativo de web ASP.NET básico e pipeline de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="dcfc7-121">Se você ainda não tem uma conta do Team Services, [crie uma](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="dcfc7-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="dcfc7-122">processo de confirmação de código do toomanage hello, criar definições e definições de versão, crie um projeto no Team Services da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="dcfc7-123">Abra o painel Team Services em um navegador da Web e escolha **Novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="dcfc7-124">Digite *myWebApp* para Olá **nome do projeto**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="dcfc7-125">Deixe todos os outros toouse de valores padrão *Git* controle de versão e *Agile* processo de item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="dcfc7-126">Escolha a opção de saudação muito**compartilhar com** *membros da equipe*, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="dcfc7-127">Quando o projeto tiver sido criado, escolha a opção de saudação muito**inicializar com um arquivo Leiame ou gitignore**, em seguida, **inicializar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="dcfc7-128">Dentro de seu novo projeto, escolha **painéis** na parte superior do hello, em seguida, selecione **aberto no Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="dcfc7-129">Criar aplicativo Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dcfc7-129">Create ASP.NET web application</span></span>
<span data-ttu-id="dcfc7-130">Na etapa anterior do hello, você criou um projeto no Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="dcfc7-131">etapa final Olá abre seu novo projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="dcfc7-132">Gerenciar as confirmações de código em Olá **Team Explorer** janela.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="dcfc7-133">Crie uma cópia local do novo projeto e crie um aplicativo Web ASP.NET de um modelo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="dcfc7-134">Selecione **Clone** toocreate um repositório git local do projeto do Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Clonar o repositório do projeto do Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="dcfc7-136">Em **Soluções**, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-136">Under **Solutions**, select **New**.</span></span>

    ![Criar a solução do aplicativo Web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="dcfc7-138">Selecione **Web** modelos e, em seguida, escolha Olá **aplicativo Web ASP.NET** modelo.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="dcfc7-139">Insira um nome para seu aplicativo, como *myWebApp*e desmarque a caixa de saudação **criar diretório para solução**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="dcfc7-140">Se a opção Olá estiver disponível, desmarque caixa Olá muito**tooproject adicionar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="dcfc7-141">Application Insights requer que você tooauthorize seu aplicativo web com o Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="dcfc7-142">tookeep-simples neste tutorial, ignore esse processo.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="dcfc7-143">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-143">Select **OK**.</span></span>
4. <span data-ttu-id="dcfc7-144">Escolha **MVC** da lista de modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="dcfc7-145">Selecione **Alterar Autenticação**, escolha **Sem Autenticação** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="dcfc7-146">Selecione **Okey** toocreate sua solução.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="dcfc7-147">Em Olá **Team Explorer** janela, escolha **alterações**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Confirmar o repositório do git alterações locais tooTeam serviços](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="dcfc7-149">Na caixa de texto de confirmação de hello, insira uma mensagem como *confirmação inicial*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="dcfc7-150">Escolha **confirmar todas as e sincronização** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="dcfc7-151">Criar definição de build</span><span class="sxs-lookup"><span data-stu-id="dcfc7-151">Create build definition</span></span>
<span data-ttu-id="dcfc7-152">No Team Services, você deve usar um toooutline de definição de compilação como seu aplicativo deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="dcfc7-153">Neste tutorial, podemos criar uma definição básica que usa nosso código-fonte, cria a solução hello, em seguida, criará web implanta pacote usamos toorun Olá web aplicativo em um servidor IIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="dcfc7-154">No seu projeto do Team Services, escolha **Build e versão** na parte superior do hello, em seguida, selecione **cria**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="dcfc7-155">Selecione **+ Nova definição**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="dcfc7-156">Escolha Olá **ASP.NET (visualização)** modelo e selecione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="dcfc7-157">Mantenha o padrão de saudação todos os valores da tarefa.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-157">Leave all hello default task values.</span></span> <span data-ttu-id="dcfc7-158">Em **obter fontes**, certifique-se de que Olá *myWebApp* repositório e *mestre* ramificação são selecionados.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Criar definição de build no projeto do Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="dcfc7-160">Em Olá **gatilhos** guia, mova o controle deslizante de saudação de **habilitar esse gatilho** muito*habilitado*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="dcfc7-161">Salvar uma nova compilação de fila e definição de compilação Olá selecionando **Salvar & fila** , em seguida, **Salvar & fila** novamente.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="dcfc7-162">Mantenha os padrões de saudação e selecione **fila**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="dcfc7-163">Inspecionar como compilação hello está agendada em um agente de host, em seguida, começa toobuild.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="dcfc7-164">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-164">hello output is similar toohello following example:</span></span>

![Compilação bem-sucedida do projeto do Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="dcfc7-166">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dcfc7-166">Create virtual machine</span></span>
<span data-ttu-id="dcfc7-167">tooprovide toorun uma plataforma seu aplicativo web ASP.NET, você precisa de uma máquina virtual do Windows que executa o IIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="dcfc7-168">Team Services usa toointeract um agente com a instância do IIS Olá conforme você confirmar que o código e compilações são disparadas.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="dcfc7-169">Criar uma VM do Windows Server 2016 usando [este exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcfc7-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="dcfc7-170">Ele leva alguns minutos para Olá script toorun e criar hello VM.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="dcfc7-171">Quando Olá VM tiver sido criado, abra a porta 80 para tráfego da web com [AzureRmNetworkSecurityRuleConfig adicionar](/powershell/module/azurerm.resources/new-azurermresourcegroup) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="dcfc7-172">tooconnect tooyour VM, obter o endereço IP público de saudação com [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="dcfc7-173">Crie uma sessão de área de trabalho remota de tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="dcfc7-174">No hello VM, abra um **do PowerShell do administrador** prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="dcfc7-175">Instale o IIS e os recursos necessários do .NET da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="dcfc7-176">Criar grupo de implantação</span><span class="sxs-lookup"><span data-stu-id="dcfc7-176">Create deployment group</span></span>
<span data-ttu-id="dcfc7-177">toopush out Olá web implantar servidor IIS do pacote toohello, definir um grupo de implantação no Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="dcfc7-178">Este grupo permite que você toospecify quais servidores são alvo de saudação de novas compilações como confirmar tooTeam código compilações e serviços são concluídas.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="dcfc7-179">No Team Services, escolha **Compilação e Versão** e selecione **Grupos de implantação**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="dcfc7-180">Escolha **Adicionar Grupo de implantação**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="dcfc7-181">Insira um nome para o grupo de saudação, como *myIIS*, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="dcfc7-182">Em Olá **registrar máquinas** seção, certifique-se de *Windows* for selecionado, marque a caixa de saudação muito**usar um token de acesso pessoal no script hello para autenticação**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="dcfc7-183">Selecione **copiar script tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="dcfc7-184">Adicionar grupo de implantação do IIS VM toohello</span><span class="sxs-lookup"><span data-stu-id="dcfc7-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="dcfc7-185">Com o grupo de implantação Olá criado, adicione cada grupo de toohello de instância do IIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="dcfc7-186">Serviços de equipe gera um script que baixa e configura um agente em Olá VM que recebe nova web implantar pacotes, em seguida, aplica tooIIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="dcfc7-187">Em Olá **do PowerShell do administrador** sessão na sua VM, cole e execute o script hello copiado do Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="dcfc7-188">Quando marcas tooconfigure solicitadas para agente hello, escolha *Y* e digite *web*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="dcfc7-189">Quando solicitado para a conta de usuário hello, pressione *retornar* tooaccept Olá padrões.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="dcfc7-190">Aguarde Olá script toofinish com uma mensagem *vstsagent.account.computername de serviço foi iniciado com êxito*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="dcfc7-191">Em Olá **grupos de implantação** página de saudação **Build e versão** menu, abra Olá *myIIS* o grupo de implantação.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="dcfc7-192">Em Olá **máquinas** , verifique se que a VM está listada.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![VM adicionado com êxito o grupo de implantação de serviços tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="dcfc7-194">Criar definição de versão</span><span class="sxs-lookup"><span data-stu-id="dcfc7-194">Create release definition</span></span>
<span data-ttu-id="dcfc7-195">toopublish suas compilações, criar uma definição de versão no Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="dcfc7-196">Essa definição é disparada automaticamente pela compilação bem-sucedida do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="dcfc7-197">Você escolha Olá toopush de grupo de implantação web implantar o pacote e define configurações de IIS apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="dcfc7-198">Escolha **Compilação e Versão** e selecione **Builds**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="dcfc7-199">Escolha a definição de compilação Olá criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="dcfc7-200">Em **concluído recentemente**, escolha a compilação mais recente do hello e selecione **versão**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="dcfc7-201">Escolha **Sim** toocreate uma definição de versão.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="dcfc7-202">Escolha Olá **vazio** modelo, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="dcfc7-203">Verifique se a definição de compilação de projeto e origem Olá são preenchidas com seu projeto.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="dcfc7-204">Selecione Olá **implantação contínua** caixa de seleção e, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="dcfc7-205">Selecione caixa de lista suspensa de saudação Avançar muito**+ adicionar tarefas** e escolha *adicionar um grupo de fase de implantação*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Adicionar definição de toorelease de tarefa no Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="dcfc7-207">Escolha **adicionar** Avançar muito**Deploy(Preview) de aplicativo Web IIS**, em seguida, selecione **fechar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="dcfc7-208">Selecione Olá **executado no grupo de implantação** tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="dcfc7-209">Para **o grupo de implantação**, selecione implantação Olá grupo criado anteriormente, como *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="dcfc7-210">Em Olá **máquina marcas** caixa, selecione **adicionar** e escolha Olá *web* marca.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Tarefa de grupo de implantação da definição de versão para o IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="dcfc7-212">Selecione Olá **implantar: implantar o aplicativo Web IIS** tarefa tooconfigure o IIS instância configurações da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="dcfc7-213">Em **nome do site**, digite *Site Padrão*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="dcfc7-214">Deixe Olá todas as outras configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="dcfc7-215">Escolha **Salvar** e selecione **OK** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="dcfc7-216">Criar uma versão e publicar</span><span class="sxs-lookup"><span data-stu-id="dcfc7-216">Create a release and publish</span></span>
<span data-ttu-id="dcfc7-217">Agora você pode enviar seu pacote de implantação Web como uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="dcfc7-218">Esta etapa se comunica com o agente de saudação em cada instância que faz parte do grupo de implantação de hello, envia Olá web implantar o pacote, em seguida, configura o aplicativo web do IIS toorun Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="dcfc7-219">Em sua definição de versão, selecione **+ Versão** e escolha **Criar Versão**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="dcfc7-220">Verificar se a compilação mais recente do hello está selecionada na lista suspensa de hello, juntamente com **implantação automatizada: após a criação de versão**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="dcfc7-221">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-221">Select **Create**.</span></span>
3. <span data-ttu-id="dcfc7-222">Uma pequena faixa aparece na parte superior de saudação da sua definição de versão, como *versão 'Versão 1' foi criado*.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="dcfc7-223">Selecione Olá versão link.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-223">Select hello release link.</span></span>
4. <span data-ttu-id="dcfc7-224">Olá abrir **Logs** guia progresso da versão toowatch hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Versão do Team Services bem-sucedida e envio do pacote de implantação Web por push](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="dcfc7-226">Após a conclusão da versão de hello, abra um navegador da web e digite Olá IIP endereço público sua VM.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="dcfc7-227">Seu aplicativo Web ASP.NET está em execução.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-227">Your ASP.NET web application is running.</span></span>

    ![Aplicativo Web ASP.NET em execução na VM do IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="dcfc7-229">Testar Olá todo CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="dcfc7-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="dcfc7-230">Com o aplicativo web em execução no IIS, tente pipeline de CI/CD inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="dcfc7-231">Depois que você fizer uma alteração no Visual Studio e seu código, uma compilação é disparado de confirmação que dispara uma versão da web atualizado implante pacote tooIIS:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="dcfc7-232">No Visual Studio, abra Olá **Solution Explorer** janela.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="dcfc7-233">Navegue tooand abrir *myWebApp | Modos de exibição | Página inicial | Cshtml*</span><span class="sxs-lookup"><span data-stu-id="dcfc7-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="dcfc7-234">Edite a linha 6 tooread:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="dcfc7-235">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-235">Save hello file.</span></span>
5. <span data-ttu-id="dcfc7-236">Olá abrir **Team Explorer** janela, selecione Olá *myWebApp* do projeto e escolha **alterações**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="dcfc7-237">Insira uma mensagem de confirmação, como *pipeline teste CI/CD*, em seguida, escolha **confirmar todos e sincronização** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="dcfc7-238">No espaço de trabalho do Team Services, uma nova compilação é disparada de confirmação de código hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="dcfc7-239">Escolha **Compilação e Versão** e selecione **Builds**.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="dcfc7-240">Escolha sua definição de compilação e selecione Olá **na fila & execução** toowatch de compilação como Olá compilar progride.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="dcfc7-241">Depois que a compilação de saudação for bem-sucedida, uma nova versão é disparada.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="dcfc7-242">Escolha **Build e versão**, em seguida, **versões** toosee Olá web implantar pacote enviado tooyour IIS VM.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="dcfc7-243">Selecione Olá **atualização** status de saudação do ícone tooupdate.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="dcfc7-244">Olá quando *ambientes* coluna mostra uma marca de seleção verde, versão Olá foi implantada com êxito tooIIS.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="dcfc7-245">toosee suas alterações aplicadas, atualize seu site do IIS em um navegador.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![Aplicativo Web ASP.NET em execução na VM do IIS pelo pipeline de CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="dcfc7-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcfc7-247">Next steps</span></span>

<span data-ttu-id="dcfc7-248">Neste tutorial, você criou um aplicativo web ASP.NET no Team Services e configurado build e versão definições toodeploy nova implantação da web tooIIS de pacotes em cada confirmação de código.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="dcfc7-249">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="dcfc7-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcfc7-250">Publicar um projeto do Team Services do tooa de aplicativo da web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dcfc7-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="dcfc7-251">Criar uma definição de build disparada por confirmações de código</span><span class="sxs-lookup"><span data-stu-id="dcfc7-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="dcfc7-252">Instalar e configurar o IIS em uma máquina virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="dcfc7-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="dcfc7-253">Adicionar grupo de implantação Olá IIS instância tooa no Team Services</span><span class="sxs-lookup"><span data-stu-id="dcfc7-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="dcfc7-254">Criar uma versão de definição toopublish nova web implantar pacotes tooIIS</span><span class="sxs-lookup"><span data-stu-id="dcfc7-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="dcfc7-255">Pipeline de CI/CD de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="dcfc7-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="dcfc7-256">Avançar toolearn tutorial do próximo toohello como toosecure um servidor web com certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="dcfc7-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcfc7-257">Proteger servidor Web com SSL</span><span class="sxs-lookup"><span data-stu-id="dcfc7-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)