---
title: "metadados de aaaOpenAPI em funções do Azure | Microsoft Docs"
description: "Visão geral do suporte OpenAPI em Azure Functions"
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
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Suporte aos metadados de OpenAPI 2.0 no Azure Functions (versão prévia)
OpenAPI 2.0 (anteriormente conhecida como Swagger) suporte a metadados em funções do Azure é um recurso de visualização que você pode usar a definição de toowrite um 2.0 OpenAPI dentro de um aplicativo de função. Em seguida, você pode hospedar esse arquivo usando o aplicativo de função hello.

[Metadados OpenAPI](http://swagger.io/) permite que uma função que está hospedando uma API REST toobe consumidos por uma ampla variedade de outros softwares. Este software inclui a ofertas da Microsoft como o PowerApps e hello [recurso de aplicativos de API do serviço de aplicativo do Azure](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), ferramentas de desenvolvedor de terceiros, como [carteiro](https://www.getpostman.com/docs/importing_swagger), e [muitos pacotes mais](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>É recomendável começar com hello [tutorial de Introdução](./functions-api-definition-getting-started.md) e, em seguida, retornar toothis documento toolearn mais sobre recursos específicos.

## <a name="enable"></a>Habilitar o suporte à definição de OpenAPI
Você pode configurar todas as configurações de OpenAPI em Olá **de definição de API** página em seu aplicativo de função **recursos de plataforma**.

geração de saudação tooenable de uma definição de OpenAPI hospedada e uma definição de início rápido, defina **origem de definição de API** muito**função (visualização)**. **URL externa** permite que sua função toouse uma definição de OpenAPI tem hospedado em outro lugar.

## <a name="generate-definition"></a>Gerar um esqueleto de Swagger dos metadados de sua função
Um modelo pode ajudar você a começar a gravar sua primeira definição de OpenAPI. recurso de modelo de definição de saudação cria uma definição de OpenAPI esparsa usando todos os metadados de saudação no arquivo de function.json Olá para cada uma das suas funções de gatilho HTTP. Você precisará toofill em mais informações sobre a API de saudação [OpenAPI especificação](http://swagger.io/specification/), como modelos de solicitação e resposta.

Para obter instruções passo a passo, consulte Olá [tutorial de Introdução](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Modelos disponíveis

|Nome| Descrição |
|:-----|:-----|
|Definição gerada|Uma definição de OpenAPI com o número máximo de saudação de informações que podem ser inferidos de metadados existentes da função hello.|

### <a name="quickstart-details"></a>Metadados incluídos na definição de saudação gerada

Olá representa da tabela a seguir Olá configurações do portal do Azure e os dados correspondentes no function.json conforme é mapeada toohello gerado Swagger esqueleto.

|Swagger.json|Interface do usuário do portal|Function.json|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**Configurações do aplicativo de funções** > **Configurações do Serviço de Aplicativo** > **Visão geral** > **URL**|*Não presente*
|[Caminhos](http://swagger.io/specification/#paths-object-29)|**Integrar** > **Métodos HTTP selecionados**|Associações: rota
|[Item de caminho](http://swagger.io/specification/#path-item-object-32)|**Integrar** > **Modelos de rota**|Associações: métodos
|[Segurança](http://swagger.io/specification/#security-scheme-object-112)|**Chaves**|*Não presente*|
|operationID*|**Rota + Verbos permitidos**|Rota + verbos permitidos|

\*ID da operação Olá é necessária apenas para integração com o PowerApps e fluxo.
> [!NOTE]
> extensão de x-ms-resumo de saudação fornece um nome para exibição no fluxo de aplicativos lógicos e PowerApps.
>
> mais, consulte toolearn [personalizar sua definição de Swagger PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Use CI/CD tooset uma API definição

 Você deve habilitar API definição hospedagem no portal de saudação antes de habilitar toomodify de controle do código-fonte sua definição de API de controle de origem. Siga estas instruções:

1. Procurar muito**de definição de API (visualização)** em suas configurações de aplicativo de função.
  1. Definir **origem de definição de API** muito**função**.
  1. Clique em **modelo de definição de API gerar** e **salvar** toocreate uma definição de modelo para modificar posteriormente.
  1. Anote a URL e a chave de definição da API.
1. [Configurar a integração contínua/implantação contínua(CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Modifique o swagger.json no controle do código-fonte em \site\wwwroot\.azurefunctions\swagger\swagger.json.

Agora, as alterações tooswagger.json no seu repositório são hospedados por seu aplicativo de função na URL de definição de saudação API e chave que você anotou na etapa 1.c.

## <a name="next-steps"></a>Próximas etapas
* [Tutorial de introdução](functions-api-definition-getting-started.md). Tente toosee nosso passo a passo uma definição de OpenAPI em ação.
* [Repositório do GitHub do Azure Functions](https://github.com/Azure/Azure-Functions/). Check-out Olá funções repositório toogive nos comentários sobre a visualização de suporte de definição de saudação API. Torne um problema do GitHub para qualquer coisa que você deseja toosee atualizado.
* [Referência do desenvolvedor do Azure Functions](functions-reference.md). Saiba mais sobre a codificação de funções e definição de gatilhos e associações.
