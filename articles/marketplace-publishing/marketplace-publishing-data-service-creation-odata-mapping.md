---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um serviço de dados para compra em hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Mapeando um tooOData de serviço da web existente por meio de CSDL
> [!IMPORTANT]
> **Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.** Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners). Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Este artigo fornece uma visão geral sobre como toouse uma toomap CSDL um tooan de serviço existente serviço compatível com OData. Ele explica como o documento de mapeamento toocreate hello (CSDL) que transforma a solicitação de entrada de saudação do cliente Olá por meio de uma chamada de serviço e hello saída (dados) volta toohello cliente por meio de um feed de OData compatível. Microsoft Azure Marketplace expõe os usuários finais toohello de serviços usando o protocolo OData de saudação. Os serviços expostos pelos provedores de conteúdo (Proprietários de Dados) são expostos de diversas formas, como REST, SOAP etc.

## <a name="what-is-a-csdl-and-its-structure"></a>O que é uma CSDL e sua estrutura?
Um CSDL (linguagem de definição de esquema conceitual) é uma especificação que define como serviço da web de toodescribe ou banco de dados de serviço em comum XML argumentação toohello Azure Marketplace.

Simples visão geral de saudação **fluxo de solicitação:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Olá **fluxo de dados** está em Olá oposta direção:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Figura 1** diagramas como o cliente deve obter dados de um provedor de conteúdo (o serviço) por meio de saudação do Azure Marketplace.  Olá CSDL é usado por solicitação de saudação de toohandle do componente de transformação do mapeamento hello e passam dados entre Olá solicitando o cliente e os serviços de provedor de conteúdo hello.

*Figura 1: O fluxo detalhado solicitem provedor toocontent do cliente por meio do Azure Marketplace*

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Para obter informações sobre o Atom, Atom Pub e protocolo do OData Olá após a qual Olá compilação de extensões do Azure Marketplace, consulte: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Trecho acima link: *"finalidade de saudação do protocolo Open Data de saudação (daqui em diante chamado tooas OData) é o protocolo de tooprovide um baseado em REST para operações de estilo CRUD (criar, ler, atualizar e excluir) com base nos recursos expostos como serviços de dados. Um "serviço de dados" é um ponto de extremidade no qual há dados expostos de uma ou mais "coleções", cada um com zero ou mais "entradas", compostas por pares de valor nomeado digitados. OData é publicado pela Microsoft em padrões do OASIS (Organization for Olá padrões de avanço de informações estruturado) para que qualquer pessoa que deseja toocan criar servidores, clientes ou ferramentas sem royalties ou restrições."*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Três partes críticas que têm toobe definido pelo Olá CSDL são:
* Olá **ponto de extremidade** de provedor de serviços de hello Olá Web endereço (URI) da saudação serviço
* Olá **parâmetros de dados** que está sendo passado como entrada toohello provedor de serviços de definições de saudação de parâmetros de saudação enviados serviço do provedor de toohello conteúdo toohello tipo de dados.
* **Esquema** Olá dados de esquema de Olá solicitando serviço toohello de dados Olá sendo entregues pelo serviço do provedor de saudação conteúdo retornados, incluindo o contêiner, coleções e tabelas, colunas/variáveis e tipos de dados.

Olá diagrama a seguir mostra uma visão geral do fluxo de saudação de onde o cliente de Olá insere Olá OData (serviço de web chamada toohello do provedor de conteúdo) da instrução toogetting Olá resultados/dados de volta.

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>Etapas:
1. Cliente envia a solicitação por meio de chamada de serviço concluída com parâmetros de entrada definidos no XML toohello Azure Marketplace
2. A CSDL é usado toovalidate Olá chamada de serviço.
   * Olá formatada chamada de serviço é enviada toohello serviço de provedores de conteúdo por hello Azure Marketplace
3. Hello Webservice executa e valida ou não a ação de saudação do hello verbo Http (ou seja, obter) são retornados dados de saudação tooAzure Marketplace onde Olá solicitou dados (se houver) é expõe em formato XML toohello cliente usando Olá mapeamento definido no hello CSDL.
4. Olá cliente é enviado dados saudação (se houver) em formato XML ou JSON

