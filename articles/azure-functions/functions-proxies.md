---
title: Trabalhar com proxies no Azure Functions | Microsoft Docs
description: "Visão geral de como usar Proxies do Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: cfowler
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: alkarche
ms.openlocfilehash: dd022b189783f2d8c6209a6cd656704ff144bfd6
ms.sourcegitcommit: 4256ebfe683b08fedd1a63937328931a5d35b157
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2017
---
# <a name="work-with-azure-functions-proxies"></a>Trabalhe com Proxies do Azure Functions

Este artigo explica como configurar e trabalhar com proxies do Azure Functions. Com esse recurso, você pode especificar os pontos de extremidade em seu aplicativo de funções que são implementados por outro recurso. Você pode usar esses proxies para dividir uma API grande em vários aplicativos de função (como uma arquitetura de microsserviços), enquanto ainda apresenta uma única superfície de API para clientes.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE] 
> A cobrança do Standard Functions se aplica para execuções de proxy. Para saber mais, confira [Preços do Azure Functions](https://azure.microsoft.com/pricing/details/functions/).

## <a name="create"></a>Criar um proxy

Esta seção mostra como criar um proxy no portal do Functions.

1. Abra o [Portal do Azure] e navegue até seu aplicativo de funções.
2. No painel esquerdo, selecione **Novo proxy**.
3. Forneça um nome para seu proxy.
4. Configurar o ponto de extremidade exposto no aplicativo de função especificando o **modelo de rota** e **Métodos HTTP**. Esses parâmetros se comportam de acordo com as regras de [gatilhos HTTP].
5. Defina a **URL de back-end** para outro ponto de extremidade. Esse ponto de extremidade pode ser uma função em outro aplicativo de funções, ou pode ser qualquer outra API. O valor não precisa ser estático e pode fazer referência as [configurações do aplicativo] e os [parâmetros da solicitação original do cliente].
6. Clique em **Criar**.

Seu proxy agora existe como um novo ponto de extremidade em seu aplicativo de funções. Da perspectiva do cliente, é equivalente a um HttpTrigger no Azure Functions. Você pode testar seu novo proxy copiando a URL do Proxy e testá-lo com seu cliente HTTP favorito.

## <a name="modify-requests-responses"></a>Modificar solicitações e respostas

Com Proxies do Azure Functions, você pode modificar solicitações e respostas do back-end. Essas transformações podem usar variáveis, conforme definido em [Usar variáveis].

### <a name="modify-backend-request"></a>Modificar a solicitação de back-end

Por padrão, a solicitação de back-end é inicializada como uma cópia da solicitação original. Além de definir a URL de back-end, é possível fazer alterações no método HTTP, cabeçalhos e parâmetros de cadeia de consulta. Os valores modificados podem referenciar as [configurações do aplicativo] e os [parâmetros da solicitação original do cliente].

Atualmente, não há experiência no portal para modificar as solicitações de back-end. Para saber como aplicar essa capacidade a partir de *proxies.json*, confira [Definir um objeto requestOverrides].

### <a name="modify-response"></a>Modificar a resposta

Por padrão, a resposta do cliente é inicializada como uma cópia da resposta de back-end. Você pode fazer alterações no código de status, na frase de motivo, nos cabeçalhos e no corpo da resposta. Os valores modificados podem referenciar as [configurações do aplicativo], os [parâmetros da solicitação original do cliente] e os [parâmetros da resposta de back-end].

Atualmente, não há experiência no portal para modificar as respostas. Para saber como aplicar essa capacidade do *proxies.json*, confira [Definir um objeto responseOverrides].

## <a name="using-variables"></a>Usar variáveis

A configuração de um proxy não precisa ser estática. Você pode condicioná-la para usar variáveis da solicitação do cliente original, da resposta de back-end ou das configurações do aplicativo.

### <a name="request-parameters"></a>Parâmetros de solicitação de referência

Use os parâmetros de solicitação como entradas para a propriedade de URL de back-end ou como parte da modificação de solicitações e respostas. Alguns parâmetros podem ser limitados ao modelo de rota especificado na configuração do proxy base, enquanto outros são obtidos de propriedades da solicitação de entrada.

#### <a name="route-template-parameters"></a>Parâmetros de modelo de rota
Os parâmetros usados no modelo de rota estão disponíveis para serem referenciados pelo nome. Os nomes de parâmetro são colocados entre chaves ({}).

Por exemplo, se um proxy tem um modelo de rota como `/pets/{petId}`, a URL do back-end pode incluir o valor de `{petId}`, como em `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`. Se o modelo de rota termina em um caractere curinga, como `/api/{*restOfPath}`, o valor `{restOfPath}` será uma representação de cadeia de caracteres dos segmentos de caminho restantes da solicitação de entrada.

#### <a name="additional-request-parameters"></a>Parâmetros de solicitação adicionais
Além dos parâmetros do modelo de rota, os seguintes valores podem ser usados em valores de configuração:

* **{request.method}**: o método HTTP usado na solicitação original.
* **{request.headers.\<HeaderName\>}**: um cabeçalho que pode ser lido por meio da solicitação original. Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja ler. Se o cabeçalho não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.
* **{request.querystring.\<ParameterName\>}**: um parâmetro de cadeia de consulta que pode ser lido por meio da solicitação original. Substitua *\<ParameterName\>* pelo nome do parâmetro que você deseja ler. Se o parâmetro não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.

### <a name="response-parameters"></a>Parâmetros de resposta de back-end de referência

Parâmetros de resposta podem ser usados como parte da modificação da resposta ao cliente. Os seguintes valores podem ser usados em valores de configuração:

* **{backend.response.statusCode}**: o código de status HTTP retornado na resposta de back-end.
* **{backend.response.statusReason}**: a frase de motivo HTTP retornada na resposta de back-end.
* **{backend.response.headers.\<HeaderName\>}**: um cabeçalho que pode ser lido por meio da resposta de back-end. Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja ler. Se o cabeçalho não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.

### <a name="use-appsettings"></a>Configurações do aplicativo de referência

Você também referenciar as [configurações do aplicativo definidas para o aplicativo de funções](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) envolvendo o nome da configuração entre sinais de percentual (%).

Por exemplo, em uma URL de back-end *https://%ORDER_PROCESSING_HOST%/api/orders*, "% ORDER_PROCESSING_HOST %" será substituído pelo valor da configuração ORDER_PROCESSING_HOST.

> [!TIP] 
> Usar configurações do aplicativo para hosts de back-end quando você tem várias implantações ou ambientes de teste. Dessa forma, você pode garantir que está sempre se comunicando com o back-end correto para aquele ambiente.

## <a name="advanced-configuration"></a>Configuração avançada

Os proxies que você configura são armazenados em um arquivo *proxies.json*, que está localizado na raiz de um diretório de aplicativo de função. Você pode editar esse arquivo manualmente e implantá-lo como parte do seu aplicativo ao usar qualquer um dos [métodos de implantação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que ofereça suporte a funções. O recurso de Proxies do Azure Functions deve ser [habilitado](#enable) para o arquivo ser processado. 

> [!TIP] 
> Se você não configurou um dos métodos de implantação, também poderá trabalhar com o arquivo *proxies.json* no portal. Vá até o aplicativo de funções e selecione **Recursos da plataforma** e,depois, selecione **Editor do Serviço de Aplicativo**. Isso permitirá que você veja toda a estrutura de arquivo do aplicativo de funções e faça alterações.

*Proxies.json* é definido por um objeto de proxies, composto de proxies nomeados e suas definições. Opcionalmente, você pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para o preenchimento do código, caso seu editor dê suporte a isso. Um arquivo de exemplo pode parecer com o seguinte:

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

Cada proxy tem um nome amigável, como *proxy1*, no exemplo acima. O objeto de definição de proxy correspondente é definido pelas seguintes propriedades:

* **matchCondition**: obrigatório - um objeto que define as solicitações que disparam a execução desse proxy. Ele contém duas propriedades compartilhadas com [gatilhos HTTP]:
    * _métodos_: uma matriz dos métodos HTTP aos quais o proxy responde. Se não for especificado, o proxy responderá a todos os métodos HTTP na rota.
    * _route_: obrigatório - define o modelo da rota, controlando para quais URLs de solicitação seu proxy responde. Ao contrário de disparadores HTTP, não há nenhum valor padrão.
* **backendUri**: a URL do recurso de back-end ao qual a solicitação deve ser transmitida por proxy. Esse valor pode referenciar as configurações do aplicativo e os parâmetros da solicitação original do cliente. Se esta propriedade não for incluída, o Azure Functions responderá com um HTTP 200 OK.
* **requestOverrides**: um objeto que define as transformações para a solicitação de back-end. Confira [Definir um objeto requestOverrides].
* **requestOverrides**: um objeto que define as transformações para a resposta do cliente. Confira [Definir um objeto responseOverrides].

> [!NOTE] 
> A propriedade de *rota* dos proxies de funções do Azure não honra a propriedade *routePrefix* da configuração de host do Aplicativo de funções. Se você quiser incluir um prefixo, como `/api`, ele deve ser incluído na propriedade de *rota*.

### <a name="requestOverrides"></a>Definir um objeto requestOverrides

O objeto requestOverrides define as alterações feitas à solicitação quando o recurso de back-end é chamado. O objeto é definido pelas seguintes propriedades:

* **backend.request.method**: O método HTTP que é usado para chamar o back-end.
* **backend.request.querystring.\<ParameterName\>**: Um parâmetro de cadeia de caracteres de consulta que pode ser definido para a chamada ao back-end. Substitua *\<ParameterName\>* pelo nome do parâmetro que você deseja definir. Se a cadeia de caracteres vazia for fornecida, o parâmetro não será incluído na solicitação de back-end.
* **backend.Request.headers.\<HeaderName\>**: Um cabeçalho que pode ser definido para a chamada ao back-end. Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja definir. Se você fornecer a cadeia de caracteres vazia, o cabeçalho não será incluído na solicitação de back-end.

Os valores podem referenciar as configurações do aplicativo e os parâmetros da solicitação original do cliente.

Uma configuração de exemplo pode ser parecida com a seguinte:

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

O objeto requestOverrides define as alterações feitas à resposta passada novamente ao cliente. O objeto é definido pelas seguintes propriedades:

* **response.statusCode**: o código de status HTTP a ser retornado ao cliente.
* **response.statusReason**: a frase de motivo do HTTP a ser retornada ao cliente.
* **response.body**: a representação de cadeia de caracteres do corpo a ser retornada ao cliente.
* **response.headers.\<HeaderName\>**: um cabeçalho que pode ser definido para a resposta ao cliente. Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja definir. Se você fornecer a cadeia de caracteres vazia, o cabeçalho não será incluído na resposta.

Os valores podem referenciar as configurações do aplicativo, os parâmetros da solicitação original do cliente e os parâmetros da resposta de back-end.

Uma configuração de exemplo pode ser parecida com a seguinte:

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
> Neste exemplo, o corpo da resposta é definido diretamente e, portanto, nenhuma propriedade `backendUri` é necessária. O exemplo mostra como você pode usar os Proxies do Azure Functions para simular APIs.

## <a name="enable"></a>Habilitar proxies do Azure Functions

Os proxies agora estão habilitados por padrão! Se você estiver usando uma versão mais antiga da versão prévia de proxies e proxies desabilitados, você precisará habilitar manualmente os proxies uma vez para que eles sejam executados.

1. Abra o [Portal do Azure] e navegue até seu aplicativo de funções.
2. Selecione **Configurações do aplicativo de funções**.
3. Alterne **Habilitar Proxies do Azure Functions (visualização)** para **Ativado**.

Você também pode retornar aqui para atualizar o tempo de execução do proxy medida que novos recursos forem disponibilizados.

[Portal do Azure]: https://portal.azure.com
[gatilhos HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
[Definir um objeto requestOverrides]: #requestOverrides
[Definir um objeto responseOverrides]: #responseOverrides
[configurações do aplicativo]: #use-appsettings
[Usar variáveis]: #using-variables
[parâmetros da solicitação original do cliente]: #request-parameters
[parâmetros da resposta de back-end]: #response-parameters
