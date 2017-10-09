---
title: "aaaUse análise de Log com um aplicativo de multilocatário do banco de dados SQL | Microsoft Docs"
description: "Configurar e usar a análise de Log (OMS) com o aplicativo de SaaS Wingtip de exemplo hello Azure SQL Database"
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
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Configurar e usar a análise de Log (OMS) com o aplicativo de SaaS Wingtip Olá

Neste tutorial, você configura e usa o *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* para monitorar pools elásticos e bancos de dados. Ele se baseia no hello [tutorial de gerenciamento e monitoramento do desempenho de](sql-database-saas-tutorial-performance-monitoring.md)e mostra como toouse *análise de Log* tooaugment Olá monitoramento e alertas fornecido no hello portal do Azure. O Log Analytics é especialmente adequado para monitoramento e alertas em grande escala, porque ele dá suporte a centenas de pools e centenas de milhares de bancos de dados. Ele também fornece uma única solução de monitoramento, que pode integrar o monitoramento de diferentes aplicativos e serviços do Azure, entre várias assinaturas do Azure.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Instalar e configurar o Log Analytics (OMS)
> * Usar pools de toomonitor de análise de logs e bancos de dados

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

Consulte Olá [tutorial de gerenciamento e monitoramento do desempenho de](sql-database-saas-tutorial-performance-monitoring.md) para obter uma discussão de cenários de SaaS hello e padrões e como eles afetam os requisitos de saudação em uma solução de monitoramento.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Monitoramento e gerenciamento de desempenho com o Log Analytics (OMS)

Para o Banco de Dados SQL, o monitoramento e o alerta estão disponíveis em bancos de dados e pools. Este interna de monitoramento e alertas é específico do recurso e conveniente para pequenas quantidades de recursos, mas é menos toomonitoring adequado grandes instalações ou para fornecer uma exibição unificada entre assinaturas e recursos diferentes.

Para cenários de alto volume, o Log Analytics pode ser usado. Este é um serviço do Azure separado que fornece análise sobre logs de diagnóstico emitido e telemetria coletada em um espaço de trabalho de análise de log, que pode coletar a telemetria de muitos serviços e ser usado tooquery e definir alertas. O Log Analytics fornece uma linguagem de consulta e ferramentas de visualização de dados internas que permitem a visualização e análise de dados operacionais. Olá solução de análise do SQL fornece vários predefinido pool Elástico e o banco de dados de monitoramento e alertas de exibições e consultas e permite que você adicione suas próprias consultas ad hoc e salvá-los conforme necessário. O OMS também fornece um designer de exibição personalizado.

Soluções de análise e espaços de trabalho de análise de log podem ser abertas no hello portal do Azure e no OMS. Olá portal do Azure é o ponto de acesso mais recente Olá, mas pode estar por trás do portal do OMS Olá em algumas áreas.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Iniciar Olá carga gerador toocreate dados tooanalyze

1. Abra **demonstração PerformanceMonitoringAndManagement.ps1** em Olá **PowerShell ISE**. Mantenha esse script aberta, talvez você queira toorun vários dos cenários de geração de carga Olá durante este tutorial.
1. Se você tiver menos de cinco locatários, provisione um lote de locatários tooprovide um contexto de monitoramento mais interessante:
   1. Defina **$DemoScenario = 1,** **Provisionar um lote de locatários**
   1. Pressione **F5** toorun script de saudação.

1. Defina **$DemoScenario** = 2, **Gerar carga de intensidade normal (aproximadamente 40 DTU)**.
1. Pressione **F5** toorun script de saudação.

## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Olá Wingtip tíquetes scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. Arquivos de script estão localizados em Olá [pasta módulos de aprendizado](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Baixar Olá **módulos de aprendizado** pasta tooyour computador local, mantendo sua estrutura de pasta.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Instalar e configurar a análise de Log e Olá solução de análise do SQL Azure

Análise de log é um serviço separado que precisa toobe configurado. O Log Analytics coleta dados de log e telemetria e métrica em um espaço de trabalho de Log Analytics. Um espaço de trabalho é um recurso, assim como outros recursos no Azure e deve ser criado. Enquanto não precisa de um espaço de trabalho de saudação toobe criado no hello mesmo grupo de recursos como aplicativos de saudação que está monitorando, isso torna hello mais sentido. No caso de saudação do aplicativo de SaaS Wingtip hello, isso permite que toobe de espaço de trabalho Olá facilmente excluído com o aplicativo hello simplesmente excluindo grupo de recursos de saudação.

