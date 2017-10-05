---
title: "Notas de versão do SDK do Azure para .NET 2.9"
description: "Notas de versão do SDK do Azure para .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="05ce3-103">Notas de versão do SDK do Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="05ce3-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="05ce3-104">Este tópico inclui as notas de versão para as versões 2.9 e 2.9.6 do SDK do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="05ce3-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="05ce3-105">Resumo da versão do SDK do Azure para .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="05ce3-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="05ce3-106">Data do lançamento: 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="05ce3-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="05ce3-107">Nenhuma alteração significativa do Azure SDK 2.9 foi introduzida nesta versão.</span><span class="sxs-lookup"><span data-stu-id="05ce3-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="05ce3-108">Também não há nenhum processo de atualização necessário para aproveitar esse SDK com projetos de Serviço de Nuvem existentes.</span><span class="sxs-lookup"><span data-stu-id="05ce3-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="05ce3-109">Visual Studio 2017 versão Release Candidate</span><span class="sxs-lookup"><span data-stu-id="05ce3-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="05ce3-110">No Visual Studio 2017 RC, esta versão do SDK do Azure para .NET é integrada à Carga de Trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="05ce3-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="05ce3-111">Todas as ferramentas que você precisa para fazer o desenvolvimento do Azure farão parte do Visual Studio 2017 RC no futuro.</span><span class="sxs-lookup"><span data-stu-id="05ce3-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="05ce3-112">Para o Visual Studio 2015 e o Visual Studio 2013, o SDK ainda estará disponível por meio do WebPI.</span><span class="sxs-lookup"><span data-stu-id="05ce3-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="05ce3-113">Suspenderemos o SDK do Azure para versões .NET para o Visual Studio 2013, quando o Visual Studio 2017 for lançado como um produto final.</span><span class="sxs-lookup"><span data-stu-id="05ce3-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="05ce3-114">Siga este link para baixar o RC do Visual Studio 2017: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="05ce3-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="05ce3-115">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="05ce3-115">Azure Diagnostics</span></span>

- <span data-ttu-id="05ce3-116">Foi alterado o comportamento para armazenar somente uma cadeia de conexão parcial somente com a chave substituída por um token de cadeia de conexão do armazenamento de diagnóstico dos Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="05ce3-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="05ce3-117">A chave de armazenamento real agora é armazenada na pasta de perfil do usuário para que seu acesso possa ser controlado.</span><span class="sxs-lookup"><span data-stu-id="05ce3-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="05ce3-118">O Visual Studio lerá a chave de armazenamento da pasta de perfil de usuário para depuração local e processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="05ce3-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="05ce3-119">Em resposta à alteração descrita acima, a equipe do Visual Studio Online aprimorou o modelo de tarefa de implantação dos Serviços de Nuvem do Azure para que os usuários possam especificar a chave de armazenamento para configurar a extensão de diagnóstico ao publicar no Azure na Implantação e Integração Contínua.</span><span class="sxs-lookup"><span data-stu-id="05ce3-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="05ce3-120">Tornamos possível armazenar a cadeia de conexão segura e a geração de tokens para Diagnóstico do Azure (WAD) a fim de ajudá-lo a solucionar problemas de configuração em ambientes.</span><span class="sxs-lookup"><span data-stu-id="05ce3-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="05ce3-121">Máquinas virtuais do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="05ce3-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="05ce3-122">O Visual Studio agora oferece suporte à implantação de Serviços de Nuvem nas máquinas virtuais da Família do SO 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="05ce3-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="05ce3-123">Para serviços de nuvem existentes, é possível alterar suas configurações para direcionar a nova Família de SO.</span><span class="sxs-lookup"><span data-stu-id="05ce3-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="05ce3-124">Ao criar novos serviços de nuvem, se você optar por criar o serviço usando o .net 4.6 ou posterior, isso padronizará o serviço para usar a Família do SO 5.</span><span class="sxs-lookup"><span data-stu-id="05ce3-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="05ce3-125">Para obter mais informações, é possível examinar a [tabela de suporte da Família do SO Convidado](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="05ce3-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="05ce3-126">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="05ce3-126">Known issues</span></span>

