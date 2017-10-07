---
title: "Portal do Azure: criar e gerenciar um pool elástico do Banco de Dados SQL | Microsoft Docs"
description: "Saiba como toouse Olá portal do Azure e toomanage de inteligência interna do banco de dados SQL, o monitor e um pool Elástico escalonável toooptimize banco de dados de desempenho de tamanho de direito e gerenciar os custos."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Criar e gerenciar um pool Elástico com hello portal do Azure
Este tópico mostra como toocreate e gerenciar escalonável [pools Elásticos](sql-database-elastic-pool.md) com hello portal do Azure. Você também pode criar e gerenciar um pool Elástico do Azure com [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Criar um pool elástico 

Há duas maneiras de criar um pool elástico. Você pode fazer isso do zero, se você souber que a instalação Olá pool desejado ou começar com uma recomendação do serviço de saudação. Banco de dados SQL tem inteligência interna que recomenda uma configuração de pool Elástico se mais eficiente com base no hello após telemetria de uso de seus bancos de dados.

Você pode criar vários pools em um servidor, mas você não pode adicionar bancos de dados de diferentes servidores em Olá mesmo pool. 

> [!NOTE]
> Os pools elásticos têm uma disponibilidade geral (DG) em todas as regiões do Azure, exceto na Índia Ocidental, onde atualmente estão no modo de visualização.  A GA dos pools elásticos nessa região ocorrerá assim que possível.
>

### <a name="step-1-create-an-elastic-pool"></a>Etapa 1: criar um pool elástico

Criando um pool Elástico de uma já existente **server** folha no portal de saudação é hello mais fácil maneira toomove bancos de dados existentes em um pool Elástico.

> [!NOTE]
> Você também pode criar um pool Elástico pesquisando **pool Elástico do SQL** em Olá **Marketplace** ou clicando em **+ adicionar** em Olá **pools Elásticos de SQL**procurar folha. Você é capaz de toospecify um servidor novo ou existente por este fluxo de trabalho de provisionamento do pool.
>
>

1. Em Olá [portal do Azure](http://portal.azure.com/), clique em **mais serviços**  **>**  **servidores SQL**e clique em servidor de saudação que contém a saudação bancos de dados você deseja que o pool Elástico do tooadd tooan.
2. Clique em **Novo pool**.

    ![Adicionar pool de servidores tooa](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-OU-**

    Você verá uma mensagem informando que há são recomendadas pools Elásticos para o servidor de saudação. Clique em Olá de toosee mensagem de saudação recomendado pools com base na telemetria de uso do banco de dados históricos, Olá camada toosee mais detalhes e clique personalizar pool hello. Consulte [entender as recomendações de pool](#understand-elastic-pool-recommendations) mais adiante neste tópico para como recomendação de saudação é feita.

    ![pool recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Olá **pool Elástico** folha é exibida, que é onde você especificar configurações de saudação para o pool. Se você clicou **novo pool** na etapa anterior de saudação, Olá preço é **padrão** por padrão e não há bancos de dados é selecionada. Você pode criar um conjunto vazio, ou especificar um conjunto de bancos de dados existentes de toomove desse servidor no pool de saudação. Se você estiver criando um pool recomendado, Olá recomendado preço, as configurações de desempenho e a lista de bancos de dados são preenchidos de antemão, mas você ainda pode alterá-los.

    ![Configurar pool elástico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Especifique um nome para o pool Elástico hello, ou deixá-lo como padrão de saudação.

### <a name="step-2-choose-a-pricing-tier"></a>Etapa 2: escolher um tipo de preço

Olá de preço do pool determina Olá recursos elastics toohello disponível no pool de saudação e Olá o número máximo de eDTUs (eDTU máximo) e o banco de dados do armazenamento (GBs) tooeach disponíveis. Para obter detalhes, consulte Camadas de serviço.

toochange Olá preço para o pool de saudação, clique em **preço**, clique em Olá preço você deseja e, em seguida, clique em **selecione**.

> [!IMPORTANT]
> Depois que você escolha Olá preço e confirmar suas alterações, clicando em **Okey** na última etapa de hello, não será Olá toochange capaz de preço do pool de saudação. toochange Olá camada de preços para um pool Elástico existente, criar um pool Elástico em Olá desejado de preço e migre Olá bancos de dados toothis novo pool.
>

![Selecione uma faixa de preço.](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Etapa 3: Configurar o pool de saudação

Depois de definir Olá preço, clique em Configurar pool onde adicionar bancos de dados, eDTUs de pool do conjunto e armazenamento (GBs de pool), e defina Olá eDTUs de min e max para elastics Olá no pool de saudação.

1. Clique em **Configurar pool**
2. Selecione bancos de dados de saudação que você deseja tooadd toohello pool. Esta etapa é opcional durante a criação de pool de saudação. Bancos de dados podem ser adicionados depois Olá pool foi criado.
    bancos de dados tooadd, clique em **Adicionar banco de dados**, clique em bancos de dados de saudação que você deseja tooadd e, em seguida, clique em Olá **selecione** botão.

    ![Adicionar bancos de dados](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Se os bancos de dados Olá estiver trabalhando com tem telemetria suficiente histórico de uso, Olá **estimado de eDTU e GB uso** gráfico e hello **real eDTU uso** toohelp de atualização de gráfico de barras que facilitam a configuração decisões. Além disso, o serviço de saudação pode oferecer um toohelp de mensagem de recomendação você direita tamanho Olá pool. Veja [Recomendações dinâmicas](#understand-elastic-pool-recommendations).

3. Usar controles Olá Olá **configurar pool** tooexplore configurações de página e configurar o pool. Confira [Limites dos pools elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para saber mais sobre os limites de cada camada de serviço, e confira as [Considerações de preço e desempenho dos pools elásticos](sql-database-elastic-pool.md) para obter uma orientação detalhada sobre o tamanho correto de um pool elástico. Para ler mais informações sobre as configurações do pool, confira as [Propriedades do pool elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Configurar pool elástico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Clique em **selecione** em Olá **configurar Pool** folha depois de alterar as configurações.
5. Clique em **Okey** toocreate pool de saudação.

## <a name="understand-elastic-pool-recommendations"></a>Compreensão das recomendações de pool elástico

Olá serviço de banco de dados SQL avalia o histórico de uso e recomenda um ou mais pools quando ele é mais econômico que bancos de dados único. Cada recomendação é configurada com um subconjunto de bancos de dados do servidor de saudação que melhor se adaptar pool Olá exclusivo.

![pool recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recomendação de pool de saudação inclui:

- A camada de preços para o pool de saudação (Basic, Standard, Premium ou Premium RS)
- Os **eDTUs do POOL** apropriados (também chamados de Máx. de eDTUs por pool)
- Olá **eDTU máximo** e **Mín** por banco de dados
- lista de saudação de bancos de dados recomendados para o pool de saudação

> [!IMPORTANT]
> serviço de saudação considera Olá últimos 30 dias de telemetria ao recomendar pools. Para ver um banco de dados do toobe considerado como candidata para um pool Elástico, ele deve existir pelo menos 7 dias. Os bancos de dados que já estão em um pool elástico não são considerados candidatos para as recomendações de pool elástico.
>

serviço de saudação avalia as necessidades de recursos e eficácia dos custos de movimentação Olá único bancos de dados em cada camada de serviço em pools de saudação mesmo nível. Por exemplo, todos os bancos de dados padrão em um servidor são avaliados para sua adaptação em um pool elástico Standard. Isso significa que o serviço Olá não faz recomendações entre camadas como mover um banco de dados padrão em um pool de Premium.

Depois de adicionar o pool de toohello de bancos de dados, as recomendações são geradas dinamicamente com base no histórico de uso de bancos de dados de saudação que você selecionou hello. Essas recomendações são mostradas em Olá eDTU e GB gráfico de uso em uma faixa de recomendação na parte superior de saudação do hello **configurar pool** folha. Essas recomendações são pretendido tooassist você na criação de um pool Elástico otimizado para seus bancos de dados específicos.

![Recomendações dinâmicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Gerenciamento e monitoração um pool elástico

Você pode usar o hello toomonitor portal do Azure e gerenciar um pool Elástico e bancos de dados de saudação no pool de saudação. No portal de hello, você pode monitorar a utilização de saudação de um pool Elástico e bancos de dados hello dentro desse pool. Você também pode fazer um conjunto de alterações de pool Elástico tooyour e enviar todas as alterações no hello mesmo tempo. Essas alterações incluem adicionar ou remover bancos de dados, alterar as configurações de pool elástico ou alterar suas configurações de banco de dados.

Olá gráfico a seguir mostra um pool Elástico de exemplo. exibição de saudação inclui:

*  Gráficos de monitoramento de uso do recurso de pool Elástico hello e bancos de dados de saudação contidos no pool de saudação.
*  Olá **configurar** pool botão toomake pool Elástico toohello é alterado.
*  Olá **criar banco de dados** botão que cria um banco de dados e adiciona-o pool Elástico atual de toohello.
*  Trabalhos elásticos que ajudam a gerenciar muitos bancos de dados executando scripts Transact SQL em todos os bancos de dados em uma lista.

![Exibição de pool][2]

Você pode ir tooa determinado pool toosee sua utilização de recursos. Por padrão, o pool de saudação é configurado tooshow armazenamento e eDTU o uso de saudação última hora. gráfico de saudação pode ser configurado tooshow diferentes métricas em várias janelas de tempo.

1. Selecione um toowork de pool Elástico com.
2. Em **Monitoramento de Pool Elástico** há um gráfico rotulado **Utilização de recursos**. Clique em gráfico de saudação.

    ![Monitoramento de pool elástico][3]

    Olá **métrica** folha abre, mostrar uma exibição detalhada de saudação especificados métricas em janela de tempo especificada de saudação.   

    ![Lâmina Métrica][9]

### <a name="toocustomize-hello-chart-display"></a>exibição de gráfico de saudação toocustomize

Você pode editar gráfico hello e Olá folha de métricas toodisplay outras métricas como porcentagem da CPU, porcentagem de e/s de dados e porcentagem de e/s de log usado.

1. Na folha de métricas de saudação, clique em **editar**.

    ![Clique em editar][6]

2. Em Olá **Editar gráfico** folha, selecione um intervalo de tempo (última hora, atualmente, ou última semana), ou clique em **personalizado** tooselect qualquer data vão Olá duas últimas semanas. Selecione o tipo de gráfico hello (barra ou linha) e selecione Olá toomonitor de recursos.

   > [!Note]
   > Somente o gráfico de métricas com hello mesma unidade de medida pode ser exibida em hello em Olá mesmo tempo. Por exemplo, se você selecionar "percentual de eDTU", em seguida, você pode apenas selecionar outras métricas com porcentagem como a unidade de medida de saudação.
   >

    ![Clique em editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Em seguida, clique em **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gerenciamento e monitoração de bancos de dados um pool elástico

Bancos de dados individuais também podem ser monitorados para identificar potenciais problemas.

1. Em **Monitoramento de Banco de Dados Elástico**, há um gráfico que exibe as métricas para cinco bancos de dados. Por padrão, Olá gráfico exibe Olá top 5 bancos de dados no pool de saudação pelo uso de eDTU médio em Olá última hora. Clique em gráfico de saudação.

    ![Monitoramento de pool elástico][4]

2. Olá **utilização de recursos de banco de dados** folha é exibida. Isso fornece uma exibição detalhada de uso do banco de dados de saudação no pool de saudação. Usando a grade de saudação na parte inferior de saudação da folha Olá, você pode selecionar qualquer banco de dados em Olá pool toodisplay seu uso no gráfico de saudação (backup de bancos de dados too5). Você também pode personalizar a janela de métricas e a hora de saudação exibida no gráfico de saudação clicando **Editar gráfico**.

    ![Folha Utilização de Recursos do Banco de Dados][8]

### <a name="toocustomize-hello-view"></a>exibição de saudação toocustomize

1. Em Olá **utilização de recursos de banco de dados** folha, clique em **Editar gráfico**.

    ![Clique em Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. Em Olá **editar** folha de gráfico, selecione um intervalo de tempo (última hora ou nas últimas 24 horas) ou clique em **personalizado** tooselect dia diferente no hello após toodisplay de 2 semanas.

    ![Clique em Personalizar](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Clique em Olá **comparar bancos de dados por** suspensa tooselect um toouse de métrica diferente ao comparar os bancos de dados.

    ![Editar gráfico Olá](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor de bancos de dados

Na lista de banco de dados de saudação do hello **utilização de recursos de banco de dados** folha, você pode encontrar bancos de dados procurando por meio de páginas de saudação na lista de saudação ou digitando o nome de saudação do banco de dados. Use banco de dados da saudação tooselect Olá caixa de seleção.

![Pesquise toomonitor de bancos de dados][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Adicionar um recurso de pool Elástico tooan alerta

Você pode adicionar regras tooan pool Elástico que enviar email de alerta ou toopeople pontos de extremidade de tooURL de cadeias de caracteres quando o pool Elástico Olá atinge um limite de utilização que você configurou.

**tooadd um recurso de alerta tooany:**

1. Clique em Olá **utilização de recursos** saudação do gráfico tooopen **métrica** folha, clique em **adicionar alerta**e, em seguida, preencha as informações Olá Olá **adicionar um alerta regra** folha (**recurso** configurar automaticamente ao pool de saudação toobe você está trabalhando com).
2. Digite um **nome** e **descrição** que identifica Olá tooyou de alerta e destinatários de saudação.
3. Escolha um **métrica** que você deseja tooalert da lista de saudação.

    gráfico de Olá dinamicamente mostra a utilização de recursos para essa métrica toohelp que você escolher um limite.

4. Escolha uma **Condição** (maior que, menor que, etc.) e um **Limite**.
5. Escolha um **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação.
6. Clique em **OK**.

Para obter mais informações, consulte [Criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Mover um banco de dados para um pool elástico

Você pode adicionar ou remover bancos de dados de um pool existente. bancos de dados Olá podem estar em outros pools. No entanto, você só pode adicionar bancos de dados que estão em Olá mesmo servidor lógico.

1. Na folha Olá para o pool de saudação em **bancos de dados Elásticos** clique **configurar pool**.

    ![Clique em Configurar pool][1]

2. Em Olá **configurar pool** folha, clique em **adicionar toopool**.

    ![Clique em Adicionar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. Em Olá **adicionar bancos de dados** folha, banco de dados selecione hello ou pool de toohello tooadd bancos de dados. Em seguida, clique em **Selecionar**.

    ![Selecione tooadd de bancos de dados](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Olá **configurar pool** folha agora listas Olá banco de dados selecionado toobe adicionado, e seu status definido muito**pendente**.

    ![Adições de pool pendentes](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. Em Olá **folha de pool configurar**, clique em **salvar**.

    ![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Remover um banco de dados de um pool elástico

1. Em Olá **configurar pool** folha, banco de dados selecione hello ou tooremove de bancos de dados.

    ![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Clique em **Remover do pool**.

    ![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Olá **configurar pool** folha agora listas Olá banco de dados selecionado toobe removida com seu status definido muito**pendente**.

    ![visualização de adição ou remoção de banco de dados](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. Em Olá **folha de pool configurar**, clique em **salvar**.

    ![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Alterar as configurações de desempenho de um pool elástico

Como monitorar a utilização de recursos de saudação de um pool Elástico, você pode descobrir que alguns ajustes são necessários. Talvez pool Olá precisa de uma alteração nos limites de armazenamento ou desempenho hello. Possivelmente, você deseja toochange configurações de banco de dados de saudação no pool de saudação. Você pode alterar a instalação de saudação do pool de saudação em qualquer tempo tooget Olá melhor equilíbrio entre desempenho e custo. Veja [Quando um pool elástico deve ser usado?](sql-database-elastic-pool.md) para saber mais.

toochange Olá eDTUs armazenamento limites ou por pool e eDTUs por banco de dados:

1. Olá abrir **configurar pool** folha.

    Em **as configurações do pool Elástico**, usar ou configurações de pool do controle deslizante toochange hello.

    ![Utilização de recursos de pool elástico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Quando altera a configuração de saudação, exibição Olá mostra Olá mensal custo estimado de alteração de saudação.

    ![Atualização de um pool elástico e o novo custo mensal](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latência de operações do pool elástico
* Alterar Olá min eDTUs por banco de dados ou o máximo de eDTUs por banco de dados normalmente é concluído em 5 minutos ou menos.
* Alterar eDTUs Olá por pool de depende da quantidade total de saudação do espaço usado por todos os bancos de dados no pool de saudação. As alterações levam, em média, 90 minutos ou menos a cada 100 GB. Por exemplo, se o espaço total Olá usado por todos os bancos de dados no pool de saudação é de 200 GB, Olá esperada de latência para mudar o eDTU do pool de saudação por pool é de 3 horas ou menos.

## <a name="next-steps"></a>Próximas etapas

- toounderstand que um pool Elástico, consulte [pool Elástico de banco de dados SQL](sql-database-elastic-pool.md).
- Para ler mais diretrizes sobre o uso dos pools elásticos, confira [Considerações de preço e desempenho para pools elásticos](sql-database-elastic-pool.md).
- toouse trabalhos Elástico toorun Transact-SQL scripts em relação a qualquer número de bancos de dados no pool de hello, consulte [visão geral de trabalhos Elástico](sql-database-elastic-jobs-overview.md).
- tooquery em qualquer número de bancos de dados no pool de hello, consulte [visão geral de consulta Elástico](sql-database-elastic-query-overview.md).
- Para transações de qualquer número de bancos de dados no pool de hello, consulte [transações Elásticos](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
