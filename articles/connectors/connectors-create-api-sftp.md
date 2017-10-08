---
title: "aaaLearn como toouse Olá conector SFTP em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se toosend tooSFTP API e receber arquivos. Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Introdução ao conector SFTP Olá
Use Olá SFTP conector tooaccess um toosend de conta SFTP e receber arquivos. Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos.  

toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico. Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Conecte-se tooSFTP
Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service. Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.  

### <a name="create-a-connection-toosftp"></a>Criar uma conexão tooSFTP
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Usar um gatilho de SFTP
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Neste exemplo, Olá **SFTP - quando um arquivo é adicionado ou modificado** gatilho é um fluxo de trabalho do aplicativo de lógica de tooinitiate usado quando um arquivo é adicionado ao ou modificado em um servidor SFTP. Você também pode adicionar uma condição que verifica o conteúdo de saudação do arquivo de novos ou modificados da saudação e faz com que um arquivo de saudação tooextract decisão se seu conteúdo indicar que deve ser extraído antes de usar o conteúdo de saudação. Finalmente, adicione um conteúdo de saudação do tooextract de ação de um arquivo e colocar o conteúdo de saudação extraído em uma pasta no servidor SFTP Olá. 

Um exemplo de empresa, você pode usar toomonitor esse gatilho uma pasta SFTP para novos arquivos que representam os pedidos de clientes.  Você pode usar uma ação de conector SFTP, tais como **obter conteúdo do arquivo**, conteúdo de saudação tooget de ordem de saudação para processamento e armazenamento em um banco de dados de pedidos.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Adicionar uma condição
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Usar uma ação de SFTP
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).
