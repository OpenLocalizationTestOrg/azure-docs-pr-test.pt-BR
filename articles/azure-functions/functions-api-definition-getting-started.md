---
title: "aaaGetting iniciado com OpenAPI Metadata em funções do Azure | Microsoft Docs"
description: "Introdução aos metadados do OpenAPI no Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Criando metadados de OpenAPI 2.0 (Swagger) para um Aplicativo de funções (versão prévia)

Este documento orienta você pelo processo de passo a passo de saudação de criação de uma definição de OpenAPI para uma API simples hospedada em funções do Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>O que é OpenAPI (Swagger)?
[Metadados de swagger](http://swagger.io/) é um arquivo que define a funcionalidade de saudação e modos de sua API de operação e permite que uma função que hospeda um toobe da API REST consumido por uma ampla variedade de outros softwares. Ofertas da Microsoft como o PowerApps e [aplicativos de API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), bem como ferramentas como de desenvolvedor de parte 3 de [carteiro](https://www.getpostman.com/docs/importing_swagger) e [muitos pacotes mais](http://swagger.io/tools/) todos permitem sua toobe API consumida com um Definição de swagger.

## <a name="prepare-function"></a>Criando uma função com uma API simples
  toocreate uma definição de OpenAPI, é preciso primeiro toocreate uma função com uma API simples. Se você já tiver uma API hospedada em um aplicativo de função, você pode ignorar toohello reta próxima seção
1. Criar um novo Aplicativo de funções.
    1. [Portal do Azure](https://portal.azure.com) > `+ New` > Procure pela "Aplicativo de funções"
1. Cria uma nova função de gatilho HTTP dentro do seu novo Aplicativo de funções
    1. Sua função é preenchida previamente com o código que define uma API REST muito simples.
    1. Qualquer cadeia de caracteres passada toohello função como um parâmetro de consulta ou no corpo de saudação é retornada como "Olá {entrada}"
1. Vá toohello `Integrate` guia da sua nova função do gatilho de HTTP
    1. Ativar/desativar `Allowed HTTP methods` muito`Selected methods`
    1. Em `Selected HTTP methods` desmarque cada verbo, exceto POST.
    ![Métodos HTTP selecionados](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Esta etapa simplificará sua definição de API mais tarde.

## <a name="enable"></a>Habilitando suporte à definição de API
1. Navegue muito`your function name` > `Platform Features` > `API Definition`
![guia definição](./media/functions-api-definition-getting-started/definitiontab.png)
1. Definir `API Definition Source` muito`Function (preview)`
    1. Esta etapa permite que um conjunto de opções OpenAPI para seu aplicativo de função, incluindo um toohost um arquivo de OpenAPI de domínio do seu aplicativo de função, uma cópia embutido de saudação do ponto de extremidade [OpenAPI Editor](http://editor.swagger.io)e um gerador de definição de início rápido.
![Definição habilitada](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Criando sua definição de API de um modelo
1. Clique em `Generate API Definition template`
    1. Essa etapa verifica seu aplicativo de função para funções de gatilho de HTTP e usa informações de saudação na functions.json toogenerate um documento OpenAPI.
1. Adicionar um objeto de operação muito`paths: /api/yourfunctionroute post:`
    1. documento de OpenAPI de início rápido de saudação é uma estrutura de um documento OpenAPI completo. Ele exige mais metadados toobe uma definição de OpenAPI completa, como objetos de operação e modelos de resposta.
    1. objeto de operação de exemplo Hello abaixo tem um preenchido produz/consome seção, um objeto de parâmetro e um objeto de resposta.
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-summary fornece um nome de exibição em aplicativos lógicos, fluxo e PowerApps.
    >
    > Check-out [personalizar sua definição de Swagger PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn mais.

1. Clique em `save` toosave suas alterações ![adicionando definição de modelo](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Usando sua definição de API
1. Copiar seu `API definition URL` e cole-o em um novo tooview de guia do navegador documento OpenAPI bruto.
1. Você pode importar seu OpenAPI documento tooany inúmeras ferramentas para teste e integração usando essa URL.
    1. Muitos recursos do Azure são tooautomatically capaz de importar seu documento OpenAPI usando Olá URL de definição de API que é salvo em suas configurações de aplicativo de função. Como parte da saudação `Function` origem de definição de API, podemos atualizar essa url para você.


## <a name="test-definition"></a>Usando Olá Swagger da interface do usuário tootest sua definição de API
Há são ferramentas de teste criadas no modo de interface do usuário toohello do editor de definição de API Olá incorporada. Adicione sua chave de API e, em seguida, use Olá `Try this operation` botão em cada método. ferramenta Olá usará a definição API tooformat Olá solicitações e respostas bem-sucedidas indicará se a sua definição está correta.

### <a name="steps"></a>Etapas:

1. Copiar a chave de API da função
    1. Olá API chave pode ser encontrada na função de gatilho de HTTP em `function name` > `Keys` > `Function Keys` 
   ![tecla de função](./media/functions-api-definition-getting-started/functionkey.png)
1. Navegue toohello `API Definition` página.
    1. Clique em `Authenticate` e adicione o objeto de segurança de chave toohello função API na parte superior da saudação.
  ![Chave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. selecione `/api/yourfunctionroute` > `POST`
1. Clique em `Try it out` e insira um nome tootest
1. Você verá um resultado de ÊXITO sob o `Pretty`
![teste de definição de API](./media/functions-api-definition-getting-started/definitionTest.png)

## <a name="next-steps"></a>Próximas etapas
* [Definição de OpenAPI na visão geral de funções](functions-api-definition.md)
  * Leia a documentação completa Olá para obter mais informações sobre o suporte de OpenAPI.
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)  
  * Referência do programador para codificação de funções e definição de gatilhos e de associações.
* [Repositório de GitHub do Azure Functions](https://github.com/Azure/Azure-Functions/)
  * Check-out Olá funções GitHub toogive nos comentários sobre a visualização de suporte de definição de saudação API! Torne um problema do GitHub para qualquer coisa que você gostaria que toosee atualizado.
