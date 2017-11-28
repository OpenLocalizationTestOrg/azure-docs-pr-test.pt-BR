---
title: "Serviços de aaaContinuous de entrega para a nuvem com o Visual Studio Online | Microsoft Docs"
description: "Saiba como tooset a entrega contínua para o Azure aplicativos de nuvem sem salvar arquivos de configuração do serviço de toohello chave de armazenamento de diagnóstico"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="528bf-103">Securely salvar serviços diagnóstico chave armazenamento em nuvem e tooAzure integração contínua de instalação e implantação usando o Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="528bf-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="528bf-104">É um projeto de origem de tooopen prática comum hoje em dia.</span><span class="sxs-lookup"><span data-stu-id="528bf-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="528bf-105">Salvar segredos do aplicativo nos arquivos de configuração não é mais uma prática segura, já que vulnerabilidades de segurança são expostas a partir de segredos vazados de controles de origem pública.</span><span class="sxs-lookup"><span data-stu-id="528bf-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="528bf-106">Armazenar segredo como texto sem formatação em um arquivo em um pipeline de integração contínua não é seguro em como servidores de compilação podem ser compartilhada recursos no ambiente de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="528bf-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="528bf-107">Este artigo explica como o Visual Studio e o Visual Studio Online reduz as preocupações de segurança Olá durante o desenvolvimento e o processo de integração contínua.</span><span class="sxs-lookup"><span data-stu-id="528bf-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="528bf-108">Remover o segredo de chave de armazenamento de diagnóstico em arquivo de configuração de projeto</span><span class="sxs-lookup"><span data-stu-id="528bf-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="528bf-109">A extensão de diagnóstico dos Serviços de Nuvem requer o armazenamento do Azure para salvar os resultados do diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="528bf-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="528bf-110">Anteriormente a cadeia de conexão de armazenamento Olá é especificada nos arquivos de configuração (. cscfg) de serviços de nuvem hello e pode fazer check-in controle toosource.</span><span class="sxs-lookup"><span data-stu-id="528bf-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="528bf-111">Na versão mais recente do SDK do Azure de saudação alteramos o repositório de tooonly comportamento Olá uma conexão parcial de cadeia de caracteres com chave Olá substituído por um token.</span><span class="sxs-lookup"><span data-stu-id="528bf-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="528bf-112">Olá etapas a seguir descreve como novas ferramentas de serviços de nuvem Olá funciona:</span><span class="sxs-lookup"><span data-stu-id="528bf-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="528bf-113">1. Abra o designer de função hello</span><span class="sxs-lookup"><span data-stu-id="528bf-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="528bf-114">Clique duas vezes ou clique com o botão direito em um designer de função de tooopen de função de serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="528bf-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Abrir o designer de função][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="528bf-116">2. Na seção de diagnóstico, uma nova caixa de seleção "Não remover o segredo da chave de armazenamento projeto" é adicionada</span><span class="sxs-lookup"><span data-stu-id="528bf-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="528bf-117">Se você estiver usando o emulador de armazenamento local hello, essa caixa de seleção está desabilitada porque não há nenhum segredo toomanage para cadeia de conexão local hello, que é UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="528bf-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![A cadeia de conexão do emulador de armazenamento local não é um segredo][1]

* <span data-ttu-id="528bf-119">Se você estiver criando um novo projeto, por padrão, essa caixa de seleção estará desmarcada.</span><span class="sxs-lookup"><span data-stu-id="528bf-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="528bf-120">Isso resulta na seção chave de armazenamento de saudação do Olá selecionado que está sendo substituída por um token de cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="528bf-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="528bf-121">Olá valor do token Olá será localizada na pasta AppData Roaming do usuário atual hello, por exemplo: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="528bf-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="528bf-122">Observe a pasta user\AppData Olá é acesso controlado pela entrada do usuário e é considerada segredos de desenvolvimento de toostore um local seguro.</span><span class="sxs-lookup"><span data-stu-id="528bf-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![A chave de armazenamento é salva na pasta de perfil de usuário][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="528bf-124">3. Selecionar uma conta de armazenamento de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="528bf-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="528bf-125">Selecione uma conta de armazenamento da caixa de diálogo Olá iniciada clicando Olá "..."</span><span class="sxs-lookup"><span data-stu-id="528bf-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="528bf-126">.</span><span class="sxs-lookup"><span data-stu-id="528bf-126">button.</span></span> <span data-ttu-id="528bf-127">Observe como cadeia de conexão de armazenamento Olá gerado não terá chave de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="528bf-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="528bf-128">Por exemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="528bf-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="528bf-129">4.    Depuração de projeto Olá</span><span class="sxs-lookup"><span data-stu-id="528bf-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="528bf-130">F5 toostart de depuração no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="528bf-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="528bf-131">Tudo deve funcionar na saudação que mesma maneira como antes.</span><span class="sxs-lookup"><span data-stu-id="528bf-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="528bf-132">![Iniciar a depuração no local][3]</span><span class="sxs-lookup"><span data-stu-id="528bf-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="528bf-133">5. Publicar o projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="528bf-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="528bf-134">Olá iniciar caixa de diálogo Publicar e prossiga com instruções entrar toopublish Olá aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="528bf-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="528bf-135">6. Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="528bf-135">6. Additional information</span></span>
> <span data-ttu-id="528bf-136">Observação: painel de configurações de saudação no designer de função hello permanecerá como é agora.</span><span class="sxs-lookup"><span data-stu-id="528bf-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="528bf-137">Se você quiser recursos de gerenciamento de informações secretas Olá toouse para diagnóstico, vá toohello guia de configurações.</span><span class="sxs-lookup"><span data-stu-id="528bf-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Adicionar configurações][4]

> <span data-ttu-id="528bf-139">Observação: Se habilitada, Olá Application Insights chave será armazenada como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="528bf-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="528bf-140">chave de saudação só é usada para carregar conteúdo para que não há dados confidenciais em risco de comprometimento.</span><span class="sxs-lookup"><span data-stu-id="528bf-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="528bf-141">Criar e publicar um projeto dos Serviços de Nuvem usando modelos de tarefa do Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="528bf-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="528bf-142">Olá, as etapas a seguir ilustra como toosetup integração contínua para serviços de nuvem projeto usar tarefas do Visual Studio online:</span><span class="sxs-lookup"><span data-stu-id="528bf-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="528bf-143">1.    Obter uma conta do VSO</span><span class="sxs-lookup"><span data-stu-id="528bf-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="528bf-144">[Criar a conta do Visual Studio Online] [ Create Visual Studio Online account] se você não tiver um</span><span class="sxs-lookup"><span data-stu-id="528bf-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="528bf-145">[Criar projeto de equipe] [ Create team project] na conta do Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="528bf-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="528bf-146">2.    Configurar o controle de origem no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="528bf-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="528bf-147">Conecte-se o projeto de equipe tooa</span><span class="sxs-lookup"><span data-stu-id="528bf-147">Connect tooa team project</span></span>

![Conectar projeto tooteam][5]

![Selecione tooconnect de projeto de equipe para][6]

* <span data-ttu-id="528bf-150">Adicionar o controle de toosource de projeto</span><span class="sxs-lookup"><span data-stu-id="528bf-150">Add your project toosource control</span></span>

![Adicionar projeto toosource controle][7]

![Pasta de controle de origem do mapa projeto tooa][8]

* <span data-ttu-id="528bf-153">Fazer check-in do seu projeto no Team Explorer</span><span class="sxs-lookup"><span data-stu-id="528bf-153">Check in your project from Team Explorer</span></span>

![Check-in de controle de toosource de projeto][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="528bf-155">3.    Configurar o processo de compilação</span><span class="sxs-lookup"><span data-stu-id="528bf-155">3.    Configure Build process</span></span>
* <span data-ttu-id="528bf-156">Procurar um projeto de equipe tooyour e adicione um novo processo de compilação modelos</span><span class="sxs-lookup"><span data-stu-id="528bf-156">Browse tooyour team project and add a new build process Templates</span></span>

![Adicionar uma nova compilação][10]

* <span data-ttu-id="528bf-158">Selecionar tarefa de compilação</span><span class="sxs-lookup"><span data-stu-id="528bf-158">Select build task</span></span>

![Adicionar uma tarefa de compilação][11]

![Selecionar o modelo de tarefa Compilação do Visual Studio][12]

* <span data-ttu-id="528bf-161">Edite a entrada da tarefa de compilação.</span><span class="sxs-lookup"><span data-stu-id="528bf-161">Edit build task input.</span></span> <span data-ttu-id="528bf-162">Personalize compilação Olá parâmetros de acordo com tooyour necessário</span><span class="sxs-lookup"><span data-stu-id="528bf-162">Please customize hello build parameters according tooyour need</span></span>

![Configurar a tarefa de compilação][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="528bf-164">Configurar variáveis de compilação</span><span class="sxs-lookup"><span data-stu-id="528bf-164">Configure build variables</span></span>

![Configurar variáveis de compilação][14]

* <span data-ttu-id="528bf-166">Adicionar um destino de compilação tooupload tarefa</span><span class="sxs-lookup"><span data-stu-id="528bf-166">Add a task tooupload build drop</span></span>

![Escolher publicar tarefa de local de compilação][15]

![Configurar publicar tarefa de compilação de local de publicação][16]

* <span data-ttu-id="528bf-169">Executar compilação Olá</span><span class="sxs-lookup"><span data-stu-id="528bf-169">Run hello build</span></span>

![Enfileirar Nova Compilação][17]

![Exibir o resumo da compilação][18]

* <span data-ttu-id="528bf-172">Se a compilação de saudação for bem-sucedida, você verá um toobelow semelhante de resultado</span><span class="sxs-lookup"><span data-stu-id="528bf-172">if hello build is successful you will see a result similar toobelow</span></span>

![Resultado da compilação][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="528bf-174">4.    Configurar o processo de lançamento</span><span class="sxs-lookup"><span data-stu-id="528bf-174">4.    Configure Release process</span></span>
* <span data-ttu-id="528bf-175">Criar uma nova versão</span><span class="sxs-lookup"><span data-stu-id="528bf-175">Create a new release</span></span>

![Criar nova versão][20]

* <span data-ttu-id="528bf-177">Selecione a tarefa de implantação de serviços de nuvem do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="528bf-177">Select hello Azure Cloud Services Deployment task</span></span>

![Selecionar a tarefa de implantação dos Serviços de Nuvem do Azure][21]

* <span data-ttu-id="528bf-179">Como a chave de conta de armazenamento Olá não está marcada no controle toosource, precisamos chave secreta do toospecify Olá para configurar extensões de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="528bf-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="528bf-180">Expanda Olá **opções avançadas para criar novo serviço** seção e editar Olá **chaves de conta de armazenamento de diagnóstico** entrada de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="528bf-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="528bf-181">Essa entrada leva em várias linhas do par chave-valor no formato de saudação do **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="528bf-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="528bf-182">Observação: se sua conta de armazenamento está sob de diagnóstico hello mesma assinatura em que você publicará o aplicativo de serviços de nuvem hello, você não tiver tooenter Olá chave na entrada de tarefa de implantação Olá; implantação Olá programaticamente Obtenha informações de armazenamento de saudação da sua assinatura</span><span class="sxs-lookup"><span data-stu-id="528bf-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Configurar a tarefa de implantação dos Serviços de Nuvem][22]

* <span data-ttu-id="528bf-184">Segredo do uso de compilação variáveis toosave chaves de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="528bf-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="528bf-185">toomask uma variável como um segredo clique no ícone de cadeado Olá Olá direita de saudação variáveis de entrada</span><span class="sxs-lookup"><span data-stu-id="528bf-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Salvar chaves de armazenamento em variáveis de compilação secretas][23]

* <span data-ttu-id="528bf-187">Criar uma versão e implantar seu projeto tooAzure</span><span class="sxs-lookup"><span data-stu-id="528bf-187">Create a release and deploy your project tooAzure</span></span>

![Criar nova versão][24]

## <a name="next-steps"></a><span data-ttu-id="528bf-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="528bf-189">Next steps</span></span>
<span data-ttu-id="528bf-190">toolearn mais sobre a configuração de extensões de diagnóstico para os serviços de nuvem do Azure, consulte [habilitar o diagnóstico nos serviços de nuvem do Azure usando o PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="528bf-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
