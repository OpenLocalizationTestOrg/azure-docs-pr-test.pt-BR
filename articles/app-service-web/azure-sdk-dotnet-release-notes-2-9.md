---
title: "aaaAzure SDK para notas de versão do .NET 2.9"
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
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="ccf21-103">Notas de versão do SDK do Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="ccf21-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="ccf21-104">Este tópico inclui as notas de versão para as versões 2.9 e 2.9.6 do SDK do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="ccf21-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="ccf21-105">Resumo da versão do SDK do Azure para .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="ccf21-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="ccf21-106">Data do lançamento: 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="ccf21-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="ccf21-107">Sem alterações de quebra toohello Azure SDK 2.9 foram introduzidos nesta versão.</span><span class="sxs-lookup"><span data-stu-id="ccf21-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="ccf21-108">Há também não tooleverage do processo de atualização necessário este SDK com projetos de serviço de nuvem existentes.</span><span class="sxs-lookup"><span data-stu-id="ccf21-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="ccf21-109">Visual Studio 2017 versão Release Candidate</span><span class="sxs-lookup"><span data-stu-id="ccf21-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="ccf21-110">No Visual Studio RC de 2017, esta versão do hello Azure SDK para .NET é criado de Olá carga de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf21-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="ccf21-111">Todas as ferramentas de saudação necessário toodo desenvolvimento do Azure farão parte do Visual Studio 2017 RC no futuro.</span><span class="sxs-lookup"><span data-stu-id="ccf21-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="ccf21-112">Para o Visual Studio 2015 e Visual Studio 2013, Olá SDK ainda estarão disponível por meio do WebPI.</span><span class="sxs-lookup"><span data-stu-id="ccf21-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="ccf21-113">Suspenderemos o SDK do Azure para versões .NET para o Visual Studio 2013, quando o Visual Studio 2017 for lançado como um produto final.</span><span class="sxs-lookup"><span data-stu-id="ccf21-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="ccf21-114">Siga este toodownload link Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="ccf21-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="ccf21-115">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf21-115">Azure Diagnostics</span></span>

