---
title: "Como solucionar problemas comuns durante a criação do VHD | Microsoft Docs"
description: "Respostas a perguntas comuns de solução de problemas e problemas durante a criação do VHD."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="417d1-103">Como solucionar problemas comuns encontrados durante a criação do VHD</span><span class="sxs-lookup"><span data-stu-id="417d1-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="417d1-104">Este artigo é fornecido para ajudar um fornecedor e/ou coadministrador do Azure Marketplace que possa enfrentar um problema ou ter dúvidas comuns ao publicar ou gerenciar suas soluções de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="417d1-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="417d1-105">Como posso alterar o nome do host?</span><span class="sxs-lookup"><span data-stu-id="417d1-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="417d1-106">Após a criação da VM, os usuários não poderão atualizar o nome do host.</span><span class="sxs-lookup"><span data-stu-id="417d1-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="417d1-107">Como redefinir o serviço de Área de Trabalho Remota ou sua senha de logon?</span><span class="sxs-lookup"><span data-stu-id="417d1-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="417d1-108">Referência de VM do Windows</span><span class="sxs-lookup"><span data-stu-id="417d1-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="417d1-109">Referência de VM do Linux</span><span class="sxs-lookup"><span data-stu-id="417d1-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="417d1-110">Como posso gerar novos certificados ssh?</span><span class="sxs-lookup"><span data-stu-id="417d1-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="417d1-111">Consulte o link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="417d1-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="417d1-112">Como configurar um certificado VPN aberta?</span><span class="sxs-lookup"><span data-stu-id="417d1-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="417d1-113">Consulte o link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="417d1-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="417d1-114">Qual é a política de suporte para a execução de software de servidor da Microsoft no ambiente de máquina virtual do Microsoft Azure (uma infraestrutura como serviço)?</span><span class="sxs-lookup"><span data-stu-id="417d1-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="417d1-115">Consulte o link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="417d1-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="417d1-116">As máquinas virtuais têm algum identificador exclusivo?</span><span class="sxs-lookup"><span data-stu-id="417d1-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="417d1-117">O Azure codifica a ID exclusiva da VM do Azure em cada VM.</span><span class="sxs-lookup"><span data-stu-id="417d1-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="417d1-118">Consulte detalhes neste blog e na documentação.</span><span class="sxs-lookup"><span data-stu-id="417d1-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="417d1-119">Em uma VM, como posso gerenciar a extensão de script personalizado na tarefa de inicialização?</span><span class="sxs-lookup"><span data-stu-id="417d1-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="417d1-120">Consulte o link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="417d1-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="417d1-121">Como criar uma VM no Portal do Azure usando o VHD carregado no armazenamento premium?</span><span class="sxs-lookup"><span data-stu-id="417d1-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="417d1-122">Ainda não oferecemos suporte a essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="417d1-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="417d1-123">Um aplicativo de 32 bits tem suporte no Azure Marketplace?</span><span class="sxs-lookup"><span data-stu-id="417d1-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="417d1-124">Consulte o link para obter detalhes sobre a política de suporte: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="417d1-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="417d1-125">Sempre que estou tentando criar uma imagem de minhas VHDs, recebo o erro "O .VHD já está registrado no repositório de imagens como o recurso"no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="417d1-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="417d1-126">Eu não criei qualquer imagem antes, nem encontrei qualquer imagem com esse nome no Azure.</span><span class="sxs-lookup"><span data-stu-id="417d1-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="417d1-127">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="417d1-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="417d1-128">Geralmente, isso acontece se o usuário provisionou uma VM a partir desse VHD e houver um bloqueio nesse VHD.</span><span class="sxs-lookup"><span data-stu-id="417d1-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="417d1-129">Verifique se não há uma VM alocada a partir desse VHD.</span><span class="sxs-lookup"><span data-stu-id="417d1-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="417d1-130">Se o erro persistir, gere um tíquete de suporte usando este link ou no portal de publicação (encontre os detalhes na resposta da pergunta 11).</span><span class="sxs-lookup"><span data-stu-id="417d1-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>