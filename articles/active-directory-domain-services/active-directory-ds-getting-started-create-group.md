---
title: "Serviços do Azure Active Directory domínio: Criar o grupo de administradores do controlador de domínio de saudação do AD do Azure | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure
Este artigo descreve e orienta durante as tarefas de configuração de saudação que são necessárias para você tooenable do Azure Active Directory serviços de domínio (Azure AD DS) para seu locatário do Azure Active Directory (AD do Azure).

> [!NOTE]
> [**Tente a nova experiência do portal (visualização) do Azure Olá em vez disso,**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Tarefa 1: criar o grupo de administradores do controlador de domínio de saudação do AD do Azure
Olá primeira tarefa é toocreate um grupo administrativo em seu locatário do AD do Azure. Este grupo administrativo especial é chamado *AAD DC Administrators*. Os membros deste grupo recebem permissões administrativas nos computadores que ingressaram no domínio toohello gerenciado do Azure Active Directory Domain Services domínio. Em computadores que ingressaram no domínio, esse grupo é adicionado toohello grupo de administradores. Além disso, os membros desse grupo podem usar a área de trabalho remota tooconnect remotamente toodomain-computadores que ingressaram no.  

> [!NOTE]
> Você não tem permissões de administrador de domínio ou administrador corporativo no hello domínio gerenciado que você criou usando o Azure Active Directory Domain Services. Em domínios gerenciados, essas permissões são reservadas pelo serviço hello em não ficam disponíveis toousers dentro do locatário hello. No entanto, você pode usar o grupo administrativo especial Olá criado no tooperform de tarefa configuração algumas operações privilegiadas. Essas operações incluem ingressar em domínio toohello dos computadores que pertencem a grupo de administração de toohello em computadores que ingressaram no domínio e configurar política de grupo.
>

Esta tarefa de configuração, criar grupo administrativo hello e adicionar um ou mais usuários no grupo de toohello de diretório. grupo administrativo do toocreate Olá para o Azure Active Directory Domain Services, Olá a seguir:

1. Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo do hello, selecione Olá **do Active Directory** botão.
3. Selecione o locatário de AD do Azure hello (diretório) para o qual você deseja que o Azure tooenable serviços de domínio Active Directory. Você pode criar apenas um domínio para cada diretório do Azure AD.

    ![Selecionar um diretório do Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Em Olá **directory visualização** , clique em Olá **grupos** guia.
5. clique de um locatário de grupo tooyour AD do Azure, no painel de tarefas de saudação na parte inferior da saudação da janela de saudação tooadd **adicionar grupo**.

    ![botão Adicionar grupo de saudação](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. Em Olá **adicionar grupo** caixa de diálogo caixa, crie um grupo chamado **AAD DC administradores**e, em seguida, defina **tipo de grupo** muito**segurança**.

   > [!WARNING]
   > acesso de tooenable em seu domínio gerenciado do Azure Active Directory Domain Services, crie um grupo com esse nome exato.
   >
   >

    ![caixa de diálogo Adicionar grupo Olá](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. Em Olá **descrição** , digite uma descrição que permite que outras pessoas toounderstand neste grupo concede permissões administrativas no Azure Active Directory Domain Services.
8. Depois de criar o grupo de hello, clique em tooview de nome de grupo Olá suas propriedades.
9. tooadd usuários como membros do grupo de hello, na parte inferior da saudação da janela de saudação, clique em Olá **adicionar membros** botão.

    ![Botão Adicionar membros do grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. Em Olá **adicionar membros** caixa de diálogo, os usuários de saudação select que devem ser membros desse grupo e clique no ícone de marca de seleção de saudação em hello inferior direito.

    ![Adicionar grupo de usuários do tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Próxima etapa
[Tarefa 2: Criar ou selecionar uma rede virtual do Azure](active-directory-ds-getting-started-vnet.md)
