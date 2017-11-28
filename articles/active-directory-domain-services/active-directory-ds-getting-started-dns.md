---
title: "Serviços do Azure Active Directory domínio: Atualizar as configurações de DNS para Olá rede virtual do Azure | Microsoft Docs"
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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a><span data-ttu-id="1d391-103">Habilitar o Azure Active Directory Domain Services (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="1d391-103">Enable Azure Active Directory Domain Services (Preview)</span></span>

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="1d391-104">Tarefa 4: atualizar as configurações de DNS para Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="1d391-104">Task 4: update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="1d391-105">Olá anterior tarefas de configuração, você habilitou com êxito do Azure Active Directory Domain Services para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="1d391-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="1d391-106">Olá próxima tarefa é tooensure que os computadores na rede virtual Olá podem se conectar e consumir esses serviços.</span><span class="sxs-lookup"><span data-stu-id="1d391-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="1d391-107">Neste artigo, você pode atualizar configurações do servidor DNS Olá para sua rede virtual toopoint toohello dois endereços IP onde o Azure Active Directory Domain Services está disponível na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1d391-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

<span data-ttu-id="1d391-108">configuração de servidor tooupdate Olá DNS para a rede virtual hello, no qual você habilitou os serviços de domínio Active Directory do Azure, a saudação concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d391-108">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="1d391-109">Olá **visão geral** guia lista um conjunto de **necessárias etapas de configuração** toobe executada depois que o domínio gerenciado está totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="1d391-109">hello **Overview** tab lists a set of **Required configuration steps** toobe performed after your managed domain is fully provisioned.</span></span> <span data-ttu-id="1d391-110">Olá a primeira etapa de configuração é **configurações do servidor de atualização de DNS para sua rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="1d391-110">hello first configuration step is **Update DNS server settings for your virtual network**.</span></span>

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned-overview.png)

2. <span data-ttu-id="1d391-112">Quando o seu domínio está totalmente provisionado, dois endereços IP são exibidos neste bloco.</span><span class="sxs-lookup"><span data-stu-id="1d391-112">When your domain is fully provisioned, two IP addresses are displayed in this tile.</span></span> <span data-ttu-id="1d391-113">Cada um do endereços IP representa um controlador de domínio para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="1d391-113">Each of these IP addresses represents a domain controller for your managed domain.</span></span>

3. <span data-ttu-id="1d391-114">Olá toocopy primeiro IP endereço tooclipboard, clique em Olá cópia botão Avançar tooit.</span><span class="sxs-lookup"><span data-stu-id="1d391-114">toocopy hello first IP address tooclipboard, click hello copy button next tooit.</span></span> <span data-ttu-id="1d391-115">Em seguida, clique em Olá **servidores DNS configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="1d391-115">Then click hello **Configure DNS servers** button.</span></span>

4. <span data-ttu-id="1d391-116">Cole o endereço IP primeiro Olá a Olá **servidor DNS adicionar** textbox em Olá **servidores DNS** folha.</span><span class="sxs-lookup"><span data-stu-id="1d391-116">Paste hello first IP address into hello **Add DNS server** textbox in hello **DNS servers** blade.</span></span> <span data-ttu-id="1d391-117">Rolar horizontalmente toohello deixado toocopy Olá segundo endereço IP e cole-o em Olá **servidor DNS adicionar** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1d391-117">Scroll horizontally toohello left toocopy hello second IP address and paste it into hello **Add DNS server** textbox.</span></span>

    ![Domain Services- atualizar o DNS](./media/getting-started/domain-services-update-dns.png)

5. <span data-ttu-id="1d391-119">Clique em **salvar** quando você terminar de servidores DNS tooupdate Olá para rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1d391-119">Click **Save** when you are done tooupdate hello DNS servers for hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="1d391-120">Máquinas virtuais na rede Olá obter somente as novas configurações de DNS Olá após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="1d391-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="1d391-121">Se você precisar deles configurações de DNS tooget Olá atualizada imediatamente, disparar uma reinicialização do portal hello, PowerShell ou Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="1d391-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="1d391-122">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="1d391-122">Next step</span></span>
[<span data-ttu-id="1d391-123">Tarefa 5: habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d391-123">Task 5: enable password synchronization tooAzure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-password-sync.md)
