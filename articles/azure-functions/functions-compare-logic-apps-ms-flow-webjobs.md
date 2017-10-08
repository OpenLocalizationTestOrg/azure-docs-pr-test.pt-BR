---
title: "aaaChoose entre fluxo, lógica de aplicativos, funções e trabalhos Web | Microsoft Docs"
description: "Comparar e contrastar Olá para serviços de integração de nuvem da Microsoft e decidir quais serviços você deve usar."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "microsoft flow, flow, aplicativos lógicos, azure functions, functions, azure webjobs, webjobs, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Escolha entre o Flow, os Aplicativos Lógicos, o Functions e o WebJobs
Este artigo compara e contrasta Olá serviços em nuvem da Microsoft hello, que todos podem solucionar problemas de integração e automação de processos de negócios a seguir:

* [Microsoft Flow](https://flow.microsoft.com/)
* [Aplicativos Lógicos do Azure](https://azure.microsoft.com/services/logic-apps/)
* [Funções do Azure](https://azure.microsoft.com/services/functions/)
* [WebJobs no Serviço de Aplicativo do Azure](../app-service-web/web-sites-create-web-jobs.md)

Todos esses serviços são úteis para "unir" sistemas diferentes. Todos eles definem entrada e saída, condições e ações. Você pode executar cada um em um cronograma ou gatilho. No entanto, cada serviço adiciona um conjunto exclusivo de valor e compará-los não é uma questão de "qual serviço é Olá melhor?" mas de "qual serviço é o mais adequado para essa situação?" Muitas vezes, uma combinação desses serviços é a melhor maneira de saudação toorapidly compilar uma solução escalonável e total integração em destaque.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow vs. Aplicativos Lógicos
Podemos discutir Microsoft Flow e os aplicativos lógicos do Azure juntos porque ambos estão *configuração primeiro* integration services, que torna fácil toobuild processos e fluxos de trabalho e integrar com vários SaaS e enterprise aplicativos. 

* O Flow é criado em cima de Aplicativos Lógicos
* Eles têm Olá mesmo designer de fluxo de trabalho
* [Conectores](../connectors/apis-list.md) que o trabalho em um também pode trabalhar no hello outros

Fluxos permite que qualquer integrações do office trabalho tooperform simples (por exemplo, get SMS para emails importantes) sem passar por desenvolvedores ou IT. Em Olá outro lado, aplicativos lógicos pode habilitar avançadas ou críticos integrações (por exemplo, processos de B2B) onde as práticas recomendadas de segurança e DevOps de nível corporativo são necessárias. É comum para um toogrow de fluxo de trabalho de negócios no tempo extra de complexidade. Da mesma forma, você pode começar com um fluxo em um primeiro e convertê-la tooa lógica aplicativo conforme necessário.

Olá tabela a seguir ajuda a determinar se o fluxo ou aplicativos lógicos é recomendados para uma determinada integração.

|  | Flow | Aplicativos Lógicos |
| --- | --- | --- |
| Público-alvo |funcionários do escritório, usuários de negócios |profissionais de TI, desenvolvedores |
| Cenários |Autoatendimento |Essenciais |
| Ferramenta de design |Aplicativo do navegador e móvel, somente interface do usuário |No navegador e no [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [Exibição de código](../logic-apps/logic-apps-author-definitions.md) disponível |
| DevOps |Ad-hoc, desenvolver em produção |controle de origem, teste, suporte, automação e capacidade de gerenciamento no [Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md) |
| Experiência de administrador |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com](https://portal.azure.com) |
| Segurança |Práticas padrão: [soberania de dados](https://wikipedia.org/wiki/Technological_Sovereignty), [criptografia em repouso](https://wikipedia.org/wiki/Data_at_rest#Encryption) para dados confidenciais etc. |Garantia de segurança do Azure: [segurança do Azure](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Central de Segurança](https://azure.microsoft.com/services/security-center/), [logs de auditoria](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/) e muito mais. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Functions vs. Trabalhos Web
Podemos discutir o Azure Functions e os WebJobs do Serviço de Aplicativo do Azure juntos porque eles são serviços de integração de *code-first* e projetados para desenvolvedores. Elas permitem que você toorun um script ou um trecho de código em eventos de toovarious de resposta, como [novos Blobs de armazenamento](functions-bindings-storage.md) ou [uma solicitação de WebHook](functions-bindings-http-webhook.md). Eis as semelhanças: 

* Ambos são criados no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) e têm recursos como [controle do código-fonte](../app-service-web/app-service-continuous-deployment.md), [autenticação](../app-service/app-service-authentication-overview.md) e [monitoramento](../app-service-web/web-sites-monitor.md).
* Ambos são serviços voltados para desenvolvedores.
* Ambos dão suporte a scripts e linguagens de programação padrão.
* Ambos têm suporte NuGet e NPM.

Funções é a evolução natural saudação de trabalhos Web que usa melhores coisas Olá WebJobs e aprimora-los. Olá aprimoramentos incluem: 

* Desenvolvimento simplificado, teste e execução de código, diretamente no navegador de saudação.
* Integração interna com outros serviços do Azure e serviços de terceiros como o [GitHub WebHooks](https://developer.github.com/webhooks/creating/).
* Pagamento por uso, toopay sem necessidade de um [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Automático, [dimensionamento dinâmico](functions-scale.md).
* Para clientes existentes do serviço de aplicativo em execução no plano do serviço de aplicativo ainda possível (tootake aproveitar recursos subutilizados).
* Integração com os Aplicativos Lógicos.

Olá, a tabela a seguir resume as diferenças de saudação entre funções e trabalhos da Web:

|  | Funções | Trabalhos Web |
| --- | --- | --- |
| Dimensionamento |Dimensionamento sem configuração |dimensionar com Plano do Serviço de Aplicativo |
| Preços |Pagamento por uso ou parte de Plano do Serviço de Aplicativo |Parte do Plano do Serviço de Aplicativo |
| Executar-tipo |disparado, agendado (pelo gatilho de temporizador) |acionado, contínuo, agendado |
| Eventos de gatilho |[temporizador](functions-bindings-timer.md), [Banco de Dados Cosmos do Azure](functions-bindings-documentdb.md), [Hubs de Eventos do Azure](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, Slack)](functions-bindings-http-webhook.md), [Aplicativos Móveis do Serviço de Aplicativo do Azure](functions-bindings-mobile-apps.md), [Hubs de Notificação do Azure](functions-bindings-notification-hubs.md), [Barramento de Serviço do Azure](functions-bindings-service-bus.md), [Armazenamento do Azure](functions-bindings-storage.md) |[Armazenamento do Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Barramento de Serviço do Azure](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Desenvolvimento no navegador |com suporte | sem suporte |
| Script de janela |experimental |com suporte |
| PowerShell |experimental |com suporte |
| C# |com suporte |com suporte |
| F# |com suporte |sem suporte |
| Bash |experimental |com suporte |
| PHP |experimental |com suporte |
| Python |experimental |com suporte |
| JavaScript |com suporte |com suporte |

Se as funções de toouse ou WebJobs depende que você já está fazendo com o serviço de aplicativo. Se você tiver um aplicativo de serviço de aplicativo para o qual você deseja toorun trechos de código, e você deseja toomanage-los juntos no mesmo ambiente DevOps de hello, você deve usar o WebJobs. Se você quiser toorun trechos de código para outros serviços do Azure ou até mesmo 3ª parte aplicativos, ou se você quiser gerenciar muito trechos de código integração separadamente de seus aplicativos de serviço de aplicativo, ou se quiser toocall trechos de código de um aplicativo lógico, você deve aproveitar todas melhorias de saudação em funções.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, Aplicativos Lógicos e Functions juntos
Como mencionado anteriormente, qual serviço é melhor adequada tooyou depende de sua situação. 

* Para a otimização de negócios simples, use o Flow.
* Se seu cenário de integração é muito avançado para o Flow, ou se você precisa de recursos de DevOps e conformidades de segurança, use os Aplicativos Lógicos.
* Se uma etapa no seu cenário de integração requer transformação altamente personalizada ou código especializado, crie um aplicativo de funções e dispare uma função como ação em seu aplicativo lógico.

Você pode chamar um aplicativo lógico em um fluxo. Você também pode chamar uma função em um aplicativo lógico e um aplicativo lógico em uma função. integração de saudação entre o fluxo, lógica de aplicativos e funções continuar tooimprove extras. Você pode criar algo em um serviço e usá-lo em Olá outros serviços. Portanto, todo o investimento feito nessas três tecnologias vale a pena.

## <a name="next-steps"></a>Próximas etapas
Comece com cada um dos serviços de saudação criando seu primeiro fluxo, lógica de aplicativo, o aplicativo de função ou WebJob. Clique em qualquer um dos links a seguir de saudação:

* [Introdução ao Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)
* [Criar sua primeira Função do Azure](functions-create-first-azure-function.md)
* [Implantar Trabalhos Web usando o Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Ou então, obter mais informações sobre esses serviços de integração com hello links a seguir:

* [Aproveitando o Azure Functions e o Serviço de Aplicativo do Azure em cenários de integração, por Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Integração simplificada, por Charles Lamanna](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Webcast ao vivo de Aplicativos Lógicos](http://aka.ms/logicappslive)
* [Perguntas frequentes sobre o Microsoft Flow](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Recursos de documentação do Azure Webjobs](../app-service-web/websites-webjobs-resources.md)

