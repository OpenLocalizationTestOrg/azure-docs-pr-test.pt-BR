---
title: 'Azure Active Directory Domain Services: criar ou selecionar uma rede virtual | Microsoft Docs'
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Criar ou selecionar uma rede virtual para o Azure Active Directory Domain Services
## <a name="before-you-begin"></a>Antes de começar
Consulte também[considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Tarefa 2: criar uma rede virtual do Azure
a próxima tarefa de configuração Olá é toocreate uma rede virtual do Azure e uma sub-rede dentro dele. Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual. Se você tiver uma rede virtual existente que você prefere toouse, você pode ignorar esta etapa.

> [!NOTE]
> Certifique-se de que Olá rede virtual do Azure crie ou escolha toouse com o Azure Active Directory Domain Services pertence tooan região do Azure que é compatível com o Azure Active Directory Domain Services. tooascertain Olá regiões do Azure em que o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).
>
>Anote o nome de saudação do hello tooensure de rede virtual que você selecione a rede virtual à direita hello quando você habilitar o Azure Active Directory Domain Services em uma etapa de configuração subsequentes.


toocreate uma rede virtual do Azure no qual você deseja tooenable do Azure Active Directory Domain Services, siga estas instruções de configuração:

1. Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo do hello, selecione **redes**.

    ![Nó de redes](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Olá **redes virtuais** janela será aberta.
3. No painel de tarefas de saudação na parte inferior da saudação da janela hello, clique em **novo**.

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Clique em **Serviços de Rede**e selecione **Rede Virtual**.

    ![Rede virtual - criação rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. toocreate uma rede virtual, clique em **criação rápida**.

6. Especifique um **nome** para sua máquina virtual, rede e considere o seguinte hello:
    * Você pode escolher tooconfigure **espaço de endereço** ou **contagem máxima de VMs** para essa rede.
    * Você pode deixar Olá **servidor DNS** definindo como **nenhum** por enquanto. Você pode atualizar a configuração de saudação depois de habilitar o Azure Active Directory Domain Services.
7. Em Olá **local** lista suspensa, selecione uma região do Azure com suporte.  
    tooascertain Olá regiões do Azure em que o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).
8. toocreate sua rede virtual, clique em **criar uma rede Virtual**.

    ![Criar uma rede virtual para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Depois de criar uma rede virtual, selecione Olá nome de rede virtual Olá e clique em Olá **configurar** guia.

    ![Criar uma sub-rede](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. Em **espaços de endereço de rede virtual**, clique em **Adicionar sub-rede**e, em seguida, especifique uma sub-rede com nome hello **AaddsSubnet**.

    ![Criar uma sub-rede para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate Olá sub-rede, clique em **salvar**.


## <a name="next-step"></a>Próxima etapa
[Tarefa 3: habilitar o Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
