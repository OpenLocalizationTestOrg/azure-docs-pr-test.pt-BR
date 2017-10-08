---
title: "limitações do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
description: "Visão geral das limitações do Azure Cloud Shell"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="6d069-103">Limitações do Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="6d069-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="6d069-104">Shell de nuvem do Azure tem a seguinte Olá limitações conhecidas:</span><span class="sxs-lookup"><span data-stu-id="6d069-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="6d069-105">Estado do sistema e persistência</span><span class="sxs-lookup"><span data-stu-id="6d069-105">System state and persistence</span></span>
<span data-ttu-id="6d069-106">máquina de saudação que fornece sua sessão do Shell de nuvem é temporária e é reciclado depois que a sessão está inativa por 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="6d069-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="6d069-107">Shell de nuvem requer um toobe de compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="6d069-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="6d069-108">Como resultado, sua assinatura deve ser capaz de tooset backup tooaccess de recursos de armazenamento Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6d069-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="6d069-109">Outras considerações incluem:</span><span class="sxs-lookup"><span data-stu-id="6d069-109">Other considerations include:</span></span>
* <span data-ttu-id="6d069-110">Com o armazenamento montado, apenas as modificações em seu diretório `$Home` ou `clouddrive` são persistidas.</span><span class="sxs-lookup"><span data-stu-id="6d069-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="6d069-111">Os compartilhamentos de arquivo só podem ser montados em sua [região atribuída](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="6d069-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="6d069-112">Os Arquivos do Azure oferece suporte apenas a armazenamento com redundância local e a contas de armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="6d069-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="6d069-113">Permissões de usuário</span><span class="sxs-lookup"><span data-stu-id="6d069-113">User permissions</span></span>
<span data-ttu-id="6d069-114">As permissões são definidas como usuários regulares sem acesso sudo.</span><span class="sxs-lookup"><span data-stu-id="6d069-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="6d069-115">Qualquer instalação fora do seu diretório `$Home` não será persistida.</span><span class="sxs-lookup"><span data-stu-id="6d069-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="6d069-116">Embora determinados comandos dentro Olá `clouddrive` diretório, como `git clone`, não tem permissões adequadas, seu `$Home` diretório tem permissões.</span><span class="sxs-lookup"><span data-stu-id="6d069-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="6d069-117">Suporte ao navegador</span><span class="sxs-lookup"><span data-stu-id="6d069-117">Browser support</span></span>
<span data-ttu-id="6d069-118">Shell de nuvem oferece suporte a versões mais recentes de saudação do Microsoft Internet Explorer, Microsoft Edge, Google Chrome, Mozilla Firefox e Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="6d069-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="6d069-119">Não há suporte para o Safari no modo particular.</span><span class="sxs-lookup"><span data-stu-id="6d069-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="6d069-120">Copiar e colar</span><span class="sxs-lookup"><span data-stu-id="6d069-120">Copy and paste</span></span>
<span data-ttu-id="6d069-121">CTRL + C e Ctrl + V não funcionar como copiar/colar atalhos no Shell de nuvem em máquinas do Windows, use Ctrl + Insert e Shift + Insert toocopy e cole respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6d069-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="6d069-122">Com o botão direito copiar e colar opções também estão disponíveis, mas função de atalho é acesso de área de transferência toobrowser específicas de assunto.</span><span class="sxs-lookup"><span data-stu-id="6d069-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="6d069-123">Edição de .bashrc</span><span class="sxs-lookup"><span data-stu-id="6d069-123">Editing .bashrc</span></span>
<span data-ttu-id="6d069-124">Tome cuidado ao editar .bashrc, uma vez que isso pode causar erros inesperados no Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6d069-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="6d069-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="6d069-125">.bash_history</span></span>
<span data-ttu-id="6d069-126">Seu histórico de comandos bash pode ser inconsistente devido a interrupções de sessão a ou sessões simultâneas do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6d069-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="6d069-127">Limites de uso</span><span class="sxs-lookup"><span data-stu-id="6d069-127">Usage limits</span></span>
<span data-ttu-id="6d069-128">O Cloud Shell destina-se a casos de uso interativos.</span><span class="sxs-lookup"><span data-stu-id="6d069-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="6d069-129">Como resultado, quaisquer sessões não interativo e de longa execução são finalizadas sem aviso.</span><span class="sxs-lookup"><span data-stu-id="6d069-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="6d069-130">Conectividade de rede</span><span class="sxs-lookup"><span data-stu-id="6d069-130">Network connectivity</span></span>
<span data-ttu-id="6d069-131">Uma latência no Shell de nuvem é a conectividade com a internet toolocal assunto, Shell de nuvem continuará toocarry tooattempt as instruções enviadas.</span><span class="sxs-lookup"><span data-stu-id="6d069-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d069-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d069-132">Next steps</span></span>
[<span data-ttu-id="6d069-133">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="6d069-133">Cloud Shell Quickstart</span></span>](quickstart.md)
