---
title: "aaaManage contas de serviços de mídia do Azure com o PowerShell"
description: Saiba como toomanage Azure Media Services contas com cmdlets do PowerShell.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="24569-103">Gerenciar contas dos Serviços de Mídia do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="24569-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24569-104">Portal</span><span class="sxs-lookup"><span data-stu-id="24569-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="24569-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24569-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="24569-106">REST</span><span class="sxs-lookup"><span data-stu-id="24569-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="24569-107">toobe toocreate capaz de uma conta de serviços de mídia do Azure, você deve ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="24569-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="24569-108">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="24569-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="24569-109">Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Avaliação Gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="24569-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="24569-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="24569-110">Overview</span></span>
<span data-ttu-id="24569-111">Este artigo lista Olá cmdlets do PowerShell do Azure para serviços de mídia do Azure (AMS) na estrutura do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="24569-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="24569-112">Olá cmdlets existe no hello **Microsoft.Azure.Commands.Media** namespace.</span><span class="sxs-lookup"><span data-stu-id="24569-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="24569-113">Versões</span><span class="sxs-lookup"><span data-stu-id="24569-113">Versions</span></span>
<span data-ttu-id="24569-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="24569-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="24569-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="24569-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="24569-116">Cria um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-117">Syntax</span></span>
<span data-ttu-id="24569-118">Conjunto de Parâmetros: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="24569-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="24569-119">Conjunto de Parâmetros: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="24569-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-120">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-120">Parameters</span></span>
<span data-ttu-id="24569-121">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-122">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-123">Aliases</span></span> | <span data-ttu-id="24569-124">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-125">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-125">Required?</span></span> |<span data-ttu-id="24569-126">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-126">true</span></span> |
| <span data-ttu-id="24569-127">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-127">Position?</span></span> |<span data-ttu-id="24569-128">0</span><span class="sxs-lookup"><span data-stu-id="24569-128">0</span></span> |
| <span data-ttu-id="24569-129">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-129">Default value</span></span> |<span data-ttu-id="24569-130">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-130">none</span></span> |
| <span data-ttu-id="24569-131">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-131">Accept pipeline input?</span></span> |<span data-ttu-id="24569-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-133">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-133">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-134">false</span><span class="sxs-lookup"><span data-stu-id="24569-134">false</span></span> |

<span data-ttu-id="24569-135">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-136">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-137">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-137">Aliases</span></span> | <span data-ttu-id="24569-138">Name</span><span class="sxs-lookup"><span data-stu-id="24569-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="24569-139">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-139">Required?</span></span> |<span data-ttu-id="24569-140">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-140">true</span></span> |
| <span data-ttu-id="24569-141">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-141">Position?</span></span> |<span data-ttu-id="24569-142">1</span><span class="sxs-lookup"><span data-stu-id="24569-142">1</span></span> |
| <span data-ttu-id="24569-143">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-143">Default value</span></span> |<span data-ttu-id="24569-144">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-144">none</span></span> |
| <span data-ttu-id="24569-145">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-145">Accept pipeline input?</span></span> |<span data-ttu-id="24569-146">false</span><span class="sxs-lookup"><span data-stu-id="24569-146">false</span></span> |
| <span data-ttu-id="24569-147">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-147">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-148">false</span><span class="sxs-lookup"><span data-stu-id="24569-148">false</span></span> |

<span data-ttu-id="24569-149">**-Location &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="24569-150">Especifica a localização do recurso de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="24569-151">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-151">Aliases</span></span> | <span data-ttu-id="24569-152">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-153">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-153">Required?</span></span> |<span data-ttu-id="24569-154">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-154">true</span></span> |
| <span data-ttu-id="24569-155">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-155">Position?</span></span> |<span data-ttu-id="24569-156">2</span><span class="sxs-lookup"><span data-stu-id="24569-156">2</span></span> |
| <span data-ttu-id="24569-157">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-157">Default value</span></span> |<span data-ttu-id="24569-158">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-158">none</span></span> |
| <span data-ttu-id="24569-159">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-159">Accept pipeline input?</span></span> |<span data-ttu-id="24569-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-161">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-161">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-162">false</span><span class="sxs-lookup"><span data-stu-id="24569-162">false</span></span> |

