---
title: "aaaNo usuários estão sendo provisionado tooan AD do Azure Galeria aplicativo | Microsoft Docs"
description: "Como tootroubleshoot problemas enfrentam quando você não vir os usuários que aparecem em um AD do Azure aplicativo Galeria que você configurou para o provisionamento de usuário com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Nenhum usuário está sendo provisionado tooan AD do Azure Galeria aplicativo

O provisionamento automático de uma vez foi configurado para um aplicativo (incluindo a verificação de que as credenciais do aplicativo hello fornecida tooAzure AD tooconnect toohello aplicativo são válidos). Em seguida, os usuários e/ou grupos são provisionados toohello aplicativo e é determinado pelo Olá coisas a seguir:

-   Quais usuários e grupos têm sido **atribuído** toohello aplicativo. Para obter mais informações sobre a atribuição, consulte [atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Ou não **mapeamentos de atributo** são atributos válidos de toosync habilitado e configurado de aplicativo do Azure AD toohello. Para obter mais informações sobre mapeamentos de atributo, consulte [Personalizando mapeamentos de atributo do provisionamento de usuário para aplicativos SaaS no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Se há ou não um **filtro de escopo** presente que está filtrando usuários com base nos valores de atributo específico. Para obter mais informações sobre filtros de escopo, consulte [provisionamento de aplicativos com base em atributo com filtros de escopo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Ao observar que os usuários não estão sendo provisionados, consulte os logs de auditoria de saudação no AD do Azure e procure entradas de log para um usuário específico.

Olá provisionamento logs de auditoria pode ser acessada no hello portal do Azure, na Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[nome do aplicativo\] &gt; Logs de auditoria**guia. Saudação de filtro logon Olá **provisionamento de conta** tooonly categoria consulte Olá provisionamento eventos para esse aplicativo. Você pode procurar usuários com base em hello "correspondência ID" que foi configurado para eles nos mapeamentos de atributo hello. Por exemplo, se você configurou hello "user principal name" ou "endereço de email" como Olá correspondência de atributo no lado de saudação do AD do Azure e não sendo provisionamento de usuário de saudação tem um valor de "audrey@contoso.com". Pesquisar logs de auditoria de saudação do "audrey@contoso.com" e examine e entradas retornadas.

Olá provisionamento auditoria registra todos Olá operações executadas pelo serviço de provisionamento hello, incluindo consultas AD do Azure para os usuários atribuídos que estejam no escopo para provisionamento, consultando o aplicativo de destino Olá existência Olá desses usuários, comparando saudação do registro objetos de usuário entre o sistema de saudação. Em seguida, adicionar, atualizar ou desabilitar a conta de usuário de saudação no sistema de destino de saudação com base em comparação de saudação.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Áreas de problemas gerais com o provisionamento tooconsider

Abaixo está uma lista de saudação áreas de problema geral que você pode analisar se você tiver uma ideia de onde toostart.

* [Serviço de provisionamento não aparece toostart](#provisioning-service-does-not-appear-to-start)
* [Logs de auditoria informa quais usuários são ignorados e não provisionados, mesmo que eles sejam atribuídos](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Serviço de provisionamento não aparece toostart

Se você definir Olá **Status de provisionamento** toobe **na** em Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[denomedeaplicativo\] &gt;Provisionamento** seção Olá portal do Azure. No entanto, nenhum outro detalhes de status são mostrados na página depois recarrega subsequentes, é provável que o serviço de hello está sendo executado, mas não concluiu uma sincronização inicial ainda. Verificar Olá **logs de auditoria** descrito acima toodetermine quais operações Olá executa, e se há erros.

>[!NOTE]
>Uma sincronização inicial pode levar de horas de tooseveral de 20 minutos, dependendo do tamanho de Olá Olá diretório AD do Azure e o número de saudação de usuários em escopo para provisionamento. As sincronizações subsequentes após a sincronização inicial de saudação são mais rápidas, como Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial de saudação. Isso melhora o desempenho de sincronizações subsequentes.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Logs de auditoria informa quais usuários são ignorados e não provisionados, mesmo que eles sejam atribuídos

Quando um usuário aparecer como "ignorado" nos logs de auditoria Olá, é muito importante tooread Olá detalhes em razão de Olá Olá log mensagem toodetermine estendidos. Veja a seguir as resoluções e motivos comuns:

-   **Um filtro de escopo foi configurado** **que está filtrando usuário Olá com base em um valor de atributo**. Para obter mais informações sobre filtros de escopo, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **usuário de saudação é "não efetivamente intitulado".** Se você vir essa mensagem de erro específica, é porque não há um problema com o registro de atribuição do usuário Olá armazenado no AD do Azure. toofix esse problema, cancele sua atribuição Olá usuário (ou grupo) do aplicativo hello e novamente atribuí-lo novamente. Para obter mais informações sobre atribuição, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Um atributo obrigatório está ausente ou não está preenchido para um usuário.** Tooconsider uma coisa importante quando a configuração de provisionamento ser tooreview e configurar mapeamentos de atributo hello e fluxos de trabalho que definem quais fluxo de propriedades de usuário (ou grupo) do aplicativo de toohello do AD do Azure. Isso inclui a configuração hello "correspondência da propriedade" ser toouniquely usada identificar e corresponder usuários/grupos entre sistemas Olá dois. Para obter mais informações sobre este importante processo, consulte [Personalizando mapeamentos de atributo do provisionamento de usuário para aplicativos SaaS no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Mapeamentos de grupos de atributos:** provisionamento de saudação grupo detalhes de nome e grupo, em membros de toohello de adição, se houver suporte para alguns aplicativos. Você pode habilitar ou desabilitar essa funcionalidade habilitando ou desabilitando Olá **mapeamento** para objetos de grupo mostrados no hello **provisionamento** guia. Se grupos de provisionamento está habilitado, certifique-se de que tooreview Olá atributo mapeamentos tooensure um campo apropriado está sendo usado para hello "correspondência de ID". Isso pode ser Olá exibição nome ou alias de email), como Olá grupo e seus membros não ser provisionado se hello a propriedade correspondente está vazio ou não preenchido para um grupo no AD do Azure.

## <a name="next-steps"></a>Próximas etapas
[Sincronização do Azure AD Connect: noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

