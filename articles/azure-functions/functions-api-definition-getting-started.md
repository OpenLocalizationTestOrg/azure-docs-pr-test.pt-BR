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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="6bafe-103">Criando metadados de OpenAPI 2.0 (Swagger) para um Aplicativo de funções (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="6bafe-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="6bafe-104">Este documento orienta você pelo processo de passo a passo de saudação de criação de uma definição de OpenAPI para uma API simples hospedada em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bafe-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="6bafe-105">O que é OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="6bafe-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="6bafe-106">[Metadados de swagger](http://swagger.io/) é um arquivo que define a funcionalidade de saudação e modos de sua API de operação e permite que uma função que hospeda um toobe da API REST consumido por uma ampla variedade de outros softwares.</span><span class="sxs-lookup"><span data-stu-id="6bafe-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="6bafe-107">Ofertas da Microsoft como o PowerApps e [aplicativos de API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), bem como ferramentas como de desenvolvedor de parte 3 de [carteiro](https://www.getpostman.com/docs/importing_swagger) e [muitos pacotes mais](http://swagger.io/tools/) todos permitem sua toobe API consumida com um Definição de swagger.</span><span class="sxs-lookup"><span data-stu-id="6bafe-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="6bafe-108"><a name="prepare-function"></a>Criando uma função com uma API simples</span><span class="sxs-lookup"><span data-stu-id="6bafe-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="6bafe-109">toocreate uma definição de OpenAPI, é preciso primeiro toocreate uma função com uma API simples.</span><span class="sxs-lookup"><span data-stu-id="6bafe-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="6bafe-110">Se você já tiver uma API hospedada em um aplicativo de função, você pode ignorar toohello reta próxima seção</span><span class="sxs-lookup"><span data-stu-id="6bafe-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="6bafe-111">Criar um novo Aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="6bafe-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="6bafe-112">[Portal do Azure](https://portal.azure.com) > `+ New` > Procure pela "Aplicativo de funções"</span><span class="sxs-lookup"><span data-stu-id="6bafe-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="6bafe-113">Cria uma nova função de gatilho HTTP dentro do seu novo Aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="6bafe-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="6bafe-114">Sua função é preenchida previamente com o código que define uma API REST muito simples.</span><span class="sxs-lookup"><span data-stu-id="6bafe-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="6bafe-115">Qualquer cadeia de caracteres passada toohello função como um parâmetro de consulta ou no corpo de saudação é retornada como "Olá {entrada}"</span><span class="sxs-lookup"><span data-stu-id="6bafe-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="6bafe-116">Vá toohello `Integrate` guia da sua nova função do gatilho de HTTP</span><span class="sxs-lookup"><span data-stu-id="6bafe-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="6bafe-117">Ativar/desativar `Allowed HTTP methods` muito`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="6bafe-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="6bafe-118">Em `Selected HTTP methods` desmarque cada verbo, exceto POST.</span><span class="sxs-lookup"><span data-stu-id="6bafe-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="6bafe-119">![Métodos HTTP selecionados](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="6bafe-120">Esta etapa simplificará sua definição de API mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6bafe-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="6bafe-121"><a name="enable"></a>Habilitando suporte à definição de API</span><span class="sxs-lookup"><span data-stu-id="6bafe-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="6bafe-122">Navegue muito`your function name` > `Platform Features` > `API Definition`
![guia definição](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="6bafe-123">Definir `API Definition Source` muito`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="6bafe-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="6bafe-124">Esta etapa permite que um conjunto de opções OpenAPI para seu aplicativo de função, incluindo um toohost um arquivo de OpenAPI de domínio do seu aplicativo de função, uma cópia embutido de saudação do ponto de extremidade [OpenAPI Editor](http://editor.swagger.io)e um gerador de definição de início rápido.</span><span class="sxs-lookup"><span data-stu-id="6bafe-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="6bafe-125">![Definição habilitada](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="6bafe-126"><a name="create-definition"></a>Criando sua definição de API de um modelo</span><span class="sxs-lookup"><span data-stu-id="6bafe-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="6bafe-127">Clique em `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="6bafe-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="6bafe-128">Essa etapa verifica seu aplicativo de função para funções de gatilho de HTTP e usa informações de saudação na functions.json toogenerate um documento OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="6bafe-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="6bafe-129">Adicionar um objeto de operação muito`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="6bafe-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="6bafe-130">documento de OpenAPI de início rápido de saudação é uma estrutura de um documento OpenAPI completo. Ele exige mais metadados toobe uma definição de OpenAPI completa, como objetos de operação e modelos de resposta.</span><span class="sxs-lookup"><span data-stu-id="6bafe-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="6bafe-131">objeto de operação de exemplo Hello abaixo tem um preenchido produz/consome seção, um objeto de parâmetro e um objeto de resposta.</span><span class="sxs-lookup"><span data-stu-id="6bafe-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="6bafe-132">x-ms-summary fornece um nome de exibição em aplicativos lógicos, fluxo e PowerApps.</span><span class="sxs-lookup"><span data-stu-id="6bafe-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="6bafe-133">Check-out [personalizar sua definição de Swagger PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="6bafe-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="6bafe-134">Clique em `save` toosave suas alterações ![adicionando definição de modelo](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="6bafe-135"><a name="use-definition"></a>Usando sua definição de API</span><span class="sxs-lookup"><span data-stu-id="6bafe-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="6bafe-136">Copiar seu `API definition URL` e cole-o em um novo tooview de guia do navegador documento OpenAPI bruto.</span><span class="sxs-lookup"><span data-stu-id="6bafe-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="6bafe-137">Você pode importar seu OpenAPI documento tooany inúmeras ferramentas para teste e integração usando essa URL.</span><span class="sxs-lookup"><span data-stu-id="6bafe-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="6bafe-138">Muitos recursos do Azure são tooautomatically capaz de importar seu documento OpenAPI usando Olá URL de definição de API que é salvo em suas configurações de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="6bafe-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="6bafe-139">Como parte da saudação `Function` origem de definição de API, podemos atualizar essa url para você.</span><span class="sxs-lookup"><span data-stu-id="6bafe-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="6bafe-140"><a name="test-definition"></a>Usando Olá Swagger da interface do usuário tootest sua definição de API</span><span class="sxs-lookup"><span data-stu-id="6bafe-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="6bafe-141">Há são ferramentas de teste criadas no modo de interface do usuário toohello do editor de definição de API Olá incorporada.</span><span class="sxs-lookup"><span data-stu-id="6bafe-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="6bafe-142">Adicione sua chave de API e, em seguida, use Olá `Try this operation` botão em cada método.</span><span class="sxs-lookup"><span data-stu-id="6bafe-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="6bafe-143">ferramenta Olá usará a definição API tooformat Olá solicitações e respostas bem-sucedidas indicará se a sua definição está correta.</span><span class="sxs-lookup"><span data-stu-id="6bafe-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="6bafe-144">Etapas:</span><span class="sxs-lookup"><span data-stu-id="6bafe-144">Steps:</span></span>

1. <span data-ttu-id="6bafe-145">Copiar a chave de API da função</span><span class="sxs-lookup"><span data-stu-id="6bafe-145">Copy your function API key</span></span>
    1. <span data-ttu-id="6bafe-146">Olá API chave pode ser encontrada na função de gatilho de HTTP em `function name` > `Keys` > `Function Keys` 
   ![tecla de função](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="6bafe-147">Navegue toohello `API Definition` página.</span><span class="sxs-lookup"><span data-stu-id="6bafe-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="6bafe-148">Clique em `Authenticate` e adicione o objeto de segurança de chave toohello função API na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6bafe-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="6bafe-149">![Chave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="6bafe-150">selecione `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="6bafe-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="6bafe-151">Clique em `Try it out` e insira um nome tootest</span><span class="sxs-lookup"><span data-stu-id="6bafe-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="6bafe-152">Você verá um resultado de ÊXITO sob o `Pretty`
![teste de definição de API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="6bafe-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bafe-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bafe-153">Next steps</span></span>
* [<span data-ttu-id="6bafe-154">Definição de OpenAPI na visão geral de funções</span><span class="sxs-lookup"><span data-stu-id="6bafe-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="6bafe-155">Leia a documentação completa Olá para obter mais informações sobre o suporte de OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="6bafe-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="6bafe-156">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6bafe-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="6bafe-157">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="6bafe-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="6bafe-158">Repositório de GitHub do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6bafe-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="6bafe-159">Check-out Olá funções GitHub toogive nos comentários sobre a visualização de suporte de definição de saudação API!</span><span class="sxs-lookup"><span data-stu-id="6bafe-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="6bafe-160">Torne um problema do GitHub para qualquer coisa que você gostaria que toosee atualizado.</span><span class="sxs-lookup"><span data-stu-id="6bafe-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
