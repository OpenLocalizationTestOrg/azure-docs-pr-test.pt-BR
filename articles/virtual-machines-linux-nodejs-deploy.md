---
title: "Implantar um aplicativo Node.js para máquinas virtuais Linux no Azure"
description: "Saiba como implantar um aplicativo Node.js em máquinas virtuais Linux no Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="dc888-103">Implantar um aplicativo Node.js para máquinas virtuais Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dc888-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="dc888-104">Este tutorial mostra como usar um aplicativo Node.js e como implantá-lo em máquinas virtuais Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc888-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="dc888-105">As instruções deste tutorial podem ser seguidas em qualquer sistema operacional que seja capaz de executar o Node.js.</span><span class="sxs-lookup"><span data-stu-id="dc888-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="dc888-106">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="dc888-106">You'll learn how to:</span></span>

* <span data-ttu-id="dc888-107">Bifurcar e clonar um repositório GitHub contendo um aplicativo TODO simples;</span><span class="sxs-lookup"><span data-stu-id="dc888-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="dc888-108">Criar e configurar duas máquinas virtuais Linux no Azure para executar o aplicativo;</span><span class="sxs-lookup"><span data-stu-id="dc888-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="dc888-109">Iterar no aplicativo pelo envio de atualizações por push para a máquina virtual de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="dc888-110">Para concluir este tutorial, você precisará de uma conta do GitHub e de uma conta do Microsoft Azure, além da capacidade de usar o Git em um computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="dc888-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="dc888-111">Se você não tiver uma conta do GitHub, poderá se inscrever [aqui](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="dc888-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="dc888-112">Se você não tiver uma conta do [Microsoft Azure](https://azure.microsoft.com/), poderá se inscrever para uma avaliação GRATUITA [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc888-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="dc888-113">Isso também o guiará pelo processo de inscrição em uma [Conta da Microsoft](http://account.microsoft.com) se você já não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="dc888-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="dc888-114">Como alternativa, se você for um assinante do Visual Studio, poderá [ativar os benefícios do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="dc888-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="dc888-115">Se você não tiver o git na máquina de desenvolvimento e estiver usando um computador Windows ou Macintosh, instale o git [aqui](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="dc888-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="dc888-116">Se você estiver usando o Linux, instale o git usando o mecanismo mais apropriado, como `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="dc888-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="dc888-117">Bifurcação e clonagem de aplicativo TODO</span><span class="sxs-lookup"><span data-stu-id="dc888-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="dc888-118">O aplicativo TODO usado por este tutorial implementa um front-end da Web simples em uma instância do MongoDB que rastreia uma lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="dc888-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="dc888-119">Depois de entrar no GitHub, acesse [aqui](https://github.com/stepro/node-todo) para localizar o aplicativo e bifurcá-lo usando o link no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="dc888-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="dc888-120">Isso deve criar um repositório em sua conta denominado *nomedaconta*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="dc888-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="dc888-121">Agora, em sua máquina de desenvolvimento, clone este repositório:</span><span class="sxs-lookup"><span data-stu-id="dc888-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="dc888-122">Usaremos esse clone local do repositório mais tarde ao fazer alterações no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="dc888-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="dc888-123">Criando e configurando máquinas virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="dc888-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="dc888-124">O Azure tem excelente suporte para computação bruta usando máquinas virtuais Linux.</span><span class="sxs-lookup"><span data-stu-id="dc888-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="dc888-125">Esta parte do tutorial mostra como é fácil criar duas máquinas virtuais Linux e implantar o aplicativo TODO, executando o front-end da Web em uma e a instância do MongoDB em outra.</span><span class="sxs-lookup"><span data-stu-id="dc888-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="dc888-126">Criando máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="dc888-126">Creating Virtual Machines</span></span>
<span data-ttu-id="dc888-127">A maneira mais fácil de criar uma nova máquina virtual no Azure é usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc888-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="dc888-128">Clique [aqui](https://portal.azure.com) para entrar e iniciar o Portal do Azure no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="dc888-129">Depois que o Portal do Azure tiver sido carregado, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dc888-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="dc888-130">Clique no link "+ Novo";</span><span class="sxs-lookup"><span data-stu-id="dc888-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="dc888-131">Selecione a categoria "Computação" e escolha "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="dc888-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="dc888-132">Selecione o modelo de implantação do "Gerenciador de Recursos" e clique em "Criar";</span><span class="sxs-lookup"><span data-stu-id="dc888-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="dc888-133">Preencha o básico de acordo com estas diretrizes:</span><span class="sxs-lookup"><span data-stu-id="dc888-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="dc888-134">Especifique um nome que você pode identificar facilmente mais tarde;</span><span class="sxs-lookup"><span data-stu-id="dc888-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="dc888-135">Neste tutorial, escolha Autenticação de senha;</span><span class="sxs-lookup"><span data-stu-id="dc888-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="dc888-136">Crie um novo grupo de recursos com um nome identificável.</span><span class="sxs-lookup"><span data-stu-id="dc888-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="dc888-137">Para o tamanho da máquina Virtual, o "Padrão A1"é uma opção razoável para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc888-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="dc888-138">Para configurações adicionais, verifique se o tipo de disco é "Padrão" e aceite os padrões restantes.</span><span class="sxs-lookup"><span data-stu-id="dc888-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="dc888-139">Inicie a criação na página Resumo.</span><span class="sxs-lookup"><span data-stu-id="dc888-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="dc888-140">Execute o processo acima duas vezes para criar duas máquinas virtuais Linux, uma para o front-end da Web e outra para a instância do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc888-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="dc888-141">A criação das máquinas virtuais levará cerca de 5 a 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="dc888-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="dc888-142">Atribuindo uma entrada DNS para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="dc888-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="dc888-143">As máquinas virtuais criadas no Azure, por padrão, somente podem ser acessadas com endereço IP público, como 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="dc888-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="dc888-144">Vamos facilitar a identificação das máquinas atribuindo-lhes entradas DNS.</span><span class="sxs-lookup"><span data-stu-id="dc888-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="dc888-145">Depois que o portal indicar a criação das máquinas virtuais, clique no link "Máquinas virtuais" na barra de navegação à esquerda e localize suas máquinas.</span><span class="sxs-lookup"><span data-stu-id="dc888-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="dc888-146">Para cada máquina:</span><span class="sxs-lookup"><span data-stu-id="dc888-146">For each machine:</span></span>

* <span data-ttu-id="dc888-147">Localize a guia Essentials e clique no endereço IP público;</span><span class="sxs-lookup"><span data-stu-id="dc888-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="dc888-148">Na configuração de endereço IP público, atribua um rótulo de nome de DNS e salve-o.</span><span class="sxs-lookup"><span data-stu-id="dc888-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="dc888-149">O portal fará com que o nome especificado esteja disponível.</span><span class="sxs-lookup"><span data-stu-id="dc888-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="dc888-150">Depois de salvar a configuração, as máquinas virtuais terão nomes de host semelhantes a `machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="dc888-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="dc888-151">Conectando-se às máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="dc888-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="dc888-152">Quando as máquinas virtuais foram provisionadas, eles foram pré-configuradas para permitir conexões remotas via SSH.</span><span class="sxs-lookup"><span data-stu-id="dc888-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="dc888-153">Esse é o mecanismo que usaremos para configurar as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="dc888-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="dc888-154">Se você estiver usando o Windows para desenvolvimento e não tiver um cliente SSH, obtenha um.</span><span class="sxs-lookup"><span data-stu-id="dc888-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="dc888-155">Uma opção comum é o PuTTY, que pode ser baixado [aqui](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="dc888-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="dc888-156">Os sistemas operacionais Macintosh e Linux vêm com uma versão do SSH pré-instalada.</span><span class="sxs-lookup"><span data-stu-id="dc888-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="dc888-157">Configurando a máquina virtual front-end da Web</span><span class="sxs-lookup"><span data-stu-id="dc888-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="dc888-158">SSH para a máquina de front-end da Web criada usando PuTTY, linha de comando SSH ou outra ferramenta de SSH favorita.</span><span class="sxs-lookup"><span data-stu-id="dc888-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="dc888-159">Você deve ver uma mensagem de boas-vindas seguida de um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="dc888-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="dc888-160">Primeiro, vamos garantir que tanto o Git quanto o Node estão instalados:</span><span class="sxs-lookup"><span data-stu-id="dc888-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="dc888-161">Como o front-end do aplicativo Web depende de alguns módulos nativos do Node.js, também precisamos instalar o conjunto essencial de ferramentas de compilação:</span><span class="sxs-lookup"><span data-stu-id="dc888-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="dc888-162">Por fim, vamos instalar um aplicativo Node.js chamado *forever*, que ajuda a executar aplicativos de servidor do Node.js:</span><span class="sxs-lookup"><span data-stu-id="dc888-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="dc888-163">Essas são todas as dependências necessárias nesta máquina virtual para poder executar o front-end do aplicativo Web; portanto, vamos executá-las.</span><span class="sxs-lookup"><span data-stu-id="dc888-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="dc888-164">Para isso, primeiro vamos criar um clone básico do repositório GitHub que você bifurcou anteriormente para poder publicar facilmente atualizações na máquina virtual (abordaremos esse cenário de atualização mais adiante) e depois clonar o clone básico para fornecer uma versão do repositório que pode realmente ser executada.</span><span class="sxs-lookup"><span data-stu-id="dc888-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="dc888-165">No diretório home (~), execute os comandos abaixo (substituindo *nomedaconta* pelo nome da conta de usuário do GitHub):</span><span class="sxs-lookup"><span data-stu-id="dc888-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="dc888-166">Agora, entre no diretório node-todo e execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="dc888-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="dc888-167">O front-end do aplicativo Web está em execução; no entanto, há mais uma etapa antes de se poder acessar o aplicativo em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="dc888-168">A máquina virtual que você criou é protegida por um recurso do Azure chamado *grupo de segurança de rede*, que foi criado quando você provisionou a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc888-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="dc888-169">Atualmente, esse recurso permite que somente as solicitações externas para a porta 22 sejam roteadas para a máquina virtual, o que permite a comunicação SSH com a máquina, mas nada além disso.</span><span class="sxs-lookup"><span data-stu-id="dc888-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="dc888-170">Então, para exibir o aplicativo TODO, que é configurado para ser executado na porta 8080, essa porta também precisa ser aberta.</span><span class="sxs-lookup"><span data-stu-id="dc888-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="dc888-171">Volte para o portal do Azure e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dc888-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="dc888-172">Clique em "Grupos de recursos" na barra de navegação à esquerda;</span><span class="sxs-lookup"><span data-stu-id="dc888-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="dc888-173">Selecione o grupo de recursos que contém sua máquina virtual;</span><span class="sxs-lookup"><span data-stu-id="dc888-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="dc888-174">Na lista de recursos resultante, selecione o grupo de segurança de rede (aquele com um ícone de escudo);</span><span class="sxs-lookup"><span data-stu-id="dc888-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="dc888-175">Nas propriedades, selecione "Regras de segurança de entrada";</span><span class="sxs-lookup"><span data-stu-id="dc888-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="dc888-176">Na barra de ferramentas, clique em "Adicionar";</span><span class="sxs-lookup"><span data-stu-id="dc888-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="dc888-177">Forneça um nome como "default-allow-todo";</span><span class="sxs-lookup"><span data-stu-id="dc888-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="dc888-178">Defina o protocolo como "TCP";</span><span class="sxs-lookup"><span data-stu-id="dc888-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="dc888-179">Defina o intervalo de porta de destino como "8080";</span><span class="sxs-lookup"><span data-stu-id="dc888-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="dc888-180">Clique em OK e aguarde a criação da regra de segurança.</span><span class="sxs-lookup"><span data-stu-id="dc888-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="dc888-181">Depois de criar essa regra de segurança, o aplicativo TODO fica visível publicamente na Internet e você pode navegar até ele usando uma URL como:</span><span class="sxs-lookup"><span data-stu-id="dc888-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="dc888-182">Você observará que, embora ainda não tenhamos configurado a máquina virtual de MongoDB, o aplicativo TODO parece estar funcionando bem.</span><span class="sxs-lookup"><span data-stu-id="dc888-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="dc888-183">Isso ocorre porque o repositório de origem é codificado para usar uma instância do MongoDB pré-instalada.</span><span class="sxs-lookup"><span data-stu-id="dc888-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="dc888-184">Depois de configurarmos a máquina virtual de MongoDB, vamos voltar e alterar o código-fonte para utilizar nossa instância privada do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc888-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="dc888-185">Configurando a máquina virtual MongoDB</span><span class="sxs-lookup"><span data-stu-id="dc888-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="dc888-186">SSH para o segundo computador que você criou usando PuTTY, linha de comando SSH ou outra ferramenta SSH favorita.</span><span class="sxs-lookup"><span data-stu-id="dc888-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="dc888-187">Após ver a mensagem de boas-vindas e o prompt de comando, instale o MongoDB (estas instruções foram tiradas [daqui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="dc888-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="dc888-188">Por padrão, o MongoDB é configurado para só poder ser acessado localmente.</span><span class="sxs-lookup"><span data-stu-id="dc888-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="dc888-189">Neste tutorial, configuraremos MongoDB para que ele possa ser acessado da máquina de virtual do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dc888-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="dc888-190">Em um contexto sudo, abra o arquivo /etc/mongod.conf e localize a seção `# network interfaces` .</span><span class="sxs-lookup"><span data-stu-id="dc888-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="dc888-191">Altere o valor de configuração `net.bindIp` para `0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="dc888-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="dc888-192">Essa configuração serve apenas para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc888-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="dc888-193">Ela **NÃO** é uma prática de segurança recomendada e não deve ser usada em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="dc888-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="dc888-194">Agora, verifique se o serviço MongoDB foi iniciado:</span><span class="sxs-lookup"><span data-stu-id="dc888-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="dc888-195">O MongoDB opera na porta 27017 por padrão.</span><span class="sxs-lookup"><span data-stu-id="dc888-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="dc888-196">Assim, da mesma forma que precisávamos abrir a porta 8080 na máquina virtual front-end da Web, precisamos abrir a porta 27017 na máquina virtual de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc888-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="dc888-197">Volte para o portal do Azure e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dc888-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="dc888-198">Clique em "Grupos de recursos" na barra de navegação à esquerda;</span><span class="sxs-lookup"><span data-stu-id="dc888-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="dc888-199">Selecione o grupo de recursos que contém a máquina virtual de MongoDB;</span><span class="sxs-lookup"><span data-stu-id="dc888-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="dc888-200">Na lista de recursos resultante, selecione o grupo de segurança de rede (aquele com um ícone de escudo) com o mesmo nome que você atribuiu à máquina virtual de MongoDB;</span><span class="sxs-lookup"><span data-stu-id="dc888-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="dc888-201">Nas propriedades, selecione "Regras de segurança de entrada";</span><span class="sxs-lookup"><span data-stu-id="dc888-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="dc888-202">Na barra de ferramentas, clique em "Adicionar";</span><span class="sxs-lookup"><span data-stu-id="dc888-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="dc888-203">Forneça um nome como "default-allow-mongo";</span><span class="sxs-lookup"><span data-stu-id="dc888-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="dc888-204">Defina o protocolo como "TCP";</span><span class="sxs-lookup"><span data-stu-id="dc888-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="dc888-205">Defina o intervalo de porta de destino como "27017";</span><span class="sxs-lookup"><span data-stu-id="dc888-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="dc888-206">Clique em OK e aguarde a criação da regra de segurança.</span><span class="sxs-lookup"><span data-stu-id="dc888-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="dc888-207">Iterando o aplicativo TODO</span><span class="sxs-lookup"><span data-stu-id="dc888-207">Iterating on the TODO application</span></span>
<span data-ttu-id="dc888-208">Até agora, provisionamos duas máquinas virtuais Linux: aquela que está executando o aplicativo front-end da Web e outra que está executando uma instância do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc888-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="dc888-209">Mas há um problema: o front-end da Web, na verdade, ainda não está usando a instância do MongoDB provisionada.</span><span class="sxs-lookup"><span data-stu-id="dc888-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="dc888-210">Vamos corrigir isso atualizando o código de front-end da Web para usar uma variável de ambiente em vez de uma instância embutida em código.</span><span class="sxs-lookup"><span data-stu-id="dc888-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="dc888-211">Alterar o aplicativo TODO</span><span class="sxs-lookup"><span data-stu-id="dc888-211">Changing the TODO application</span></span>
<span data-ttu-id="dc888-212">Na máquina de desenvolvimento onde você clonou o repositório node-todo pela primeira vez, abra o `node-todo/config/database.js` no seu editor favorito e altere o valor de URL do valor embutido em código, como `mongodb://...`, para `process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="dc888-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="dc888-213">Confirme as alterações e envie por push ao mestre do GitHub:</span><span class="sxs-lookup"><span data-stu-id="dc888-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="dc888-214">Infelizmente, isso não publica a alteração para a máquina virtual de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="dc888-215">Vamos fazer mais algumas alterações na máquina virtual para criar um mecanismo simples, mas eficaz, de publicação de atualizações, para que você possa ver rapidamente os efeitos das alterações no ambiente em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="dc888-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="dc888-216">Configurando a máquina virtual front-end da Web</span><span class="sxs-lookup"><span data-stu-id="dc888-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="dc888-217">Lembre-se de que criamos anteriormente um clone básico do repositório node-todo na máquina virtual de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="dc888-218">Acontece que essa ação criou um novo Git remoto para onde as alterações podem ser enviadas por push.</span><span class="sxs-lookup"><span data-stu-id="dc888-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="dc888-219">No entanto, o simples envio por push para esse Git remoto não fornece o modelo de iteração rápida que os desenvolvedores buscam ao trabalhar em seus códigos.</span><span class="sxs-lookup"><span data-stu-id="dc888-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="dc888-220">O que queremos fazer é garantir que quando ocorrer um envio por push para o repositório remoto na máquina virtual, o aplicativo TODO em execução será atualizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dc888-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="dc888-221">Felizmente, isso é fácil de conseguir com o git.</span><span class="sxs-lookup"><span data-stu-id="dc888-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="dc888-222">O Git expõe um número de ganchos que são chamados em momentos específicos para reagir às ações realizadas no repositório.</span><span class="sxs-lookup"><span data-stu-id="dc888-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="dc888-223">Eles são especificados usando scripts do shell na pasta `hooks` do repositório.</span><span class="sxs-lookup"><span data-stu-id="dc888-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="dc888-224">O gancho que mais se aplica ao cenário de atualização automática é o evento `post-update` .</span><span class="sxs-lookup"><span data-stu-id="dc888-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="dc888-225">Em uma sessão SSH para a máquina virtual de front-end da Web, altere para o `~/node-todo.git/hooks` diretório e adicione o seguinte conteúdo em um arquivo chamado `post-update` (substituindo `machinename` e `region` com as informações de máquina virtual do MongoDB):</span><span class="sxs-lookup"><span data-stu-id="dc888-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="dc888-226">Verifique se o arquivo é executável executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="dc888-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="dc888-227">Esse script garante que se o aplicativo de servidor atual for interrompido, o código no repositório clonado será atualizado com o mais recente, as dependências atualizadas serão atendidas e o servidor será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="dc888-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="dc888-228">Ela também garante que o ambiente foi configurado em preparação para o recebimento de nossa primeira atualização de aplicativo para obter a instância do MongoDB de uma variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="dc888-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="dc888-229">Configurando seu computador de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="dc888-229">Configuring your Development Machine</span></span>
<span data-ttu-id="dc888-230">Agora, vejamos sua máquina de desenvolvimento conectada à máquina virtual de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="dc888-231">Isso é tão simples quanto adicionar o repositório vazio na máquina virtual como um repositório remoto.</span><span class="sxs-lookup"><span data-stu-id="dc888-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="dc888-232">Execute o seguinte comando para fazer isso (substituindo *usuário* pelo nome de logon de máquina virtual de front-end da Web, e *nomedamáquina* e *região* conforme apropriado):</span><span class="sxs-lookup"><span data-stu-id="dc888-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="dc888-233">Isso é tudo o que é necessário para habilitar o envio por push, ou a devida publicação, das alterações para a máquina virtual de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="dc888-234">Publicação de atualizações</span><span class="sxs-lookup"><span data-stu-id="dc888-234">Publishing Updates</span></span>
<span data-ttu-id="dc888-235">Vamos publicar uma alteração feita até o momento para que o aplicativo use nossa própria instância do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="dc888-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="dc888-236">Você deve ver saídas semelhantes às seguintes:</span><span class="sxs-lookup"><span data-stu-id="dc888-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="dc888-237">Após a conclusão do comando, tente atualizar o aplicativo em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="dc888-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="dc888-238">Você deve ser capaz de ver que a lista de tarefas pendentes apresentada aqui está vazia e não mais associada à instância do MongoDB implantada e compartilhada.</span><span class="sxs-lookup"><span data-stu-id="dc888-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="dc888-239">Para concluir o tutorial, vamos fazer outra alteração mais visível.</span><span class="sxs-lookup"><span data-stu-id="dc888-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="dc888-240">Na máquina de desenvolvimento, abra o arquivo node-todo/public/index.html usando seu editor favorito.</span><span class="sxs-lookup"><span data-stu-id="dc888-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="dc888-241">Localize o cabeçalho jumbotron e altere o título de "I’m a Todo-aholilc" para "I’m a Todo-aholic on Azure!".</span><span class="sxs-lookup"><span data-stu-id="dc888-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="dc888-242">Agora, vamos confirmar:</span><span class="sxs-lookup"><span data-stu-id="dc888-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="dc888-243">Dessa vez, vamos publicar a alteração no Azure antes de enviá-la de volta por push para o repositório GitHub:</span><span class="sxs-lookup"><span data-stu-id="dc888-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="dc888-244">Quando esse comando for concluído, atualize a página da Web para ver as alterações.</span><span class="sxs-lookup"><span data-stu-id="dc888-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="dc888-245">Se estiverem boas, envie a alteração por push de volta à origem remota:</span><span class="sxs-lookup"><span data-stu-id="dc888-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="dc888-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc888-246">Next Steps</span></span>
<span data-ttu-id="dc888-247">Este artigo mostrou como utilizar um aplicativo Node.js e implantá-lo em máquinas virtuais Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc888-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="dc888-248">Para saber mais sobre máquinas virtuais Linux no Azure, confira [Introdução ao Linux no Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="dc888-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="dc888-249">Para obter mais informações sobre como desenvolver aplicativos do Node.js no Azure, consulte o [Centro de desenvolvedores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="dc888-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