1. Abrir... \\Módulos de aprendizado\\gerenciamento e monitoramento do desempenho de\\análise de Log\\*demonstração LogAnalytics.ps1* em Olá **PowerShell ISE**.
1. Pressione **F5** toorun script de saudação.

Agora você deve ser capaz de análise de Log abertos no portal do Azure hello (ou portal do OMS Olá). Levará alguns minutos para toobe de telemetria coletados no espaço de trabalho de análise de Log hello e toobecome visível. será Hello mais que deixar o sistema Olá coleta dados Olá experiência de hello mais interessante. Agora é um bom momento toograb bebidas - apenas certifique-se de gerador de carga Olá ainda está em execução!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Use a análise de Log e Olá bancos de dados e pools de toomonitor de solução de análise do SQL


Neste exercício, abra a análise de Log e Olá toolook portal do OMS em Telemetria Olá sendo coletada pools de bancos de dados e hello.

1. Procurar toohello [portal do Azure](https://portal.azure.com) , abra a análise de Log clicando mais serviços e procure a análise de Log:

   ![abrir log analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Selecionar espaço de trabalho de saudação denominado *wtploganalytics -&lt;usuário&gt;*.

1. Selecione **visão geral** tooopen Olá solução de análise de Log em Olá portal do Azure.
   ![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **IMPORTANTE**: pode levar alguns minutos antes de saudação solução está ativa. Tenha paciência!

1. Clique em Olá tooopen do bloco de análise do SQL Azure.

    ![visão geral](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![análise](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Olá exibição no hello solução blade rola para os lados com sua própria barra de rolagem na parte inferior do hello (atualização Olá folha se necessário).

1. Explorar Olá várias exibições clicando neles ou em recursos individuais tooopen um Gerenciador de busca detalhada, onde você pode usar o controle deslizante de tempo Olá no hello superior esquerda ou clique na vertical barra toofocus em um intervalo de tempo mais estreito. Com essa exibição, você pode selecionar toofocus individuais de bancos de dados ou os pools de recursos específicos:

    ![gráfico](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. Volta na folha de solução de hello, se você rolar toohello extrema direita você verá algumas consultas salvas que você pode clicar em tooopen e explorar. Você pode tentar modificar essas consultas e salvar as consultas interessantes que produzir, as quais você poderá abrir novamente e usar com outros recursos.

1. Volta na folha de espaço de trabalho de análise de Log de hello, selecione solução de saudação de tooopen Portal do OMS existe.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. No portal do OMS hello, você pode configurar alertas. Clique na parte de alerta de saudação do banco de dados Olá exibição DTU.

1. Saudação de pesquisa de Log de modo de exibição que aparece, você verá um gráfico de barras das métricas de saudação que está sendo representados.

    ![pesquisa do log](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Se você clicar no alerta, na barra de ferramentas de saudação você será capaz de toosee configuração de alerta de saudação e pode alterá-la.

    ![adicionar regra de alerta](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Olá, monitoramento e alertas em análise de Log e o OMS se baseia em consultas em dados Olá no espaço de trabalho hello, diferentemente de saudação alertas em cada folha de recursos, que é específico do recurso. Portanto, você pode definir um alerta que examina todos os bancos de dados, digamos, em vez de definir um alerta por banco de dados. Ou escrever um alerta que usa uma consulta composta sobre vários tipos de recurso. Consultas só são limitadas por dados Olá disponíveis no espaço de trabalho de saudação.

Análise de log do banco de dados SQL é cobrado com base no volume de dados Olá no espaço de trabalho de saudação. Neste tutorial, você criou um espaço livre, que é too500MB limitado por dia. Quando esse limite é atingido dados não são adicionados toohello espaço de trabalho.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Instalar e configurar o Log Analytics (OMS)
> * Usar pools de toomonitor de análise de logs e bancos de dados

[Tutorial de análise de locatário](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Recursos adicionais

* [Tutoriais adicionais que se baseiam na implantação de aplicativos SaaS Wingtip inicial Olá](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
