---
title: "conector de banco de dados Oracle aaaAdd Olá em seus aplicativos do Azure lógica | Microsoft Docs"
description: "Usar o conector do banco de dados Oracle de saudação em um aplicativo de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Introdução ao conector do banco de dados Oracle Olá

Usando o conector do banco de dados Oracle hello, crie o organizacionais fluxos de trabalho que usam dados no banco de dados existente. Esse conector pode se conectar a tooan banco de dados do Oracle no local ou uma máquina virtual do Azure com o banco de dados Oracle instalado. Com esse conector, você pode:

* Crie o fluxo de trabalho adicionando um novo cliente tooa clientes banco de dados, ou atualizando um pedido em um banco de dados de pedidos.
* Use ações tooget uma linha de dados, inserir uma nova linha e até mesmo excluir. Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados Oracle (uma ação). 

Este tópico mostra como toouse Olá conector de banco de dados Oracle em um aplicativo de lógica.

## <a name="prerequisites"></a>Pré-requisitos

* Versões do Oracle com suporte: 
    * Oracle 9 e versões posteriores
    * Software cliente do Oracle 8.1.7 e posteriores

* Saudação de instalar o gateway de dados no local. [Conecte-se a dados locais tooon de aplicativos lógicos](../logic-apps/logic-apps-gateway-connection.md) listas Olá etapas. gateway de saudação é necessário tooconnect tooan banco de dados do Oracle no local ou uma VM do Azure com o banco de dados Oracle instalado. 

    > [!NOTE]
    > gateway de dados local Olá atua como uma ponte e fornece uma transferência de dados segura entre os dados de local (dados que não está na nuvem Olá) e seus aplicativos lógicos. Olá mesmo gateway pode ser usado com vários serviços e várias fontes de dados. Portanto, talvez seja necessário apenas gateway de saudação tooinstall uma vez.

* Instale Olá cliente Oracle na máquina de saudação onde você instalou o gateway de dados local hello. Certifique-se de que tooinstall hello provedor de dados Oracle de 64 bits para .NET do Oracle:  

  [ODAC 12c Release 4 (12.1.0.2.4) de 64 bits para Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Se o cliente do Oracle Olá não estiver instalado, ocorrerá um erro quando você tentar toocreate ou usa conexão hello. Consulte os erros comuns Olá neste tópico.


## <a name="add-hello-connector"></a>Adicionar Olá conector

> [!IMPORTANT]
> Esse conector não tem gatilhos. Ele tem somente ações. Para quando você criar seu aplicativo lógico, adicionar outro toostart de gatilho sua lógica de aplicativo, como **agenda - recorrência**, ou **de solicitação / resposta - resposta**. 

1. Em Olá [portal do Azure](https://portal.azure.com), criar um aplicativo em branco lógica.

2. No início de saudação do seu aplicativo lógico, selecione Olá **de solicitação / resposta - solicitação** gatilho: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Selecione **Salvar**. Quando você salva, a URL de uma solicitação é gerada automaticamente. 

4. Selecione **Nova etapa** e selecione **Adicionar uma ação**. Digite `oracle` toosee Olá ações disponíveis: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Isso também é toosee de maneira mais rápida de Olá Olá gatilhos e ações disponíveis para qualquer conector. Digite parte do nome do conector hello, como `oracle`. designer de saudação lista todos os gatilhos e ações. 

5. Selecione uma das ações de saudação, como **banco de dados Oracle - Get linha**. Selecione **Conectar por meio do gateway de dados local**. Insira o nome do servidor Oracle hello, método de autenticação, nome de usuário, senha e selecione Olá gateway:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Uma vez conectado, selecione uma tabela da lista de saudação e inserir a tabela de tooyour de identificação de linha de saudação. Você precisa de tabela de toohello tooknow Olá identificador. Se você não souber, contate o administrador de banco de dados Oracle e obter a saída Olá `select * from yourTableName`. Isso proporciona Olá necessário tooproceed de informações de identificação.

    Em Olá exemplo a seguir, os dados do trabalho está sendo retornados de um banco de dados de recursos humanos: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. Nesta próxima etapa, você pode usar qualquer Olá toobuild outros conectores seu fluxo de trabalho. Se você quiser tootest Obtendo dados do Oracle, envie por conta própria um email com os dados de Oracle hello usando uma saudação envie email conectores, Office 365 ou Gmail. Usar os tokens dinâmico Olá de saudação do hello Oracle tabela toobuild `Subject` e `Body` do email:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Salve** seu aplicativo lógico e selecione **Executar**. Fechar o designer de saudação e examine Olá executa histórico de status de saudação. Se ele falhar, selecione a linha de mensagem com falha de saudação. Olá designer é aberto e mostra qual etapa falha e também mostra Olá informações de erro. Se tiver êxito, você receberá um email com informações de saudação que você adicionou.


### <a name="workflow-ideas"></a>Ideias de fluxo de trabalho

* Você deseja toomonitor Olá #oracle hashtag e colocar Olá tweets em um banco de dados para que possam ser consultados e usados em outros aplicativos. Em um aplicativo de lógica, adicionar Olá `Twitter - When a new tweet is posted` disparar e digite Olá **#oracle** hashtag. Em seguida, adicione Olá `Oracle Database - Insert row` ação e selecione a tabela:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* As mensagens são enviadas tooa fila de barramento de serviço. Você deseja que essas mensagens tooget e colocá-los em um banco de dados. Em um aplicativo de lógica, adicionar Olá `Service Bus - when a message is received in a queue` gatilho e selecione Olá fila. Em seguida, adicione Olá `Oracle Database - Insert row` ação e selecione a tabela:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Erros comuns

#### <a name="error-cannot-reach-hello-gateway"></a>**Erro**: não é possível alcançar o hello Gateway

**Causa**: gateway de dados local Olá não é capaz de tooconnect toohello nuvem. 

**Mitigação**: Verifique se o gateway está em execução na máquina local de saudação onde você instalou e que ele pode se conectar a toohello internet.  É recomendável não instalar o gateway de saudação em um computador que pode ser desativado ou suspensão. Também é possível reiniciar o serviço de gateway de dados de local de saudação (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Erro**: Olá provedor que está sendo usado foi preterido: ' OracleClient exige software cliente Oracle versão 8.1.7 ou posterior.'. Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) provedor oficial do tooinstall hello.

**Causa**: Olá Oracle cliente SDK não está instalado na máquina de saudação onde hello gateway de dados está em execução ao local.  

**Resolução**: baixar e instalar o SDK de cliente Oracle Olá Olá mesmo computador que o gateway de dados local hello.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Erro**: a tabela '[Nome_da_tabela]' não define colunas de chave

**Causa**: Olá tabela não tem nenhuma chave primária.  

**Resolução**: conector do banco de dados Oracle Olá requer uma tabela com uma coluna de chave primária.

#### <a name="currently-not-supported"></a>Não há suporte no momento

* Exibições e procedimentos armazenados 
* Qualquer tabela com chaves compostas
* Tipos de objeto aninhados em tabelas
 
## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/oracle/). 

## <a name="get-some-help"></a>Obtenha ajuda

Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) é um ótimo colocar tooask perguntas, responder a perguntas e veja o que outros usuários de aplicativos lógicos estão fazendo. 

Você pode ajudar a melhorar os Aplicativos Lógicos e os conectores vitando e enviando suas ideias em [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)e explorar os conectores disponíveis Olá na lógica de aplicativos no nosso [lista APIs](apis-list.md).
