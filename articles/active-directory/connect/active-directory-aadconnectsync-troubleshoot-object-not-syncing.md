---
title: "aaaTroubleshoot um objeto que não está sincronizando tooAzure AD | Microsoft Docs"
description: "Solucionar problemas de por que um objeto não está sincronizando tooAzure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Solucionar problemas de um objeto que não está sincronizando tooAzure AD

Se um objeto não está sincronizando como esperado tooAzure AD, ele pode ser devido a vários motivos. Se você recebeu uma mensagem de erro do AD do Azure ou consulte o erro Olá no Azure AD Connect Health, em seguida, ler [solucionar problemas de erros de exportação](active-directory-aadconnect-troubleshoot-sync-errors.md) em vez disso. Mas se você estiver solucionando um problema em que o objeto de Olá não está no AD do Azure, em seguida, este tópico é para você. Descreve como sincronizar a toofind erros no componente de local de saudação do Azure AD Connect.

erros de saudação toofind, você vai toolook em alguns locais diferentes da saudação ordem a seguir:

1. Olá [logs de operação](#operations) para localizar os erros identificados pelo mecanismo de sincronização de saudação durante a importação e sincronização.
2. Olá [espaço conector](#connector-space-object-properties) para localizar objetos ausentes e erros de sincronização.
3. Olá [metaverso](#metaverse-object-properties) para localizar problemas relacionados a dados.

Inicie o [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) antes de começar estas etapas.

## <a name="operations"></a>Operações
Guia de operações Olá Olá Synchronization Service Manager é onde você deve iniciar a solução de problemas. Guia de operações de saudação mostra os resultados de saudação de operações mais recentes hello.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

metade superior Olá mostra todas as execuções em ordem crônicos. Por padrão, o log de operações Olá mantém informações sobre Olá últimos sete dias, mas essa configuração pode ser alterada com hello [Agendador](active-directory-aadconnectsync-feature-scheduler.md). Você deseja toolook para qualquer execução que não mostra um status de êxito. Você pode alterar Olá classificação clicando em cabeçalhos de saudação.

Olá **Status** coluna informações mais importantes hello e mostra Olá problema mais sério para uma execução. Aqui está um resumo de status mais comuns de saudação em ordem de prioridade tooinvestigate (onde * indicar várias cadeias de caracteres de erro possível).

| Status | Comentário |
| --- | --- |
| stopped-* |não foi possível concluir a saudação executar. Por exemplo, se hello sistema remoto está inoperante e não pode ser contatado. |
| stopped-error-limit |Há mais de 5.000 erros. Olá executar automaticamente foi interrompido devido a toohello grande número de erros. |
| completed-\*-errors |Olá execução foi concluída, mas há erros (menos de 5.000) que devem ser investigados. |
| completed-\*-warnings |Olá executar concluída, mas alguns dados não estão em estado de saudação esperado. Se houver erros, geralmente, essa mensagem indicará apenas um sintoma. Até que tenha resolvido os erros, você não deverá investigar os avisos. |
| sucesso |Nenhum problema. |

Quando você seleciona uma linha, inferior Olá atualiza tooshow detalhes de saudação do que executar. toohello à extrema esquerda da parte inferior da saudação, talvez seja necessário dizer uma lista **etapa #**. Essa lista só será exibida se você tiver vários domínios na floresta, em que cada domínio é representado por uma etapa. o nome de domínio Olá pode ser encontrado sob o título de saudação **partição**. Em **estatísticas de sincronização**, você pode encontrar mais informações sobre o número de saudação de alterações que foram processadas. Você pode clicar em Olá links tooget uma lista de objetos de saudação alterado. Se você tiver objetos com erros, eles aparecerão em **erros de sincronização**.

### <a name="troubleshoot-errors-in-operations-tab"></a>Solucionar problemas de erros na guia Operações
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Quando você encontrar erros, ambos objeto Olá no erro e o próprio erro Olá são links que fornecem mais informações.

Iniciar clicando em cadeia de caracteres de erro hello (**disparado por sincronização-regra-erro-função** na imagem de saudação). Primeiro, você tem uma visão geral do objeto hello. toosee Olá erro real, clique botão Olá **rastreamento de pilha**. Este rastreamento fornece informações de nível de depuração para o erro de saudação.

Clique em Olá **informações de pilha de chamadas** caixa, escolha **Selecionar tudo**, e **cópia**. Você pode copiar pilha hello e examine o erro de saudação em seu editor favorito, como o bloco de notas.

* Se o erro de saudação do **SyncRulesEngine**, e informações de pilha de chamada hello primeiro tem uma lista de todos os atributos no objeto de saudação. Role para baixo até ver título Olá **InnerException = >**.  
  ![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  linha de saudação depois mostra Olá erro. Na Figura Olá acima, erro de saudação é de um Fabrikam de regra de sincronização personalizado criado.

Se o erro de saudação em si não fornecem informações suficientes, é toolook de tempo em dados de saudação em si. Clique Olá link com o identificador de objeto hello e continuar com a solução Olá [objeto importado de espaço do conector](#cs-import).

## <a name="connector-space-object-properties"></a>Propriedades do objeto do espaço conector
Se você não tem qualquer erro encontrado no hello [operações](#operations) guia, Olá próxima etapa é o objeto de espaço do conector toofollow saudação do Active Directory, toohello metaverso e tooAzure AD. Nesse caminho, você deve encontrar onde está o problema de saudação.

### <a name="search-for-an-object-in-hello-cs"></a>Procurar um objeto no hello CS

Em **Synchronization Service Manager**, clique em **conectores**, selecione Olá conector do Active Directory, e **espaço do conector de pesquisa**.

Em **escopo**, selecione **RDN** (quando você quiser toosearch no atributo CN Olá) ou **DN ou âncora** (quando você quiser toosearch no atributo de distinguishedName Olá). Insira um valor e clique em **Pesquisar**.  
![Pesquisa do Espaço Conector](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Se você não encontrar o objeto Olá você está procurando, em seguida, ele pode ter sido filtrado com [filtragem baseada em domínio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) ou [filtragem baseada em unidade Organizacional](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Saudação de leitura [configurar a filtragem de](active-directory-aadconnectsync-configure-filtering.md) tooverify tópico que Olá filtragem está configurado como esperado.

Outra pesquisa útil é tooselect Olá conector AD do Azure, na **escopo** selecione **importação pendente**e selecione hello **adicionar** caixa de seleção. Essa pesquisa fornece todos os objetos sincronizados no Azure AD que não podem ser associados a um objeto local.  
![Órfão de pesquisa do Espaço Conector](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Esses objetos foram criados por outro mecanismo de sincronização ou por um mecanismo de sincronização com outra configuração de filtragem. Essa exibição é uma lista de objetos **órfãos** que não são mais gerenciados. Examine esta lista e Considere remover esses objetos usando Olá [PowerShell do Azure AD](http://aka.ms/aadposh) cmdlets.

### <a name="cs-import"></a>Importação do CS
Quando você abre um objeto do cs, há várias guias na parte superior da saudação. Olá **importar** guia mostra dados de saudação preparado após uma importação.  
![Objeto do CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Olá **valor antigo** mostra o que é armazenado em conectar e Olá **novo valor** que foi recebido do sistema de origem hello e ainda não foram aplicado. Se houver um erro no objeto hello, as alterações não são processadas.

**Erro**  
![Objeto do CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Olá **erro de sincronização** guia só é visível se houver um problema com o objeto de saudação. Para obter mais informações, consulte [Solucionar problemas de erros de sincronização](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Linhagem do CS
Guia de linhagem Olá mostra como o objeto de espaço do conector de saudação é objeto do metaverso toohello relacionados. Você pode ver quando Olá conector última importado de uma alteração de Olá sistema conectado e quais dados toopopulate regras aplicadas Olá metaverso.  
![Linhagem do CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
Em Olá **ação** coluna, você pode ver houver **entrada** regra de sincronização com ação Olá **provisionar**. Que indica que desde que este objeto de espaço do conector estiver presente, o objeto de metaverso Olá permaneça. Se Olá de lista de regras de sincronização em vez disso, mostra uma regra de sincronização com direção **saída** e **provisionar**, ele indica que esse objeto é excluído quando o objeto do metaverso Olá é excluído.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Você também pode ver no hello **PasswordSync** coluna Olá espaço do conector de entrada pode contribuir senha de toohello alterações como uma regra de sincronização tem valor Olá **True**. Essa senha é enviada tooAzure AD por meio de regras de saída hello.

Na guia de linhagem Olá, é possível obter toohello metaverso clicando [propriedades de objeto do metaverso](#mv-attributes).

Na parte inferior da saudação de todas as guias são dois botões: **visualização** e **Log**.

### <a name="preview"></a>Visualização
página de visualização de saudação é usado toosynchronize um único objeto. É útil se você estiver solucionando problemas de algumas regras de sincronização personalizadas e deseja toosee Olá efeito uma alteração em um único objeto. É possível selecionar entre **Sincronização completa** e **Sincronização delta**. Você também pode selecionar entre **gerar visualização**, que mantém apenas Olá alteração na memória, e **visualização confirmar**, qual atualizado Olá metaverso e estágios todos os espaços de conector tootarget é alterado.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Você pode inspecionar o objeto hello e qual regra é aplicada para um fluxo de atributo específico.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Registro
página de registro de saudação é histórico e status de sincronização de senha de saudação toosee usado. Para obter mais informações, consulte [Solucionar problemas de sincronização de senha](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Propriedades do objeto do metaverso
É geralmente melhor toostart pesquisa de origem de saudação do Active Directory [espaço conector](#connector-space). Mas você também pode iniciar a pesquisa de metaverso hello.

### <a name="search-for-an-object-in-hello-mv"></a>Pesquisa de um objeto no hello MV
No **Synchronization Service Manager**, clique em **Pesquisa de Metaverso**. Crie uma consulta que você sabe que localiza Olá usuário. É possível pesquisar atributos comuns, como accountName (sAMAccountName) e userPrincipalName. Para obter mais informações, consulte [Pesquisa de metaverso](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

Em Olá **resultados da pesquisa** janela, clique em objeto hello.

Se não encontrar o objeto de Olá, em seguida, ele ainda não alcançou Olá metaverso. Continue toosearch para objeto Olá Olá do Active Directory [espaço conector](#connector-space-object-properties). Pode haver um erro de sincronização que está bloqueando o objeto de saudação do metaverso próximos de toohello ou pode haver um filtro aplicado.

### <a name="mv-attributes"></a>Atributos do MV
Na guia de atributos hello, você pode ver os valores hello e quais conector a contribuição.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Se um objeto não está sincronizando, então, ser Olá seguintes atributos no metaverso hello:
- Atributo Olá **cloudFiltered** apresentar e defina muito**true**? Se ele é, foram filtrado de acordo com o toohello etapas [filtragem baseada em atributo](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Atributo Olá **sourceAnchor** presente? Caso contrário, você tem uma topologia de floresta de conta-recurso? Se um objeto é identificado como uma caixa de correio vinculada (atributo Olá **msExchRecipientTypeDetails** tem Olá valor 2), e em seguida, Olá sourceAnchor vem por floresta Olá com uma conta do Active Directory habilitada. Certifique-se de conta principal Olá foi importada e sincronizada corretamente. conta principal Olá deve estar listada em Olá [conectores](#mv-connectors) para objeto hello.

### <a name="mv-connectors"></a>Conectores do MV
Guia de conectores Olá mostra todos os espaços de conector que têm uma representação de objeto hello.  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
É necessário ter um conector para:

- Cada usuário de saudação de floresta do Active Directory é representado no. Essa representação pode incluir os objetos foreignSecurityPrincipals e Contact.
- Um conector no Azure AD.

Se você não tiver Olá conector tooAzure AD, em seguida, ler [atributos de MV](#MV-attributes) tooverify critérios de saudação do que está sendo provisionado tooAzure AD.

Este guia também permite que você toonavigate toohello [o objeto de espaço do conector](#connector-space-object-properties). Selecione uma linha e clique em **Propriedades**.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
