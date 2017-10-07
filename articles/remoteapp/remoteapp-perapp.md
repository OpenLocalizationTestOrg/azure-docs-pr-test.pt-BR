---
title: "aaaPublish aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure (visualização) | Microsoft Docs"
description: "Saiba como você pode publicar os usuários tooindividual de aplicativos, em vez de dependendo grupos no Azure RemoteApp."
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="29144-103">Publicar aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="29144-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="29144-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="29144-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="29144-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="29144-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="29144-106">Este artigo explica como toopublish aplicativos tooindividual os usuários em uma coleção do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="29144-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="29144-107">Isso é uma nova funcionalidade no Azure RemoteApp, atualmente na visualização privada e pioneiros disponível tooselect apenas para fins de avaliação.</span><span class="sxs-lookup"><span data-stu-id="29144-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="29144-108">Originalmente o Azure RemoteApp habilitado apenas uma maneira de publicação de aplicativos: administrador Olá seria publicar aplicativos de imagem de saudação e estariam visíveis tooall usuários na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="29144-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="29144-109">Um cenário comum é tooinclude muitos aplicativos em uma única imagem e implantar uma coleção em custos de gerenciamento de tooreduce de ordem.</span><span class="sxs-lookup"><span data-stu-id="29144-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="29144-110">Muitas vezes, nem todos os aplicativos são usuários relevantes tooall – os administradores prefere toopublish usuários de tooindividual de aplicativos para que eles não verão os aplicativos desnecessários em seus aplicativos de feed.</span><span class="sxs-lookup"><span data-stu-id="29144-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="29144-111">Isso já é possível no Azure RemoteApp, atualmente como um recurso de visualização limitada.</span><span class="sxs-lookup"><span data-stu-id="29144-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="29144-112">Aqui está um resumo da nova funcionalidade de saudação:</span><span class="sxs-lookup"><span data-stu-id="29144-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="29144-113">Uma coleção pode ser definida em um destes dois modos:</span><span class="sxs-lookup"><span data-stu-id="29144-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="29144-114">Olá original modo de coleta onde todos os usuários em uma coleção podem ver todos os aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="29144-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="29144-115">Este é o modo de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="29144-115">This is hello default mode.</span></span>
   * <span data-ttu-id="29144-116">novo modo de aplicativo Hello, onde os usuários veem somente os aplicativos que foram explicitamente atribuídas toothem</span><span class="sxs-lookup"><span data-stu-id="29144-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="29144-117">No momento de saudação o modo de aplicativo hello só pode ser habilitado usando cmdlets do PowerShell do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="29144-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="29144-118">Ao definir o modo de tooapplication, atribuição de usuário na coleção de saudação não pode ser gerenciado por meio de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29144-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="29144-119">Atribuição do usuário tem toobe gerenciada por meio de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29144-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="29144-120">Os usuários verão apenas aplicativos Olá publicados diretamente toothem.</span><span class="sxs-lookup"><span data-stu-id="29144-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="29144-121">No entanto, talvez ainda seja possível para um usuário toolaunch Olá outros aplicativos disponíveis na imagem de saudação acessando-los diretamente no sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="29144-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="29144-122">Este recurso não fornece um bloqueio seguro de aplicativos; ela apenas limita a visibilidade no aplicativo hello feed.</span><span class="sxs-lookup"><span data-stu-id="29144-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="29144-123">Se você precisar tooisolate usuários de aplicativos, você precisará coleções separadas toouse para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="29144-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="29144-124">Como tooget cmdlets do PowerShell do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="29144-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="29144-125">tootry Olá nova visualização funcionalidade, você precisará toouse cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="29144-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="29144-126">No momento não é toouse possíveis Olá Azure Management portal tooenable Olá nova publicação modo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29144-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="29144-127">Primeiro, verifique se você tem Olá [módulo Azure PowerShell](/powershell/azure/overview) instalado.</span><span class="sxs-lookup"><span data-stu-id="29144-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="29144-128">Em seguida, inicie o console do PowerShell Olá no modo de administrador e execute hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="29144-129">Ele solicitará seu nome de usuário e senha do Azure.</span><span class="sxs-lookup"><span data-stu-id="29144-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="29144-130">Depois de conectado, será capaz de toorun cmdlets do Azure RemoteApp em relação a suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="29144-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="29144-131">Como toocheck modo no qual uma coleção está em</span><span class="sxs-lookup"><span data-stu-id="29144-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="29144-132">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Verificar o modo de coleta de saudação](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="29144-134">Olá AclLevel propriedade pode ter Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="29144-135">Coleta: Olá publicação modo original.</span><span class="sxs-lookup"><span data-stu-id="29144-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="29144-136">Todos os usuários veem todos os aplicativos publicados.</span><span class="sxs-lookup"><span data-stu-id="29144-136">All users see all published apps.</span></span>
* <span data-ttu-id="29144-137">Aplicativo: Olá nova publicação modo.</span><span class="sxs-lookup"><span data-stu-id="29144-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="29144-138">Os usuários veem somente Olá aplicativos publicados diretamente toothem.</span><span class="sxs-lookup"><span data-stu-id="29144-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="29144-139">Como o modo de publicação de tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="29144-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="29144-140">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="29144-141">Estado de publicação de aplicativo será preservado: inicialmente todos os usuários verão todos os aplicativos publicados original de saudação.</span><span class="sxs-lookup"><span data-stu-id="29144-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="29144-142">Como os usuários toolist quem podem ver um aplicativo específico</span><span class="sxs-lookup"><span data-stu-id="29144-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="29144-143">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="29144-144">Lista todos os usuários que podem ver o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="29144-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="29144-145">Observação: Você pode ver aliases de aplicativo hello (chamados "alias do aplicativo" na sintaxe de saudação acima) executando Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="29144-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="29144-146">Como tooassign um usuário do aplicativo tooa</span><span class="sxs-lookup"><span data-stu-id="29144-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="29144-147">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="29144-148">usuário Hello agora verá saudação do aplicativo no cliente do Azure RemoteApp hello e será capaz de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="29144-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="29144-149">Como tooremove um aplicativo de um usuário</span><span class="sxs-lookup"><span data-stu-id="29144-149">How tooremove an application from a user</span></span>
<span data-ttu-id="29144-150">Execute Olá cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="29144-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="29144-151">Como fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="29144-151">Providing feedback</span></span>
<span data-ttu-id="29144-152">Agradecemos seus comentários e sugestões sobre este recurso de visualização.</span><span class="sxs-lookup"><span data-stu-id="29144-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="29144-153">Por favor, preencha Olá [pesquisa](http://www.instant.ly/s/FDdrb) toolet no que você acha.</span><span class="sxs-lookup"><span data-stu-id="29144-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="29144-154">Ainda não teve um recurso de visualização chance tootry Olá?</span><span class="sxs-lookup"><span data-stu-id="29144-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="29144-155">Se você não participou de visualização Olá ainda, use isso [pesquisa](http://www.instant.ly/s/AY83p) toorequest acesso.</span><span class="sxs-lookup"><span data-stu-id="29144-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

