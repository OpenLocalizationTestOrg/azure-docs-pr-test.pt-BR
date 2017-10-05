---
title: "Gerenciar contas dos Serviços de Mídia do Azure com o PowerShell"
description: "Saiba como gerenciar contas dos Serviços de Mídia do Azure com cmdlets do PowerShell."
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
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="6fdd1-103">Gerenciar contas dos Serviços de Mídia do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fdd1-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fdd1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6fdd1-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="6fdd1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fdd1-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="6fdd1-106">REST</span><span class="sxs-lookup"><span data-stu-id="6fdd1-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="6fdd1-107">Para poder criar uma conta de Serviços de Mídia do Azure, você deve ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="6fdd1-108">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6fdd1-109">Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Avaliação Gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="6fdd1-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6fdd1-110">Overview</span></span>
<span data-ttu-id="6fdd1-111">Este artigo lista os cmdlets do Azure PowerShell para os Serviços de Mídia do Azure (AMS) na estrutura do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="6fdd1-112">Os cmdlets existem no namespace **Microsoft.Azure.Commands.Media** .</span><span class="sxs-lookup"><span data-stu-id="6fdd1-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="6fdd1-113">Versões</span><span class="sxs-lookup"><span data-stu-id="6fdd1-113">Versions</span></span>
<span data-ttu-id="6fdd1-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="6fdd1-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="6fdd1-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="6fdd1-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="6fdd1-116">Cria um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-117">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-117">Syntax</span></span>
<span data-ttu-id="6fdd1-118">Conjunto de Parâmetros: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="6fdd1-119">Conjunto de Parâmetros: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-120">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-120">Parameters</span></span>
<span data-ttu-id="6fdd1-121">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-122">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-123">Aliases</span></span> | <span data-ttu-id="6fdd1-124">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-125">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-125">Required?</span></span> |<span data-ttu-id="6fdd1-126">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-126">true</span></span> |
| <span data-ttu-id="6fdd1-127">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-127">Position?</span></span> |<span data-ttu-id="6fdd1-128">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-128">0</span></span> |
| <span data-ttu-id="6fdd1-129">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-129">Default value</span></span> |<span data-ttu-id="6fdd1-130">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-130">none</span></span> |
| <span data-ttu-id="6fdd1-131">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-131">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-133">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-133">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-134">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-134">false</span></span> |

<span data-ttu-id="6fdd1-135">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-136">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-137">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-137">Aliases</span></span> | <span data-ttu-id="6fdd1-138">Name</span><span class="sxs-lookup"><span data-stu-id="6fdd1-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-139">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-139">Required?</span></span> |<span data-ttu-id="6fdd1-140">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-140">true</span></span> |
| <span data-ttu-id="6fdd1-141">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-141">Position?</span></span> |<span data-ttu-id="6fdd1-142">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-142">1</span></span> |
| <span data-ttu-id="6fdd1-143">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-143">Default value</span></span> |<span data-ttu-id="6fdd1-144">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-144">none</span></span> |
| <span data-ttu-id="6fdd1-145">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-145">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-146">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-146">false</span></span> |
| <span data-ttu-id="6fdd1-147">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-147">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-148">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-148">false</span></span> |

<span data-ttu-id="6fdd1-149">**-Location &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-150">Especifica a localização do recurso do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="6fdd1-151">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-151">Aliases</span></span> | <span data-ttu-id="6fdd1-152">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-153">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-153">Required?</span></span> |<span data-ttu-id="6fdd1-154">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-154">true</span></span> |
| <span data-ttu-id="6fdd1-155">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-155">Position?</span></span> |<span data-ttu-id="6fdd1-156">2</span><span class="sxs-lookup"><span data-stu-id="6fdd1-156">2</span></span> |
| <span data-ttu-id="6fdd1-157">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-157">Default value</span></span> |<span data-ttu-id="6fdd1-158">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-158">none</span></span> |
| <span data-ttu-id="6fdd1-159">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-159">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-161">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-161">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-162">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-162">false</span></span> |

