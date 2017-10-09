---
title: "desempenho aaaMonitor de muitos bancos de dados do SQL Azure em um aplicativo de SaaS multilocatário | Microsoft Docs"
description: "Monitorar e gerenciar o desempenho de bancos de dados e pools no aplicativo do Azure SQL Database Wingtip SaaS Olá"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Monitorar o desempenho de saudação aplicativo SaaS Wingtip

Neste tutorial, vários dos principais cenários de gerenciamento de desempenho usados em aplicativos SaaS são explorados. Usar uma atividade de toosimulate do gerador de carga em todos os bancos de dados de locatário, monitoramento interno do hello e recursos de alerta de banco de dados SQL e pools Elásticos são demonstrados.

Olá Wingtip SaaS aplicativo usa um modelo de dados de locatário único, onde cada local (Locatário) tem seu próprio banco de dados. Como muitos aplicativos SaaS, Olá previsto padrão de carga de trabalho de locatário é imprevisível e esporádica. Em outras palavras, as vendas de ingressos podem ocorrer a qualquer momento. tootake vantagem desse padrão de uso típico do banco de dados, bancos de dados são implantados em pools de banco de dados Elástico de locatário. Pools Elásticos otimizam o custo de saudação de uma solução de compartilhamento de recursos em vários bancos de dados. Com esse tipo de padrão, é importante toomonitor banco de dados e tooensure de uso de recursos do pool que carrega razoavelmente são balanceados entre pools. Você também precisa tooensure bancos de dados individuais têm recursos adequados e que os pools não estão atingindo sua [eDTU](sql-database-what-is-a-dtu.md) limites. Este tutorial explora maneiras toomonitor e gerenciar bancos de dados e pools e como a ação corretiva tootake na resposta toovariations na carga de trabalho.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]

> * Simule o uso em bancos de dados de locatário Olá executando um gerador de carga fornecido
> * Bancos de dados de locatário de saudação do monitor como eles respondem toohello aumento na carga
> * Dimensionar o hello pool Elástico em resposta toohello maior banco de dados de carga
> * Provisionar uma segunda atividade de banco de dados de saldo de tooload pool Elástico


toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>Padrões de gerenciamento de desempenho de tooSaaS de Introdução

Gerenciando o desempenho do banco de dados consiste de compilação e analisando dados de desempenho e, em seguida, reagindo toothis dados ajustando parâmetros toomaintain um tempo de resposta aceitável para o seu aplicativo. Ao hospedar vários locatários, pools de banco de dados Elástico são uma maneira econômica tooprovide e gerenciar os recursos de um grupo de bancos de dados com cargas de trabalho imprevisíveis. Com determinados padrões carga de trabalho, não mais que dois bancos de dados S3 poderiam se beneficiar sendo gerenciados em um pool.

