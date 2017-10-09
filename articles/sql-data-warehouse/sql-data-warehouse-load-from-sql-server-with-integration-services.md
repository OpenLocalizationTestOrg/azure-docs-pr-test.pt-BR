---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (SSIS) | Microsoft Docs
description: Mostra como toocreate um SQL Server Integration Services (SSIS) pacote toomove os dados de uma ampla variedade de dados de fontes tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Carregar dados do SQL Server no Azure SQL Data Warehouse (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Crie um SQL Server Integration Services (SSIS) pacote tooload de dados do SQL Server para o Azure SQL Data Warehouse. Você pode opcionalmente reestruturar, transformar e limpar dados saudação conforme ele passa pelo fluxo de dados do SSIS hello.

Neste tutorial, você irá:

* Criar um novo projeto do Integration Services no Visual Studio.
* Conecte-se toodata fontes, inclusive SQL Server (como uma fonte) e SQL Data Warehouse (como um destino).
* Crie um pacote do SSIS que carrega dados de origem de saudação em destino hello.
* Execute Olá SSIS pacote tooload Olá dados.

Este tutorial usa o SQL Server como fonte de dados de saudação. O SQL Server pode estar em execução local ou em uma máquina virtual do Azure.

## <a name="basic-concepts"></a>Conceitos básicos
pacote de saudação é a unidade de saudação do trabalho no SSIS. Os pacotes relacionados são agrupados em projetos. Você cria projetos e pacotes de design no Visual Studio com o SQL Server Data Tools. design de saudação é um processo visual na qual você pode arrastar e soltar componentes da superfície de design de toohello de caixa de ferramentas Olá, conectá-los e definir suas propriedades. Depois de concluir seu pacote, você pode, opcionalmente, implantá-lo tooSQL Server para o gerenciamento abrangente, monitoramento e segurança.

## <a name="options-for-loading-data-with-ssis"></a>Opções de carregamento de dados com o SSIS
O SSIS (SQL Server Integration Services) é um conjunto flexível de ferramentas que fornece uma variedade de opções para se conectar a e carregar dados no SQL Data Warehouse.

1. Use um tooSQL tooconnect de destino do ADO NET Data Warehouse. Este tutorial usa um destino do ADO NET porque ela tem Olá menos opções de configuração.
2. Use um tooSQL tooconnect do destino OLE DB Data Warehouse. Esta opção pode fornecer desempenho ligeiramente melhor do que Olá destino ADO NET.
3. Use dados de saudação de toostage de tarefa de carregamento de BLOBs do Azure Olá no armazenamento de BLOBs do Azure. Em seguida, use Olá SSIS executar SQL tarefa toolaunch um script de Polybase que carrega dados saudação em SQL Data Warehouse. Essa opção fornece melhor desempenho Olá Olá três opções listadas aqui. Olá tooget tarefa de Upload do Blob do Azure, baixe Olá [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn mais sobre o Polybase, consulte [guia do PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Antes de começar
toostep este tutorial, você precisa:

1. **SSIS (SQL Server Integration Services)**. O SSIS é um componente do SQL Server e requer uma versão de avaliação ou uma versão licenciada do SQL Server. tooget uma versão de avaliação do SQL Server 2016 Preview, consulte [avaliações do SQL Server][SQL Server Evaluations].
2. **Visual Studio**. tooget Olá livre Visual Studio Community Edition, consulte [Visual Studio Community][Visual Studio Community].
3. **SSDT (SQL Server Data Tools) para Visual Studio**. tooget SQL Server Data Tools para Visual Studio, consulte [baixar SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Dados de exemplo**. Este tutorial usa dados de exemplo armazenados no SQL Server no banco de dados do exemplo hello AdventureWorks como Olá toobe de dados de origem carregado no SQL Data Warehouse. Olá tooget banco de dados de exemplo AdventureWorks, consulte [bancos de dados de exemplo do AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Um banco de dados e permissões do SQL Data Warehouse**. Este tutorial se conecta a instância do SQL Data Warehouse tooa e carrega dados nele. Você tem uma tabela e tooload dados toohave permissões toocreate.
6. **Uma regra de firewall**. Você tem toocreate uma regra de firewall no SQL Data Warehouse com o endereço IP de saudação do computador local antes de carregar dados toohello SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Etapa 1: Criar um novo projeto do Integration Services
1. Inicie o Visual Studio.
2. Em Olá **arquivo** menu, selecione **novo | Projeto**.
3. Navegue toohello **instalado | Modelos | Business Intelligence | Serviços de integração** tipos de projeto.
4. Selecione **Projeto do Integration Services**. Forneça valores para **Nome** e **Local** e, em seguida, selecione **OK**.

O Visual Studio abre e cria um novo projeto do SSIS (Integration Services). Em seguida, o Visual Studio abrirá designer Olá Olá único novo pacote SSIS (Package. dtsx) no projeto de saudação. Você verá Olá áreas da tela a seguir:

* Olá esquerda, Olá **caixa de ferramentas** dos componentes do SSIS.
* No meio de Olá Olá superfície de design, com várias guias. Você normalmente usa pelo menos Olá **fluxo de controle** e hello **de fluxo de dados** guias.
* Em Olá direita, Olá **Solution Explorer** e hello **propriedades** painéis.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Etapa 2: Criar o fluxo de dados básicos de saudação
1. Arraste uma tarefa de fluxo de dados do Centro de toohello da caixa de ferramentas Olá Olá da superfície de design (em Olá **fluxo de controle** guia).
   
    ![][02]
2. Clique duas vezes no guia de fluxo de dados toohello tooswitch a tarefa de fluxo de dados hello.
3. Na lista de outras fontes de saudação de saudação da caixa de ferramentas, arraste uma superfície de design de toohello de origem do ADO.NET. Com o adaptador de origem Olá ainda selecionado, altere seu nome muito**fonte do SQL Server** em Olá **propriedades** painel.
4. Na lista de outros destinos de saudação de saudação da caixa de ferramentas, arraste uma superfície de design do destino do ADO.NET toohello em Olá origem ADO.NET. Com o adaptador de destino Olá ainda selecionado, altere seu nome muito**destino SQL DW** em Olá **propriedades** painel.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Etapa 3: Configurar o adaptador de origem de saudação
1. Clique duas vezes em Olá Olá de tooopen do adaptador de origem **Editor de origem do ADO.NET**.
   
    ![][03]
2. Em Olá **Gerenciador de Conexão** guia da saudação **Editor de origem do ADO.NET**, clique em Olá **novo** toohello próximo botão **Gerenciador de conexão ADO.NET**Olá de tooopen lista **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo caixa e criar configurações de conexão do banco de dados do SQL Server Olá carrega os dados do qual este tutorial.
   
    ![][04]
3. Em Olá **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo, clique em Olá **novo** saudação do botão tooopen **Gerenciador de Conexão** caixa de diálogo caixa e criar uma nova conexão de dados.
   
    ![][05]
4. Em Olá **Gerenciador de Conexão** caixa de diálogo caixa, Olá coisas a seguir.
   
   1. Para **provedor**, selecione Olá provedor de dados SqlClient.
   2. Para **nome do servidor**, digite Olá nome de SQL Server.
   3. Em Olá **fazer logon no servidor de toohello** seção, selecione ou insira as informações de autenticação.
   4. Em Olá **o banco de dados do Connect tooa** seção, selecione o banco de dados do exemplo hello AdventureWorks.
   5. Clique em **Testar conexão**.
      
       ![][06]
   6. Na caixa de diálogo de saudação que relata os resultados de saudação do teste de conexão hello, clique em **Okey** tooreturn toohello **Gerenciador de Conexão** caixa de diálogo.
   7. Em Olá **Gerenciador de Conexão** caixa de diálogo, clique em **Okey** tooreturn toohello **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo.
5. Em Olá **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo, clique em **Okey** tooreturn toohello **Editor de origem do ADO.NET**.
6. Em Olá **Editor de origem do ADO.NET**, em Olá **nome da tabela de saudação ou exibição de saudação** lista, selecione Olá **Sales. SalesOrderDetail** tabela.
   
    ![][07]
7. Clique em **visualização** toosee Olá primeiras 200 linhas de dados na tabela de origem Olá Olá **visualizar resultados da consulta** caixa de diálogo.
   
    ![][08]
8. Em Olá **visualizar resultados da consulta** caixa de diálogo, clique em **fechar** tooreturn toohello **Editor de origem do ADO.NET**.
9. Em Olá **Editor de origem do ADO.NET**, clique em **Okey** toofinish configurar fonte de dados de saudação.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Etapa 4: Conectar o adaptador de destino toohello do adaptador de origem Olá
1. Selecione o adaptador de origem de saudação na superfície de design de saudação.
2. Selecione a seta Olá azul que se estende do adaptador de origem de saudação e arraste toohello editor de destino até que ele se encaixe.
   
    ![][10]
   
    Em um pacote SSIS típico, use um número de outros componentes da saudação da caixa de ferramentas do SSIS entre origem hello e Olá destino toorestructure, transformar e limpar seus dados conforme ele passa pelo fluxo de dados do SSIS hello. tookeep neste exemplo é tão simple quanto possível, estamos nos conectando diretamente da saudação fonte toohello destino.

## <a name="step-5-configure-hello-destination-adapter"></a>Etapa 5: Configurar o adaptador de destino Olá
1. Clique duas vezes em Olá Olá de tooopen do adaptador de destino **Editor de destino ADO.NET**.
   
    ![][11]
2. Em hello **Gerenciador de Conexão** guia da saudação **Editor de destino ADO.NET**, clique em hello **novo** toohello próximo botão **doGerenciadordeConexão**Olá de tooopen lista **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo caixa e criar configurações de conexão do banco de dados do Azure SQL Data Warehouse Olá carrega os dados no qual este tutorial.
3. Em Olá **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo, clique em Olá **novo** saudação do botão tooopen **Gerenciador de Conexão** caixa de diálogo caixa e criar uma nova conexão de dados.
4. Em Olá **Gerenciador de Conexão** caixa de diálogo caixa, Olá coisas a seguir.
   1. Para **provedor**, selecione Olá provedor de dados SqlClient.
   2. Para **nome do servidor**, digite nome de SQL Data Warehouse hello.
   3. Em Olá **fazer logon no servidor de toohello** seção, selecione **autenticação Use SQL Server** e insira as informações de autenticação.
   4. Em Olá **o banco de dados do Connect tooa** seção, selecione um banco de dados existente do SQL Data Warehouse.
   5. Clique em **Testar conexão**.
   6. Na caixa de diálogo de saudação que relata os resultados de saudação do teste de conexão hello, clique em **Okey** tooreturn toohello **Gerenciador de Conexão** caixa de diálogo.
   7. Em Olá **Gerenciador de Conexão** caixa de diálogo, clique em **Okey** tooreturn toohello **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo.
5. Em Olá **configurar Gerenciador de Conexão ADO.NET** caixa de diálogo, clique em **Okey** tooreturn toohello **Editor de destino ADO.NET**.
6. Em Olá **Editor de destino ADO.NET**, clique em **novo** toohello próximo **usar uma tabela ou exibição** Olá de tooopen lista **Create Table** caixa de diálogo toocreate uma nova tabela de destino com uma lista de colunas que coincide com a tabela de origem hello.
   
    ![][12a]
7. Em Olá **Create Table** caixa de diálogo caixa, Olá coisas a seguir.
   
   1. Alterar o nome de saudação da tabela de destino Olá muito**SalesOrderDetail**.
   2. Remover Olá **rowguid** coluna. Olá **uniqueidentifier** não há suporte para o tipo de dados no SQL Data Warehouse.
   3. Alterar tipo de dados de saudação do hello **LineTotal** coluna muito**money**. Olá **decimal** não há suporte para o tipo de dados no SQL Data Warehouse. Para obter informações sobre tipos de dados com suporte, consulte [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Clique em **Okey** toocreate Olá tabela e retornar toohello **Editor de destino ADO.NET**.
8. Em Olá **Editor de destino ADO.NET**, selecione Olá **mapeamentos** guia toosee como colunas na fonte de saudação são mapeados toocolumns no destino hello.
   
    ![][13]
9. Clique em **Okey** toofinish configurar fonte de dados de saudação.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Etapa 6: Executar dados de saudação do hello pacote tooload
Pacote de execução Olá clicando Olá **iniciar** botão na barra de ferramentas de saudação ou selecionando uma saudação **executar** opções Olá **depurar** menu.

Como o pacote de saudação começa toorun, consulte amarelo rodas de rotação tooindicate atividade, bem como o número de saudação de linhas processadas até o momento.

![][14]

Quando a execução do pacote de saudação for concluída, você consulte marcas de seleção verdes tooindicate êxito bem como Olá número total de linhas de dados carregados de saudação origem toohello destino.

![][15]

Parabéns! Você usou dados do SQL Server Integration Services tooload com êxito no Azure SQL Data Warehouse.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o fluxo de dados do SSIS hello. Comece por aqui: [Fluxo de Dados][Data Flow].
* Saiba como toodebug e solucionar problemas de seu direito de pacotes no ambiente de design de saudação. Comece por aqui: [Solução de problemas de ferramentas para o desenvolvimento de pacotes][Troubleshooting Tools for Package Development].
* Saiba como a toodeploy o SSIS projetos e pacotes tooIntegration tooanother ou servidor dos serviços de local de armazenamento. Comece por aqui: [Implantação de projetos e pacotes][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
