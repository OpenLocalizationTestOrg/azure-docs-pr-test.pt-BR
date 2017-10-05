---
title: "Consumo do Azure Functions e planos de Serviço de Aplicativo | Microsoft Docs"
description: "Entenda como os Azure Functions escalam para atender às necessidades das cargas de trabalho orientadas por eventos."
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
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Consumo do Azure Functions e planos de Serviço de Aplicativo 

## <a name="introduction"></a>Introdução

Você pode executar o Azure Functions em dois modos diferentes: o plano de Consumo e o plano do Serviço de Aplicativo do Azure. O plano de Consumo automaticamente aloca potência de computação quando seu código está em execução, escala horizontalmente conforme a necessidade para tratar da carga e reduz verticalmente quando o código não está em execução. Assim, você não precisa pagar por VMs ociosas e não precisa reservar capacidade com antecedência. Este artigo se concentra no plano de Consumo. Para obter detalhes sobre como o plano do Serviço de Aplicativo funciona, consulte [Visão geral detalhada de planos de Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Se ainda não estiver familiarizado com o Azure Functions, veja a [Visão geral do Azure Functions](functions-overview.md).

Ao criar um aplicativo de funções, você deve configurar um plano de hospedagem para funções contidas no aplicativo. Em qualquer modo, uma instância do *host do Azure Functions* executa as funções. O tipo de controles de plano:

* Como as instâncias de host são dimensionadas.
* Os recursos que estão disponíveis para cada host.

No momento, você deve escolher o tipo de plano durante a criação do aplicativo de funções. Não é possível alterá-lo posteriormente. 

É possível dimensionar entre camadas no Plano do serviço de aplicativo. No plano de Consumo, o Azure Functions trata automaticamente de toda a alocação de recursos.

## <a name="consumption-plan"></a>Plano de consumo

Ao usar um plano de Consumo, as instâncias do host do Azure Functions são adicionadas e removidas dinamicamente com base no número de eventos de entrada. Esse plano é escalado automaticamente, e você é cobrado pelos recursos de computação apenas durante a execução de suas funções. Em um plano de Consumo, uma função pode ser executada por no máximo 10 minutos. 

> [!NOTE]
> O tempo limite padrão para funções em um plano de consumo é de 5 minutos. O valor pode ser aumentado para 10 minutos para o aplicativo Função, alterando a propriedade `functionTimeout` em [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

A cobrança é baseada no tempo de execução e na memória usada e é agregada em todas as funções dentro de um aplicativo de funções. Para saber mais, confira a [página de preços do Azure Functions].

O plano de Consumo é o padrão e oferece os seguintes benefícios:
- Pague apenas quando suas funções forem executadas.
- Escale horizontalmente de forma automática, mesmo durante períodos de carga alta.

## <a name="app-service-plan"></a>Plano do Serviço de Aplicativo

No Plano do Serviço de Aplicativo, seus aplicativos de funções são executados em VMs dedicadas, em SKUs Basic, Standard e Premium, assim como os Aplicativos Web. VMs dedicadas são alocadas aos seus aplicativos do Serviço de Aplicativo, o que significa que o host das funções está sempre em execução.

Considere um Plano do Serviço de Aplicativo nos seguintes casos:
- Você tem VMs subutilizadas que já estão executando outras instâncias do Serviço de Aplicativo.
- Você espera que seus aplicativos de função executem de forma contínua, ou quase contínua.
- Você precisa de mais opções de CPU ou memória do que é fornecido no plano de Consumo.
- Você precisa executar por mais tempo do que o tempo de execução máximo permitido no plano de Consumo.

Uma VM separa o custo do tempo de execução e do tamanho da memória. Como resultado, você não paga mais do que o custo da instância da VM alocada. Para obter detalhes sobre como o plano do Serviço de Aplicativo funciona, consulte [Visão geral detalhada de planos de Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Com um plano do Serviço de Aplicativo, você pode escalar horizontalmente manualmente adicionando mais instâncias de VM ou você pode habilitar o dimensionamento automático. Para obter mais informações, consulte [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Você também pode escalar verticalmente escolhendo um plano do Serviço de Aplicativo diferente. Para obter mais informações, consulte [Escalar verticalmente um aplicativo no Azure](../app-service-web/web-sites-scale.md). Se você estiver planejando executar funções do JavaScript em um plano do Serviço de Aplicativo, deverá escolher um plano com menos núcleos. Para obter mais informações, consulte a [Referência do JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On

Se você executar em um plano do Serviço de Aplicativo, habilite a configuração **Sempre ativado** para que seu aplicativo de funções seja executado corretamente. Em um plano do Serviço de Aplicativo, o tempo de execução das funções ficará ocioso após alguns minutos de inatividade, portanto, apenas gatilhos HTTP "despertarão" suas funções. Isso é parecido com a necessidade de o WebJobs ter o Always On habilitado. 

A opção Sempre ativo está disponível apenas em um plano do Serviço de Aplicativo. Em um plano de Consumo, a plataforma ativa automaticamente os aplicativos de função.

## <a name="storage-account-requirements"></a>Requisitos da conta de armazenamento

Em um plano de Consumo ou plano do Serviço de Aplicativo, um aplicativo de funções exige uma conta de Armazenamento do Azure com suporte ao armazenamento de Blobs, Filas e Tabelas do Azure. Internamente, o Azure Functions usa o Armazenamento do Azure para operações como gerenciamento de gatilhos e log de execuções de função. Algumas contas de armazenamento não dão suporte a filas e tabelas, como contas de armazenamento somente blob (incluindo o armazenamento premium) e contas de armazenamento de uso geral com a replicação de armazenamento com redundância de zona. Essas contas são filtradas na folha **Conta de Armazenamento** durante a criação de um aplicativo de Funções.

Para saber mais sobre os tipos de conta de armazenamento, consulte [Apresentando os serviços de armazenamento do Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-the-consumption-plan-works"></a>Como funciona o plano de consumo

O plano de Consumo escala automaticamente os recursos de CPU e memória adicionando outras instâncias do host do Functions de acordo com o número de eventos nos quais suas funções são disparadas. Cada instância do host do Funções é limitada a 1,5 GB de memória.

Ao usar o plano de hospedagem de Consumo, os arquivos do código de função são armazenados em compartilhamentos dos Arquivos do Azure na conta de armazenamento principal. Ao excluir a conta de armazenamento principal, esse conteúdo será excluído e não poderá ser recuperado.

> [!NOTE]
> Ao usar um gatilho de blob em um plano de Consumo, pode haver um atraso de até 10 minutos no processamento de novos blobs se um aplicativo de funções ficar ocioso. Depois que o aplicativo de funções estiver em execução, os blobs serão processados imediatamente. Para evitar esse atraso inicial, considere uma das seguintes opções:
> - Use um plano do Serviço de Aplicativo com a opçao Sempre ativado habilitada.
> - Use outro mecanismo para disparar o processamento de blob, como uma mensagem de fila que contém o nome do blob. Para obter um exemplo, confira [Gatilho de fila com associação de entrada de blob](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Escalonamento de tempo de execução

O Azure Functions usa um componente chamado *controlador de escala* para monitorar a taxa de eventos e determinar se deve escalar horizontalmente ou verticalmente. O controlador de escala usa heurística para cada tipo de gatilho. Por exemplo, ao usar um gatilho do armazenamento de Filas do Azure, ele escala com base no tamanho da fila e na idade da mensagem em fila mais antiga.

A unidade de escala é o aplicativo de funções. Quando o aplicativo de funções é dimensionado na horizontal, mais recursos são alocados para executar várias instâncias do host do Azure Functions. Em contrapartida, quando a demanda por computação é reduzida, o controlador de escala remove as instâncias do host de função. O número de instâncias é eventualmente reduzido a zero quando nenhuma função está em execução em um aplicativo de funções.

![Controlador de escala monitorando eventos e criando instâncias](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modelo de cobrança

A cobrança do plano de Consumo é descrita detalhadamente na [página de preços do Azure Functions]. O uso é agregado no nível do aplicativo de funções e conta apenas o tempo durante o qual o código de função está em execução. Veja a seguir as unidades de cobrança: 
* **Consumo de recursos em GB/s (gigabyte por segundo)**. Calculado como uma combinação do tamanho da memória e o tempo de execução para todas as funções dentro de um aplicativo de Funções. 
* **Execuções**. Contadas toda vez que uma função é executada em resposta a um evento, disparado por uma associação.

[página de preços do Azure Functions]: https://azure.microsoft.com/pricing/details/functions
