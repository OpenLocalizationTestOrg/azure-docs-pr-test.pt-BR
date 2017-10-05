---
title: "Atualizar sua coleção do Azure RemoteApp | Microsoft Docs"
description: "Saiba como atualizar a coleção do RemoteApp do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="60422-103">Criar uma coleção de RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="60422-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="60422-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="60422-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="60422-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60422-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="60422-106">Pelo menos uma vez, inevitavelmente, você precisará atualizar os aplicativos ou a imagem em sua coleção de RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="60422-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="60422-107">Se você estiver usando uma das imagens incluídas com sua assinatura do Azure RemoteApp, na coleção de uma nuvem ou híbrida, quaisquer atualizações serão manipuladas pelo Azure RemoteApp, portanto você poderá descansar em paz.</span><span class="sxs-lookup"><span data-stu-id="60422-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="60422-108">No entanto, se você estiver usando uma imagem personalizada (que é criada do zero ou que você criou, modificando uma das nossas imagens), você é responsável pela manutenção da imagem e dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="60422-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="60422-109">Se você precisar atualizar sua imagem ou de qualquer aplicativo dentro dele, será necessário criar uma nova versão atualizada da imagem e então substituir a imagem existente em sua coleção pela nova imagem atualizada.</span><span class="sxs-lookup"><span data-stu-id="60422-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="60422-110">Então, como você para atualizar sua coleção?</span><span class="sxs-lookup"><span data-stu-id="60422-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="60422-111">É bem simples:</span><span class="sxs-lookup"><span data-stu-id="60422-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="60422-112">Atualize a imagem que você usou em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="60422-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="60422-113">Aplique os patches ou atualizações necessárias e salve-a com um novo nome.</span><span class="sxs-lookup"><span data-stu-id="60422-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="60422-114">[Carregue](remoteapp-uploadimage.md) ou [importe](remoteapp-image-on-azurevm.md) essa imagem no RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="60422-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="60422-115">Agora, na página de coleção, clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="60422-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="60422-116">Escolha a nova imagem a partir da lista **Imagem de modelo** .</span><span class="sxs-lookup"><span data-stu-id="60422-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="60422-117">Aqui está a parte complicada - você precisa decidir como lidar com quaisquer usuários que estão usando um aplicativo na coleção.</span><span class="sxs-lookup"><span data-stu-id="60422-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="60422-118">Você tem as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="60422-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="60422-119">**Dar aos usuários 60 minutos após a atualização**.</span><span class="sxs-lookup"><span data-stu-id="60422-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="60422-120">Assim que a atualização estiver concluída, o RemoteApp do Azure exibirá uma mensagem para qualquer usuário ativo informando-os para salvar seu trabalho e fazer logoff e logon novamente.</span><span class="sxs-lookup"><span data-stu-id="60422-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="60422-121">Após 60 minutos, quaisquer usuários ativos que não tiverem feito logoff serão automaticamente desconectados.</span><span class="sxs-lookup"><span data-stu-id="60422-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="60422-122">Os usuários podem fazer logon de novo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="60422-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="60422-123">**Desconectar os usuários imediatamente**.</span><span class="sxs-lookup"><span data-stu-id="60422-123">**Sign users out immediately**.</span></span> <span data-ttu-id="60422-124">Assim que a atualização estiver concluída, faça logoff de todos os usuários automaticamente sem qualquer aviso.</span><span class="sxs-lookup"><span data-stu-id="60422-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="60422-125">Se você escolher essa opção, os usuários poderão perder dados.</span><span class="sxs-lookup"><span data-stu-id="60422-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="60422-126">No entanto, eles podem se reconectar ao aplicativo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="60422-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="60422-127">Clique na marca de seleção para iniciar a atualização.</span><span class="sxs-lookup"><span data-stu-id="60422-127">Click the check mark to start the update.</span></span>