<span data-ttu-id="6fdd1-163">**-StorageAccountId &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-164">Especifica uma conta de armazenamento principal associada ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="6fdd1-165">Nova conta de armazenamento (criada com a API do Gerenciador de Recursos) com suporte apenas.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="6fdd1-166">A conta de armazenamento deve existir e ter o mesmo local do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="6fdd1-167">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-167">Aliases</span></span> | <span data-ttu-id="6fdd1-168">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-169">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-169">Required?</span></span> |<span data-ttu-id="6fdd1-170">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-170">true</span></span> |
| <span data-ttu-id="6fdd1-171">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-171">Position?</span></span> |<span data-ttu-id="6fdd1-172">3</span><span class="sxs-lookup"><span data-stu-id="6fdd1-172">3</span></span> |
| <span data-ttu-id="6fdd1-173">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-173">Default value</span></span> |<span data-ttu-id="6fdd1-174">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-174">none</span></span> |
| <span data-ttu-id="6fdd1-175">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-175">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-177">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-177">Parameter set name</span></span> |<span data-ttu-id="6fdd1-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="6fdd1-179">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-179">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-180">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-180">false</span></span> |

<span data-ttu-id="6fdd1-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="6fdd1-182">Especifica as contas de armazenamento associadas ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="6fdd1-183">Nova conta de armazenamento (criada com a API do Gerenciador de Recursos) com suporte apenas.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="6fdd1-184">A conta de armazenamento deve existir e ter o mesmo local do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="6fdd1-185">Apenas uma conta de armazenamento pode ser especificada como principal.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="6fdd1-186">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-186">Aliases</span></span> | <span data-ttu-id="6fdd1-187">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-188">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-188">Required?</span></span> |<span data-ttu-id="6fdd1-189">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-189">true</span></span> |
| <span data-ttu-id="6fdd1-190">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-190">Position?</span></span> |<span data-ttu-id="6fdd1-191">3</span><span class="sxs-lookup"><span data-stu-id="6fdd1-191">3</span></span> |
| <span data-ttu-id="6fdd1-192">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-192">Default value</span></span> |<span data-ttu-id="6fdd1-193">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-193">none</span></span> |
| <span data-ttu-id="6fdd1-194">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-194">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-196">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-196">Parameter set name</span></span> |<span data-ttu-id="6fdd1-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="6fdd1-198">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-198">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-199">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-199">false</span></span> |

<span data-ttu-id="6fdd1-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="6fdd1-201">Especifica uma tabela de hash das marcações associadas ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="6fdd1-202">Exemplo: @{"tag1"="value1";" tag2 "=: valor2"}</span><span class="sxs-lookup"><span data-stu-id="6fdd1-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="6fdd1-203">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-203">Aliases</span></span> | <span data-ttu-id="6fdd1-204">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-205">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-205">Required?</span></span> |<span data-ttu-id="6fdd1-206">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-206">false</span></span> |
| <span data-ttu-id="6fdd1-207">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-207">Position?</span></span> |<span data-ttu-id="6fdd1-208">nomeado</span><span class="sxs-lookup"><span data-stu-id="6fdd1-208">named</span></span> |
| <span data-ttu-id="6fdd1-209">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-209">Default value</span></span> |<span data-ttu-id="6fdd1-210">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-210">none</span></span> |
| <span data-ttu-id="6fdd1-211">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-211">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-212">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-212">false</span></span> |
| <span data-ttu-id="6fdd1-213">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-213">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-214">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-214">false</span></span> |

<span data-ttu-id="6fdd1-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-216">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-217">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-217">Inputs</span></span>
<span data-ttu-id="6fdd1-218">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-219">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-219">Outputs</span></span>
<span data-ttu-id="6fdd1-220">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="6fdd1-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="6fdd1-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="6fdd1-222">Atualiza um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-223">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-224">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-224">Parameters</span></span>
<span data-ttu-id="6fdd1-225">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-226">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-227">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-227">Aliases</span></span> | <span data-ttu-id="6fdd1-228">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-229">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-229">Required?</span></span> |<span data-ttu-id="6fdd1-230">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-230">true</span></span> |
| <span data-ttu-id="6fdd1-231">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-231">Position?</span></span> |<span data-ttu-id="6fdd1-232">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-232">0</span></span> |
| <span data-ttu-id="6fdd1-233">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-233">Default Value</span></span> |<span data-ttu-id="6fdd1-234">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-234">none</span></span> |
| <span data-ttu-id="6fdd1-235">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="6fdd1-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-237">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-237">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-238">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-238">false</span></span> |

