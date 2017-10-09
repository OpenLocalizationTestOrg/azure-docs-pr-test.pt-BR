---
title: aaaOptimize seu ambiente do Active Directory com o Azure Log Analytics | Microsoft Docs
description: "Você pode usar o hello avaliação de diretório ativo tooassess solução Olá risco e a integridade de seus ambientes de servidor em um intervalo regular."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Otimizar seu ambiente do Active Directory com hello solução de avaliação do Active Directory na análise de Log

![Símbolo da Avaliação do AD](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

Você pode usar o hello avaliação de diretório ativo tooassess solução Olá risco e a integridade de seus ambientes de servidor em um intervalo regular. Este artigo ajuda você a instalar e usar a solução de saudação para que você pode executar ações corretivas para problemas potenciais.

Essa solução fornece uma lista priorizada de infraestrutura de servidor implantado recomendações tooyour específico. Olá recomendações são categorizadas em foco quatro áreas, que ajuda você a rapidamente entender Olá risco e execute a ação.

recomendações de saudação baseiam-se no conhecimento do hello e experiência obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. Cada recomendação fornece diretrizes sobre por que uma questão pode ser relevante tooyou e como o tooimplement Olá alterações sugeridas.

Você pode escolher áreas de foco que são mais importante organização de tooyour e acompanham seu progresso em direção a um ambiente íntegro e livre de risco.

Depois que você adicionou a solução hello e uma avaliação é concluído, resumo informações para as áreas de foco são mostradas na Olá **avaliação do AD** painel de infraestrutura de saudação em seu ambiente. Olá seções a seguir descrevem como toouse Olá informações sobre Olá **avaliação do AD** painel, onde você pode exibir e executar as ações recomendadas para sua infraestrutura de servidor do Active Directory.

![imagem do bloco de Avaliação do SQL](./media/log-analytics-ad-assessment/ad-tile.png)

![imagem do painel de avaliação do SQL](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar soluções de saudação.

* Agentes devem ser instalados em controladores de domínio que são membros de saudação domínio toobe avaliada.
* Olá avaliação de diretório ativo solução requer uma versão com suporte do .NET Framework 4 (4.5.2 ou superior) instalado em cada computador que tenha um agente do OMS.
* Adicionar espaço de trabalho do hello avaliação do Active Directory solução tooyour OMS do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).  Não é necessária nenhuma configuração.

  > [!NOTE]
  > Depois que você adicionou a solução hello, arquivo AdvisorAssessment.exe de saudação é adicionado tooservers com agentes. Dados de configuração lidos e, em seguida, enviados toohello serviço do OMS na nuvem Olá para processamento. Lógica é aplicada toohello recebida dados e o serviço de nuvem Olá registra dados de saudação.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Detalhes de coleta de dados da Avaliação do Active Directory

Avaliação do Active Directory coleta dados de saudação usando Olá agentes que você habilitou as origens a seguir:

- Coletores de registro
- Coletores de LDAP
- .NET Framework
- Coletores de log de eventos
- ADSI (Interfaces de Serviço do Active Directory)
- Windows PowerShell
- Coletores de dados de arquivo
- WMI (Instrumentação de Gerenciamento do Windows)
- API de ferramentas DCDIAG
- API do NTFRS (Serviço de Replicação de Arquivos)
- Código em C# personalizado


Olá tabela a seguir mostra os métodos de coleta de dados para os agentes se Operations Manager (SCOM) é necessária e como geralmente os dados são coletados por um agente.

| plataforma | Agente direto | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |

## <a name="understanding-how-recommendations-are-prioritized"></a>Compreendendo como as recomendações são priorizadas
Cada recomendação feita recebe um valor de ponderação que identifica Olá a importância relativa da recomendação hello. Somente recomendações mais importantes de saudação 10 são mostradas.

### <a name="how-weights-are-calculated"></a>Como os pesos são calculados
Os pesos são valores agregados com base em três fatores principais:

* Olá *probabilidade* um problema identificado causa problemas. Uma probabilidade mais alta é igual a pontuação geral maior de tooa de recomendação de saudação.
* Olá *impacto* do problema de saudação na sua organização se ela causar um problema. Um impacto maior é igual a pontuação geral maior de tooa de recomendação de saudação.
* Olá *esforço* necessário tooimplement recomendação de saudação. Um esforço maior é igual a pontuação geral menor de tooa de recomendação de saudação.

Olá peso de cada recomendação é expressa como um percentual da pontuação total da saudação disponíveis para cada área de foco. Por exemplo, se uma recomendação na hello segurança e área de foco de conformidade tiver uma pontuação de 5%, implementar essa recomendação aumentará a segurança e conformidade pontuação geral por 5%.

### <a name="focus-areas"></a>Áreas de foco
**Segurança e conformidade** - essa área de foco mostra recomendações para possíveis ameaças de segurança e violações, políticas corporativas, bem como os requisitos de conformidade técnica, legal e regulatória.

**Disponibilidade e continuidade dos negócios** - essa área de foco mostra as recomendações para a disponibilidade de serviço, resiliência de sua infraestrutura e proteção dos negócios.

**Desempenho e escalabilidade** -essa área de foco mostra recomendações toohelp da sua organização crescer de infraestrutura de TI, certifique-se de que seu ambiente de TI atende aos requisitos de desempenho atuais e é capaz de toorespond toochanging precisa de infraestrutura.

**Atualização, implantação e migração** – essa área de foco mostra recomendações toohelp atualizar, migrar e implantar a infraestrutura existente do Active Directory tooyour.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Você deve visar tooscore 100% em cada área de foco?
Não necessariamente. recomendações de saudação baseiam-se no conhecimento do hello e experiências obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. No entanto, nenhuma infraestrutura de servidor é Olá mesmo e recomendações específicas podem ser mais ou menos relevante tooyou. Por exemplo, algumas recomendações de segurança podem ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet. Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem relatórios e coleta de dados ad hoc de baixa prioridade. Problemas de empresas maduras tooa importante podem ser menos importante inicialização de tooa. Você pode desejar tooidentify quais áreas de foco são suas prioridades e depois examinar como suas pontuações mudam ao longo do tempo.

Cada recomendação inclui diretrizes sobre sua importância. Você deve usar essa orientação tooevaluate se implementar Olá recomendação é adequada para você, considerando a natureza Olá seu IT services e hello necessidades de negócios da sua organização.

## <a name="use-assessment-focus-area-recommendations"></a>Use as recomendações de área de foco de avaliação
Antes de usar uma solução de avaliação no OMS, você deve ter a solução Olá instalada. tooread mais informações sobre a instalação de soluções, consulte [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Após a instalação, você pode exibir o resumo de saudação das recomendações usando o bloco de avaliação de saudação na página de visão geral de saudação do OMS.

Saudação de exibição resumida avaliações de conformidade para sua infraestrutura e detalhada das recomendações.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendações de tooview para um foco área e take corretivas
1. Em Olá **visão geral** , clique em Olá **avaliação** lado a lado para sua infraestrutura de servidor.
2. Em Olá **avaliação** página, examine as informações de resumo de saudação em uma saudação foco das folhas da área e, em seguida, clique em um tooview recomendações para a área de foco.
3. Em qualquer uma das páginas da área de foco hello, você pode exibir as recomendações de saudação priorizada para seu ambiente. Clique em uma recomendação em **objetos afetados** tooview detalhes sobre por que Olá recomendação foi feita.  
    ![imagem das recomendações da Avaliação](./media/log-analytics-ad-assessment/ad-focus.png)
4. É possível executar as ações corretivas sugeridas em **Ações Sugeridas**. Quando o item de saudação tiver sido resolvido, registros avaliações posteriores que as ações recomendadas foram executados e sua pontuação de conformidade aumentará. Os itens corrigido aparecem como **Objetos Passados**.

## <a name="ignore-recommendations"></a>Ignorar as recomendações
Se tiver recomendações que você deseja tooignore, você pode criar um arquivo de texto que o OMS usará tooprevent as recomendações apareçam nos resultados da avaliação.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendações de tooidentify que você irá ignorar
1. Entre no espaço de trabalho tooyour e abra a pesquisa de Log. Use Olá consulta toolist recomendações que falharam para computadores em seu ambiente a seguir.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Aqui está uma consulta de pesquisa de Log de saudação de captura de tela mostrando: ![falha recomendações](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Escolha as recomendações que você deseja tooignore. Você usará os valores hello para RecommendationId no próximo procedimento de saudação.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e usar um arquivo de texto IgnoreRecommendations.txt
1. Crie um arquivo chamado IgnoreRecommendations.txt.
2. Cole ou digite cada RecommendationId de cada recomendação que você deseja tooignore de análise de Log em uma linha separada e salve e feche o arquivo hello.
3. Arquivo hello PUT na Olá pasta a seguir em cada computador onde você deseja que as recomendações de tooignore do OMS.
   * Em computadores com hello Microsoft Monitoring Agent (conectado diretamente ou por meio do Operations Manager) - *SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * No servidor de gerenciamento do Operations Manager Olá - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que as recomendações são ignoradas
Depois de ser executado Olá próxima avaliação agendada, por padrão a cada 7 dias, Olá especificado recomendações são marcadas *ignorado* e não serão exibidos no painel de avaliação de saudação.

1. Você pode usar o hello toolist de consultas de pesquisa de Log a seguir todas as recomendações de saudação ignorada.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Se você decidir posteriormente que deseja toosee ignorado recomendações, remova os arquivos IgnoreRecommendations.txt ou remova as RecommendationIDs deles.

## <a name="ad-assessment-solutions-faq"></a>Perguntas frequentes sobre soluções da Avaliação do AD
*Com que frequência uma avaliação é executada?*

* Olá avaliação é executada a cada 7 dias.

*Há um tooconfigure de maneira com que frequência Olá avaliação é executada?*

* Não no momento.

*Se outro servidor for descoberto depois que eu adicionar uma solução de avaliação, ele será avaliado?*

* Sim, assim que for descoberto, ele é avaliado a partir de então a cada sete dias.

*Se um servidor for encerrado, quando ele será removido da avaliação de Olá?*

* Se um servidor não enviar dados por três semanas, ele será removido.

*O que é o nome de saudação do processo Olá Olá a coleta de dados?*

* AdvisorAssessment.exe

*Quanto tempo leva para toobe dados coletado?*

* coleta de dados reais de saudação no servidor de saudação leva aproximadamente 1 hora. Pode levar mais tempo em servidores que têm um grande número de servidores do Active Directory.

*Há uma maneira tooconfigure quando os dados são coletados?*

* Não no momento.

*Por que apenas Olá 10 principais recomendações são exibidas?*

* Em vez de apresentar uma lista exaustiva de tarefas, é recomendável que você se concentre em tratar as recomendações de saudação priorizada primeiro. Depois de tratar dessas recomendações, recomendações adicionais serão disponibilizadas. Se você preferir a lista detalhada de saudação toosee, você pode exibir todas as recomendações usando a pesquisa de Log.

*Há uma maneira tooignore uma recomendação?*

* Sim, confira a seção [Ignorar recomendações](#ignore-recommendations) acima.

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de avaliação do AD e as recomendações.
