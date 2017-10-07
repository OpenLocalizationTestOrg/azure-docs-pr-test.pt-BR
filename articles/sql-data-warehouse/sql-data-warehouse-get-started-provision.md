---
title: "aaaCreate um SQL Data Warehouse em Olá portal do Azure | Microsoft Docs"
description: "Saiba como toocreate um Azure SQL Data Warehouse em Olá portal do Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>Criar um Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este tutorial usa Olá toocreate portal do Azure SQL Data Warehouse que contém um banco de dados de exemplo AdventureWorksDW.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, você precisa:

* **Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do Azure MSDN] [ MSDN Azure Credits] toocreate uma conta.
* **Servidor do SQL Azure**: consulte [criar um banco de dados do SQL Azure com hello portal do Azure] [ Create an Azure SQL database in hello Azure portal] para obter mais detalhes.

> [!NOTE]
> A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.  Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes.
>
>

## <a name="create-a-sql-data-warehouse"></a>Criar um SQL Data Warehouse
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+ Novo** > **Bancos de dados** > **SQL Data Warehouse**.

    ![Criar](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. Em Olá **SQL Data Warehouse** folha, preencha as informações de saudação necessárias, em seguida, pressione toocreate 'Criar'.

    ![Criar banco de dados](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Servidor**: recomendamos que você selecione seu servidor primeiro.  
   * **Nome do banco de dados**: nome de Olá Olá usado tooreference SQL Data Warehouse.  Ele deve ser exclusivo toohello server.
   * **Desempenho**: é recomendável começar com 400 [DWUs][DWU]. Você pode mover Olá toohello de controle deslizante à esquerda ou direita tooadjust desempenho de saudação do seu data warehouse ou escala para cima ou para baixo após a criação.  toolearn mais sobre DWUs, consulte nossa documentação sobre [dimensionamento](sql-data-warehouse-manage-compute-overview.md) ou nosso [página de preços][SQL Data Warehouse pricing].
   * **Assinatura**: selecione Olá [assinatura] que fará a cobrança para este depósito de dados do SQL.
   * **Grupo de recursos**: [grupos de recursos] [ Resource group] são contêineres projetados toohelp você gerenciar uma coleção de recursos do Azure. Saiba mais sobre [grupos de recursos](../azure-resource-manager/resource-group-overview.md).
   * **Selecionar origem**: clique em **Selecionar origem** > **Exemplo**. Azure preenche automaticamente Olá **exemplo Select** opção com AdventureWorksDW.

   > [!NOTE]
   > agrupamento de padrão de saudação para um SQL Data Warehouse é SQL_Latin1_General_CP1_CI_AS. Se for necessário um agrupamento diferente, [T-SQL] [ T-SQL] pode ser usado toocreate banco de dados de saudação com um agrupamento diferente.
   >
   >

1. Clique em **criar** toocreate seu SQL Data Warehouse.
2. Aguarde alguns minutos. Quando o data warehouse estiver pronto, você deve ser retornado toohello [portal do Azure](https://portal.azure.com). Você pode localizar seu SQL Data Warehouse no seu painel, listado em bancos de dados SQL, ou em recurso Olá grupo que você usou toocreate-lo.

    ![exibição de portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você criou um SQL Data Warehouse, você está pronto muito[conectar](sql-data-warehouse-connect-overview.md) e começar a consultar.

dados de tooload no SQL Data Warehouse, consulte Olá [visão geral de carregamento](sql-data-warehouse-overview-load.md).

Se você estiver tentando toomigrate um tooSQL de banco de dados do Data Warehouse existente, consulte Olá [visão geral da migração](sql-data-warehouse-overview-migrate.md) ou use [utilitário de migração](sql-data-warehouse-migrate-migration-utility.md).

As regras de firewall também podem ser configuradas usando o Transact-SQL. Para saber mais, confira [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Também é toolook uma grande ideia no hello [práticas recomendadas][Best practices].

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[assinatura]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
