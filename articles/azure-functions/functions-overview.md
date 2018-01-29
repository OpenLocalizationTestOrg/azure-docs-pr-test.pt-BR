---
title: "Visão geral do Azure Functions | Microsoft Docs"
description: "Compreenda como usar o Azure Functions para otimizar cargas de trabalho assíncronas em minutos."
services: functions
documentationcenter: na
author: mattchenderson
manager: cfowler
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/03/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: d60c898225b944801504f38d536262134a31e021
ms.sourcegitcommit: c7215d71e1cdeab731dd923a9b6b6643cee6eb04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="an-introduction-to-azure-functions"></a>Uma introdução ao Azure Functions  
O Azure Functions é uma solução para executar facilmente pequenos trechos de código, ou "funções", na nuvem. Você pode simplesmente escrever o código de que necessita para o problema em questão, sem se preocupar com todo o aplicativo ou a infraestrutura para executá-lo. O Functions pode tornar o desenvolvimento ainda mais produtivo e você pode usar a linguagem de desenvolvimento de sua escolha, como C#, F#, Node.js, Java, Python ou PHP. Pague somente pelo tempo de execução do seu código e confie no Azure para dimensioná-lo conforme a necessidade. O Azure Functions permite desenvolver aplicativos [sem servidor](https://azure.microsoft.com/overview/serverless-computing/) no Microsoft Azure.

Este tópico fornece uma visão geral de alto nível do Azure Functions. Se você quiser começar a usar imediatamente o Functions, comece com [Criar seu primeiro Azure Function](functions-create-first-azure-function.md). Se você estiver procurando informações mais técnicas sobre o Functions, confira a [referência do desenvolvedor](functions-reference.md).

## <a name="features"></a>Recursos
Aqui estão alguns dos principais recursos do Functions:

