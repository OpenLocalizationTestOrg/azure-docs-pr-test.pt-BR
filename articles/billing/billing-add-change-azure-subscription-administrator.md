---
title: "aaaAdd ou alterar funções de assinatura de administração do Azure | Microsoft Docs"
description: "Descreve como tooadd ou alterar Coadministrador do Azure, o administrador de serviço e o administrador da conta"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Adicionar ou alterar as funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços
Você pode alterar Olá administrador do Azure que gerencia a sua assinatura do Azure ou gerencia Olá serviços do Azure usados na sua assinatura. tooview as informações de cobrança do Azure e gerenciar assinaturas, você deve entrar no toohello [Centro de contas](https://account.windowsazure.com/Home/Index) como Olá administrador da conta. 

## <a name="add-an-admin-for-a-subscription"></a>Adicionar um administrador para uma assinatura
Você pode adicionar um administrador do Azure em Olá portal do Azure ou em Olá portal clássico do Azure.

**Portal do Azure**

tooadd alguém como um administrador para uma assinatura no hello portal do Azure, você lhes função de proprietário de saudação. função de proprietário de saudação só pode gerenciar recursos Olá na assinatura de saudação que você atribuiu. Ele não tem assinaturas de tooother de privilégio de acesso. Olá proprietários adicionar por meio de saudação [portal do Azure](https://portal.azure.com) não é possível gerenciar recursos no hello [portal clássico do Azure](https://manage.windowsazure.com).

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, selecione **assinatura** > *Olá assinatura que você deseja Olá administrador tooaccess*.

    ![Captura de tela que mostra a assinatura selecionada](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Na folha de assinatura hello, selecione **(IAM) do controle de acesso**.
4. Selecione **Adicionar** > **Função** > **Proprietário**. Digite o endereço de email de saudação do usuário Olá você deseja tooadd como proprietário, o usuário selecione Olá e, em seguida, selecione **salvar**.

    ![Captura de tela que mostra a função de proprietário de saudação selecionada](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Se quiser que a conta do proprietário Olá tooadd como coadministrador, em hello **(IAM) do controle de acesso** página, clique com botão direito usuário Olá e, em seguida, selecione **adicionar como coadministrador**. Esse recurso agora está disponível na [versão prévia do portal do Azure](https://preview.portal.azure.com/). 

     ![Captura de tela que adiciona o coadministrador](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Você precisará de usuário de "Proprietário" hello tooadd como coadministrador se precisar de usuário Olá toomanage Olá serviços do Azure em [portal clássico do Azure](https://manage.windowsazure.com/).

    tooremove permissão de coadministrador hello, usuário de "coadministrador" hello e, em seguida, selecione **remover o coadministrador**.

    ![Captura de tela que remove o coadministrador](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Portal clássico do Azure**

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/).
2. No painel de navegação hello, selecione **configurações**> **administradores**> **adicionar**. </br>

    ![Captura de tela que mostra como tooget toohello adicionar botão](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Saudação de tipo endereço de email da pessoa a saudação ser tooadd como coadministrador e selecione Olá assinatura que você deseja Olá coadministrador tooaccess.</br>

    ![Captura de tela que mostra uma assinatura selecionada ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Olá, endereço de email a seguir pode ser adicionada como um Coadministrador:

* **Conta da Microsoft** (anteriormente Windows Live Id) </br>
  Você pode usar um toosign Account da Microsoft em tooall orientados ao consumidor produtos da Microsoft e serviços de nuvem, como o Outlook (Hotmail), (MSN) Skype, OneDrive, Windows Phone e Xbox LIVE.
* **Organizational account**</br>
  : uma conta organizacional é uma conta criada no Active Directory do Azure. endereço de conta organizacional Olá tem este formato:

    usuario@&lt;seu domínio&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Alterar o Administrador de Serviços de uma assinatura
Olá administrador da conta pode alterar Olá administrador de serviço para uma assinatura.

1. Entrar muito[Centro de contas Azure](https://account.windowsazure.com/subscriptions) usando Olá administrador da conta.
2. Selecione a assinatura de saudação toochange desejado.
3. Selecione direita hello, **Editar assinatura** detalhes. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. Em Olá **administrador de serviço** , digite o endereço de email de saudação do hello novo administrador do serviço. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Alterar Olá administrador da conta
a propriedade tootransfer de saudação do Azure tooanother conta, consulte [transferir a propriedade de uma assinatura do Azure](billing-subscription-transfer.md).

É altamente recomendável que você não exclua ou renomeie o endereço de email do administrador da conta de saudação. Você pode observar o comportamento e não esperado com hello conta do Azure. Você não pode ser tooAzure capaz de entrar com essa conta, fazer alterações toohello conta ou gerenciar recursos com essa conta. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Verificar Olá administrador da conta de assinatura de saudação
Se você não tiver certeza de que o administrador da conta Olá é para sua assinatura, use Olá seguindo as etapas toofind-out.

  1. Entrar toohello [portal do Azure](https://portal.azure.com).
  2. No menu de Hub hello, selecione **assinatura**.
  3. Selecione Olá assinatura você deseja toocheck e, em seguida, procure em **configurações**.
  4. Selecione **Propriedades**. Olá administrador da conta Olá assinatura é exibido no hello **administrador da conta** caixa.  

## <a name="types-of-azure-admin-accounts"></a>Tipos de contas de administrador do Azure
 Conta de administrador, administrador de serviço e co-administrador são três tipos de saudação de funções de administrador no Microsoft Azure. Olá, tabela a seguir descreve Olá diferença entre essas três funções administrativas.

| Função administrativa | Limite | Descrição |
| --- | --- | --- |
| AA (Administrador da Conta) |1 por conta do Azure |Isso é Olá pessoa inscreveu ou comprar assinaturas do Azure e é autorizado tooaccess hello [Centro de contas](https://account.windowsazure.com/Home/Index) e executar várias tarefas de gerenciamento. Esses incluem toocreate capaz de assinaturas, cancelar assinaturas, alterar a cobrança Olá para uma assinatura e alterar Olá administrador de serviço. |
| SA (Administrador de Serviços) |1 por assinatura do Azure |Essa função é serviços autorizados toomanage em Olá [portal do Azure](https://portal.azure.com). Por padrão, para uma nova assinatura, Olá administrador da conta é também Olá administrador de serviço. |
| Coadministrador (CA) em Olá [portal clássico do Azure](https://manage.windowsazure.com) |200 por assinatura |Essa função tem Olá mesmo privilégios de acesso como Olá administrador de serviço, mas não é possível alterar a associação de saudação dos diretórios de tooAzure de assinaturas. |

Controle de acesso do Azure com base em função do Active Directory (RBAC) permite que os usuários toobe adicionado toomultiple funções. Para obter mais informações, confira [Controle de acesso baseado em função do Active Directory do Azure](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Limitações e restrições para contas de administrador
* Cada assinatura é associada um diretório do AD do Azure (também conhecido como Olá diretório padrão). Olá toofind assinatura de saudação do diretório padrão está associado, vá toohello [portal clássico do Azure](https://manage.windowsazure.com/), selecione **configurações** > **assinaturas**. Verifique Olá assinatura ID toofind Olá diretório padrão.
* Se você tiver entrado com uma Account da Microsoft, você só pode adicionar outros Accounts da Microsoft ou usuários no diretório padrão de saudação como Coadministrador.
* Se você estiver conectado a uma conta organizacional, você poderá adicionar outras contas organizacionais em sua organização como Coadministrador. Por exemplo, abby@contoso.com pode adicionar bob@contoso.com como Administrador de Serviços ou Coadministrador, mas não pode adicionar john@notcontoso.com, a menos que john@notcontoso.com esteja no Diretório Padrão. Usuários conectados com as contas organizacionais podem continuar tooadd usuários de Account da Microsoft como administrador de serviço ou Coadministrador.
* Agora que é possível toosign em tooAzure com uma conta organizacional, aqui estão Olá alterações tooService administrador e requisitos de conta de coadministrador:

  | Método de entrada | Adicionar Conta da Microsoft ou usuários no Diretório Padrão como CA ou SA? | Adicionar conta organizacional no hello mesma organização como autoridade de certificação ou SA? | Adicionar conta organizacional em uma organização diferente como CA ou SA? |
  | --- | --- | --- | --- |
  |  Conta da Microsoft |Sim |Não |Não |
  |  Conta organizacional |Sim |Sim |Não |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Saiba mais sobre o controle de acesso a recursos e o Active Directory
* toolearn mais sobre como o acesso aos recursos é controlado no Microsoft Azure, consulte [Noções básicas sobre o acesso a recursos no Azure](../active-directory/active-directory-understanding-resource-access.md).
* Para saber mais sobre como o Azure Active Directory, confira [Como as assinaturas do Azure estão associadas ao Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) e [Atribuição de funções de administrador no Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
