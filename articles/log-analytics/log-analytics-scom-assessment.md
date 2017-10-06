---
title: aaaOptimize seu ambiente do System Center Operations Manager com o Azure Log Analytics | Microsoft Docs
description: "Você pode usar o hello Center Operations Manager avaliação do sistema de solução tooassess Olá risco e a integridade de seus ambientes de servidor em um intervalo regular."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Otimizar seu ambiente com hello solução de avaliação de Gerenciador de operações do System Center (visualização)

![Símbolo do Avaliação do System Center Operations Manager](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Você pode usar o hello Center Operations Manager avaliação do sistema de solução tooassess Olá risco e a integridade de seus ambientes de servidor do System Center Operations Manager em um intervalo regular. Este artigo ajuda você a instalar, configurar e usar a solução de saudação para que você pode executar ações corretivas para problemas potenciais.

Essa solução fornece uma lista priorizada de infraestrutura de servidor implantado recomendações tooyour específico. Olá recomendações são categorizadas em foco quatro áreas, que ajuda você a rapidamente entender Olá risco e tomar uma ação corretiva.

recomendações Olá baseiam-se no conhecimento hello e experiência obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. Cada recomendação fornece diretrizes sobre por que uma questão pode ser relevante tooyou e como o tooimplement Olá alterações sugeridas.

Você pode escolher áreas de foco que são mais importante organização de tooyour e acompanham seu progresso em direção a um ambiente íntegro e livre de risco.

Depois que você adicionou a solução hello e uma avaliação é concluído, resumo informações para as áreas de foco são mostradas na Olá **System Center Operations Manager avaliação** painel para sua infraestrutura. Olá seções a seguir descrevem como toouse Olá informações sobre Olá **System Center Operations Manager avaliação** painel, onde você pode exibir e executar as ações recomendadas para sua infraestrutura do SCOM.

![Bloco de solução do System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![Painel do System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá

solução de saudação funciona com o sistema do Microsoft Operations Manager 2012 R2 e 2012 SP1.

Use Olá tooinstall informações a seguir e configurar a solução de saudação.

 - Antes de usar uma solução de avaliação no OMS, você deve ter a solução Olá instalada. Instalar a solução de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) ou seguindo as instruções de saudação em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

 - Depois de adicionar espaço de trabalho do hello solução toohello, bloco de avaliação de Gerenciador de operações do System Center de saudação no painel de saudação exibe mensagens do hello configuração adicional necessária. Clique no bloco de saudação e siga as etapas de configuração Olá mencionadas na página Olá

 ![Bloco do painel do System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Configuração de saudação do System Center Operations Manager pode ser feita por meio de script hello seguindo etapas Olá mencionadas na página de configuração de saudação de solução de saudação do OMS.

 Em vez disso, avaliação de saudação tooconfigure por meio do Console do SCOM, siga Olá abaixo as etapas em Olá mesma ordem
1. [Definir Olá executar como conta para o System Center Operations Manager avaliação](#operations-manager-run-as-accounts-for-oms)  
2. [Configurar regra de avaliação de Gerenciador de operações do System Center Olá](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Detalhes da coleta de dados de avaliação do System Center Operations Manager

saudação de avaliação do System Center Operations Manager coleta dados do WMI, dados de registro, dados de log de eventos, dados do Operations Manager por meio do Windows PowerShell, consultas SQL, o coletor de informações de arquivo usando o servidor de saudação que você tiver habilitado.

Olá tabela a seguir mostra os métodos de coleta de dados para o System Center Operations Manager avaliação e a frequência com dados são coletados por um agente.

| plataforma | Agente direto | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | sete dias |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Contas Executar como do Operations Manager para OMS

Compilações OMS em pacotes de gerenciamento para cargas de trabalho tooprovide serviços de valor agregado. Cada carga de trabalho requer pacotes de gerenciamento de toorun de privilégios de carga de trabalho específica em um contexto de segurança diferente, como uma conta de domínio. Configure um executar como do Operations Manager conta tooprovide informações de credenciais.

Use Olá tooset hello conta executar como do Operations Manager para System Center Operations Manager avaliação de informações a seguir.

### <a name="set-hello-run-as-account"></a>Saudação de conjunto de conta executar como

1. No Console do Operations Manager do hello, vá toohello **administração** guia.
2. Em Olá **configuração Executar como**, clique em **contas**.
3. Crie hello conta executar como, por meio de saudação Assistente de criação de uma conta do Windows a seguir. Olá conta toouse é hello um identificado e ter todos os pré-requisitos de saudação abaixo:

    >[!NOTE]
    Olá conta executar como deve atender aos seguintes requisitos:
    - Um membro da conta de domínio do grupo de administradores local Olá em todos os servidores no ambiente de saudação (todas as operações de Gerenciador de funções - servidor de gerenciamento, banco de dados do MOM, Data Warehouse, relatórios, Console Web, Gateway)
    - Função de administrador do Gerenciador de operação Olá grupo de gerenciamento que está sendo avaliado
    - Executar Olá [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant conta de toohello permissões granulares na instância do SQL usada pelo Operations Manager.
      Observação: Se essa conta tem direitos sysadmin já, ignore a execução do script hello.

4. Em **Segurança da Distribuição**, selecione **Mais seguro**.
5. Especifique o servidor de gerenciamento de saudação onde a conta de saudação é distribuída.
3. Voltar toohello configuração Executar como e clique em **perfis**.
4. Pesquise Olá *perfil de avaliação do SCOM*.
5. nome do perfil Olá deve ser: *Microsoft System Center Advisor SCOM avaliação perfil executar como*.
6. Clique com botão direito e atualize suas propriedades e adicionar Olá recentemente criado a conta executar como criada na etapa 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL script toogrant permissões granulares toohello conta executar como

Execute Olá SQL script toogrant necessárias permissões toohello conta executar como na instância do SQL Olá usada pelo Operations Manager a seguir.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Configurar regra de avaliação Olá

Olá Center Operations Manager avaliação do sistema de pacote de gerenciamento da solução inclui uma regra denominada *Microsoft System Center Advisor SCOM avaliação executar avaliação regra*. Essa regra é responsável pela execução da avaliação de saudação. tooenable Olá regra e configurar a frequência de hello, use Olá procedimentos abaixo.

Por padrão, a saudação Microsoft System Center Advisor SCOM avaliação executar avaliação regra está desabilitada. avaliação de saudação toorun, você deve habilitar regra Olá em um servidor de gerenciamento. Olá Use as etapas a seguir.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Habilitar a regra de saudação de um servidor de gerenciamento específico

1. Em Olá **criação** espaço de trabalho do console do Operations Manager hello, pesquise a regra de saudação *Microsoft System Center Advisor SCOM avaliação executar avaliação regra* em Olá **regras** painel.
2. Nos resultados da pesquisa Olá Olá select que inclui o texto de saudação *tipo: servidor de gerenciamento*.
3. Clique em regra hello e, em seguida, clique em **substitui** > **para um objeto específico da classe: servidor de gerenciamento**.
4.  Na lista de servidores de gerenciamento disponíveis hello, selecione o servidor de gerenciamento de saudação onde executar regra hello.
5.  Certifique-se de que você altere o valor de substituição muito**True** para Olá **habilitado** o valor do parâmetro.  
    ![parâmetro de substituição](./media/log-analytics-scom-assessment/rule.png)

Ainda nessa janela, configure frequência Olá Olá executado usando o procedimento a seguir hello.

#### <a name="configure-hello-run-frequency"></a>Configurar a frequência de saudação executar

avaliação de saudação é intervalo de padrão de saudação configurado toorun cada 10.080 minutos (ou sete dias). Você pode substituir o valor mínimo do hello valor tooa de 1440 minutos (ou um dia). valor de saudação representa o intervalo de tempo mínimo Olá necessário entre as execuções sucessivas de avaliação. intervalo de saudação toooverride, use Olá etapas abaixo.

1. Em Olá **criação** espaço de trabalho do console do Operations Manager hello, pesquise a regra de saudação *Microsoft System Center Advisor SCOM avaliação executar avaliação regra* em Olá **regras** painel.
2. Nos resultados da pesquisa Olá Olá select que inclui o texto de saudação *tipo: servidor de gerenciamento*.
3. Clique em regra hello e, em seguida, clique em **Olá de substituição de regra** > **para todos os objetos da classe: servidor de gerenciamento**.
4. Saudação de alteração **intervalo** tooyour de valor de parâmetro desejado o valor do intervalo. O exemplo hello abaixo, Olá valor é definido too1440 minutos (um dia).  
    ![parâmetro do intervalo](./media/log-analytics-scom-assessment/interval.png)  
    Se o valor de saudação é definido tooless de 1440 minutos, regra de saudação é executado em um intervalo de um dia. Neste exemplo, a regra de saudação ignora o valor de intervalo de saudação e é executado em uma frequência de um dia.


## <a name="understanding-how-recommendations-are-prioritized"></a>Compreendendo como as recomendações são priorizadas

Cada recomendação feita recebe um valor de ponderação que identifica Olá a importância relativa da recomendação hello. Somente recomendações mais importantes de saudação 10 são mostradas.

### <a name="how-weights-are-calculated"></a>Como os pesos são calculados

Os pesos são valores agregados com base em três fatores principais:

- Olá *probabilidade* que um problema identificado cause problemas. Uma probabilidade mais alta é igual a pontuação geral maior de tooa de recomendação de saudação.
- Olá *impacto* do problema de saudação na sua organização se ela causar um problema. Um impacto maior é igual a pontuação geral maior de tooa de recomendação de saudação.
- Olá *esforço* necessário tooimplement recomendação de saudação. Um esforço maior é igual a pontuação geral menor de tooa de recomendação de saudação.

Olá peso de cada recomendação é expressa como um percentual da pontuação total da saudação disponíveis para cada área de foco. Por exemplo, se uma recomendação na Olá área de foco de disponibilidade e continuidade dos negócios tiver uma pontuação de 5%, implementar essa recomendação aumentará sua disponibilidade e continuidade dos negócios pontuação geral por 5%.

### <a name="focus-areas"></a>Áreas de foco

**Disponibilidade e continuidade dos negócios** - essa área de foco mostra as recomendações para a disponibilidade de serviço, resiliência de sua infraestrutura e proteção dos negócios.

**Desempenho e escalabilidade** -essa área de foco mostra recomendações toohelp da sua organização crescer de infraestrutura de TI, certifique-se de que seu ambiente de TI atende aos requisitos de desempenho atuais e é capaz de toorespond toochanging precisa de infraestrutura.

**Implantação, atualização e migração** – essa área de foco mostra recomendações toohelp atualizar, migrar e implantar a infraestrutura existente do SQL Server tooyour.

**Operações e monitoramento** - essa área de foco mostra recomendações toohelp simplificar as operações de TI, implementar manutenção preventiva e maximizar o desempenho.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Você deve visar tooscore 100% em cada área de foco?

Não necessariamente. recomendações de saudação baseiam-se no conhecimento do hello e experiências obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. No entanto, nenhuma infraestrutura de servidor é Olá mesmo e recomendações específicas podem ser mais ou menos relevante tooyou. Por exemplo, algumas recomendações de segurança podem ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet. Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem relatórios e coleta de dados ad hoc de baixa prioridade. Problemas de empresas maduras tooa importante podem ser menos importante inicialização de tooa. Você pode desejar tooidentify quais áreas de foco são suas prioridades e depois examinar como suas pontuações mudam ao longo do tempo.

Cada recomendação inclui diretrizes sobre sua importância. Use esta orientação tooevaluate se implementar Olá recomendação é adequada para você, considerando a natureza Olá seu IT services e hello necessidades de negócios da sua organização.

## <a name="use-assessment-focus-area-recommendations"></a>Use as recomendações de área de foco de avaliação

Antes de usar uma solução de avaliação no OMS, você deve ter a solução Olá instalada. tooread mais informações sobre a instalação de soluções, consulte [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Após a instalação, você pode exibir o resumo de saudação das recomendações usando o bloco de avaliação de Gerenciador de operações do System Center Olá na página de visão geral de saudação do OMS.

Saudação de exibição resumida avaliações de conformidade para sua infraestrutura e detalhada das recomendações.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendações de tooview para um foco área e take corretivas

1. Em Olá **visão geral** , clique em Olá **System Center Operations Manager avaliação** lado a lado.
2. Em Olá **System Center Operations Manager avaliação** página, examine as informações de resumo de saudação em uma saudação foco das folhas da área e, em seguida, clique em um tooview recomendações para a área de foco.
3. Em qualquer uma das páginas da área de foco hello, você pode exibir as recomendações de saudação priorizada para seu ambiente. Clique em uma recomendação em **objetos afetados** tooview detalhes sobre por que Olá recomendação foi feita.  
    ![área de foco](./media/log-analytics-scom-assessment/focus-area.png)
4. É possível executar as ações corretivas sugeridas em **Ações Sugeridas**. Quando o item de saudação tiver sido resolvido, avaliações posteriores gravarão que recomendado ações foram executadas e sua pontuação de conformidade aumentará. Os itens corrigido aparecem como **Objetos Passados**.

## <a name="ignore-recommendations"></a>Ignorar as recomendações

Se tiver recomendações que você deseja tooignore, você pode criar um arquivo de texto que o OMS usa tooprevent as recomendações apareçam nos resultados da avaliação.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>recomendações de tooidentify que você deseja tooignore

1. Entre no espaço de trabalho tooyour e abra a pesquisa de Log. Use Olá consulta toolist recomendações que falharam para computadores em seu ambiente a seguir.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Aqui está uma consulta de pesquisa de Log captura de tela mostrando hello:  
    ![pesquisa do log](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Escolha as recomendações que você deseja tooignore. Você usará os valores hello para RecommendationId no próximo procedimento de saudação.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e usar um arquivo de texto IgnoreRecommendations.txt

1. Crie um arquivo chamado IgnoreRecommendations.txt.
2. Cole ou digite cada RecommendationId de cada recomendação que você deseja tooignore OMS em uma linha separada e salve e feche o arquivo hello.
3. Arquivo hello PUT na Olá pasta a seguir em cada computador onde você deseja que as recomendações de tooignore do OMS.
4. No servidor de gerenciamento do Operations Manager Olá - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que as recomendações são ignoradas

1. Depois de ser executado Olá próxima avaliação agendada, por padrão a cada sete dias, Olá especificado recomendações são marcadas como ignoradas e não serão exibidos no painel de avaliação de saudação.
2. Você pode usar o hello toolist de consultas de pesquisa de Log a seguir todas as recomendações de saudação ignorada.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Se você decidir posteriormente que deseja toosee ignorado recomendações, remova os arquivos IgnoreRecommendations.txt ou remova as RecommendationIDs deles.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>Perguntas frequentes da solução System Center Operations Manager Assessment

*Adicionei espaço de trabalho do hello avaliação solução toomy OMS. Mas não vejo as recomendações de saudação. Por que não?* Depois de adicionar a solução hello, use Olá etapas exibição Olá recomendações a seguir para no painel do OMS hello.  

- [Definir Olá executar como conta para o System Center Operations Manager avaliação](#operations-manager-run-as-accounts-for-oms)  
- [Configurar regra de avaliação de Gerenciador de operações do System Center Olá](#configure-the-assessment-rule)


*Há um tooconfigure de maneira com que frequência Olá avaliação é executada?* Sim. Consulte [Olá configurar frequência de execução](#configure-the-run-frequency).

*Se outro servidor for descoberto após ter adicionado Olá solução de avaliação de Gerenciador de operações do System Center, ele será avaliado?* Sim, após a descoberta, ele será avaliado deste ponto em diante – por padrão, a cada sete dias.

*O que é o nome de saudação do processo Olá Olá a coleta de dados?* AdvisorAssessment.exe

*Em que o processo de AdvisorAssessment.exe Olá é executada?* AdvisorAssessment.exe compatível com hello saudação do servidor de gerenciamento do serviço de integridade em que a regra de avaliação hello está habilitada. Usando esse processo, a descoberta de todo o ambiente é obtida por meio da coleta de dados remota.

*Quanto tempo leva para a coleta dos dados?* Coleta de dados no servidor de saudação leva cerca de uma hora. Pode levar mais tempo nos ambientes com muitas instâncias do Operations Manager ou bancos de dados.

*Se configurar o intervalo de saudação do tooless de avaliação de saudação de 1440 minutos?*  avaliação Olá é pré-configurado toorun no máximo uma vez por dia. Se você substituir o valor de tooa do valor de intervalo de saudação menor 1440 minutos, avaliação de saudação usa 1440 minutos como valor de intervalo de saudação.

*Como tooknow se há falhas de pré-requisito?* Se a avaliação de saudação foi executado e você não vê os resultados, é provável que alguns dos pré-requisitos para avaliação de saudação do hello falhou. Você pode executar consultas: `Type=Operation Solution=SCOMAssessment` e `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` na saudação de toosee de pesquisa de Log Falha na pré-requisitos.

*Há uma `Failed tooconnect toohello SQL Instance (….).` mensagem nas falhas do pré-requisito. O que é um problema de saudação?* AdvisorAssessment.exe, processo de saudação que coleta dados, é executado sob Olá saudação do servidor de gerenciamento do serviço de integridade. Como parte da avaliação de hello, processo Olá tentativas tooconnect toohello SQL Server onde o banco de dados do Operations Manager hello está presente. Esse erro pode ocorrer quando as regras de firewall bloqueiam a instância do SQL Server Olá conexão toohello.

*O tipo de dados é coletado?*  Olá seguintes tipos de dados é coletado: - WMI - registro dados - EventLog - Operations Manager dados por meio do Windows PowerShell, consultas SQL e arquivo de coletor de informações.

*Por que tenho tooconfigure uma conta executar como?* Para um servidor do Operations Manager, são executadas várias consultas SQL. Para que eles toorun, você deve usar uma conta executar como com as permissões necessárias. Além disso, as credenciais de administrador local são necessária tooquery WMI.

*Por que apenas Olá 10 principais recomendações são exibidas?* Em vez de apresentar uma lista exaustiva esmagadora de tarefas, é recomendável que você se concentre em tratar as recomendações de saudação priorizada primeiro. Depois de tratar dessas recomendações, recomendações adicionais serão disponibilizadas. Se você preferir a lista detalhada de saudação toosee, você pode exibir todas as recomendações usando a pesquisa de Log.

*Há uma maneira tooignore uma recomendação?* Sim, consulte Olá [ignorar recomendações](#Ignore-recommendations).


## <a name="next-steps"></a>Próximas etapas

- [Pesquisar logs](log-analytics-log-searches.md) tooview obter dados do System Center Operations Manager avaliação e recomendações.
