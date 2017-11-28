---
title: Publicar um aplicativo no RemoteApp do Azure | Microsoft Docs
description: Saiba como publicar aplicativos e recursos no RemoteApp do Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="1eddb-103">Como publicar um aplicativo no RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1eddb-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1eddb-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="1eddb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1eddb-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="1eddb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1eddb-106">Depois de criar sua coleção RemoteApp, você precisa publicar os aplicativos ou recursos que você deseja disponibilizar para os usuários.</span><span class="sxs-lookup"><span data-stu-id="1eddb-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="1eddb-107">As imagens de modelo fornecidas com sua assinatura tem apenas alguns aplicativos publicados por padrão – para compartilhar os outros aplicativos, é necessário publicá-los.</span><span class="sxs-lookup"><span data-stu-id="1eddb-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="1eddb-108">Você precisa atualizar um aplicativo?</span><span class="sxs-lookup"><span data-stu-id="1eddb-108">Do you need to update an app?</span></span> <span data-ttu-id="1eddb-109">Você precisará [atualizar a imagem](remoteapp-update.md) primeiro.</span><span class="sxs-lookup"><span data-stu-id="1eddb-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="1eddb-110">Na guia **Publicação** no portal, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="1eddb-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="1eddb-111">Você pode adicionar um aplicativo da imagem do modelo do menu **Iniciar** ou fornecer o caminho onde o aplicativo está instalado na imagem do modelo.</span><span class="sxs-lookup"><span data-stu-id="1eddb-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="1eddb-112">Se você optar por adicionar do menu **Iniciar** , escolha na lista o aplicativo para publicação.</span><span class="sxs-lookup"><span data-stu-id="1eddb-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="1eddb-113">Se você optar por fornecer o caminho para o aplicativo, digite um nome para o aplicativo e o caminho para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1eddb-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="1eddb-114">Use variáveis no caminho - por exemplo, "%systemdrive%" em vez de "c:\"".</span><span class="sxs-lookup"><span data-stu-id="1eddb-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="1eddb-115">Se quiser adicionar seu aplicativo do menu **Iniciar**, precisará ter *adicionado esse aplicativo ao menu **Iniciar** em sua imagem de modelo.*</span><span class="sxs-lookup"><span data-stu-id="1eddb-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="1eddb-116">Caso contrário, o RemoteApp verá somente o que *está* no menu **Iniciar** e você ficará confuso.</span><span class="sxs-lookup"><span data-stu-id="1eddb-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="1eddb-117">Para ter certeza de que seu aplicativo está no menu **Iniciar**, coloque um arquivo de atalho - **.lnk** - dentro da pasta %systemdrive%\ProgramData\Microsoft\Windows\Menu Iniciar\Programas.</span><span class="sxs-lookup"><span data-stu-id="1eddb-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="1eddb-118">Se você se esqueceu de adicionar o aplicativo ao menu **Iniciar** quando criou o modelo, opte por adicionar o caminho ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1eddb-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="1eddb-119">(Ou recrie a imagem do seu modelo, mas é muito mais trabalhoso.)</span><span class="sxs-lookup"><span data-stu-id="1eddb-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

