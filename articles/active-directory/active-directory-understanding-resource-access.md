---
title: acesso a recursos no Azure aaaUnderstanding | Microsoft Docs
description: "Este tópico explica os conceitos sobre como usar o acesso a recursos assinatura administradores toocontrol Olá portal completo do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Noções básicas sobre o acesso aos recursos do Azure
> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Olá portal do Azure fornece [controle de acesso baseado em função](role-based-access-control-configure.md) para recursos do Azure possam ser gerenciados com mais precisão.
> 
> 

Em outubro de 2013, Olá portal clássico do Azure e as APIs de gerenciamento do serviço foram integrados com o Active Directory do Azure em bases de saudação toolay ordem para melhorar a experiência do usuário Olá para gerenciar recursos de tooAzure de acesso. O Active Directory do Azure já fornece ótimos recursos como o gerenciamento de usuários, sincronização de diretórios local, autenticação multifator e controle de acesso do aplicativo. Naturalmente, eles também devem ser disponibilizados para gerenciar os recursos do Azure globalmente.

O controle de acesso no Azure parte de uma perspectiva de cobrança. proprietário de saudação de uma conta do Azure, acessado visitando Olá [Centro de contas Azure](https://account.windowsazure.com/subscriptions), é hello conta AA (administrador). As assinaturas são um contêiner para cobrança, mas também atuam como um limite de segurança: cada assinatura tem um serviço SA (administrador) que pode adicionar, remover e modificar recursos do Azure nessa assinatura usando Olá [portal clássico do Azure](https://manage.windowsazure.com/). Olá SA de padrão de uma nova assinatura é Olá AA, mas Olá AA pode alterar Olá SA no hello Centro de contas do Azure.

<br><br>![Contas do Azure][1]

As assinaturas também têm uma associação com um diretório. diretório de saudação define um conjunto de usuários. Eles podem ser usuários de saudação ou de estudante que criou o diretório de saudação ou podem ser usuários externos (ou seja, Accounts da Microsoft). As assinaturas são acessíveis por um subconjunto desses usuários de diretório que foram atribuídos como administrador de serviços (SA) ou CA (Coadministrador); Olá apenas a exceção é que, por razões herdadas, Accounts da Microsoft (anteriormente Windows Live ID) podem ser atribuídas como SA ou CA sem estarem presentes no diretório de saudação.

<br><br>![Controle de acesso no Azure][2]

Funcionalidade em Olá portal clássico do Azure permite que os SAs que se conectaram usando um diretório de saudação toochange Account da Microsoft que uma assinatura está associada usando Olá **Editar diretório** comando Olá **Assinaturas** página **configurações**. Observe que esta operação tem implicações no controle de acesso de saudação de assinatura.

> [!NOTE]
> Olá **Editar diretório** comando em Olá clássico do Azure portal não está disponível toousers que se conectaram usando uma conta corporativa ou de estudante porque essas contas podem entrar apenas toohello directory toowhich pertencem.
> 
> 

<br><br>![Fluxo de Logon de Usuário Simples][3]

No caso mais simples hello, uma organização (por exemplo, Contoso) impõe a cobrança e controle de acesso no mesmo conjunto de assinaturas de saudação. Ou seja, o diretório de saudação é toosubscriptions associado que pertencem a uma única conta do Azure. Após o logon bem-sucedido toohello portal clássico do Azure, os usuários veem duas coleções de recursos (descritos em laranja na ilustração anterior Olá):

* Diretórios onde sua conta de usuário existe (originados ou adicionados como uma entidade externa). Observe diretório Olá usado para o logon não é toothis relevantes de computação, assim os diretórios serão sempre mostrados independentemente de onde você fez logon.
* Recursos que fazem parte das assinaturas associadas com o diretório Olá usado para logon e que Olá usuário podem acessar (seja um SA ou CA).

<br><br>![Usuário com Várias Assinaturas e Diretórios][4]

Usuários com assinaturas em vários diretórios têm Olá Olá capacidade tooswitch atual contexto de saudação portal clássico do Azure usando o filtro de assinatura de saudação. Olá oculta, isso resulta em um diretório diferente de tooa logon separado, mas isso é feito de maneira integrada usando o logon único (SSO).

Operações como mover recursos entre as assinaturas podem ser mais difíceis como resultado desta visão única de diretório de assinaturas. transferência de recursos do tooperform hello, talvez seja necessário toofirst usar Olá **Editar diretório** comando na página de assinaturas de saudação em **configurações** tooassociate Olá assinaturas toohello mesmo diretório .

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre como os administradores de toochange para uma assinatura do Azure, consulte [como tooadd ou alterar funções de administrador do Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Para obter mais informações sobre como o Active Directory do Azure se relaciona tooyour assinatura do Azure, consulte [assinaturas do Azure como estão associadas com o Active Directory do Azure](active-directory-how-subscriptions-associated-directory.md)
* Para obter mais informações sobre como as funções de tooassign no AD do Azure, consulte [atribuindo funções de administrador no Active Directory do Azure](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
