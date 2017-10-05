---
title: "Introdução aos metadados do OpenAPI no Azure Functions | Microsoft Docs"
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
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="af819-103">Criando metadados de OpenAPI 2.0 (Swagger) para um Aplicativo de funções (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="af819-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="af819-104">Este documento orienta você pelo processo passo a passo da criação de uma definição de OpenAPI para uma API simples hospedada no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="af819-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="af819-105">O que é OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="af819-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="af819-106">[Metadados de swagger](http://swagger.io/) é um arquivo que define a funcionalidade e os modos de operação de sua API e permite que uma função que hospeda uma API REST para serem consumidos por uma ampla variedade de outros softwares.</span><span class="sxs-lookup"><span data-stu-id="af819-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="af819-107">Ofertas da Microsoft, como PowerApps e [aplicativos de API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), bem como ferramentas de desenvolvedores terceiros, como [Postman](https://www.getpostman.com/docs/importing_swagger) e [muitos outros pacotes](http://swagger.io/tools/); todos permitem sua API a ser consumida com uma definição de Swagger.</span><span class="sxs-lookup"><span data-stu-id="af819-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="af819-108"><a name="prepare-function"></a>Criando uma função com uma API simples</span><span class="sxs-lookup"><span data-stu-id="af819-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="af819-109">Para criar uma definição de OpenAPI, primeiro precisamos criar uma função com uma API simples.</span><span class="sxs-lookup"><span data-stu-id="af819-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="af819-110">Se você já tiver uma API hospedada em um Aplicativo de funções, você poderá pular diretamente para a próxima seção</span><span class="sxs-lookup"><span data-stu-id="af819-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="af819-111">Criar um novo Aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="af819-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="af819-112">[Portal do Azure](https://portal.azure.com) > `+ New` > Procure pela "Aplicativo de funções"</span><span class="sxs-lookup"><span data-stu-id="af819-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="af819-113">Cria uma nova função de gatilho HTTP dentro do seu novo Aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="af819-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="af819-114">Sua função é preenchida previamente com o código que define uma API REST muito simples.</span><span class="sxs-lookup"><span data-stu-id="af819-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="af819-115">Qualquer cadeia de caracteres passada para a função como um parâmetro de consulta ou no corpo é retornada como "Olá {entrada}"</span><span class="sxs-lookup"><span data-stu-id="af819-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="af819-116">Vá para a guia `Integrate` da sua nova função de gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="af819-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="af819-117">Ativar/desativar `Allowed HTTP methods` para `Selected methods`</span><span class="sxs-lookup"><span data-stu-id="af819-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="af819-118">Em `Selected HTTP methods` desmarque cada verbo, exceto POST.</span><span class="sxs-lookup"><span data-stu-id="af819-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="af819-119">![Métodos HTTP selecionados](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="af819-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="af819-120">Esta etapa simplificará sua definição de API mais tarde.</span><span class="sxs-lookup"><span data-stu-id="af819-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="af819-121"><a name="enable"></a>Habilitando suporte à definição de API</span><span class="sxs-lookup"><span data-stu-id="af819-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="af819-122">Navegue até `your function name`  >  `Platform Features`  >  `API Definition` 
 ![guia definição](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="af819-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="af819-123">Defina `API Definition Source` como `Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="af819-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="af819-124">Esta etapa permite que um pacote de opções OpenAPI para seu Aplicativo de funções, incluindo um ponto de extremidade para hospedar um arquivo OpenAPI de domínio do seu Aplicativo de funções, uma cópia embutida do [Editor de OpenAPI](http://editor.swagger.io), e um gerador de definição de início rápido.</span><span class="sxs-lookup"><span data-stu-id="af819-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="af819-125">![Definição habilitada](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="af819-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="af819-126"><a name="create-definition"></a>Criando sua definição de API de um modelo</span><span class="sxs-lookup"><span data-stu-id="af819-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="af819-127">Clique em `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="af819-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="af819-128">Essa etapa verifica seu Aplicativo de funções para funções de gatilho de HTTP e usa as informações no functions.json para gerar um documento OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="af819-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="af819-129">Adicionar um objeto de operação para `paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="af819-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="af819-130">O documento de OpenAPI de início rápido é uma estrutura de tópicos de um documento OpenAPI completo. Ele requer que mais metadados sejam uma definição OpenAPI completa, como objetos de operação e modelos de resposta.</span><span class="sxs-lookup"><span data-stu-id="af819-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="af819-131">O objeto de operação de exemplo abaixo tem uma seção que produz/consome, um objeto de parâmetro e um objeto de resposta.</span><span class="sxs-lookup"><span data-stu-id="af819-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="af819-132">x-ms-summary fornece um nome de exibição em aplicativos lógicos, fluxo e PowerApps.</span><span class="sxs-lookup"><span data-stu-id="af819-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="af819-133">Confira [personalizar sua definição de Swagger para PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="af819-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="af819-134">Clique em `save` para salvar suas alterações ![Adicionando definição de modelo](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="af819-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="af819-135"><a name="use-definition"></a>Usando sua definição de API</span><span class="sxs-lookup"><span data-stu-id="af819-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="af819-136">Copie o `API definition URL` e cole-o em uma nova guia do navegador para exibir o documento OpenAPI bruto.</span><span class="sxs-lookup"><span data-stu-id="af819-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="af819-137">Você pode importar o documento de OpenAPI para qualquer número de ferramentas para teste e integração usando essa URL.</span><span class="sxs-lookup"><span data-stu-id="af819-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="af819-138">Muitos recursos do Azure são capazes de importar automaticamente o documento OpenAPI usando a URL de definição de API que é salvo em suas configurações de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="af819-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="af819-139">Como parte da `Function` fonte de definição de API, nós atualizamos essa URL para você.</span><span class="sxs-lookup"><span data-stu-id="af819-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="af819-140"><a name="test-definition"></a>Usando a interface do usuário do Swagger para testar sua definição de API</span><span class="sxs-lookup"><span data-stu-id="af819-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="af819-141">Existem ferramentas de teste integradas para o modo de exibição da interface do usuário do editor de definição de API incorporado.</span><span class="sxs-lookup"><span data-stu-id="af819-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="af819-142">Adicione sua chave de API e, em seguida, use o `Try this operation` botão em cada método.</span><span class="sxs-lookup"><span data-stu-id="af819-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="af819-143">A ferramenta usará a definição de API para formatar as solicitações e respostas bem-sucedidas indicará que a definição está correta.</span><span class="sxs-lookup"><span data-stu-id="af819-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="af819-144">Etapas:</span><span class="sxs-lookup"><span data-stu-id="af819-144">Steps:</span></span>

1. <span data-ttu-id="af819-145">Copiar a chave de API da função</span><span class="sxs-lookup"><span data-stu-id="af819-145">Copy your function API key</span></span>
    1. <span data-ttu-id="af819-146">A chave de API pode ser encontrada na função de gatilho de HTTP em `function name` > `Keys` > `Function Keys` 
   ![tecla de função](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="af819-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="af819-147">Navegue até a página `API Definition`.</span><span class="sxs-lookup"><span data-stu-id="af819-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="af819-148">Clique em `Authenticate` e adicione sua chave de API de função ao objeto de segurança na parte superior.</span><span class="sxs-lookup"><span data-stu-id="af819-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="af819-149">![Chave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="af819-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="af819-150">selecione `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="af819-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="af819-151">Clique em `Try it out` e digite um nome para testar</span><span class="sxs-lookup"><span data-stu-id="af819-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="af819-152">Você verá um resultado de ÊXITO sob o `Pretty`
![teste de definição de API](./media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="af819-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="af819-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af819-153">Next steps</span></span>
* [<span data-ttu-id="af819-154">Definição de OpenAPI na visão geral de funções</span><span class="sxs-lookup"><span data-stu-id="af819-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="af819-155">Leia a documentação completa para obter mais informações sobre o suporte de OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="af819-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="af819-156">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="af819-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="af819-157">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="af819-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="af819-158">Repositório de GitHub do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="af819-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="af819-159">Confira as funções de GitHub para fornecer comentários sobre a versão prévia de suporte de definição de API!</span><span class="sxs-lookup"><span data-stu-id="af819-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="af819-160">Execute o GitHub para qualquer coisa que você gostaria de ver atualizada.</span><span class="sxs-lookup"><span data-stu-id="af819-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
