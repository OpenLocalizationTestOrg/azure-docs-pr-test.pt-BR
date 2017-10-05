---
title: "Azure Active Directory Domain Services: Atualizar as configurações do DNS para a rede virtual do Azure | Microsoft Docs"
description: "Introdução aos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="a6ba9-103">Habilitar o Azure Active Directory Domain Services (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="a6ba9-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="a6ba9-104">Tarefa 4: atualizar as configurações do DNS para a rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ba9-104">Task 4: update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="a6ba9-105">Nas tarefas de configuração anteriores, você habilitou o Azure Active Directory Domain Services para seu diretório com êxito.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="a6ba9-106">A próxima tarefa é garantir que os computadores na rede virtual possam se conectar e consumir esses serviços.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="a6ba9-107">Neste artigo, você atualiza as configurações do servidor DNS para sua rede virtual para apontar para os dois endereços IP em que o Azure Active Directory Domain Services fica disponível na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

<span data-ttu-id="a6ba9-108">Para atualizar uma configuração do servidor DNS para a rede virtual na qual você tiver habilitado o Azure Active Directory Domain Services, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a6ba9-108">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="a6ba9-109">A guia **Visão Geral** lista um conjunto de **etapas de configuração necessárias** que deverão ser executadas depois que o domínio gerenciado for totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-109">The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="a6ba9-110">A primeira etapa de configuração é **Atualizar configurações do servidor DNS para sua rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-110">The first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="a6ba9-112">Quando o seu domínio está totalmente provisionado, dois endereços IP são exibidos neste bloco.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="a6ba9-113">Cada um do endereços IP representa um controlador de domínio para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="a6ba9-114">Para copiar o primeiro endereço IP na área de transferência, clique no botão Copiar ao lado dele.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-114">To copy the first IP address to clipboard, click the copy button next to it.</span></span> <span data-ttu-id="a6ba9-115">Em seguida, clique no botão **Configurar servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-115">Then click the **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="a6ba9-116">Cole o primeiro endereço IP na caixa de texto **Adicionar servidor DNS** na folha **servidores DNS**.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-116">Paste the first IP address into the **Add DNS server** textbox in the **DNS servers** blade.</span></span> <span data-ttu-id="a6ba9-117">Role horizontalmente para a esquerda a fim de copiar o segundo endereço IP e cole-o na caixa de texto **Adicionar servidor DNS**.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-117">Scroll horizontally to the left to copy the second IP address and paste it into the **Add DNS server** textbox.</span></span>

    ![Domain Services- atualizar o DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="a6ba9-119">Clique em **Salvar** quando terminar de atualizar os servidores DNS para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-119">Click **Save** when you are done to update the DNS servers for the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="a6ba9-120">As máquinas virtuais na rede só recebem as novas configurações de DNS após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="a6ba9-121">Se você precisar deles para obter as configurações de DNS atualizadas imediatamente, dispare uma reinicialização do portal, do PowerShell ou da CLI.</span><span class="sxs-lookup"><span data-stu-id="a6ba9-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="a6ba9-122">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="a6ba9-122">Next step</span></span>
<span data-ttu-id="a6ba9-123">Tarefa 5: [habilitar a sincronização de senhas para o Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="a6ba9-123">[Task 5: enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
