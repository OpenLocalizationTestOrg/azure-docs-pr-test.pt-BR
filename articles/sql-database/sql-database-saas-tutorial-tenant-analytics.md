---
title: "consultas de análise de aaaRun em vários bancos de dados SQL do Azure | Microsoft Docs"
description: "Extrair dados de bancos de dados de locatário para um banco de dados analítico para análise offline"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Extrair dados de bancos de dados de locatário para um banco de dados analítico para análise offline

Neste tutorial, você deve usar um trabalho de Elástico toorun consulta cada banco de dados de locatário. trabalho de saudação extrai dados de vendas de tíquete e carrega-os em um banco de dados de análise (ou data warehouse) para análise. Olá banco de dados de análise é então consultada insights tooextract dos dados operacionais diários de todos os locatários.


Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar banco de dados de análise de locatário Olá
> * Criar um trabalho agendado de tooretrieve de dados e popular o banco de dados de análise de saudação

toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir forem atendidas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* versão mais recente de saudação do SQL Server Management Studio (SSMS) está instalado. [Baixar e Instalar o SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Padrão de Análise Operacional do Locatário

Um dos grandes oportunidades Olá com aplicativos SaaS é dados de locatário sofisticado de saudação toouse que são armazenados na nuvem hello. Use este insights toogain de dados em operação hello e uso de seu aplicativo e seus locatários. Esses dados podem guia de desenvolvimento de recursos, aprimoramentos de usabilidade e outros investimentos em aplicativo hello e plataforma. É fácil acessar esses dados quando estiverem em um único banco de dados multilocatário, mas não tão fácil quando são distribuídos em escala por, potencialmente, milhares de bancos de dados. Tooaccessing de uma abordagem esses dados são trabalhos Elástico toouse, que permitem que os resultados da consulta retorna resultados de toobe de execução do trabalho capturados em um banco de dados de saída e a tabela.

## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Implantar um banco de dados de resultados de análise de locatário

Este tutorial requer toohave que Olá de toocapture implantado um banco de dados resultante da execução do trabalho de scripts, que contêm consultas retornam resultados. Vamos criar um banco de dados chamado tenantanalytics para essa finalidade.

1. Abrir... \\Módulos de aprendizado\\análise operacional\\locatário análise\\*demonstração TenantAnalyticsDB.ps1* em Olá *PowerShell ISE* e defina Olá seguinte valor:
   * **$DemoScenario** = **2** *Implantar banco de dados de análise operacional*
1. Pressione **F5** script de demonstração toorun hello (Olá que chamadas *TenantAnalyticsDB.ps1 implantar* script) que cria o banco de dados de análise de locatário hello.

## <a name="create-some-data-for-hello-demo"></a>Criar alguns dados de demonstração de Olá

1. Abrir... \\Módulos de aprendizado\\análise operacional\\locatário análise\\*demonstração TenantAnalyticsDB.ps1* em Olá *PowerShell ISE* e defina Olá seguinte valor:
   * **$DemoScenario** = **1** *Comprar ingressos para eventos em todos os locais*
1. Pressione **F5** toorun Olá script e criar o tíquete de histórico de compras.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Criar uma análise de locatário do trabalho agendado tooretrieve sobre compras de tíquete

Esse script cria um informações de compra de tíquete de tooretrieve de trabalho de todos os locatários. Quando agregados em uma única tabela, você pode obter métricas criteriosos avançadas sobre padrões de compra por locatários Olá de tíquete.

1. Abra o SSMS e conecte-se toohello catálogo -&lt;usuário&gt;. servidor t
1. Abra... \\Módulos de Aprendizado\\Análise Operacional\\Locatário Análise\\*TicketPurchasesfromAllTenants.sql*
1. Modificar &lt;usuário&gt;, use o nome de usuário de Olá usado quando você implantou o aplicativo de SaaS Wingtip Olá na parte superior de saudação do script hello, **sp\_adicionar\_destino\_grupo\_membro** e **sp\_adicionar\_jobstep**
1. Clique com botão direito, selecione **Conexão**e conecte-se toohello catálogo -&lt;usuário&gt;. t server, se ainda não estiver conectado
1. Certifique-se de que você está conectado toohello **jobaccount** banco de dados e pressione **F5** para executar o script hello

* **SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino Olá *TenantGroup*, agora precisamos tooadd membros de destino.
* **SP\_adicionar\_destino\_grupo\_membro** adiciona um *server* tipo de membro, o que considerar todos os bancos de dados nesse servidor (note que esta é Olá customer1 - de destino &lt;Usuário&gt; que contém os bancos de dados de locatário de saudação do servidor) em tempo de trabalho de execução deve ser incluída no trabalho de saudação.
* **sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "Compras de Tíquetes de todos os Locatários"
* **SP\_adicionar\_jobstep** cria todas as informações de compra de tíquete de saudação de etapa de trabalho de saudação contendo tooretrieve de texto do comando T-SQL de todos os locatários e Olá cópia retornando o conjunto de resultados em uma tabela chamada  *AllTicketsPurchasesfromAllTenants*
* Olá restantes no script hello exibem existência de saudação de objetos hello e execução do trabalho de monitor. Examine o valor de status de saudação do hello **ciclo de vida** status da coluna toomonitor hello. Uma vez, foi bem-sucedida, trabalho de saudação foi concluído com êxito em todos os bancos de dados de locatário e dois bancos de dados adicionais contendo Olá Olá referenciam tabela.

Executado com êxito o script hello deve resultar em resultados semelhantes:

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Criar um tooretrieve de trabalho, um resumo da contagem de tíquete de compras de todos os locatários

Esse script cria uma soma de tooretrieve de trabalho de todas as aquisições do tíquete de todos os locatários.

1. Abra o SSMS e conecte-se toohello *catálogo -&lt;usuário&gt;. t* server
1. Arquivo hello abrir... \\Módulos de aprendizado\\provisionar e catálogo\\análise operacional\\locatário análise\\*TicketPurchasesfromAllTenants.sql resultados*
1. Modificar &lt;usuário&gt;, use o nome de usuário Olá usado quando você implantou o aplicativo de SaaS Wingtip Olá no script hello, em hello **sp\_adicionar\_jobstep** procedimento armazenado
1. Clique com botão direito, selecione **Conexão**e conecte-se toohello catálogo -&lt;usuário&gt;. t server, se ainda não estiver conectado
1. Certifique-se de que você está conectado toohello **tenantanalytics** banco de dados e pressione **F5** para executar o script hello

Executado com êxito o script hello deve resultar em resultados semelhantes:

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "ResultsTicketsOrders"

* **SP\_adicionar\_jobstep** cria todas as informações de compra de tíquete de saudação de etapa de trabalho de saudação contendo tooretrieve de texto do comando T-SQL de todos os locatários e retornando o conjunto de resultados em uma tabela chamada CountofTicketOrders de saudação de cópia

* Olá restantes no script hello exibem existência de saudação de objetos hello e execução do trabalho de monitor. Examine o valor de status de saudação do hello **ciclo de vida** status da coluna toomonitor hello. Uma vez, foi bem-sucedida, trabalho de saudação foi concluído com êxito em todos os bancos de dados de locatário e dois bancos de dados adicionais contendo Olá Olá referenciam tabela.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Implantar um banco de dados de análise do locatário
> * Criar uma tarefa agendada tooretrieve de dados analíticos por locatários

Parabéns!

## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais que se baseiam na Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Trabalhos Elásticos](sql-database-elastic-jobs-overview.md)