<span data-ttu-id="24569-163">**-StorageAccountId &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="24569-164">Especifica uma conta de armazenamento primário associado ao serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="24569-165">Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.</span><span class="sxs-lookup"><span data-stu-id="24569-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="24569-166">Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="24569-167">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-167">Aliases</span></span> | <span data-ttu-id="24569-168">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-169">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-169">Required?</span></span> |<span data-ttu-id="24569-170">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-170">true</span></span> |
| <span data-ttu-id="24569-171">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-171">Position?</span></span> |<span data-ttu-id="24569-172">3</span><span class="sxs-lookup"><span data-stu-id="24569-172">3</span></span> |
| <span data-ttu-id="24569-173">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-173">Default value</span></span> |<span data-ttu-id="24569-174">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-174">none</span></span> |
| <span data-ttu-id="24569-175">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-175">Accept pipeline input?</span></span> |<span data-ttu-id="24569-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-177">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-177">Parameter set name</span></span> |<span data-ttu-id="24569-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="24569-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="24569-179">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-179">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-180">false</span><span class="sxs-lookup"><span data-stu-id="24569-180">false</span></span> |

<span data-ttu-id="24569-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="24569-182">Especifica as contas de armazenamento associado ao serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="24569-183">Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.</span><span class="sxs-lookup"><span data-stu-id="24569-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="24569-184">Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="24569-185">Apenas uma conta de armazenamento pode ser especificada como principal.</span><span class="sxs-lookup"><span data-stu-id="24569-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="24569-186">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-186">Aliases</span></span> | <span data-ttu-id="24569-187">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-188">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-188">Required?</span></span> |<span data-ttu-id="24569-189">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-189">true</span></span> |
| <span data-ttu-id="24569-190">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-190">Position?</span></span> |<span data-ttu-id="24569-191">3</span><span class="sxs-lookup"><span data-stu-id="24569-191">3</span></span> |
| <span data-ttu-id="24569-192">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-192">Default value</span></span> |<span data-ttu-id="24569-193">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-193">none</span></span> |
| <span data-ttu-id="24569-194">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-194">Accept pipeline input?</span></span> |<span data-ttu-id="24569-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-196">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-196">Parameter set name</span></span> |<span data-ttu-id="24569-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="24569-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="24569-198">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-198">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-199">false</span><span class="sxs-lookup"><span data-stu-id="24569-199">false</span></span> |

<span data-ttu-id="24569-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="24569-201">Especifica uma tabela de hash de marcas de saudação que estão associados com o serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="24569-202">Exemplo: @{"tag1"="value1";" tag2 "=: valor2"}</span><span class="sxs-lookup"><span data-stu-id="24569-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="24569-203">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-203">Aliases</span></span> | <span data-ttu-id="24569-204">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-205">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-205">Required?</span></span> |<span data-ttu-id="24569-206">false</span><span class="sxs-lookup"><span data-stu-id="24569-206">false</span></span> |
| <span data-ttu-id="24569-207">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-207">Position?</span></span> |<span data-ttu-id="24569-208">nomeado</span><span class="sxs-lookup"><span data-stu-id="24569-208">named</span></span> |
| <span data-ttu-id="24569-209">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-209">Default value</span></span> |<span data-ttu-id="24569-210">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-210">none</span></span> |
| <span data-ttu-id="24569-211">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-211">Accept pipeline input?</span></span> |<span data-ttu-id="24569-212">false</span><span class="sxs-lookup"><span data-stu-id="24569-212">false</span></span> |
| <span data-ttu-id="24569-213">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-213">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-214">false</span><span class="sxs-lookup"><span data-stu-id="24569-214">false</span></span> |

<span data-ttu-id="24569-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-216">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-217">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-217">Inputs</span></span>
<span data-ttu-id="24569-218">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-219">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-219">Outputs</span></span>
<span data-ttu-id="24569-220">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="24569-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="24569-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="24569-222">Atualiza um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-223">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-224">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-224">Parameters</span></span>
<span data-ttu-id="24569-225">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-226">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-227">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-227">Aliases</span></span> | <span data-ttu-id="24569-228">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-229">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-229">Required?</span></span> |<span data-ttu-id="24569-230">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-230">true</span></span> |
| <span data-ttu-id="24569-231">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-231">Position?</span></span> |<span data-ttu-id="24569-232">0</span><span class="sxs-lookup"><span data-stu-id="24569-232">0</span></span> |
| <span data-ttu-id="24569-233">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-233">Default Value</span></span> |<span data-ttu-id="24569-234">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-234">none</span></span> |
| <span data-ttu-id="24569-235">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="24569-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-237">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-237">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-238">false</span><span class="sxs-lookup"><span data-stu-id="24569-238">false</span></span> |

