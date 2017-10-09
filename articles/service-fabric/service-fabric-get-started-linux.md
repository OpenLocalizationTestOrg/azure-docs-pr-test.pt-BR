---
title: aaaSet seu ambiente de desenvolvimento no Linux | Microsoft Docs
description: "Instalar o tempo de execução de saudação e SDK e criar um cluster de desenvolvimento local no Linux. Depois de concluir esta instalação, você será aplicativos toobuild pronto."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="07512-104">Preparar seu ambiente de desenvolvimento no Linux</span><span class="sxs-lookup"><span data-stu-id="07512-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07512-105">Windows</span><span class="sxs-lookup"><span data-stu-id="07512-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="07512-106">Linux</span><span class="sxs-lookup"><span data-stu-id="07512-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="07512-107">OSX</span><span class="sxs-lookup"><span data-stu-id="07512-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="07512-108">toodeploy e executar [aplicativos do Azure Service Fabric](service-fabric-application-model.md) em sua máquina de desenvolvimento do Linux, instalar o runtime do hello e SDK comuns.</span><span class="sxs-lookup"><span data-stu-id="07512-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="07512-109">Você também pode instalar os SDKs opcionais para Java e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="07512-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07512-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07512-110">Prerequisites</span></span>

<span data-ttu-id="07512-111">Olá versões de sistemas operacionais a seguir têm suporte para desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="07512-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="07512-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="07512-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="07512-113">Atualizar suas fontes APT</span><span class="sxs-lookup"><span data-stu-id="07512-113">Update your APT sources</span></span>
<span data-ttu-id="07512-114">tooinstall Olá SDK e hello em tempo de execução associado pacote por meio da ferramenta de linha de comando de apt get hello, primeiro você deve atualizar suas fontes de ferramenta de empacotamento avançadas (APT).</span><span class="sxs-lookup"><span data-stu-id="07512-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="07512-115">Abra um terminal.</span><span class="sxs-lookup"><span data-stu-id="07512-115">Open a terminal.</span></span>
2. <span data-ttu-id="07512-116">Adicione lista de fontes de saudação do Service Fabric repositório tooyour.</span><span class="sxs-lookup"><span data-stu-id="07512-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="07512-117">Adicionar Olá `dotnet` lista de fontes de tooyour do repositório.</span><span class="sxs-lookup"><span data-stu-id="07512-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="07512-118">Adicionar Olá APT tooyour de token de autenticação de chave de nova proteção de privacidade do Gnu (GnuPG ou GPG).</span><span class="sxs-lookup"><span data-stu-id="07512-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="07512-119">Adicione Olá oficial GPG Docker tooyour chave APT token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="07512-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="07512-120">Configure o repositório de Docker hello.</span><span class="sxs-lookup"><span data-stu-id="07512-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="07512-121">O pacote de atualização de lista com base nas Olá recentemente adicionado repositórios.</span><span class="sxs-lookup"><span data-stu-id="07512-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="07512-122">Instalar e configurar o hello SDK para a instalação de cluster local</span><span class="sxs-lookup"><span data-stu-id="07512-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="07512-123">Depois de atualizar as fontes, você pode instalar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="07512-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="07512-124">Instalar o pacote do SDK do Service Fabric hello, Confirmar instalação hello e aceitar o contrato de licença de toohello.</span><span class="sxs-lookup"><span data-stu-id="07512-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="07512-125">Olá, comandos a seguir automatizam aceitando licença Olá para pacotes de malha do serviço:</span><span class="sxs-lookup"><span data-stu-id="07512-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="07512-126">Configurar um cluster local</span><span class="sxs-lookup"><span data-stu-id="07512-126">Set up a local cluster</span></span>
  <span data-ttu-id="07512-127">Se Olá instalação for bem-sucedida, você deve ser capaz de toostart um cluster local.</span><span class="sxs-lookup"><span data-stu-id="07512-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="07512-128">Execute o script de instalação de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="07512-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="07512-129">Abra um navegador da web e vá muito[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="07512-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="07512-130">Se Olá cluster foi iniciado, você deverá ver o painel do Gerenciador do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="07512-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer no Linux][sfx-linux]

  <span data-ttu-id="07512-132">Neste ponto, você é capaz de implantar os pacotes do aplicativo Service Fabric predefinidos ou novos com base nos contêineres ou executáveis do convidado.</span><span class="sxs-lookup"><span data-stu-id="07512-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="07512-133">toobuild novos serviços usando Olá Java ou .NET Core SDKs, execute as etapas de configuração opcional de saudação que são fornecidas nas seções subsequentes.</span><span class="sxs-lookup"><span data-stu-id="07512-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="07512-134">Não há suporte para os clusters autônomos no Linux.</span><span class="sxs-lookup"><span data-stu-id="07512-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="07512-135">Olá visualização dá suporte a apenas uma caixa e clusters de vários computadores Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="07512-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="07512-136">Configurar Olá CLI de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="07512-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="07512-137">Olá [CLI de malha do serviço](service-fabric-cli.md) tem comandos para interagir com entidades de malha do serviço, incluindo clusters e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07512-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="07512-138">Ela se baseia em python, portanto, se toohave python e pip instalado antes de prosseguir com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="07512-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="07512-139">Instalar e configurar os geradores de saudação para contêineres e executáveis de convidado</span><span class="sxs-lookup"><span data-stu-id="07512-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="07512-140">O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo do Service Fabric no terminal usando gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="07512-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="07512-141">Siga as etapas de saudação abaixo tooensure que têm o gerador de modelo yeoman Olá Service Fabric para trabalhar em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07512-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="07512-142">Instalar o nodejs e o NPM em seu computador</span><span class="sxs-lookup"><span data-stu-id="07512-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="07512-143">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="07512-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="07512-144">Instalar gerador de contêiner de serviço malha Yeo hello e gerador de execuatble guest de NPM</span><span class="sxs-lookup"><span data-stu-id="07512-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="07512-145">Depois que você instalou Olá acima geradores, você deve ser capaz de toocreate aplicativos com serviços de contêiner ou um executável de convidado executando `yo azuresfguest` ou `yo azuresfcontainer` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="07512-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="07512-146">Instalar Olá Java artefatos necessários (opcionais, se você quiser toouse Olá Java modelos de programação)</span><span class="sxs-lookup"><span data-stu-id="07512-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="07512-147">Serviços de malha do serviço toobuild usando Java, certifique-se de ter 1.8 JDK instalado junto com o Gradle que é usado para executar tarefas de compilação.</span><span class="sxs-lookup"><span data-stu-id="07512-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="07512-148">saudação de trecho de código a seguir instala abrir 1.8 JDK junto com Gradle.</span><span class="sxs-lookup"><span data-stu-id="07512-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="07512-149">bibliotecas do Service Fabric Java Olá são extraídas da Maven.</span><span class="sxs-lookup"><span data-stu-id="07512-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="07512-150">Instalar Olá Eclipse Neon plug-in (opcional)</span><span class="sxs-lookup"><span data-stu-id="07512-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="07512-151">Você pode instalar Olá plug-in do Eclipse para a malha do serviço de dentro de saudação **IDE do Eclipse para desenvolvedores de Java**.</span><span class="sxs-lookup"><span data-stu-id="07512-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="07512-152">Você pode usar aplicativos executáveis do Eclipse toocreate Service Fabric convidado e aplicativos de contêiner em aplicativos de malha Java tooService adição.</span><span class="sxs-lookup"><span data-stu-id="07512-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="07512-153">No Eclipse, certifique-se de ter Neon mais recente do Eclipse e Olá a versão mais recente do Buildship (1.0.17 ou posterior) instalado.</span><span class="sxs-lookup"><span data-stu-id="07512-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="07512-154">Você pode verificar as versões de saudação dos componentes instalados selecionando **ajuda** > **detalhes da instalação**.</span><span class="sxs-lookup"><span data-stu-id="07512-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="07512-155">Você pode atualizar Buildship usando instruções Olá em [Buildship Eclipse: Plug-ins do Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="07512-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="07512-156">tooinstall Olá selecione plug-in do Service Fabric **ajuda** > **instalar novo Software**.</span><span class="sxs-lookup"><span data-stu-id="07512-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="07512-157">Em Olá **trabalhar com** , digite **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="07512-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="07512-158">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07512-158">Click **Add**.</span></span>

    ![página de Software disponíveis Olá][sf-eclipse-plugin]

