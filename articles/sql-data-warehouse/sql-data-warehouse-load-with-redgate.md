---
title: "depósito de dados do Azure aaaUse Redgate tooload dados tooyour | Microsoft Docs"
description: "Saiba como Studio do toouse Redgate de plataforma de dados para cenários de data warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Carregar dados com o Data Platform Studio da Redgate
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Fábrica de dados](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Este tutorial mostra como toouse [Studio de plataforma de dados do Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) dados de toomove (DPS) de um tooAzure do SQL Server local SQL Data Warehouse. Studio da plataforma de dados aplica correções de compatibilidade mais apropriadas hello e otimizações, portanto, não tem mais rápido possível Olá maneira tooget iniciado com o SQL Data Warehouse.

> [!NOTE]
> [Redgate](http://www.red-gate.com) é um antigo parceiro da Microsoft que oferece várias ferramentas de SQL Server. Esse recurso no Data Platform Studio ficou disponível gratuitamente para uso comercial e não comercial.
> 
> 

## <a name="before-you-begin"></a>Antes de começar
### <a name="create-or-identify-resources"></a>Criar ou identificar recursos
Antes de iniciar este tutorial, você precisará toohave:

* **o banco de dados do SQL Server local**: Olá dados que você deseja tooimport tooSQL Data Warehouse precisa toocome de um SQL Server no local (versão 2008R2 ou superior). Data Platform Studio não pode importar dados diretamente de um Banco de Dados SQL do Azure ou de arquivos de texto.
* **Conta de armazenamento do Azure**: Studio da plataforma de dados prepara os dados de saudação no armazenamento de BLOBs do Azure antes de carregá-lo no SQL Data Warehouse. conta de armazenamento Olá deve estar usando o modelo de implantação do "Gerenciador de recursos" saudação (padrão de saudação) em vez do modelo de implantação "Clássico" hello. Se você não tiver uma conta de armazenamento, saiba como tooCreate uma conta de armazenamento. 
* **SQL Data Warehouse**: neste tutorial move Olá dados do local do SQL Server tooSQL Data Warehouse, para que seja necessário toohave um data warehouse on-line. Se você ainda não tiver um data warehouse, saiba como tooCreate um Azure SQL Data Warehouse.

> [!NOTE]
> Desempenho é aprimorado se a conta de armazenamento hello e Olá data warehouse são criados no hello mesmo região.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Etapa 1: Inscrever-se em tooData Studio plataforma com sua conta do Azure
Abra seu navegador da web e navegue toohello [Studio da plataforma de dados](https://www.dataplatformstudio.com/) site. Entrar com hello a mesma conta do Azure que você toocreate usado Olá armazenamento conta e do data warehouse. Se seu endereço de email for associado a um trabalho ou conta de escola e uma conta da Microsoft, conta de Olá toochoose-se de que tem acesso tooyour recursos.

> [!NOTE]
> Se essa é a primeira vez usando o Studio de plataforma de dados, você será solicitado toogrant Olá aplicativo permissão toomanage seus recursos do Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Etapa 2: Inicie o Assistente de importação de saudação
Na tela principal de DPS hello, selecione Olá tooAzure SQL Data Warehouse link toostart Olá Importar Assistente de importação.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Etapa 3: Instalar Olá dados plataforma Studio Gateway
tooconnect tooyour no SQL Server banco de dados local, você precisa tooinstall Olá DPS Gateway. gateway de saudação é um agente de cliente que fornece acesso tooyour ambiente local, extrai dados de saudação e carrega-tooyour conta de armazenamento. Os dados nunca passam por servidores da Redgate. Olá tooinstall Gateway:

1. Clique em Olá **criar Gateway** link
2. Baixar e instalar usando o Gateway Olá Olá instalador fornecido

![][2]

> [!NOTE]
> Olá Gateway pode ser instalado em qualquer computador com o banco de dados do network access toohello origem do SQL Server. Ele acessa o banco de dados do SQL Server hello usando a autenticação do Windows com credenciais de saudação do usuário atual do hello.
> 
> 

Uma vez instalado, Olá tooConnected de alterações de status do Gateway e você pode selecionar o próximo.

## <a name="step-4-identify-hello-source-database"></a>Etapa 4: Identificar o banco de dados de origem de saudação
Em Olá *insira o nome do servidor* caixa de texto, insira o nome de saudação do servidor de saudação que hospeda seu banco de dados e selecione **próximo**. Do menu suspenso de Olá, selecione Olá banco de dados que você deseja tooimport dados.

![][3]

DPS inspeciona o banco de dados selecionados para tabelas tooimport hello. Por padrão, o DPS importa todas as tabelas de saudação no banco de dados de saudação. Você pode selecionar ou desmarcar tabelas expandindo Olá vincular todas as tabelas. Selecione Olá próximo botão toomove para frente.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Etapa 5: Escolha um armazenamento conta toostage Olá de dados
DPS solicita um local toostage Olá de dados. Escolha uma conta de armazenamento existente na sua assinatura e selecione **Avançar**.

> [!NOTE]
> DPS criará um novo contêiner de blob no hello escolhido conta de armazenamento e usar uma pasta distinta para cada importação.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Etapa 6: Criar um data warehouse
Em seguida, selecione um online [Azure SQL Data Warehouse](http://aka.ms/sqldw) dados Olá tooimport de banco de dados. Depois de selecionar o banco de dados, você precisa tooenter Olá credenciais tooconnect toohello banco de dados e selecione **próximo**.

![][5]

> [!NOTE]
> DPS mescla tabelas de dados de origem de saudação do data warehouse de saudação. DPS avisa se o nome de tabela Olá exige toooverwrite as tabelas existentes no data warehouse de saudação. Você pode, opcionalmente, excluir quaisquer objetos existentes no data warehouse de saudação acionamento excluir todos os objetos existentes antes da importação.
> 
> 

## <a name="step-7-import-hello-data"></a>Etapa 7: Importar dados de saudação
DPS confirma que você gostaria que dados de saudação tooimport. Basta clicar em Olá Iniciar importação botão toobegin Olá a importação de dados.

![][6]

DPS exibe uma visualização que mostra o andamento da saudação de extração e carregamento de dados de saudação do progresso de SQL Server e Olá de local de Olá da importação de saudação no SQL Data Warehouse.

![][7]

Após a conclusão da importação de hello, DPS exibe um resumo da importação de dados hello e um relatório de alteração de correções de compatibilidade de saudação que foram executadas.

![][8]

## <a name="next-steps"></a>Próximas etapas
tooexplore seus dados no SQL Data Warehouse, inicie por meio da exibição:

* [Consultar o Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]
* [Visualizar os dados com o Power BI][Visualize data with Power BI]

toolearn mais sobre o Studio de plataforma de dados do Redgate:

* [Visite a home page DPS Olá](http://www.dataplatformstudio.com/)
* [Assista a uma demonstração do DPS no Channel9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Para obter uma visão geral de outras maneiras toomigrate e carregar os dados no Data Warehouse SQL consulte:

* [Migrar tooSQL sua solução do Data Warehouse][Migrate your solution tooSQL Data Warehouse]
* [Carregar dados no SQL Data Warehouse do Azure](sql-data-warehouse-overview-load.md)

Para obter mais dicas de desenvolvimento, consulte Olá [visão geral do desenvolvimento de SQL Data Warehouse](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
