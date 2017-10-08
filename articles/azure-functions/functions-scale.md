---
title: "planos de serviço de aplicativo e o consumo de funções aaaAzure | Microsoft Docs"
description: "Entenda como funções do Azure pode ser dimensionado toomeet necessidades de saudação das cargas de trabalho controlada por evento."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Consumo do Azure Functions e planos de Serviço de Aplicativo 

## <a name="introduction"></a>Introdução

Você pode executar o Azure Functions em dois modos diferentes: o plano de Consumo e o plano do Serviço de Aplicativo do Azure. plano de consumo Olá aloca automaticamente a capacidade de computação quando seu código está em execução, pode ser dimensionado como carga de toohandle necessário e expande para baixo quando o código não está em execução. Portanto, você não tem toopay para VMs ociosas e não tiver capacidade de tooreserve com antecedência. Este artigo se concentra no plano de consumo de saudação. Para obter detalhes sobre como funciona a saudação plano de serviço de aplicativo, consulte Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Se você não estiver familiarizado com as funções do Azure, consulte Olá [visão geral de funções do Azure](functions-overview.md).

Quando você criar um aplicativo de função, você deve configurar um plano de hospedagem para funções que o aplicativo hello contém. Em qualquer modo, uma instância do hello *host de funções do Azure* executa funções hello. tipo de saudação de controles de plano:

* Como as instâncias de host são dimensionadas.
* Olá recursos host tooeach disponíveis.

No momento, você deve escolher o tipo de plano de saudação durante a criação de saudação do aplicativo de função hello. Não é possível alterá-lo posteriormente. 

Você pode dimensionar entre camadas em Olá plano de serviço de aplicativo. Plano de consumo hello, funções do Azure controla automaticamente a alocação de todos os recursos.

## <a name="consumption-plan"></a>Plano de consumo

Quando você estiver usando um plano de consumo, instâncias do host de funções do Azure Olá dinamicamente são adicionadas e removidas com base no número de saudação de eventos de entrada. Esse plano é escalado automaticamente, e você é cobrado pelos recursos de computação apenas durante a execução de suas funções. Em um plano de Consumo, uma função pode ser executada por no máximo 10 minutos. 

