---
title: aaaUse cmdlets do PowerShell com o Azure RemoteApp | Microsoft Docs
description: Saiba como toouse cmdlets do Windows PowerShell no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="624f5-103">Usar os cmdlets do Windows PowerShell com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="624f5-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="624f5-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="624f5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="624f5-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="624f5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="624f5-106">Você pode usar tooadminister de cmdlets do PowerShell do Azure RemoteApp hello e manter suas coleções.</span><span class="sxs-lookup"><span data-stu-id="624f5-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="624f5-107">Use Olá tooget informações de Introdução a seguir.</span><span class="sxs-lookup"><span data-stu-id="624f5-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="624f5-108">Obter Olá cmdlets</span><span class="sxs-lookup"><span data-stu-id="624f5-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="624f5-109">Baixe primeiro o cmdlets do Powershell do Azure Olá [aqui](http://go.microsoft.com/?linkid=9811175), Olá RemoteApp cmdlets são incluídos.</span><span class="sxs-lookup"><span data-stu-id="624f5-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="624f5-110">Check-out Olá [ajuda de cmdlet do Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="624f5-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="624f5-111">Configurar a sua assinatura toouse de cmdlets do Azure</span><span class="sxs-lookup"><span data-stu-id="624f5-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="624f5-112">Execute [neste guia](/powershell/azure/overview) , você pode usar os cmdlets de saudação em relação a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="624f5-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="624f5-113">Você pode usar esses tooget etapas iniciado rapidamente:</span><span class="sxs-lookup"><span data-stu-id="624f5-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="624f5-114">Baixe e instale Olá [cmdlets do PowerShell do Azure](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="624f5-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="624f5-115">Inicie o Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="624f5-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="624f5-116">Executar **Add-AzureAccount** tooauthenticate tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="624f5-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="624f5-117">Quando solicitado, digite Olá o mesmo nome de usuário e senha que você use toosign no portal de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="624f5-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="624f5-118">Executar **Get-AzureSubscription** assinaturas de saudação toolist associadas à sua conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="624f5-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="624f5-119">Executar **Select-AzureSubscription - SubscriptionName &lt;nome da assinatura&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID da assinatura&gt;**  toospecify Olá assinatura toouse.</span><span class="sxs-lookup"><span data-stu-id="624f5-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="624f5-120">Parabéns, o console do PowerShell do Azure está configurado e pronto toouse.</span><span class="sxs-lookup"><span data-stu-id="624f5-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="624f5-121">Lembre-se de que você precisará toorepeate etapas 2 a 5 cada vez que iniciar o console do hello hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="624f5-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="624f5-122">Listar todas as coleções</span><span class="sxs-lookup"><span data-stu-id="624f5-122">List all collections</span></span>
- - -
     <span data-ttu-id="624f5-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="624f5-124">Excluir uma coleção</span><span class="sxs-lookup"><span data-stu-id="624f5-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="624f5-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="624f5-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="624f5-126">Exemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="624f5-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="624f5-127">Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="624f5-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="624f5-128">É simple, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="624f5-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="624f5-129">Olá acima comando publica automaticamente os aplicativos do Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).</span><span class="sxs-lookup"><span data-stu-id="624f5-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="624f5-130">Criação de coleção pode levar 30 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="624f5-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="624f5-131">Portanto, este comando retorna uma ID de acompanhamento que pode ser usada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="624f5-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="624f5-132">Após a coleta de saudação é feita, você pode adicionar a coleção de toohello de usuários com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="624f5-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="624f5-133">E pronto!</span><span class="sxs-lookup"><span data-stu-id="624f5-133">And you're done!</span></span> <span data-ttu-id="624f5-134">Esse usuário deve ser capaz de tooconnect toohello aplicativo usando o cliente do Azure RemoteApp Olá encontrado [aqui](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="624f5-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="624f5-135">Cmdlets disponíveis</span><span class="sxs-lookup"><span data-stu-id="624f5-135">Available cmdlets</span></span>
<span data-ttu-id="624f5-136">Há muitos outros comandos que temos, documentação de saudação para eles estarão disponíveis em breve:</span><span class="sxs-lookup"><span data-stu-id="624f5-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="624f5-137">Cmdlets de coleção de RemoteApp básicos:</span><span class="sxs-lookup"><span data-stu-id="624f5-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="624f5-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="624f5-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="624f5-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="624f5-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="624f5-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="624f5-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="624f5-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="624f5-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="624f5-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="624f5-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="624f5-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="624f5-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="624f5-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="624f5-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="624f5-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="624f5-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="624f5-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="624f5-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="624f5-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="624f5-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="624f5-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="624f5-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="624f5-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="624f5-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="624f5-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="624f5-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="624f5-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="624f5-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="624f5-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="624f5-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="624f5-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="624f5-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="624f5-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="624f5-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="624f5-157">Cmdlets da rede virtual do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="624f5-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="624f5-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="624f5-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="624f5-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="624f5-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="624f5-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="624f5-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="624f5-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="624f5-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="624f5-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="624f5-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="624f5-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="624f5-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="624f5-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="624f5-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="624f5-165">Cmdlets de imagem do modelo do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="624f5-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="624f5-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="624f5-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="624f5-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="624f5-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="624f5-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="624f5-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="624f5-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="624f5-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="624f5-170">Outros cmdlets do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="624f5-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="624f5-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="624f5-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="624f5-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="624f5-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="624f5-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="624f5-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="624f5-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="624f5-174">Get-AzureRemoteAppOperationResult</span></span>