<span data-ttu-id="6fdd1-239">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-240">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-241">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-241">Aliases</span></span> | <span data-ttu-id="6fdd1-242">Name</span><span class="sxs-lookup"><span data-stu-id="6fdd1-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-243">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-243">Required?</span></span> |<span data-ttu-id="6fdd1-244">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-244">True</span></span> |
| <span data-ttu-id="6fdd1-245">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-245">Position?</span></span> |<span data-ttu-id="6fdd1-246">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-246">1</span></span> |
| <span data-ttu-id="6fdd1-247">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-247">Default value</span></span> |<span data-ttu-id="6fdd1-248">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-248">None</span></span> |
| <span data-ttu-id="6fdd1-249">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-249">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-251">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-251">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-252">Falso</span><span class="sxs-lookup"><span data-stu-id="6fdd1-252">False</span></span> |

<span data-ttu-id="6fdd1-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="6fdd1-254">Especifica as contas de armazenamento associadas ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="6fdd1-255">Nova conta de armazenamento (criada com a API do Gerenciador de Recursos) com suporte apenas.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="6fdd1-256">A conta de armazenamento deve existir e ter o mesmo local do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="6fdd1-257">Apenas uma conta de armazenamento pode ser especificada como principal.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="6fdd1-258">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-258">Aliases</span></span> | <span data-ttu-id="6fdd1-259">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-260">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-260">Required?</span></span> |<span data-ttu-id="6fdd1-261">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-261">false</span></span> |
| <span data-ttu-id="6fdd1-262">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-262">Position?</span></span> |<span data-ttu-id="6fdd1-263">nomeado</span><span class="sxs-lookup"><span data-stu-id="6fdd1-263">Named</span></span> |
| <span data-ttu-id="6fdd1-264">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-264">Default value</span></span> |<span data-ttu-id="6fdd1-265">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-265">none</span></span> |
| <span data-ttu-id="6fdd1-266">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-266">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-268">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-268">Parameter set name</span></span> |<span data-ttu-id="6fdd1-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="6fdd1-270">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-270">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-271">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-271">false</span></span> |

<span data-ttu-id="6fdd1-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="6fdd1-273">Especifica uma tabela de hash das marcações associadas a este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="6fdd1-274">As marcações associadas ao serviço de mídia são substituídas pelo valor especificado pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="6fdd1-275">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-275">Aliases</span></span> | <span data-ttu-id="6fdd1-276">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-277">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-277">Required?</span></span> |<span data-ttu-id="6fdd1-278">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-278">False</span></span> |
| <span data-ttu-id="6fdd1-279">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-279">Position?</span></span> |<span data-ttu-id="6fdd1-280">nomeado</span><span class="sxs-lookup"><span data-stu-id="6fdd1-280">Named</span></span> |
| <span data-ttu-id="6fdd1-281">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-281">Default value</span></span> |<span data-ttu-id="6fdd1-282">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-282">None</span></span> |
| <span data-ttu-id="6fdd1-283">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-283">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-285">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-285">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-286">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-286">false</span></span> |

<span data-ttu-id="6fdd1-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-288">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-289">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-289">Inputs</span></span>
<span data-ttu-id="6fdd1-290">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-291">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-291">Outputs</span></span>
<span data-ttu-id="6fdd1-292">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="6fdd1-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="6fdd1-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="6fdd1-294">Remove um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-295">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-296">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-296">Parameters</span></span>
<span data-ttu-id="6fdd1-297">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-298">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-299">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-299">Aliases</span></span> | <span data-ttu-id="6fdd1-300">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-301">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-301">Required?</span></span> |<span data-ttu-id="6fdd1-302">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-302">true</span></span> |
| <span data-ttu-id="6fdd1-303">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-303">Position?</span></span> |<span data-ttu-id="6fdd1-304">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-304">0</span></span> |
| <span data-ttu-id="6fdd1-305">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-305">Default value</span></span> |<span data-ttu-id="6fdd1-306">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-306">none</span></span> |
| <span data-ttu-id="6fdd1-307">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-307">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-309">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-309">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-310">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-310">false</span></span> |