![mídia](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Pools e bancos de dados de saudação em pools, devem ser monitorado tooensure permanecem dentro dos intervalos aceitáveis de desempenho. Ajustar as necessidades de Olá Olá pool configuração toomeet de carga de trabalho agregado de todos os bancos de dados, garantindo que Olá eDTUs de pool apropriados para Olá Olá carga de trabalho geral. Ajuste Olá por banco de dados por banco de dados e min eDTU máximo valores tooappropriate valores para seus requisitos de aplicativo específico.

### <a name="performance-management-strategies"></a>Estratégias de gerenciamento de desempenho

* tooavoid ter toomanually monitorar o desempenho, é mais eficiente muito**definir alertas disparam quando os bancos de dados ou os pools afastem fora dos intervalos normais**.
* Olá flutuações de termo tooshort toorespond no nível de desempenho de agregação de saudação de um pool, **nível de eDTU do pool pode ser aumentado ou reduzidos**. Se este flutuação ocorre em uma base regular ou previsível, **dimensionamento pool Olá possível toooccur agendado automaticamente**. Por exemplo, reduzir verticalmente quando você souber que sua carga de trabalho é leve, talvez durante a noite ou durante os finais de semana.
* toorespond toolonger termo flutuações ou alterações em Olá número de bancos de dados, **bancos de dados individuais podem ser movidos para outros pools**.
* aumenta a toorespond tooshort termo *individuais* carregamento de banco de dados **bancos de dados individuais podem ser retirados de um pool e atribuídos a um nível de desempenho individuais**. Depois que a carga de saudação é reduzida, Olá banco de dados pode, em seguida, retornar toohello pool. Quando isso é conhecido com antecedência, bancos de dados podem ser movidos preventivamente banco de dados do tooensure Olá sempre tem recursos Olá necessárias e tooavoid impacto em outros bancos de dados no pool de saudação. Se esse requisito é previsível, como um local com um surto de vendas de tíquete para um evento popular, esse comportamento de gerenciamento pode ser integrado em um aplicativo hello.

Olá [portal do Azure](https://portal.azure.com) fornece monitoramento e alertas na maioria dos recursos internos. Para o Banco de Dados SQL, o monitoramento e o alerta estão disponíveis em bancos de dados e pools. Este interna de monitoramento e alertas é específicas do recurso, portanto, é conveniente toouse para pequenas quantidades de recursos, mas não é muito conveniente ao trabalhar com muitos recursos.

Para cenários de alto volume em que você está trabalhando com muitos recursos, o [Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) pode ser usado. Esse é um serviço separado do Azure que fornece a análise de logs de diagnóstico emitidos e da telemetria coletada em um espaço de trabalho de análise de logs. Análise de log pode coletar telemetria dos muitos serviços e ser usado tooquery e definir alertas.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Obter o código-fonte Olá Wingtip aplicativos e scripts

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Provisionar locatários adicionais

Enquanto os pools podem ser tão econômicos com apenas dois bancos de dados S3, Olá mais bancos de dados que estão em Olá Olá de pool mais econômico Olá média efeito torna-se. Para uma boa compreensão do funcionamento do monitoramento de desempenho e do gerenciamento em grande escala, este tutorial requer que você tenha pelo menos 20 bancos de dados implantados.

Se você já provisionado um lote de locatários em um tutorial anterior, ignorar toohello [simular o uso em todos os bancos de dados de locatário](#simulate-usage-on-all-tenant-databases) seção.

1. Abrir... \\Módulos de aprendizado\\gerenciamento e monitoramento do desempenho de\\*demonstração PerformanceMonitoringAndManagement.ps1* em Olá *PowerShell ISE*. Mantenha esse script aberto pois você executará vários cenários durante este tutorial.
1. Defina **$DemoScenario** = **1**, **Provisionar um lote de locatários**
1. Pressione **F5** toorun script de saudação.

script Hello implantará 17 locatários em menos de cinco minutos.

Olá *New-TenantBatch* script usa um conjunto de aninhada ou vinculado [Gerenciador de recursos de](../azure-resource-manager/index.md) modelos criados por um lote de locatários, que, por padrão, copia o banco de dados de saudação **basetenantdb** Olá catálogo server toocreate Olá novo locatário bancos de dados, em seguida, registra esses no catálogo hello e finalmente inicializa-los com o tipo de nome e local do locatário hello. Isso é consistente com a maneira Olá Olá aplicativo provisiona um novo locatário. Todas as alterações feitas muito*basetenantdb* é aplicada tooany novos locatários provisionados depois disso. Consulte Olá [tutorial de gerenciamento de esquema](sql-database-saas-tutorial-schema-management.md) toosee como toomake alterações de esquema muito*existente* locatário bancos de dados (incluindo Olá *basetenantdb* banco de dados).

## <a name="simulate-usage-on-all-tenant-databases"></a>Simular o uso em todos os bancos de dados de locatário

Olá *PerformanceMonitoringAndManagement.ps1 demonstração* script é fornecido que simula uma carga de trabalho em execução em todos os bancos de dados de locatário. carga de saudação é gerada usando um dos cenários de saudação de carga disponíveis:

| Demonstração | Cenário |
|:--|:--|
| 2 | Gerar carga de intensidade normal (aproximadamente 40 DTU) |
| 3 | Gerar carga com picos mais longos e mais frequentes por banco de dados|
| 4 | Gerar carga com picos maiores de DTU por banco de dados (aprox. 80 DTU)|
| 5 | Gerar uma carga normal e uma carga alta em um locatário único (aprox. 95 DTU)|
| 6 | Gerar carga desbalanceada entre vários pools|

Gerador de carga Olá aplica-se um *sintético* banco de dados de locatário de tooevery carga de CPU. Gerador de saudação inicia um trabalho para cada banco de dados de locatário, que chama um procedimento armazenado periodicamente que gera a carga de saudação. Olá carga níveis (eDTUs), a duração e os intervalos variam em todos os bancos de dados, simulando a atividade de locatário imprevisível.

1. Abrir... \\Módulos de aprendizado\\gerenciamento e monitoramento do desempenho de\\*demonstração PerformanceMonitoringAndManagement.ps1* em Olá *PowerShell ISE*. Mantenha esse script aberto pois você executará vários cenários durante este tutorial.
1. Defina **$DemoScenario** = **2**, *Gerar uma carga de intensidade normal*.
1. Pressione **F5** tooapply tooall uma carga de seus bancos de dados de locatário.

Wingtip é um aplicativo SaaS e carga do Olá mundo real em um aplicativo SaaS normalmente é esporádica e imprevisível. toosimulate isso, Olá carga gerador produz uma carga aleatória distribuída em todos os locatários. Vários minutos são necessários para Olá carga padrão tooemerge, portanto, execute gerador de carga Olá por 3 a 5 minutos antes de tentar toomonitor Olá carga no hello seções a seguir.

> [!IMPORTANT]
> Gerador de carga Hello está em execução como uma série de trabalhos na sessão do PowerShell local. Lembre-Olá *PerformanceMonitoringAndManagement.ps1 demonstração* guia Abrir! Se você fechar a guia hello, ou suspender sua máquina, gerador de carga hello interrompe. Gerador de carga Olá permanece em um *invocar trabalho* estado em que ele gera carga em quaisquer novos locatários que são provisionados depois do início do gerador de saudação. Use *Ctrl-C* toostop invocar novos trabalhos e saída Olá script. Gerador de carga Olá continuará toorun, mas apenas em locatários existentes.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Monitorar o uso de recursos usando Olá portal do Azure

uso de recursos do hello toomonitor resultados da saudação carregar sendo aplicadas, abrir o pool de toohello portal de saudação que contém os bancos de dados de locatário de saudação:

1. Olá abrir [portal do Azure](https://portal.azure.com) e procurar toohello *tenants1 -&lt;usuário&gt;*  server.
1. Role para baixo e localize os pools elásticos e clique em **Pool1**. Este pool contém todos os Olá locatário bancos de dados foi criados.

Observar Olá **monitoramento de pool Elástico** e **monitoramento de banco de dados Elástico** gráficos.

Olá, utilização de recursos do pool é utilização do banco de dados de agregação Olá para todos os bancos de dados no pool de saudação. gráfico de banco de dados de saudação mostra Olá cinco principais bancos de dados:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Porque há bancos de dados adicionais no pool de saudação além Olá cinco principais, utilização do pool de saudação mostra a atividade que não será refletida no gráfico de cinco bancos de dados principais hello. Para obter mais detalhes, clique em **Utilização de Recursos do Banco de Dados**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Configurar alertas de desempenho de pool de saudação

Definir um alerta em pool Olá aciona em \>75% de utilização da seguinte maneira:

1. Abra *Pool1* (em Olá *tenants1 -\<usuário\>*  servidor) no hello [portal do Azure](https://portal.azure.com).
1. Clique em **Regras de Alerta** e, em seguida, clique em **+ Adicionar alerta**:

   ![adicionar alerta](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Forneça um nome, como **Alto DTU**,
1. Saudação de conjunto de valores a seguir:
   * **Métrica = percentual de eDTU**
   * **Condição = maior que**.
   * **Limite = 75**.
   * **Período = sobre Olá últimos 30 minutos**.
1. Adicionar um toohello de endereço de email *administrador adicional email(s)* caixa e clique em **Okey**.

   ![definir alerta](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Escalar verticalmente um pool ocupado

Se o nível de carga de agregação de saudação aumenta em um ponto de toohello do pool que dá o máximo de pool hello e atingir 100% de uso de eDTU, desempenho de banco de dados individual é afetado, potencialmente reduzindo os tempos de resposta de consulta para todos os bancos de dados no pool de saudação.

**Curto prazo**, considere a possibilidade de dimensionar os recursos adicionais do hello pool tooprovide ou removendo bancos de dados do pool de saudação (movendo-os pools de tooother ou fora da camada de serviço autônoma Olá pool tooa).

**Longo prazo**, considere otimizar consultas ou o índice de desempenho de banco de dados de tooimprove de uso. Dependendo da saudação tooperformance de sensibilidade do aplicativo emite seu tooscale de prática recomendada um pool de backup antes de atingir 100% de uso de eDTU. Use um alerta toowarn você com antecedência.

Você pode simular um pool de ocupado pelo aumento da carga Olá produzido pelo gerador de saudação. Causando Olá tooburst de bancos de dados com mais frequência e para carga de agregação hello mais longo, aumentando em pool Olá sem alterações de requisitos de saudação de bancos de dados individuais hello. Expansão do pool de saudação é feito facilmente no portal de saudação ou do PowerShell. Este exercício usa o portal de saudação.

1. Definir *$DemoScenario* = **3**, _gerar carga com intermitências mais e mais frequentes por banco de dados_ tooincrease intensidade de saudação de carga de agregação Olá no pool de saudação sem alterar a carga de pico Olá exigida por cada banco de dados.
1. Pressione **F5** tooapply tooall uma carga de seus bancos de dados de locatário.

1. Vá muito**Pool1** em Olá portal do Azure.

Olá monitor maior uso de eDTU do pool no gráfico superior hello. Leva alguns minutos para Olá novo maior carga tookick, mas você deve ver rapidamente pool Olá iniciar utilização máxima toohit e como carga Olá steadies no padrão de novos hello, rapidamente sobrecarrega pool hello.

1. tooscale pool hello, clique em **configurar pool** na parte superior de saudação do hello **Pool1** página.
1. Ajustar Olá **eDTU de Pool** configuração muito**100**. Alterar o eDTU do pool de saudação não alterar Olá por banco de dados (que ainda é 50 eDTU máximo por banco de dados). Ver configurações do hello por banco de dados no lado direito de saudação do hello **configurar pool** página.
1. Clique em **salvar** pool de saudação do toosubmit Olá solicitação tooscale.

Voltar muito**Pool1** > **visão geral** tooview Olá gráficos de monitoramento. Monitore o efeito de saudação do fornecimento de pool de saudação com mais recursos (embora com alguns bancos de dados e uma carga aleatória nem sempre é fácil toosee conclusivamente até que seja executado por algum tempo). Enquanto você está vendo hello gráficos tenha em mente que 100% em Olá superior agora o gráfico representa 100 eDTUs, enquanto no hello gráfico 100% inferior é ainda 50 eDTUs como Olá por banco de dados max ainda é 50 eDTUs.

Bancos de dados permanecem online e totalmente disponível durante o processo de saudação. Em Olá último momento como cada banco de dados está pronto toobe habilitado com hello novo eDTU do pool, qualquer conexão ativa foram interrompido. Código do aplicativo deve sempre ser gravado conexões tooretry descartado e, portanto, reconectará toohello banco de dados no pool do hello expandidos.

## <a name="load-balance-between-pools"></a>Balancear carga entre pools

Como uma alternativa tooscaling pool hello, crie um pool de segundo e mover bancos de dados para ela toobalance Olá carregar entre hello dois pools. toodo este novo pool de saudação deve ser criado em Olá Olá mesmo servidor primeiro.

1. Em Olá [portal do Azure](https://portal.azure.com), abra Olá **tenants1 -&lt;usuário&gt;**  server.
1. Clique em **+ novo pool** toocreate um pool no servidor de saudação atual.
1. Em Olá **pool Elástico de banco de dados** modelo:

    1. Definir **nome** muito*Pool2*.
    1. Deixe Olá preço como **Pool padrão**.
    1. Clique em **Configurar pool**,
    1. Definir **eDTU de Pool** muito*eDTU 50*.
    1. Clique em **adicionar bancos de dados** toosee uma lista de bancos de dados no servidor de saudação que podem ser adicionados muito*Pool2*.
    1. Selecione qualquer toomove 10 bancos de dados essas toohello novo pool e, em seguida, clique em **selecione**. Se você executa o gerador de carga hello, serviço Olá já sabe que o perfil de desempenho exige um pool maior que tamanho de eDTU 50 saudação padrão e recomenda que você comece com uma configuração de eDTU 100.

    ![recomendação](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Para este tutorial, mantenha o padrão de saudação em 50 eDTUs e clique em **selecione** novamente.
    1. Selecione **Okey** toocreate Olá novo pool e toomove Olá bancos de dados selecionados para ele.

Criar pool de saudação e mover bancos de dados Olá leva alguns minutos. Como bancos de dados são movidos permaneçam online e acessível até o último momento de hello, no ponto em que todas as conexões abertas são fechadas. Contanto que você tenha alguma lógica de repetição, clientes, em seguida, conectará toohello banco de dados no novo pool de saudação.

Procurar muito**Pool2** (em Olá *tenants1* server) tooopen Olá pool e monitorar o desempenho. Se você não estiver visível, aguarde o provisionamento de saudação novo pool toocomplete.

Agora você vê que o uso de recursos do *Pool1* caiu e que o *Pool2* é carregado de maneira semelhante.

## <a name="manage-performance-of-a-single-database"></a>Gerenciar o desempenho de um banco de dados individual

Se um único banco de dados em um pool de apresentar uma alta carga sustentável, dependendo da configuração do pool de Olá, ele pode tendem a recursos de saudação toodominate no pool de saudação e afetar outros bancos de dados. Se a atividade de saudação é provavelmente toocontinue por algum tempo, o banco de dados de saudação pode ser movido temporariamente fora do pool de saudação. Isso permite Olá Olá de toohave do banco de dados de recursos extras necessárias e isola da saudação outros bancos de dados.

Este exercício simula o efeito de saudação de Contoso conjunto Hall apresentando uma alta carga quando tíquetes de venda para um conjunto popular.

1. Olá abrir... \\ *Demonstração PerformanceMonitoringAndManagement.ps1* script.
1. Defina **$DemoScenario = 5, Gerar uma carga normal e uma carga alta em um locatário único (aprox. 95 DTU).**
1. Defina **$SingleTenantDatabaseName = contosoconcerthall**
1. Executar usando o script hello **F5**.


1. Em Olá [portal do Azure](https://portal.azure.com) abrir **Pool1**.
1. Inspecionar Olá **monitoramento de pool Elástico** do gráfico e procure Olá maior uso de eDTU do pool. Depois de um ou dois minutos, uma carga maior Olá deve começar tookick no, e você deverá ver rapidamente pool Olá atinge 100% de utilização.
1. Inspecionar Olá **monitoramento de banco de dados Elástico** exibição que mostra bancos de dados principais Olá Olá última hora. Olá *contosoconcerthall* banco de dados em breve deve aparecer como um Olá cinco principais bancos de dados.
1. **Clique em monitoramento de banco de dados Elástico Olá** **gráfico** e ele abre Olá **utilização de recursos de banco de dados** página onde você pode monitorar qualquer um dos bancos de dados de saudação. Isso lhe permite isolar exibição Olá para Olá *contosoconcerthall* banco de dados.
1. Na lista de saudação de bancos de dados, clique em **contosoconcerthall**.
1. Clique em **preço (escala DTUs)** tooopen Olá **Configure desempenho** página onde você pode definir um nível de desempenho independente do banco de dados de saudação.
1. Clique em Olá **padrão** guia Opções de escala de saudação tooopen na camada padrão hello.
1. Deslize Olá **controle deslizante DTU** tooright tooselect **100** DTUs. Observe que isso corresponde toohello objetivo de serviço, **S3**.
1. Clique em **aplicar** toomove Olá fora do pool de saudação do banco de dados e torná-lo um *Standard S3* banco de dados.
1. Depois que o dimensionamento é concluída, monitor Olá efeito no banco de dados do hello contosoconcerthall e Pool1 em folhas Elásticos Olá pool e o banco de dados.

Depois que a alta carga Olá no banco de dados de contosoconcerthall Olá diminuir devolva-toohello pool tooreduce seu custo. Se não está claro ao que acontece você pode definir um alerta no banco de dados de saudação que irá disparar quando o uso DTU está abaixo da saudação por banco de dados max em pool hello. Mover um banco de dados para um pool é descrito no exercício 5.

## <a name="other-performance-management-patterns"></a>Outros padrões de gerenciamento de desempenho

**Dimensionamento preventivo** exercício Olá acima em que você usou como tooscale um banco de dados isolado, você sabia que toolook de banco de dados para. Se o gerenciamento de saudação do Contoso conjunto Hall tinha informado Wingtips de venda de tíquete iminente Olá, banco de dados de saudação pode ter sido movido fora do pool de saudação preventivamente. Caso contrário, ele provavelmente exigiria um alerta no pool de saudação ou Olá toospot de banco de dados que estava acontecendo. Você não quer toolearn sobre isso da saudação outros locatários em Olá pool reclama degradação do desempenho. E se o locatário Olá pode prever quanto tempo eles precisarão recursos adicionais, você pode configurar uma automação do Azure runbook toomove Olá banco de dados fora do pool de saudação e, em seguida, volte outra vez em um agendamento definido.

**Dimensionamento de autoatendimento de locatário** como dimensionamento é uma tarefa chamada facilmente por meio da API de gerenciamento Olá, você pode facilmente criar bancos de dados de locatário tooscale de capacidade de saudação em seu aplicativo de voltada para o locatário e oferecê-lo como um recurso de seu serviço de SaaS. Por exemplo, permitem que os locatários self-administer dimensionamento para cima e para baixo, talvez vinculados diretamente a cobrança tootheir!

**Dimensionando um pool de cima para baixo nos padrões de uso de toomatch agenda**

Quando o uso de agregação locatário segue os padrões de uso previsível, você pode usar automação do Azure tooscale um pool para cima e para baixo em uma agenda. Por exemplo, reduzir um pool verticalmente após as 18h e escalar verticalmente novamente antes das 6h em dias da semana nos quais você sabe que há uma queda nos requisitos de recursos.



## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Simule o uso em bancos de dados de locatário Olá executando um gerador de carga fornecido
> * Bancos de dados de locatário de saudação do monitor como eles respondem toohello aumento na carga
> * Dimensionar o hello pool Elástico em resposta toohello maior banco de dados de carga
> * Provisionar uma segunda atividade de banco de dados do pool Elástico tooload saldo Olá

[Tutorial para restaurar um locatário único](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais que se baseiam na Olá implantação de aplicativos SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Pools elásticos do SQL](sql-database-elastic-pool.md)
* [Automação do Azure](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) – Tutorial de configuração e uso do Log Analytics
