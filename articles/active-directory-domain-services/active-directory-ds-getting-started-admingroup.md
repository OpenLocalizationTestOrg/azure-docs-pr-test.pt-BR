---
title: "Azure Active Directory Domain Services: introdução | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)"
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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)


## <a name="task-3-configure-administrative-group"></a>Tarefa 3: configurar um grupo administrativo
Nesta tarefa de configuração, você cria um grupo administrativo em seu diretório do Azure AD. Este grupo administrativo especial é chamado *AAD DC Administrators*. Os membros deste grupo recebem permissões administrativas nos computadores com domínio gerenciado toohello ingressado no domínio. Em computadores que ingressaram no domínio, esse grupo é adicionado toohello grupo de administradores. Além disso, os membros desse grupo podem usar a área de trabalho remota tooconnect remotamente toodomain-computadores que ingressaram no.

> [!NOTE]
> Você não tem permissões de administrador de domínio ou administrador corporativo no hello domínio gerenciado que você criou usando o Azure Active Directory Domain Services. Em domínios gerenciados, essas permissões são reservadas pelo serviço hello em não ficam disponíveis toousers dentro do locatário hello. No entanto, você pode usar o grupo administrativo especial Olá criado no tooperform de tarefa configuração algumas operações privilegiadas. Essas operações incluem ingressar em domínio toohello dos computadores que pertencem a grupo de administração de toohello em computadores que ingressaram no domínio e configurar política de grupo.
>

Assistente de saudação cria automaticamente o grupo administrativo Olá em seu diretório do AD do Azure. Esse grupo se chama "Administradores do AAD DC". Se você tiver um grupo existente com esse nome no diretório do AD do Azure, o Assistente de saudação seleciona esse grupo. Você pode configurar a associação de grupo usando Olá **grupo administrador** página do assistente.

1. associação de grupo tooconfigure, clique em **AAD DC administradores**.

    ![Configurar associação ao grupo](./media/getting-started/domain-services-blade-admingroup.png)

2. Clique em Olá **adicionar membros** botão tooadd usuários do seu grupo de administradores do AD do Azure diretório toohello.

3. Quando terminar, clique em **Okey** toomove na toohello **resumo** página do Assistente de saudação.

4. Em Olá **resumo** página do Assistente de saudação, examine Olá configurações de domínio gerenciado hello. Você pode voltar tooany etapa do assistente toomake altera o hello, se necessário. Quando terminar, clique em **Okey** toocreate Olá gerenciados novo domínio.

    ![Resumo](./media/getting-started/domain-services-blade-summary.png)

5. Você verá uma notificação que mostra o andamento da saudação da sua implantação de serviços de domínio do AD do Azure. Clique em notificação Olá toosee detalhadas progresso para a implantação de saudação.

    ![Notificação – implantação em andamento](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Provisionar o domínio gerenciado
Olá processo de provisionamento de seu domínio gerenciado pode levar horas tooan.

1. Durante a implantação está em andamento, você pode procurar 'Serviços de domínio' hello **pesquisar recursos** caixa de pesquisa. Selecione **serviços de domínio do AD do Azure** Olá resultados de pesquisa. Olá **serviços de domínio do AD do Azure** folha lista Olá domínio gerenciado que está sendo provisionado.

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Clique o nome de saudação do hello gerenciado toosee de domínio (por exemplo, ' contoso100.com') mais detalhes sobre o domínio de saudação.

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. Olá **visão geral** guia mostra esse domínio hello está atualmente sendo provisionado. Você não pode configurar o domínio gerenciado Olá até que ele está totalmente provisionado. Pode levar até horas tooan para sua toobe domínio gerenciado totalmente provisionado.

    ![Serviços de domínio - guia de visão geral durante a saudação estado de provisionamento ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Quando o domínio gerenciado hello está totalmente provisionado, Olá **visão geral** guia mostra o status de domínio hello como **executando**.

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned.png)

5. Em Olá **propriedades** guia, você ver dois endereços IP no qual domínio os controladores estão disponíveis para rede virtual hello.

    ![Serviços de domínio – guia Propriedades após a conclusão do provisionado](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Próxima etapa
[Tarefa 4: atualizar configurações de DNS Olá Olá rede virtual do Azure](active-directory-ds-getting-started-dns.md)
