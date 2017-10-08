---
title: "aaaLearn como toouse Olá conector FTP em aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte tooFTP server toomanage seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no servidor FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Introdução ao conector FTP Olá
Use Olá FTP conector toomonitor, gerenciar e criar arquivos em um servidor FTP. 

toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico. Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Conecte-se tooFTP
Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service. Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.  

### <a name="create-a-connection-tooftp"></a>Criar uma conexão tooFTP
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Usar o gatilho de FTP
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> conector FTP Olá requer um servidor FTP que é acessível de saudação à Internet e é configurado toooperate com modo passivo. Além disso, o conector Olá FTP é **não é compatível com implícita FTPS (FTP sobre SSL)**. conector FTP Olá suporta apenas explícita FTPS (FTP sobre SSL).  
> 
> 

Neste exemplo, mostrarei como Olá toouse **FTP - quando um arquivo é adicionado ou modificado** disparar um fluxo de trabalho do aplicativo de lógica de tooinitiate quando um arquivo é adicionado ao ou modificado em um servidor FTP. Um exemplo de empresa, você pode usar toomonitor esse gatilho uma pasta FTP para novos arquivos que representam os pedidos de clientes.  Você pode usar uma ação de conector FTP como **obter conteúdo do arquivo** tooget conteúdo de saudação de ordem de saudação para processamento e armazenamento no banco de dados Pedidos.

1. Digite *ftp* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **FTP - quando um arquivo é adicionado ou modificado** gatilho   
   ![Imagem 1 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Olá **quando um arquivo é adicionado ou modificado** controle abre  
   ![Imagem 2 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Selecione Olá **...**  localizado no lado direito de saudação do controle de saudação. Isso abre o controle de seletor de pasta Olá  
   ![Imagem 3 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Selecione Olá  **>**  (seta para a direita) e procure a pasta de saudação toofind que você deseja toomonitor para arquivos novos ou modificados. Selecionar pasta hello e observe a pasta Olá agora é exibida no hello **pasta** controle.  
   ![Imagem 4 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

Neste ponto, seu aplicativo lógica foi configurado com um gatilho que começará uma execução de saudação outros gatilhos e ações no fluxo de trabalho hello quando um arquivo é modificado ou criado na pasta FTP específica hello. 

> [!NOTE]
> Para uma lógica aplicativo toobe funcional, ele deve conter pelo menos um gatilho e uma ação. Siga as etapas de Olá Olá tooadd próximo da seção uma ação.  
> 
> 

## <a name="use-a-ftp-action"></a>Usar uma ação de FTP
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Agora que você adicionou um gatilho, siga essas etapas tooadd uma ação que obterão o conteúdo de saudação do arquivo de novos ou modificados de Olá encontrado pelo gatilho hello.    

1. Selecione **+ nova etapa** tooadd Olá Olá ação tooget Olá conteúdo de Olá arquivo no servidor de saudação FTP  
2. Selecione Olá **adicionar uma ação** link.  
   ![Imagem 1 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Digite *FTP* toosearch para todas as ações relacionadas tooFTP.
4. Selecione **FTP - obter o conteúdo do arquivo** como Olá tootake ação quando um arquivo novo ou modificado for encontrado na pasta de saudação FTP.      
   ![Imagem 2 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Olá **obter conteúdo do arquivo** controlar é aberta. **Observação**: você será solicitado tooauthorize tooaccess de aplicativo sua lógica de conta, seu servidor FTP se você não tiver feito isso anteriormente.  
   ![Imagem 3 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Selecione Olá **arquivo** controle (espaço em branco Olá localizada abaixo **arquivo***). Aqui, você pode usar qualquer Olá em várias propriedades de arquivo novo ou modificado Olá encontrado no servidor FTP hello.  
6. Selecione Olá **o conteúdo do arquivo** opção.  
   ![Imagem 4 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. controle de saudação é atualizado, indicando que Olá **FTP - obter o conteúdo do arquivo** ação obterá Olá *o conteúdo do arquivo* do arquivo de saudação novos ou modificados no servidor de saudação FTP.      
   ![Imagem 5 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Salve seu trabalho e adicione um tootest de pasta do arquivo toohello FTP seu fluxo de trabalho.    

Neste ponto, Olá lógica aplicativo tiver sido configurado com toomonitor um gatilho uma pasta em um servidor FTP e o fluxo de trabalho Iniciar hello quando encontra um novo arquivo ou um arquivo modificado no servidor de saudação FTP. 

Olá lógica aplicativo também foi configurado com um conteúdo de saudação tooget ação de arquivo novo ou modificado de saudação.

Agora você pode adicionar outra ação como Olá [SQL Server - Inserir linha](connectors-create-api-sqlazure.md) ação tooinsert Olá conteúdo Olá novos ou modificados arquivo em uma tabela de banco de dados SQL.  

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)

