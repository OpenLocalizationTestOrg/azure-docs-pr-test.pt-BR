---
title: aaaSet seu ambiente de desenvolvimento em toowork do Mac OS X com o Azure Service Fabric | Microsoft Docs
description: "Instalar o tempo de execução hello, SDK e as ferramentas e criar um cluster de desenvolvimento local. Depois de concluir esta instalação, você será aplicativos toobuild pronto no Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="6fa6f-104">Configurar seu ambiente de desenvolvimento no Mac OS X</span><span class="sxs-lookup"><span data-stu-id="6fa6f-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fa6f-105">Windows</span><span class="sxs-lookup"><span data-stu-id="6fa6f-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="6fa6f-106">Linux</span><span class="sxs-lookup"><span data-stu-id="6fa6f-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="6fa6f-107">OSX</span><span class="sxs-lookup"><span data-stu-id="6fa6f-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="6fa6f-108">Você pode criar toorun de aplicativos do Service Fabric em clusters do Linux usando o Mac OS X. Este artigo aborda como tooset o Mac para o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fa6f-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6fa6f-109">Prerequisites</span></span>
<span data-ttu-id="6fa6f-110">Serviço de malha não executar nativamente OS X. toorun um cluster local do serviço de malha, fornecemos uma máquina de virtual pré-configurado Ubuntu usando Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="6fa6f-111">Antes de começar, você precisa do:</span><span class="sxs-lookup"><span data-stu-id="6fa6f-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="6fa6f-112">Vagrant (v1.8.4 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="6fa6f-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="6fa6f-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="6fa6f-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="6fa6f-114">Você precisa toouse mutuamente suporte para versões de Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="6fa6f-115">O Vagrant pode se comportar incorretamente em uma versão sem suporte do VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="6fa6f-116">Criar hello VM local</span><span class="sxs-lookup"><span data-stu-id="6fa6f-116">Create hello local VM</span></span>
<span data-ttu-id="6fa6f-117">toocreate Olá VM local que contém um cluster do Service Fabric 5 nós, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fa6f-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="6fa6f-118">Saudação de clone `Vagrantfile` repositório</span><span class="sxs-lookup"><span data-stu-id="6fa6f-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="6fa6f-119">Esta etapa é colocar análises Olá arquivo `Vagrantfile` contendo Olá VM configuração junto com a saudação de local de saudação VM é baixada do.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="6fa6f-120">Navegue toohello clone de local de repositório de saudação</span><span class="sxs-lookup"><span data-stu-id="6fa6f-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="6fa6f-121">(Opcional) Modificar configurações de VM saudação padrão</span><span class="sxs-lookup"><span data-stu-id="6fa6f-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="6fa6f-122">Por padrão, Olá VM local está configurado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6fa6f-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="6fa6f-123">3 GB de memória alocada</span><span class="sxs-lookup"><span data-stu-id="6fa6f-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="6fa6f-124">Rede privada host configurado no IP 192.168.50.50 habilitando a passagem de tráfego de host de Mac Olá</span><span class="sxs-lookup"><span data-stu-id="6fa6f-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="6fa6f-125">Você pode alterar qualquer uma dessas configurações ou adicionar outros toohello configuração VM em Olá `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="6fa6f-126">Consulte Olá [documentação Vagrant](http://www.vagrantup.com/docs) para obter a lista completa Olá das opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="6fa6f-127">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="6fa6f-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="6fa6f-128">Esta etapa baixa a imagem de VM de Olá pré-configurado, inicialização-o localmente e em seguida, configure uma malha local do serviço de cluster nele.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="6fa6f-129">Você deve esperar que ele tootake alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="6fa6f-130">Se a instalação for concluída com êxito, você verá uma mensagem na saída de hello indicando a que esse cluster hello está sendo inicializado.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![A configuração do cluster começa após o provisionamento da VM][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="6fa6f-132">Se o download VM hello está demorando muito tempo, você pode baixá-lo usando wget ou Ondulação ou por meio de um navegador, navegando toohello link especificado por **config.vm.box_url** no arquivo hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="6fa6f-133">Depois de baixar localmente, editar `Vagrantfile` toopoint toohello caminho local onde você baixou a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="6fa6f-134">Por exemplo se você baixou Olá imagem too/home/users/test/azureservicefabric.tp8.box, em seguida, definir **config.vm.box_url** toothat caminho.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="6fa6f-135">Testar esse Olá cluster foi configurado corretamente, navegando tooService Fabric Explorer no http://192.168.50.50:19080/Explorer (supondo que mantidos IP de rede privada de padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="6fa6f-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric Explorer exibido a partir do host de saudação Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="6fa6f-137">Criar um aplicativo Mac usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="6fa6f-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="6fa6f-138">O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo do Service Fabric no terminal usando gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="6fa6f-139">Siga as etapas de saudação abaixo tooensure que têm o gerador de modelo yeoman Service Fabric Olá trabalhando em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="6fa6f-140">Você precisará toohave Node. js e NPM mac é instalado.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="6fa6f-141">Se não é possível instalar Node. js e NPM usando Homebrew usando os seguintes hello.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="6fa6f-142">versões de saudação do toocheck do Node. js e NPM instalado no seu Mac, você pode usar o hello ``-v`` opção.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="6fa6f-143">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="6fa6f-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="6fa6f-144">Instalar Olá Yeoman gerador você deseja toouse, seguindo as etapas de Olá Olá Introdução [documentação](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6fa6f-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="6fa6f-145">Aplicativos de malha do serviço toocreate usando Yeoman, execute as etapas de saudação-</span><span class="sxs-lookup"><span data-stu-id="6fa6f-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="6fa6f-146">toobuild um aplicativo de serviço do Fabric Java no Mac, você precisaria - JDK 1.8 e instalado na máquina de saudação do Gradle.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="6fa6f-147">Instalar o plug-in do Service Fabric Olá para Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="6fa6f-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="6fa6f-148">Serviço de malha fornece um plug-in para Olá **Neon Eclipse para Java IDE** que pode simplificar o processo de saudação de criar, compilar e implantar serviços de Java.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="6fa6f-149">Você pode seguir etapas de instalação Olá mencionadas neste geral [documentação](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sobre como instalar ou atualizar o plug-in do Eclipse de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="6fa6f-150">Por padrão oferecemos suporte a saudação padrão IP conforme mencionado em Olá ``Vagrantfile`` em Olá ``Local.json`` do aplicativo hello gerado.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="6fa6f-151">No caso de você alterá-la e implantar Vagrant com um IP diferente, atualize o IP de saudação correspondente no ``Local.json`` do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6fa6f-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fa6f-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fa6f-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="6fa6f-153">Criar e implantar seu primeiro aplicativo Java de do Service Fabric no Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="6fa6f-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="6fa6f-154">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in do Service Fabric para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="6fa6f-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="6fa6f-155">Criar um cluster do Service Fabric no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6fa6f-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="6fa6f-156">Criar um cluster do Service Fabric usando hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6fa6f-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="6fa6f-157">Entender o modelo de aplicativo do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="6fa6f-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
