---
title: "Entrega contínua para serviços de nuvem com o Visual Studio Online | Microsoft Docs"
description: "Saiba como configurar a entrega contínua para aplicativos de nuvem do Azure sem salvar a chave de armazenamento de diagnóstico para os arquivos de configuração de serviço"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="adb36-103">Salvar com segurança a chave de armazenamento de diagnóstico dos Serviços de Nuvem e configure a integração contínua e a implantação no Azure usando o Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="adb36-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="adb36-104">Hoje, é uma prática comum para projetos de software livre.</span><span class="sxs-lookup"><span data-stu-id="adb36-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="adb36-105">Salvar segredos do aplicativo nos arquivos de configuração não é mais uma prática segura, já que vulnerabilidades de segurança são expostas a partir de segredos vazados de controles de origem pública.</span><span class="sxs-lookup"><span data-stu-id="adb36-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="adb36-106">O armazenamento do segredo como texto sem formatação em um pipeline de Integração Contínua não é seguro porque os servidores de compilação poderiam ser recursos compartilhados no ambiente de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="adb36-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="adb36-107">Este artigo explica como o Visual Studio e o Visual Studio Online minimizam as preocupações de segurança durante o desenvolvimento e o processo de Integração Contínua.</span><span class="sxs-lookup"><span data-stu-id="adb36-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="adb36-108">Remover o segredo de chave de armazenamento de diagnóstico em arquivo de configuração de projeto</span><span class="sxs-lookup"><span data-stu-id="adb36-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="adb36-109">A extensão de diagnóstico dos Serviços de Nuvem requer o armazenamento do Azure para salvar os resultados do diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="adb36-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="adb36-110">Anteriormente, a cadeia de conexão de armazenamento era especificada nos arquivos de configuração (.cscfg) dos Serviços de Nuvem e você podia fazer check-in deles para o controle de origem.</span><span class="sxs-lookup"><span data-stu-id="adb36-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="adb36-111">Na última versão do SDK do Azure, alteramos o comportamento para armazenar somente uma cadeia de conexão parcial somente com a chave substituída por um token.</span><span class="sxs-lookup"><span data-stu-id="adb36-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="adb36-112">As etapas a seguir descrevem o funcionamento das novas ferramentas dos Serviços de Nuvem:</span><span class="sxs-lookup"><span data-stu-id="adb36-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="adb36-113">1. Abra o Designer de função</span><span class="sxs-lookup"><span data-stu-id="adb36-113">1. Open the Role designer</span></span>
* <span data-ttu-id="adb36-114">Clique duas vezes ou clique com o botão direito do mouse em uma função dos Serviços de Nuvem para abrir o Designer de função</span><span class="sxs-lookup"><span data-stu-id="adb36-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Abrir o designer de função][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="adb36-116">2. Na seção de diagnóstico, uma nova caixa de seleção "Não remover o segredo da chave de armazenamento projeto" é adicionada</span><span class="sxs-lookup"><span data-stu-id="adb36-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="adb36-117">Se você estiver usando o emulador de armazenamento local, essa caixa de seleção estará desabilitada porque não há nenhum segredo a ser gerenciado para a cadeia de conexão local, que é UseDevelopmentStorage=true.</span><span class="sxs-lookup"><span data-stu-id="adb36-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![A cadeia de conexão do emulador de armazenamento local não é um segredo][1]

