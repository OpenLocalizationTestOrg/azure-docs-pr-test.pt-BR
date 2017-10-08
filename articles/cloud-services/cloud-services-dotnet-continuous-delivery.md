---
title: "Serviços de entrega de aaaContinuous para a nuvem com o TFS no Azure | Microsoft Docs"
description: "Saiba como aplicativos de nuvem tooset a entrega contínua para o Azure. Exemplos de código para instruções de linha de comando do MSBuild e scripts do PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="9e3a0-104">Fornecimento contínuo de serviços de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="9e3a0-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="9e3a0-105">Olá processo descrito neste artigo mostra como tooset a entrega contínua para aplicativos de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="9e3a0-106">Esse processo permite que você crie automaticamente os pacotes e implantar Olá pacote tooAzure após cada check-in do código.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="9e3a0-107">Olá, processo de compilação do pacote descrito neste artigo é equivalente toohello **pacote** comando no Visual Studio e as etapas de publicação são equivalente toohello **publicar** comando no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="9e3a0-108">Olá artigo abrange Olá métodos você usaria toocreate um servidor de compilação com instruções de linha de comando do MSBuild e scripts do Windows PowerShell e ele também demonstra como configurar o Visual Studio Team Foundation Server - definições Team Build toooptionally comandos de MSBuild Olá toouse e scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="9e3a0-109">processo de saudação é personalizável para seu ambiente de compilação e ambientes de destino do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="9e3a0-110">Você também pode usar o Visual Studio Team Services, uma versão do TFS que é hospedado no Azure, toodo isso mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="9e3a0-111">Antes de começar, você deve publicar seu aplicativo do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="9e3a0-112">Isso garantirá que todos os recursos de saudação estão disponíveis e inicializado quando você tenta tooautomate processo de publicação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="9e3a0-113">1: configurar Olá servidor de compilação</span><span class="sxs-lookup"><span data-stu-id="9e3a0-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="9e3a0-114">Antes de criar um pacote do Azure usando o MSBuild, você deve instalar o software Olá necessárias e as ferramentas no servidor de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="9e3a0-115">O Visual Studio não é necessário toobe instalado no servidor de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="9e3a0-116">Se você quiser toouse Team Foundation Build Service toomanage seu servidor de compilação, siga as instruções de Olá Olá [Team Foundation Build Service] [ Team Foundation Build Service] documentação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="9e3a0-117">No servidor de compilação hello, instalar Olá [do .NET Framework 4.5.2][.NET Framework 4.5.2], que inclui o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="9e3a0-118">Instalar hello mais recente [ferramentas de criação do Azure para .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="9e3a0-119">Instalar Olá [bibliotecas do Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="9e3a0-120">Copie o arquivo de WebApplication de saudação de um toohello de instalação do Visual Studio criar o servidor.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="9e3a0-121">Em um computador com Visual Studio instalado, esse arquivo está localizado no diretório Olá c:\\arquivos de programa (x86)\\MSBuild\\Microsoft\\VisualStudio\\v 14.0\\aplicativos daWeb.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="9e3a0-122">Você deve copiá-lo toohello mesmo diretório no servidor de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="9e3a0-123">Instalar Olá [ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="9e3a0-124">2: Compilar um Pacote usando comandos MSBuild</span><span class="sxs-lookup"><span data-stu-id="9e3a0-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="9e3a0-125">Esta seção descreve como tooconstruct um MSBuild comando que cria um pacote do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="9e3a0-126">Execute esta etapa no hello tooverify de servidor de compilação que tudo está configurado corretamente e que o comando de MSBuild Olá o que você deseja toodo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="9e3a0-127">Você pode adicionar essa linha de comando tooexisting criar scripts no servidor de compilação hello, ou você pode usar saudação de linha de comando em uma definição de compilação do TFS, conforme descrito na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="9e3a0-128">Para obter mais informações sobre parâmetros de linha de comando e sobre o MSBuild, consulte [Referência de linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="9e3a0-129">Se o Visual Studio está instalado no servidor de compilação hello, localize e selecione **Prompt de comando do Visual Studio** em Olá **ferramentas do Visual Studio** pasta no Windows.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="9e3a0-130">Se o Visual Studio não está instalado no servidor de compilação Olá, abra um prompt de comando e verifique se MSBuild.exe está acessível no caminho.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="9e3a0-131">MSBuild é instalado com a saudação do .NET Framework em Olá caminho % WINDIR %\\Microsoft.NET\\Framework\\*versão*.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="9e3a0-132">Por exemplo, para adicionar a variável de ambiente MSBuild.exe toohello caminho quando você tiver o .NET Framework 4 instalado, digite hello comando no prompt de comando Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="9e3a0-133">No prompt de comando hello, navegue toohello pasta que contém o arquivo de projeto do Azure que você deseja toobuild.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="9e3a0-134">Executar o MSBuild com hello /target: opção como no exemplo a seguir de saudação de publicação:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="9e3a0-135">Essa opção pode ser abreviada como /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="9e3a0-136">opção de /t:Publish Olá no MSBuild não deve ser confundida com comandos de publicação Olá disponíveis no Visual Studio quando você tiver hello que Azure SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="9e3a0-137">Olá /t: opção de publicação somente compilações Olá pacotes do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="9e3a0-138">Não implanta pacotes de saudação assim como os comandos do hello publicar no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="9e3a0-139">Opcionalmente, você pode especificar o nome do projeto hello como um parâmetro de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="9e3a0-140">Se não for especificado, o diretório atual da saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="9e3a0-141">Para saber mais sobre as opções da linha de comando, veja [Referência da linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="9e3a0-142">Localize a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-142">Locate hello output.</span></span> <span data-ttu-id="9e3a0-143">Por padrão, este comando cria um diretório na relação toohello pasta raiz do projeto Olá, como *ProjectDir*\\bin\\*configuração* \\ App.Publish\\.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="9e3a0-144">Quando você compila um projeto do Azure, você deve gerar dois arquivos, o próprio arquivo de pacote hello e Olá que acompanha o arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="9e3a0-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="9e3a0-145">Project.cspkg</span></span>
   * <span data-ttu-id="9e3a0-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="9e3a0-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="9e3a0-147">Por padrão, cada projeto do Azure inclui um arquivo de configuração de serviço (arquivo .cscfg) para compilações locais (depuração) e outro para compilações de nuvem (de preparo ou produção), mas você pode adicionar ou remover arquivos de configuração de serviço conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="9e3a0-148">Quando você criar um pacote do Visual Studio, você será solicitado que tooinclude de arquivo de configuração de serviço junto com o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="9e3a0-149">Especifique o arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-149">Specify hello service configuration file.</span></span> <span data-ttu-id="9e3a0-150">Quando você criar um pacote usando o MSBuild, o arquivo de configuração do serviço local hello está incluído por padrão.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="9e3a0-151">tooinclude um arquivo de configuração de serviço diferentes, defina a propriedade TargetProfile do comando de MSBuild hello, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="9e3a0-152">Especifique o local de saudação para saída de hello.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-152">Specify hello location for hello output.</span></span> <span data-ttu-id="9e3a0-153">Definir o caminho de saudação usando o /p: publishdir =*diretório* \\ opção, incluindo Olá separador de barra invertida, como no exemplo a seguir de saudação à direita:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="9e3a0-154">Depois de criada e testada uma MSBuild apropriado toobuild de linha de comando seus projetos e combiná-los em um pacote do Azure, você pode adicionar scripts de compilação de tooyour essa linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="9e3a0-155">Se seu servidor de compilação usar scripts personalizados, esse processo dependerá das especificidades de seu processo de compilação personalizado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="9e3a0-156">Se você estiver usando o TFS como um ambiente de compilação, você pode seguir instruções Olá Olá próxima etapa tooadd Olá pacote do Azure compilação tooyour processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="9e3a0-157">3: Compilar um Pacote usando o TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9e3a0-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="9e3a0-158">Se você tiver Team Foundation Server (TFS) configurado como um controlador de compilação e hello criar servidor configurado como um computador de compilação do TFS, opcionalmente, você pode configurar uma compilação automatizada para seu pacote do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="9e3a0-159">Para obter informações sobre como tooset backup e usar o Team Foundation server como um sistema de compilação, consulte [seu sistema de compilação em expansão][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="9e3a0-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="9e3a0-160">Em particular, o procedimento a seguir supõe que você configurou seu servidor de compilação conforme descrito em [implantar e configurar um servidor de compilação][Deploy and configure a build server], e que você tenha criado um projeto de equipe criado uma nuvem projeto de serviço no projeto de equipe hello.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="9e3a0-161">tooconfigure TFS toobuild Azure pacotes, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="9e3a0-162">No Visual Studio no computador de desenvolvimento, no menu de exibição hello, escolha **Team Explorer**, ou escolha Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="9e3a0-163">Na janela do Team Explorer, expanda Olá **cria** nó ou escolha Olá **cria** página e selecione **nova definição de compilação**.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opção Nova Definição de Compilação][0]
2. <span data-ttu-id="9e3a0-165">Escolha Olá **gatilho** guia e, em seguida, especifique a saudação desejado condições para quando você quiser Olá toobe pacote criado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="9e3a0-166">Por exemplo, especificar **integração contínua** ocorre de pacote de saudação toobuild sempre que o check-in de controle de uma origem.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="9e3a0-167">Escolha Olá **configurações de fonte de** guia e certifique-se de sua pasta de projeto está listada na Olá **pasta de controle de origem** coluna, e o status de saudação é **Active**.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="9e3a0-168">Escolha Olá **padrões de compilação** guia e no controlador de compilação, verifique o nome de saudação do servidor de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="9e3a0-169">Além disso, escolha a opção de saudação **seguinte de toohello de saída de compilação de cópia Remover pasta** e especifique o local de destino Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="9e3a0-170">Escolha Olá **processo** guia. Na guia do processo hello, escolher o modelo de padrão de saudação, em **criar**, escolha o projeto de saudação se não ainda estiver selecionada e expanda Olá **avançado** seção Olá **Build**seção da grade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="9e3a0-171">Escolha **argumentos de MSBuild**e defina os argumentos de linha de comando do MSBuild apropriados Olá conforme descrito na etapa 2 acima.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="9e3a0-172">Por exemplo, digite **/t: publicar /p: publishdir =\\\\myserver\\descarta\\**  toobuild um pacote de saudação do pacote e copiar arquivos de local de toohello \\ \\myserver\\descarta\\:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Argumentos do MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="9e3a0-174">Copiando Olá arquivos tooa compartilhamento público torna mais fácil toomanually implantar pacotes de saudação do seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="9e3a0-175">Testar o sucesso de saudação da etapa de compilação verificando-se em um projeto de tooyour de alteração ou enfileirar uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="9e3a0-176">tooqueue a uma nova compilação no Team Explorer, clique com botão direito **todas as definições de compilação,** e, em seguida, escolha **enfileirar nova compilação**.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="9e3a0-177">4: Publicar um Pacote usando um Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e3a0-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="9e3a0-178">Esta seção descreve como tooconstruct um script do Windows PowerShell que publicará o pacote de aplicativos de nuvem Olá saída tooAzure usando parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="9e3a0-179">Esse script pode ser chamado após a etapa de compilação de saudação na sua automação de compilação personalizada.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="9e3a0-180">Ele também pode ser chamado das atividades do fluxo de trabalho do Modelo de processo no Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="9e3a0-181">Instalar Olá [cmdlets do PowerShell do Azure] [ Azure PowerShell cmdlets] (v0.6.1 ou superior).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="9e3a0-182">Durante a fase de instalação do cmdlet hello, escolha tooinstall como um snap-in.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="9e3a0-183">Observe que esta versão com suporte oficialmente substitui a versão mais antiga do hello oferecido por meio do CodePlex, embora as versões anteriores do hello foram numeradas 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="9e3a0-184">Inicie o PowerShell do Azure usando o menu de início de saudação ou página inicial.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="9e3a0-185">Se você iniciar dessa forma, Olá cmdlets do PowerShell do Azure será carregado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="9e3a0-186">No prompt do PowerShell hello, verifique se Olá cmdlets do PowerShell são carregados digitando o comando parcial Olá `Get-Azure` e, em seguida, pressionar Olá a tecla Tab para conclusão de instrução.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="9e3a0-187">Se você pressionar a tecla Tab de saudação repetidamente, você verá vários comandos do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="9e3a0-188">Verifique se que você pode conectar tooyour assinatura do Azure importando as informações de assinatura de arquivo. publishsettings de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="9e3a0-189">Em seguida, insira o comando Olá</span><span class="sxs-lookup"><span data-stu-id="9e3a0-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="9e3a0-190">Isso mostra informações sobre sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-190">This shows information about your subscription.</span></span> <span data-ttu-id="9e3a0-191">Verifique se tudo está correto.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="9e3a0-192">Salvar modelo de script hello fornecido no final da saudação deste artigo para a pasta de scripts, como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="9e3a0-193">Examine a seção de parâmetros de saudação do script hello.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="9e3a0-194">Adicione ou modifique os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-194">Add or modify any default values.</span></span> <span data-ttu-id="9e3a0-195">Esses valores podem ser substituídos sempre passando parâmetros explícitos.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="9e3a0-196">Certifique-se de serviço de nuvem válido e não contas de armazenamento criadas na sua assinatura que pode ser afetada por Olá script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="9e3a0-197">A conta de armazenamento (armazenamento de blob) será usado tooupload e armazenar temporariamente o arquivo de pacote e a configuração de implantação de saudação durante a implantação está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="9e3a0-198">toocreate um novo serviço de nuvem, você pode chamar esse script ou Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9e3a0-199">nome do serviço de nuvem Olá será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, ele deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="9e3a0-200">toocreate uma nova conta de armazenamento, você pode chamar esse script ou Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9e3a0-201">o nome de conta de armazenamento Olá será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, ele deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="9e3a0-202">Você pode tentar usar Olá mesmo nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="9e3a0-203">Chamar o script hello diretamente do PowerShell do Azure ou conectar este toooccur de automação de compilação do script tooyour host após a compilação do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9e3a0-204">script Hello serão sempre excluir ou substituir as implantações existentes por padrão, se eles são detectados.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9e3a0-205">Isso é necessário para habilitar o fornecimento contínuo de automação onde não é possível nenhum aviso ao usuário.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="9e3a0-206">**Cenário de exemplo 1:** toohello implantação contínua preparação do ambiente de serviço:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9e3a0-207">Isso é normalmente seguido pela verificação da execução de teste e uma troca de VIP.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="9e3a0-208">permuta de VIP de saudação pode ser feita por meio de saudação [portal do Azure](https://portal.azure.com) ou usando o cmdlet Olá Move-implantação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="9e3a0-209">**Cenário de exemplo 2:** ambiente de produção toohello implantação contínua de um serviço de teste dedicados</span><span class="sxs-lookup"><span data-stu-id="9e3a0-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9e3a0-210">**Área de trabalho remota:**</span><span class="sxs-lookup"><span data-stu-id="9e3a0-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="9e3a0-211">Se a área de trabalho remota está habilitada no seu projeto do Azure, você precisará tooperform etapas única adicionais Olá tooensure que certificado de serviço de nuvem correto é carregado tooall serviços de nuvem direcionados por esse script.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="9e3a0-212">Localize valores de impressão digital do certificado Olá esperados por suas funções.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="9e3a0-213">Os valores de impressão digital são visíveis na seção de certificados de saudação do arquivo de configuração de nuvem (ou seja, ServiceConfiguration).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="9e3a0-214">Também é visível na caixa de diálogo de configuração da área de trabalho remota de saudação no Visual Studio quando você Mostrar opções e exibir hello selecionado certificado.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="9e3a0-215">Carregar certificados de área de trabalho remota como uma etapa de configuração única usando Olá cmdlet script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="9e3a0-216">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="9e3a0-217">Como alternativa, você pode exportar arquivo de certificado PFX Olá com chave privada e carregar certificados tooeach serviço de destino nuvem usando o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="9e3a0-218">**Atualizar implantação vs. Excluir Implantação -\> Nova Implantação**</span><span class="sxs-lookup"><span data-stu-id="9e3a0-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="9e3a0-219">Olá script por padrão executará uma implantação de atualização ($enableDeploymentUpgrade = 1) quando nenhum parâmetro é passado ou o valor 1 é passado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="9e3a0-220">Para instâncias únicas isso tem a vantagem de levar menos tempo do que uma implantação completa.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="9e3a0-221">Para instâncias que exigem alta disponibilidade, que isso também tem a vantagem de saudação de deixar algumas instâncias em execução enquanto outros são atualizadas (percorrer seu domínio de atualização), além de seu VIP não será excluído.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="9e3a0-222">Implantação de atualização pode ser desabilitada no script hello ($enableDeploymentUpgrade = 0) ou passando *- enableDeploymentUpgrade 0* como um parâmetro, que altera a exclusão do script comportamento toofirst qualquer implantação existente e, em seguida, criar um nova implantação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9e3a0-223">script Hello serão sempre excluir ou substituir as implantações existentes por padrão, se eles são detectados.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9e3a0-224">Isso é necessário para habilitar o fornecimento contínuo de automação onde é possível sem nenhum aviso ao usuário/operador.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="9e3a0-225">5: Publicar um Pacote usando o TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9e3a0-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="9e3a0-226">Esta etapa opcional conecta o TFS Team Build toohello script criado na etapa 4, que manipula a publicação de tooAzure de compilação do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="9e3a0-227">Isso envolve a modificação Olá usada por sua definição de compilação para que ele executa uma atividade de publicação no final de saudação do fluxo de trabalho de saudação do modelo de processo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="9e3a0-228">Hello atividade publicar executará o comando PowerShell passando parâmetros de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="9e3a0-229">Saída de hello MSBuild tem como alvo e script de publicação será conectada na saída de compilação padrão hello.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="9e3a0-230">Editar saudação definição de compilação responsável por contínua implantar.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="9e3a0-231">Selecione Olá **processo** guia.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="9e3a0-232">Execute [estas instruções](http://msdn.microsoft.com/library/dd647551.aspx) tooadd um projeto de atividade para hello criar modelo de processo, baixe o modelo padrão de saudação, adicioná-lo ao projeto Olá e check-in.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="9e3a0-233">Dê um novo nome, como AzureBuildProcessTemplate de modelo de processo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="9e3a0-234">Retornar toohello **processo** guia e usar **Mostrar detalhes** tooshow uma lista de modelos de processo de compilação disponível.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="9e3a0-235">Escolha Olá **New...**  botão e, em seguida, navegue toohello projeto recém-adicionado e check-in.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="9e3a0-236">Localize o modelo Olá recém-criado e escolha **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="9e3a0-237">Abra Olá selecionada do modelo de processo para edição.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="9e3a0-238">Você pode abrir diretamente no designer de fluxo de trabalho de saudação ou no hello toowork de editor de XML com hello XAML.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="9e3a0-239">Adicione Olá lista de argumentos novos a seguir como itens separados de linha na guia de argumentos de saudação do designer de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="9e3a0-240">Todos os argumentos devem ter direção =In e digite =String.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="9e3a0-241">Esses serão usados tooflow parâmetros da definição de compilação Olá no fluxo de trabalho hello, quais Olá de toocall usado get, em seguida, o script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   <span data-ttu-id="9e3a0-243">Olá que correspondente XAML tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="9e3a0-244">Adicione uma nova sequência de final de saudação do executar no agente:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="9e3a0-245">Comece adicionando um toocheck de atividade de instrução If para um arquivo de script válida.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="9e3a0-246">Defina o valor de toothis de condição de saudação:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="9e3a0-247">Em Olá caso de Olá instrução If, adicione uma nova atividade de sequência.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="9e3a0-248">Publicar too'Start de nome de exibição do conjunto de saudação '</span><span class="sxs-lookup"><span data-stu-id="9e3a0-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="9e3a0-249">Com hello início publicar sequência ainda selecionada, adicione a seguinte lista de novas variáveis como itens separados de linha na guia variáveis de designer de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="9e3a0-250">Todas as variáveis devem ter um tipo de Variável =String e Escopo=Início da publicação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="9e3a0-251">Esses serão usados tooflow parâmetros da definição de compilação Olá no fluxo de trabalho, quais Olá de toocall usado get, em seguida, o script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="9e3a0-252">SubscriptionDataFilePath, do tipo String</span><span class="sxs-lookup"><span data-stu-id="9e3a0-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="9e3a0-253">PublishScriptFilePath, do tipo String</span><span class="sxs-lookup"><span data-stu-id="9e3a0-253">PublishScriptFilePath, of type String</span></span>

        ![Novas variáveis][4]
   4. <span data-ttu-id="9e3a0-255">Se você estiver usando o TFS 2012 ou anterior, adicionar uma atividade de ConvertWorkspaceItem no início de saudação do hello nova sequência.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="9e3a0-256">Se você estiver usando o TFS 2013 ou posterior, adicione uma atividade de GetLocalPath no início de saudação da nova sequência de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="9e3a0-257">Para um ConvertWorkspaceItem, definir propriedades de saudação da seguinte maneira: direção = ServerToLocal, DisplayName = 'Converter a publicação de nome de arquivo de script', entrada = 'PublishScriptLocation', resultado = 'PublishScriptFilePath', espaço de trabalho = 'Espaço de trabalho'.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9e3a0-258">Para uma atividade de GetLocalPath, defina Olá propriedade IncomingPath too'PublishScriptLocation', e Olá too'PublishScriptFilePath de resultado '.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="9e3a0-259">Este toohello de caminho hello atividade converte publicar script a partir de locais do servidor TFS (se aplicável) tooa caminho de disco local padrão.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="9e3a0-260">Se você estiver usando o TFS 2012 ou anterior, adicione outra atividade de ConvertWorkspaceItem final Olá Olá nova sequência.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="9e3a0-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9e3a0-262">Se estiver usando o TFS 2013 ou posterior, adicione outra atividade GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="9e3a0-263">IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="9e3a0-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="9e3a0-264">Adicionar uma atividade de InvokeProcess final Olá Olá nova sequência.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="9e3a0-265">Essa chamadas de atividade PowerShell.exe com argumentos Olá passado por Olá definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="9e3a0-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="9e3a0-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="9e3a0-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="9e3a0-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="9e3a0-268">FileName = "PowerShell" (incluir aspas Olá)</span><span class="sxs-lookup"><span data-stu-id="9e3a0-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="9e3a0-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="9e3a0-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="9e3a0-270">Em Olá **tratar saída padrão** seção o InvokeProcess de texto, defina too'data de valor de caixa de texto de saudação '.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="9e3a0-271">Este é um dados de saída padrão de saudação toostore variável.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="9e3a0-272">Adicionar uma atividade WriteBuildMessage logo abaixo Olá **tratar saída padrão** seção.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="9e3a0-273">Definir Olá importância = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' e mensagem de saudação = 'data'.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="9e3a0-274">Isso garante que a saída padrão de saudação do script será gravada toohello saída da compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="9e3a0-275">Em Olá **tratar a saída de erro** seção o InvokeProcess de texto, defina too'data de valor de caixa de texto de saudação '.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="9e3a0-276">Este é um toostore variável de dados de erro padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="9e3a0-277">Adicionar uma atividade WriteBuildError logo abaixo Olá **tratar a saída de erro** seção.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="9e3a0-278">Defina a mensagem de saudação = 'data'.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-278">Set hello Message='data'.</span></span> <span data-ttu-id="9e3a0-279">Isso garante que erros de padrão de saudação do script hello serão gravados toohello saída de erro de compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="9e3a0-280">Corrija quaisquer erros, indicados por sinais de exclamação azuis.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="9e3a0-281">Passe o mouse sobre o pontos de exclamação tooget uma dica sobre o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="9e3a0-282">Salve fluxo de trabalho de saudação para limpar os erros.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="9e3a0-283">resultado final Olá Olá publicar atividades terá esta aparência no designer de saudação do fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Atividades do fluxo de trabalho][5]

   <span data-ttu-id="9e3a0-285">resultado final Olá Olá publicar atividades terá esta aparência em XAML de fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="9e3a0-286">Salve fluxo de trabalho modelo processo de compilação de saudação e Check-In deste arquivo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="9e3a0-287">Editar definição de compilação da saudação (fechá-lo se ele já estiver aberto) e selecione hello **novo** botão se você ainda não ver Olá novo modelo na lista de saudação de modelos de processo.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="9e3a0-288">Defina valores de propriedade de parâmetro de saudação em Olá Misc seção da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9e3a0-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="9e3a0-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Esse valor é derivado de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="9e3a0-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="9e3a0-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Esse valor é derivado de: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="9e3a0-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="9e3a0-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="9e3a0-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="9e3a0-292">ServiceName = 'mycloudservicename' *a nome de serviço de nuvem apropriado de saudação de uso aqui*</span><span class="sxs-lookup"><span data-stu-id="9e3a0-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="9e3a0-293">Ambiente = 'Teste'</span><span class="sxs-lookup"><span data-stu-id="9e3a0-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="9e3a0-294">StorageAccountName = 'mystorageaccountname' *a nome de conta de armazenamento apropriado de saudação de uso aqui*</span><span class="sxs-lookup"><span data-stu-id="9e3a0-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="9e3a0-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="9e3a0-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="9e3a0-296">SubscriptionName = 'padrão'</span><span class="sxs-lookup"><span data-stu-id="9e3a0-296">SubscriptionName = 'default'</span></span>

    ![Valores de propriedade do parâmetro][6]
11. <span data-ttu-id="9e3a0-298">Salve alterações de saudação toohello definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="9e3a0-299">Fila tooexecute uma compilação ambos Olá compilação do pacote e publicação.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="9e3a0-300">Se você tiver um gatilho definido tooContinuous integração, você executará esse comportamento em cada check-in.</span><span class="sxs-lookup"><span data-stu-id="9e3a0-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="9e3a0-301">Modelo de script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="9e3a0-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="9e3a0-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e3a0-302">Next steps</span></span>
<span data-ttu-id="9e3a0-303">depuração remota tooenable ao usar a entrega contínua, consulte [habilitar a depuração remota ao usar a entrega contínua toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="9e3a0-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
