---
title: "Publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp (versão prévia) | Microsoft Docs"
description: "Saiba como pode publicar aplicativos para usuários individuais, em vez de depender de grupos no Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="f7c84-103">Publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp (Visualização)</span><span class="sxs-lookup"><span data-stu-id="f7c84-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f7c84-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f7c84-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f7c84-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f7c84-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f7c84-106">Este artigo explica como publicar aplicativos para usuários individuais em uma coleção do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f7c84-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="f7c84-107">Essa é uma nova funcionalidade no Azure RemoteApp, atualmente em visualização particular, e está disponível somente para usuários pioneiros específicos para fins de avaliação.</span><span class="sxs-lookup"><span data-stu-id="f7c84-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="f7c84-108">Originalmente, o Azure RemoAppte habilitava apenas uma maneira de publicar aplicativos: o administrador publicava os aplicativos a partir da imagem e eles ficavam visíveis para todos os usuários na coleção.</span><span class="sxs-lookup"><span data-stu-id="f7c84-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="f7c84-109">Um cenário comum é incluir vários aplicativos em uma única imagem e implantar uma coleção para reduzir os custos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f7c84-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="f7c84-110">Muitas vezes, nem todos os aplicativos são relevantes para todos os usuários. Os administradores preferem publicar aplicativos para usuários individuais, assim, eles não veem aplicativos desnecessários em seu feed de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f7c84-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="f7c84-111">Isso já é possível no Azure RemoteApp, atualmente como um recurso de visualização limitada.</span><span class="sxs-lookup"><span data-stu-id="f7c84-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="f7c84-112">Veja um pequeno resumo sobre a nova funcionalidade:</span><span class="sxs-lookup"><span data-stu-id="f7c84-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="f7c84-113">Uma coleção pode ser definida em um destes dois modos:</span><span class="sxs-lookup"><span data-stu-id="f7c84-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="f7c84-114">o modo de coleção original, em que todos os usuários em uma coleção podem ver todos os aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="f7c84-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="f7c84-115">Esse é o modo padrão.</span><span class="sxs-lookup"><span data-stu-id="f7c84-115">This is the default mode.</span></span>
   * <span data-ttu-id="f7c84-116">o novo modo de aplicativo, em que os usuários veem apenas os aplicativos que foram explicitamente atribuídos a eles</span><span class="sxs-lookup"><span data-stu-id="f7c84-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="f7c84-117">No momento, o modo de aplicativo só pode ser habilitado por meio de cmdlets do PowerShell do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f7c84-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="f7c84-118">Quando é definido como modo de aplicativo, a atribuição de usuário na coleção não pode ser gerenciada por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c84-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="f7c84-119">A atribuição de usuário deve ser gerenciada por meio de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7c84-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="f7c84-120">Os usuários verão apenas os aplicativos publicados diretamente para eles.</span><span class="sxs-lookup"><span data-stu-id="f7c84-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="f7c84-121">No entanto, ainda é possível que um usuário inicie os outros aplicativos disponíveis na imagem, acessando-os diretamente no sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f7c84-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="f7c84-122">Esse recurso não fornece um bloqueio seguro de aplicativos. Ele apenas limita a visibilidade no feed de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f7c84-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="f7c84-123">Se precisar isolar usuários dos aplicativos, será preciso usar coleções separadas para isso.</span><span class="sxs-lookup"><span data-stu-id="f7c84-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="f7c84-124">Como obter os cmdlets do PowerShell do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f7c84-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="f7c84-125">Para experimentar a nova funcionalidade de visualização, você precisará usar os cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7c84-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f7c84-126">No momento, não é possível usar o Portal de Gerenciamento do Azure para habilitar o novo modo de publicação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f7c84-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="f7c84-127">Primeiro, verifique se você tem o [módulo Azure PowerShell](/powershell/azure/overview) instalado.</span><span class="sxs-lookup"><span data-stu-id="f7c84-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="f7c84-128">Em seguida, inicie o console do PowerShell no modo de administrador e execute este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f7c84-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="f7c84-129">Ele solicitará seu nome de usuário e senha do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c84-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="f7c84-130">Depois de conectado, você poderá executar os cmdlets do RemoteApp do Azure em suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c84-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="f7c84-131">Como verificar o modo no qual uma coleção está</span><span class="sxs-lookup"><span data-stu-id="f7c84-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="f7c84-132">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7c84-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Verificar o modo de coleção](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="f7c84-134">A propriedade AclLevel pode ter os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="f7c84-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="f7c84-135">Coleção: o modo de publicação original.</span><span class="sxs-lookup"><span data-stu-id="f7c84-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="f7c84-136">Todos os usuários veem todos os aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="f7c84-136">All users see all published apps.</span></span>
* <span data-ttu-id="f7c84-137">Aplicativo: o novo modo de publicação.</span><span class="sxs-lookup"><span data-stu-id="f7c84-137">Application: the new publishing mode.</span></span> <span data-ttu-id="f7c84-138">Os usuários veem apenas os aplicativos publicados diretamente para eles.</span><span class="sxs-lookup"><span data-stu-id="f7c84-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="f7c84-139">Como alternar para o modo de publicação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="f7c84-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="f7c84-140">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7c84-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="f7c84-141">O estado de publicação do aplicativo será preservado: inicialmente, todos os usuários verão todos os aplicativos publicados originais.</span><span class="sxs-lookup"><span data-stu-id="f7c84-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="f7c84-142">Como listar os usuários que podem ver um aplicativo específico</span><span class="sxs-lookup"><span data-stu-id="f7c84-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="f7c84-143">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7c84-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="f7c84-144">Isso lista todos os usuários que podem ver o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7c84-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="f7c84-145">Observação: você pode ver os aliases de aplicativos (chamados de "alias de aplicativos" na sintaxe acima) executando Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="f7c84-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="f7c84-146">Como atribuir um aplicativo a um usuário</span><span class="sxs-lookup"><span data-stu-id="f7c84-146">How to assign an application to a user</span></span>
<span data-ttu-id="f7c84-147">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7c84-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="f7c84-148">Agora, o usuário verá o aplicativo no cliente RemoteApp do Azure e poderá conectar-se a ele.</span><span class="sxs-lookup"><span data-stu-id="f7c84-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="f7c84-149">Como remover um aplicativo de um usuário</span><span class="sxs-lookup"><span data-stu-id="f7c84-149">How to remove an application from a user</span></span>
<span data-ttu-id="f7c84-150">Execute o cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7c84-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="f7c84-151">Como fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="f7c84-151">Providing feedback</span></span>
<span data-ttu-id="f7c84-152">Agradecemos seus comentários e sugestões sobre este recurso de visualização.</span><span class="sxs-lookup"><span data-stu-id="f7c84-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="f7c84-153">Preencha a [pesquisa](http://www.instant.ly/s/FDdrb) para nos informar sobre sua opinião.</span><span class="sxs-lookup"><span data-stu-id="f7c84-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="f7c84-154">Ainda não teve a oportunidade de experimentar o recurso de visualização?</span><span class="sxs-lookup"><span data-stu-id="f7c84-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="f7c84-155">Se você ainda não participou da visualização, use esta [pesquisa](http://www.instant.ly/s/AY83p) para solicitar acesso.</span><span class="sxs-lookup"><span data-stu-id="f7c84-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