* <span data-ttu-id="adb36-119">Se você estiver criando um novo projeto, por padrão, essa caixa de seleção estará desmarcada.</span><span class="sxs-lookup"><span data-stu-id="adb36-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="adb36-120">Isso resulta na seção de armazenamento de chave de armazenamento da cadeia de conexão selecionada que está sendo substituída por um token.</span><span class="sxs-lookup"><span data-stu-id="adb36-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="adb36-121">O valor do token será encontrado na pasta AppData Roaming do usuário atual, por exemplo: C:\Usuários\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="adb36-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="adb36-122">Observe que a pasta user\AppData tem Acesso Controlado pela entrada do usuário e é considerada como um local seguro para armazenar os segredos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="adb36-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![A chave de armazenamento é salva na pasta de perfil de usuário][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="adb36-124">3. Selecionar uma conta de armazenamento de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="adb36-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="adb36-125">Selecione uma conta de armazenamento do diálogo iniciado quando você clica em “...”</span><span class="sxs-lookup"><span data-stu-id="adb36-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="adb36-126">.</span><span class="sxs-lookup"><span data-stu-id="adb36-126">button.</span></span> <span data-ttu-id="adb36-127">Observe como a cadeia de conexão de armazenamento gerada não terá a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="adb36-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="adb36-128">Por exemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="adb36-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="adb36-129">4.    Depuração do projeto</span><span class="sxs-lookup"><span data-stu-id="adb36-129">4.    Debugging the project</span></span>
* <span data-ttu-id="adb36-130">Pressione F5 para iniciar a depuração no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="adb36-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="adb36-131">Tudo deve funcionar da mesma maneira como antes.</span><span class="sxs-lookup"><span data-stu-id="adb36-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="adb36-132">![Iniciar a depuração no local][3]</span><span class="sxs-lookup"><span data-stu-id="adb36-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="adb36-133">5. Publicar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adb36-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="adb36-134">Inicie o diálogo de publicação e prossiga com as instruções de entrada para publicar o aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="adb36-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="adb36-135">6. Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="adb36-135">6. Additional information</span></span>
> <span data-ttu-id="adb36-136">Observação: o painel Configurações no designer de função permanecerá como está agora.</span><span class="sxs-lookup"><span data-stu-id="adb36-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="adb36-137">Se você quiser usar a funcionalidade de gerenciamento de informações de segredos para diagnóstico, vá para a guia Configurações.</span><span class="sxs-lookup"><span data-stu-id="adb36-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Adicionar configurações][4]

> <span data-ttu-id="adb36-139">Observação: se habilitada, a chave do Application Insights será armazenada como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="adb36-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="adb36-140">A chave só será usada para carregar conteúdo de forma que nenhum dado confidencial corra o risco de ser comprometido.</span><span class="sxs-lookup"><span data-stu-id="adb36-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="adb36-141">Criar e publicar um projeto dos Serviços de Nuvem usando modelos de tarefa do Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="adb36-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="adb36-142">As etapas a seguir ilustram como configurar a Integração Contínua para o projeto dos Serviços de Nuvem usando tarefas do Visual Studio Online:</span><span class="sxs-lookup"><span data-stu-id="adb36-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="adb36-143">1.    Obter uma conta do VSO</span><span class="sxs-lookup"><span data-stu-id="adb36-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="adb36-144">[Criar a conta do Visual Studio Online] [ Create Visual Studio Online account] se você não tiver um</span><span class="sxs-lookup"><span data-stu-id="adb36-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="adb36-145">[Criar projeto de equipe] [ Create team project] na conta do Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="adb36-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="adb36-146">2.    Configurar o controle de origem no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adb36-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="adb36-147">Conectar-se a um projeto de equipe</span><span class="sxs-lookup"><span data-stu-id="adb36-147">Connect to a team project</span></span>

![Conectar-se ao projeto de equipe][5]

![Selecione o projeto de equipe ao qual você se conectará][6]

* <span data-ttu-id="adb36-150">Adicionar seu projeto ao controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="adb36-150">Add your project to source control</span></span>

![Adicionar projeto ao controle do código-fonte][7]

![Mapear projeto para uma pasta de controle de origem][8]

* <span data-ttu-id="adb36-153">Fazer check-in do seu projeto no Team Explorer</span><span class="sxs-lookup"><span data-stu-id="adb36-153">Check in your project from Team Explorer</span></span>

