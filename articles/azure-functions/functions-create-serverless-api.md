---
title: "aaaCreate uma API serverless usando funções do Azure | Microsoft Docs"
description: "Como toocreate uma API serverless usando funções do Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Criar uma API sem servidor usando o Azure Functions

Neste tutorial você aprenderá como funções do Azure permite que você toobuild APIs altamente dimensionável. As funções do Azure vem com uma coleção de internos HTTP gatilhos e associações que torna fácil tooauthor um ponto de extremidade em uma variedade de linguagens, incluindo Node. js, c# e muito mais. Neste tutorial, você irá Personalizar ações específicas do gatilho toohandle um HTTP no seu projeto de API. Você também preparará a expansão de sua API integrando-a aos Proxies do Azure Functions e configurando APIs de simulação. Tudo isso é feito sobre o ambiente de computação sem servidor funções de hello, portanto você não tem tooworry sobre como dimensionar recursos - assim, você pode se concentrar na lógica da sua API.

## <a name="prerequisites"></a>Pré-requisitos 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

função resultante Olá será usada para o restante deste tutorial hello.

### <a name="sign-in-tooazure"></a>Entrar tooAzure

Olá Abrir portal do Azure. toodo isso, entrar muito[https://portal.azure.com](https://portal.azure.com) com sua conta do Azure.

## <a name="customize-your-http-function"></a>Personalizar sua função HTTP

Por padrão, a função disparado HTTP é tooaccept configurado qualquer método HTTP. Também é uma URL padrão do formulário de saudação `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Se você seguiu quickstart hello, em seguida, `<funcname>` parece ser algo como "HttpTriggerJS1". Nesta seção, você modificará a solicitações do hello função toorespond tooGET somente nos `/api/hello` rotear em vez disso. 

Navegue tooyour função hello portal do Azure. Selecione **integrar** em Olá barra de navegação esquerda.

![Personalizar uma função HTTP](./media/functions-create-serverless-api/customizing-http.png)

Use as configurações do disparador HTTP conforme especificado na tabela de saudação.

| Campo | Valor de exemplo | Descrição |
|---|---|---|
| Métodos HTTP selecionados | Métodos selecionados | Determina quais métodos HTTP podem ser usado tooinvoke esta função |
| Métodos HTTP selecionados | GET | Permite que somente selecionado toobe de métodos HTTP usadas tooinvoke esta função |
| Modelo de rota | /hello | Determina quais rota é tooinvoke usada nesta função |

Observe que você não incluiu Olá `/api` de prefixo de caminho no modelo de rota Olá, como isso é tratado por uma configuração global.

Clique em **Salvar**.

Você pode aprender mais sobre a personalização de funções HTTP em [Associações HTTP e webhook do Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Testar sua API

Em seguida, teste sua função toosee-lo funcionar com a nova superfície de API hello.

Navegue página de desenvolvimento toohello back clicando no nome da função de saudação na barra de navegação esquerda de saudação.

Clique em **obter URL de função** e copie a URL de saudação. Você verá que ele usa Olá `/api/hello` rotear agora.

Copie a URL de saudação em uma nova guia do navegador ou o cliente REST preferencial. Navegadores usarão GET por padrão.

Executar função hello e confirme se ele está funcionando. Parâmetro de "nome" hello tooprovide talvez seja necessário como um código de início rápido da saudação consulta cadeia de caracteres toosatisfy.

Você também pode tentar chamar o ponto de extremidade de saudação com outro tooconfirm de método HTTP que a função hello não é executada. Para isso, você precisará toouse um cliente REST, como rotação, carteiro ou o Fiddler.

## <a name="proxies-overview"></a>Visão geral dos proxies

Na próxima seção, Olá, você será superficial sua API por meio de um proxy. Proxies de funções do Azure é um recurso de visualização que permite que você tooforward solicitações tooother recursos. Definir um ponto de extremidade HTTP como com o gatilho HTTP, mas em vez de escrever código tooexecute quando é chamado de ponto de extremidade, você fornece uma implementação de remoto tooa URL. Isso permite que você toocompose API várias fontes em uma única superfície de API que é fácil para os clientes tooconsume. Isso é particularmente útil se você quiser toobuild sua API como microservices.

Um proxy pode apontar o recurso de tooany HTTP, como:
- Funções do Azure 
- Aplicativos de API no [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- Contêineres de docker no [Serviço de Aplicativo no Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)
- Qualquer outra API hospedada

toolearn mais sobre proxies, consulte [trabalhando com Proxies de funções do Azure (visualização)].

## <a name="create-your-first-proxy"></a>Criar seu primeiro proxy

Nesta seção, você criará um novo proxy que serve como um front-end tooyour API geral. 

### <a name="setting-up-hello-frontend-environment"></a>Configurando o ambiente de front-end Olá

Repita as etapas de saudação muito[criar um aplicativo de função](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate um novo aplicativo de função na qual você irá criar o proxy. Esse novo aplicativo servirá como front-end Olá para nossa API e Olá função aplicativo que você estava editando anteriormente servirá como um back-end.

Navegue tooyour novo aplicativo de front-end função no portal de saudação.

Escolha a opção **Configurações**. Em seguida, alternar **habilitar Proxies de funções do Azure (visualização)** muito "On".

Selecione **Configurações de Plataforma** e escolha **Configurações de Aplicativo**.

Role para baixo demais**configurações do aplicativo** e criar uma nova configuração com a chave "HELLO_HOST". Definir seu host toohello de valor do seu aplicativo de função de back-end, tais como `<YourApp>.azurewebsites.net`. Isso faz parte da URL de saudação que você copiou anteriormente ao testar sua função HTTP. Você vai fazer referência a essa configuração na configuração de hello mais tarde.

> [!NOTE] 
> Configurações do aplicativo são recomendadas para tooprevent de configuração de host Olá uma dependência de ambiente embutida para proxy hello. Usando as configurações de aplicativo significa que você pode mover a configuração de proxy de saudação entre ambientes e configurações de aplicativo específico do ambiente hello serão aplicadas.

Clique em **Salvar**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Criando um proxy no front-end Olá

Navegue de aplicativo de função de front-end tooyour Voltar no portal de saudação.

Na navegação do lado esquerdo hello, clique em Olá sinal de mais próximo '+' muito "Proxies (visualização)".

![Criação de um proxy](./media/functions-create-serverless-api/creating-proxy.png)

Use as configurações de proxy conforme especificado na tabela de saudação.

| Campo | Valor de exemplo | Descrição |
|---|---|---|
| Nome | HelloProxy | Um nome amigável usado apenas para gerenciamento |
| Modelo de rota | /api/hello | Determina quais rota é usada tooinvoke esse proxy |
| URL do back-end | https://%HELLO_HOST%/api/hello | Especifica a solicitação de Olá Olá ponto de extremidade toowhich deve ser delegada |

Observe que os Proxies não fornecer Olá `/api` prefixo de caminho base e este deve ser incluído no modelo de rota hello.

Olá `%HELLO_HOST%` sintaxe fará referência a configuração do aplicativo hello criado anteriormente. Olá resolvido que URL de ponto de função original tooyour.

Clique em **Criar**.

Você pode testar seu novo proxy copiando Olá URL do Proxy e testá-lo no navegador de saudação ou com o cliente HTTP favorito.

## <a name="create-a-mock-api"></a>Criar uma API de simulação

Em seguida, você usará um proxy toocreate uma API de simulação para sua solução. Isso permite o desenvolvimento de cliente tooprogress, sem a necessidade de back-end de saudação totalmente implementado. Mais tarde no desenvolvimento, você pode criar um novo aplicativo de função que dá suporte a essa lógica e redirecionar seu tooit de proxy.

toocreate isso simular API, vamos criar um novo proxy, desta vez usando Olá [Editor de aplicativo de serviço](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget iniciado, navegue tooyour função aplicativo no portal de saudação. Selecione **Recursos da plataforma** e localize o **Editor do Serviço de Aplicativo**. Isso permite abrir Olá Editor de aplicativo de serviço em uma nova guia.

Selecione `proxies.json` na barra de navegação esquerda de saudação. Este é o arquivo de saudação que armazena a configuração de Olá para todos os proxies. Se você usar uma saudação [métodos de implantação de funções](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), este é o arquivo hello serão mantidas no controle de origem. toolearn mais sobre esse arquivo, consulte [configuração avançada de Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Se você acompanhou até aqui até agora, seu proxies.json deve ter a aparência Olá a seguir:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Em seguida, você adicionará sua API de simulação. Substitua o arquivo proxies.json com os seguintes hello:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

Isso adiciona um novo proxy de, "GetUserByName", sem a propriedade de backendUri hello. Em vez de chamar outro recurso, ele modifica a resposta de padrão de saudação do Proxies usando uma substituição de resposta. Substituições de solicitação e resposta também podem ser usadas em conjunto com uma URL de back-end. Isso é particularmente útil quando o proxy tooa sistema herdado, em que talvez seja necessário toomodify cabeçalhos, parâmetros de consulta, etc. toolearn mais informações sobre substituições de solicitação e resposta, consulte [modificando solicitações e respostas no Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Testar sua API fictícia chamada hello `/api/users/{username}` ponto de extremidade usando um navegador ou o cliente REST favorito. Ser tooreplace se _{username}_ com um valor de cadeia de caracteres que representa um nome de usuário.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como toobuild e personalizar uma API em funções do Azure. Você também aprendeu como toobring várias APIs, incluindo mocks, juntos como uma superfície de API unificada. Você pode usar esses toobuild técnicas out APIs de qualquer complexidade, todos os durante a execução em Olá serverless computação modelo fornecido pelas funções do Azure.

Olá referências a seguir podem ser úteis à medida que desenvolve sua API adicional:

- [Associações HTTP e de webhook do Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [trabalhando com Proxies de funções do Azure (visualização)]
- [Documentar uma API do Azure Functions (visualização)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabalhando com Proxies de funções do Azure (visualização)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
