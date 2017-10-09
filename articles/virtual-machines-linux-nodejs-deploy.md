---
title: "aaaDeploy tooLinux de aplicativo um Node. js máquinas virtuais no Azure"
description: "Saiba como toodeploy um Node. js máquinas de virtuais de tooLinux do aplicativo no Azure."
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
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="f19a9-103">Implantar um aplicativo de Node. js tooLinux máquinas virtuais no Azure</span><span class="sxs-lookup"><span data-stu-id="f19a9-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="f19a9-104">Este tutorial mostra como tootake um aplicativo Node. js e implantá-lo em máquinas virtuais de tooLinux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="f19a9-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="f19a9-105">instruções de saudação neste tutorial podem ser seguidas em qualquer sistema operacional que é capaz de executar o Node. js.</span><span class="sxs-lookup"><span data-stu-id="f19a9-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="f19a9-106">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f19a9-106">You'll learn how to:</span></span>

* <span data-ttu-id="f19a9-107">Bifurcar e clonar um repositório GitHub contendo um aplicativo TODO simples;</span><span class="sxs-lookup"><span data-stu-id="f19a9-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="f19a9-108">Criar e configurar duas máquinas virtuais de Linux no aplicativo do Azure toorun hello;</span><span class="sxs-lookup"><span data-stu-id="f19a9-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="f19a9-109">Itere o aplicativo hello enviando a máquina virtual do atualizações toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="f19a9-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="f19a9-110">toocomplete neste tutorial, você precisa de uma conta do GitHub e uma conta do Microsoft Azure e Olá capacidade toouse Git de um computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f19a9-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="f19a9-111">Se você não tiver uma conta do GitHub, poderá se inscrever [aqui](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="f19a9-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="f19a9-112">Se você não tiver uma conta do [Microsoft Azure](https://azure.microsoft.com/), poderá se inscrever para uma avaliação GRATUITA [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f19a9-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f19a9-113">Isso também levará você por meio do processo de inscrição Olá um [Account Microsoft](http://account.microsoft.com) se você ainda não tiver um.</span><span class="sxs-lookup"><span data-stu-id="f19a9-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="f19a9-114">Como alternativa, se você for um assinante do Visual Studio, poderá [ativar os benefícios do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f19a9-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="f19a9-115">Se você não tiver o git na máquina de desenvolvimento e estiver usando um computador Windows ou Macintosh, instale o git [aqui](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="f19a9-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="f19a9-116">Se você estiver usando o Linux, instale o git usando o mecanismo de hello mais apropriado para você, como `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="f19a9-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="f19a9-117">Bifurcação e clonagem Olá TODO aplicativo</span><span class="sxs-lookup"><span data-stu-id="f19a9-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="f19a9-118">Olá aplicativo TODO usado por este tutorial implementa um front-end da web simples sobre uma instância do MongoDB que mantém o controle de uma lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="f19a9-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="f19a9-119">Depois de entrar no tooGitHub, vá [aqui](https://github.com/stepro/node-todo) toofind Olá aplicativo e bifurcação usando o link de saudação na parte superior de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="f19a9-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="f19a9-120">Isso deve criar um repositório em sua conta denominado *nomedaconta*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="f19a9-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="f19a9-121">Agora, em sua máquina de desenvolvimento, clone este repositório:</span><span class="sxs-lookup"><span data-stu-id="f19a9-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="f19a9-122">Usaremos esse clone local do repositório de saudação um pouco mais tarde ao fazer alterações de código-fonte toohello.</span><span class="sxs-lookup"><span data-stu-id="f19a9-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="f19a9-123">Criando e configurando Olá máquinas virtuais do Linux</span><span class="sxs-lookup"><span data-stu-id="f19a9-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="f19a9-124">O Azure tem excelente suporte para computação bruta usando máquinas virtuais Linux.</span><span class="sxs-lookup"><span data-stu-id="f19a9-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="f19a9-125">Esta parte do mostra de tutorial hello como você pode facilmente criar duas máquinas virtuais do Linux e implantar Olá TODO aplicativo toothem, executando Olá front-end da web em um e Olá instância MongoDB Olá outros.</span><span class="sxs-lookup"><span data-stu-id="f19a9-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="f19a9-126">Criando máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f19a9-126">Creating Virtual Machines</span></span>
<span data-ttu-id="f19a9-127">toocreate de maneira mais fácil de saudação uma nova máquina virtual no Azure é toouse Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f19a9-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="f19a9-128">Clique em [aqui](https://portal.azure.com) toosign no e inicie Olá Portal do Azure no seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f19a9-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="f19a9-129">Uma vez hello Azure Portal for carregada, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f19a9-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="f19a9-130">Clique em Olá "+ novo" vincular;</span><span class="sxs-lookup"><span data-stu-id="f19a9-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="f19a9-131">Selecione a categoria de "Computação" hello e escolha "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="f19a9-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="f19a9-132">Selecione o modelo de implantação do hello "Gerenciador de recursos" e clique em "Criar";</span><span class="sxs-lookup"><span data-stu-id="f19a9-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="f19a9-133">Preencha as Noções básicas de saudação estas diretrizes:</span><span class="sxs-lookup"><span data-stu-id="f19a9-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="f19a9-134">Especifique um nome que você pode identificar facilmente mais tarde;</span><span class="sxs-lookup"><span data-stu-id="f19a9-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="f19a9-135">Neste tutorial, escolha Autenticação de senha;</span><span class="sxs-lookup"><span data-stu-id="f19a9-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="f19a9-136">Crie um novo grupo de recursos com um nome identificável.</span><span class="sxs-lookup"><span data-stu-id="f19a9-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="f19a9-137">Para Olá tamanho da máquina Virtual, o "Padrão" A1"é uma opção razoável para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f19a9-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="f19a9-138">Para configurações adicionais, certifique-se de que o tipo de disco Olá é "Padrão" e aceite que todas Olá padrões restantes.</span><span class="sxs-lookup"><span data-stu-id="f19a9-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="f19a9-139">Iniciar criação de saudação na página de resumo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f19a9-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="f19a9-140">Executar Olá acima processar duas vezes toocreate duas máquinas virtuais do Linux, uma para Olá web front-end e uma instância do MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="f19a9-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="f19a9-141">Criação de máquinas virtuais de saudação levará cerca de 5 a 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="f19a9-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="f19a9-142">Atribuindo uma entrada DNS para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f19a9-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="f19a9-143">As máquinas virtuais criadas no Azure, por padrão, somente podem ser acessadas com endereço IP público, como 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="f19a9-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="f19a9-144">Vamos fazer máquinas hello mais facilmente identificáveis, atribuindo-lhes as entradas DNS.</span><span class="sxs-lookup"><span data-stu-id="f19a9-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="f19a9-145">Depois que o portal Olá indica que as máquinas virtuais de saudação tenham sido criadas, clique no link de "Máquinas virtuais" hello na barra de navegação esquerda hello e localize a suas máquinas.</span><span class="sxs-lookup"><span data-stu-id="f19a9-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="f19a9-146">Para cada máquina:</span><span class="sxs-lookup"><span data-stu-id="f19a9-146">For each machine:</span></span>

* <span data-ttu-id="f19a9-147">Localize o guia do Essentials hello e clique em Olá endereço IP público;</span><span class="sxs-lookup"><span data-stu-id="f19a9-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="f19a9-148">Na configuração do endereço IP pública Olá, atribuir um rótulo de nome DNS e salvar.</span><span class="sxs-lookup"><span data-stu-id="f19a9-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="f19a9-149">portal de saudação garantirá que você especificar o nome hello está disponível.</span><span class="sxs-lookup"><span data-stu-id="f19a9-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="f19a9-150">Depois de salvar a configuração de hello, as máquinas virtuais terão nomes de host semelhantes muito`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f19a9-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="f19a9-151">Conectando toohello máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f19a9-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="f19a9-152">Quando as máquinas virtuais foram provisionadas, eles eram conexões remotas tooallow pré-configurado via SSH.</span><span class="sxs-lookup"><span data-stu-id="f19a9-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="f19a9-153">Esse é o mecanismo de saudação usaremos tooconfigure Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="f19a9-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="f19a9-154">Se você estiver usando o Windows para o desenvolvimento, você precisará tooget um cliente SSH se você ainda não tiver um.</span><span class="sxs-lookup"><span data-stu-id="f19a9-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="f19a9-155">Uma opção comum é o PuTTY, que pode ser baixado [aqui](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="f19a9-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="f19a9-156">Os sistemas operacionais Macintosh e Linux vêm com uma versão do SSH pré-instalada.</span><span class="sxs-lookup"><span data-stu-id="f19a9-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="f19a9-157">Configurando Olá máquina de Virtual de front-end da Web</span><span class="sxs-lookup"><span data-stu-id="f19a9-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="f19a9-158">Máquina de front-end do SSH toohello web que você criou usando PuTTY, ssh linha de comando ou outra ferramenta SSH favorita.</span><span class="sxs-lookup"><span data-stu-id="f19a9-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="f19a9-159">Você deve ver uma mensagem de boas-vindas seguida de um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="f19a9-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="f19a9-160">Primeiro, vamos garantir que tanto o Git quanto o Node estão instalados:</span><span class="sxs-lookup"><span data-stu-id="f19a9-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="f19a9-161">Como o front-end da web do aplicativo hello depende de alguns módulos nativos do Node. js, também precisamos conjunto essencial de saudação de tooinstall de ferramentas de compilação:</span><span class="sxs-lookup"><span data-stu-id="f19a9-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="f19a9-162">Por fim, vamos instalar um aplicativo Node. js chamado *para sempre*, que ajuda a aplicativos de servidor toorun Node. js:</span><span class="sxs-lookup"><span data-stu-id="f19a9-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="f19a9-163">Estas são todas as dependências de saudação necessárias no front-end da web do aplicativo esta máquina virtual toobe toorun capaz de hello, então vamos que a execução.</span><span class="sxs-lookup"><span data-stu-id="f19a9-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="f19a9-164">toodo isso, vamos primeiro criar um clone bare do repositório do GitHub Olá você bifurcada anteriormente para que você pode facilmente publicar atualizações toohello virtual machine (vamos abordar esse cenário de atualização mais tarde) e depois clonar Olá clone bare tooprovide uma versão de hello repositório que, na verdade, pode ser executado.</span><span class="sxs-lookup"><span data-stu-id="f19a9-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="f19a9-165">A partir do diretório do saudação inicial (~), execute o hello comandos a seguir (substituindo *accountname* com seu nome de conta de usuário do GitHub):</span><span class="sxs-lookup"><span data-stu-id="f19a9-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="f19a9-166">Agora insira Olá todo nó diretório e execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="f19a9-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="f19a9-167">Olá front-end do aplicativo web está em execução, no entanto, há uma ou mais etapas antes de poder acessar o aplicativo hello em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f19a9-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="f19a9-168">Olá máquina virtual que você criou é protegida por um recurso do Azure chamado um *grupo de segurança de rede*, que foi criado para você quando você provisionou Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f19a9-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="f19a9-169">No momento, esse recurso permite que somente solicitações externas tooport toobe 22 roteadas toohello máquina virtual, que permite a comunicação SSH com hello máquina, mas nada mais.</span><span class="sxs-lookup"><span data-stu-id="f19a9-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="f19a9-170">Portanto Olá tooview de ordem aplicativo TODO, que é toorun configurado na porta 8080, essa porta também precisa toobe aberta.</span><span class="sxs-lookup"><span data-stu-id="f19a9-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="f19a9-171">Retorno toohello Portal do Azure e Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f19a9-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="f19a9-172">Clique em "Grupos de recursos" na barra de navegação esquerda Olá;</span><span class="sxs-lookup"><span data-stu-id="f19a9-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="f19a9-173">Selecionar grupo de recursos de saudação que contém sua máquina virtual;</span><span class="sxs-lookup"><span data-stu-id="f19a9-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="f19a9-174">Na lista resultante de saudação de recursos, selecione o grupo de segurança de rede de hello (Olá um com um ícone de escudo);</span><span class="sxs-lookup"><span data-stu-id="f19a9-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="f19a9-175">Nas propriedades de saudação, escolha "regras de segurança de entrada";</span><span class="sxs-lookup"><span data-stu-id="f19a9-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="f19a9-176">Na barra de ferramentas hello, clique em "Adicionar";</span><span class="sxs-lookup"><span data-stu-id="f19a9-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="f19a9-177">Forneça um nome como "default-allow-todo";</span><span class="sxs-lookup"><span data-stu-id="f19a9-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="f19a9-178">Definir o protocolo de saudação muito "TCP";</span><span class="sxs-lookup"><span data-stu-id="f19a9-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="f19a9-179">Definir o intervalo de porta de destino Olá muito "8080;"</span><span class="sxs-lookup"><span data-stu-id="f19a9-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="f19a9-180">Clique em Okey e aguarde Olá toobe de regra de segurança criado.</span><span class="sxs-lookup"><span data-stu-id="f19a9-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="f19a9-181">Depois de criar essa regra de segurança, Olá aplicativo TODO é visível publicamente em Olá internet e você pode procurar tooit, por exemplo, usando uma URL como:</span><span class="sxs-lookup"><span data-stu-id="f19a9-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="f19a9-182">Você observará que mesmo que nós ainda não tiver configurado Olá MongoDB virtual machine, Olá aplicativo TODO aparece toobe totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="f19a9-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="f19a9-183">Isso ocorre porque o repositório de origem de saudação é codificado toouse uma instância previamente implantada do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f19a9-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="f19a9-184">Depois que configuramos Olá MongoDB virtual machine, podemos será voltar e alterar Olá tooutilize de código de origem nossa instância particular do MongoDB em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f19a9-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="f19a9-185">Configurando Olá MongoDB Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="f19a9-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="f19a9-186">SSH toohello segunda máquina que você criou usando PuTTY, ssh linha de comando ou outra ferramenta SSH favorita.</span><span class="sxs-lookup"><span data-stu-id="f19a9-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="f19a9-187">Depois de ver a mensagem de boas-vindas hello e prompt de comando, instale o MongoDB (estas instruções foram tiradas da [aqui](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="f19a9-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="f19a9-188">Por padrão, o MongoDB é configurado para só poder ser acessado localmente.</span><span class="sxs-lookup"><span data-stu-id="f19a9-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="f19a9-189">Para este tutorial, configuraremos MongoDB para que ele possa ser acessado da máquina de virtual do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f19a9-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="f19a9-190">Em um contexto de sudo, abra o arquivo de /etc/mongod.conf hello e localize Olá `# network interfaces` seção.</span><span class="sxs-lookup"><span data-stu-id="f19a9-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="f19a9-191">Saudação de alteração `net.bindIp` configuração valor muito`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f19a9-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="f19a9-192">Essa configuração é para fins de saudação apenas deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f19a9-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="f19a9-193">Ela **NÃO** é uma prática de segurança recomendada e não deve ser usada em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="f19a9-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="f19a9-194">Certifique-se agora Olá MongoDB serviço foi iniciado:</span><span class="sxs-lookup"><span data-stu-id="f19a9-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="f19a9-195">O MongoDB opera na porta 27017 por padrão.</span><span class="sxs-lookup"><span data-stu-id="f19a9-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="f19a9-196">Portanto, em Olá a mesma forma que precisávamos tooopen porta 8080 na máquina virtual do Olá web front-end, precisamos de porta tooopen 27017 na máquina de virtual Olá MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f19a9-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="f19a9-197">Retorno toohello Portal do Azure e Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f19a9-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="f19a9-198">Clique em "Grupos de recursos" na barra de navegação esquerda Olá;</span><span class="sxs-lookup"><span data-stu-id="f19a9-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="f19a9-199">Selecionar grupo de recursos de saudação que contém a máquina de virtual do MongoDB Olá;</span><span class="sxs-lookup"><span data-stu-id="f19a9-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="f19a9-200">Na lista resultante de saudação de recursos, selecione grupo de segurança de rede hello (Olá um com um ícone de escudo) com hello que mesmo nome que você deu a máquina de virtual do MongoDB toohello;</span><span class="sxs-lookup"><span data-stu-id="f19a9-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="f19a9-201">Nas propriedades de saudação, escolha "regras de segurança de entrada";</span><span class="sxs-lookup"><span data-stu-id="f19a9-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="f19a9-202">Na barra de ferramentas hello, clique em "Adicionar";</span><span class="sxs-lookup"><span data-stu-id="f19a9-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="f19a9-203">Forneça um nome como "default-allow-mongo";</span><span class="sxs-lookup"><span data-stu-id="f19a9-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="f19a9-204">Definir o protocolo de saudação muito "TCP";</span><span class="sxs-lookup"><span data-stu-id="f19a9-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="f19a9-205">Definir o intervalo de porta de destino Olá muito "27017";</span><span class="sxs-lookup"><span data-stu-id="f19a9-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="f19a9-206">Clique em Okey e aguarde Olá toobe de regra de segurança criado.</span><span class="sxs-lookup"><span data-stu-id="f19a9-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="f19a9-207">Iterando em Olá aplicativo TODO</span><span class="sxs-lookup"><span data-stu-id="f19a9-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="f19a9-208">Até agora, podemos ter provisionado duas máquinas virtuais do Linux: um que está executando o aplicativo hello front-end da web e um que está executando uma instância do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f19a9-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="f19a9-209">Mas há um problema - Olá web front-end não está realmente usando Olá provisionado MongoDB instância ainda.</span><span class="sxs-lookup"><span data-stu-id="f19a9-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="f19a9-210">Vamos corrigir isso atualizando Olá web front-end código toouse uma variável de ambiente em vez de uma instância embutido.</span><span class="sxs-lookup"><span data-stu-id="f19a9-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="f19a9-211">Alterar Olá TODO aplicativo</span><span class="sxs-lookup"><span data-stu-id="f19a9-211">Changing hello TODO application</span></span>
<span data-ttu-id="f19a9-212">No computador de desenvolvimento em que você clonou primeiro repositório de todo nó hello, abra Olá `node-todo/config/database.js` arquivo em seu editor favorito e altere o valor de url de saudação do valor embutido em hello como `mongodb://...` muito`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="f19a9-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="f19a9-213">Confirmar as alterações e enviar por push toohello GitHub mestre:</span><span class="sxs-lookup"><span data-stu-id="f19a9-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="f19a9-214">Infelizmente, isso não publica máquina de virtual Olá alteração toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="f19a9-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="f19a9-215">Vamos fazer algumas alterações toothat máquina virtual tooenable mais um mecanismo simple, porém efetivo para publicar atualizações para que você pode observar rapidamente efeito Olá alterações de saudação em ambiente dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="f19a9-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="f19a9-216">Configurando Olá máquina de Virtual de front-end da Web</span><span class="sxs-lookup"><span data-stu-id="f19a9-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="f19a9-217">Lembre-se de que é criado anteriormente um clone bare do repositório de todo nó Olá na máquina virtual do Olá web front-end.</span><span class="sxs-lookup"><span data-stu-id="f19a9-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="f19a9-218">Na verdade, essa ação criada uma nova Git alterações toowhich remoto podem ser enviadas.</span><span class="sxs-lookup"><span data-stu-id="f19a9-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="f19a9-219">No entanto, simplesmente pressionando toothis remoto não bastante dá modelo de iteração rápido Olá procurando por desenvolvedores ao trabalhar em seu código.</span><span class="sxs-lookup"><span data-stu-id="f19a9-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="f19a9-220">O que podemos gostariam de ter toodo capaz de toobe é garantir que, quando ocorre um repositório remoto do push toohello na máquina virtual de hello, aplicativo de tarefas em execução hello é atualizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f19a9-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="f19a9-221">Felizmente, isso é fácil tooachieve com o git.</span><span class="sxs-lookup"><span data-stu-id="f19a9-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="f19a9-222">Git expõe um número de conexões que são chamados em momentos específicos tooreact tooactions efetuados no repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="f19a9-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="f19a9-223">Eles são especificados usando scripts do shell no repositório de saudação `hooks` pasta.</span><span class="sxs-lookup"><span data-stu-id="f19a9-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="f19a9-224">gancho de saudação que é mais aplicável para o cenário de atualização automática de saudação é hello `post-update` eventos.</span><span class="sxs-lookup"><span data-stu-id="f19a9-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="f19a9-225">Em uma SSH sessão toohello web front-end máquina virtual, alterar toohello `~/node-todo.git/hooks` diretório e adicione Olá após o arquivo de conteúdo tooa chamado `post-update` (substituindo `machinename` e `region` com suas informações de máquina virtual do MongoDB):</span><span class="sxs-lookup"><span data-stu-id="f19a9-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="f19a9-226">Certifique-se de que esse arquivo é executável executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f19a9-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="f19a9-227">Esse script garante que Olá aplicativo de servidor atual está parado, Olá código repositório clonado Olá é toohello atualizada mais recente, todas as dependências atualizadas são atendidas e Olá servidor é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="f19a9-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="f19a9-228">Também garante que o ambiente de saudação foi configurado na preparação para receber nosso primeira instância aplicativo atualização tooget Olá MongoDB de uma variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f19a9-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="f19a9-229">Configurando seu computador de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="f19a9-229">Configuring your Development Machine</span></span>
<span data-ttu-id="f19a9-230">Agora vamos em sua máquina de desenvolvimento vinculada a máquina virtual do toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="f19a9-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="f19a9-231">Isso é tão simple quanto adicionar repositório bare Olá na máquina virtual de saudação como um controle remoto.</span><span class="sxs-lookup"><span data-stu-id="f19a9-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="f19a9-232">Execute Olá toodo de comando a seguir (substituindo *usuário* com seu nome de logon de máquina virtual de front-end da web e *machinename* e *região* conforme apropriado):</span><span class="sxs-lookup"><span data-stu-id="f19a9-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="f19a9-233">Isso é tudo o que é necessário tooenable enviar por push, ou publicar em vigor, alterações de máquina virtual do toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="f19a9-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="f19a9-234">Publicação de atualizações</span><span class="sxs-lookup"><span data-stu-id="f19a9-234">Publishing Updates</span></span>
<span data-ttu-id="f19a9-235">Vamos publicar Olá uma alteração foi feita até o momento para que o aplicativo hello usará sua própria instância do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="f19a9-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="f19a9-236">Você deve ver toothis semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="f19a9-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
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
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="f19a9-237">Depois que esse comando for concluído, tente atualizar o aplicativo hello em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f19a9-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="f19a9-238">Você deve ser capaz de toosee que lista de tarefas Olá apresentada aqui está vazia e não mais toohello empatado compartilhado implantados MongoDB instância.</span><span class="sxs-lookup"><span data-stu-id="f19a9-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="f19a9-239">tutorial de saudação toocomplete, vamos fazer a alteração mais visível e outra.</span><span class="sxs-lookup"><span data-stu-id="f19a9-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="f19a9-240">No computador de desenvolvimento, abra o arquivo de node-todo/public/index.html de saudação usando seu editor favorito.</span><span class="sxs-lookup"><span data-stu-id="f19a9-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="f19a9-241">Localize o cabeçalho de jumbotron Olá e altere o título de saudação do "Eu sou um aholic Todo" muito "eu sou um aholic de tarefas no Azure!".</span><span class="sxs-lookup"><span data-stu-id="f19a9-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="f19a9-242">Agora, vamos confirmar:</span><span class="sxs-lookup"><span data-stu-id="f19a9-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="f19a9-243">Esse tempo, vamos publicar Olá alteração tooAzure antes de enviar a ele tooback toohello do repositório GitHub:</span><span class="sxs-lookup"><span data-stu-id="f19a9-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="f19a9-244">Depois que esse comando for concluído, página da web de atualização de saudação e você verá as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f19a9-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="f19a9-245">Desde que eles tenham uma boas aparência, push Olá alteração toohello back origem remota:</span><span class="sxs-lookup"><span data-stu-id="f19a9-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="f19a9-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f19a9-246">Next Steps</span></span>
<span data-ttu-id="f19a9-247">Este artigo mostrado como tootake um aplicativo Node. js e implantá-lo em máquinas virtuais de tooLinux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="f19a9-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="f19a9-248">toolearn mais sobre máquinas virtuais Linux no Azure, consulte [tooLinux de Introdução no Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="f19a9-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="f19a9-249">Para obter mais informações sobre como toodevelop Node. js aplicativos no Azure, consulte Olá [Node. js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="f19a9-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

