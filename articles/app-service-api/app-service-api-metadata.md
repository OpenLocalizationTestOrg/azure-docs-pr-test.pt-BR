---
title: "metadados de aplicativos de API do serviço de aaaApp para API descoberta e geração de código | Microsoft Docs"
description: "Saiba como aplicativos de API no serviço de aplicativo do Azure usar Swagger metadados toofacilitate API descoberta e geração de código."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Metadados de Aplicativos de API do Serviço de Aplicativo para geração de códigos e descoberta de API
O suporte para metadados de API do [Swagger 2.0](http://swagger.io/) baseia-se em Aplicativos de API do Serviço de Aplicativo. Você não tem toouse Swagger, mas se você usá-lo, você pode tirar proveito dos recursos de aplicativos de API que facilitam a descoberta e o consumo.   

## <a name="swagger-endpoint"></a>Ponto de extremidade do Swagger
Você pode especificar um ponto de extremidade que fornece os metadados do Swagger 2.0 JSON para um aplicativo de API em uma propriedade de saudação do aplicativo de API. ponto de extremidade Olá pode ser toohello relativo a URL base do aplicativo de API de saudação ou uma URL absoluta. URLs absolutas podem apontar fora do aplicativo de API hello. 

Muitos clientes downstream (por exemplo, geração de código do Visual Studio e PowerApps "Adicionar API" fluxo), Olá URL deve estar publicamente acessível (não seja protegido pelo usuário ou autenticação de serviço). Isso significa que, se você estiver usando a autenticação do serviço de aplicativo e deseja tooexpose de definição de API de saudação de dentro de seu próprio aplicativo, você precisa toouse opção de autenticação que permite que o tráfego anônimo tooreach sua API. Para obter mais informações, consulte [Autenticação e autorização para Aplicativos de API do Serviço de Aplicativo](app-service-api-authentication.md).

### <a name="portal-blade"></a>Folha do Portal
Em Olá [portal do Azure](https://portal.azure.com/) Olá ponto de extremidade de URL pode ser vista e alterada em Olá **de definição de API** folha.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Propriedade do Gerenciador de Recursos do Azure
Você também pode configurar a URL de definição de saudação API para um aplicativo de API usando [Resource Explorer](https://resources.azure.com/) ou [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) em ferramentas de linha de comando como [Azure PowerShell](/powershell/azureps-cmdlets-docs)e hello [CLI do Azure](../cli-install-nodejs.md). 

Em **Resource Explorer**, ir muito**assinaturas > {sua assinatura} > resourceGroups > {seu grupo de recursos} > provedores > Microsoft > sites > {seu site} > Configuração > web**, e você verá Olá `apiDefinition` propriedade:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Para obter um exemplo de um modelo do Gerenciador de recursos do Azure que define Olá `apiDefinition` propriedade, abra Olá [azuredeploy.json arquivo no aplicativo de exemplo da lista de tarefas pendentes de saudação](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Localize a seção de saudação do modelo Olá que se parece com exemplo JSON hello mostrado acima.

### <a name="default-value"></a>Valor padrão
Quando você usa o Visual Studio toocreate um aplicativo de API, ponto de extremidade de definição de saudação API é definido automaticamente toohello a URL base do aplicativo de API de hello mais `/swagger/docs/v1`. Esta é a URL de padrão de saudação que Olá [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pacote NuGet usa os metadados do Swagger tooserve gerado dinamicamente de um projeto de API da Web ASP.NET. 

## <a name="code-generation"></a>Geração de código
Um dos benefícios de saudação da integração do Swagger em aplicativos de API do Azure é a geração de código automática. Classes de cliente gerada tornam mais fácil toowrite o código que chama um aplicativo de API.

Você pode gerar o código do cliente para um aplicativo de API usando o Visual Studio ou da linha de comando de saudação. Para obter informações sobre como o cliente toogenerate classes no Visual Studio para um projeto de API da Web ASP.NET, consulte [começar a usar aplicativos de API e ASP.NET](app-service-api-dotnet-get-started.md#codegen). Para obter informações sobre como toodo-lo do comando Olá linha para todos os idiomas com suporte, consulte o arquivo Leiame Olá Olá [Azure/autorest](https://github.com/azure/autorest) repositório em GitHub.com.

## <a name="next-steps"></a>Próximas etapas
Para obter um tutorial passo a passo que oriente você durante a criação, a implantação e o consumo de um aplicativo de API, confira [Introdução aos Aplicativos de API no Serviço de Aplicativo do Azure](app-service-api-dotnet-get-started.md).

Se você usar o gerenciamento de API do Azure com aplicativos de API, você pode usar o tooimport de metadados Swagger sua API em gerenciamento de API. Para obter mais informações, consulte [como tooimport Olá a definição de uma API com operações em gerenciamento do Azure API](../api-management/api-management-howto-import-api.md). 

