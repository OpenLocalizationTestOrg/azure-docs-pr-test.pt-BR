---
title: "aaaUpdate sua coleção do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como tooupdate sua coleção do RemoteApp"
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="19f5f-103">Criar uma coleção de RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="19f5f-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="19f5f-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="19f5f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="19f5f-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="19f5f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="19f5f-106">Virão um tempo, inevitavelmente, quando você precisar tooupdate Olá aplicativos ou imagem em sua coleção do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="19f5f-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="19f5f-107">Se você estiver usando uma das imagens de saudação incluídas com a sua assinatura do Azure RemoteApp na coleção de uma nuvem ou híbrida, todas as atualizações são manipuladas pelo Azure RemoteApp em si, para que você possa ter fácil.</span><span class="sxs-lookup"><span data-stu-id="19f5f-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="19f5f-108">No entanto, se você estiver usando uma imagem personalizada (que é criado do zero ou que você criou, modificando uma das nossas imagens), será responsável pela manutenção de aplicativos e a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="19f5f-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="19f5f-109">Se você precisar tooupdate sua imagem ou qualquer um dos aplicativos hello dentro dele, será necessário toocreate uma nova versão da imagem de Olá e, em seguida, substituir Olá existente imagem atualizada em sua coleção com a nova imagem atualizada.</span><span class="sxs-lookup"><span data-stu-id="19f5f-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="19f5f-110">Então, como você para atualizar sua coleção?</span><span class="sxs-lookup"><span data-stu-id="19f5f-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="19f5f-111">É bem simples:</span><span class="sxs-lookup"><span data-stu-id="19f5f-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="19f5f-112">Atualize imagem Olá usado na sua coleção.</span><span class="sxs-lookup"><span data-stu-id="19f5f-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="19f5f-113">Aplique os patches ou atualizações necessárias e salve-a com um novo nome.</span><span class="sxs-lookup"><span data-stu-id="19f5f-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="19f5f-114">[Carregar](remoteapp-uploadimage.md) ou [importar](remoteapp-image-on-azurevm.md) tooRemoteApp essa imagem.</span><span class="sxs-lookup"><span data-stu-id="19f5f-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="19f5f-115">Agora, na página de coleção de saudação, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="19f5f-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="19f5f-116">Escolher imagem nova Olá Olá **imagem de modelo** lista.</span><span class="sxs-lookup"><span data-stu-id="19f5f-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="19f5f-117">Esta é uma parte complicada Olá - precisar toodecide como toodeal com todos os usuários que estão usando um aplicativo na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="19f5f-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="19f5f-118">Você tem Olá opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="19f5f-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="19f5f-119">**Fornecer aos usuários 60 minutos após a atualização de saudação**.</span><span class="sxs-lookup"><span data-stu-id="19f5f-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="19f5f-120">Assim que Olá atualização estiver concluída, Azure RemoteApp exibirá uma mensagem tooany ativa os usuários informando toosave seus trabalhos e log off e faça logon.</span><span class="sxs-lookup"><span data-stu-id="19f5f-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="19f5f-121">Após 60 minutos, quaisquer usuários ativos que não tiverem feito logoff serão automaticamente desconectados.</span><span class="sxs-lookup"><span data-stu-id="19f5f-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="19f5f-122">Os usuários podem fazer logon de novo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="19f5f-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="19f5f-123">**Desconectar os usuários imediatamente**.</span><span class="sxs-lookup"><span data-stu-id="19f5f-123">**Sign users out immediately**.</span></span> <span data-ttu-id="19f5f-124">Como Olá atualização estiver concluída, fazer logoff de todos os usuários automaticamente sem aviso.</span><span class="sxs-lookup"><span data-stu-id="19f5f-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="19f5f-125">Se você escolher essa opção, os usuários poderão perder dados.</span><span class="sxs-lookup"><span data-stu-id="19f5f-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="19f5f-126">No entanto, eles poderão se reconectar toohello aplicativo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="19f5f-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="19f5f-127">Clique em atualizar de Olá Olá marca de seleção toostart.</span><span class="sxs-lookup"><span data-stu-id="19f5f-127">Click hello check mark toostart hello update.</span></span>

