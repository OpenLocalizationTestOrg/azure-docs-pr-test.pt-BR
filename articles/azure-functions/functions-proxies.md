---
title: "aaaWork com proxies em funções do Azure | Microsoft Docs"
description: "Visão geral de como toouse Proxies de funções do Azure"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a>Trabalhar com proxies do Azure Functions (visualização)

> [!NOTE] 
> Proxies do Azure Functions está atualmente em visualização. É gratuito enquanto na visualização, mas as funções padrão cobrança aplica tooproxy execuções. Para saber mais, confira [Preços do Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

Este artigo explica como tooconfigure e trabalhar com Proxies de funções do Azure. Com esse recurso, você pode especificar os pontos de extremidade em seu aplicativo de funções que são implementados por outro recurso. Você pode usar esses toobreak proxies uma API grande em vários aplicativos de função (como em uma arquitetura de microsserviço), enquanto ainda apresentar uma superfície de API simples para clientes.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <a name="enable"></a>Habilitar proxies do Azure Functions

Os proxies não estão habilitados por padrão. Você pode criar proxies enquanto Olá recurso está desabilitado, mas elas não serão executadas. tooenable proxies, Olá a seguir:

1. Olá abrir [portal do Azure], e em seguida, acesse o aplicativo de função tooyour.
2. Selecione **Configurações do aplicativo de funções**.
3. Opção **habilitar Proxies de funções do Azure (visualização)** muito**em**.

Você também pode retornar aqui tooupdate Olá proxy runtime conforme novos recursos se tornam disponíveis.


## <a name="create"></a>Criar um proxy

Esta seção mostra como toocreate um proxy no hello portal de funções.

1. Olá abrir [portal do Azure], e em seguida, acesse o aplicativo de função tooyour.
2. No painel esquerdo do hello, selecione **novo proxy**.
3. Forneça um nome para seu proxy.
4. Configurar o ponto de extremidade de saudação que é exposto no aplicativo função especificando Olá **modelo de rota** e **métodos HTTP**. Esses parâmetros se comportam de acordo regras toohello para [HTTP gatilhos].
5. Saudação de conjunto **URL de back-end** tooanother de ponto de extremidade. Esse ponto de extremidade pode ser uma função em outro aplicativo de funções, ou pode ser qualquer outra API. Olá valor não precisa toobe estático, e ele pode fazer referência [configurações do aplicativo] e [parâmetros da solicitação de cliente original Olá].
6. Clique em **Criar**.

Seu proxy agora existe como um novo ponto de extremidade em seu aplicativo de funções. Da perspectiva do cliente, é equivalente tooan HttpTrigger em funções do Azure. Você pode testar seu novo proxy copiando Olá URL do Proxy e testá-lo com seu cliente HTTP favorito.

## <a name="modify-requests-responses"></a>Modificar solicitações e respostas

Com Proxies de funções do Azure, você pode modificar solicitações tooand respostas de back-end hello. Essas transformações podem usar variáveis, conforme definido em [Usar variáveis].

### <a name="modify-backend-request"></a>Modificar a solicitação de back-end Olá

Por padrão, a solicitação de back-end de saudação é inicializado como uma cópia da solicitação original hello. Além disso toosetting Olá back-end URL, você pode fazer alterações toohello HTTP método, cabeçalhos e parâmetros de cadeia de caracteres de consulta. Olá valores modificados podem fazer referência a [configurações do aplicativo] e [parâmetros da solicitação de cliente original Olá].

Atualmente, não há experiência no portal para modificar as solicitações de back-end. toolearn como tooapply essa capacidade de proxies.json, consulte [definir um objeto requestOverrides].

### <a name="modify-response"></a>Modificar a resposta de saudação

Por padrão, resposta de cliente Olá é inicializada como uma cópia da resposta de back-end de saudação. Você pode fazer o código de status da resposta de toohello alterações, frase de motivo, cabeçalhos e corpo. Olá valores modificados podem fazer referência a [configurações do aplicativo], [parâmetros da solicitação de cliente original Olá], e [parâmetros de resposta de back-end Olá].

Atualmente, não há experiência no portal para modificar as respostas. toolearn como tooapply essa capacidade de proxies.json, consulte [definir um objeto responseOverrides].

## <a name="using-variables"></a>Usar variáveis

configuração de saudação para um proxy não precisa toobe estático. Você pode condição ele toouse variáveis de solicitação original hello, resposta de back-end de saudação ou as configurações do aplicativo.

### <a name="request-parameters"></a>Parâmetros de solicitação de referência

Você pode usar parâmetros de solicitação como entradas toohello propriedade de URL de back-end ou como parte da modificação de solicitações e respostas. Alguns parâmetros podem ser vinculados de modelo de rota de saudação que é especificado na configuração de proxy base hello e outras pessoas podem vir de propriedades de solicitação de entrada hello.

#### <a name="route-template-parameters"></a>Parâmetros de modelo de rota
Parâmetros que são usados no modelo de rota Olá estão disponível toobe referenciada por nome. nomes de parâmetro Hello são colocados entre chaves ({}).

Por exemplo, se um proxy tem um modelo de rota, como `/pets/{petId}`, Olá URL de back-end pode incluir o valor de saudação do `{petId}`, como em `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Se o modelo de rota Olá termina em um caractere curinga, como `/api/{*restOfPath}`, Olá valor `{restOfPath}` é uma representação de cadeia de caracteres de saudação restantes segmentos de caminho da solicitação de entrada hello.

#### <a name="additional-request-parameters"></a>Parâmetros de solicitação adicionais
Além do toohello parâmetros de modelo de rota, Olá valores a seguir pode ser usado em valores de configuração:

* **{Request}** : Olá o método HTTP usado na solicitação original hello.
* **{: Request. Headers. \<HeaderName\>}**: um cabeçalho que pode ser lido da solicitação original hello. Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooread. Se o cabeçalho de saudação não está incluído na solicitação Olá, o valor de Olá será a cadeia de caracteres vazia hello.
* **{Request. QueryString. \<ParameterName\>}**: um parâmetro de cadeia de caracteres de consulta que possa ser lido da solicitação original hello. Substituir  *\<ParameterName\>*  com o nome de saudação do parâmetro hello que você deseja tooread. Se o parâmetro hello não está incluído na solicitação Olá, o valor de saudação será a cadeia de caracteres vazia hello.

### <a name="response-parameters"></a>Parâmetros de resposta de back-end de referência

Parâmetros de resposta podem ser usados como parte de modificar Olá resposta toohello cliente. Olá valores a seguir pode ser usado em valores de configuração:

* **{backend.response.statusCode}** : Olá código de status HTTP retornado na resposta de back-end de saudação.
* **{backend.response.statusReason}** : frase de motivo Olá HTTP que é retornado na resposta de back-end de saudação.
* **{backend.response.headers. \<HeaderName\>}**: um cabeçalho que pode ser lido da resposta de back-end de saudação. Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação você deseja tooread. Se o cabeçalho de saudação não está incluído na solicitação Olá, o valor de Olá será a cadeia de caracteres vazia hello.

### <a name="use-appsettings"></a>Configurações do aplicativo de referência

Você também pode referenciar [configurações de aplicativo definidas para o aplicativo de função hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) envolvendo o nome da configuração Olá sinais de porcentagem (%).

Por exemplo, uma URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* teria "% ORDER_PROCESSING_HOST %" substituído pelo valor de saudação da configuração de ORDER_PROCESSING_HOST hello.

> [!TIP] 
> Usar configurações do aplicativo para hosts de back-end quando você tem várias implantações ou ambientes de teste. Dessa forma, você pode garantir que estamos falando sempre toohello volta terminar para esse ambiente.

## <a name="advanced-configuration"></a>Configuração avançada

proxies de saudação que você configura são armazenados em um arquivo proxies.json, que está localizado na raiz de saudação de um diretório de aplicativo de função. Você pode editar esse arquivo manualmente e implantá-lo como parte do seu aplicativo quando você usar qualquer Olá [métodos de implantação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que ofereça suporte a funções. saudação de recurso deve ser [habilitado](#enable) para toobe do arquivo hello processado. 

> [!TIP] 
> Se você não configurou um dos métodos de implantação Olá, você também pode trabalhar com arquivos de proxies.json Olá no portal de saudação. Aplicativo de função tooyour vá, selecione **recursos de plataforma**e, em seguida, selecione **Editor de aplicativo de serviço**. Fazendo isso, você pode exibir estrutura de todo o arquivo de saudação do seu aplicativo de função e, em seguida, fazer alterações.

Proxies.json é definido por um objeto de proxies, composto de proxies nomeados e suas definições. Opcionalmente, você pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para o preenchimento do código, caso seu editor dê suporte a isso. Um exemplo de arquivo pode parecer Olá a seguir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

Cada proxy tem um nome amigável, como *proxy1* em Olá anterior de exemplo. objeto de definição de proxy correspondente Olá é definido pela Olá propriedades a seguir:

* **matchCondition**: necessário – um objeto que define as solicitações de saudação que disparam execução Olá desse proxy. Ele contém duas propriedades compartilhadas com [HTTP gatilhos]:
    * _métodos_: uma matriz de métodos de saudação HTTP que Olá proxy responde. Se não for especificado, o proxy de saudação responde tooall métodos HTTP na rota de saudação.
    * _rota_: exigido-- define o modelo de rota hello, controlar qual solicitação URLs seu proxy responde. Ao contrário de disparadores HTTP, não há nenhum valor padrão.
* **backendUri**: Olá URL de solicitação de Olá Olá recursos de back-end toowhich deve usar o proxy. Esse valor pode referenciar parâmetros e configurações do aplicativo da solicitação de cliente original hello. Se esta propriedade não for incluída, o Azure Functions responderá com um HTTP 200 OK.
* **requestOverrides**: um objeto que define a solicitação de back-end toohello transformações. Confira [definir um objeto requestOverrides].
* **responseOverrides**: um objeto que define a resposta de cliente toohello transformações. Confira [definir um objeto responseOverrides].

> [!NOTE] 
> propriedade de rota Olá Proxies de funções do Azure não aceita a propriedade de routePrefix Olá Olá funções da configuração do host. Se você quiser tooinclude um prefixo, como /api, ela deve ser incluída na propriedade de rota hello.

### <a name="requestOverrides"></a>Definir um objeto requestOverrides

objeto de requestOverrides de saudação define as alterações feitas a solicitação toohello quando recursos de back-end de saudação é chamado. objeto de saudação é definido pela Olá propriedades a seguir:

* **backend.Request.Method**: Olá método HTTP que foi usado o back-end de saudação toocall.
* **backend.Request.QueryString. \<ParameterName\>**: um parâmetro de cadeia de caracteres de consulta que pode ser definido para Olá chamada toohello back-end. Substituir  *\<ParameterName\>*  com o nome de saudação do parâmetro hello que você deseja tooset. Se a cadeia de caracteres vazia Olá for fornecida, o parâmetro hello não está incluído na solicitação de back-end de saudação.
* **backend.Request.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para Olá chamada toohello back-end. Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooset. Se você fornecer a cadeia de caracteres vazia hello, cabeçalho de saudação não está incluído na solicitação de back-end de saudação.

Valores podem referenciar parâmetros e configurações do aplicativo da solicitação de cliente original hello.

Um exemplo de configuração pode parecer com hello seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <a name="responseOverrides"></a>Definir um objeto responseOverrides

objeto de requestOverrides Olá define as alterações feitas resposta toohello que passou toohello back cliente. objeto de saudação é definido pela Olá propriedades a seguir:

* **response.statusCode**: Olá HTTP toobe de código de status retornado toohello cliente.
* **response.statusReason**: toobe de frase de motivo Olá HTTP retornado toohello cliente.
* **Response.body**: representação de cadeia de caracteres de saudação do hello corpo toobe retornado toohello cliente.
* **Response.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para o cliente do hello resposta toohello. Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooset. Se você fornecer a cadeia de caracteres vazia hello, cabeçalho de saudação não está incluído na resposta de saudação.

Valores podem referenciar as configurações do aplicativo, parâmetros de solicitação de cliente original hello e parâmetros da resposta de back-end de saudação.

Um exemplo de configuração pode parecer com hello seguinte:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> Neste exemplo, o corpo de hello está sendo definido diretamente, portanto não `backendUri` propriedade é necessária. exemplo Hello mostra como você pode usar Proxies de funções do Azure para APIs de simulação.

[portal do Azure]: https://portal.azure.com
[HTTP gatilhos]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir um objeto requestOverrides]: #requestOverrides
[definir um objeto responseOverrides]: #responseOverrides
[configurações do aplicativo]: #use-appsettings
[Usar variáveis]: #using-variables
[parâmetros da solicitação de cliente original Olá]: #request-parameters
[parâmetros de resposta de back-end Olá]: #response-parameters