## <a name="definitions"></a>Definições
### <a name="odata-atom-pub"></a>ATOM pub OData
Uma publicação ATOM toohello extensão em que cada entrada representa uma linha de um resultado definido. Olá parte conteúdo entrada hello é aprimorado toocontain Olá valores de linha hello – como pares chave-valor. Encontre mais informações aqui: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - Linguagem de Definição de Esquema Conceitual
Permite definir funções (SPROCs) e entidades expostas por meio de um banco de dados. Encontre mais informações aqui: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Clique em Olá **outras versões** lista suspensa e selecione uma versão, se você não vir o artigo hello.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - Modelo de Dados de Entrada
* Visão geral: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Visualização: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Tipos de dados: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Veja a seguir Olá Olá detalhadas tooRight esquerdo fluxo de onde o cliente de Olá insere Olá OData (serviço de web chamada toohello do provedor de conteúdo) da instrução toogetting Olá resultados/dados de volta:

  ![desenho](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Noções básicas de CSDL
Um CSDL (linguagem de definição de esquema conceitual) é uma especificação que define como serviço da web de toodescribe ou banco de dados de serviço em comum XML argumentação toohello Azure Marketplace. Descreve CSDL Olá crítico peças que **possibilita a passagem de saudação de dados da fonte de dados de saudação toohello Azure Marketplace.** partes principais da saudação são descritas aqui:

* Informações de interface que descrevem todas as funções disponíveis publicamente (Nó FunctionImport)
* Informações de tipo de dados para todas as solicitações (entrada) e respostas (saídas) de mensagem (nós EntitySet/EntityContainer/EntityType)
* Informações sobre Olá toobe de protocolo de transporte de associação usado (nó de cabeçalho)
* Informações de endereço para a localização de saudação especificado (atributo BaseURI) de serviço

Em resumo, Olá CSDL representa um contrato de independente de plataforma e de idioma entre o solicitante de serviço hello e provedor de serviços de saudação. Usando Olá CSDL, um cliente pode localizar um serviço de banco de dados/serviço da web e invocar qualquer de suas funções publicamente disponíveis.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Relacionando um tooa CSDL banco de dados ou uma coleção
**Olá especificação CSDL**

A CSDL é uma gramática XML para descrição de um serviço Web. especificação da saudação é dividida em 4 elementos principais: EntitySet, FunctionImport; NameSpace e EntityType.

toomake este toounderstand mais fácil de abstração permite relacionar uma tabela de tooa CSDL.

Lembre-se;

  CSDL representa um contrato independente de plataforma e de idioma entre hello **solicitante serviço** e hello **provedor**. Com a CSDL, um **cliente** pode localizar um **serviço Web/serviço de banco de dados** e chamar suas **funções** disponíveis publicamente.

Para uma saudação do serviço de dados quatro partes de um CSDL pode ser considerado em termos de um banco de dados, tabela, coluna e procedimento armazenado.

Relacione essas partes da seguinte maneira para um Serviço de Dados:

* EntityContainer ~= Database
* EntitySet ~= Table
* EntityType ~= Columns
* FunctionImport ~= Stored Procedure

**Verbos HTTP permitidos**

* GET-retorna os valores do banco de dados de saudação (retorna uma coleção)
* POST – toopass tooand opcional retornar valores de dados usados do banco de dados da saudação (criar uma nova entrada na coleção de hello, retorno de id/URI)
* Excluir – exclui dados de saudação DB (exclui uma coleção)
* PUT – atualizar dados em um banco de dados (substituir uma coleção ou criar uma)

## <a name="metadatamapping-document"></a>Documento de metadados/mapeamento
documento de metadados/mapeamento Olá é usado toomap web existentes de um provedor de conteúdo serviços para que pode ser exposta como um serviço web OData pelo sistema do Azure Marketplace hello. Ele se baseia na CSDL e implementa algumas extensões tooCSDL tooaccommodate Olá necessidades do REST com base em serviços da web expostos por meio do Azure Marketplace. Olá extensões são encontradas no hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.

Segue um exemplo de hello CSDL: (copiar e colar Olá CSDL do exemplo em um editor de XML abaixo e alterar toomatch seu serviço.  Cole no mapeamento de CSDL DataService guia ao criar seu serviço em Olá [Portal de publicação do Azure Marketplace](https://publish.windowsazure.com)).

**Termos:** Relating Olá CSDL termos toohello [Portal de publicação](https://publish.windowsazure.com) termos de interface do usuário (PPUI).

* Oferecer "Title" hello PPUI relaciona tooMyWebOffer
* MyCompany em Olá PPUI relaciona muito**nome de exibição do publicador** em Olá [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) interface do usuário
* A API relacionada tooa da Web ou serviço de dados (um plano no hello PPUI)

**Hierarquia:** uma Empresa (Provedor de Conteúdo) tem Ofertas com Planos, ou seja, Serviços, que se alinham a uma API.

### <a name="webservice-csdl-example"></a>Exemplo de CSDL de Serviço Web
Conecta-se o serviço de tooa que é expor um ponto de extremidade de aplicativo da web (como um aplicativo c#)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Exibir mais exemplos de serviço da Web de CSDL artigo Olá [exemplos de mapeamento existente web tooOData de serviço por meio de CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Exemplo de CSDL de DataService
Conecta-se o serviço tooa que expõe uma tabela de banco de dados ou o modo de exibição como um ponto de extremidade de exemplo abaixo mostra duas APIs de banco de dados com base em CSDL de API (pode usar modos de exibição em vez de tabelas).

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>Consulte também
* Se você estiver interessado em aprendizado e nós específicos de saudação de compreensão e seus parâmetros, leia este artigo [dados serviço OData mapeamento nós](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para definições e explicações, exemplos e contexto de casos de uso.
* Se você estiver interessado em examinar os exemplos, leia este artigo [dados serviço OData mapeamento exemplos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de exemplo e entender a sintaxe de código e o contexto.
* toohello tooreturn prescrita caminho para publicar um serviço de dados de toohello Azure Marketplace, leia este artigo [guia de publicação de serviço de dados](marketplace-publishing-data-service-creation.md).

