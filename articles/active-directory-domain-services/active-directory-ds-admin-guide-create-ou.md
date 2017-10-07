---
title: "Azure Active Directory Domain Services: guia de administração | Microsoft Docs"
description: "Criar uma UO (Unidade Organizacional) em um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Criar uma Unidade Organizacional (UO) em um domínio gerenciado dos Serviços de Domínio do Azure AD
Domínios gerenciados dos Serviços de Domínio do Azure AD incluem dois contêineres internos chamados 'Computadores do AADDC' e 'Usuários do AADDC', respectivamente. Olá 'AADDC computadores' contêiner tem objetos de computador para todos os computadores que estão unidas domínio gerenciado toohello. contêiner de 'Usuários AADDC' Hello inclui usuários e grupos no locatário do AD do Azure hello. Ocasionalmente, pode ser necessário toocreate contas de serviço Olá gerenciado domínio toodeploy cargas de trabalho. Para essa finalidade, você pode criar um personalizado UO (unidade organizacional) no domínio gerenciado hello e criar contas de serviço dessa ou. Este artigo mostra como toocreate uma UO no seu domínio gerenciado.

## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).
4. Uma máquina virtual de domínio do qual você administrar os serviços de domínio de saudação do AD do Azure gerenciados domínio. Se você não tiver tal uma máquina virtual, execute todas as tarefas de saudação descritas no artigo Olá intitulado [ingressar em um domínio gerenciado do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Você precisa ter credenciais de saudação de um **usuário conta pertencentes toohello ' AAD controlador de domínio do grupo 'Administradores** em seu diretório, toocreate uma UO personalizada no seu domínio gerenciado.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Instalar ferramentas de administração do AD em uma máquina virtual ingressada no domínio para administração remota
Domínios gerenciados de serviços de domínio do AD do Azure podem ser gerenciados remotamente usando ferramentas familiares de administrativo do Active Directory como Olá Active Directory Administrative ADAC (centro) ou o PowerShell do AD. Administradores de inquilinos não possuem controladores de toodomain tooconnect privilégios Olá de domínio gerenciados por meio da área de trabalho remota. tooadminister Olá domínio gerenciado, instale o recurso de ferramentas de administração de saudação AD em um domínio gerenciado de toohello unidas de máquina virtual. Consulte o artigo toohello intitulado [administrar um domínio gerenciado do serviços de domínio do AD do Azure](active-directory-ds-admin-guide-administer-domain.md) para obter instruções.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Criar uma unidade organizacional no domínio gerenciado Olá
Agora que ferramentas administrativas Olá AD estão instaladas em Olá ingressado no domínio máquina virtual, podemos usar essas ferramentas toocreate uma unidade organizacional no domínio Olá gerenciado. Execute Olá etapas a seguir:

> [!NOTE]
> Somente membros Olá ' AAD DC' do grupo de administradores têm Olá toocreate privilégios necessários um OU personalizado. Certifique-se de que você realize Olá etapas a seguir como um usuário que pertence a grupo toothis.
>
>

1. Na tela de início de saudação, clique em **ferramentas administrativas**. Você deve ver as ferramentas administrativas do AD de saudação instaladas na máquina virtual de saudação.

    ![Ferramentas Administrativas instaladas no servidor](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Clique em **Centro Administrativo do Active Directory**.

    ![Centro Administrativo do Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. domínio de saudação tooview, clique em nome de domínio de saudação no painel esquerdo da saudação (por exemplo, ' contoso100.com').

    ![ADAC - exibir domínio](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Olá direita **tarefas** painel, clique em **novo** sob o nó de nome de domínio de saudação. Neste exemplo, se clicarmos **novo** nó Olá 'contoso100(local)' hello direita **tarefas** painel.

    ![ADAC - nova UO](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Você deve ver Olá opção toocreate uma unidade organizacional. Clique em **unidade organizacional** toolaunch Olá **Criar unidade organizacional** caixa de diálogo.
6. Em Olá **Criar unidade organizacional** caixa de diálogo, especifique um **nome** para Olá nova UO. Forneça uma breve descrição de saudação UO. Você também pode definir Olá **gerenciado por** hello OU campo. toocreate hello OU personalizada, clique em **Okey**.

    ![ADAC - criar caixa de diálogo da UO](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. Olá recém-criado OU agora deve aparecer em Olá AD ADAC (Centro Administrativo).

    ![ADAC - UO criada](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Permissões/segurança para UOs recém-criadas
Por padrão, o usuário de saudação (membro do grupo Olá 'Administradores do controlador de domínio do AAD') que criou a saudação OU personalizado tem privilégios administrativos (controle total) sobre Olá UO. usuário Hello, vá em frente e conceder privilégios tooother usuários ou toohello ao grupo 'Administradores de controlador de domínio do AAD' conforme desejado. Conforme visto no hello captura de tela a seguir, Olá usuário 'bob@domainservicespreview.onmicrosoft.com' que a nova unidade de organização 'MyCustomOU' hello criado é concedida controle total sobre ele.

 ![ADAC - segurança da nova UO](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Notas sobre como administrar UOs personalizadas
Agora que você criou uma UO personalizada, pode criar usuários, grupos, computadores e contas de serviço nessa UO. Você não pode mover os usuários ou grupos de saudação 'AADDC usuários' UO toocustom UOs.

> [!WARNING]
> As contas de usuário, de grupos, as contas de serviço e de objetos de computador que você criar em OUs personalizadas não ficam disponíveis no seu locatário do Azure AD. Em outras palavras, esses objetos não mostrar o uso de saudação do Azure AD Graph API ou em Olá da interface do AD do Azure. Esses objetos só estarão disponíveis no seu domínio gerenciado dos Azure AD Domain Services.
>
>

## <a name="related-content"></a>Conteúdo relacionado
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Configurar a Política de Grupo em um domínio gerenciado](active-directory-ds-admin-guide-administer-group-policy.md)
* [Centro Administrativo do Active Directory: introdução](https://technet.microsoft.com/library/dd560651.aspx)
* [Guia passo a passo de contas de serviço](https://technet.microsoft.com/library/dd548356.aspx)
