---
title: "Usar a janela do Azure Cloud Shell (visualização) | Microsoft Docs"
description: "Orientações sobre a janela do Azure Cloud Shell."
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
ms.openlocfilehash: a47961dfdaf178a6b793bd68105d9792a9275bb3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-azure-cloud-shell-window"></a><span data-ttu-id="a81d2-103">Usando a janela do Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a81d2-103">Using the Azure Cloud Shell window</span></span>

<span data-ttu-id="a81d2-104">Este documento explica como usar a janela do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a81d2-104">This document explains how to use the Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="a81d2-105">Sessões simultâneas</span><span class="sxs-lookup"><span data-stu-id="a81d2-105">Concurrent sessions</span></span>
<span data-ttu-id="a81d2-106">O Cloud Shell permite várias sessões simultâneas em guias do navegador permitindo que cada sessão exista como um processo do Bash separado.</span><span class="sxs-lookup"><span data-stu-id="a81d2-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.</span></span>
<span data-ttu-id="a81d2-107">Ao sair de uma sessão, saia de cada janela de sessão, pois cada processo é executado de forma independente apesar de serem executados no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="a81d2-107">If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="a81d2-108">Reiniciar o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a81d2-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="a81d2-109">Reiniciar o Cloud Shell redefinirá o estado do computador e quaisquer arquivos não persistidos pelo seu compartilhamento de arquivos serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="a81d2-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="a81d2-110">Clique no ícone de reinicialização na barra de ferramentas para receber um novo ambiente do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a81d2-110">Click the restart icon on the toolbar to receive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="a81d2-111">Minimizar e maximizar a janela do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a81d2-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="a81d2-112">Clique no ícone de minimizar no canto superior direito da janela para ocultá-lo.</span><span class="sxs-lookup"><span data-stu-id="a81d2-112">Click the minimize icon on the top right of the window to hide it.</span></span> <span data-ttu-id="a81d2-113">Clique novamente no ícone do Cloud Shell para reexibir.</span><span class="sxs-lookup"><span data-stu-id="a81d2-113">Click the Cloud Shell icon again to unhide.</span></span>
* <span data-ttu-id="a81d2-114">Clique no ícone de maximizar para definir a janela com a altura máxima.</span><span class="sxs-lookup"><span data-stu-id="a81d2-114">Click the maximize icon to set window to max height.</span></span> <span data-ttu-id="a81d2-115">Para restaurar a janela ao tamanho anterior, clique em Restaurar.</span><span class="sxs-lookup"><span data-stu-id="a81d2-115">To restore window to previous size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="a81d2-116">Copiar e colar</span><span class="sxs-lookup"><span data-stu-id="a81d2-116">Copy and paste</span></span>
* <span data-ttu-id="a81d2-117">Windows: `Ctrl-insert` para copiar e `Shift-insert` para colar.</span><span class="sxs-lookup"><span data-stu-id="a81d2-117">Windows: `Ctrl-insert` to copy and `Shift-insert` to paste.</span></span> <span data-ttu-id="a81d2-118">A lista suspensa aberta com um clique com o botão direito do mouse também pode habilitar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="a81d2-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="a81d2-119">Talvez o FireFox/IE não dê suporte apropriado a permissões de área de transferência.</span><span class="sxs-lookup"><span data-stu-id="a81d2-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="a81d2-120">Mac OS: `Cmd-c` para copiar e `Cmd-v` para colar.</span><span class="sxs-lookup"><span data-stu-id="a81d2-120">Mac OS: `Cmd-c` to copy and `Cmd-v` to paste.</span></span> <span data-ttu-id="a81d2-121">A lista suspensa aberta com um clique com o botão direito do mouse também pode habilitar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="a81d2-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="a81d2-122">Redimensionar a janela do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a81d2-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="a81d2-123">Clique e arraste a borda superior da barra de ferramentas para cima ou para baixo para redimensionar a janela do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a81d2-123">Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="a81d2-124">Rolagem pela exibição de texto</span><span class="sxs-lookup"><span data-stu-id="a81d2-124">Scrolling text display</span></span>
* <span data-ttu-id="a81d2-125">Role com o mouse ou teclado para ir ao texto de terminal.</span><span class="sxs-lookup"><span data-stu-id="a81d2-125">Scroll with your mouse or touchpad to move terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="a81d2-126">Comando de saída</span><span class="sxs-lookup"><span data-stu-id="a81d2-126">Exit command</span></span>
<span data-ttu-id="a81d2-127">Executar `exit` encerra a sessão ativa.</span><span class="sxs-lookup"><span data-stu-id="a81d2-127">Running `exit` terminates the active session.</span></span> <span data-ttu-id="a81d2-128">Esse comportamento ocorre por padrão após 20 minutos sem interação.</span><span class="sxs-lookup"><span data-stu-id="a81d2-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a81d2-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a81d2-129">Next steps</span></span>
[<span data-ttu-id="a81d2-130">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a81d2-130">Cloud Shell Quickstart</span></span>](quickstart.md)
