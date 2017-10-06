---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um serviço de dados para compra em hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Noções básicas sobre o esquema de nós Olá para mapear um tooOData de serviço da web existente por meio de CSDL
> [!IMPORTANT]
> **Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.** Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners). Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Este documento ajudará a esclarecer a estrutura de nó Olá para mapear um tooCSDL de protocolo OData. É importante toonote que a estrutura de nó hello está bem formado XML. Então o esquema raiz, pai e filho é aplicável ao desenhar o seu mapeamento de OData.

## <a name="ignored-elements"></a>Elementos ignorados
Olá seguem Olá alto níveis elementos CSDL (nós XML) que não estejam sendo toobe usada pelo back-end do hello Azure Marketplace durante a importação de saudação de metadados do serviço da web hello. Eles podem estar presentes, mas serão ignorados.

| Elemento | Escopo |
| --- | --- |
| Usando o elemento |nó de Hello, nós sub e todos os atributos |
| Elemento de documentação |nó de Hello, nós sub e todos os atributos |
| ComplexType |nó de Hello, nós sub e todos os atributos |
| Elemento de associação |nó de Hello, nós sub e todos os atributos |
| Propriedade estendida |nó de Hello, nós sub e todos os atributos |
| EntityContainer |Somente hello seguintes atributos são ignorados: *estende* e *AssociationSet* |
| Esquema |Somente hello seguintes atributos são ignorados: *Namespace* |
| FunctionImport |Somente hello seguintes atributos são ignorados: *modo* (o valor padrão de ln é assumido) |
| EntityType |Somente hello seguintes subnós são ignorados: *chave* e *PropertyRef* |

Olá informações a seguir descrevem Olá alterações (adicionado e ignorados elementos) toohello vários nós de CSDL XML em detalhes.

## <a name="functionimport-node"></a>Nó FunctionImport
Um nó de FunctionImport representa uma URL (ponto de entrada) que expõe um usuário final toohello de serviço. nó de saudação permite que descreve como a URL de saudação é resolvido, quais parâmetros são toohello disponível ao usuário final e como esses parâmetros são fornecidos.

Há detalhes sobre esse nó [aqui][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)

Olá seguem atributos adicionais hello (ou adições tooattributes) que são expostas pelo nó de FunctionImport hello:

**d:BaseUri** -modelo de URI Olá para o recurso REST de saudação que é exposto tooMarketplace. Marketplace usa tooconstruct consultas modelo Olá Olá serviço web REST. modelo de URI Olá contém espaços reservados para parâmetros de saudação na forma de saudação de {parameterName}, onde o nome do parâmetro é o nome de saudação do parâmetro hello. Ex.: apiVersion={apiVersion}.
Parâmetros são permitidos tooappear como parâmetros URI ou como parte do caminho do URI de saudação. No caso de saudação de aparência Olá no caminho de saudação eles sempre são obrigatórios (não pode ser marcado como anulável). *Exemplo:* `d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Nome** -nome de saudação do hello importados de função.  Não é possível ser Olá mesmo que outros nomes definidos no hello CSDL.  Ex.: Name="GetModelUsageFile"

**EntitySet** *(opcional)* - se a função hello retorna uma coleção de tipos de entidade, o valor de saudação do hello **EntitySet** deve ser a coleção de Olá Olá entidade definida toowhich pertence. Caso contrário, Olá **EntitySet** atributo não deve ser usado. *Exemplo:* `EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(opcional)* -Especifica o tipo de saudação de elementos retornados pela Olá URI.  Não use esse atributo se a função hello não retorna um valor. Olá seguem tipos Olá com suporte:

* **Coleção (<Entity type name>)**: especifica uma coleção de tipos de entidade definidos. nome de saudação está presente no atributo de nome de saudação do nó de EntityType hello. Um exemplo é Collection(WXC.HourlyResult).
* **Bruto (<mime type>)**: especifica um documento/blob bruto que é retornado toohello usuário. Um exemplo é Raw(image/jpeg) outros exemplos:

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:paging** -Especifica como a paginação é tratada pelo Olá recurso REST. Olá parâmetro valores são usados em chaves braches, por exemplo, a página = {$page} & itemsperpage = Olá {$size} opções disponíveis são:

