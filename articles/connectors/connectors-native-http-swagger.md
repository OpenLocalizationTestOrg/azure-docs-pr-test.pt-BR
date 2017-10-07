---
title: "pontos de extremidade REST de aaaCall com HTTP + Swagger connector para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Conectar a pontos de extremidade de tooREST de aplicativos lógicos por meio de Swagger com Olá HTTP + Swagger conector"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Introdução ao Olá HTTP + Swagger ação

Você pode criar um ponto de extremidade do conector de primeira classe tooany REST por meio de um [Swagger documento](https://swagger.io) quando você usa Olá HTTP + Swagger ação em um fluxo de trabalho de sua lógica do aplicativo. Você também pode estender lógica aplicativos toocall qualquer ponto de extremidade REST com uma experiência de Designer do aplicativo de lógica de primeira classe.

toolearn como aplicativos de lógica de toocreate com conectores, consulte [criar um novo aplicativo de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Usar HTTP + Swagger como um gatilho ou uma ação

Olá HTTP + trabalho de gatilho e a ação de Swagger Olá mesmo como Olá [ação HTTP](connectors-native-http.md) mas fornecer uma melhor experiência no Designer de lógica do aplicativo, expondo a estrutura de saudação API e saídas de saudação [Swagger metadados](https://swagger.io) . Você também pode usar Olá HTTP + Swagger conector como um disparador. Se você quiser tooimplement um gatilho de sondagem, seguem o padrão de sondagem de saudação que é descrita em [criar toocall APIs personalizada outras APIs, serviços e sistemas de aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Saiba mais sobre [gatilhos e ações de aplicativo lógico](connectors-overview.md).

Aqui está um exemplo de como toouse Olá HTTP + Swagger operação como uma ação em um fluxo de trabalho em um aplicativo de lógica.

1. Selecione Olá **nova etapa** botão.
2. Escolha **Adicionar uma ação**.
3. Na caixa de pesquisa de ação hello, digite **swagger** Olá toolist HTTP + Swagger ação.
   
    ![Selecionar ação de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. Digite a URL para um documento de Swagger hello:
   
   * toowork de saudação lógica de aplicativo Designer, Olá URL deve ser um ponto de extremidade HTTPS e tiver habilitado CORS.
   * Se o documento de Swagger de saudação não atender a esse requisito, você pode usar [armazenamento do Azure com CORS habilitado](#hosting-swagger-from-storage) toostore documento de saudação.
5. Clique em **próximo** tooread e renderização de Olá Swagger documento.
6. Adicione quaisquer parâmetros que são necessários para a chamada de saudação HTTP.
   
    ![Concluir a ação HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave e publicar seu aplicativo lógico, clique em **salvar** na barra de ferramentas do designer.

### <a name="host-swagger-from-azure-storage"></a>Hospedar o Swagger do Armazenamento do Azure
Talvez você queira tooreference um documento de Swagger que não está hospedado ou que não atende aos requisitos de segurança e entre origens de saudação do designer de saudação. tooresolve esse problema, você pode armazenar o documento de Swagger Olá no armazenamento do Azure e habilitar CORS tooreference Olá documentos.  

Aqui estão Olá etapas toocreate, configurar e armazenar documentos Swagger no armazenamento do Azure:

1. [Crie uma conta de armazenamento do Azure com o armazenamento de Blobs do Azure](../storage/common/storage-create-storage-account.md). tooperform essa etapa, defina as permissões muito**acesso público**.

2. Habilite o CORS no blob de saudação. 

   tooautomatically definir essa configuração, você pode usar [este script do PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Carregar um blob de toohello de arquivo hello Swagger. 

   Você pode executar essa etapa de saudação [portal do Azure](https://portal.azure.com) ou de uma ferramenta como [Azure Storage Explorer](http://storageexplorer.com/).

4. Fazer referência a um documento de toohello link HTTPS no armazenamento de BLOBs do Azure. 

   link de saudação usa este formato:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Detalhes técnicos
A seguir é Olá detalhes Olá gatilhos e ações que este HTTP + Swagger conector dá suporte a.

## <a name="http--swagger-triggers"></a>Gatilhos de HTTP + Swagger
Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico. [Saiba mais sobre gatilhos.](connectors-overview.md) Olá HTTP + Swagger conector tem um gatilho.

| Gatilho | Descrição |
| --- | --- |
| HTTP + Swagger |Fazer uma chamada HTTP e retornar o conteúdo da resposta Olá |

## <a name="http--swagger-actions"></a>Ações de HTTP + Swagger
Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico. [Saiba mais sobre ações.](connectors-overview.md) Olá HTTP + Swagger connector tem uma ação possível.

| Ação | Descrição |
| --- | --- |
| HTTP + Swagger |Fazer uma chamada HTTP e retornar o conteúdo da resposta Olá |

### <a name="action-details"></a>Detalhes da ação
Olá HTTP + Swagger conector vem com uma ação possível. A seguir é informações sobre cada uma das ações hello, campos de entrada necessários e opcionais e Olá correspondente detalhes de saída que estão associados com o seu uso.

#### <a name="http--swagger"></a>HTTP + Swagger
Faça uma solicitação de saída HTTP com a assistência dos metadados do Swagger.
Um asterisco (*) significa um campo obrigatório.

| Nome de exibição | Nome da propriedade | Descrição |
| --- | --- | --- |
| Método* |estático |Toouse de verbo HTTP. |
| URI* |uri |URI da solicitação HTTP de saudação. |
| Cabeçalhos |headers |Um objeto JSON de tooinclude de cabeçalhos HTTP. |
| Corpo |body |Olá corpo da solicitação HTTP. |
| Autenticação |Autenticação |Toouse de autenticação para a solicitação. Para obter mais informações, consulte Olá [conector HTTP](connectors-native-http.md#authentication). |

**Detalhes de saída**

Resposta HTTP

| Nome da propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| headers |objeto |Cabeçalhos de resposta |
| Corpo |objeto |Objeto de resposta |
| Código de status |int |Código de status HTTP |

### <a name="http-responses"></a>Respostas HTTP
Ao fazer chamadas toovarious ações, você poderá obter respostas de determinados. A seguir, uma tabela que descreve respostas e descrições correspondentes.

| Name | Descrição |
| --- | --- |
| 200 |OK |
| 202 |Aceita |
| 400 |Solicitação incorreta |
| 401 |Não Autorizado |
| 403 |Proibido |
| 404 |Não encontrado |
| 500 |Erro interno do servidor. Ocorreu um erro desconhecido. |

- - -
## <a name="next-steps"></a>Próximas etapas

* [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)
* [Localizar outros conectores](apis-list.md)