- <span data-ttu-id="05ce3-127">O SDK 2.9.6 para .NET do Azure introduziu uma restrição que bloqueia a implantação de projetos usando estruturas .NET sem suporte (como .NET 4.6) para qualquer Família de SO anterior a 5.</span><span class="sxs-lookup"><span data-stu-id="05ce3-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="05ce3-128">Uma solução alternativa é fornecida [aqui](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="05ce3-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="05ce3-129">Cache na função do Azure</span><span class="sxs-lookup"><span data-stu-id="05ce3-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="05ce3-130">O suporte para o Cache na Função do Azure termina em 30 de novembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="05ce3-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="05ce3-131">Para obter mais detalhes, clique [aqui](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="05ce3-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="05ce3-132">Modelos do Azure Resource Manager para o Azure Stack</span><span class="sxs-lookup"><span data-stu-id="05ce3-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="05ce3-133">Apresentamos o Azure Stack como um destino de implantação para seus Modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05ce3-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="05ce3-134">Resumo do SDK para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="05ce3-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="05ce3-135">Visão geral</span><span class="sxs-lookup"><span data-stu-id="05ce3-135">Overview</span></span>
<span data-ttu-id="05ce3-136">Este documento contém as notas de versão do SDK do Azure para a versão do .NET 2.9.</span><span class="sxs-lookup"><span data-stu-id="05ce3-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="05ce3-137">Para obter informações detalhadas sobre atualizações nesta versão, consulte a [Postagem de anúncio do SDK do Azure 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="05ce3-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="05ce3-138">Atualização 2 do SDK do Azure 2.9 para Visual Studio 2015 e Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="05ce3-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="05ce3-139">Esta atualização inclui as seguintes correções de bug:</span><span class="sxs-lookup"><span data-stu-id="05ce3-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="05ce3-140">Problema relacionado à API REST de Geração de Cliente no qual a cadeia de caracteres "Tipo Desconhecido" seria exibida como o nome da pasta de geração de código e/ou o nome do namespace descartado no código gerado.</span><span class="sxs-lookup"><span data-stu-id="05ce3-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="05ce3-141">Problema relacionado a WebJobs Agendados no qual as informações de autenticação estavam falhando em serem passadas para o processo de provisionamento do Agendador.</span><span class="sxs-lookup"><span data-stu-id="05ce3-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="05ce3-142">Esta atualização inclui o novo recurso a seguir:</span><span class="sxs-lookup"><span data-stu-id="05ce3-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="05ce3-143">Suporte para Serviços de Aplicativos secundários na guia "Serviços" da caixa de diálogo de provisionamento do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="05ce3-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="05ce3-144">Atualização 2 das Ferramentas do Azure Data Lake para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="05ce3-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="05ce3-145">Essa atualização inclui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="05ce3-145">This updates includes the following:</span></span>

* <span data-ttu-id="05ce3-146">**Ferramentas do Azure Data Lake** para Visual Studio agora estão mescladas ao SDK do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="05ce3-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="05ce3-147">A ferramenta é instalada automaticamente ao instalar o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="05ce3-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="05ce3-148">A ferramenta é atualizada com frequência, acesse [aqui](http://aka.ms/datalaketool) para obter as atualizações.</span><span class="sxs-lookup"><span data-stu-id="05ce3-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="05ce3-149">**Gerenciador de Servidores** agora permite exibir tudo e criar algumas entidades de metadados U-SQL.</span><span class="sxs-lookup"><span data-stu-id="05ce3-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="05ce3-150">Para saber mais, confira [este](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="05ce3-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="05ce3-151">Ferramentas do HDInsight</span><span class="sxs-lookup"><span data-stu-id="05ce3-151">HDInsight Tools</span></span>
<span data-ttu-id="05ce3-152">**Ferramentas do HDInsight** para Visual Studio agora dão suporte ao HDInsight versão 3.3, incluindo a exibição de gráficos Tez e outras correções de linguagem.</span><span class="sxs-lookup"><span data-stu-id="05ce3-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="05ce3-153">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="05ce3-153">Azure Resource Manager</span></span>
<span data-ttu-id="05ce3-154">Essa versão adiciona o suporte para [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) para modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05ce3-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="05ce3-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="05ce3-155">See also</span></span>
[<span data-ttu-id="05ce3-156">Postagem de anúncio do SDK 2.9 do Azure</span><span class="sxs-lookup"><span data-stu-id="05ce3-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