* **None:** nenhuma paginação está disponível
* **Skip:** a paginação é expressa por meio de uma lógica "skip" e "take" (superior). Ignorar pula sobre take e M elementos e em seguida, retorna Olá Avançar N elementos. Parameter value: $skip
* **Take:** Take retorna Olá próximos N elementos. Parameter value: $take
* **PageSize:** a paginação é expressa por meio de uma página lógica e o tamanho (itens por página). Página representa Olá da página atual que é retornado. Parameter value: $page
* **Tamanho:** tamanho representa o número de saudação de itens retornados para cada página. Parameter value: $size

**d:AllowedHttpMethods** *(opcional)* -Especifica o verbo é manipulado pelo recurso REST de saudação. Além disso, restringe toohello aceita verbo especificado valor.  Padrão = POST.  *Exemplo:* `d:AllowedHttpMethods="GET"` Olá opções disponíveis são:

* **GET:** normalmente usadas tooreturn dados
* **POSTAGEM:** normalmente usadas tooinsert novos dados
* **PUT:** normalmente usadas tooupdate dados
* **EXCLUSÃO:** toodelete dados usados

Nós filho adicionais (não abordadas pela documentação de CSDL Olá) no nó de FunctionImport Olá são:

**d:RequestBody** *(opcional)* -solicitação Olá corpo é usado tooindicate que Olá solicitação espera um toobe corpo enviado. Parâmetros podem ser fornecidos no corpo da solicitação hello. Eles são expressos entre chaves, por exemplo, {parameterName}. Esses parâmetros são mapeados da saudação entrada do usuário no corpo da saudação que é transferido serviço do provedor de toohello conteúdo. elemento de requestBody Olá tem um atributo com nome httpMethod. atributo Olá permite que dois valores:

* **POSTAGEM:** usado se a solicitação de saudação é um HTTP POST
* **GET:** usado se a solicitação de saudação é um HTTP GET

    Exemplo:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:namespaces** e **d:Namespace** -este nó descreve Olá namespaces que estão definidos na Olá XML retornado pela importação de função hello (ponto de extremidade do URI). Olá XML que é retornado pelo serviço de back-end Olá pode conter qualquer número de conteúdo de saudação do namespaces toodifferentiate que é retornado. **Todos esses espaços para nome, se usado em consultas de XPath d:Map ou d:Match necessário toobe listado.** nó de d:Namespaces Olá contém uma conjunto/lista de nós de d:Namespace. Cada um deles lista um espaço para nome usado na resposta do serviço de back-end de saudação. Olá seguem Olá atributo de saudação d:Namespace nó:

* **d:prefix:** Olá prefixo de namespace hello, como visto no hello resultados XML retornados pelo serviço hello, por exemplo, f:FirstName, f:LastName, onde f é o prefixo de saudação.
* **d:URI:** Olá completo URI do namespace Olá usado no documento de resultado de saudação. Representa o valor de saudação prefixo Olá é resolvido tooat tempo de execução.

**d:ErrorHandling** *(Opcional)* - Esse nó contém condições para tratamento de erros. Cada uma das condições de saudação é validada em relação a resultados de saudação que é retornado pelo serviço do provedor de saudação conteúdo. Se Olá proposto o código de erro HTTP corresponde a uma condição de uma mensagem de erro é retornada toohello do usuário final.

**d:ErrorHandling** *(opcional)* e **d:Condition** *(opcional)* -um nó de condição contém uma condição que é verificada no hello resultado retornado pelo serviço do provedor de saudação conteúdo. Olá seguem Olá **necessária** atributos:

* **d:match:** uma expressão XPath que valida se um determinado nó/valor está presente no provedor de conteúdo de saudação de saída XML. Olá XPath é executada em relação a saída de hello e deve retornar true se a condição de saudação é uma correspondência ou FALSO caso contrário.
* **d:HttpStatusCode:** Olá código de status HTTP deve ser retornado pelo Marketplace em Olá Olá caso condição correspondências. Marketplace signalizes usuário de toohello de erros por meio de códigos de status HTTP. Uma lista de códigos de status HTTP estão disponíveis em https://pt.wikipedia.org/wiki/Lista_de_c%C3%B3digos_de_estado_HTTP
* **d:ErrorMessage:** mensagem de erro de saudação que é retornado, com código de status HTTP de hello – toohello pelos usuários finais. Essa deve ser uma mensagem de erro amigável que não contém nenhum segredo.

**d:Title** *(opcional)* -permite descrever o título de saudação do função hello. valor Olá título Olá é proveniente