<span data-ttu-id="24569-239">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-240">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-241">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-241">Aliases</span></span> | <span data-ttu-id="24569-242">Name</span><span class="sxs-lookup"><span data-stu-id="24569-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="24569-243">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-243">Required?</span></span> |<span data-ttu-id="24569-244">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-244">True</span></span> |
| <span data-ttu-id="24569-245">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-245">Position?</span></span> |<span data-ttu-id="24569-246">1</span><span class="sxs-lookup"><span data-stu-id="24569-246">1</span></span> |
| <span data-ttu-id="24569-247">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-247">Default value</span></span> |<span data-ttu-id="24569-248">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-248">None</span></span> |
| <span data-ttu-id="24569-249">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-249">Accept pipeline input?</span></span> |<span data-ttu-id="24569-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-251">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-251">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-252">Falso</span><span class="sxs-lookup"><span data-stu-id="24569-252">False</span></span> |

<span data-ttu-id="24569-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="24569-254">Especifica as contas de armazenamento associado ao serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="24569-255">Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.</span><span class="sxs-lookup"><span data-stu-id="24569-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="24569-256">Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="24569-257">Apenas uma conta de armazenamento pode ser especificada como principal.</span><span class="sxs-lookup"><span data-stu-id="24569-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="24569-258">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-258">Aliases</span></span> | <span data-ttu-id="24569-259">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-260">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-260">Required?</span></span> |<span data-ttu-id="24569-261">false</span><span class="sxs-lookup"><span data-stu-id="24569-261">false</span></span> |
| <span data-ttu-id="24569-262">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-262">Position?</span></span> |<span data-ttu-id="24569-263">nomeado</span><span class="sxs-lookup"><span data-stu-id="24569-263">Named</span></span> |
| <span data-ttu-id="24569-264">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-264">Default value</span></span> |<span data-ttu-id="24569-265">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-265">none</span></span> |
| <span data-ttu-id="24569-266">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-266">Accept pipeline input?</span></span> |<span data-ttu-id="24569-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-268">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-268">Parameter set name</span></span> |<span data-ttu-id="24569-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="24569-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="24569-270">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-270">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-271">false</span><span class="sxs-lookup"><span data-stu-id="24569-271">false</span></span> |

<span data-ttu-id="24569-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="24569-273">Especifica uma tabela de hash de marcas de saudação que estão associados esse serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="24569-274">marcas de saudação que estão associadas com o serviço de mídia Olá são substituídas com o valor especificado pelo cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="24569-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="24569-275">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-275">Aliases</span></span> | <span data-ttu-id="24569-276">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-277">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-277">Required?</span></span> |<span data-ttu-id="24569-278">false</span><span class="sxs-lookup"><span data-stu-id="24569-278">False</span></span> |
| <span data-ttu-id="24569-279">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-279">Position?</span></span> |<span data-ttu-id="24569-280">nomeado</span><span class="sxs-lookup"><span data-stu-id="24569-280">Named</span></span> |
| <span data-ttu-id="24569-281">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-281">Default value</span></span> |<span data-ttu-id="24569-282">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-282">None</span></span> |
| <span data-ttu-id="24569-283">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-283">Accept pipeline input?</span></span> |<span data-ttu-id="24569-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-285">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-285">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-286">false</span><span class="sxs-lookup"><span data-stu-id="24569-286">false</span></span> |

<span data-ttu-id="24569-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-288">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-289">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-289">Inputs</span></span>
<span data-ttu-id="24569-290">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-291">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-291">Outputs</span></span>
<span data-ttu-id="24569-292">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="24569-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="24569-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="24569-294">Remove um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-295">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-296">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-296">Parameters</span></span>
<span data-ttu-id="24569-297">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-298">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-299">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-299">Aliases</span></span> | <span data-ttu-id="24569-300">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-301">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-301">Required?</span></span> |<span data-ttu-id="24569-302">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-302">true</span></span> |
| <span data-ttu-id="24569-303">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-303">Position?</span></span> |<span data-ttu-id="24569-304">0</span><span class="sxs-lookup"><span data-stu-id="24569-304">0</span></span> |
| <span data-ttu-id="24569-305">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-305">Default value</span></span> |<span data-ttu-id="24569-306">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-306">none</span></span> |
| <span data-ttu-id="24569-307">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-307">Accept pipeline input?</span></span> |<span data-ttu-id="24569-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-309">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-309">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-310">false</span><span class="sxs-lookup"><span data-stu-id="24569-310">false</span></span> |

