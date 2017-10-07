---
title: "aaaAutomated SaaS aplicativo provisionamento do usuário no AD do Azure | Microsoft Docs"
description: "Um toohow de Introdução, você pode usar o provisionamento de tooautomatically do AD do Azure, desprovisionar e atualizar continuamente as contas de usuário em vários aplicativos SaaS de terceiros."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatizar o provisionamento e desprovisionamento tooSaaS aplicativos com o Azure Active Directory de usuário
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>O que é o provisionamento automatizado de usuários para aplicativos SaaS?
Azure Active Directory (AD do Azure) permite a criação de saudação tooautomate, manutenção e remoção das identidades de usuário na nuvem ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplicativos como o Dropbox, Salesforce, ServiceNow e muito mais.

**Abaixo estão alguns exemplos de como o que esse recurso permite que você toodo:**

* Crie automaticamente novas contas na Olá direita aplicativos de SaaS para novas pessoas quando estiverem em sua equipe.
* Desative automaticamente contas de aplicativos SaaS quando pessoas inevitavelmente deixam equipe hello.
* Certifique-se de que as identidades de saudação em seus aplicativos SaaS são mantidas backup toodate com base em alterações no diretório de saudação.
* Provisionar objetos não-usuário, como grupos, tooSaaS aplicativos que dão suporte a eles.

**Provisionamento automatizado de usuários também inclui Olá funcionalidade a seguir:**

* Olá identidades existentes do capacidade toomatch entre o Azure AD e aplicativos SaaS.
* Toohelp de opções de personalização do AD do Azure ajusta as configurações atuais de saudação de aplicativos SaaS Olá que sua organização está usando atualmente.
* Alertas de email opcionais para erros de provisionamento.
* Emissão de relatórios e a atividade toohelp de logs com o monitoramento e solução de problemas.

## <a name="why-use-automated-provisioning"></a>Por que usar o provisionamento automatizado?
Alguns motivos comuns para usar esse recurso incluem:

* custos de saudação tooavoid, ineficiências e erro humano associado com processos de provisionamento manual.
* toosecure de sua organização removendo instantaneamente as identidades dos usuários de chave aplicativos SaaS quando sair da organização hello.
* tooeasily importar em massa de usuários em um determinado aplicativo SaaS.
* conveniência de saudação tooenjoy de sua solução de provisionamento executar logoff Olá mesmas políticas de acesso de aplicativo que você definiu para o Azure AD Single Sign-On.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
**Frequência o AD do Azure escrever o aplicativo de SaaS do diretório alterações toohello?**

AD do Azure verifica alterações a cada cinco minutos tooten. Se o aplicativo de SaaS hello está retornando vários erros (como no caso de saudação de credenciais de administrador inválido), o AD do Azure gradualmente lenta tooonce de tooup sua frequência por dia até Olá erros sejam corrigidos.

**Quanto tempo levará tooprovision meus usuários?**

Alterações incrementais acontecem quase instantaneamente, mas se você está tentando tooprovision a maior parte do seu diretório, e depende do número de saudação de usuários e grupos que você possui. Diretórios pequenos podem levar apenas alguns minutos, diretórios de médio porte podem levar vários minutos e diretórios muito grandes podem levar várias horas.

**Como posso acompanhar o progresso Olá Olá trabalho de provisionamento atual?**

Você pode revisar Olá relatório de provisionamento de conta na seção de relatórios de saudação do seu diretório. Outra opção é toovisit Olá painel Guia de saudação aplicativo SaaS que estiver Provisionando para e procure Olá a seção "Status da integração" inferior Olá da página de saudação.

**Como saber se os usuários não tooget provisionado corretamente?**

Final Olá Olá provisionamento Assistente de configuração existe é uma opção toosubscribe tooemail as notificações provisionamento falhas. Você também pode verificar toosee do relatório de erros de provisionamento Olá quais usuários falha toobe provisionado e por quê.

**O AD do Azure pode gravar alterações do diretório de backup toohello Olá SaaS aplicativo?**

