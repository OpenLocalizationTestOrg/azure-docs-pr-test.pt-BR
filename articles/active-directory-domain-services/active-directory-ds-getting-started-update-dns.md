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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="5627b-103">Atualizar configurações de DNS para Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5627b-103">Update DNS settings for hello Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a><span data-ttu-id="5627b-104">Tarefa 4: Atualizar as configurações de DNS para Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5627b-104">Task 4: Update DNS settings for hello Azure virtual network</span></span>
<span data-ttu-id="5627b-105">Olá anterior tarefas de configuração, você habilitou com êxito do Azure Active Directory Domain Services para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="5627b-105">In hello preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="5627b-106">Olá próxima tarefa é tooensure que os computadores na rede virtual Olá podem se conectar e consumir esses serviços.</span><span class="sxs-lookup"><span data-stu-id="5627b-106">hello next task is tooensure that computers within hello virtual network can connect and consume these services.</span></span> <span data-ttu-id="5627b-107">Neste artigo, você pode atualizar configurações do servidor DNS Olá para sua rede virtual toopoint toohello dois endereços IP onde o Azure Active Directory Domain Services está disponível na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="5627b-107">In this article, you update hello DNS server settings for your virtual network toopoint toohello two IP addresses where Azure Active Directory Domain Services is available on hello virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="5627b-108">Depois de habilitar o Azure Active Directory Domain Services para o diretório de hello, observe endereços IP Olá para o Azure Active Directory Domain Services que são exibidos em Olá **configurar** guia de seu diretório.</span><span class="sxs-lookup"><span data-stu-id="5627b-108">After you've enabled Azure Active Directory Domain Services for hello directory, note hello IP addresses for Azure Active Directory Domain Services that are displayed on hello **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="5627b-109">configuração de servidor tooupdate Olá DNS para a rede virtual hello, no qual você habilitou os serviços de domínio Active Directory do Azure, a saudação concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5627b-109">tooupdate hello DNS server setting for hello virtual network in which you have enabled Azure Active Directory Domain Services, complete hello following steps:</span></span>

1. <span data-ttu-id="5627b-110">Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5627b-110">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5627b-111">No painel esquerdo do hello, selecione **redes**.</span><span class="sxs-lookup"><span data-stu-id="5627b-111">In hello left pane, select **Networks**.</span></span>  
    <span data-ttu-id="5627b-112">Olá **redes** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="5627b-112">hello **Networks** window opens.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="5627b-114">Em Olá **redes virtuais** guia, no qual você habilitou Azure Active Directory Domain Services tooview suas propriedades de rede virtual do hello select.</span><span class="sxs-lookup"><span data-stu-id="5627b-114">On hello **Virtual Networks** tab, select hello virtual network in which you enabled Azure Active Directory Domain Services tooview its properties.</span></span>
4. <span data-ttu-id="5627b-115">Clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="5627b-115">Click hello **Configure** tab.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="5627b-117">Em Olá **servidores DNS** seção, digite os endereços IP de saudação eram exibidos no hello **dos serviços de domínio** seção Olá **configurar** guia de seu diretório.</span><span class="sxs-lookup"><span data-stu-id="5627b-117">In hello **DNS servers** section, enter both of hello IP addresses that were displayed in hello **Domain Services** section on hello **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="5627b-118">Clique em configurações do servidor DNS toosave Olá para essa rede virtual, no painel de tarefas de saudação na parte inferior da saudação da janela de saudação **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5627b-118">toosave hello DNS server settings for this virtual network, in hello task pane at hello bottom of hello window, click **Save**.</span></span>

   ![Atualizar configurações do servidor DNS Olá para rede virtual Olá](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="5627b-120">Máquinas virtuais na rede Olá obter somente as novas configurações de DNS Olá após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="5627b-120">Virtual machines in hello network only get hello new DNS settings after a restart.</span></span> <span data-ttu-id="5627b-121">Se você precisar deles configurações de DNS tooget Olá atualizada imediatamente, disparar uma reinicialização do portal hello, PowerShell ou Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="5627b-121">If you need them tooget hello updated DNS settings right away, trigger a restart either by hello portal, PowerShell, or hello CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5627b-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5627b-122">Next steps</span></span>
<span data-ttu-id="5627b-123">Tarefa 5: [habilitar sincronização de senha tooAzure serviços de domínio do Active Directory](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="5627b-123">Task 5: [Enable password synchronization tooAzure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