<span data-ttu-id="24569-311">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-312">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-313">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-313">Aliases</span></span> | <span data-ttu-id="24569-314">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-315">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-315">Required?</span></span> |<span data-ttu-id="24569-316">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-316">true</span></span> |
| <span data-ttu-id="24569-317">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-317">Position?</span></span> |<span data-ttu-id="24569-318">2</span><span class="sxs-lookup"><span data-stu-id="24569-318">2</span></span> |
| <span data-ttu-id="24569-319">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-319">Default value</span></span> |<span data-ttu-id="24569-320">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-320">None</span></span> |
| <span data-ttu-id="24569-321">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-321">Accept pipeline input?</span></span> |<span data-ttu-id="24569-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-323">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-323">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-324">Falso</span><span class="sxs-lookup"><span data-stu-id="24569-324">False</span></span> |

<span data-ttu-id="24569-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-326">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-327">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-327">Inputs</span></span>
<span data-ttu-id="24569-328">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-329">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-329">Outputs</span></span>
<span data-ttu-id="24569-330">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="24569-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="24569-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="24569-332">Obtém todos os serviços de mídia em um grupo de recursos ou um serviço de mídia com um determinado nome.</span><span class="sxs-lookup"><span data-stu-id="24569-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-333">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-333">Syntax</span></span>
<span data-ttu-id="24569-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="24569-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="24569-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="24569-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-336">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-336">Parameters</span></span>
<span data-ttu-id="24569-337">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-338">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-339">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-339">Aliases</span></span> | <span data-ttu-id="24569-340">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-341">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-341">Required?</span></span> |<span data-ttu-id="24569-342">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-342">true</span></span> |
| <span data-ttu-id="24569-343">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-343">Position?</span></span> |<span data-ttu-id="24569-344">0</span><span class="sxs-lookup"><span data-stu-id="24569-344">0</span></span> |
| <span data-ttu-id="24569-345">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-345">Default value</span></span> |<span data-ttu-id="24569-346">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-346">none</span></span> |
| <span data-ttu-id="24569-347">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-347">Accept pipeline input?</span></span> |<span data-ttu-id="24569-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-349">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-349">Parameter set name</span></span> |<span data-ttu-id="24569-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="24569-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="24569-351">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-351">Accept wildcard characters?</span></span>   <span data-ttu-id="24569-352">false</span><span class="sxs-lookup"><span data-stu-id="24569-352">false</span></span>

<span data-ttu-id="24569-353">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-354">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-355">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-355">Aliases</span></span> | <span data-ttu-id="24569-356">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-357">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-357">Required?</span></span> |<span data-ttu-id="24569-358">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-358">true</span></span> |
| <span data-ttu-id="24569-359">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-359">Position?</span></span> |<span data-ttu-id="24569-360">1</span><span class="sxs-lookup"><span data-stu-id="24569-360">1</span></span> |
| <span data-ttu-id="24569-361">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-361">Default value</span></span> |<span data-ttu-id="24569-362">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-362">none</span></span> |
| <span data-ttu-id="24569-363">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-363">Accept pipeline input?</span></span> |<span data-ttu-id="24569-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-365">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-365">Parameter set name</span></span> |<span data-ttu-id="24569-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="24569-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="24569-367">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-367">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-368">false</span><span class="sxs-lookup"><span data-stu-id="24569-368">false</span></span> |

<span data-ttu-id="24569-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-370">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-371">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-371">Inputs</span></span>
<span data-ttu-id="24569-372">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-373">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-373">Outputs</span></span>
<span data-ttu-id="24569-374">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="24569-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="24569-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="24569-376">Obtém as chaves de um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-377">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-378">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-378">Parameters</span></span>
<span data-ttu-id="24569-379">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-380">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-381">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-381">Aliases</span></span> | <span data-ttu-id="24569-382">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-383">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-383">Required?</span></span> |<span data-ttu-id="24569-384">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-384">true</span></span> |
| <span data-ttu-id="24569-385">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-385">Position?</span></span> |<span data-ttu-id="24569-386">0</span><span class="sxs-lookup"><span data-stu-id="24569-386">0</span></span> |
| <span data-ttu-id="24569-387">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-387">Default value</span></span> |<span data-ttu-id="24569-388">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-388">none</span></span> |
| <span data-ttu-id="24569-389">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-389">Accept pipeline input?</span></span> |<span data-ttu-id="24569-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-391">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-391">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-392">false</span><span class="sxs-lookup"><span data-stu-id="24569-392">false</span></span> |