> [!NOTE]
> tempo limite padrão de saudação para funções em um plano de consumo é 5 minutos. valor de saudação pode ser maior too10 minutos para Olá função aplicativo alterando a propriedade Olá `functionTimeout` na [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

A cobrança é baseada no tempo de execução e na memória usada e é agregada em todas as funções dentro de um aplicativo de funções. Para obter mais informações, consulte Olá [funções do Azure página de preços].

plano de consumo Olá Olá padrão e oferece Olá benefícios a seguir:
- Pague apenas quando suas funções forem executadas.
- Escale horizontalmente de forma automática, mesmo durante períodos de carga alta.

## <a name="app-service-plan"></a>Plano do Serviço de Aplicativo

Planeje saudação do serviço de aplicativo, sua função os aplicativos executados em VMs dedicadas em Basic, Standard e Premium SKUs, tooWeb aplicativos semelhante. Máquinas virtuais dedicadas são alocados tooyour aplicativos de serviço de aplicativo, o que significa que host de funções hello está sempre em execução.

Considere um plano de serviço de aplicativo hello casos a seguir:
- Você tem VMs subutilizadas que já estão executando outras instâncias do Serviço de Aplicativo.
- Você espera que seu toorun de aplicativos de função continuamente ou quase contínua.
- Você precisa de mais opções de CPU ou memória, que é fornecido no plano de consumo de saudação.
- É necessário toorun mais de saudação tempo de execução máximo permitido no plano de consumo de saudação.

Uma VM separa o custo do tempo de execução e do tamanho da memória. Como resultado, você não pagará maior que o custo de Olá Olá VM da instância de que você alocar. Para obter detalhes sobre como funciona a saudação plano de serviço de aplicativo, consulte Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Com um plano do Serviço de Aplicativo, você pode escalar horizontalmente manualmente adicionando mais instâncias de VM ou você pode habilitar o dimensionamento automático. Para obter mais informações, consulte [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Você também pode escalar verticalmente escolhendo um plano do Serviço de Aplicativo diferente. Para obter mais informações, consulte [Escalar verticalmente um aplicativo no Azure](../app-service-web/web-sites-scale.md). Se você estiver planejando toorun funções de JavaScript em um plano de serviço de aplicativo, você deve escolher um plano que tem menos núcleos. Para obter mais informações, consulte Olá [referência de JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On

Se você executar um plano de serviço de aplicativo, você deve habilitar Olá **AlwaysOn** configuração para que seu aplicativo de função seja executado corretamente. Um plano de serviço de aplicativo, tempo de execução de funções hello irá ocioso após alguns minutos de inatividade, portanto apenas para gatilhos HTTP serão "ativado" suas funções. Isso é semelhante toohow que webjobs deve ter Always On habilitado. 

A opção Sempre ativo está disponível apenas em um plano do Serviço de Aplicativo. Em um plano de consumo, plataforma Olá ativa automaticamente aplicativos de função.

## <a name="storage-account-requirements"></a>Requisitos da conta de armazenamento

Em um plano de Consumo ou plano do Serviço de Aplicativo, um aplicativo de funções exige uma conta de Armazenamento do Azure com suporte ao armazenamento de Blobs, Filas e Tabelas do Azure. Internamente, o Azure Functions usa o Armazenamento do Azure para operações como gerenciamento de gatilhos e log de execuções de função. Algumas contas de armazenamento não dão suporte a filas e tabelas, como contas de armazenamento somente blob (incluindo o armazenamento premium) e contas de armazenamento de uso geral com a replicação de armazenamento com redundância de zona. Essas contas são filtradas da saudação **conta de armazenamento** folha quando estiver criando um aplicativo de função.

toolearn mais sobre os tipos de conta de armazenamento, consulte [apresentando os serviços de armazenamento do Azure Olá](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Como funciona o plano de consumo Olá

plano de consumo de saudação dimensiona automaticamente os recursos de CPU e memória adicionando mais instâncias do host de funções hello, com base no número de saudação de eventos disparados em suas funções. Cada instância do host de funções hello é limitado too1.5 GB de memória.

Quando você usa Olá consumo de plano de hospedagem, arquivos de código de função armazenados em compartilhamentos de arquivos do Azure na conta de armazenamento principal de saudação. Quando você exclui a conta de armazenamento principal hello, esse conteúdo será excluído e não pode ser recuperado.

> [!NOTE]
> Quando você estiver usando um gatilho de blob em um plano de consumo, pode haver o atraso de 10 minutos tooa em processamento novos blobs, se um aplicativo de função ficou ocioso. Olá função aplicativo em execução, os blobs são processados imediatamente. tooavoid neste inicial atraso, considere uma saudação as opções a seguir:
> - Use um plano do Serviço de Aplicativo com a opçao Sempre ativado habilitada.
> - Use outro blob de saudação do tootrigger mecanismo de processamento, como uma mensagem da fila que contém o nome do blob hello. Para obter um exemplo, confira [Gatilho de fila com associação de entrada de blob](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Escalonamento de tempo de execução

As funções do Azure usa um componente chamado hello *controlador escala* toomonitor Olá taxa de eventos e determinar se tooscale out ou reduzir. controlador de escala Olá usa heurística para cada tipo de gatilho. Por exemplo, quando você estiver usando um gatilho de armazenamento de fila do Azure, ele é dimensionado com base no comprimento da fila de saudação e a idade de saudação de mensagem de fila hello mais antiga.

unidade de saudação de escala é Olá função app. Quando o aplicativo de função hello é expandido, mais recursos são alocados toorun várias instâncias do host de funções do Azure hello. Por outro lado, como redução de demanda de computação, o controlador de escala de saudação remove instâncias de função do host. número de saudação de instâncias é reduzido eventualmente toozero quando nenhuma função estiver executando em um aplicativo de função.

![Controlador de escala monitorando eventos e criando instâncias](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modelo de cobrança

Cobrança para o plano de consumo de saudação é descrito em detalhes em Olá [funções do Azure página de preços]. Uso é agregado no nível de aplicativo de função hello e contagens apenas o tempo de saudação que está executando o código de função. Olá seguem unidades de cobrança: 
* **Consumo de recursos em GB/s (gigabyte por segundo)**. Calculado como uma combinação do tamanho da memória e o tempo de execução para todas as funções dentro de um aplicativo de Funções. 
* **Execuções**. Contado cada vez que uma função é executada no evento de tooan de resposta, disparado por uma associação.

[funções do Azure página de preços]: https://azure.microsoft.com/pricing/details/functions