<span data-ttu-id="6fdd1-311">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-312">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-313">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-313">Aliases</span></span> | <span data-ttu-id="6fdd1-314">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-315">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-315">Required?</span></span> |<span data-ttu-id="6fdd1-316">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-316">true</span></span> |
| <span data-ttu-id="6fdd1-317">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-317">Position?</span></span> |<span data-ttu-id="6fdd1-318">2</span><span class="sxs-lookup"><span data-stu-id="6fdd1-318">2</span></span> |
| <span data-ttu-id="6fdd1-319">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-319">Default value</span></span> |<span data-ttu-id="6fdd1-320">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-320">None</span></span> |
| <span data-ttu-id="6fdd1-321">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-321">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-323">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-323">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-324">Falso</span><span class="sxs-lookup"><span data-stu-id="6fdd1-324">False</span></span> |

<span data-ttu-id="6fdd1-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-326">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-327">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-327">Inputs</span></span>
<span data-ttu-id="6fdd1-328">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-329">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-329">Outputs</span></span>
<span data-ttu-id="6fdd1-330">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="6fdd1-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="6fdd1-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="6fdd1-332">Obtém todos os serviços de mídia em um grupo de recursos ou um serviço de mídia com um determinado nome.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-333">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-333">Syntax</span></span>
<span data-ttu-id="6fdd1-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="6fdd1-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-336">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-336">Parameters</span></span>
<span data-ttu-id="6fdd1-337">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-338">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-339">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-339">Aliases</span></span> | <span data-ttu-id="6fdd1-340">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-341">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-341">Required?</span></span> |<span data-ttu-id="6fdd1-342">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-342">true</span></span> |
| <span data-ttu-id="6fdd1-343">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-343">Position?</span></span> |<span data-ttu-id="6fdd1-344">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-344">0</span></span> |
| <span data-ttu-id="6fdd1-345">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-345">Default value</span></span> |<span data-ttu-id="6fdd1-346">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-346">none</span></span> |
| <span data-ttu-id="6fdd1-347">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-347">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-349">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-349">Parameter set name</span></span> |<span data-ttu-id="6fdd1-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="6fdd1-351">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-351">Accept wildcard characters?</span></span>   <span data-ttu-id="6fdd1-352">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-352">false</span></span>

<span data-ttu-id="6fdd1-353">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-354">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-355">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-355">Aliases</span></span> | <span data-ttu-id="6fdd1-356">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-357">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-357">Required?</span></span> |<span data-ttu-id="6fdd1-358">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-358">true</span></span> |
| <span data-ttu-id="6fdd1-359">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-359">Position?</span></span> |<span data-ttu-id="6fdd1-360">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-360">1</span></span> |
| <span data-ttu-id="6fdd1-361">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-361">Default value</span></span> |<span data-ttu-id="6fdd1-362">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-362">none</span></span> |
| <span data-ttu-id="6fdd1-363">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-363">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-365">Nome do conjunto de parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-365">Parameter set name</span></span> |<span data-ttu-id="6fdd1-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="6fdd1-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="6fdd1-367">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-367">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-368">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-368">false</span></span> |

<span data-ttu-id="6fdd1-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-370">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-371">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-371">Inputs</span></span>
<span data-ttu-id="6fdd1-372">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-373">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-373">Outputs</span></span>
<span data-ttu-id="6fdd1-374">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="6fdd1-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="6fdd1-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="6fdd1-376">Obtém as chaves de um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-377">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-378">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-378">Parameters</span></span>
<span data-ttu-id="6fdd1-379">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-380">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-381">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-381">Aliases</span></span> | <span data-ttu-id="6fdd1-382">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-383">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-383">Required?</span></span> |<span data-ttu-id="6fdd1-384">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-384">true</span></span> |
| <span data-ttu-id="6fdd1-385">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-385">Position?</span></span> |<span data-ttu-id="6fdd1-386">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-386">0</span></span> |
| <span data-ttu-id="6fdd1-387">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-387">Default value</span></span> |<span data-ttu-id="6fdd1-388">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-388">none</span></span> |
| <span data-ttu-id="6fdd1-389">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-389">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-391">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-391">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-392">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-392">false</span></span> |