* Olá mapa opcional atributo (um xpath) que especifica onde toofind título de saudação em resposta Olá retornado da solicitação de serviço de saudação.
* - Ou - título Olá especificado como o valor do nó de saudação.

**d:Rights** *(opcional)* -Olá direitos (por exemplo, direitos autorais) associados à função hello. valor Olá direitos Olá seja proveniente de:

* Olá mapa opcional atributo (um xpath) que especifica onde toofind direitos de saudação em resposta Olá retornado da solicitação de serviço de saudação.
* - Ou - Olá direitos especificados como o valor do nó de saudação.

**d:Description** *(opcional)* - uma breve descrição para a função hello. Valor Descrição Olá Olá é proveniente

* Olá mapa opcional atributo (um xpath) que especifica onde toofind descrição de saudação em resposta Olá retornado da solicitação de serviço de saudação.
* - Ou – descrição Olá especificado como o valor do nó de saudação.

**d:EmitSelfLink** - *Veja o exemplo acima "FunctionImport para 'Paginação' através dos dados retornados"*

**d:EncodeParameterValue** -tooOData extensão opcional

**d:QueryResourceCost** -tooOData extensão opcional

**d:Map** -tooOData extensão opcional

**d:Headers** -tooOData extensão opcional

**d:Headers** -tooOData extensão opcional

**d:Value** -tooOData extensão opcional

**d:HttpStatusCode** -tooOData extensão opcional

**d:ErrorMessage** -tooOData extensão opcional

## <a name="parameter-node"></a>Nó do parâmetro
Este nó representa um parâmetro que é exposto como parte do modelo de URI Olá / corpo foi especificado no nó de FunctionImport Olá da solicitação.

