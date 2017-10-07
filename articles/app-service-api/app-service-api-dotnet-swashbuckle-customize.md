---
title: "definições de aaaCustomize gerado Swashbuckle API"
description: "Saiba como definições de API de Swagger toocustomize que são geradas por Swashbuckle para um aplicativo de API no serviço de aplicativo do Azure."
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
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Personalizar as definições da API gerada por Swashbuckle
## <a name="overview"></a>Visão geral
Este artigo explica como toocustomize Swashbuckle toohandle comuns cenários em que convém tooalter Olá comportamento padrão:

* O Swashbuckle gera identificadores de operação duplicados para sobrecargas dos métodos do controlador
* Swashbuckle pressupõe que Olá somente uma resposta válida de um método é HTTP 200 (Okey) 

## <a name="customize-operation-identifier-generation"></a>Personalizar a geração de identificador de operação
O Swashbuckle gera identificadores de operação do Swagger concatenando o nome do controlador e o nome do método. Esse padrão cria um problema quando você tem várias sobrecargas de um método: o Swashbuckle gera ids de operação duplicadas, o que é um JSON de Swagger inválido.

Por exemplo, Olá código do controlador a seguir faz com que Swashbuckle toogenerate três ids de operação Contact_Get.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Você pode resolver o problema de saudação manualmente, fornecendo métodos Olá nomes exclusivos, como a seguinte Olá para este exemplo:

* Obter
* GetById
* GetPage

alternativa de saudação é tooextend Swashbuckle toomake-gerar automaticamente ids exclusivas de operação.

Olá etapas a seguir mostram como toocustomize Swashbuckle usando Olá *SwaggerConfig.cs* arquivo que está incluído no projeto de saudação pelo modelo de projeto do Visual Studio Preview de aplicativos de API de saudação.  Você também pode personalizar o Swashbuckle em um projeto de API da Web que você configura para implantação como um aplicativo de API.

1. Criar uma implementação de `IOperationFilter` personalizada 
   
    Olá `IOperationFilter` interface fornece um ponto de extensibilidade para usuários Swashbuckle que desejam toocustomize vários aspectos do processo de metadados do Swagger hello. Olá código a seguir demonstra um método de alteração de comportamento de geração de id de operação de saudação. código de saudação anexa o nome de id da operação de toohello de nomes de parâmetro.  
   
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
2. Em *App_Start\SwaggerConfig.cs* arquivo, chamada hello `OperationFilter` Olá Swashbuckle de toouse do toocause método novo `IOperationFilter` implementação.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Olá *SwaggerConfig.cs* arquivo descartado pelo Olá pacote Swashbuckle NuGet contém muitos exemplos de comentada de pontos de extensibilidade. comentários adicionais Olá não são mostrados aqui. 
   
    Depois de fazer essa alteração, o `IOperationFilter` implementação é usada e faz com que o toobe de ids de operação exclusivo gerado.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Permitir códigos de resposta diferentes de 200
Por padrão, Swashbuckle pressupõe que uma resposta HTTP 200 (Okey) é hello *somente* legítimas resposta de um método de API da Web. Em alguns casos, convém tooreturn outros códigos de resposta sem causar Olá cliente tooraise uma exceção.  Por exemplo, hello API da Web código a seguir demonstra um cenário no qual você desejaria Olá cliente tooaccept uma resposta 200 ou 404 como as respostas válidas.

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

Nesse cenário, Olá Swagger Swashbuckle gera por padrão especifica apenas um legítimo código de status HTTP 200 HTTP.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Como o Visual Studio usa Olá toogenerate código da definição de Swagger API cliente Olá, ele cria código do cliente que gera uma exceção para qualquer resposta diferente de HTTP 200. Olá código a seguir é de um cliente c# gerado para este método de API da Web de exemplo.

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

