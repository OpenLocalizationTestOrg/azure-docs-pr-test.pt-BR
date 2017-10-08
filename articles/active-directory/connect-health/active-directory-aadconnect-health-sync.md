---
title: "aaaUsing do Azure AD Connect Health com sincronização | Microsoft Docs"
description: "Esta é a página de integridade de conexão de saudação do AD do Azure que discutiremos como toomonitor do Azure AD Connect a sincronização."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Monitorar a sincronização do Azure AD Connect com o Azure AD Connect Health
Olá documentação a seguir é toomonitoring específico do Azure AD Connect (sincronização) com o Azure AD Connect Health.  Para saber mais sobre como monitorar o AD FS com o Azure AD Connect Health, consulte [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md). Além disso, para obter informações sobre como monitorar os Serviços de Domínio do Active Directory com o Azure AD Connect Health, confira [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md).

![Azure AD Connect Health para sincronização](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alertas do Azure AD Connect Health para sincronização
Alertas de integridade de conectar-se de saudação do AD do Azure para a seção de sincronização fornece que Olá lista de alertas ativos. Cada alerta inclui informações relevantes, etapas de resolução e documentação de toorelated links. Ao selecionar um alerta ativo ou resolvido, você verá uma nova folha com informações adicionais, bem como etapas a serem seguidas tooresolve Olá alerta e documentação de tooadditional links. Você também pode exibir dados históricos sobre alertas que foram resolvidos no hello anterior.

Ao selecionar um alerta que será fornecido com informações adicionais, bem como etapas você pode colocar links e alerta de saudação tooresolve tooadditional documentação.

![Erro de sincronização do Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Avaliação limitada de alertas
Se o Azure AD Connect não estiver usando a configuração padrão de saudação (por exemplo, se a filtragem de atributos é alterado de configuração personalizada de tooa Olá de configuração padrão), em seguida, agente de integridade de conexão de saudação do AD do Azure não carregará Olá erro eventos relacionados tooAzure Conexão do AD.

Isso limita a avaliação de saudação de alertas pelo serviço de saudação. Seria verá um banner que indica essa condição em Olá Portal do Azure em seu serviço.

![Azure AD Connect Health para sincronização](./media/active-directory-aadconnect-health-sync/banner.png)

Você pode alterar isso clicando em "Configurações" e permitindo que tooupload de agente do Azure AD Connect Health todos os logs de erro.

![Azure AD Connect Health para sincronização](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Detalhes da sincronização
Administradores frequentemente querem tooknow sobre Olá tempo toosync alterações tooAzure AD e quantidade de saudação de mudanças que ocorrem. Este recurso fornece uma maneira fácil toovisualize isso usando Olá abaixo gráficos:   

* Latência de operações de sincronização
* Tendência de alteração de objeto

### <a name="sync-latency"></a>Latência de Sincronização
Este recurso fornece uma tendência de gráfica de latência de saudação operações de sincronização (importar, exportar, etc.) para conectores.  Isso fornece uma rápida e toounderstand de maneira fácil não só Olá latência de suas operações (maiores se você tiver um grande conjunto de alterações ocorridas), mas também anomalias de toodetect uma forma da latência de saudação que pode exigir mais investigação.

![Latência de Sincronização](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Por padrão, somente a latência Olá da operação de saudação 'Export' para o conector do AD do Azure Olá é mostrada.  toosee mais operações no conector hello ou operações tooview em outros conectores, clique no gráfico de hello, selecione Editar gráfico ou clique no botão de "Editar gráfico de latência" hello e escolha operação específica hello e conectores.

### <a name="sync-object-changes"></a>Alterações de objeto de sincronização
Este recurso fornece uma tendência de gráfica do número de saudação de alterações que estão sendo avaliados e exportados tooAzure AD.  Hoje, tentando toogather essas informações de logs de sincronização de saudação são difícil.  Olá gráfico fornece, não apenas uma maneira simples de monitoramento do número de saudação de alterações que estão ocorrendo no seu ambiente, mas também uma exibição visual de falhas de saudação que estão ocorrendo.

![Latência de Sincronização](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Relatório de erros de sincronização no nível do objeto (Visualização)
Esse recurso fornece um relatório sobre os erros de sincronização que podem ocorrer quando os dados de identidade são sincronizados entre o Windows Server AD e o Azure AD usando o Azure AD Connect.

* relatório de saudação abrange erros registrados pelo cliente de sincronização de saudação (Azure AD Connect versão 1.1.281.0 ou superior)
* Ele inclui erros Olá que ocorreram na última operação de sincronização Olá no mecanismo de sincronização de saudação. ("Exportar" hello conector AD do Azure.)
* Agente de integridade de conexão do AD do Azure para sincronização deve ter pontos de extremidade de toohello necessária conectividade de saída para dados mais recentes do Olá Olá relatório tooinclude.
* Olá relatório **atualizada a cada 30 minutos** usando dados Olá carregado pelo agente do Azure AD Connect Health para sincronização. Ele fornece Olá funcionalidades principais a seguir

  * Categorização de erros
  * Lista de objetos com erro por categoria
  * Todos os dados de saudação sobre erros de saudação em um só lugar
  * Lado a lado comparação lado dos objetos com erro devido a conflito de tooa
  * Baixar o relatório de erros do hello como um CVS (em breve)

### <a name="categorization-of-errors"></a>Categorização de erros
relatório de saudação categoriza os erros de sincronização existente Olá no hello categorias a seguir:

| Categoria | Descrição |
| --- | --- |
| Duplicar atributo |Erros quando o Azure AD Connect tenta criar ou atualizar objetos com valores duplicados de um ou mais atributos no Azure AD que deve ser exclusivo em um Locatário, como proxyAddresses, UserPrincipalName. |
| Incompatibilidade de dados |Erros quando Olá soft-match falha toomatch objetos que resultam em erros de sincronização. |
| Falha na validação de dados |Erros devido a dados de tooinvalid, como caracteres sem suporte em atributos importantes, como UserPrincipalName, formatar erros que falharem na validação antes de serem gravados no AD do Azure. |
| Atributo grande |Erros quando um ou mais atributos são maiores do que Olá permitido tamanho, comprimento ou contagem. |
| outro |Todos os outros erros que não se ajustarem Olá acima das categorias. Com base nos comentários, essa categoria será dividida em subcategorias. |

![Resumo do relatório de erro de sincronização](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Categorias de relatório de erro de sincronização](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lista de objetos com erro por categoria
Busca detalhada em cada categoria fornecerá a lista de saudação de objetos que têm o erro Olá nessa categoria.
![Lista de relatórios de erros de sincronização](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Detalhes do Erro
Dados a seguir está disponível no hello detalhadas de exibição para cada erro

* Identificadores de saudação *objeto AD* envolvidos
* Identificadores de saudação *objeto do AD do Azure* envolvidos (conforme aplicável)
* Descrição do erro e como toofix
* Artigos relacionados

![Detalhes do relatório de erro de sincronização](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Baixar o relatório de erro de saudação como CSV
Selecionando hello "exporte" você pode baixar um arquivo CSV com todos os detalhes de saudação sobre todos os erros de saudação do botão.

## <a name="related-links"></a>Links relacionados
* [Solucionando problemas de erros durante a sincronização](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Duplicar a resiliência do atributo](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)