![Fazer check-in em um projeto para o controle do código-fonte][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="adb36-155">3.    Configurar o processo de compilação</span><span class="sxs-lookup"><span data-stu-id="adb36-155">3.    Configure Build process</span></span>
* <span data-ttu-id="adb36-156">Navegar até seu projeto de equipe e adicionar um novo processo de compilação Modelos</span><span class="sxs-lookup"><span data-stu-id="adb36-156">Browse to your team project and add a new build process Templates</span></span>

![Adicionar uma nova compilação][10]

* <span data-ttu-id="adb36-158">Selecionar tarefa de compilação</span><span class="sxs-lookup"><span data-stu-id="adb36-158">Select build task</span></span>

![Adicionar uma tarefa de compilação][11]

![Selecionar o modelo de tarefa Compilação do Visual Studio][12]

* <span data-ttu-id="adb36-161">Edite a entrada da tarefa de compilação.</span><span class="sxs-lookup"><span data-stu-id="adb36-161">Edit build task input.</span></span> <span data-ttu-id="adb36-162">Personalizar os parâmetros de compilação de acordo com a sua necessidade</span><span class="sxs-lookup"><span data-stu-id="adb36-162">Please customize the build parameters according to your need</span></span>

![Configurar a tarefa de compilação][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="adb36-164">Configurar variáveis de compilação</span><span class="sxs-lookup"><span data-stu-id="adb36-164">Configure build variables</span></span>

![Configurar variáveis de compilação][14]

* <span data-ttu-id="adb36-166">Adicionar uma tarefa para carregar o local de compilação</span><span class="sxs-lookup"><span data-stu-id="adb36-166">Add a task to upload build drop</span></span>

![Escolher publicar tarefa de local de compilação][15]

![Configurar publicar tarefa de compilação de local de publicação][16]

* <span data-ttu-id="adb36-169">Executar a compilação</span><span class="sxs-lookup"><span data-stu-id="adb36-169">Run the build</span></span>

![Enfileirar Nova Compilação][17]

![Exibir o resumo da compilação][18]

* <span data-ttu-id="adb36-172">Se a compilação for bem-sucedida, você verá um resultado semelhante a este</span><span class="sxs-lookup"><span data-stu-id="adb36-172">if the build is successful you will see a result similar to below</span></span>

![Resultado da compilação][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="adb36-174">4.    Configurar o processo de lançamento</span><span class="sxs-lookup"><span data-stu-id="adb36-174">4.    Configure Release process</span></span>
* <span data-ttu-id="adb36-175">Criar uma nova versão</span><span class="sxs-lookup"><span data-stu-id="adb36-175">Create a new release</span></span>

![Criar nova versão][20]

* <span data-ttu-id="adb36-177">Selecionar a tarefa Implantação dos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="adb36-177">Select the Azure Cloud Services Deployment task</span></span>

![Selecionar a tarefa de implantação dos Serviços de Nuvem do Azure][21]

* <span data-ttu-id="adb36-179">Se você não fizer o check-in da chave da conta de armazenamento no controle de origem, precisaremos especificar a chave secreta para a configuração de extensões de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="adb36-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="adb36-180">Expanda a seção **Opções Avançadas para a Criação de Novo Serviço** e edite a entrada do parâmetro **Chaves de Conta de Armazenamento de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="adb36-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="adb36-181">Essa entrada obtém várias linhas do par de valor de chave no formato **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="adb36-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="adb36-182">Observação: se a sua conta de armazenamento de diagnóstico estiver sob a mesma assinatura em que você publicará o aplicativo dos Serviços de Nuvem, não será necessário inserir a chave na entrada da tarefa de implantação; a implantação obterá programaticamente as informações de armazenamento de sua assinatura</span><span class="sxs-lookup"><span data-stu-id="adb36-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Configurar a tarefa de implantação dos Serviços de Nuvem][22]

* <span data-ttu-id="adb36-184">Use as variáveis de compilação secretas para salvar as Chaves de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="adb36-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="adb36-185">Para mascarar uma variável como segredo, clique no ícone de bloqueio no lado direito da entrada Variáveis</span><span class="sxs-lookup"><span data-stu-id="adb36-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Salvar chaves de armazenamento em variáveis de compilação secretas][23]

* <span data-ttu-id="adb36-187">Criar uma versão e implantar seu projeto no Azure</span><span class="sxs-lookup"><span data-stu-id="adb36-187">Create a release and deploy your project to Azure</span></span>

![Criar nova versão][24]

## <a name="next-steps"></a><span data-ttu-id="adb36-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adb36-189">Next steps</span></span>
<span data-ttu-id="adb36-190">Para saber mais sobre como configurar as extensões de diagnóstico para os serviços de nuvem do Azure, consulte [habilitar o diagnóstico nos serviços de nuvem do Azure usando o PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="adb36-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
