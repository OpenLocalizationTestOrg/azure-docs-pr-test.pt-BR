---
title: aaaCustom cache no gerenciamento de API do Azure
description: Saiba como toocache itens por chave no gerenciamento de API do Azure
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Cache personalizado no Gerenciamento de API do Azure
Serviço de gerenciamento de API do Azure tem suporte interno para [cache de resposta HTTP](api-management-howto-cache.md) usando a URL de recurso hello como chave de saudação. Olá chave pode ser modificada por cabeçalhos de solicitação usando Olá `vary-by` propriedades. Isso é útil para armazenar em cache respostas HTTP inteiras (também conhecido como representações), mas às vezes é útil toojust cache uma parte de uma representação. Olá novo [valor de pesquisa de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [valor do repositório de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) políticas fornecem a capacidade de saudação toostore e recuperar partes arbitrárias de dados do grupo de definições de política. Essa capacidade também adiciona valor toohello introduzida anteriormente [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) política porque você agora pode armazenar em cache respostas de serviços externos.

## <a name="architecture"></a>Arquitetura
Serviço de gerenciamento de API usa um cache de dados compartilhado por locatário para que, ao dimensionar unidades toomultiple você ainda terá acesso toohello mesmo dados armazenados em cache. No entanto, ao trabalhar com uma implantação de várias regiões são independentes caches dentro de cada uma das regiões de saudação. Vencimento toothis, é importante toonot tratar cache hello como um repositório de dados, onde é a única fonte Olá de alguma informação. Se você fez e posteriormente decidir tootake vantagem da implantação de várias regiões hello, os clientes com usuários que viajam poderão perder acesso toothat armazenado em cache dados.

## <a name="fragment-caching"></a>Cache de fragmento
Há alguns casos onde as respostas que está sendo retornadas contêm uma parte dos dados que são caro toodetermine e ainda permanecem atualizada por um período de tempo razoável. Por exemplo, considere um serviço criado por uma companhia aérea que fornece informações relacionadas a reservas de voo, status de voo, etc. Se o usuário Olá é membro do programa de pontos de companhias aéreas hello, eles também teriam informações sobre o status atual de tootheir e quilometragem acumulados. Essas informações relacionadas ao usuário podem ser armazenadas em um sistema diferente, mas pode ser desejável tooinclude em respostas retornada sobre o status de voo e reservas. Isso pode ser feito usando um processo chamado cache fragmentado. Olá representação primária pode ser retornada do servidor de origem hello usando algum tipo de token tooindicate onde informações relacionadas ao usuário de saudação são toobe inserido. 

Considere Olá seguindo a resposta JSON de uma API de back-end.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

E o recursos secundário em `/userprofile/{userid}` , semelhante.

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

Ordem toodetermine Olá usuário apropriado informações tooinclude, precisamos tooidentify que o usuário final de saudação. Esse mecanismo é dependente da implementação. Por exemplo, estou usando Olá `Subject` de declaração de um `JWT` token. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Armazenamos o valor `enduserid` em uma variável de contexto para uso posterior. Olá próxima etapa é toodetermine se uma solicitação anterior já recuperar informações de saudação do usuário e armazená-lo em cache hello. Para isso, usamos Olá `cache-lookup-value` política.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Se não houver nenhuma entrada no cache de saudação que corresponde o valor da chave toohello e não `userprofile` variável de contexto será criado. Precisamos verificar o sucesso de saudação da pesquisa hello usando Olá `choose` política de fluxo de controle.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Se hello `userprofile` variável de contexto não existir, então, será contínuo toohave toomake um HTTP solicitação tooretrieve-lo.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Usamos Olá `enduserid` recurso de perfil de usuário tooconstruct Olá URL toohello. Assim que tivermos resposta hello, podemos extrair texto Olá sem resposta hello e armazená-lo novamente em uma variável de contexto.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid tenhamos toomake essa solicitação HTTP novamente, ao mesmo usuário hello faz outra solicitação, que pode armazenar Olá perfil de usuário no cache de saudação.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Armazenamos valor Olá no cache de saudação usando Olá exata mesma chave que tentamos originalmente tooretrieve com. Olá duração, escolhemos o valor de saudação toostore deve ser baseada em frequência hello usuários como tolerante a falhas e alterações de informações são tooout de informações de data. 

É importante toorealize que recuperar do cache de saudação ainda é um fora do processo, a solicitação de rede e potencialmente ainda poderá adicionar dezenas de solicitação de toohello milissegundos. benefícios de saudação vir ao determinar informações de perfil de usuário Olá leva significativamente mais tempo do que o devido a consultas de banco de dados de toodo tooneeding ou agregar informações de vários back-ends.

Olá, etapa final do processo de saudação é Olá tooupdate retornada uma resposta com nosso informações de perfil do usuário.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Escolhi tooinclude Olá aspas como parte do token Olá para que, mesmo quando não ocorre Olá replace, resposta Olá era JSON ainda é válido. Isso foi principalmente toomake depuração mais fácil.

Depois que você pode combinar todas essas etapas juntas, o resultado de final de saudação é uma política que se parece com hello seguindo um.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Essa abordagem de cache é usada principalmente em sites da web onde o HTML é composto no lado do servidor de saudação para que ele pode ser renderizado como uma única página. No entanto, ele também pode ser útil para onde os clientes não é possível executar o cliente de APIs do lado do cache de HTTP ou é desejável não tooput essa responsabilidade no cliente de saudação.

Esse tipo de cache de fragmento também pode ser feito nos servidores de web de back-end hello usando um servidor de cache de Redis, no entanto, usar tooperform de serviço de gerenciamento de API Olá esse trabalho é útil quando fragmentos Olá armazenados em cache são provenientes de back-ends diferentes que Olá respostas primárias.

## <a name="transparent-versioning"></a>Controle de versão transparente
É uma prática comum para várias versões diferentes de implementação de um toobe de API com suporte a qualquer momento. Essa é talvez toosupport diferentes ambientes, como desenvolvimento, teste, produção, etc., ou pode ser toosupport de versões mais antigas de tempo de toogive Olá API para as versões de API consumidores toomigrate toonewer. 

Uma abordagem toohandling em vez de exigir saudação do cliente desenvolvedores toochange URLs de `/v1/customers` muito`/v2/customers` é toostore nos dados de perfil do consumidor Olá qual versão de API do hello eles atualmente deseja toouse e chamar hello URL de back-end. Em ordem toodetermine Olá correto de back-end URL toocall para um determinado cliente, é necessário tooquery alguns dados de configuração. Armazenando em cache esses dados de configuração, é possível minimizar penalidade de desempenho de saudação de fazer essa pesquisa.

Olá primeira etapa é o identificador de saudação toodetermine usado versão desejada do tooconfigure hello. Neste exemplo, escolhi chave de assinatura de produto tooassociate Olá versão toohello. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

Em seguida, fazemos uma toosee de pesquisa do cache se já recuperamos versão de cliente desejado de saudação.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Em seguida, marcamos toosee se não foi encontrada-la no cache de saudação.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Se não, nós a recuperamos.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Extrai o texto do corpo de resposta de saudação da resposta de saudação.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Armazená-lo novamente no cache de saudação para uso futuro.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

E finalmente Olá back-end URL tooselect Olá versão da atualização do serviço de saudação desejado pelo cliente hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Olá completamente política é da seguinte maneira.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

Ativando o controle de tootransparently consumidores de API qual versão de back-end está sendo acessado por clientes sem ter que clientes tooupdate e a reimplantação é uma solução elegante que resolve muitos problemas de controle de versão de API.

## <a name="tenant-isolation"></a>Isolamento de locatário
Em implantações maiores, de vários locatários, algumas empresas criar grupos separados de locatários em implantações distintas do hardware de back-end. Isso minimiza o número de saudação de clientes que são afetados por um problema de hardware em Olá back-end. Ele também permite que o novo toobe de versões de software distribuído em estágios. O ideal é essa arquitetura de back-end deve ser consumidores tooAPI transparente. Isso pode ser obtido de um controle de versão de tootransparent de maneira semelhante, porque ela é baseada no hello mesma técnica de manipulação de URL de back-end hello usando o estado de configuração por chave de API.  

Em vez de retornar uma versão preferencial do hello API para cada chave de assinatura, você retornará um identificador que está relacionada a um grupo de hardware do locatário toohello atribuído. Esse identificador pode ser usado tooconstruct Olá back-end apropriado URL.

## <a name="summary"></a>Resumo
saudação de toouse Olá liberdade cache de gerenciamento de API do Azure para armazenar qualquer tipo de dados permite que os dados de tooconfiguration acesso eficiente que podem afetar a maneira de saudação que uma solicitação de entrada é processada. Ele também pode ser usado toostore os fragmentos de dados que podem aumentar respostas, retornadas de uma API de back-end.

## <a name="next-steps"></a>Próximas etapas
. Forneça seus comentários no hello threads do Disqus para este tópico se há outros cenários que essas políticas tem habilitado para você, ou se há cenários você gostaria que tooachieve, mas não se sinta são possíveis no momento.

