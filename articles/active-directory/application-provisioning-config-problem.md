---
title: "aaaProblem configurar provisionamento de aplicativo da Galeria de tooan AD do Azure do usuário | Microsoft Docs"
description: "Como tootroubleshoot problemas enfrentam durante a configuração de aplicativo tooan já listado na Galeria de aplicativos de saudação do AD do Azure de provisionamento do usuário"
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Problema na configuração de aplicativo da Galeria de tooan AD do Azure de provisionamento do usuário

Configurando [provisionamento automático de usuário](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) para um aplicativo (onde houver suporte), requer que as instruções específicas sejam tooprepare seguido Olá aplicativo para o provisionamento automático. Em seguida, você pode usar Olá tooconfigure portal do Azure Olá provisionamento de aplicativo toohello de contas de usuário do serviço toosynchronize.

Você sempre deve começar encontrando instalação Olá tutorial toosetting específico o provisionamento para seu aplicativo. Em seguida, siga essas etapas tooconfigure ambos aplicativo hello e AD do Azure toocreate Olá provisionamento de conexão. Uma lista de tutoriais de aplicativo pode ser encontrada em [lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Como toosee se provisionamento está funcionando 

Depois que o serviço Olá estiver configurado, a maioria das informações na operação de saudação do serviço Olá podem ser desenhadas em dois locais:

-   **Logs de auditoria** – hello provisionamento todas as operações de saudação executadas pelo Olá provisionamento do serviço de registro de logs de auditoria, incluindo consultas AD do Azure para atribuídas a usuários que estejam no escopo para provisionamento. Aplicativo de destino Olá existência Olá desses usuários, comparando Olá objetos de usuário entre o sistema de saudação de consulta. Em seguida, adicionar, atualizar ou desabilitar a conta de usuário de saudação no sistema de destino de saudação com base em comparação de saudação. Olá provisionamento logs de auditoria pode ser acessada no hello portal do Azure, na Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[nome do aplicativo\] &gt; Logs de auditoria**guia. Saudação de filtro logon Olá **provisionamento de conta** tooonly categoria consulte Olá provisionamento eventos para esse aplicativo.

-   **Provisionamento de status –** um resumo da saudação última provisionamento executar para um determinado aplicativo pode ser visto no hello **Active Directory do Azure &gt; aplicativos corporativos &gt; \[nome do aplicativo\] &gt; Provisionamento** seção na parte inferior da saudação da tela de saudação em configurações de serviço hello. Esta seção resume quantos usuários (e/ou grupos) estão sendo atualmente sincronizados entre hello dois sistemas, e se há erros. Detalhes do erro ser nos logs de auditoria de saudação. Observe que Olá status de provisionamento não seja preenchido até que uma sincronização completa inicial foi concluída entre o AD do Azure e o aplicativo hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Áreas de problemas gerais com o provisionamento tooconsider

Abaixo está uma lista de saudação áreas de problema geral que você pode analisar se você tiver uma ideia de onde toostart.

* [Serviço de provisionamento não aparece toostart](#provisioning-service-does-not-appear-to-start)
* [Não é possível salvar a configuração devido a credenciais tooapp não está funcionando](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Logs de auditoria informa quais usuários são ignorados e não provisionados, mesmo que eles sejam atribuídos](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Serviço de provisionamento não aparece toostart

Se você definir Olá **Status de provisionamento** toobe **na** em Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[denomedeaplicativo\] &gt;Provisionamento** seção Olá portal do Azure. No entanto, nenhum outro detalhe de status é mostrado nessa página depois recarregamentos subsequentes. É provável que o serviço de hello está sendo executado, mas não concluiu uma sincronização inicial ainda. Verificar Olá **logs de auditoria** descrito acima toodetermine quais operações Olá executa, e se há erros.

>[!NOTE]
>Uma sincronização inicial pode levar de horas de tooseveral de 20 minutos, dependendo do tamanho de Olá Olá diretório AD do Azure e o número de saudação de usuários em escopo para provisionamento. As sincronizações subsequentes após a sincronização inicial Olá ser mais rápido, Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial hello, melhorando o desempenho de sincronizações subsequentes.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Não é possível salvar a configuração devido a credenciais tooapp não está funcionando

Em ordem para provisionamento toowork, o AD do Azure requer credenciais válidas que permitem que o gerenciamento de usuários tooconnect tooa API fornecida pelo aplicativo. Se essas credenciais não funcionam, ou você não souber wat estiverem, revise o tutorial Olá para configurar este aplicativo, descrito anteriormente.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Logs de auditoria informa quais usuários são ignorados e não provisionados, mesmo que eles sejam atribuídos

Quando um usuário aparecer como "ignorado" nos logs de auditoria Olá, é muito importante tooread Olá detalhes em razão de Olá Olá log mensagem toodetermine estendidos. Veja a seguir as resoluções e motivos comuns:

-   **Um filtro de escopo foi configurado** **que está filtrando usuário Olá com base em um valor de atributo**. Para obter mais informações sobre filtros de escopo, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **usuário de saudação é "não efetivamente intitulado".** Se você vir essa mensagem de erro específica, é porque não há um problema com o registro de atribuição do usuário Olá armazenado no AD do Azure. toofix esse problema, cancele sua atribuição Olá usuário (ou grupo) do aplicativo hello e novamente atribuí-lo novamente. Para obter mais informações sobre atribuição, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Um atributo obrigatório está ausente ou não está preenchido para um usuário.** Tooconsider uma coisa importante quando a configuração de provisionamento ser tooreview e configurar mapeamentos de atributo hello e fluxos de trabalho que definem quais fluxo de propriedades de usuário (ou grupo) do aplicativo de toohello do AD do Azure. Isso inclui a configuração hello "correspondência da propriedade" ser toouniquely usada identificar e corresponder usuários/grupos entre sistemas Olá dois. Para obter mais informações sobre esse processo importante, consulte <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Mapeamentos de grupos de atributos:** provisionamento de saudação grupo detalhes de nome e grupo, em membros de toohello de adição, se houver suporte para alguns aplicativos. Você pode habilitar ou desabilitar essa funcionalidade habilitando ou desabilitando Olá **mapeamento** para objetos de grupo mostrados no hello **provisionamento** guia. Se grupos de provisionamento está habilitado, certifique-se de que tooreview Olá atributo mapeamentos tooensure um campo apropriado está sendo usado para hello "correspondência de ID". Isso pode ser Olá exibição nome ou alias de email), como Olá grupo e seus membros não ser provisionado se hello a propriedade correspondente está vazio ou não preenchido para um grupo no AD do Azure.

#<a name="next-steps"></a>Próximas etapas
[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md)