5. <span data-ttu-id="07512-160">Selecione Olá **ServiceFabric** plug-in e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07512-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="07512-161">Conclua as etapas de instalação hello e, em seguida, aceite o contrato de licença de usuário final de saudação.</span><span class="sxs-lookup"><span data-stu-id="07512-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="07512-162">Se você já tiver Olá plug-in Eclipse de malha do serviço instalado, verifique se você tem a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="07512-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="07512-163">Você pode verificar selecionando **ajuda** > **detalhes da instalação** e procurando Service Fabric na lista de saudação do instalado plug-ins. Se uma versão mais recente estiver disponível, selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="07512-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="07512-164">Para obter mais informações, consulte [Plug-in Service Fabric para o desenvolvimento de aplicativos Java do Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="07512-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="07512-165">Instalar Olá .NET Core SDK (opcional, se desejar que os modelos de programação toouse Olá .NET Core)</span><span class="sxs-lookup"><span data-stu-id="07512-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="07512-166">Olá .NET Core SDK fornece bibliotecas hello e modelos de serviços do Service Fabric toobuild necessária com .NET Core.</span><span class="sxs-lookup"><span data-stu-id="07512-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="07512-167">Instalar pacote do SDK do .NET Core Olá em execução a seguir Olá-</span><span class="sxs-lookup"><span data-stu-id="07512-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="07512-168">Saudação de atualização SDK e o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="07512-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="07512-169">versão mais recente do tooupdate toohello de saudação SDK e o tempo de execução, execute Olá comandos a seguir (desmarque Olá SDKs que você não deseja):</span><span class="sxs-lookup"><span data-stu-id="07512-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="07512-170">binários do Java SDK tooupdate saudação do Maven, você precisa tooupdate detalhes de versão de saudação do binário correspondente de saudação em hello ``build.gradle`` versão mais recente do arquivo toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="07512-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="07512-171">tooknow exatamente onde você precisa de tooupdate Olá versão, você pode consultar tooany ``build.gradle`` arquivo nos exemplos de guia de Introdução do Service Fabric [aqui](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="07512-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="07512-172">Atualizando pacotes de saudação pode causar o toostop de cluster de desenvolvimento local em execução.</span><span class="sxs-lookup"><span data-stu-id="07512-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="07512-173">Reinicie o cluster local após uma atualização seguindo as instruções de saudação nesta página.</span><span class="sxs-lookup"><span data-stu-id="07512-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07512-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07512-174">Next steps</span></span>

* [<span data-ttu-id="07512-175">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o Yeoman</span><span class="sxs-lookup"><span data-stu-id="07512-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="07512-176">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in Service Fabric para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="07512-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="07512-177">Criar seu primeiro aplicativo do CSharp no Linux</span><span class="sxs-lookup"><span data-stu-id="07512-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="07512-178">Preparar seu ambiente de desenvolvimento no OSX</span><span class="sxs-lookup"><span data-stu-id="07512-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="07512-179">Usar Olá CLI de malha do serviço toomanage seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="07512-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="07512-180">Diferenças Windows/Linux do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07512-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="07512-181">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="07512-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
