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
ms.openlocfilehash: 8bee2a25f196d645b27f30f21305b1550e44e07a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3fbf6-103">Atualizar as configurações do DNS para a rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="3fbf6-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="3fbf6-104">Tarefa 4: atualizar as configurações do DNS para a rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="3fbf6-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="3fbf6-105">Nas tarefas de configuração anteriores, você habilitou o Azure Active Directory Domain Services para seu diretório com êxito.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="3fbf6-106">A próxima tarefa é garantir que os computadores na rede virtual possam se conectar e consumir esses serviços.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="3fbf6-107">Neste artigo, você atualiza as configurações do servidor DNS para sua rede virtual para apontar para os dois endereços IP em que o Azure Active Directory Domain Services fica disponível na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="3fbf6-108">Depois de habilitar o Azure Active Directory Domain Services para o diretório, observe os endereços IP para o Azure Active Directory Domain Services que são exibidos na guia **Configurar** de seu diretório.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="3fbf6-109">Para atualizar uma configuração do servidor DNS para a rede virtual na qual você tiver habilitado o Azure Active Directory Domain Services, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3fbf6-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:</span></span>

1. <span data-ttu-id="3fbf6-110">Vá para o [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3fbf6-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3fbf6-111">No painel esquerdo, selecione **Redes**.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="3fbf6-112">A janela **redes** é aberta.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-112">The **Networks** window opens.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="3fbf6-114">Na guia **Redes Virtuais** , selecione a rede virtual na qual você habilitou o Azure Active Directory Domain Services para exibir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="3fbf6-115">Clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="3fbf6-115">Click the **Configure** tab.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="3fbf6-117">Na seção **Servidores DNS**, insira os endereços IP que foram exibidos na seção **Serviços de Domínio** da guia **Configurar** do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="3fbf6-118">Para salvar as configurações do servidor DNS para essa rede virtual, clique em **Salvar** no painel de tarefas na parte inferior da janela.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Atualizar as configurações do servidor DNS para a rede virtual](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  <span data-ttu-id="3fbf6-120">As máquinas virtuais na rede só recebem as novas configurações de DNS após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-120">Virtual machines in the network only get the new DNS settings after a restart.</span></span> <span data-ttu-id="3fbf6-121">Se você precisar deles para obter as configurações de DNS atualizadas imediatamente, dispare uma reinicialização do portal, do PowerShell ou da CLI.</span><span class="sxs-lookup"><span data-stu-id="3fbf6-121">If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3fbf6-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3fbf6-122">Next steps</span></span>
<span data-ttu-id="3fbf6-123">Tarefa 5: [habilitar a sincronização de senhas para o Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="3fbf6-123">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>
