---
title: "Limitações do Azure Cloud Shell (Visualização) | Microsoft Docs"
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
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="08210-103">Limitações do Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="08210-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="08210-104">O Azure Cloud Shell tem as seguintes limitações conhecidas:</span><span class="sxs-lookup"><span data-stu-id="08210-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="08210-105">Estado do sistema e persistência</span><span class="sxs-lookup"><span data-stu-id="08210-105">System state and persistence</span></span>
<span data-ttu-id="08210-106">O computador que fornece a sessão do Cloud Shell é temporário e é reciclado após a sessão ficar inativa por 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="08210-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="08210-107">O Cloud Shell exige a montagem de um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="08210-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="08210-108">Como resultado, sua assinatura deve ser capaz de configurar recursos de armazenamento para acessar o Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="08210-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="08210-109">Outras considerações incluem:</span><span class="sxs-lookup"><span data-stu-id="08210-109">Other considerations include:</span></span>
* <span data-ttu-id="08210-110">Com o armazenamento montado, apenas as modificações em seu diretório `$Home` ou `clouddrive` são persistidas.</span><span class="sxs-lookup"><span data-stu-id="08210-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="08210-111">Os compartilhamentos de arquivo só podem ser montados em sua [região atribuída](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="08210-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="08210-112">Os Arquivos do Azure oferece suporte apenas a armazenamento com redundância local e a contas de armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="08210-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="08210-113">Permissões de usuário</span><span class="sxs-lookup"><span data-stu-id="08210-113">User permissions</span></span>
<span data-ttu-id="08210-114">As permissões são definidas como usuários regulares sem acesso sudo.</span><span class="sxs-lookup"><span data-stu-id="08210-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="08210-115">Qualquer instalação fora do seu diretório `$Home` não será persistida.</span><span class="sxs-lookup"><span data-stu-id="08210-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="08210-116">Apesar de alguns comandos dentro do diretório `clouddrive`, como `git clone`, não terem as permissões adequadas, seu diretório `$Home` tem essas permissões.</span><span class="sxs-lookup"><span data-stu-id="08210-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="08210-117">Suporte ao navegador</span><span class="sxs-lookup"><span data-stu-id="08210-117">Browser support</span></span>
<span data-ttu-id="08210-118">O Cloud Shell oferece suporte às versões mais recentes do Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox e Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="08210-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="08210-119">Não há suporte para o Safari no modo particular.</span><span class="sxs-lookup"><span data-stu-id="08210-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="08210-120">Copiar e colar</span><span class="sxs-lookup"><span data-stu-id="08210-120">Copy and paste</span></span>
<span data-ttu-id="08210-121">Como Ctrl+C e Ctrl+V não funcionam como atalhos de copiar e colar no Cloud Shell em computadores Windows, use Ctrl+Insert e Shift+Insert para copiar e colar, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="08210-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="08210-122">As opções de copiar e colar com o botão direito também estão disponíveis, mas a função de clicar com o botão direito está sujeita ao acesso de área de transferência específico de um navegador.</span><span class="sxs-lookup"><span data-stu-id="08210-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="08210-123">Edição de .bashrc</span><span class="sxs-lookup"><span data-stu-id="08210-123">Editing .bashrc</span></span>
<span data-ttu-id="08210-124">Tome cuidado ao editar .bashrc, uma vez que isso pode causar erros inesperados no Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="08210-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="08210-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="08210-125">.bash_history</span></span>
<span data-ttu-id="08210-126">Seu histórico de comandos bash pode ser inconsistente devido a interrupções de sessão a ou sessões simultâneas do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="08210-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="08210-127">Limites de uso</span><span class="sxs-lookup"><span data-stu-id="08210-127">Usage limits</span></span>
<span data-ttu-id="08210-128">O Cloud Shell destina-se a casos de uso interativos.</span><span class="sxs-lookup"><span data-stu-id="08210-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="08210-129">Como resultado, quaisquer sessões não interativo e de longa execução são finalizadas sem aviso.</span><span class="sxs-lookup"><span data-stu-id="08210-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="08210-130">Conectividade de rede</span><span class="sxs-lookup"><span data-stu-id="08210-130">Network connectivity</span></span>
<span data-ttu-id="08210-131">Qualquer latência no Cloud Shell está sujeita à conectividade de internet local, o Cloud Shell continuará tentando realizar todas as instruções enviadas.</span><span class="sxs-lookup"><span data-stu-id="08210-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08210-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08210-132">Next steps</span></span>
[<span data-ttu-id="08210-133">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="08210-133">Cloud Shell Quickstart</span></span>](quickstart.md)
