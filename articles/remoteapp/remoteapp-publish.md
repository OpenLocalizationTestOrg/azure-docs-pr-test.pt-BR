---
title: aaaPublish um aplicativo no Azure RemoteApp | Microsoft Docs
description: Saiba como toopublish aplicativos e recursos no Azure RemoteApp.
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
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="3c490-103">Como toopublish um aplicativo no RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3c490-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3c490-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3c490-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3c490-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3c490-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3c490-106">Depois de criar sua coleção do RemoteApp, você precisará toopublish Olá aplicativos ou recursos que você deseja toomake disponível para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="3c490-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="3c490-107">Olá imagens de modelo fornecidas com sua assinatura tem apenas alguns aplicativos publicados por padrão, - tooshare Olá outros aplicativos, você precisa toopublish-los.</span><span class="sxs-lookup"><span data-stu-id="3c490-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="3c490-108">Você precisa de um aplicativo de tooupdate?</span><span class="sxs-lookup"><span data-stu-id="3c490-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="3c490-109">Você precisará de muito[atualização Olá imagem](remoteapp-update.md) primeiro.</span><span class="sxs-lookup"><span data-stu-id="3c490-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="3c490-110">Em Olá **publicação** no portal de saudação, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="3c490-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="3c490-111">Você pode adicionar um aplicativo de sua imagem de modelo **iniciar** menu ou forneça Olá caminho toowhere Olá aplicativo está instalado na imagem de modelo hello.</span><span class="sxs-lookup"><span data-stu-id="3c490-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="3c490-112">Se você escolher tooadd Olá **iniciar** menu, escolha Olá aplicativo toopublish Olá lista.</span><span class="sxs-lookup"><span data-stu-id="3c490-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="3c490-113">Se você escolher tooprovide Olá caminho toohello aplicativo, insira um nome para o aplicativo hello e Olá caminho toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c490-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="3c490-114">Usar variáveis no caminho Olá - por exemplo, "% systemdrive %" em vez de "c:\".</span><span class="sxs-lookup"><span data-stu-id="3c490-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="3c490-115">Se você quiser tooadd seu aplicativo de saudação **iniciar** menu, você precisa toohave *adicionado toohello esse aplicativo **iniciar** menu em sua imagem de modelo.*</span><span class="sxs-lookup"><span data-stu-id="3c490-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="3c490-116">Caso contrário, RemoteApp só verá o que *é* em Olá **iniciar** menu e você será confuso.</span><span class="sxs-lookup"><span data-stu-id="3c490-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="3c490-117">toomake-se de que seu aplicativo estiver em Olá **iniciar** menu, colocar um arquivo de atalho - **. lnk** - Olá %systemdrive%\ProgramData\Microsoft\Windows\Start Iniciar\Programas pasta.</span><span class="sxs-lookup"><span data-stu-id="3c490-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="3c490-118">Se você esqueceu tooadd Olá aplicativo toohello **iniciar** menu quando você criou o modelo de saudação, escolha tooadd Olá caminho toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c490-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="3c490-119">(Ou recrie a imagem do seu modelo, mas é muito mais trabalhoso.)</span><span class="sxs-lookup"><span data-stu-id="3c490-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

