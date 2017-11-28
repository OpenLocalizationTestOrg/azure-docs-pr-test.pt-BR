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
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="65576-103">Personalizar as definições da API gerada por Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="65576-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="65576-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="65576-104">Overview</span></span>
<span data-ttu-id="65576-105">Este artigo explica como toocustomize Swashbuckle toohandle comuns cenários em que convém tooalter Olá comportamento padrão:</span><span class="sxs-lookup"><span data-stu-id="65576-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="65576-106">O Swashbuckle gera identificadores de operação duplicados para sobrecargas dos métodos do controlador</span><span class="sxs-lookup"><span data-stu-id="65576-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="65576-107">Swashbuckle pressupõe que Olá somente uma resposta válida de um método é HTTP 200 (Okey)</span><span class="sxs-lookup"><span data-stu-id="65576-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="65576-108">Personalizar a geração de identificador de operação</span><span class="sxs-lookup"><span data-stu-id="65576-108">Customize operation identifier generation</span></span>
<span data-ttu-id="65576-109">O Swashbuckle gera identificadores de operação do Swagger concatenando o nome do controlador e o nome do método.</span><span class="sxs-lookup"><span data-stu-id="65576-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="65576-110">Esse padrão cria um problema quando você tem várias sobrecargas de um método: o Swashbuckle gera ids de operação duplicadas, o que é um JSON de Swagger inválido.</span><span class="sxs-lookup"><span data-stu-id="65576-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="65576-111">Por exemplo, Olá código do controlador a seguir faz com que Swashbuckle toogenerate três ids de operação Contact_Get.</span><span class="sxs-lookup"><span data-stu-id="65576-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="65576-112">Você pode resolver o problema de saudação manualmente, fornecendo métodos Olá nomes exclusivos, como a seguinte Olá para este exemplo:</span><span class="sxs-lookup"><span data-stu-id="65576-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="65576-113">Obter</span><span class="sxs-lookup"><span data-stu-id="65576-113">Get</span></span>
* <span data-ttu-id="65576-114">GetById</span><span class="sxs-lookup"><span data-stu-id="65576-114">GetById</span></span>
* <span data-ttu-id="65576-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="65576-115">GetPage</span></span>

<span data-ttu-id="65576-116">alternativa de saudação é tooextend Swashbuckle toomake-gerar automaticamente ids exclusivas de operação.</span><span class="sxs-lookup"><span data-stu-id="65576-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="65576-117">Olá etapas a seguir mostram como toocustomize Swashbuckle usando Olá *SwaggerConfig.cs* arquivo que está incluído no projeto de saudação pelo modelo de projeto do Visual Studio Preview de aplicativos de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="65576-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="65576-118">Você também pode personalizar o Swashbuckle em um projeto de API da Web que você configura para implantação como um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="65576-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="65576-119">Criar uma implementação de `IOperationFilter` personalizada</span><span class="sxs-lookup"><span data-stu-id="65576-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="65576-120">Olá `IOperationFilter` interface fornece um ponto de extensibilidade para usuários Swashbuckle que desejam toocustomize vários aspectos do processo de metadados do Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="65576-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="65576-121">Olá código a seguir demonstra um método de alteração de comportamento de geração de id de operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="65576-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="65576-122">código de saudação anexa o nome de id da operação de toohello de nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="65576-122">hello code appends parameter names toohello operation id name.</span></span>  
   
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
2. <span data-ttu-id="65576-123">Em *App_Start\SwaggerConfig.cs* arquivo, chamada hello `OperationFilter` Olá Swashbuckle de toouse do toocause método novo `IOperationFilter` implementação.</span><span class="sxs-lookup"><span data-stu-id="65576-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="65576-124">Olá *SwaggerConfig.cs* arquivo descartado pelo Olá pacote Swashbuckle NuGet contém muitos exemplos de comentada de pontos de extensibilidade.</span><span class="sxs-lookup"><span data-stu-id="65576-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="65576-125">comentários adicionais Olá não são mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="65576-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="65576-126">Depois de fazer essa alteração, o `IOperationFilter` implementação é usada e faz com que o toobe de ids de operação exclusivo gerado.</span><span class="sxs-lookup"><span data-stu-id="65576-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="65576-127">Permitir códigos de resposta diferentes de 200</span><span class="sxs-lookup"><span data-stu-id="65576-127">Allow response codes other than 200</span></span>
<span data-ttu-id="65576-128">Por padrão, Swashbuckle pressupõe que uma resposta HTTP 200 (Okey) é hello *somente* legítimas resposta de um método de API da Web.</span><span class="sxs-lookup"><span data-stu-id="65576-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="65576-129">Em alguns casos, convém tooreturn outros códigos de resposta sem causar Olá cliente tooraise uma exceção.</span><span class="sxs-lookup"><span data-stu-id="65576-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="65576-130">Por exemplo, hello API da Web código a seguir demonstra um cenário no qual você desejaria Olá cliente tooaccept uma resposta 200 ou 404 como as respostas válidas.</span><span class="sxs-lookup"><span data-stu-id="65576-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

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

<span data-ttu-id="65576-131">Nesse cenário, Olá Swagger Swashbuckle gera por padrão especifica apenas um legítimo código de status HTTP 200 HTTP.</span><span class="sxs-lookup"><span data-stu-id="65576-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="65576-132">Como o Visual Studio usa Olá toogenerate código da definição de Swagger API cliente Olá, ele cria código do cliente que gera uma exceção para qualquer resposta diferente de HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="65576-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="65576-133">Olá código a seguir é de um cliente c# gerado para este método de API da Web de exemplo.</span><span class="sxs-lookup"><span data-stu-id="65576-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

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

