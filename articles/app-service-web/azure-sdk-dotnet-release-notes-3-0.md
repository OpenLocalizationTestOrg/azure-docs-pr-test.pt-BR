---
title: "Notas de versão do SDK do Azure para .NET 3.0 | Microsoft Docs"
description: "Notas de Versão do SDK do Azure para .NET 3.0"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: eea4e569ac2d0192ed7872d2fcb9bed03614832b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="8c834-103">Notas de versão do SDK do Azure para .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="8c834-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="8c834-104">Este tópico inclui as notas de versão para a versão 3.0 do SDK do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="8c834-104">This topic includes release notes for version 3.0 of the Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="8c834-105">Resumo da versão do SDK do Azure para .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="8c834-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="8c834-106">Data do lançamento: 03/07/2017</span><span class="sxs-lookup"><span data-stu-id="8c834-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="8c834-107">Nenhuma alteração significativa do Azure SDK 3.0 foi introduzida nesta versão.</span><span class="sxs-lookup"><span data-stu-id="8c834-107">No breaking changes to the Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="8c834-108">Também não há nenhum processo de atualização necessário para aproveitar esse SDK com projetos de Serviço de Nuvem existentes.</span><span class="sxs-lookup"><span data-stu-id="8c834-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="8c834-109">Para permitir o uso do SDK do Azure 3.0 sem a necessidade de um processo de atualização, o SDK do Azure 3.0 instala os mesmos diretórios do SDK do Azure 2.9.</span><span class="sxs-lookup"><span data-stu-id="8c834-109">To allow use of the Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs to the same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="8c834-110">A maioria dos componentes não alterou a versão principal 2.9, apenas atualizou o número de build.</span><span class="sxs-lookup"><span data-stu-id="8c834-110">Most the components did not change the major version from 2.9 but instead just updated the build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="8c834-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="8c834-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="8c834-112">No Visual Studio 2017, esta versão do SDK do Azure para .NET é integrada à Carga de Trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c834-112">In Visual Studio 2017, this release of the Azure SDK for .NET is built in to the Azure Workload.</span></span> <span data-ttu-id="8c834-113">Todas as ferramentas que você precisa para fazer o desenvolvimento do Azure farão parte do Visual Studio 2017 no futuro.</span><span class="sxs-lookup"><span data-stu-id="8c834-113">All the tools you need to do Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="8c834-114">Para o Visual Studio 2015, o SDK ainda estará disponível por meio do WebPI.</span><span class="sxs-lookup"><span data-stu-id="8c834-114">For Visual Studio 2015 the SDK will still be available through WebPI.</span></span> <span data-ttu-id="8c834-115">Agora que o Visual Studio 2017 foi lançado, descontinuamos as versões do SDK do Azure para .NET para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8c834-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="8c834-116">Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="8c834-116">Azure Diagnostics</span></span>

- <span data-ttu-id="8c834-117">Foi alterado o comportamento para armazenar somente uma cadeia de conexão parcial somente com a chave substituída por um token de cadeia de conexão do armazenamento de diagnóstico dos Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="8c834-117">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="8c834-118">A chave de armazenamento real agora é armazenada na pasta de perfil do usuário para que seu acesso possa ser controlado.</span><span class="sxs-lookup"><span data-stu-id="8c834-118">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="8c834-119">O Visual Studio lerá a chave de armazenamento da pasta de perfil de usuário para depuração local e processo de publicação.</span><span class="sxs-lookup"><span data-stu-id="8c834-119">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="8c834-120">Em resposta à alteração descrita acima, a equipe do Visual Studio Online aprimorou o modelo de tarefa de implantação dos Serviços de Nuvem do Azure para que os usuários possam especificar a chave de armazenamento para configurar a extensão de diagnóstico ao publicar no Azure na Implantação e Integração Contínua.</span><span class="sxs-lookup"><span data-stu-id="8c834-120">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="8c834-121">Tornamos possível armazenar a cadeia de conexão segura e a geração de tokens para Diagnóstico do Azure (WAD) a fim de ajudá-lo a solucionar problemas de configuração em ambientes.</span><span class="sxs-lookup"><span data-stu-id="8c834-121">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="8c834-122">Máquinas virtuais do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8c834-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="8c834-123">O Visual Studio agora oferece suporte à implantação de Serviços de Nuvem nas máquinas virtuais da Família do SO 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="8c834-123">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="8c834-124">Para serviços de nuvem existentes, é possível alterar suas configurações para direcionar a nova Família de SO.</span><span class="sxs-lookup"><span data-stu-id="8c834-124">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="8c834-125">Ao criar novos serviços de nuvem, se você optar por criar o serviço usando o .net 4.6 ou posterior, isso padronizará o serviço para usar a Família do SO 5.</span><span class="sxs-lookup"><span data-stu-id="8c834-125">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="8c834-126">Para obter mais informações, é possível examinar a [tabela de suporte da Família do SO Convidado](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8c834-126">For more information, you can review the [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="8c834-127">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="8c834-127">Known issues</span></span>

- <span data-ttu-id="8c834-128">O SDK do Azure para .NET 3.0 apresentou um problema ao remover o Visual Studio 2017 em uma configuração lado a lado com o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8c834-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="8c834-129">Se você tiver o SDK do Azure instalado para Visual Studio 2015, o Emulador de Armazenamento do Microsoft Azure e o emulador de computação do Microsoft Azure serão removidos se você desinstalar o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8c834-129">If you have the Azure SDK installed for Visual Studio 2015, the Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="8c834-130">Isso produzirá um erro durante a criação e depuração de novos projetos de serviços de nuvem no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8c834-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="8c834-131">Para corrigir esse problema, reinstale o SDK do Azure do Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="8c834-131">In order to fix this issue,  reinstall the Azure SDK from the Web Platform Installer.</span></span>  <span data-ttu-id="8c834-132">O problema será resolvido em uma atualização futura do Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8c834-132">The issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="8c834-133">.</span><span class="sxs-lookup"><span data-stu-id="8c834-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="8c834-134">Cache na função do Azure</span><span class="sxs-lookup"><span data-stu-id="8c834-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="8c834-135">O suporte para Cache na Função do Azure terminou em 30 de novembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="8c834-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="8c834-136">Para obter mais detalhes, clique [aqui](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="8c834-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




