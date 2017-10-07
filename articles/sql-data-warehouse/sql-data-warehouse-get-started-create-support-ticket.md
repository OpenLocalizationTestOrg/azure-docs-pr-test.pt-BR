---
title: "aaaHow toocreate um tíquete de suporte para o SQL Data Warehouse | Microsoft Docs"
description: "Como toocreate suporte um tíquete no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Como toocreate suporte um tíquete para SQL Data Warehouse
Caso você tenha problemas com o SQL Data Warehouse, crie um tíquete de suporte para que nossa equipe de engenharia possa ajudá-lo.

> [!NOTE] 
> A partir de 20/12/2016, não é precisa Olá verificação de integridade de recursos no hello portal do Azure. Estamos trabalhando ativamente toofix esse problema. 


## <a name="create-a-support-ticket"></a>Criar um tíquete de suporte
1. Olá abrir [portal do Azure][Azure portal].
2. Na tela de início de saudação, clique em Olá **ajuda + suporte** lado a lado.
   
    ![Ajuda + suporte](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. No Olá ajuda + suporte folha, clique em **criar solicitação de suporte**.
   
    ![Nova solicitação de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Selecione Olá **tipo de solicitação**.
   
    ![Tipo de Solicitação](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Por padrão, cada SQL Server (por exemplo, myserver.database.windows.net) tem uma **Cota de DTU** de 45.000. Essa cota é simplesmente um limite de segurança. Você pode aumentar a cota, crie um tíquete de suporte e selecione *cota* como tipo de solicitação de saudação. toocalculate precisa, multiplique o DTU Olá 7.5 por Olá total [DWU] [ DWU] necessário. Por exemplo, você gostaria que toohost duas DW6000s em um SQL server, você deve solicitar uma cota DTU de 90.000.  Você pode exibir seu consumo de DTU atual da folha de saudação SQL server no portal de saudação. Bancos de dados em pausa e retomados contam para a cota de DTU de saudação. 
   > 
   > 
5. Selecione Olá **assinatura** hosts Olá banco de dados com problema Olá você está se comunicando.
   
    ![Assinatura](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Selecione **SQL Data Warehouse** como Olá recursos.
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Selecione seu [Plano de suporte do Azure][Azure support plan].
   
   * **gerenciamento de assinaturas, cobrança e cotas** está disponível em todos os níveis de suporte.
   * O suporte do **reparo** é fornecido por meio do suporte do [Desenvolvedor][Developer], [Standard][Standard], [Professional Direct][Professional Direct] ou [Premier][Premier]. Problemas são problemas enfrentados pelos clientes durante o uso do Azure onde há uma expectativa razoável problema Olá Microsoft causada.
   * **Desenvolvedor aconselhamento** e **os serviços de consultoria** estão disponíveis em Olá [Professional Direct] [ Professional Direct] e [Premier] [ Premier] níveis de suporte. 
     
     Se você tiver um Premier plano de suporte, você também pode relatar SQL Data Warehouse relacionados a problemas de saudação [portal online da Microsoft Premier][Microsoft Premier online portal].  Consulte [planos de suporte do Azure] [ Azure support plan] toolearn mais sobre Olá vários oferecem suporte a planos, incluindo o escopo, tempos de resposta, preços, etc.  Para ver as perguntas frequentes sobre o suporte do Azure, consulte [Perguntas frequentes do suporte do Azure][Azure support FAQs].  
     
     ![Plano de suporte](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Selecione Olá **tipo de problema** e **categoria**. Neste exemplo, escolhemos como tipo de problema de hello "ferramentas" e "Ferramentas de cliente" como categoria da saudação. 
   
    ![Categoria de tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Descreva o problema de saudação e escolha Olá nível de impacto nos negócios.
   
    ![Descrição do problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Suas **informações de contato** para esse tíquete de suporte serão preenchidas previamente. Atualize-as se necessário.
    
    ![Informações de contato](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Clique em **criar** toosubmit Olá o suporte da solicitação.

## <a name="monitor-a-support-ticket"></a>Monitorar um tíquete de suporte
Depois que você enviou a solicitação de suporte Olá, equipe de suporte do Azure Olá entrará em contato com você. toocheck seu status de solicitação e os detalhes, clique em **gerenciar solicitações de suporte** no painel de saudação.

![Verificar o status](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Outros recursos
Além disso, você pode se conectar com hello da comunidade do SQL Data Warehouse em [estouro de pilha] [ Stack Overflow] ou em Olá [Fórum do MSDN do Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