<span data-ttu-id="65576-134">Swashbuckle fornece duas maneiras de personalizar a lista de saudação de códigos de resposta HTTP esperados gerado usando comentários XML ou hello `SwaggerResponse` atributo.</span><span class="sxs-lookup"><span data-stu-id="65576-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="65576-135">atributo Olá é mais fácil, mas só está disponível no Swashbuckle 5.1.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="65576-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="65576-136">Aplicativos de API visualizar novo projeto modelo no Visual Studio 2013 Hello inclui Swashbuckle versão 5.0.0, portanto, se você usou o modelo de saudação e não quiser tooupdate Swashbuckle, sua única opção é toouse os comentários XML.</span><span class="sxs-lookup"><span data-stu-id="65576-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="65576-137">Personalizar códigos de resposta esperados ao utilizar comentários XML</span><span class="sxs-lookup"><span data-stu-id="65576-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="65576-138">Use os códigos de resposta de toospecify este método se sua versão Swashbuckle for anterior a 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="65576-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="65576-139">Primeiro, adicione comentários de documentação XML sobre desejar toospecify códigos de resposta HTTP para os métodos hello.</span><span class="sxs-lookup"><span data-stu-id="65576-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="65576-140">Executar uma ação de API da Web de exemplo hello tooit de documentação XML mostrado acima e aplicando Olá resultaria em código como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="65576-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
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
2. <span data-ttu-id="65576-141">Adicionar instruções no hello *SwaggerConfig.cs* toodirect Swashbuckle toomake uso do arquivo de documentação XML saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="65576-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="65576-142">Abra *SwaggerConfig.cs* e criar um método no hello *SwaggerConfig* arquivo de classe toospecify Olá caminho toohello documentação XML.</span><span class="sxs-lookup"><span data-stu-id="65576-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="65576-143">Role para baixo na Olá *SwaggerConfig.cs* arquivo até que você veja Olá comentada de linha de código semelhante a saudação captura tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="65576-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="65576-144">Remova os comentários Olá linha tooenable Olá XML processamento durante a geração de Swagger.</span><span class="sxs-lookup"><span data-stu-id="65576-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="65576-145">No arquivo de documentação XML do hello de toogenerate de ordem, vá para propriedades do projeto hello e habilitar Olá arquivo de documentação XML conforme mostrado na captura de tela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="65576-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="65576-146">Depois de executar essas etapas, Olá Swagger JSON gerado pelo Swashbuckle refletirá códigos de resposta HTTP Olá especificado nos comentários XML hello.</span><span class="sxs-lookup"><span data-stu-id="65576-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="65576-147">saudação de captura de tela abaixo demonstra essa nova carga JSON.</span><span class="sxs-lookup"><span data-stu-id="65576-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="65576-148">Quando você usa o código de cliente do Visual Studio tooregenerate Olá para a API REST, Olá código c# aceita ambos os códigos de status de HTTP Okey e não encontrada Olá sem gerar uma exceção, permitindo que as decisões de toomake código consumo em como Olá toohandle de retorno de um valor nulo Entre em contato com o registro.</span><span class="sxs-lookup"><span data-stu-id="65576-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

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

<span data-ttu-id="65576-149">código de saudação para esta demonstração pode ser encontrado em [este repositório GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="65576-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="65576-150">Juntamente com hello API da Web do projeto marcado com comentários de documentação XML é um projeto de aplicativo de Console que contém um cliente gerada para esta API.</span><span class="sxs-lookup"><span data-stu-id="65576-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="65576-151">Personalizar os códigos de resposta esperada usando o atributo SwaggerResponse Olá</span><span class="sxs-lookup"><span data-stu-id="65576-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="65576-152">Olá [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) atributo está disponível em Swashbuckle 5.1.5 e posterior.</span><span class="sxs-lookup"><span data-stu-id="65576-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="65576-153">Caso você tenha uma versão anterior em seu projeto, esta seção inicia explicando como Olá tooupdate Swashbuckle NuGet pacote para que você pode usar esse atributo.</span><span class="sxs-lookup"><span data-stu-id="65576-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="65576-154">No **Gerenciador de Soluções**, clique com o botão direito do mouse em seu projeto de API da Web e clique em **Gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="65576-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="65576-155">Clique em Olá *atualização* toohello próximo botão *Swashbuckle* pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="65576-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="65576-156">Adicionar Olá *SwaggerResponse* atributos toohello métodos de ação de API da Web para o qual você deseja toospecify códigos de resposta HTTP válidos.</span><span class="sxs-lookup"><span data-stu-id="65576-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
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
4. <span data-ttu-id="65576-157">Adicionar um `using` declaração de namespace do atributo hello:</span><span class="sxs-lookup"><span data-stu-id="65576-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="65576-158">Procurar toohello */swagger/docs/v1* URL do seu projeto e Olá vários códigos de resposta HTTP ficarão visíveis no hello Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="65576-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="65576-159">código de saudação para esta demonstração pode ser encontrado em [este repositório GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="65576-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="65576-160">Juntamente com hello projeto de API da Web decorados com hello *SwaggerResponse* atributo é um projeto de aplicativo de Console que contém um cliente gerada para esta API.</span><span class="sxs-lookup"><span data-stu-id="65576-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="65576-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65576-161">Next steps</span></span>
<span data-ttu-id="65576-162">Este artigo mostra como forma de saudação toocustomize Swashbuckle gera ids de operação e códigos de resposta válido.</span><span class="sxs-lookup"><span data-stu-id="65576-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="65576-163">Para obter mais informações, consulte [Swashbuckle no GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="65576-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

