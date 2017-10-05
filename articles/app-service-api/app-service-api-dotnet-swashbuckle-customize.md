---
title: "Personalizar as definições da API gerada por Swashbuckle"
description: "Aprenda a personalizar definições de API do Swagger que são geradas pelo Swashbuckle para um aplicativo de API no Serviço de Aplicativo do Azure."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: c83905a97fb2ee988fe06fc1f9a7379c1741fd02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Personalizar as definições da API gerada por Swashbuckle
## <a name="overview"></a>Visão geral
Este artigo explica como personalizar Swashbuckle para lidar com cenários comuns em que talvez você queira alterar o comportamento padrão:

* O Swashbuckle gera identificadores de operação duplicados para sobrecargas dos métodos do controlador
* O Swashbuckle pressupõe que somente a resposta válida de um método seja HTTP 200 (OK) 

## <a name="customize-operation-identifier-generation"></a>Personalizar a geração de identificador de operação
O Swashbuckle gera identificadores de operação do Swagger concatenando o nome do controlador e o nome do método. Esse padrão cria um problema quando você tem várias sobrecargas de um método: o Swashbuckle gera ids de operação duplicadas, o que é um JSON de Swagger inválido.

Por exemplo, o código de controlador a seguir faz com que o Swashbuckle gere três ids de operação Contact_Get.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Você pode resolver o problema manualmente fornecendo nomes exclusivos aos métodos, como no seguinte exemplo:

* Obter
* GetById
* GetPage

A alternativa é estender Swashbuckle para fazer com que ele gere automaticamente ids de operação exclusivas.

As etapas a seguir mostram como personalizar o Swashbuckle usando o arquivo *SwaggerConfig.cs* incluído no projeto pelo modelo de projeto de Visualização de aplicativos de API do Visual Studio.  Você também pode personalizar o Swashbuckle em um projeto de API da Web que você configura para implantação como um aplicativo de API.

1. Criar uma implementação de `IOperationFilter` personalizada 
   
    A interface `IOperationFilter` fornece um ponto de extensibilidade para usuários do Swashbuckle que desejam personalizar vários aspectos do processo de metadados do Swagger. O código a seguir demonstra um método para alterar o comportamento de geração de id de operação. O código acrescenta nomes de parâmetro ao nome de id de operação.  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. No arquivo *App_Start\SwaggerConfig.cs`IOperationFilter`, chamar o método* faz com que o Swashbuckle use a nova implementação de `OperationFilter`.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    O arquivo *SwaggerConfig.cs* que é fornecido pelo pacote do Swashbuckle NuGet contém muitos exemplos comentados de pontos de extensibilidade. Os comentários adicionais não são mostrados aqui. 
   
    Depois que você faz essa alteração, a implementação de `IOperationFilter` é usada e faz com que ids de operação exclusivas sejam geradas.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Permitir códigos de resposta diferentes de 200
Por padrão, o Swashbuckle supõe que uma resposta HTTP 200 (OK) é a *única* resposta legítima de um método de API da Web. Em alguns casos, você talvez queira retornar outros códigos de resposta sem fazer com que o cliente gere uma exceção.  Por exemplo, o código de API da Web a seguir demonstra um cenário no qual você deseja que o cliente aceite uma resposta 200 ou 404 como resposta válida.

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

Nesse cenário, o Swagger que o Swashbuckle gera por padrão especifica apenas um código de status HTTP legítimo, HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Como o Visual Studio usa a definição de API Swagger para gerar código para o cliente, ele cria o código do cliente que gera uma exceção para qualquer resposta que não seja um HTTP 200. O código a seguir é de um cliente C# gerado para esse método de API da Web de exemplo.

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

O Swashbuckle fornece duas maneiras de personalizar a lista de códigos de resposta HTTP esperados que é gerada, usando comentários XML ou o atributo `SwaggerResponse` . O atributo é mais fácil, mas só está disponível no Swashbuckle 5.1.5 ou posterior. O modelo de novo projeto de visualização de aplicativos da API no Visual Studio 2013 inclui Swashbuckle, versão 5.0.0, portanto, se você usou o modelo e não quiser atualizar o Swashbuckle, sua única opção é usar comentários XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Personalizar códigos de resposta esperados ao utilizar comentários XML
Use este método para especificar códigos de resposta se sua versão do Swashbuckle for anterior a 5.1.5.

1. Primeiro, adicione comentários da documentação XML sobre os métodos que você deseja para especificar os códigos de resposta HTTP. Usando a ação da API da Web de exemplo mostrada acima e aplicando a documentação XML a ela, resultaria em um código como o exemplo a seguir. 
   
        /// <summary>
        /// Returns the specified contact.
        /// </summary>
        /// <param name="id">The ID of the contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. Adicione instruções no arquivo *SwaggerConfig.cs* para direcionar o Swashbuckle para utilizar o arquivo de documentação XML.
   
   * Abra *SwaggerConfig.cs* e crie um método na classe *SwaggerConfig* para especificar o caminho para o arquivo de documentação XML. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Role para baixo no arquivo *SwaggerConfig.cs* até que você veja a linha comentada de códigos semelhantes à captura de tela abaixo. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Remova a marca de comentário da linha para habilitar o processamento de comentários XML durante a geração de Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Para gerar o arquivo de documentação XML, acesse as propriedades do projeto e habilite o arquivo de documentação XML, como mostrado na captura de tela abaixo. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Depois de executar essas etapas, o JSON do Swagger gerado pelo Swashbuckle refletirá os códigos de resposta HTTP que você especificou nos comentários XML. A captura de tela abaixo demonstra essa nova carga JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Quando você usa o Visual Studio para gerar o código do cliente para a API REST, o código C# aceita os códigos de status “HTTP OK” e “Não encontrado” sem gerar uma exceção, permitindo que seu código consumidor tome decisões sobre como tratar o retorno de um registro de contato nulo. 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

O código para esta demonstração pode ser encontrado [nesse repositório GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Junto com o projeto da API da Web marcado com comentários da documentação XML está um projeto de aplicativo de console que contém um cliente gerado para esta API. 

### <a name="customize-expected-response-codes-using-the-swaggerresponse-attribute"></a>Personalizar códigos de resposta esperados usando o atributo SwaggerResponse
O atributo [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) está disponível em Swashbuckle 5.1.5 e posterior. Caso você tenha uma versão anterior em seu projeto, esta seção inicia explicando como atualizar o pacote NuGet do Swashbuckle para que você possa usar esse atributo.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em seu projeto de API da Web e clique em **Gerenciar pacotes NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Clique no botão *Atualizar* próximo ao pacote do NuGet do *Swashbuckle*. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Adicione os atributos *SwaggerResponse* aos métodos de ação de API da Web para os quais você deseja especificar códigos de resposta HTTP válidos. 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. Adicione uma `using` declaração de namespace do atributo:
   
        using Swashbuckle.Swagger.Annotations;
5. Navegue até a URL */swagger/docs/v1* do seu projeto e os vários códigos de resposta HTTP estarão visíveis no JSON Swagger. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

O código para esta demonstração pode ser encontrado [nesse repositório GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Junto com o projeto da API da Web marcado com o atributo *SwaggerResponse* está um projeto de aplicativo de console que contém um cliente gerado para esta API. 

## <a name="next-steps"></a>Próximas etapas
Este artigo mostrou como personalizar a maneira que o Swashbuckle gera ids de operação e códigos de resposta válidos. Para obter mais informações, consulte [Swashbuckle no GitHub](https://github.com/domaindrivendev/Swashbuckle).

