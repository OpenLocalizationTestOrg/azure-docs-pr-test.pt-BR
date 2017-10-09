---
title: "implantação da máquina virtual aaaAzure com Chef | Microsoft Docs"
description: "Saiba como toouse Chef toodo automatizado implantação da máquina virtual e a configuração no Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="4c7bf-103">Automatizando a implantação de máquina virtual do Azure com o Chef</span><span class="sxs-lookup"><span data-stu-id="4c7bf-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="4c7bf-104">O Chef é uma excelente ferramenta para a entrega de automação e configurações de estado de desejado.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="4c7bf-105">Com nossa última versão de api de nuvem, Chef fornece integração perfeita com o Azure, oferecendo Olá tooprovision de capacidade e implantar os estados de configuração por meio de um único comando.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="4c7bf-106">Neste artigo, mostrarei como tooset o seu ambiente de Chef tooprovision virtuais do Azure máquinas e orientá-lo a criar uma política ou um "Livro de receitas" e, em seguida, implantar este tooan livro de receitas máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="4c7bf-107">Vamos começar!</span><span class="sxs-lookup"><span data-stu-id="4c7bf-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="4c7bf-108">Noções básicas do Chef</span><span class="sxs-lookup"><span data-stu-id="4c7bf-108">Chef basics</span></span>
<span data-ttu-id="4c7bf-109">Antes de começar, sugerimos que você revisar os conceitos básicos de saudação do Chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="4c7bf-110">Há um excelente material <a href="http://www.chef.io/chef" target="_blank">aqui</a> e recomendo que você leia rapidamente antes de tentar este passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="4c7bf-111">No entanto, será recapitular Noções básicas de saudação antes de começar.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="4c7bf-112">Olá diagrama a seguir mostra a arquitetura chefe de alto nível hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="4c7bf-113">O Chef tem três componentes principais de arquitetura: Chef Server, Chef Client (nó) e Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="4c7bf-114">Olá servidor nosso ponto de gerenciamento e há duas opções para o servidor de saudação: uma solução hospedada ou uma solução local.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="4c7bf-115">Vamos usar uma solução hospedada.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="4c7bf-116">Cliente do Chef Hello (nó) é agente Olá localizado nos servidores de saudação que está gerenciando.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="4c7bf-117">Olá estação de trabalho do Chef é nossa estação de trabalho do administrador em que criamos nossas políticas e executar os comandos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="4c7bf-118">Podemos executar Olá **knife** nossa infraestrutura de comando de saudação toomanage de estação de trabalho do Chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="4c7bf-119">Também há conceito de saudação de "Guias" e "Receitas".</span><span class="sxs-lookup"><span data-stu-id="4c7bf-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="4c7bf-120">Esses são efetivamente políticas hello, definir e aplicar tooour servidores.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="4c7bf-121">Preparando a estação de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="4c7bf-121">Preparing hello workstation</span></span>
<span data-ttu-id="4c7bf-122">Primeiro, permite que a estação de trabalho de preparação hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="4c7bf-123">Estou usando uma estação de trabalho padrão do Windows.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="4c7bf-124">Precisamos toocreate toostore um diretório de nossos arquivos de configuração e guias.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="4c7bf-125">Primeiro, crie um diretório chamado C:\chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="4c7bf-126">Em seguida, crie um segundo diretório chamado c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="4c7bf-127">Agora precisamos toodownload nosso arquivo de configurações do Azure para que chefe possa se comunicar com nossa assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="4c7bf-128">Baixe o publicar configurações usando hello PowerShell Azure [AzurePublishSettingsFile Get](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="4c7bf-129">Salvar Olá publica arquivo de configurações em C:\chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="4c7bf-130">Criando uma conta gerenciada do Chef</span><span class="sxs-lookup"><span data-stu-id="4c7bf-130">Creating a managed Chef account</span></span>
<span data-ttu-id="4c7bf-131">Inscreva-se para uma conta hospedada do Chef [aqui](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="4c7bf-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="4c7bf-132">Durante o processo de inscrição hello, você será solicitado a toocreate uma nova organização.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="4c7bf-133">Depois de criar a sua organização, baixe Olá starter kit.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="4c7bf-134">Se você receber um aviso informando que as chaves serão redefinidas, é tooproceed okey como não temos nenhuma infraestrutura existente configurada ainda.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="4c7bf-135">Este arquivo zip do kit inicial contém arquivos de configuração de organização e chaves.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="4c7bf-136">Configurando a estação de trabalho do hello Chef</span><span class="sxs-lookup"><span data-stu-id="4c7bf-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="4c7bf-137">Extrai o conteúdo de saudação do hello chef starter.zip tooC:\chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="4c7bf-138">Copie todos os arquivos em starter\chef-chef-repo\.chef tooyour c:\chef directory.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="4c7bf-139">Seu diretório agora deve ser semelhante a saudação de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="4c7bf-140">Agora você deve ter quatro arquivos, incluindo Olá arquivo de publicação do Azure na raiz de saudação do c:\chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="4c7bf-141">arquivos PEM de saudação contenham sua organização e chaves privadas de administração para comunicação enquanto o arquivo de knife Olá contém sua configuração de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="4c7bf-142">Precisaremos de arquivo de knife tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="4c7bf-143">Abra o arquivo de saudação em seu editor de preferência e modifique cookbook_path"hello" Removendo Olá /... / do caminho Olá para que ele apareça como mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="4c7bf-144">Também adicione Olá linha refletindo nome hello do Azure publica o arquivo de configurações.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="4c7bf-145">O arquivo knife. RB agora deve ser semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="4c7bf-146">Essas linhas garantirá que Knife faz referência a saudação guias diretório em c:\chef\cookbooks e também usa o nosso arquivo de configurações de publicação do Azure durante as operações do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="4c7bf-147">Olá chefe Development Kit de instalação</span><span class="sxs-lookup"><span data-stu-id="4c7bf-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="4c7bf-148">Próxima [baixar e instalar](http://downloads.getchef.com/chef-dk/windows) Olá tooset ChefDK (chefe Development Kit) a sua estação de trabalho do Chef.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="4c7bf-149">Instale no local padrão de saudação do c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="4c7bf-150">Esta instalação levará cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="4c7bf-151">Confirme que sua variável PATH contém entradas para C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="4c7bf-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="4c7bf-152">Se eles não estão lá, certifique-se que adicionar esses caminhos!</span><span class="sxs-lookup"><span data-stu-id="4c7bf-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="4c7bf-153">*Observação Olá ordem de saudação caminho é importante!*</span><span class="sxs-lookup"><span data-stu-id="4c7bf-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="4c7bf-154">Se seus caminhos opscode não estão na ordem correta hello, que você terá problemas.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="4c7bf-155">Reinicie a estação de trabalho antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="4c7bf-156">Em seguida, vamos instalar extensão do Knife Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="4c7bf-157">Isso fornece ferramentas com hello "Plug-in do Azure".</span><span class="sxs-lookup"><span data-stu-id="4c7bf-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="4c7bf-158">Execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="4c7bf-159">argumento de pré-Olá garante que você está recebendo a última versão RC Olá de saudação Knife Azure plug-in que fornece acesso toohello último conjunto de APIs.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="4c7bf-160">É provável que um número de dependências também será instalado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="4c7bf-161">tooensure que tudo está configurado corretamente, Olá executar comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="4c7bf-162">Se tudo estiver configurado corretamente, você verá uma lista de imagens do Azure disponíveis rolar.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="4c7bf-163">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-163">Congratulations.</span></span> <span data-ttu-id="4c7bf-164">Configurar a estação de trabalho Olá!</span><span class="sxs-lookup"><span data-stu-id="4c7bf-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="4c7bf-165">Criação de um Guia</span><span class="sxs-lookup"><span data-stu-id="4c7bf-165">Creating a Cookbook</span></span>
<span data-ttu-id="4c7bf-166">Um livro de receitas é usado pelo Chef toodefine um conjunto de comandos que você deseja tooexecute no seu cliente gerenciado.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="4c7bf-167">Criar um livro de receitas é simples e usamos Olá **chef gerar livro de receitas** comando toogenerate nosso modelo de livro de receitas.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="4c7bf-168">Eu chamarei meu servidor Web do Guia como eu faria com a política que implanta automaticamente o IIS.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="4c7bf-169">Em seu diretório C:\Chef execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="4c7bf-170">Isso irá gerar um conjunto de arquivos no diretório Olá C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="4c7bf-171">Agora precisamos de conjunto de saudação do toodefine de comandos gostaríamos que nossas tooexecute de cliente do Chef na máquina virtual gerenciada.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="4c7bf-172">comandos de saudação são armazenados no RB de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="4c7bf-173">Nesse arquivo, eu vai definir um conjunto de comandos que instala o IIS, o IIS é iniciado e copia um modelo arquivo toohello na pasta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="4c7bf-174">Modificar o arquivo de C:\chef\cookbooks\webserver\recipes\default.rb hello e adicione Olá linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="4c7bf-175">Salve o arquivo de saudação quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="4c7bf-176">Criando um modelo</span><span class="sxs-lookup"><span data-stu-id="4c7bf-176">Creating a template</span></span>
<span data-ttu-id="4c7bf-177">Conforme mencionado anteriormente, é preciso toogenerate um arquivo de modelo que será usado como nossa página de Default.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="4c7bf-178">Execute Olá modelo de saudação do comando toogenerate a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="4c7bf-179">Agora, navegar toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb arquivo.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="4c7bf-180">Editar arquivo hello adicionando um código de "Hello World" HTML simples e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="4c7bf-181">Carregar Olá livro de receitas toohello Chef Server</span><span class="sxs-lookup"><span data-stu-id="4c7bf-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="4c7bf-182">Nesta etapa, estamos fazendo uma cópia de saudação livro de receitas que você criou na máquina local e carregá-lo toohello o servidor do Chef hospedado.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="4c7bf-183">Uma vez carregado, Olá livro de receitas aparecerá sob Olá **política** guia.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="4c7bf-184">Implantar uma máquina virtual com o Knife Azure</span><span class="sxs-lookup"><span data-stu-id="4c7bf-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="4c7bf-185">Agora vamos implantar uma máquina virtual do Azure e aplicar hello "Webserver" livro de receitas que instalará nossa IIS página da web padrão e o serviço web.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="4c7bf-186">Em ordem toodo isso, use Olá **knife azure server criar** comando.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="4c7bf-187">Estou exemplo hello comando aparece em seguida.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="4c7bf-188">parâmetros de saudação são autoexplicativos.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="4c7bf-189">Substitua variáveis específicas e executar.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="4c7bf-190">Por meio da linha de comando Olá Olá eu estou também automatizar meu regras de filtro de rede do ponto de extremidade usando o parâmetro de pontos de extremidade tcp – hello.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="4c7bf-191">Eu abrir portas 80 e página da web do tooprovide acesso toomy 3389 e sessão RDP.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="4c7bf-192">Quando você executar o comando hello, vá toohello Azure portal e você verá sua máquina começar tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="4c7bf-193">prompt de comando Olá aparece em seguida.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="4c7bf-194">Após a conclusão da implantação hello, podemos deve ser capaz de tooconnect toohello web Services pela porta 80 tinha abrir porta hello quando nós provisionamos máquina virtual Olá Olá comando Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="4c7bf-195">Como essa máquina virtual é Olá de máquina virtual somente em meu serviço de nuvem, eu o conectarei com hello url do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="4c7bf-196">Como você pode ver, fui criativo com meu código HTML.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="4c7bf-197">Não se esqueça de que nós também pode se conectar por meio de uma sessão RDP do portal do Azure através da porta 3389 de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c7bf-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="4c7bf-198">Espero que isso tenha sido útil!</span><span class="sxs-lookup"><span data-stu-id="4c7bf-198">I hope this has been helpful!</span></span> <span data-ttu-id="4c7bf-199">Siga adiante e comece sua jornada de infraestrutura como código com o Azure hoje mesmo!</span><span class="sxs-lookup"><span data-stu-id="4c7bf-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