<span data-ttu-id="6fdd1-393">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-394">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-395">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-395">Aliases</span></span> | <span data-ttu-id="6fdd1-396">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-397">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-397">Required?</span></span> |<span data-ttu-id="6fdd1-398">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-398">true</span></span> |
| <span data-ttu-id="6fdd1-399">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-399">Position?</span></span> |<span data-ttu-id="6fdd1-400">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-400">1</span></span> |
| <span data-ttu-id="6fdd1-401">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-401">Default value</span></span> |<span data-ttu-id="6fdd1-402">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-402">none</span></span> |
| <span data-ttu-id="6fdd1-403">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-403">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-405">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-405">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-406">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-406">false</span></span> |

<span data-ttu-id="6fdd1-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-408">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-409">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-409">Inputs</span></span>
<span data-ttu-id="6fdd1-410">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-411">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-411">Outputs</span></span>
<span data-ttu-id="6fdd1-412">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="6fdd1-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="6fdd1-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="6fdd1-414">Regenera uma chave primária ou secundária de um serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-415">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-416">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-416">Parameters</span></span>
<span data-ttu-id="6fdd1-417">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-418">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-419">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-419">Aliases</span></span> | <span data-ttu-id="6fdd1-420">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-421">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-421">Required?</span></span> |<span data-ttu-id="6fdd1-422">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-422">true</span></span> |
| <span data-ttu-id="6fdd1-423">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-423">Position?</span></span> |<span data-ttu-id="6fdd1-424">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-424">0</span></span> |
| <span data-ttu-id="6fdd1-425">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-425">Default value</span></span> |<span data-ttu-id="6fdd1-426">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-426">none</span></span> |
| <span data-ttu-id="6fdd1-427">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-427">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-429">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-429">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-430">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-430">false</span></span> |

<span data-ttu-id="6fdd1-431">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-432">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-433">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-433">Aliases</span></span> | <span data-ttu-id="6fdd1-434">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-435">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-435">Required?</span></span> |<span data-ttu-id="6fdd1-436">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-436">true</span></span> |
| <span data-ttu-id="6fdd1-437">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-437">Position?</span></span> |<span data-ttu-id="6fdd1-438">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-438">1</span></span> |
| <span data-ttu-id="6fdd1-439">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-439">Default value</span></span> |<span data-ttu-id="6fdd1-440">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-440">none</span></span> |
| <span data-ttu-id="6fdd1-441">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-441">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-443">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-443">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-444">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-444">false</span></span> |

<span data-ttu-id="6fdd1-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="6fdd1-446">Especifica o tipo de chave do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="6fdd1-447">Primária ou Secundária</span><span class="sxs-lookup"><span data-stu-id="6fdd1-447">Primary or Secondary</span></span>

| <span data-ttu-id="6fdd1-448">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-448">Aliases</span></span> | <span data-ttu-id="6fdd1-449">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-450">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-450">Required?</span></span> |<span data-ttu-id="6fdd1-451">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-451">true</span></span> |
| <span data-ttu-id="6fdd1-452">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-452">Position?</span></span> |<span data-ttu-id="6fdd1-453">2</span><span class="sxs-lookup"><span data-stu-id="6fdd1-453">2</span></span> |
| <span data-ttu-id="6fdd1-454">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-454">Default value</span></span> |<span data-ttu-id="6fdd1-455">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-455">none</span></span> |
| <span data-ttu-id="6fdd1-456">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-456">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-457">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-457">false</span></span> |
| <span data-ttu-id="6fdd1-458">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-458">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-459">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-459">false</span></span> |

