---
title: "janela do Shell de nuvem do Azure (visualização) de saudação aaaUsing | Microsoft Docs"
description: "Janela do Shell de nuvem do Azure de Olá passo a passo."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="0e11c-103">Usando a janela do Shell de nuvem do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0e11c-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="0e11c-104">Este documento explica como toouse Olá janela do Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0e11c-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="0e11c-105">Sessões simultâneas</span><span class="sxs-lookup"><span data-stu-id="0e11c-105">Concurrent sessions</span></span>
<span data-ttu-id="0e11c-106">Shell de nuvem permite várias sessões simultâneas em guias do navegador, permitindo que cada tooexist de sessão como um processo separado do Bash.</span><span class="sxs-lookup"><span data-stu-id="0e11c-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="0e11c-107">Se sair de uma sessão, não se esqueça de tooexit de cada janela de sessão como cada processo é executado independentemente embora eles sejam executados em Olá mesma máquina.</span><span class="sxs-lookup"><span data-stu-id="0e11c-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="0e11c-108">Reiniciar o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0e11c-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="0e11c-109">Reiniciar o Cloud Shell redefinirá o estado do computador e quaisquer arquivos não persistidos pelo seu compartilhamento de arquivos serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="0e11c-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="0e11c-110">Clique ícone reinicialização Olá Olá barra de ferramentas tooreceive um novo ambiente de nuvem Shell.</span><span class="sxs-lookup"><span data-stu-id="0e11c-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="0e11c-111">Minimizar e maximizar a janela do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0e11c-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="0e11c-112">Clique em Olá minimizar ícone Olá parte superior direita da saudação janela toohide-lo.</span><span class="sxs-lookup"><span data-stu-id="0e11c-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="0e11c-113">Olá ícone nuvem Shell clique novamente em toounhide.</span><span class="sxs-lookup"><span data-stu-id="0e11c-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="0e11c-114">Clique em Olá maximizar a altura do ícone tooset janela toomax.</span><span class="sxs-lookup"><span data-stu-id="0e11c-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="0e11c-115">toorestore janela tooprevious tamanho, clique em Restaurar.</span><span class="sxs-lookup"><span data-stu-id="0e11c-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="0e11c-116">Copiar e colar</span><span class="sxs-lookup"><span data-stu-id="0e11c-116">Copy and paste</span></span>
* <span data-ttu-id="0e11c-117">Windows: `Ctrl-insert` toocopy e `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="0e11c-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="0e11c-118">A lista suspensa aberta com um clique com o botão direito do mouse também pode habilitar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="0e11c-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="0e11c-119">Talvez o FireFox/IE não dê suporte apropriado a permissões de área de transferência.</span><span class="sxs-lookup"><span data-stu-id="0e11c-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="0e11c-120">Mac OS: `Cmd-c` toocopy e `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="0e11c-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="0e11c-121">A lista suspensa aberta com um clique com o botão direito do mouse também pode habilitar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="0e11c-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="0e11c-122">Redimensionar a janela do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0e11c-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="0e11c-123">Clique e arraste a borda superior do hello da barra de ferramentas Olá para cima ou para baixo da janela do Shell de nuvem de saudação tooresize.</span><span class="sxs-lookup"><span data-stu-id="0e11c-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="0e11c-124">Rolagem pela exibição de texto</span><span class="sxs-lookup"><span data-stu-id="0e11c-124">Scrolling text display</span></span>
* <span data-ttu-id="0e11c-125">Rola com o texto de terminal toomove mouse ou teclado sensível ao toque.</span><span class="sxs-lookup"><span data-stu-id="0e11c-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="0e11c-126">Comando de saída</span><span class="sxs-lookup"><span data-stu-id="0e11c-126">Exit command</span></span>
<span data-ttu-id="0e11c-127">Executando `exit` encerra a sessão ativa hello.</span><span class="sxs-lookup"><span data-stu-id="0e11c-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="0e11c-128">Esse comportamento ocorre por padrão após 20 minutos sem interação.</span><span class="sxs-lookup"><span data-stu-id="0e11c-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e11c-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e11c-129">Next steps</span></span>
[<span data-ttu-id="0e11c-130">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0e11c-130">Cloud Shell Quickstart</span></span>](quickstart.md)