- <span data-ttu-id="ccf21-116">Olá alterados comportamento tooonly armazenar uma cadeia de caracteres de conexão parcial com chave Olá substituído por um token de cadeia de conexão de armazenamento de diagnóstico de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ccf21-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="ccf21-117">chave de armazenamento real do Hello agora é armazenada na pasta de perfil de usuário Olá assim seu acesso pode ser controlado.</span><span class="sxs-lookup"><span data-stu-id="ccf21-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="ccf21-118">O Visual Studio lerá a chave de armazenamento de saudação da pasta de perfil de usuário para depuração local e o processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="ccf21-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="ccf21-119">Na resposta, altere toohello descrito acima, Visual Studio Online team Olá avançado modelo de tarefa de implantação de serviços de nuvem do Azure para que usuários podem especificar a chave de armazenamento de saudação para definir a extensão de diagnóstico ao publicar tooAzure na integração contínua e a implantação.</span><span class="sxs-lookup"><span data-stu-id="ccf21-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="ccf21-120">Fizemos-a cadeia de caracteres de conexão segura toostore possíveis e geração de tokens para diagnóstico WAD (Azure), toohelp você solucionar problemas de configuração em environements.</span><span class="sxs-lookup"><span data-stu-id="ccf21-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="ccf21-121">Máquinas virtuais do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ccf21-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="ccf21-122">O Visual Studio agora oferece suporte a implantação dos serviços de nuvem tooOS máquinas virtuais de família 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="ccf21-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="ccf21-123">Para serviços de nuvem existente, você pode alterar sua configurações tootarget Olá nova família de sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="ccf21-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="ccf21-124">Ao criar novos serviços em nuvem, se você escolher toocreate Olá serviço usando o .net 4.6 ou posterior, o padrão será Olá serviço toouse 5 de família do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ccf21-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="ccf21-125">Para obter mais informações, você pode examinar Olá [família do sistema operacional convidado suporte tabela](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="ccf21-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ccf21-126">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="ccf21-126">Known issues</span></span>

- <span data-ttu-id="ccf21-127">SDK do .NET do Azure 2.9.6 introduziu uma restrição que bloqueia a implantação de projetos usando tooany de estruturas (como o .NET 4.6) sem suporte .NET família do sistema operacional < 5.</span><span class="sxs-lookup"><span data-stu-id="ccf21-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="ccf21-128">Uma solução alternativa é fornecida [aqui](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="ccf21-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="ccf21-129">Cache na função do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf21-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="ccf21-130">O suporte para o Cache na Função do Azure termina em 30 de novembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="ccf21-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="ccf21-131">Para obter mais detalhes, clique [aqui](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="ccf21-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="ccf21-132">Modelos do Azure Resource Manager para o Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ccf21-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="ccf21-133">Apresentamos o Azure Stack como um destino de implantação para seus Modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ccf21-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="ccf21-134">Resumo do SDK para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="ccf21-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="ccf21-135">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ccf21-135">Overview</span></span>
<span data-ttu-id="ccf21-136">Este documento contém notas de versão de saudação do hello Azure SDK versão 2.9 .NET.</span><span class="sxs-lookup"><span data-stu-id="ccf21-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="ccf21-137">Para obter informações detalhadas sobre atualizações nesta versão, consulte Olá [post de lançamento do Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="ccf21-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="ccf21-138">Atualização 2 do SDK do Azure 2.9 para Visual Studio 2015 e Visual Studio "15" Preview</span><span class="sxs-lookup"><span data-stu-id="ccf21-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="ccf21-139">Esta atualização inclui Olá correções de bug a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccf21-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="ccf21-140">Emitir tooREST relacionado geração de API de cliente na cadeia de caracteres que hello "Tipo desconhecido" deverá aparecer como Olá nome da pasta de geração de código hello e/ou Olá Olá namespace soltas no código Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="ccf21-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="ccf21-141">Emita WebJobs tooScheduled relacionados nos quais Olá informações de autenticação foi com falha toobe passado toohello o processo de provisionamento de Agendador.</span><span class="sxs-lookup"><span data-stu-id="ccf21-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="ccf21-142">Esta atualização inclui Olá novo recurso a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccf21-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="ccf21-143">Suporte para serviços de aplicativo secundários na guia "Serviços" Olá Olá caixa de diálogo de provisionamento do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccf21-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="ccf21-144">Atualização 2 das Ferramentas do Azure Data Lake para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ccf21-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="ccf21-145">Esta atualização inclui os seguintes de saudação:</span><span class="sxs-lookup"><span data-stu-id="ccf21-145">This updates includes hello following:</span></span>

* <span data-ttu-id="ccf21-146">**Azure Data Lake Tools** para Visual Studio agora é mesclado hello Azure SDK para a versão do .NET.</span><span class="sxs-lookup"><span data-stu-id="ccf21-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="ccf21-147">ferramenta de saudação é instalada automaticamente quando você instala o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf21-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="ccf21-148">ferramenta de saudação é atualizada com frequência, vá [aqui](http://aka.ms/datalaketool) tooget Olá atualizações.</span><span class="sxs-lookup"><span data-stu-id="ccf21-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="ccf21-149">**Gerenciador de servidores** agora permite que você tooview todos e criar algumas entidades de metadados U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ccf21-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="ccf21-150">Para saber mais, confira [este](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="ccf21-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="ccf21-151">Ferramentas do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ccf21-151">HDInsight Tools</span></span>
<span data-ttu-id="ccf21-152">**Ferramentas do HDInsight** para Visual Studio agora dão suporte ao HDInsight versão 3.3, incluindo a exibição de gráficos Tez e outras correções de linguagem.</span><span class="sxs-lookup"><span data-stu-id="ccf21-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="ccf21-153">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf21-153">Azure Resource Manager</span></span>
<span data-ttu-id="ccf21-154">Essa versão adiciona o suporte para [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) para modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ccf21-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="ccf21-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ccf21-155">See also</span></span>
[<span data-ttu-id="ccf21-156">Postagem de anúncio do SDK 2.9 do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf21-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

