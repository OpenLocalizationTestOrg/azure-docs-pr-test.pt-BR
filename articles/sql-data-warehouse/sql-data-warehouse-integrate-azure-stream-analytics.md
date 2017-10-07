---
title: aaaUse Stream Analytics do Azure, SQL Data warehouse | Microsoft Docs
description: "Dicas para usar o Stream Analytics do Azure com o Azure SQL Data Warehouse para desenvolver as soluções."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Usar o Stream Analytics do Azure com o SQL Data Warehouse
Análise de fluxo do Azure é um serviço totalmente gerenciado fornecendo processamento de eventos complexos de baixa latência, altamente disponível e dimensionável ao longo do fluxo de dados na nuvem hello. Você pode aprender os fundamentos de saudação lendo [tooAzure de Introdução do Stream Analytics][Introduction tooAzure Stream Analytics]. Em seguida, saiba como toocreate uma solução de ponta a ponta com análises de fluxo seguindo Olá [começar a usar o Azure Stream Analytics] [ Get started using Azure Stream Analytics] tutorial.

Neste artigo, você aprenderá como toouse o Azure SQL Data Warehouse banco de dados como um coletor de saída para os trabalhos de análise de fluxo.

## <a name="prerequisites"></a>Pré-requisitos
Primeiro, execute Olá etapas Olá [começar a usar o Azure Stream Analytics] [ Get started using Azure Stream Analytics] tutorial.  

1. Criar uma entrada de Hub de eventos
2. Configurar e iniciar o aplicativo gerador de evento
3. Provisionar um trabalho de análise de fluxo
4. Especifique a entrada e a consulta do trabalho

Em seguida, crie um banco de dados do SQL Data Warehouse do Azure

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Especifique a saída do trabalho: banco de dados do SQL Data Warehouse do Azure
### <a name="step-1"></a>Etapa 1
O trabalho do Stream Analytics em **saída** da parte superior da saudação de página hello e clique **adicionar saída**.

### <a name="step-2"></a>Etapa 2
Selecione o Banco de Dados SQL e clique em Avançar.

![][add-output]

### <a name="step-3"></a>Etapa 3
Digite hello valores a seguir na página seguinte hello:

* *Alias de saída*: insira um nome amigável para essa saída de trabalho.
* *Assinatura*:
  * Se seu banco de dados do SQL Data Warehouse estiver em Olá mesma assinatura que o trabalho de análise de fluxo de saudação, selecione Usar banco de dados SQL da assinatura atual.
  * Se o seu banco de dados estiver em uma assinatura diferente, selecione Usar Banco de Dados SQL de Outra Assinatura.
* *Banco de dados*: especifique o nome de saudação de um banco de dados de destino.
* *Nome do servidor*: especificar nome do servidor de saudação do banco de dados de saudação especificado. Você pode usar Olá Portal clássico do Azure toofind isso.

![][server-name]

* *Nome de usuário*: especificar Olá nome de usuário de uma conta que tenha permissões de gravação para o banco de dados de saudação.
* *Senha*: fornecer senha Olá Olá especificar conta de usuário.
* *Tabela*: especifique o nome de Olá Olá tabela de destino no banco de dados de saudação.

![][add-database]

### <a name="step-4"></a>Etapa 4
Esta saída de trabalho e tooverify que Stream Analytics pode se conectar com êxito toohello banco de dados, clique em Olá tooadd de botão de seleção.

![][test-connection]

Quando o banco de dados do hello conexão toohello for bem-sucedida, você verá uma notificação na parte inferior de saudação do portal de saudação. Você pode clicar em Conexão de teste no hello inferior tootest Olá conexão toohello banco de dados.

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].

Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