* **Opção de linguagem** – grave funções usando sua seleção de C#, F # ou Javascript. Consulte [Linguagens com suporte](supported-languages.md) para outras opções.
* **Modelo de preços de pagamento por uso** – pague somente pelo tempo gasto na execução de seu código. Veja a opção de plano de hospedagem de consumo na [seção de preços](#pricing).  
* **Traga suas próprias dependências** – o Functions dá suporte a NuGet e NPM e, portanto, você pode usar suas bibliotecas favoritas.  
* **Segurança integrada** – proteja funções disparadas por HTTP com provedores de OAuth como Azure Active Directory, Facebook, Google, Twitter e Conta da Microsoft.  
* **Integração simplificada** – aproveite facilmente as ofertas dos serviços do Azure e de SaaS (software como um serviço). Confira a [seção de integrações](#integrations) para obter alguns exemplos.  
* **Desenvolvimento flexível** – escreva suas funções diretamente no portal ou configure a integração contínua e implante seu código por meio do [GitHub](../app-service/scripts/app-service-cli-continuous-deployment-github.md), do [Visual Studio Team Services](../app-service/scripts/app-service-cli-continuous-deployment-vsts.md) e de outras [ferramentas de desenvolvimento com suporte](../app-service/app-service-deploy-local-git.md).  
* **Software livre** – O Functions é um software livre e [está disponível no GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>O que posso fazer com o Functions?
O Functions é uma ótima solução para processamento de dados, integração de sistemas, trabalho com a IoT (Internet das coisas) e criação de APIs e microsserviços simples. Considere o Functions para tarefas como processamento de imagens ou pedidos, manutenção de arquivos ou tarefas que você deseja executar de maneira agendada. 

O Functions fornece modelos para você poder começar em cenários chave, incluindo os seguintes:

* **HTTPTrigger** – dispara a execução do seu código usando uma solicitação HTTP. Para obter um exemplo, consulte [Criar sua primeira função](functions-create-first-azure-function.md).
* **TimerTrigger** – execute limpeza ou outras tarefas em lotes em uma programação predefinida. Para um exemplo, consulte [Criar uma função disparada por um temporizador](functions-create-scheduled-function.md).
* **Webhook GitHub** – responde a eventos que ocorrem em seus repositórios GitHub. Para um exemplo, consulte [Criar uma função disparada pelo webhook do GitHub](functions-create-github-webhook-triggered-function.md).
* **Webhook genérico** – processa solicitações de webhook HTTP de qualquer serviço que dá suporte a webhooks. Para um exemplo, consulte [Criar uma função disparada por um webhook genérico](functions-create-generic-webhook-triggered-function.md).
* **CosmosDBTrigger** – processe documentos do Azure Cosmos DB quando eles forem adicionados ou atualizados em coleções em um banco de dados NoSQL. Para ver um exemplo, consulte [Criar uma função disparada pelo Azure Cosmos DB](functions-create-cosmos-db-triggered-function.md).
* **BlobTrigger** – processa blobs do Armazenamento do Azure quando são adicionados a contêineres. Você pode usar essa função para o redimensionamento de imagens. Para obter mais informações, consulte [Associações de armazenamento de blobs](functions-bindings-storage-blob.md).
* **QueueTrigger** – responde às mensagens que chegam em uma fila do Armazenamento do Azure. Para ver um exemplo, consulte [Criar uma função disparada pelo armazenamento de fila do Azure](functions-create-storage-queue-triggered-function.md).
* **EventHubTrigger** - responder a eventos entregues a um Hub de Eventos do Azure. É especialmente útil em cenários de instrumentação de aplicativos, de processamento de fluxo de trabalho ou experiência do usuário e de Internet das Coisas (IoT). Para obter mais informações, consulte [Associações de Hubs de Eventos](functions-bindings-event-hubs.md).
* **ServiceBusQueueTrigger** – conecte seu código a outros serviços do Azure ou serviços locais por meio da escuta de filas de mensagens. Para obter mais informações, consulte [Associações de Barramento de Serviço](functions-bindings-service-bus.md).
* **ServiceBusTopicTrigger** – conecte seu código a outros serviços do Azure ou serviços locais por meio da assinatura de tópicos. Para obter mais informações, consulte [Associações de Barramento de Serviço](functions-bindings-service-bus.md).

O Azure Functions dá suporte a *gatilhos*, que são maneiras de iniciar a execução do seu código, e *associações*, que são maneiras de simplificar a codificação de dados de entrada e de saída. Para obter uma descrição detalhada dos gatilhos e associações que o Azure Functions fornece, confira a [Referência do desenvolvedor de disparadores e associações do Azure Functions](functions-triggers-bindings.md).

## <a name="integrations"></a>Integrações
O Azure Functions integra-se com uma variedade de serviços do Azure e de terceiros. Esses serviços podem disparar a sua função e iniciar a execução ou podem servir como entrada e saída para seu código. As integrações de serviço a seguir têm suporte do Azure Functions:

* Azure Cosmos DB
* Hubs de eventos do Azure 
* Grade de Eventos do Azure
* Aplicativos Móveis do Azure (tabelas)
* Hubs de Notificação do Azure
* Barramento de Serviço do Azure (filas e tópicos)
* Armazenamento do Azure (blob, filas e tabelas) 
* GitHub (webhooks)
* No local (usando o Barramento de Serviço)
* Twilio (mensagens SMS)

## <a name="pricing"></a>Quanto custa o Functions?
As funções do Azure têm dois tipos de planos de preços. Escolha a opção que melhor atende às suas necessidades: 

* **Plano de consumo** – quando sua função é executada, o Azure fornece todos os recursos computacionais necessários. Você não precisa se preocupar com o gerenciamento de recursos e paga apenas pelo tempo de execução do seu código. 
* **Plano do Serviço de Aplicativo** – executa suas funções como aplicativos Web, móveis e de API. Quando você já estiver usando o Serviço de Aplicativo para os outros aplicativos, poderá executar suas funções no mesmo plano sem custo adicional. 

Para obter mais informações sobre planos de hospedagem, consulte [Comparação de planos de hospedagem do Azure Functions](functions-scale.md). Os detalhes de preços completos estão disponíveis na [página Preço do Functions](https://azure.microsoft.com/pricing/details/functions/).

## <a name="next-steps"></a>Próximas etapas
* [Criar sua primeira função](functions-create-first-azure-function.md)  
  Crie diretamente sua primeira função usando o início rápido do Azure Functions. 
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)  
  Fornece informações mais técnicas sobre o tempo de execução do Azure Functions e uma referência para funções de codificação e definição de associações e gatilhos.
* [Testando o Azure Functions](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar suas funções.
* [Como escalar o Azure Functions](functions-scale.md)  
  Discute os planos de serviço disponíveis com o Azure Functions, incluindo o plano de hospedagem de consumo e como escolher o plano certo. 
* [Saiba mais sobre o Serviço de Aplicativo do Azure](../app-service/app-service-web-overview.md)  
  O Azure Functions aproveita o Serviço de Aplicativo do Azure para a funcionalidade básica como implantações, variáveis de ambiente e diagnóstico. 