Uma página do documento muito útil detalhes sobre o nó de "elemento de parâmetro" hello é encontrada em [aqui](http://msdn.microsoft.com/library/ee473431.aspx) (Olá Use **versão outras** suspensa tooselect uma versão diferente, se necessário tooview Olá documentação). *Exemplo:* `<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Atributo de parâmetro | Obrigatório | Valor |
| --- | --- | --- |
| Nome |Sim |nome de saudação do parâmetro hello. Diferencia maiúsculas de minúsculas!  Diferenciar maiusculas de minúsculas de BaseUri de saudação. **Exemplo:** `<Property Name="IsDormant" Type="Byte" />` |
| Tipo |Sim |tipo de parâmetro Hello. Olá valor deve ser um **EDMSimpleType** ou um tipo complexo que está dentro do escopo de saudação do modelo de saudação. Para obter mais informações, consulte "Os 6 tipos de propriedade/parâmetro compatíveis".  (Diferencia maiúsculas de minúsculas! O primeiro caractere é maiúsculo, os demais são minúsculos.)  Confira também [Tipos de modelo conceituais (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Exemplo:** `<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |Não |**Em**, Out ou InOut dependendo se o parâmetro hello é uma entrada, saída ou parâmetro de entrada/saída. (Somente "IN" está disponível no Azure Marketplace.) **Exemplo:** `<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |Não |Olá comprimento máximo permitido de parâmetro hello. **Exemplo:** `<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precisão |Não |precisão de saudação do parâmetro hello. **Exemplo:** `<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Escala |Não |escala de saudação do parâmetro hello. **Exemplo:** `<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Olá seguem atributos Olá que tenham sido adicionados a especificação de CSDL toohello:

| Atributo de parâmetro | Descrição |
| --- | --- |
| **d:Regex** *(Opcional)* |Uma instrução de regex usado toovalidate valor de entrada hello parâmetro hello. Se o valor de entrada hello não coincidir com valor de Olá Olá instrução será rejeitado. Isso permite toospecify também um conjunto de valores possíveis, por exemplo, ^ [0-9] +? $ tooonly permitir números. **Exemplo:** `<Nome do Parâmetro="name" Modo="In" Tipo="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Descrição="Um nome que não pode conter espaços ou caracteres não alfanumérico e não inglês" d:SampleValues="George |
| **d:Enum** *(Opcional)* |Um pipe separados a lista de valores válidos para o parâmetro hello. tipo de saudação de valores hello deve toomatch Olá definido pelo tipo de saudação parâmetro. Exemplo: `inglês |
| **d:Nullable** *(Opcional)* |Permite definir se um parâmetro pode ser nulo. saudação padrão é: true. No entanto, os parâmetros que são expostos como parte do caminho de saudação no modelo de URI de saudação não podem ser nulos. Quando o atributo de saudação é definido toofalse para esses parâmetros – Olá entrada do usuário é substituída. **Exemplo:** `<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(Opcional)* |Um valor do exemplo toodisplay como toohello uma observação cliente em Olá da interface do usuário.  É possível listar tooadd separados de diversos valores usando um pipe, por exemplo, ' um |

## <a name="entitytype-node"></a>Nó EntityType
Este nó representa um dos tipos de saudação que são retornados de usuário do Marketplace toohello final. Ele também contém o mapeamento de saudação da saída de saudação que é retornado por valores de toohello do serviço do provedor de saudação conteúdo retornados toohello do usuário final.

Detalhes sobre esse nó são encontrados em [aqui](http://msdn.microsoft.com/library/bb399206.aspx) (Olá Use **versão outras** suspensa tooselect uma versão diferente, se necessário tooview Olá documentação.)

| Nome do atributo | Obrigatório | Valor |
| --- | --- | --- |
| Nome |Sim |nome de Olá Olá do tipo de entidade. **Exemplo:** `<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |Não |nome da saudação de outro tipo de entidade que é do tipo de base de saudação do tipo de entidade Olá que está sendo definido. **Exemplo:** `<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Olá seguem atributos Olá que tenham sido adicionados a especificação de CSDL toohello:

**d:Map** -uma expressão XPath executada na saída do serviço de saudação. Olá suposição aqui é que a saída de serviço de Olá contém um conjunto de elementos que se repetem, como um ATOM feed onde há um conjunto de nós de entrada que se repetem. Cada um desses nós de repetição contém um registro. Olá XPath for toopoint especificado no nó de repetição individuais Olá no resultado de serviço do provedor de saudação conteúdo que contém valores de saudação para um registro individual. Exemplo de saída do serviço de saudação:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Olá expressão XPath seria /foo/bar porque cada nó da barra Olá Olá Olá nó de saída e seu conteúdo Olá real que é retornado toohello do usuário final de repetição.

**Key** - Esse atributo é ignorado pelo Marketplace. Em geral, os serviços web baseado em REST não expõem uma chave primária.

## <a name="property-node"></a>Nó de propriedade
Esse nó contém uma propriedade de registro de saudação.

Detalhes sobre esse nó são encontrados em [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (Olá Use **versão outras** suspensa tooselect uma versão diferente, se necessário tooview Olá documentação.) *Exemplo:* `<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | obrigatórios | Valor |
| --- | --- | --- |
| Nome |Sim |nome de saudação da propriedade de saudação. |
| Tipo |Sim |tipo de saudação do valor da propriedade hello. tipo de valor de propriedade Olá deve ser um **EDMSimpleType** ou um tipo complexo (indicado por um nome totalmente qualificado) que está dentro do escopo do modelo de saudação. Para obter mais informações, consulte os tipos de modelo conceituais (CSDL). |
| Nullable |Não |**True** (Olá valor padrão) ou **False** dependendo se a propriedade Olá pode ter um valor nulo. Observação: Em Olá versão de CSDL indicado pelo Olá [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) namespace, uma propriedade de tipo complexo deve ter Nullable = "False". |
| DefaultValue |Não |valor padrão de saudação da propriedade hello. |
| MaxLength |Não |comprimento máximo de saudação do valor da propriedade hello. |
| FixedLength |Não |**True** ou **False** dependendo se o valor da propriedade hello será armazenado como uma cadeia de caracteres de comprimento de fiexed. |
| Precisão |Não |Refere-se toohello o número máximo de dígitos tooretain no valor numérico hello. |
| Escala |Não |Número máximo de casas decimais tooretain no valor numérico hello. |
| Unicode |Não |**True** ou **False** dependendo se o valor da propriedade Olá ser armazenado como uma cadeia de caracteres Unicode. |
| Collation |Não |Uma cadeia de caracteres que especifica a saudação toobe de sequência usado na fonte de dados de saudação de agrupamento. |
| ConcurrencyMode |Não |**Nenhum** (Olá valor padrão) ou **fixo**. Se o valor de saudação é definido muito**fixo**, será usado o valor da propriedade Olá em verificações de simultaneidade otimista. |

Olá seguem os atributos adicionais Olá especificação de CSDL toohello foram adicionados:

**d:Map** -expressão XPath executada no serviço de saudação de saída e extrai uma propriedade de saída de hello. Olá XPath especificada é relativa toohello repetindo o nó que foi selecionado no XPath do nó de EntityType hello. Também é possível toospecify um tooallow XPath absoluto incluindo um recurso estático em cada Olá nós, como por exemplo uma declaração de direitos autorais é encontrada apenas depois de saudação serviço original de saída mas deve estar presente em cada uma das linhas Olá Olá OData de saída saída. Exemplo de serviço hello:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

expressão do XPath Olá aqui seria o nó do ./bar/baz0 tooget Olá baz0 do serviço do provedor de saudação conteúdo.

**d:CharMaxLength** -para o tipo de cadeia de caracteres, você pode especificar o comprimento máximo de saudação. Exemplo de CSDL de DataService

**d:IsPrimaryKey** -indica se a coluna de saudação é a chave primária Olá na exibição da tabela hello. Exemplo de CSDL de DataService.

**d:isExposed** -determina se o esquema da tabela Olá é exposta (geralmente true). Exemplo de CSDL de DataService

**d:IsView** *(Opcional)* - true se for baseado em um modo de exibição em vez de uma tabela.  Exemplo de CSDL de DataService

**d:Tableschema** - Consulte o exemplo de CSDL de DataService

**d:ColumnName** -é Olá nome da coluna de saudação na exibição da tabela hello.  Exemplo de CSDL de DataService

**d:IsReturned** -é hello booliano que determina se Olá serviço expõe este cliente toohello de valor.  Exemplo de CSDL de DataService

**d:IsQueryable** -é hello booliano que determina se a coluna Olá pode ser usada em uma consulta de banco de dados.   Exemplo de CSDL de DataService

**d:OrdinalPosition** -é Olá posição da coluna numérica da aparência, x, na tabela de saudação ou exibição de hello, onde x é de 1 toohello o número de colunas na tabela de saudação.  Exemplo de CSDL de DataService

**d:DatabaseDataType** -é Olá o tipo de dados da coluna Olá no banco de dados de hello, ou seja, o tipo de dados SQL. Exemplo de CSDL de DataService

## <a name="supported-parametersproperty-types"></a>Tipos de parâmetros/propriedade compatíveis
Olá seguem tipos Olá tem suportada para parâmetros e propriedades. (Diferencia maiúsculas de minúsculas)

| Tipos primitivos | Descrição |
| --- | --- |
| Nulo |Representa a ausência de saudação de um valor |
| Booliano |Representa o conceito matemático de saudação da lógica de valores binários |
| Byte |Valor inteiro não assinado de 8 bits |
| DateTime |Representa a data e hora com valores que variam de 00:00:00, meia-noite de 1º de janeiro de 1753 D.C. até 23:59:59, dezembro de 9999 D.C. |
| Decimal |Representa valores numéricos com precisão e escala fixas. Esse tipo pode descrever um valor numérico que variam do negativo 10 ^ 255 + 1 toopositive 10 ^-255 1 |
| Duplo |Representa um número de ponto flutuante com precisão de 15 dígitos que pode representar valores de intervalo aproximado de ± 2, 23E -308 a ± 1, 79E +308. **Use Decimal devido a problema de exportação tooExel** |
| Single |Representa um número de ponto flutuante com precisão de 7 dígitos que pode representar valores de intervalo aproximado de ± 1,18E -38 a ± 3,40E +38. |
| Guid |Representa um valor de identificador exclusivo de 16 bytes (128 bits) |
| Int16 |Representa um valor inteiro assinado de 16 bits |
| Int32 |Representa um valor inteiro assinado de 32 bits |
| Int64 |Representa um valor inteiro assinado de 64 bits |
| Cadeia de caracteres |Representa dados de caracteres de comprimento fixo ou variável |

## <a name="see-also"></a>Consulte também
* Se você estiver interessado em entender Olá processo geral de mapeamento de OData e a finalidade, leia este artigo [dados serviço OData mapeamento](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definições, estruturas e instruções.
* Se você estiver interessado em examinar os exemplos, leia este artigo [dados serviço OData mapeamento exemplos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de exemplo e entender a sintaxe de código e o contexto.
* toohello tooreturn prescrita caminho para publicar um serviço de dados de toohello Azure Marketplace, leia este artigo [guia de publicação de serviço de dados](marketplace-publishing-data-service-creation.md).
