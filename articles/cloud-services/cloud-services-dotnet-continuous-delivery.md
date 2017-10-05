---
title: "Entrega contínua de serviços de nuvem com TFS no Azure | Microsoft Docs"
description: "Saiba como configurar a entrega contínua para aplicativos de nuvem do Azure. Exemplos de código para instruções de linha de comando do MSBuild e scripts do PowerShell."
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="9741f-104">Fornecimento contínuo de serviços de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="9741f-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="9741f-105">O processo descrito neste artigo mostra como configurar o fornecimento contínuo de aplicativos na nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="9741f-106">Este processo permite criar pacotes automaticamente e implantar o pacote no Azure após cada verificação de código.</span><span class="sxs-lookup"><span data-stu-id="9741f-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="9741f-107">O processo de compilação do pacote descrito neste artigo equivale ao comando **Package** do Visual Studio, e as etapas de publicação equivalem ao comando **Publish** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9741f-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="9741f-108">O artigo aborda os métodos que você usaria para criar um servidor de compilação com instruções de linha de comando do MSBuild e scripts do Windows PowerShell, além de demonstrar como configurar as definições do Visual Studio Team Foundation Server - Team Build para usar os comandos do MSBuild e os scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9741f-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="9741f-109">O processo é personalizável para o ambiente de compilação e os ambientes de destino do Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="9741f-110">Você também pode usar o Visual Studio Team Services, uma versão do TFS hospedada no Azure, para fazer isso com mais facilidade.</span><span class="sxs-lookup"><span data-stu-id="9741f-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="9741f-111">Antes de começar, você deve publicar seu aplicativo do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9741f-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="9741f-112">Isso garantirá que todos os recursos estejam disponíveis e sejam inicializados quando você tentar automatizar o processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="9741f-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="9741f-113">1: Configurar o Servidor de Build</span><span class="sxs-lookup"><span data-stu-id="9741f-113">1: Configure the Build Server</span></span>
<span data-ttu-id="9741f-114">Antes de criar um pacote do Azure usando o MSBuild, você deve instalar o software e as ferramentas necessárias no servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="9741f-115">O Visual Studio não precisa estar instalado no servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="9741f-116">Se você quiser usar o Team Foundation Build Service para gerenciar o servidor de compilação, siga as instruções na documentação do [Team Foundation Build Service][Team Foundation Build Service].</span><span class="sxs-lookup"><span data-stu-id="9741f-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="9741f-117">No servidor de build, instale o [.NET Framework 4.5.2][.NET Framework 4.5.2], que inclui o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9741f-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="9741f-118">Instale a versão mais recente das [Ferramentas de criação do Azure para .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="9741f-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="9741f-119">Instale as [Bibliotecas do Azure para .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="9741f-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="9741f-120">Copie o arquivo Microsoft.WebApplication.targets de uma instalação do Visual Studio no servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="9741f-121">Em um computador com o Visual Studio instalado, esse arquivo está localizado no diretório C:\\Arquivos de Programas(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="9741f-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="9741f-122">Você deve copiá-lo para o mesmo diretório no servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="9741f-123">Instale as [Ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="9741f-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="9741f-124">2: Compilar um Pacote usando comandos MSBuild</span><span class="sxs-lookup"><span data-stu-id="9741f-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="9741f-125">Esta seção descreve como criar um comando do MSBuild que compila um pacote do Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="9741f-126">Execute esta etapa no servidor de compilação para verificar setudo está configurado corretamente e se o comando do MSBuild faz o que você deseja fazer.</span><span class="sxs-lookup"><span data-stu-id="9741f-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="9741f-127">Você pode adicionar essa linha de comando a scripts de construção existentes no servidor de compilação ou usar a linha de comando em uma definição de compilação do TFS, conforme descrito na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="9741f-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="9741f-128">Para obter mais informações sobre parâmetros de linha de comando e sobre o MSBuild, consulte [Referência de linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9741f-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="9741f-129">Se o Visual Studio estiver instalado no servidor de build, localize e escolha **Prompt de Comando do Studio Visual** na pasta **Ferramentas do Visual Studio** do Windows.</span><span class="sxs-lookup"><span data-stu-id="9741f-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="9741f-130">Se o Visual Studio não estiver instalado no servidor de compilação, abra um prompt de comando e verifique se MSBuild.exe está acessível no caminho.</span><span class="sxs-lookup"><span data-stu-id="9741f-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="9741f-131">O MSBuild é instalado com o .NET Framework no caminho %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span><span class="sxs-lookup"><span data-stu-id="9741f-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="9741f-132">Por exemplo, para adicionar MSBuild.exe à variável de ambiente PATH quando você tem o .NET Framework 4 instalado, digite o seguinte comando no prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="9741f-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="9741f-133">No prompt de comando, navegue até a pasta que contém o arquivo de projeto do Azure que você deseja compilar.</span><span class="sxs-lookup"><span data-stu-id="9741f-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="9741f-134">Execute MSBuild com a opção /target:Publish, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9741f-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="9741f-135">Essa opção pode ser abreviada como /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="9741f-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="9741f-136">A opção /t:Publish no MSBuild não deve ser confundida com os comandos Publicar disponíveis no Visual Studio quando você tem o SDK do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="9741f-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="9741f-137">A opção /t:Publish compila apenas os pacotes do Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="9741f-138">Ela não implanta os pacotes como os comandos Publicar no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9741f-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="9741f-139">Você também pode especificar o nome do projeto como um parâmetro do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9741f-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="9741f-140">Se não for especificado, o diretório atual é usado.</span><span class="sxs-lookup"><span data-stu-id="9741f-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="9741f-141">Para saber mais sobre as opções da linha de comando, veja [Referência da linha de comando do MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9741f-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="9741f-142">Localize a saída.</span><span class="sxs-lookup"><span data-stu-id="9741f-142">Locate the output.</span></span> <span data-ttu-id="9741f-143">Por padrão, esse comando cria um diretório relacionado à pasta raiz do projeto, como *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="9741f-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="9741f-144">Ao criar um projeto do Azure, você gera dois arquivos, o arquivo do pacote propriamente dito e o arquivo de configuração que o acompanha:</span><span class="sxs-lookup"><span data-stu-id="9741f-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="9741f-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="9741f-145">Project.cspkg</span></span>
   * <span data-ttu-id="9741f-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="9741f-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="9741f-147">Por padrão, cada projeto do Azure inclui um arquivo de configuração de serviço (arquivo .cscfg) para compilações locais (depuração) e outro para compilações de nuvem (de preparo ou produção), mas você pode adicionar ou remover arquivos de configuração de serviço conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="9741f-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="9741f-148">Quando compilar um pacote dentro do Visual Studio, você será questionado quanto ao arquivo de configuração de serviço a ser incluído com o pacote.</span><span class="sxs-lookup"><span data-stu-id="9741f-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="9741f-149">Especifique o arquivo de configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="9741f-149">Specify the service configuration file.</span></span> <span data-ttu-id="9741f-150">Quando você compila um pacote usando o MSBuild, o arquivo de configuração de serviço local é incluído por padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="9741f-151">Para incluir um arquivo de configuração de serviço diferente, defina a propriedade TargetProfile do comando MSBuild, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9741f-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="9741f-152">Especifique o local para a saída.</span><span class="sxs-lookup"><span data-stu-id="9741f-152">Specify the location for the output.</span></span> <span data-ttu-id="9741f-153">Defina o caminho usando a opção /p:PublishDir=*Directory*\\, incluindo o separador de barra invertida à direita, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9741f-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="9741f-154">Depois de criar e testar uma linha de comando do MSBuild apropriada para compilar os projetos e integrá-los em um pacote do Azure, você poderá adicionar essa linha de comando aos scripts de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="9741f-155">Se seu servidor de compilação usar scripts personalizados, esse processo dependerá das especificidades de seu processo de compilação personalizado.</span><span class="sxs-lookup"><span data-stu-id="9741f-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="9741f-156">Se estiver usando o TFS como um ambiente de compilação, você poderá seguir as instruções na próxima etapa para adicionar a compilação do pacote do Azure ao processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="9741f-157">3: Compilar um Pacote usando o TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9741f-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="9741f-158">Se você tiver o TFS (Team Foundation Server) configurado como um controlador de compilação e o servidor de compilação estiver configurado como um computador de compilação TFS, você poderá configurar uma compilação automatizada para o pacote do Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="9741f-159">Para obter informações sobre como configurar e usar o Team Foundation Server como um sistema de build, veja [Escalar horizontalmente seu sistema de build][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="9741f-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="9741f-160">Em particular, o procedimento a seguir presume que você configurou seu servidor de build, conforme descrito em [Implantar e configurar um servidor de build][Deploy and configure a build server] e que criou um projeto de equipe e um projeto de serviço de nuvem no projeto de equipe.</span><span class="sxs-lookup"><span data-stu-id="9741f-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="9741f-161">Para configurar o TFS para compilar pacotes do Azure, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9741f-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="9741f-162">No Visual Studio, no computador de desenvolvimento, no menu Exibir , escolha **Team Explorer** ou Ctrl+\\, Ctrl+M.</span><span class="sxs-lookup"><span data-stu-id="9741f-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="9741f-163">Na janela do Team Explorer, expanda o nó **Builds** ou escolha a página **Builds** e escolha **Definição de Nova Compilação**.</span><span class="sxs-lookup"><span data-stu-id="9741f-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Opção Nova Definição de Compilação][0]
2. <span data-ttu-id="9741f-165">Escolha a guia **Gatilho** e especifique as condições desejadas para quando deseja que o pacote seja compilado.</span><span class="sxs-lookup"><span data-stu-id="9741f-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="9741f-166">Por exemplo, especifique **Integração Contínua** para compilar o pacote sempre que um check-in de controle do código-fonte ocorrer.</span><span class="sxs-lookup"><span data-stu-id="9741f-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="9741f-167">Selecione a guia **Configurações de Origem**, e certifique-se de que a pasta do projeto esteja listada na coluna **Pasta do Controle do Código-Fonte** e que o status seja **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="9741f-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="9741f-168">Escolha a guia **Padrões de Compilação** e, em Controlador de compilação, verifique o nome do servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="9741f-169">Além disso, escolha a opção **Copiar resultado da criação para a seguinte pasta** de recebimento e especifique o local de recebimento desejado.</span><span class="sxs-lookup"><span data-stu-id="9741f-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="9741f-170">Escolha a guia **Processo** . Na guia Processo, selecione o modelo padrão, em **Build**, selecione o projeto se ele ainda não estiver selecionado e expanda a seção **Avançado** na seção **Build** da grade.</span><span class="sxs-lookup"><span data-stu-id="9741f-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="9741f-171">Escolha **Argumentos do MSBuild**e defina os argumentos da linha de comando do MSBuild apropriados, conforme descrito na Etapa 2 acima.</span><span class="sxs-lookup"><span data-stu-id="9741f-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="9741f-172">Por exemplo, insira **/t:Publish /p:PublishDir=\\\\meuservidor\\drops\\** para compilar um pacote e copie os arquivos de pacote para o local \\\\meuservidor\\drops\\:</span><span class="sxs-lookup"><span data-stu-id="9741f-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![Argumentos do MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="9741f-174">Copiar os arquivos para um compartilhamento público torna mais fácil implantar manualmente os pacotes do seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9741f-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="9741f-175">Teste o êxito da etapa de compilação fazendo check-in de uma alteração para o projeto ou coloque na fila uma nova compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="9741f-176">Para colocar na fila uma nova compilação, no Team Explorer, clique com o botão direito do mouse em **Todas as Definições de Compilação** e, em seguida, escolha **Colocar Nova Compilação na Fila**.</span><span class="sxs-lookup"><span data-stu-id="9741f-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="9741f-177">4: Publicar um Pacote usando um Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9741f-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="9741f-178">Esta seção descreve como criar um script do Windows PowerShell que publicará a saída do pacote do aplicativo de nuvem para o Azure usando parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="9741f-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="9741f-179">Esse script pode ser chamado após a etapa de compilação na sua automação de compilação personalizada.</span><span class="sxs-lookup"><span data-stu-id="9741f-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="9741f-180">Ele também pode ser chamado das atividades do fluxo de trabalho do Modelo de processo no Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="9741f-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="9741f-181">Instale os [cmdlets do Azure PowerShell][Azure PowerShell cmdlets] (v0.6.1 ou superior).</span><span class="sxs-lookup"><span data-stu-id="9741f-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="9741f-182">Durante a fase de instalação do cmdlet, opte por instalar como um snap-in.</span><span class="sxs-lookup"><span data-stu-id="9741f-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="9741f-183">Observeque essa versão suportada oficialmente substitui a versão mais antigaoferecida por meio do CodePlex, embora as versões anteriores foram numeradas 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="9741f-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="9741f-184">Inicie o PowerShell do Azure usando o menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="9741f-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="9741f-185">Se você iniciar dessa forma, os cmdlets do PowerShell do Azure serão carregados.</span><span class="sxs-lookup"><span data-stu-id="9741f-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="9741f-186">No prompt do PowerShell, verifique se os cmdlets do PowerShell são carregados digitando o comando parcial `Get-Azure` e pressionando a tecla Tab para o preenchimento de declaração.</span><span class="sxs-lookup"><span data-stu-id="9741f-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="9741f-187">Se você pressionar a tecla Tab repetidamente, deverá ver diversos comandos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9741f-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="9741f-188">Verifique se você consegue se conectar à assinatura do Azure importando as informações de assinatura do arquivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="9741f-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="9741f-189">Em seguida, digite o comando</span><span class="sxs-lookup"><span data-stu-id="9741f-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="9741f-190">Isso mostra informações sobre sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9741f-190">This shows information about your subscription.</span></span> <span data-ttu-id="9741f-191">Verifique se tudo está correto.</span><span class="sxs-lookup"><span data-stu-id="9741f-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="9741f-192">Salve o modelo de script fornecido ao final deste artigo em sua pasta de scripts como c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="9741f-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="9741f-193">Consulte a seção de parâmetros do script.</span><span class="sxs-lookup"><span data-stu-id="9741f-193">Review the parameters section of the script.</span></span> <span data-ttu-id="9741f-194">Adicione ou modifique os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-194">Add or modify any default values.</span></span> <span data-ttu-id="9741f-195">Esses valores podem ser substituídos sempre passando parâmetros explícitos.</span><span class="sxs-lookup"><span data-stu-id="9741f-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="9741f-196">Verifique se há contas de serviço de nuvem e de armazenamento válidas criadas na assinatura que possam ser direcionadas pelo script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9741f-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="9741f-197">A conta de armazenamento (armazenamento de blob) será usada para carregar e armazenar temporariamente o arquivo de configuração e o pacote de implantação, enquanto a implantação está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="9741f-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="9741f-198">Para criar um novo serviço de nuvem, você pode chamar esse script ou usar o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9741f-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9741f-199">O nome do serviço de nuvem será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9741f-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="9741f-200">Para criar uma nova conta de armazenamento, você pode chamar esse script ou usar o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9741f-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9741f-201">O nome da conta de armazenamento será usado como um prefixo em um nome de domínio totalmente qualificado e, portanto, deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9741f-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="9741f-202">Você pode tentar usar o mesmo nome que o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9741f-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="9741f-203">Chame o script diretamente do PowerShell do Azure, ou conecte esse script à automação de compilação do host para ocorrer após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="9741f-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9741f-204">O script sempre vai excluir ou substituir as implantações existentes por padrão, se eles forem detectados.</span><span class="sxs-lookup"><span data-stu-id="9741f-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9741f-205">Isso é necessário para habilitar o fornecimento contínuo de automação onde não é possível nenhum aviso ao usuário.</span><span class="sxs-lookup"><span data-stu-id="9741f-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="9741f-206">**Cenário de exemplo 1:** implantação contínua ao ambiente de preparo de um serviço:</span><span class="sxs-lookup"><span data-stu-id="9741f-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9741f-207">Isso é normalmente seguido pela verificação da execução de teste e uma troca de VIP.</span><span class="sxs-lookup"><span data-stu-id="9741f-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="9741f-208">A troca de VIP pode ser feita por meio do [portal do Azure](https://portal.azure.com) ou usando o cmdlet Move-Deployment.</span><span class="sxs-lookup"><span data-stu-id="9741f-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="9741f-209">**Cenário de exemplo 2:** implantação contínua ao ambiente de produção de um serviço de teste dedicado</span><span class="sxs-lookup"><span data-stu-id="9741f-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9741f-210">**Área de trabalho remota:**</span><span class="sxs-lookup"><span data-stu-id="9741f-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="9741f-211">Se a Área de Trabalho Remota estiver habilitada no projeto do Azure, você precisará realizar etapas individuais adicionais para garantir que o certificado de serviço de nuvem seja carregado em todos os serviços de nuvem segmentados por esse script.</span><span class="sxs-lookup"><span data-stu-id="9741f-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="9741f-212">Localize os valores de impressão digital do certificado esperados por suas funções.</span><span class="sxs-lookup"><span data-stu-id="9741f-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="9741f-213">Os valores da impressão digital são visíveis na seção Certificados no arquivo de configuração de nuvem (ou seja, ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="9741f-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="9741f-214">Ela também é visível na caixa de diálogo Configuração de Área de Trabalho Remota no Visual Studio, quando você Mostrar Opções e exibir o certificado selecionado.</span><span class="sxs-lookup"><span data-stu-id="9741f-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="9741f-215">Carregue certificados de Área de Trabalho Remota como uma etapa única de configuração usando o seguinte script de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9741f-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="9741f-216">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9741f-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="9741f-217">Como alternativa, você pode exportar o arquivo de certificado PFX com a chave privada e carregar certificados para cada serviço de nuvem de destino usando o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9741f-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="9741f-218">**Atualizar implantação vs. Excluir Implantação -\> Nova Implantação**</span><span class="sxs-lookup"><span data-stu-id="9741f-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="9741f-219">O script vai, por padrão, executar uma implantação de atualização($enableDeploymentUpgrade = 1) quando nenhum parâmetro for passado ou o valor 1 for passado explicitamente.</span><span class="sxs-lookup"><span data-stu-id="9741f-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="9741f-220">Para instâncias únicas isso tem a vantagem de levar menos tempo do que uma implantação completa.</span><span class="sxs-lookup"><span data-stu-id="9741f-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="9741f-221">Para instâncias que exigem alta disponibilidade, isso também tem a vantagem de deixar algumas instâncias em execução enquanto outras são atualizadas (movimentação de seu domínio de atualização), além de seu VIP não ser excluído.</span><span class="sxs-lookup"><span data-stu-id="9741f-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="9741f-222">A Implantação de Atualização pode ser desabilitada no script ($enableDeploymentUpgrade = 0) ou transmitindo *-enableDeploymentUpgrade 0* como um parâmetro, o que altera o comportamento do script para excluir primeiro qualquer implantação existente e, em seguida, criar uma nova implantação.</span><span class="sxs-lookup"><span data-stu-id="9741f-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9741f-223">O script sempre vai excluir ou substituir as implantações existentes por padrão, se eles forem detectados.</span><span class="sxs-lookup"><span data-stu-id="9741f-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9741f-224">Isso é necessário para habilitar o fornecimento contínuo de automação onde é possível sem nenhum aviso ao usuário/operador.</span><span class="sxs-lookup"><span data-stu-id="9741f-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="9741f-225">5: Publicar um Pacote usando o TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9741f-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="9741f-226">Esta etapa opcional conecta o TFS Team Build ao script criado na etapa 4, que manipula a publicação da compilação do pacote no Azure.</span><span class="sxs-lookup"><span data-stu-id="9741f-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="9741f-227">Isso implica modificar o modelo de processo usado pela sua definição de compilação para que seja executada uma atividade de Publicar no final do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9741f-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="9741f-228">A atividade de Publicar executará o comando PowerShell passando parâmetros da compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="9741f-229">A saída dos destinos do MSBuild e o script de publicação serão redirecionados para a saída de compilação padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="9741f-230">Edite a definição de compilação responsável pela implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="9741f-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="9741f-231">Selecione a guia **Processo** .</span><span class="sxs-lookup"><span data-stu-id="9741f-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="9741f-232">Execute [estas instruções](http://msdn.microsoft.com/library/dd647551.aspx) para adicionar um projeto de atividade ao modelo de processo de compilação, baixe o modelo padrão, adicione-o ao projeto e faça check-in.</span><span class="sxs-lookup"><span data-stu-id="9741f-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="9741f-233">Atribua um novo nome ao modelo de processo de compilação, como AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="9741f-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="9741f-234">Volte à guia **Processo** e use **Mostrar Detalhes** para mostrar uma lista dos modelos de processos de compilação disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9741f-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="9741f-235">Escolha o botão **Novo...** e navegue para o projeto recém-adicionado e faça o check-in.</span><span class="sxs-lookup"><span data-stu-id="9741f-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="9741f-236">Localize o modelo que você acabou de criar e escolha **OK**.</span><span class="sxs-lookup"><span data-stu-id="9741f-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="9741f-237">Abra o modelo de processo selecionado para edição.</span><span class="sxs-lookup"><span data-stu-id="9741f-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="9741f-238">Você pode abrir diretamente no designer de fluxo de trabalho ou no editor de XML para trabalhar como XAML.</span><span class="sxs-lookup"><span data-stu-id="9741f-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="9741f-239">Adicione a seguinte lista de novos argumentos como itens de linha separados na guia de argumentos do designer de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9741f-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="9741f-240">Todos os argumentos devem ter direção =In e digite =String.</span><span class="sxs-lookup"><span data-stu-id="9741f-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="9741f-241">Esses serão usados para parâmetros de fluxo da definição de compilação para o fluxo de trabalho, que, em seguida, é usado para chamar o script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9741f-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista de argumentos][3]

   <span data-ttu-id="9741f-243">O XAML correspondente tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="9741f-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="9741f-244">Adicione uma nova sequência no final do Agente de Execução:</span><span class="sxs-lookup"><span data-stu-id="9741f-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="9741f-245">Comece adicionando uma atividade de declaração If para verificar se há um arquivo de script válido.</span><span class="sxs-lookup"><span data-stu-id="9741f-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="9741f-246">Defina a condição para este valor:</span><span class="sxs-lookup"><span data-stu-id="9741f-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="9741f-247">No caso Then da declaração If, adicione uma nova atividade de sequência.</span><span class="sxs-lookup"><span data-stu-id="9741f-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="9741f-248">Defina o nome de exibição para 'Iniciar publicação'</span><span class="sxs-lookup"><span data-stu-id="9741f-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="9741f-249">Com a sequência de publicação inicial ainda selecionada, adicione a lista a seguir de novas variáveis como itens de linha separadas na guia de variáveis do designer de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9741f-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="9741f-250">Todas as variáveis devem ter um tipo de Variável =String e Escopo=Início da publicação.</span><span class="sxs-lookup"><span data-stu-id="9741f-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="9741f-251">Esses serão usados para parâmetros de fluxo da definição de compilação para o fluxo de trabalho, que, em seguida, é usado para chamar o script de publicação.</span><span class="sxs-lookup"><span data-stu-id="9741f-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="9741f-252">SubscriptionDataFilePath, do tipo String</span><span class="sxs-lookup"><span data-stu-id="9741f-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="9741f-253">PublishScriptFilePath, do tipo String</span><span class="sxs-lookup"><span data-stu-id="9741f-253">PublishScriptFilePath, of type String</span></span>

        ![Novas variáveis][4]
   4. <span data-ttu-id="9741f-255">Se estiver usando o TFS 2012 ou anterior, adicione uma atividade ConvertWorkspaceItem ao início da nova Sequência.</span><span class="sxs-lookup"><span data-stu-id="9741f-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="9741f-256">Se estiver usando o TFS 2013 ou posterior, adicione uma atividade GetLocalPath ao início da nova sequência.</span><span class="sxs-lookup"><span data-stu-id="9741f-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="9741f-257">Para um ConvertWorkspaceItem, defina as propriedades da seguinte maneira: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="9741f-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9741f-258">Para uma atividade GetLocalPath, defina a propriedade IncomingPath como 'PublishScriptLocation’ e o Resultado como 'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="9741f-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="9741f-259">Esta atividade converte o caminho para o script de publicação dos locais do servidor TFS (se aplicável) para um caminho de disco local padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="9741f-260">Se estiver usando o TFS 2012 ou anterior, adicione outra atividade ConvertWorkspaceItem ao final da nova Sequência.</span><span class="sxs-lookup"><span data-stu-id="9741f-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="9741f-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="9741f-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9741f-262">Se estiver usando o TFS 2013 ou posterior, adicione outra atividade GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="9741f-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="9741f-263">IncomingPath='SubscriptionDataFileLocation' e Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="9741f-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="9741f-264">Adicione uma atividade InvokeProcess ao final da nova sequência.</span><span class="sxs-lookup"><span data-stu-id="9741f-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="9741f-265">Essa atividade chama PowerShell.exe com os argumentos passados pela definição de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="9741f-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="9741f-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="9741f-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="9741f-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="9741f-268">FileName = "PowerShell" (incluindo as aspas)</span><span class="sxs-lookup"><span data-stu-id="9741f-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="9741f-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="9741f-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="9741f-270">Na caixa de texto da seção **Gerenciar Saída Padrão** de InvokeProcess, defina o valor da caixa de texto como “ data”.</span><span class="sxs-lookup"><span data-stu-id="9741f-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="9741f-271">Essa é uma variável para armazenar os dados de saída padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="9741f-272">Adicione uma atividade WriteBuildMessage logo abaixo da seção de **Gerenciar Saída Padrão** .</span><span class="sxs-lookup"><span data-stu-id="9741f-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="9741f-273">Defina a importância ='Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High'e a mensagem = 'dados'.</span><span class="sxs-lookup"><span data-stu-id="9741f-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="9741f-274">Isso garante que a saída padrão do script será gravada na saída de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="9741f-275">Na caixa de texto da seção **Gerenciar Erro de Saída** de InvokeProcess, defina o valor da caixa de texto como “data”.</span><span class="sxs-lookup"><span data-stu-id="9741f-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="9741f-276">Essa é uma variável para armazenar os dados de erro padrão.</span><span class="sxs-lookup"><span data-stu-id="9741f-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="9741f-277">Adicione uma atividade WriteBuildError pouco abaixo da seção **Gerenciar Erro de Saída** .</span><span class="sxs-lookup"><span data-stu-id="9741f-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="9741f-278">Defina a mensagem = 'dados'.</span><span class="sxs-lookup"><span data-stu-id="9741f-278">Set the Message='data'.</span></span> <span data-ttu-id="9741f-279">Isso garante que os erros padrões do script serão gravados na saída do erro de compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="9741f-280">Corrija quaisquer erros, indicados por sinais de exclamação azuis.</span><span class="sxs-lookup"><span data-stu-id="9741f-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="9741f-281">Passe o mouse sobre os pontos de exclamação para ver informações sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="9741f-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="9741f-282">Salve o fluxo de trabalho para limpar os erros.</span><span class="sxs-lookup"><span data-stu-id="9741f-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="9741f-283">O resultado final das atividades de fluxo de trabalho de publicação terá a seguinte aparência no designer:</span><span class="sxs-lookup"><span data-stu-id="9741f-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Atividades do fluxo de trabalho][5]

   <span data-ttu-id="9741f-285">O resultado final das atividades de fluxo de trabalho de publicação terá a seguinte aparência neste XAML:</span><span class="sxs-lookup"><span data-stu-id="9741f-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="9741f-286">Salve o fluxo de trabalho do modelo de processo de compilação e o faça check-in deste arquivo.</span><span class="sxs-lookup"><span data-stu-id="9741f-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="9741f-287">Edite a definição de compilação (feche-a se já estiver aberta), e selecione o botão **Novo** se não quiser ver o novo modelo na lista de Modelos de Processo.</span><span class="sxs-lookup"><span data-stu-id="9741f-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="9741f-288">Defina os valores da propriedade do parâmetro na seção Vários como segue:</span><span class="sxs-lookup"><span data-stu-id="9741f-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="9741f-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Esse valor é derivado de: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="9741f-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="9741f-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Esse valor é derivado de: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="9741f-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="9741f-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="9741f-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="9741f-292">ServiceName = 'mycloudservicename' *Use o nome de serviço de nuvem apropriado aqui*</span><span class="sxs-lookup"><span data-stu-id="9741f-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="9741f-293">Ambiente = 'Teste'</span><span class="sxs-lookup"><span data-stu-id="9741f-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="9741f-294">StorageAccountName = 'mystorageaccountname' *Use o nome da conta de armazenamento adequado aqui*</span><span class="sxs-lookup"><span data-stu-id="9741f-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="9741f-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="9741f-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="9741f-296">SubscriptionName = 'padrão'</span><span class="sxs-lookup"><span data-stu-id="9741f-296">SubscriptionName = 'default'</span></span>

    ![Valores de propriedade do parâmetro][6]
11. <span data-ttu-id="9741f-298">Salve as alterações para a Definição de Compilação.</span><span class="sxs-lookup"><span data-stu-id="9741f-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="9741f-299">Coloque uma compilação em fila para executar a compilação do pacote e publicar.</span><span class="sxs-lookup"><span data-stu-id="9741f-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="9741f-300">Se você tiver um gatilho definido para Integração Contínua, você vai executar esse comportamento em cada check-in.</span><span class="sxs-lookup"><span data-stu-id="9741f-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="9741f-301">Modelo de script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="9741f-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="9741f-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9741f-302">Next steps</span></span>
<span data-ttu-id="9741f-303">Para habilitar a depuração remota ao usar a entrega contínua, consulte [Habilitar a depuração remota ao usar a entrega contínua para publicar no Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="9741f-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
