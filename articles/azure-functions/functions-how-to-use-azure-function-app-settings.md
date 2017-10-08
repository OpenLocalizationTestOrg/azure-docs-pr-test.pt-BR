---
title: "aaaConfigure configurações de aplicativo de função do Azure | Microsoft Docs"
description: "Saiba como tooconfigure Azure funciona configurações do aplicativo."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Como um aplicativo de função no portal do Azure de saudação do toomanage 

Em funções do Azure, um função de aplicativo fornece o contexto de execução de saudação para suas funções individuais. Comportamentos de aplicativo de função se aplicam a funções tooall hospedadas por um aplicativo de determinada função. Este tópico descreve como tooconfigure e gerenciar seus aplicativos de função no hello portal do Azure.

toobegin, vá toohello [portal do Azure](http://portal.azure.com) e entrar tooyour conta do Azure. Na barra de pesquisa Olá na parte superior de saudação do portal Olá, digite nome de saudação do seu aplicativo de função e selecioná-lo na lista de saudação. Depois de selecionar o aplicativo de função, você verá Olá página a seguir:

![Visão geral do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Guia Configurações do aplicativo de funções

![Visão geral de função aplicativo no portal do Azure de saudação.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Olá **configurações** guia é onde você pode atualizar a versão de tempo de execução de funções hello usado pelo seu aplicativo de função. Também é onde você gerencia Olá host chaves usadas toorestrict HTTP acesso tooall funções hospedadas pelo aplicativo de função hello.

O Functions oferece suporte aos planos de hospedagem de Consumo e Serviço de Aplicativo. Para obter mais informações, consulte [escolha plano de serviço correta Olá para funções do Azure](functions-scale.md). Para aprimorar a previsibilidade no plano de consumo hello, funções permite limitar o uso de plataforma, definindo uma cota de uso diário, em gigabytes segundos. Quando a cota de uso diário de saudação é atingida, Olá função aplicativo está parado. Um aplicativo de função interrompido como resultado de alcançar Olá gastos cota pode ser habilitado novamente de saudação mesmo contexto de estabelecer Olá diariamente gastos cota. Consulte Olá [funções do Azure página de preços](http://azure.microsoft.com/pricing/details/functions/) para obter detalhes sobre a cobrança.   

## <a name="platform-features-tab"></a>Guia Recursos da plataforma

![Guia Recursos da plataforma do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Função aplicativos executados no e são mantidos pela plataforma do serviço de aplicativo do Azure hello. Como tal, seus aplicativos de função tem acesso toomost dos recursos de saudação da plataforma de hospedagem na web do Azure núcleo. Olá **recursos de plataforma** guia é onde você acesso Olá muitos recursos da saudação plataforma de serviço de aplicativo que você pode usar em seus aplicativos de função. 

> [!NOTE]
> Nem todos os recursos do serviço de aplicativo estão disponíveis quando um função de aplicativo é executado no plano de hospedagem de consumo de saudação.

rest Olá deste tópico se concentra em Olá seguintes recursos do serviço de aplicativo hello portal do Azure que são úteis para funções:

+ [Editor do Serviço de Aplicativo](#editor)
+ [Configurações do aplicativo](#settings) 
+ [Console](#console)
+ [Ferramentas avançadas (Kudu)](#kudu)
+ [Opções de implantação](#deployment)
+ [CORS](#cors)
+ [Autenticação](#auth)
+ [Definição da API](#swagger)

Para obter mais informações sobre como toowork com configurações de serviço de aplicativo, consulte [definir configurações de serviço de aplicativo do Azure](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Editor de Serviço de Aplicativo

| | |
|-|-|
| ![Editor do Serviço de Aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Olá editor de serviço de aplicativo é um editor no portal avançado que você pode usar arquivos de configuração JSON toomodify e arquivos de código semelhantes. Escolher essa opção inicia uma nova guia do navegador com um editor básico. Isso permite que você toointegrate com código de repositório, executar e depurar Git hello e modificar configurações de função do aplicativo. Esse editor fornece um ambiente de desenvolvimento aprimoradas para funções, em comparação com folha saudação padrão de função do aplicativo.    |

![Olá editor de serviço de aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Configurações do aplicativo

| | |
|-|-|
| ![Configurações de aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | saudação do serviço de aplicativo **configurações de aplicativo** folha é onde você pode configura e gerencia versões do framework, depuração remota, as configurações do aplicativo e cadeias de caracteres de conexão. Ao integrar seu aplicativo de funções ao Azure e a outros serviços de terceiros, você pode modificar essas configurações aqui. |

![Definir as configurações do aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Console

| | |
|-|-|
| ![Console do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | console de no portal de saudação é uma ferramenta de desenvolvedor ideal quando você prefere toointeract com seu aplicativo de função na linha de comando hello. Os comandos comuns incluem criação e navegação de diretório e arquivo, bem como execução scripts e arquivos em lote. |

![Console do aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Ferramentas avançadas (Kudu)

| | |
|-|-|
| ![Função app Kudu Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Olá ferramentas avançadas para o serviço de aplicativo (também conhecido como Kudu) fornecem acesso a recursos administrativos tooadvanced do seu aplicativo de função. No Kudu, você pode gerenciar informações do sistema, configurações do aplicativo, variáveis de ambiente, extensões do site, cabeçalhos HTTP e variáveis de servidor. Você também pode iniciar **Kudu** navegando toohello o ponto de extremidade SCM para seu aplicativo de função, como`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Opções de implantação

| | |
|-|-|
| ![Opções de implantação de aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | O Functions permite que você desenvolva o código de sua função em seu computador local. Em seguida, você pode carregar seu tooAzure de projeto de aplicativo de função local. Além disso tootraditional de carregamento FTP, funções permite que você implante seu aplicativo de função usando soluções de integração contínua populares, como GitHub, VSTS, Dropbox, Bitbucket e outros. Para saber mais, confira [Implantação contínua do Azure Functions](functions-continuous-deployment.md). tooupload manualmente usando FTP ou Git local, você também deve [configurar suas credenciais de implantação](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Função app CORS Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | execução de código mal-intencionado tooprevent em seus serviços, blocos de serviço de aplicativo chama tooyour função aplicativos de fontes externas. Funções dá suporte a recursos entre origens (CORS) toolet definir uma "lista branca" de origens das quais funções podem aceitar solicitações remotas de permissão de compartilhamento.  |

![Configurar CORS do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Autenticação

| | |
|-|-|
| ![Autenticação do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Quando as funções usam um gatilho HTTP, você pode exigir chamadas toofirst ser autenticada. O Serviço de Aplicativo oferece suporte à autenticação do Azure Active Directory e a entrada com provedores sociais, como Facebook, Microsoft e Twitter. Para obter detalhes sobre como configurar provedores de autenticação específicos, consulte [Visão geral de autenticação do serviço de aplicativo do Azure](../app-service/app-service-authentication-overview.md). |

![Configurar a autenticação para um aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Definição da API

| | |
|-|-|
| ![API de função de aplicativo swagger de definição em Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Oferece suporte a funções Swagger tooallow clientes toomore facilmente consumir funções disparado por HTTP. Para obter mais informações sobre como criar definições de API com Swagger, visite [Introdução aos aplicativos de API, ASP.NET e Swagger no Azure](../app-service-api/app-service-api-dotnet-get-started.md). Você também pode usar funções Proxies toodefine uma única superfície de API para várias funções. Para saber mais, veja [Trabalhar com o Proxies do Azure Functions](functions-proxies.md). |

![Configurar API do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Próximas etapas

+ [Definir configurações do Serviço de Aplicativo do Azure](../app-service-web/web-sites-configure.md)
+ [Implantação contínua para Azure Functions](functions-continuous-deployment.md)



