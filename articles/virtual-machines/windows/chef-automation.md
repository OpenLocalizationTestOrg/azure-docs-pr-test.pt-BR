---
title: "Implantação de máquina virtual do Azure com o Chef | Microsoft Docs"
description: "Saiba como usar o Chef para realizar implantação e configuração automatizadas da máquina virtual no Microsoft Azure"
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
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="5c2d3-103">Automatizando a implantação de máquina virtual do Azure com o Chef</span><span class="sxs-lookup"><span data-stu-id="5c2d3-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5c2d3-104">O Chef é uma excelente ferramenta para a entrega de automação e configurações de estado de desejado.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="5c2d3-105">Com nossa versão mais recente da api de nuvem, o Chef fornece integração perfeita com o Azure, dando a você a capacidade de provisionar e implantar os estados de configuração por meio de um único comando.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="5c2d3-106">Neste artigo, mostrarei a você como configurar o ambiente do Chef para provisionar máquinas virtuais do Azure e a criar uma política ou um "Guia" e, em seguida, implantar esse guia em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="5c2d3-107">Vamos começar!</span><span class="sxs-lookup"><span data-stu-id="5c2d3-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="5c2d3-108">Noções básicas do Chef</span><span class="sxs-lookup"><span data-stu-id="5c2d3-108">Chef basics</span></span>
<span data-ttu-id="5c2d3-109">Antes de começar, sugiro que você leia os conceitos básicos do Chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="5c2d3-110">Há um excelente material <a href="http://www.chef.io/chef" target="_blank">aqui</a> e recomendo que você leia rapidamente antes de tentar este passo-a-passo.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="5c2d3-111">No entanto, irei recapitular os conceitos básicos antes de começarmos.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="5c2d3-112">O diagrama a seguir ilustra a arquitetura de alto nível do Chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="5c2d3-113">O Chef tem três componentes principais de arquitetura: Chef Server, Chef Client (nó) e Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="5c2d3-114">O Chef Server é o nosso ponto de gerenciamento e há duas opções para o Chef Server: uma solução hospedada ou uma solução local.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="5c2d3-115">Vamos usar uma solução hospedada.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="5c2d3-116">O Chef Client (nó) é o agente que reside nos servidores que você está gerenciando.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="5c2d3-117">O Chef Workstation é nossa estação de trabalho administrativa onde criamos nossas políticas e executamos os comandos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="5c2d3-118">Executamos o comando **knife** do Chef Workstation para gerenciar nossa infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="5c2d3-119">Há também o conceito de “Guias" e "Receitas".</span><span class="sxs-lookup"><span data-stu-id="5c2d3-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="5c2d3-120">Estas são efetivamente as políticas que definimos e aplicamos aos nossos servidores.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="5c2d3-121">Preparando a estação de trabalho</span><span class="sxs-lookup"><span data-stu-id="5c2d3-121">Preparing the workstation</span></span>
<span data-ttu-id="5c2d3-122">Primeiro, vamos preparar a estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-122">First, lets prep the workstation.</span></span> <span data-ttu-id="5c2d3-123">Estou usando uma estação de trabalho padrão do Windows.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="5c2d3-124">É necessário criar um diretório para armazenar os arquivos de configuração e guias.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="5c2d3-125">Primeiro, crie um diretório chamado C:\chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="5c2d3-126">Em seguida, crie um segundo diretório chamado c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="5c2d3-127">Agora, é necessário baixar o arquivo de configurações do Azure para que o Chef possa se comunicar com a nossa assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="5c2d3-128">Baixe as configurações de publicação usando o comando [AzurePublishSettingsFile Get](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) do PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="5c2d3-129">Salve o arquivo de configurações de publicação em C:\chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="5c2d3-130">Criando uma conta gerenciada do Chef</span><span class="sxs-lookup"><span data-stu-id="5c2d3-130">Creating a managed Chef account</span></span>
<span data-ttu-id="5c2d3-131">Inscreva-se para uma conta hospedada do Chef [aqui](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="5c2d3-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="5c2d3-132">Durante o processo de inscrição, você será solicitado a criar uma nova organização.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="5c2d3-133">Depois de criar sua organização, baixe o kit inicial.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="5c2d3-134">Se você receber um aviso informando que as suas chaves serão redefinidas, está tudo bem prosseguir, visto que não temos nenhuma infraestrutura existente configurada ainda.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="5c2d3-135">Este arquivo zip do kit inicial contém arquivos de configuração de organização e chaves.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="5c2d3-136">Configurando o Chef Workstation</span><span class="sxs-lookup"><span data-stu-id="5c2d3-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="5c2d3-137">Extraia o conteúdo do chef-starter.zip em C:\chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="5c2d3-138">Copie todos os arquivos em chef-starter\chef-repo\.chef no seu diretório c:\chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="5c2d3-139">O diretório agora deve ser semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="5c2d3-140">Agora você deve ter quatro arquivos, incluindo o arquivo de publicação do Azure na raiz do c:\chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="5c2d3-141">Os arquivos PEM contêm as chaves particulares de organização e administração para comunicação enquanto o arquivo knife.rb contém a configuração knife.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="5c2d3-142">Será necessário editar o arquivo knife.rb.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="5c2d3-143">Abra o arquivo no seu editor de escolha e modifique o "cookbook_path" removendo o /../ do caminho para que ele se pareça como mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="5c2d3-144">Além disso, adicione a seguinte linha para refletir o nome do seu arquivo de publicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="5c2d3-145">O arquivo knife.rb agora deve ser semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="5c2d3-146">Essas linhas garantirão as referências knife em nosso diretório de guias c:\chef\cookbooks e também usam o arquivo Configurações de Publicação do Azure durante as operações do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="5c2d3-147">Instale o Kit de desenvolvimento Chef</span><span class="sxs-lookup"><span data-stu-id="5c2d3-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="5c2d3-148">Em seguida [baixe e instale](http://downloads.getchef.com/chef-dk/windows) o ChefDK (Chef Development Kit) para configurar seu Chef Workstation.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="5c2d3-149">Instale-o no local padrão c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="5c2d3-150">Esta instalação levará cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="5c2d3-151">Confirme que sua variável PATH contém entradas para C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="5c2d3-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="5c2d3-152">Se eles não estão lá, certifique-se que adicionar esses caminhos!</span><span class="sxs-lookup"><span data-stu-id="5c2d3-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="5c2d3-153">*OBSERVE QUE A ORDEM DO CAMINHO É IMPORTANTE!*</span><span class="sxs-lookup"><span data-stu-id="5c2d3-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="5c2d3-154">Se seus caminhos opscode não estiverem na ordem correta, você terá problemas.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="5c2d3-155">Reinicie a estação de trabalho antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="5c2d3-156">Em seguida, instalaremos a extensão do Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="5c2d3-157">Isso fornece Knife com o "plug-in Azure".</span><span class="sxs-lookup"><span data-stu-id="5c2d3-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="5c2d3-158">Execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="5c2d3-159">O argumento –pre garante que você está recebendo a última versão do RC do Plug-in Knife Azure, que fornece acesso ao conjunto mais recente de APIs.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="5c2d3-160">É provável que um número de dependências também seja instalado ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="5c2d3-161">Para garantir que tudo esteja configurado corretamente, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="5c2d3-162">Se tudo estiver configurado corretamente, você verá uma lista de imagens do Azure disponíveis rolar.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="5c2d3-163">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-163">Congratulations.</span></span> <span data-ttu-id="5c2d3-164">O Workstation está configurado!</span><span class="sxs-lookup"><span data-stu-id="5c2d3-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="5c2d3-165">Criação de um Guia</span><span class="sxs-lookup"><span data-stu-id="5c2d3-165">Creating a Cookbook</span></span>
<span data-ttu-id="5c2d3-166">Um Guia é usado pelo Chef para definir um conjunto de comandos que você deseja executar no cliente gerenciado.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="5c2d3-167">Criar um Guia é muito simples e direto e usamos o comando **chef generate cookbook** para gerar nosso modelo de Guia.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="5c2d3-168">Eu chamarei meu servidor Web do Guia como eu faria com a política que implanta automaticamente o IIS.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="5c2d3-169">No diretório C:\Chef, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="5c2d3-170">Isso irá gerar um conjunto de arquivos no diretório C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="5c2d3-171">Agora, precisamos definir o conjunto de comandos que gostaríamos que nosso Chef Client executasse em nossa máquina virtual gerenciada.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="5c2d3-172">Os comandos são armazenados no arquivo default.rb.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="5c2d3-173">Nesse arquivo, estarei definindo um conjunto de comandos que instala o IIS, inicia o IIS e copia um arquivo de modelo para a pasta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="5c2d3-174">Modifique o arquivo C:\chef\cookbooks\webserver\recipes\default.rb e adicione as linhas a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

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

<span data-ttu-id="5c2d3-175">Quando terminar, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="5c2d3-176">Criando um modelo</span><span class="sxs-lookup"><span data-stu-id="5c2d3-176">Creating a template</span></span>
<span data-ttu-id="5c2d3-177">Conforme mencionado anteriormente, é necessário gerar um arquivo de modelo que será usado como nossa página default.html.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="5c2d3-178">Execute o comando a seguir para gerar o modelo.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="5c2d3-179">Agora, navegue para o arquivo C:\chef\cookbooks\webserver\templates\default\Default.htm.erb.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="5c2d3-180">Edite o arquivo adicionando um código HTML simples "Hello World" e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="5c2d3-181">Carregue o Guia no Chef Server</span><span class="sxs-lookup"><span data-stu-id="5c2d3-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="5c2d3-182">Nesta etapa, estamos fazendo uma cópia do Guia que criamos na máquina local e carregando no servidor hospedado do Chef.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="5c2d3-183">Uma vez carregado, o Guia aparecerá sob a guia **Política** .</span><span class="sxs-lookup"><span data-stu-id="5c2d3-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="5c2d3-184">Implantar uma máquina virtual com o Knife Azure</span><span class="sxs-lookup"><span data-stu-id="5c2d3-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="5c2d3-185">Agora podemos implantar uma máquina virtual do Azure e aplicar o Guia "Webserver", que instalará nossa página da Web padrão e o serviço Web do IIS.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="5c2d3-186">Para fazer isso, use o comando **knife azure server create** .</span><span class="sxs-lookup"><span data-stu-id="5c2d3-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="5c2d3-187">Veja a seguir, um exemplo do comando.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="5c2d3-188">Os parâmetros são autoexplicativos.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="5c2d3-189">Substitua variáveis específicas e executar.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="5c2d3-190">Por meio da linha de comando, também estou automatizando minhas regras de filtro de rede do ponto de extremidade usando o parâmetro –tcp-endpoints.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="5c2d3-191">Eu abri as portas 80 e 3389 para fornecer acesso a minha página da Web e à sessão RDP.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="5c2d3-192">Depois de executar o comando, vá para o portal do Azure e você verá o início do provisionamento de seu computador.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="5c2d3-193">O prompt de comando aparecem a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="5c2d3-194">Depois que a implantação estiver concluída, devemos ser capazes de nos conectarmos ao serviço web pela porta 80, visto que abrimos a porta quando provisionamos a máquina virtual com o comando Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="5c2d3-195">Como essa máquina virtual é a única em meu serviço de nuvem, vou conectá-la à url do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="5c2d3-196">Como você pode ver, fui criativo com meu código HTML.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="5c2d3-197">Não se esqueça de que também podemos nos conectar através de uma sessão RDP do portal do Azure por meio da porta 3389.</span><span class="sxs-lookup"><span data-stu-id="5c2d3-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="5c2d3-198">Espero que isso tenha sido útil!</span><span class="sxs-lookup"><span data-stu-id="5c2d3-198">I hope this has been helpful!</span></span> <span data-ttu-id="5c2d3-199">Siga adiante e comece sua jornada de infraestrutura como código com o Azure hoje mesmo!</span><span class="sxs-lookup"><span data-stu-id="5c2d3-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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