<span data-ttu-id="6fdd1-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-461">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-462">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-462">Inputs</span></span>
<span data-ttu-id="6fdd1-463">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-464">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-464">Outputs</span></span>
<span data-ttu-id="6fdd1-465">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="6fdd1-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="6fdd1-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="6fdd1-467">Sincroniza as chaves da conta de armazenamento para uma conta de armazenamento associada ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="6fdd1-468">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fdd1-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="6fdd1-469">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fdd1-469">Parameters</span></span>
<span data-ttu-id="6fdd1-470">**-ResourceGroupName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-471">Especifica o nome do grupo de recursos ao qual pertence este serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="6fdd1-472">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-472">Aliases</span></span> | <span data-ttu-id="6fdd1-473">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-474">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-474">Required?</span></span> |<span data-ttu-id="6fdd1-475">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-475">true</span></span> |
| <span data-ttu-id="6fdd1-476">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-476">Position?</span></span> |<span data-ttu-id="6fdd1-477">0</span><span class="sxs-lookup"><span data-stu-id="6fdd1-477">0</span></span> |
| <span data-ttu-id="6fdd1-478">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-478">Default value</span></span> |<span data-ttu-id="6fdd1-479">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-479">none</span></span> |
| <span data-ttu-id="6fdd1-480">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-480">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-482">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-482">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-483">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-483">false</span></span> |

<span data-ttu-id="6fdd1-484">**-AccountName &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-485">Especifica o nome do serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="6fdd1-486">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-486">Aliases</span></span> | <span data-ttu-id="6fdd1-487">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-488">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-488">Required?</span></span> |<span data-ttu-id="6fdd1-489">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-489">true</span></span> |
| <span data-ttu-id="6fdd1-490">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-490">Position?</span></span> |<span data-ttu-id="6fdd1-491">1</span><span class="sxs-lookup"><span data-stu-id="6fdd1-491">1</span></span> |
| <span data-ttu-id="6fdd1-492">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-492">Default value</span></span> |<span data-ttu-id="6fdd1-493">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-493">none</span></span> |
| <span data-ttu-id="6fdd1-494">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-494">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-496">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-496">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-497">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-497">false</span></span> |

<span data-ttu-id="6fdd1-498">**-StorageAccountId &lt;Cadeia de caracteres&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="6fdd1-499">Especifica a conta de armazenamento associada ao serviço de mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="6fdd1-500">Aliases</span><span class="sxs-lookup"><span data-stu-id="6fdd1-500">Aliases</span></span> | <span data-ttu-id="6fdd1-501">ID</span><span class="sxs-lookup"><span data-stu-id="6fdd1-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="6fdd1-502">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-502">Required?</span></span> |<span data-ttu-id="6fdd1-503">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fdd1-503">true</span></span> |
| <span data-ttu-id="6fdd1-504">Position?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-504">Position?</span></span> |<span data-ttu-id="6fdd1-505">2</span><span class="sxs-lookup"><span data-stu-id="6fdd1-505">2</span></span> |
| <span data-ttu-id="6fdd1-506">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="6fdd1-506">Default value</span></span> |<span data-ttu-id="6fdd1-507">nenhum</span><span class="sxs-lookup"><span data-stu-id="6fdd1-507">none</span></span> |
| <span data-ttu-id="6fdd1-508">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-508">Accept pipeline input?</span></span> |<span data-ttu-id="6fdd1-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="6fdd1-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="6fdd1-510">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="6fdd1-510">Accept wildcard characters?</span></span> |<span data-ttu-id="6fdd1-511">false</span><span class="sxs-lookup"><span data-stu-id="6fdd1-511">false</span></span> |

<span data-ttu-id="6fdd1-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="6fdd1-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="6fdd1-513">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="6fdd1-514">Entradas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-514">Inputs</span></span>
<span data-ttu-id="6fdd1-515">O tipo de entrada é o tipo dos objetos que você pode enviar ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="6fdd1-516">Saídas</span><span class="sxs-lookup"><span data-stu-id="6fdd1-516">Outputs</span></span>
<span data-ttu-id="6fdd1-517">O tipo de saída é o tipo dos objetos que o cmdlet transmite.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="6fdd1-518">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6fdd1-518">Next step</span></span>
<span data-ttu-id="6fdd1-519">Confira os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="6fdd1-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6fdd1-520">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6fdd1-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

