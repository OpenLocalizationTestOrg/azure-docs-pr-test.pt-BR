---
title: "aaaGet iniciado com as ferramentas de banco de dados Elástico | Microsoft Docs"
description: "Explicação básica do recurso de ferramentas de banco de dados Elástico de saudação do banco de dados do SQL Azure, incluindo um aplicativo de exemplo para executar."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Introdução às ferramentas do Banco de Dados Elástico
Este documento apresenta a experiência do desenvolvedor toohello, ajudando você a aplicativo de exemplo hello toorun. exemplo Hello cria um aplicativo simples de fragmentada e explora os principais recursos das ferramentas de banco de dados Elástico. exemplo Hello demonstra funções de saudação [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md).

biblioteca de saudação tooinstall, ir muito[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). biblioteca de saudação é instalada com o aplicativo de exemplo hello descrito Olá seção a seguir.

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2012 ou posterior com C#. Baixe a versão gratuita em [Downloads do Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 ou posterior. versão mais recente do tooget hello, consulte [instalando NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Baixe e execute o aplicativo de exemplo hello
Olá **Elástico ferramentas de banco de dados do SQL Azure - Introdução** aplicativo de exemplo ilustra os aspectos mais importantes de saudação da experiência de desenvolvimento Olá fragmentados aplicativos que usam as ferramentas de banco de dados Elástico. Ele se concentra nos principais casos de uso para [gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md), [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e [consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md). toodownload e exemplo de execução hello, siga estas etapas: 

1. Baixar Olá [Elástico ferramentas de banco de dados do SQL Azure - exemplo de Introdução](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) do MSDN. Descompacte Olá exemplo tooa de local de sua escolha.

2. toocreate um projeto, abra Olá **ElasticScaleStarterKit.sln** solução da saudação **c#** directory.

3. Solução Olá para o projeto de exemplo hello, abra Olá **App. config** arquivo. Siga as instruções de Olá Olá arquivo tooadd o nome do seu servidor de banco de dados SQL e suas informações de logon (nome de usuário e senha).

4. Compilar e executar o aplicativo hello. Quando solicitado, ative os pacotes do NuGet Visual Studio toorestore Olá de solução de saudação. Isso baixa a versão mais recente Olá Olá Elástico de banco de dados da biblioteca de cliente do NuGet.

5. Experimentar Olá diferentes opções toolearn mais informações sobre recursos de biblioteca de cliente hello. Observe etapas Olá Olá leva de aplicativo na saída do console hello e se sentir livre tooexplore Olá código em segundo plano da saudação.
   
    ![Andamento][4]

Parabéns -- você criou e executou com sucesso seu primeiro aplicativo fragmentado usando as ferramentas de banco de dados elástico no Banco de Dados SQL. Use o Visual Studio ou o SQL Server Management Studio tooconnect tooyour banco de dados SQL e dar uma olhada rápida em fragmentos Olá que Olá exemplo criado. Você observará que novos bancos de dados de fragmento de exemplo e um banco de dados do Gerenciador de mapa do fragmento exemplo hello criou.

> [!IMPORTANT]
> É recomendável que você sempre usar a versão mais recente saudação do Management Studio para que você fique sincronizado com atualizações tooAzure e banco de dados SQL. [Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Informações importantes de código de exemplo hello
* **Gerenciamento de fragmentos e fragmentos de mapas**: hello código ilustra como toowork com fragmentos, intervalos e mapeamentos no arquivo hello **ShardManagementUtils.cs**. Para obter mais informações, consulte [expansão de bancos de dados com o Gerenciador do mapa de fragmentos Olá](http://go.microsoft.com/?linkid=9862595).  

* **Roteamento dependente de dados**: roteamento de fragmento direito de toohello de transações é mostrado na **DataDependentRoutingSample.cs**. Para obter mais detalhes, veja [Roteamento dependente de dados](http://go.microsoft.com/?linkid=9862596). 

* **Consultas em vários fragmentos**: consultando através de fragmentos é ilustrado no arquivo hello **MultiShardQuerySample.cs**. Para saber mais, confira [Consulta de vários fragmentos](http://go.microsoft.com/?linkid=9862597).

* **Adicionando fragmentos vazios**: Olá iterativo de adição de novos fragmentos vazios é executada pelo código de saudação no arquivo hello **CreateShardSample.cs**. Para obter mais informações, consulte [expansão de bancos de dados com o Gerenciador do mapa de fragmentos Olá](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Outras operações da escala elástica
* **Dividindo um fragmento existente**: fragmentos de toosplit recurso Olá é fornecido pelo Olá **ferramenta de mesclagem de divisão**. Para saber mais, confira [Mover dados entre bancos de dados na nuvem escalados horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md).

* **Mesclando os fragmentos existentes**: mesclagens de fragmento também são executadas usando Olá **ferramenta de mesclagem de divisão**. Para saber mais, confira [Mover dados entre bancos de dados na nuvem escalados horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Custo
ferramentas de banco de dados Elástico Olá são gratuitas. Quando você usar ferramentas de banco de dados Elástico, você não recebe encargos adicionais sobre o custo de saudação do uso do Azure. 

Por exemplo, o aplicativo de exemplo hello cria novos bancos de dados. custo de saudação para isso depende de edição do banco de dados SQL Olá que você escolher e hello uso do Azure do seu aplicativo.

Para obter informações sobre os preços, veja [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre as ferramentas de banco de dados Elástico, consulte Olá páginas a seguir:

* Exemplos de código: 
  * [Ferramentas de Banco de Dados Elástico para Azure SQL - Introdução](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Ferramentas de Banco de Dados Elástico para SQL Azure – Integração ao Entity Framework](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [Elasticidade do fragmento no Script Center](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog: [Anúncio da escala elástica](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [implementando Scale-Out usando fragmentação com hello vídeo de biblioteca de cliente de banco de dados Elástico](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Channel 9: [Visão geral da Escala Elástica](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Fórum de discussão: [Fórum do Banco de Dados SQL do Azure](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* desempenho toomeasure: [contadores de desempenho para o Gerenciador do mapa de fragmentos](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