<span data-ttu-id="24569-393">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-394">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-395">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-395">Aliases</span></span> | <span data-ttu-id="24569-396">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-397">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-397">Required?</span></span> |<span data-ttu-id="24569-398">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-398">true</span></span> |
| <span data-ttu-id="24569-399">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-399">Position?</span></span> |<span data-ttu-id="24569-400">1</span><span class="sxs-lookup"><span data-stu-id="24569-400">1</span></span> |
| <span data-ttu-id="24569-401">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-401">Default value</span></span> |<span data-ttu-id="24569-402">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-402">none</span></span> |
| <span data-ttu-id="24569-403">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-403">Accept pipeline input?</span></span> |<span data-ttu-id="24569-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-405">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-405">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-406">false</span><span class="sxs-lookup"><span data-stu-id="24569-406">false</span></span> |

<span data-ttu-id="24569-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-408">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-409">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-409">Inputs</span></span>
<span data-ttu-id="24569-410">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-411">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-411">Outputs</span></span>
<span data-ttu-id="24569-412">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="24569-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="24569-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="24569-414">Regenera uma chave primária ou secundária de um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-415">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-416">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-416">Parameters</span></span>
<span data-ttu-id="24569-417">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-418">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-419">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-419">Aliases</span></span> | <span data-ttu-id="24569-420">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-421">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-421">Required?</span></span> |<span data-ttu-id="24569-422">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-422">true</span></span> |
| <span data-ttu-id="24569-423">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-423">Position?</span></span> |<span data-ttu-id="24569-424">0</span><span class="sxs-lookup"><span data-stu-id="24569-424">0</span></span> |
| <span data-ttu-id="24569-425">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-425">Default value</span></span> |<span data-ttu-id="24569-426">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-426">none</span></span> |
| <span data-ttu-id="24569-427">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-427">Accept pipeline input?</span></span> |<span data-ttu-id="24569-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-429">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-429">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-430">false</span><span class="sxs-lookup"><span data-stu-id="24569-430">false</span></span> |

<span data-ttu-id="24569-431">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-432">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-433">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-433">Aliases</span></span> | <span data-ttu-id="24569-434">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-435">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-435">Required?</span></span> |<span data-ttu-id="24569-436">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-436">true</span></span> |
| <span data-ttu-id="24569-437">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-437">Position?</span></span> |<span data-ttu-id="24569-438">1</span><span class="sxs-lookup"><span data-stu-id="24569-438">1</span></span> |
| <span data-ttu-id="24569-439">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-439">Default value</span></span> |<span data-ttu-id="24569-440">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-440">none</span></span> |
| <span data-ttu-id="24569-441">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-441">Accept pipeline input?</span></span> |<span data-ttu-id="24569-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-443">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-443">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-444">false</span><span class="sxs-lookup"><span data-stu-id="24569-444">false</span></span> |

<span data-ttu-id="24569-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="24569-446">Especifica o tipo de serviço de mídia Olá chave hello.</span><span class="sxs-lookup"><span data-stu-id="24569-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="24569-447">Primária ou Secundária</span><span class="sxs-lookup"><span data-stu-id="24569-447">Primary or Secondary</span></span>

| <span data-ttu-id="24569-448">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-448">Aliases</span></span> | <span data-ttu-id="24569-449">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-450">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-450">Required?</span></span> |<span data-ttu-id="24569-451">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-451">true</span></span> |
| <span data-ttu-id="24569-452">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-452">Position?</span></span> |<span data-ttu-id="24569-453">2</span><span class="sxs-lookup"><span data-stu-id="24569-453">2</span></span> |
| <span data-ttu-id="24569-454">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-454">Default value</span></span> |<span data-ttu-id="24569-455">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-455">none</span></span> |
| <span data-ttu-id="24569-456">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-456">Accept pipeline input?</span></span> |<span data-ttu-id="24569-457">false</span><span class="sxs-lookup"><span data-stu-id="24569-457">false</span></span> |
| <span data-ttu-id="24569-458">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-458">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-459">false</span><span class="sxs-lookup"><span data-stu-id="24569-459">false</span></span> |

