---
title: "Visão geral de funções de aaaAzure | Microsoft Docs"
description: "Entender como toouse funções do Azure toooptimize assíncronas cargas de trabalho em minutos."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Uma introdução tooAzure funções  
As funções do Azure é uma solução para executar facilmente pequenos pedaços de código ou "funções", na nuvem de saudação. Você pode gravar apenas o código Olá que é necessário para problema de saudação à mão, sem se preocupar um toorun de infraestrutura de aplicativo ou hello todo ele. Funções podem tornar o desenvolvimento ainda mais produtivo e você pode usar a linguagem de desenvolvimento de sua escolha, por exemplo, C#, F#, Node.js, Python ou PHP. Pague somente pelo tempo de saudação que seu código é executado e confiança do Azure tooscale conforme necessário. O Azure Functions permite desenvolver aplicativos sem servidor no Microsoft Azure.

Este tópico fornece uma visão geral de alto nível do Azure Functions. Se você quiser toojump direita e começar com funções do Azure, comece com [criar sua primeira função Azure](functions-create-first-azure-function.md). Se você estiver procurando para obter informações técnicas sobre funções, consulte Olá [referência do desenvolvedor](functions-reference.md).

## <a name="features"></a>Recursos
Aqui estão alguns dos principais recursos do Azure Functions:

* **Opção de linguagem** – escreva funções usando C#, F#, Node.js, Python, PHP, batch, bash ou qualquer executável.
* **Modelo de preços pagamento por uso** - pagar apenas para Olá tempo gasto na execução do seu código. Consulte a hospedagem de consumo Olá plano opção Olá [preços seção](#pricing).  
* **Traga suas próprias dependências** – o Functions dá suporte a NuGet e NPM e, portanto, você pode usar suas bibliotecas favoritas.  
* **Segurança integrada** – proteja funções disparadas por HTTP com provedores de OAuth como Azure Active Directory, Facebook, Google, Twitter e Conta da Microsoft.  
* **Integração simplificada** – aproveite facilmente as ofertas dos serviços do Azure e de SaaS (software como um serviço). Consulte Olá [seção integrações](#integrations) para obter alguns exemplos.  
* **Desenvolvimento flexível** - o direito de funções no portal de saudação de código ou configurar a integração contínua e implantar seu código por meio do GitHub, Visual Studio Team Services e outros [suporte para ferramentas de desenvolvimento](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Código-fonte aberto** -tempo de execução de funções de saudação é o código-fonte aberto e [disponível no GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>O que posso fazer com o Functions?
As funções do Azure é uma ótima solução para processamento de dados, integração de sistemas, trabalhando com hello internet das coisas (IoT) e criar APIs simples e microservices. Considere a possibilidade de funções para tarefas como imagem ou processamento de pedidos, manutenção de arquivo ou para qualquer tarefa que você deseja toorun em uma agenda. 

Funções fornecem modelos tooget iniciada com os principais cenários, incluindo Olá seguinte:

* **BlobTrigger** -quando eles são adicionados toocontainers os blobs de armazenamento do Azure de processo. Você pode usar essa função para o redimensionamento de imagens.
* **EventHubTrigger** -responder tooevents entregues tooan Hub de eventos do Azure. É especialmente útil em cenários de instrumentação de aplicativos, de processamento de fluxo de trabalho ou experiência do usuário e de Internet das Coisas (IoT).
* **Webhook genérico** – processa solicitações de webhook HTTP de qualquer serviço que dá suporte a webhooks.
* **GitHub webhook** -tooevents responder que ocorrem em seus repositórios GitHub. Para obter um exemplo, confira [Criar uma função de API ou webhook](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -disparar a execução de saudação do seu código usando uma solicitação HTTP.
* **QueueTrigger** -responder toomessages assim que elas chegam em uma fila de armazenamento do Azure. Para obter um exemplo, consulte [criar uma função do Azure que associa tooan serviço do Azure](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -conectar tooother seu código Azure serviços ou serviços locais por filas de toomessage escuta. 
* **ServiceBusTopicTrigger** -conectar tooother seu código do Azure services ou serviços locais ao inscrever-se tootopics. 
* **TimerTrigger** – execute limpeza ou outras tarefas em lotes em uma programação predefinida. Para ver um exemplo, confira [Criar um função de processamento de eventos](functions-create-an-event-processing-function.md).

Dá suporte a funções de Azure *gatilhos*, que são maneiras toostart de execução do seu código, e *associações*, que é maneiras toosimplify codificação para dados de entrada e saídos. Para obter uma descrição detalhada de gatilhos de saudação e associações que fornece funções do Azure, consulte [gatilhos e associações de referência do desenvolvedor do Azure funções](functions-triggers-bindings.md).

## <a name="integrations"></a>Integrações
O Azure Functions integra-se com uma variedade de serviços do Azure e de terceiros. Esses serviços podem disparar a sua função e iniciar a execução ou podem servir como entrada e saída para seu código. Olá integrações de serviço a seguir é suportado pelas funções do Azure. 

* Azure Cosmos DB
* Hubs de eventos do Azure 
* Aplicativos Móveis do Azure (tabelas)
* Hubs de Notificação do Azure
* Barramento de Serviço do Azure (filas e tópicos)
* Armazenamento do Azure (blob, filas e tabelas) 
* GitHub (webhooks)
* No local (usando o Barramento de Serviço)
* Twilio (mensagens SMS)

## <a name="pricing"></a>Quanto custa o Functions?
As funções do Azure tem dois tipos de planos de preços, escolha Olá que melhor atenda às suas necessidades: 

* **Plano de consumo** - quando a função é executada, o Azure fornece todos os recursos de computação necessários hello. Você não tem tooworry sobre gerenciamento de recursos, e você só paga pelo tempo de saudação que seu código seja executado. 
* **Plano do Serviço de Aplicativo** – executa suas funções como aplicativos Web, móveis e de API. Quando você já estiver usando o serviço de aplicativo para os outros aplicativos, você pode executar funções no mesmo plano sem custo adicional de saudação. 

Detalhes de preços completos estão disponíveis no hello [página de preços de funções](https://azure.microsoft.com/pricing/details/functions/). Para obter mais informações sobre como dimensionar suas funções, consulte [como tooscale funções do Azure](functions-scale.md).

## <a name="next-steps"></a>Próximas etapas
* [Criar sua primeira Função do Azure](functions-create-first-azure-function.md)  
  Começar imediatamente e criar sua primeira função usando o início rápido do Azure funções hello. 
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)  
  Fornece mais informações técnicas sobre o tempo de execução de funções do Azure hello e uma referência para funções de codificação e definir associações e gatilhos.
* [Testando o Azure Functions](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar suas funções.
* [Como tooscale funções do Azure](functions-scale.md)  
  Discute os planos de serviço disponíveis com as funções do Azure, incluindo o plano de hospedagem de consumo hello e como toochoose Olá plano à direita. 
* [Saiba mais sobre o Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md)  
  As funções do Azure utiliza a plataforma de serviço de aplicativo do Azure de saudação para a funcionalidade de núcleo como implantações, variáveis de ambiente e diagnóstico. 

