---
title: Usar os cmdlets do PowerShell com o Azure RemoteApp | Microsoft Docs
description: Saiba como usar os cmdlets do Windows PowerShell com o Azure RemoteApp.
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
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="5a869-103">Usar os cmdlets do Windows PowerShell com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="5a869-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5a869-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="5a869-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5a869-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5a869-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="5a869-106">Você pode usar os cmdlets do Azure RemoteApp PowerShell para administrar e manter suas coleções.</span><span class="sxs-lookup"><span data-stu-id="5a869-106">You can use the Azure RemoteApp PowerShell cmdlets to administer and maintain your collections.</span></span> <span data-ttu-id="5a869-107">Use as informações a seguir para começar.</span><span class="sxs-lookup"><span data-stu-id="5a869-107">Use the following information to get started.</span></span>

## <a name="get-the-cmdlets"></a><span data-ttu-id="5a869-108">Obtenha os cmdlets</span><span class="sxs-lookup"><span data-stu-id="5a869-108">Get the cmdlets</span></span>
- - -
<span data-ttu-id="5a869-109">Baixe primeiro os cmdlets do Azure PowerShell [aqui](http://go.microsoft.com/?linkid=9811175), os do RemoteApp estão incluídos nele.</span><span class="sxs-lookup"><span data-stu-id="5a869-109">First download the Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), the RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="5a869-110">Confira a [ajuda do cmdlet do Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="5a869-110">Check out the [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a><span data-ttu-id="5a869-111">Configurar os cmdlets do Azure para usar sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5a869-111">Configure Azure cmdlets to use your subscription</span></span>
- - -
<span data-ttu-id="5a869-112">Siga [este guia](/powershell/azure/overview) para que possa usar os cmdlets em relação à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a869-112">Follow [this guide](/powershell/azure/overview) so you can use the cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="5a869-113">Você pode usar estas etapas para começar rapidamente:</span><span class="sxs-lookup"><span data-stu-id="5a869-113">You can use these steps to get started quickly:</span></span>

1. <span data-ttu-id="5a869-114">Baixe e instale os [cmdlets do Azure PowerShell](http://go.microsoft.com/?linkid=9811175).</span><span class="sxs-lookup"><span data-stu-id="5a869-114">Download and install the [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="5a869-115">Inicie o Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a869-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="5a869-116">Execute **Add-AzureAccount** para autenticar sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a869-116">Run **Add-AzureAccount** to authenticate to your Azure subscription.</span></span> <span data-ttu-id="5a869-117">Quando solicitado, insira o mesmo nome de usuário e a senha que você usa para entrar no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a869-117">When prompted, enter the same user name and password that you use to sign in to Azure portal.</span></span>  
4. <span data-ttu-id="5a869-118">Execute **Get-AzureSubscription** para listar as assinaturas associadas à sua conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="5a869-118">Run **Get-AzureSubscription** to list the subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="5a869-119">Execute **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** ou **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** para especificar a assinatura a ser usada.</span><span class="sxs-lookup"><span data-stu-id="5a869-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** to specify the subscription to use.</span></span>

<span data-ttu-id="5a869-120">Parabéns, seu console do Azure PowerShell está configurado e pronto para usar.</span><span class="sxs-lookup"><span data-stu-id="5a869-120">Congratulations, your Azure PowerShell console is configured and ready to use.</span></span> <span data-ttu-id="5a869-121">Lembre-se de que você precisará repetir as etapas 2 a 5 sempre que iniciar o console do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a869-121">Be aware that you'll need to repeate steps 2 through 5 each time you start the the Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="5a869-122">Listar todas as coleções</span><span class="sxs-lookup"><span data-stu-id="5a869-122">List all collections</span></span>
- - -
     <span data-ttu-id="5a869-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="5a869-124">Excluir uma coleção</span><span class="sxs-lookup"><span data-stu-id="5a869-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="5a869-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="5a869-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="5a869-126">Exemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="5a869-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="5a869-127">Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="5a869-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="5a869-128">É simples, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a869-128">It's simple, run the following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="5a869-129">O comando acima publica automaticamente os aplicativos do Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio e Word).</span><span class="sxs-lookup"><span data-stu-id="5a869-129">The above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="5a869-130">A criação de uma coleção pode levar 30 minutos ou mais para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="5a869-130">Collection creation can take 30 minutes or longer to complete.</span></span> <span data-ttu-id="5a869-131">Portanto, este comando retorna uma ID de acompanhamento que pode ser usada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5a869-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="5a869-132">Após a coleta ser feita, você pode adicionar usuários à coleção com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a869-132">After the collection is done, you can add users to the collection with the following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="5a869-133">E pronto!</span><span class="sxs-lookup"><span data-stu-id="5a869-133">And you're done!</span></span> <span data-ttu-id="5a869-134">Esse usuário deve ser capaz de se conectar ao aplicativo usando o cliente do Azure RemoteApp encontrado [aqui](https://www.remoteapp.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5a869-134">That user should be able to connect to the application using the Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="5a869-135">Cmdlets disponíveis</span><span class="sxs-lookup"><span data-stu-id="5a869-135">Available cmdlets</span></span>
<span data-ttu-id="5a869-136">Há muitos outros comandos que temos, a documentação para eles será lançada em breve:</span><span class="sxs-lookup"><span data-stu-id="5a869-136">There are lots of other commands that we have, the documentation for them will be coming shortly:</span></span>

<span data-ttu-id="5a869-137">Cmdlets de coleção de RemoteApp básicos:</span><span class="sxs-lookup"><span data-stu-id="5a869-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="5a869-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="5a869-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="5a869-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="5a869-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="5a869-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="5a869-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="5a869-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="5a869-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="5a869-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="5a869-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="5a869-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="5a869-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="5a869-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="5a869-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="5a869-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="5a869-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="5a869-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="5a869-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="5a869-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="5a869-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="5a869-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="5a869-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="5a869-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="5a869-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="5a869-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="5a869-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="5a869-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="5a869-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="5a869-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="5a869-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="5a869-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="5a869-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="5a869-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="5a869-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="5a869-157">Cmdlets da rede virtual do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="5a869-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="5a869-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="5a869-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="5a869-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="5a869-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="5a869-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="5a869-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="5a869-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="5a869-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="5a869-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="5a869-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="5a869-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="5a869-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="5a869-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="5a869-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="5a869-165">Cmdlets de imagem do modelo do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="5a869-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="5a869-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="5a869-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="5a869-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="5a869-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="5a869-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="5a869-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="5a869-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="5a869-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="5a869-170">Outros cmdlets do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="5a869-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="5a869-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="5a869-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="5a869-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="5a869-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="5a869-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="5a869-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="5a869-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="5a869-174">Get-AzureRemoteAppOperationResult</span></span>