<span data-ttu-id="24569-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-461">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-462">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-462">Inputs</span></span>
<span data-ttu-id="24569-463">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toothe cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-464">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-464">Outputs</span></span>
<span data-ttu-id="24569-465">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="24569-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="24569-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="24569-467">Sincroniza as chaves de conta de armazenamento para uma conta de armazenamento associado ao serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="24569-468">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24569-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="24569-469">parâmetros</span><span class="sxs-lookup"><span data-stu-id="24569-469">Parameters</span></span>
<span data-ttu-id="24569-470">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-471">Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="24569-472">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-472">Aliases</span></span> | <span data-ttu-id="24569-473">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-474">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-474">Required?</span></span> |<span data-ttu-id="24569-475">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-475">true</span></span> |
| <span data-ttu-id="24569-476">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-476">Position?</span></span> |<span data-ttu-id="24569-477">0</span><span class="sxs-lookup"><span data-stu-id="24569-477">0</span></span> |
| <span data-ttu-id="24569-478">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-478">Default value</span></span> |<span data-ttu-id="24569-479">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-479">none</span></span> |
| <span data-ttu-id="24569-480">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-480">Accept pipeline input?</span></span> |<span data-ttu-id="24569-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-482">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-482">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-483">false</span><span class="sxs-lookup"><span data-stu-id="24569-483">false</span></span> |

<span data-ttu-id="24569-484">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="24569-485">Especifica o nome de saudação do serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="24569-486">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-486">Aliases</span></span> | <span data-ttu-id="24569-487">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="24569-488">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-488">Required?</span></span> |<span data-ttu-id="24569-489">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-489">true</span></span> |
| <span data-ttu-id="24569-490">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-490">Position?</span></span> |<span data-ttu-id="24569-491">1</span><span class="sxs-lookup"><span data-stu-id="24569-491">1</span></span> |
| <span data-ttu-id="24569-492">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-492">Default value</span></span> |<span data-ttu-id="24569-493">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-493">none</span></span> |
| <span data-ttu-id="24569-494">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-494">Accept pipeline input?</span></span> |<span data-ttu-id="24569-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-496">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-496">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-497">false</span><span class="sxs-lookup"><span data-stu-id="24569-497">false</span></span> |

<span data-ttu-id="24569-498">**-StorageAccountId &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="24569-499">Especifica a conta de armazenamento de saudação associada ao serviço de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="24569-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="24569-500">Aliases</span><span class="sxs-lookup"><span data-stu-id="24569-500">Aliases</span></span> | <span data-ttu-id="24569-501">ID</span><span class="sxs-lookup"><span data-stu-id="24569-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="24569-502">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="24569-502">Required?</span></span> |<span data-ttu-id="24569-503">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="24569-503">true</span></span> |
| <span data-ttu-id="24569-504">Position?</span><span class="sxs-lookup"><span data-stu-id="24569-504">Position?</span></span> |<span data-ttu-id="24569-505">2</span><span class="sxs-lookup"><span data-stu-id="24569-505">2</span></span> |
| <span data-ttu-id="24569-506">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="24569-506">Default value</span></span> |<span data-ttu-id="24569-507">nenhum</span><span class="sxs-lookup"><span data-stu-id="24569-507">none</span></span> |
| <span data-ttu-id="24569-508">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="24569-508">Accept pipeline input?</span></span> |<span data-ttu-id="24569-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="24569-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="24569-510">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="24569-510">Accept wildcard characters?</span></span> |<span data-ttu-id="24569-511">false</span><span class="sxs-lookup"><span data-stu-id="24569-511">false</span></span> |

<span data-ttu-id="24569-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="24569-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="24569-513">Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24569-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="24569-514">Entradas</span><span class="sxs-lookup"><span data-stu-id="24569-514">Inputs</span></span>
<span data-ttu-id="24569-515">tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="24569-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="24569-516">outputs</span><span class="sxs-lookup"><span data-stu-id="24569-516">Outputs</span></span>
<span data-ttu-id="24569-517">tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="24569-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="24569-518">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="24569-518">Next step</span></span>
<span data-ttu-id="24569-519">Confira os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="24569-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24569-520">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="24569-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