Para a maioria dos aplicativos SaaS, o provisionamento é somente de saída, que significa que os usuários são gravados do aplicativo de toohello directory hello e alterações de aplicativo hello não podem ser gravadas novamente toohello directory. Para [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), no entanto, o provisionamento é apenas de entrada, o que significa que o que os usuários são importados para o diretório de saudação do Workday e da mesma forma, as alterações no diretório de saudação não obter write-back em dia de trabalho.

**Como posso enviar a equipe de engenharia de toohello comentários?**

Entre em contato conosco por meio de saudação [Fórum de comentários do Active Directory do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>Como funciona o trabalho de provisionamento automatizado?
O AD do Azure provisiona usuários tooSaaS aplicativos conectando-se pontos de extremidade de tooprovisioning fornecidos por cada fornecedor do aplicativo. Esses pontos de extremidade permite que o Azure AD tooprogrammatically criar, atualizar e remover usuários. Abaixo está uma visão geral de saudação etapas diferentes que o AD do Azure usa tooautomate provisionamento.

1. Quando você habilitar o provisionamento de um aplicativo para Olá primeira vez, Olá ações a seguir é executada:
   * O AD do Azure tentará toomatch quaisquer usuários existentes no aplicativo de SaaS Olá com suas identidades correspondentes no diretório de saudação. Quando um usuário for correspondido, ele *não* será automaticamente habilitado para logon único. Em ordem para um aplicativo de toohello de acesso do usuário toohave, eles devem ser explicitamente atribuídos toohello aplicativo no AD do Azure, diretamente ou por meio de associação de grupo.
   * Se você já especificou quais usuários devem ser atribuídos toohello aplicativo, e se o AD do Azure falha toofind a contas existentes para os usuários, o AD do Azure provisionar novas contas para eles no aplicativo hello.
2. Depois que a sincronização inicial hello foi concluída conforme descrito acima, o AD do Azure verificará cada 10 minutos para Olá as seguintes alterações:
   * Se novos usuários foram atribuídos toohello aplicativo (diretamente ou por meio da associação de grupo), eles serão provisionados uma nova conta no aplicativo de SaaS hello.
   * Se um acesso de usuário foi removido, suas contas no aplicativo de SaaS Olá serão marcada como desabilitado (os usuários são nunca totalmente excluídos, que protege contra perda de dados no evento de saudação de uma configuração incorreta).
   * Se um usuário foi atribuído recentemente toohello aplicativo e já tiverem uma conta no hello aplicativo SaaS, que conta será marcada como habilitado, e podem ser atualizadas determinadas propriedades de usuário se eles estiverem desatualizadas toohello em comparação com o diretório.
   * Se as informações do usuário (como número de telefone, local do escritório, etc) foi alteradas no diretório hello, essas informações também serão atualizadas no hello aplicativo SaaS.

Para obter mais informações sobre como os atributos são mapeados entre o AD do Azure e seu aplicativo SaaS, consulte o artigo Olá no [personalizando mapeamentos de atributo](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lista de aplicativos que dão suporte a provisionamento automatizado de usuários
Todos os aplicativos de "Em destaque" hello na Galeria de aplicativo do Azure AD Olá suportam provisionamento automatizado de usuários. [lista de saudação de aplicativos em destaque pode ser exibida aqui.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

Em ordem para um aplicativo toosupport automatizada provisionamento de usuário, ela deve primeiro fornecer Olá necessários pontos de extremidade que permitem a criação de saudação tooautomate programas externos, manutenção e remoção de usuários. Portanto, nem todos os aplicativos SaaS são compatíveis com esse recurso. Para aplicativos que dão suporte a isso, equipe de engenharia do hello AD do Azure será, em seguida, ser capaz de toobuild um provisionamento toothose de conector de aplicativos e esse trabalho é priorizado pelas necessidades de saudação de clientes atuais e potenciais.

engenharia de saudação do AD do Azure toocontact toorequest suporte para aplicativos adicionais de provisionamento da equipe, envie uma mensagem por meio de saudação [Fórum de comentários do Active Directory do Azure](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Personalizando os mapeamentos de atributos para provisionamento de usuários](active-directory-saas-customizing-attribute-mappings.md)
* [Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de escopo para provisionamento de usuários](active-directory-saas-scoping-filters.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)
* [Notificações de provisionamento de conta](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriais sobre como tooIntegrate aplicativos SaaS](active-directory-saas-tutorial-list.md)