Swashbuckle fornece duas maneiras de personalizar a lista de saudação de códigos de resposta HTTP esperados gerado usando comentários XML ou hello `SwaggerResponse` atributo. atributo Olá é mais fácil, mas só está disponível no Swashbuckle 5.1.5 ou posterior. Aplicativos de API visualizar novo projeto modelo no Visual Studio 2013 Hello inclui Swashbuckle versão 5.0.0, portanto, se você usou o modelo de saudação e não quiser tooupdate Swashbuckle, sua única opção é toouse os comentários XML. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Personalizar códigos de resposta esperados ao utilizar comentários XML
Use os códigos de resposta de toospecify este método se sua versão Swashbuckle for anterior a 5.1.5.

1. Primeiro, adicione comentários de documentação XML sobre desejar toospecify códigos de resposta HTTP para os métodos hello. Executar uma ação de API da Web de exemplo hello tooit de documentação XML mostrado acima e aplicando Olá resultaria em código como Olá exemplo a seguir. 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
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
2. Adicionar instruções no hello *SwaggerConfig.cs* toodirect Swashbuckle toomake uso do arquivo de documentação XML saudação do arquivo.
   
   * Abra *SwaggerConfig.cs* e criar um método no hello *SwaggerConfig* arquivo de classe toospecify Olá caminho toohello documentação XML. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Role para baixo na Olá *SwaggerConfig.cs* arquivo até que você veja Olá comentada de linha de código semelhante a saudação captura tela abaixo. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Remova os comentários Olá linha tooenable Olá XML processamento durante a geração de Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. No arquivo de documentação XML do hello de toogenerate de ordem, vá para propriedades do projeto hello e habilitar Olá arquivo de documentação XML conforme mostrado na captura de tela de saudação abaixo. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Depois de executar essas etapas, Olá Swagger JSON gerado pelo Swashbuckle refletirá códigos de resposta HTTP Olá especificado nos comentários XML hello. saudação de captura de tela abaixo demonstra essa nova carga JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Quando você usa o código de cliente do Visual Studio tooregenerate Olá para a API REST, Olá código c# aceita ambos os códigos de status de HTTP Okey e não encontrada Olá sem gerar uma exceção, permitindo que as decisões de toomake código consumo em como Olá toohandle de retorno de um valor nulo Entre em contato com o registro. 

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

código de saudação para esta demonstração pode ser encontrado em [este repositório GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Juntamente com hello API da Web do projeto marcado com comentários de documentação XML é um projeto de aplicativo de Console que contém um cliente gerada para esta API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Personalizar os códigos de resposta esperada usando o atributo SwaggerResponse Olá
Olá [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atributo está disponível em Swashbuckle 5.1.5 e posterior. Caso você tenha uma versão anterior em seu projeto, esta seção inicia explicando como Olá tooupdate Swashbuckle NuGet pacote para que você pode usar esse atributo.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em seu projeto de API da Web e clique em **Gerenciar pacotes NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Clique em Olá *atualização* toohello próximo botão *Swashbuckle* pacote NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Adicionar Olá *SwaggerResponse* atributos toohello métodos de ação de API da Web para o qual você deseja toospecify códigos de resposta HTTP válidos. 
   
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
4. Adicionar um `using` declaração de namespace do atributo hello:
   
        using Swashbuckle.Swagger.Annotations;
5. Procurar toohello */swagger/docs/v1* URL do seu projeto e Olá vários códigos de resposta HTTP ficarão visíveis no hello Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

código de saudação para esta demonstração pode ser encontrado em [este repositório GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Juntamente com hello projeto de API da Web decorados com hello *SwaggerResponse* atributo é um projeto de aplicativo de Console que contém um cliente gerada para esta API. 

## <a name="next-steps"></a>Próximas etapas
Este artigo mostra como forma de saudação toocustomize Swashbuckle gera ids de operação e códigos de resposta válido. Para obter mais informações, consulte [Swashbuckle no GitHub](https://github.com/domaindrivendev/Swashbuckle).

