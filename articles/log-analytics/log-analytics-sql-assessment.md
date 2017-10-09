---
title: aaaOptimize seu ambiente SQL Server com o Azure Log Analytics | Microsoft Docs
description: "Com análise de logs do Azure, você pode usar o hello solução tooassess Olá risco e a integridade de seus ambientes do SQL server em um intervalo regular de avaliação do SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Otimizar seu ambiente SQL Server com hello solução de avaliação do SQL na análise de Log

![Símbolo da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Você pode usar o hello avaliação SQL tooassess solução Olá risco e a integridade de seus ambientes de servidor em um intervalo regular. Este artigo o ajudará a instalar a solução Olá para que você pode executar ações corretivas para problemas potenciais.

Essa solução fornece uma lista priorizada de infraestrutura de servidor implantado recomendações tooyour específico. Olá recomendações são categorizadas em seis foco áreas que ajudar você a entender Olá risco e tomar uma ação corretiva.

recomendações Olá baseiam-se no conhecimento hello e experiência obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. Cada recomendação fornece diretrizes sobre por que uma questão pode ser relevante tooyou e como o tooimplement Olá alterações sugeridas.

Você pode escolher áreas de foco que são mais importante organização de tooyour e acompanham seu progresso em direção a um ambiente íntegro e livre de risco.

Depois que você adicionou a solução hello e uma avaliação é concluído, resumo informações para as áreas de foco são mostradas na Olá **avaliação SQL** painel de infraestrutura de saudação em seu ambiente. Olá seções a seguir descrevem como toouse Olá informações sobre Olá **avaliação SQL** painel, onde você pode exibir e executar as ações recomendadas para sua infraestrutura do SQL server.

![imagem do bloco de Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagem do painel de avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Avaliação do SQL funciona com todas as versões com suporte no momento do SQL Server para as edições Enterprise, Standard e Developer do hello.

Use Olá tooinstall informações a seguir e configurar a solução de saudação.

* Agentes devem ser instalados em servidores que têm o SQL Server instalado.
* Olá solução de avaliação do SQL requer uma versão com suporte do .NET Framework 4 instalado em cada computador que tenha um agente do OMS.
* Na solução de saudação do tooinstall de ordem, o usuário Olá deve ser um administrador ou colaborador toohello assinatura do Azure quando usando Olá portal do Azure. Além disso, o usuário de saudação deve ser um membro da saudação OMS espaço de trabalho Colaborador ou o administrador de função no portal do OMS hello.
* Ao usar o agente do Operations Manager Olá com a avaliação do SQL, você precisará toouse uma conta Run-As do Operations Manager. Consulte [Contas Executar como do Operations Manager para OMS](#operations-manager-run-as-accounts-for-oms) , abaixo, para obter mais informações.

  > [!NOTE]
  > agente MMA Olá não oferece suporte a contas do Operations Manager Run-As.
  >
  >
* Adicionar tooyour de solução de avaliação do SQL Olá espaço de trabalho do OMS usando Olá processo descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Não é necessária nenhuma configuração.

> [!NOTE]
> Depois que você adicionou a solução hello, arquivo AdvisorAssessment.exe de saudação é adicionado tooservers com agentes. Dados de configuração lidos e, em seguida, enviados toohello serviço do OMS na nuvem Olá para processamento. Lógica é aplicada toohello recebida dados e o serviço de nuvem Olá registra dados de saudação.

## <a name="sql-assessment-data-collection-details"></a>Detalhes de coleta de dados da Avaliação de SQL
Avaliação do SQL coleta dados do WMI, dados de registro, dados de desempenho e resultados de exibição de gerenciamento dinâmico do SQL Server usando Olá agentes que você tiver habilitado.

Olá tabela a seguir mostra os métodos de coleta de dados para os agentes se Operations Manager (SCOM) é necessária e como geralmente os dados são coletados por um agente.

| plataforma | Agente direto | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 dias |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Contas Executar como do Operations Manager para OMS
Análise de log no OMS usa hello agente do Operations Manager e toocollect do grupo de gerenciamento e envia dados toohello OMS service. OMS criado com base nos pacotes de gerenciamento para cargas de trabalho tooprovide serviços de valor agregado. Cada carga de trabalho requer pacotes de gerenciamento de toorun de privilégios de carga de trabalho específica em um contexto de segurança diferente, como uma conta de domínio. É necessário tooprovide informações de credenciais Configurando uma conta executar como do Operations Manager.

Use Olá seguindo informações tooset saudação do Operations Manager conta executar como para avaliação do SQL.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Definir Olá a conta executar como para avaliação do SQL
 Se você já estiver usando Olá pacote de gerenciamento do SQL Server, você deve usar essa conta executar como.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>Olá tooconfigure conta executar como do SQL no console de operações de saudação
> [!NOTE]
> Se você estiver usando hello OMS direto agente, em vez de agente do SCOM hello, pacote de gerenciamento Olá sempre é executado no contexto de segurança de saudação do hello conta Sistema Local. Ignorar as etapas 1 a 5 abaixo e execute ou Olá exemplo de T-SQL ou o Powershell, especificando NT AUTHORITY\SYSTEM como nome de usuário de saudação.
>
>

1. No Operations Manager, abra o console de operações hello e, em seguida, clique em **administração**.
2. Em **Configuração Executar como**, clique em **Perfis** e abra **Perfil Executar como da Avaliação SQL do OMS**.
3. Em Olá **contas executar como** , clique em **adicionar**.
4. Selecione uma conta executar como do Windows que contenha Olá credenciais necessárias para o SQL Server, ou clique em **novo** toocreate um.

   > [!NOTE]
   > Olá executar como tipo de conta deve ser Windows. Olá conta executar como também deve fazer parte do grupo de administradores locais em todos os servidores Windows que hospedam instâncias do SQL Server.
   >
   >
5. Clique em **Salvar**.
6. Modifique e, em seguida, execute Olá exemplo de T-SQL a seguir no tooRun necessário cada instância do SQL Server toogrant permissões mínimas tooperform conta como avaliação do SQL. No entanto, você não precisa toodo isso se uma conta executar como já fizer parte da função de servidor sysadmin Olá em instâncias do SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>Olá tooconfigure conta executar como do SQL usando o Windows PowerShell
Abra uma janela do PowerShell e execute o script a seguir depois de atualizá-lo com suas informações de saudação:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Compreendendo como as recomendações são priorizadas
Cada recomendação feita recebe um valor de ponderação que identifica Olá a importância relativa da recomendação hello. Olá apenas dez recomendações mais importantes são mostradas.

### <a name="how-weights-are-calculated"></a>Como os pesos são calculados
Os pesos são valores agregados com base em três fatores principais:

* Olá *probabilidade* que um problema identificado cause problemas. Uma probabilidade mais alta é igual a pontuação geral maior de tooa de recomendação de saudação.
* Olá *impacto* do problema de saudação na sua organização se ela causar um problema. Um impacto maior é igual a pontuação geral maior de tooa de recomendação de saudação.
* Olá *esforço* necessário tooimplement recomendação de saudação. Um esforço maior é igual a pontuação geral menor de tooa de recomendação de saudação.

Olá peso de cada recomendação é expressa como um percentual da pontuação total da saudação disponíveis para cada área de foco. Por exemplo, se uma recomendação na hello segurança e área de foco de conformidade tiver uma pontuação de 5%, implementar essa recomendação aumentará a segurança e conformidade pontuação geral por 5%.

### <a name="focus-areas"></a>Áreas de foco
**Segurança e conformidade** - essa área de foco mostra recomendações para possíveis ameaças de segurança e violações, políticas corporativas, bem como os requisitos de conformidade técnica, legal e regulatória.

**Disponibilidade e continuidade dos negócios** - essa área de foco mostra as recomendações para a disponibilidade de serviço, resiliência de sua infraestrutura e proteção dos negócios.

**Desempenho e escalabilidade** -essa área de foco mostra recomendações toohelp da sua organização crescer de infraestrutura de TI, certifique-se de que seu ambiente de TI atende aos requisitos de desempenho atuais e é capaz de toorespond toochanging precisa de infraestrutura.

**Atualização, implantação e migração** – essa área de foco mostra recomendações toohelp atualizar, migrar e implantar a infraestrutura existente do SQL Server tooyour.

**Operações e monitoramento** - essa área de foco mostra recomendações toohelp simplificar as operações de TI, implementar manutenção preventiva e maximizar o desempenho.

**Gerenciamento de alterações e configuração** -essa área de foco mostra recomendações toohelp proteger as operações diárias, verifique se as alterações não negativamente afetam sua infraestrutura, estabelecer procedimentos de controle de alterações e tootrack e auditoria configurações do sistema.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Você deve visar tooscore 100% em cada área de foco?
Não necessariamente. recomendações de saudação baseiam-se no conhecimento do hello e experiências obtidas pelos engenheiros da Microsoft em milhares de visitas a clientes. No entanto, nenhuma infraestrutura de servidor é Olá mesmo e recomendações específicas podem ser mais ou menos relevante tooyou. Por exemplo, algumas recomendações de segurança podem ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet. Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem relatórios e coleta de dados ad hoc de baixa prioridade. Problemas de empresas maduras tooa importante podem ser menos importante inicialização de tooa. Você pode desejar tooidentify quais áreas de foco são suas prioridades e depois examinar como suas pontuações mudam ao longo do tempo.

Cada recomendação inclui diretrizes sobre sua importância. Você deve usar essa orientação tooevaluate se implementar Olá recomendação é adequada para você, considerando a natureza Olá seu IT services e hello necessidades de negócios da sua organização.

## <a name="use-assessment-focus-area-recommendations"></a>Use as recomendações de área de foco de avaliação
Antes de usar uma solução de avaliação no OMS, você deve ter a solução Olá instalada. tooread mais informações sobre a instalação de soluções, consulte [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Após a instalação, você pode exibir o resumo de saudação das recomendações usando o bloco de avaliação SQL Olá na página de visão geral de saudação do OMS.

Saudação de exibição resumida avaliações de conformidade para sua infraestrutura e detalhada das recomendações.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendações de tooview para um foco área e take corretivas
1. Em Olá **visão geral** , clique em Olá **avaliação SQL** lado a lado.
2. Em Olá **avaliação SQL** página, examine as informações de resumo de saudação em uma saudação foco das folhas da área e, em seguida, clique em um tooview recomendações para a área de foco.
3. Em qualquer uma das páginas da área de foco hello, você pode exibir as recomendações de saudação priorizada para seu ambiente. Clique em uma recomendação em **objetos afetados** tooview detalhes sobre por que Olá recomendação foi feita.  
    ![imagem de recomendações da Avaliação do SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. É possível executar as ações corretivas sugeridas em **Ações Sugeridas**. Quando o item de saudação tiver sido resolvido, avaliações posteriores gravarão que recomendado ações foram executadas e sua pontuação de conformidade aumentará. Os itens corrigido aparecem como **Objetos Passados**.

## <a name="ignore-recommendations"></a>Ignorar as recomendações
Se tiver recomendações que você deseja tooignore, você pode criar um arquivo de texto que o OMS usará tooprevent as recomendações apareçam nos resultados da avaliação.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendações de tooidentify que você irá ignorar
1. Entre no espaço de trabalho tooyour e abra a pesquisa de Log. Use Olá consulta toolist recomendações que falharam para computadores em seu ambiente a seguir.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Aqui está uma consulta de pesquisa de Log de saudação de captura de tela mostrando: ![falha recomendações](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Escolha as recomendações que você deseja tooignore. Você usará os valores hello para RecommendationId no próximo procedimento de saudação.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate e usar um arquivo de texto IgnoreRecommendations.txt
1. Crie um arquivo chamado IgnoreRecommendations.txt.
2. Cole ou digite cada RecommendationId de cada recomendação que você deseja tooignore OMS em uma linha separada e salve e feche o arquivo hello.
3. Arquivo hello PUT na Olá pasta a seguir em cada computador onde você deseja que as recomendações de tooignore do OMS.
   * Em computadores com hello Microsoft Monitoring Agent (conectado diretamente ou por meio do Operations Manager) - *SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * No servidor de gerenciamento do Operations Manager Olá - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que as recomendações são ignoradas
1. Depois de ser executado Olá próxima avaliação agendada, por padrão a cada 7 dias, Olá especificado recomendações são marcadas como ignoradas e não serão exibidos no painel de avaliação de saudação.
2. Você pode usar o hello toolist de consultas de pesquisa de Log a seguir todas as recomendações de saudação ignorada.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Se você decidir posteriormente que deseja toosee ignorado recomendações, remova os arquivos IgnoreRecommendations.txt ou remova as RecommendationIDs deles.

## <a name="sql-assessment-solution-faq"></a>Perguntas frequentes sobre soluções de Avaliação de SQL
*Com que frequência uma avaliação é executada?*

* Olá avaliação é executada a cada 7 dias.

*Há um tooconfigure de maneira com que frequência Olá avaliação é executada?*

* Não no momento.

*Se outro servidor for descoberto após ter adicionado Olá solução de avaliação do SQL, ele será avaliado?*

* Sim, assim que for descoberto, ele é avaliado a partir de então a cada sete dias.

*Se um servidor for encerrado, quando ele será removido da avaliação de Olá?*

* Se um servidor não enviar dados por três semanas, ele será removido.

*O que é o nome de saudação do processo Olá Olá a coleta de dados?*

* AdvisorAssessment.exe

*Quanto tempo leva para toobe dados coletado?*

* coleta de dados reais de saudação no servidor de saudação leva aproximadamente 1 hora. Pode levar mais tempo em servidores que têm um grande número de instâncias ou bancos de dados SQL.

*Que tipo de dados é coletado?*

* Olá seguintes tipos de dados é coletado:
  * WMI
  * Registro
  * Contadores de desempenho
  * Exibições de gerenciamento dinâmico SQL (DMV).

*Há uma maneira tooconfigure quando os dados são coletados?*

* Não no momento.

*Por que tenho tooconfigure uma conta executar como?*

* Para o SQL Server, um pequeno número de consultas SQL é executado. Para que eles toorun, uma conta executar como com tooSQL de permissões Exibir estado do servidor deve ser usado.  Além disso, em ordem tooquery WMI, as credenciais de administrador local são necessárias.

*Por que apenas Olá 10 principais recomendações são exibidas?*

* Em vez de apresentar uma lista exaustiva de tarefas, é recomendável que você se concentre em tratar as recomendações de saudação priorizada primeiro. Depois de tratar dessas recomendações, recomendações adicionais serão disponibilizadas. Se você preferir a lista detalhada de saudação toosee, você pode exibir todas as recomendações usando a pesquisa de log OMS hello.

*Há uma maneira tooignore uma recomendação?*

* Sim, confira a seção [Ignorar recomendações](#ignore-recommendations) acima.

## <a name="next-steps"></a>Próximas etapas
* [Pesquisar logs](log-analytics-log-searches.md) tooview obter dados de avaliação do SQL e as recomendações.
