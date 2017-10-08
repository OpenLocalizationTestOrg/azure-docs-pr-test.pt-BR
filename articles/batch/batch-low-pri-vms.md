---
title: "aaaRun cargas de trabalho de lote do Azure em VMs de baixa prioridade econômicas (visualização) | Microsoft Docs"
description: "Saiba como saudação de tooreduce de VMs de baixa prioridade tooprovision custo de cargas de trabalho de lote do Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Usar VMs de baixa prioridade com o Lote (versão prévia)

Lote do Azure oferece o custo de saudação tooreduce baixa priorty máquinas de virtuais (VMs) de cargas de trabalho em lotes. VMs de baixa prioridade possibilitam novos tipos de cargas de trabalho do Lote, fornecendo uma grande capacidade de computação que também é mais econômica.

VMs de baixa prioridade tiram proveito da capacidade excedente do Azure. Quando você especifica VMs de baixa prioridade em seus pools, o Lote do Azure pode usar automaticamente esse excedente quando ele estiver disponível.

compensação Olá para o uso de máquinas virtuais de prioridade baixa é que essas VMs podem ser apropriadas quando não há capacidade excedente está disponível no Azure. Por esse motivo, as VMs de baixa prioridade são mais adequadas para determinados tipos de cargas de trabalho. Use máquinas virtuais de baixa prioridade para o lote e cargas de trabalho de processamento assíncrono em que o tempo de conclusão do trabalho de saudação é flexível e trabalho Olá é distribuído entre várias VMs.

VMs de baixa prioridade são significativamente mais baratas que VMs dedicadas. Para ver detalhes dos preços, consulte [Preços do Lote](https://azure.microsoft.com/pricing/details/batch/).

Para uma discussão adicional de VMs de baixa prioridade, consulte o anúncio de postagem de blog Olá: [em lote de computação em uma fração do preço Olá](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Atualmente, as VMs de baixa prioridade estão na fase de versão prévia e estão disponíveis apenas para cargas de trabalho em execução no Lote. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Casos de uso para VMs de baixa prioridade

Dadas as características de saudação de VMs de baixa prioridade, quais cargas de trabalho podem e não podem usá-los? De modo geral, cargas de trabalho de processamento em lote são uma boa opção, uma vez que os trabalhos são divididos em várias tarefas paralelas ou há muitos trabalhos que são expandidos e distribuídos entre várias VMs.

-   uso de toomaximize de capacidade excedente em trabalhos do Azure, adequados pode expandir.

-   Ocasionalmente, máquinas virtuais podem não estar disponíveis ou serão superados, que resultará na capacidade reduzida de trabalhos e pode causar a execução repetida e tootask interrupção. Trabalhos, portanto, devem ser flexíveis em tempo de saudação que toorun podem ser tomadas.

-   Trabalhos com tarefas mais longas podem ser mais afetados se forem interrompidos. Se demoradas tarefas implementam o andamento do ponto de verificação toosave conforme eles são executados, em seguida, o impacto de interrupção seria muito menor. Tarefas com tempos de execução menores tendem toowork melhor com baixa prioridade VMs como Olá impacto de interrupção é muito menor.

-   Trabalhos MPI que utilizam várias VMs não são toouse adequado de longa execução VMs de baixa prioridade como uma VM admitiu preempção serão provavelmente lead toohello todo trabalho executará toobe novamente.

Alguns exemplos de processamento em lotes usam casos toouse adequado VMs de baixa prioridade são:

-   **Desenvolvimento e teste**: em particular, se soluções de grande escala estiverem sendo desenvolvidas, economias significativas podem ser obtidas. Todos os tipos de testes podem ser beneficiados, mas testes de carga de larga escala e testes de regressão são ótimas opções.

-   **Complementando a capacidade sob demanda**: VMs de baixa prioridade podem ser usadas para complementar as VMs regular dedicadas - quando disponível, os trabalhos podem dimensionar e, portanto, conclua mais rápido para reduzir o custo; quando não está disponível, linha de base de saudação do dedicado VMs estão disponíveis.

-   **Tempo de execução de trabalho flexível**: se há flexibilidade em trabalhos de timer Olá ter toocomplete, e em seguida, descarta potencial na capacidade pode ser tolerada; no entanto, com hello adição dos trabalhos de VMs de baixa prioridade frequentemente será executado mais rapidamente e para reduzir o custo.

Pools de lote podem ser configurado toouse VMs de baixa prioridade de algumas maneiras, dependendo da flexibilidade de saudação em tempo de execução do trabalho:

-   VMs de baixa prioridade podem ser usadas somente em um pool e o Lote simplesmente recuperará qualquer capacidade ignorada quando disponível. Isso é mais baratos trabalhos de tooexecute de maneira hello como VMs de baixa prioridade só são usadas.

-   VMs de baixa prioridade podem ser usadas em conjunto com uma linha de base fixa de VMs dedicadas. Olá número fixo de VMs dedicados garante que haja sempre alguns tookeep capacidade um trabalho em andamento.

-   Pode ser dinâmica mistura de VMs dedicadas e de baixa prioridade, para que as VMs de baixa prioridade mais baratas são usadas somente quando disponível, mas Olá preço completo dedicado VMs são expandidas quando necessário, tookeep uma quantidade mínima de trabalhos de saudação do capacidade tookeep disponíveis em andamento.

## <a name="batch-support-for-low-priority-vms"></a>Suporte do Lote para VMs de baixa prioridade

Lote do Azure fornece vários recursos que o tornam fácil tooconsume e se beneficiar de VMs de baixa prioridade:

-   Pools do Lote podem conter VMs dedicadas e VMs de baixa prioridade. número de saudação de cada tipo de VM pode ser especificado quando um pool é criado ou alterado a qualquer momento para um pool existente, usando a operação de redimensionamento explícita de saudação ou dimensionamento automático. Envio de trabalhos e tarefas pode permanecer inalterado e não precisa se preocupar com tipos VM Olá no pool de saudação. Também é possível toohave um pool completamente usar baixa prioridade VMs toorun trabalhos barata possível, mas de aceleração dedicadas VMs se capacidade Olá cair abaixo do limite mínimo, para manter os trabalhos em execução.

-   Pools de lote automaticamente buscam toohello número de destino de VMs de baixa prioridade. Se as VMs são capturadas, lote tentará Olá tooreplace perda a capacidade e o destino de retorno toohello.

-   No caso de saudação de tarefas que está sendo interrompida, lote detectará e automaticamente enfileiramento toobe tarefas execute novamente.

-   VMs de baixa prioridade têm uma cota de núcleos que difere das VMs dedicadas. 
    Olá aspas para VMs de baixa prioridade é maior do que VMs dedicadas, porque as VMs de baixa prioridade menor custam. Consulte [Limites e cotas do serviço de Lote](batch-quota-limit.md#resource-quotas) para obter mais informações.    

> [!NOTE]
> Máquinas virtuais de baixa prioridade atualmente não têm suporte para contas de lote em que o modo de alocação de pool hello está definido muito[assinatura de usuário](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Criar e atualizar pools

Um pool de lote pode conter dedicados e de baixa prioridade máquinas virtuais (também chamados tooas nós de computação). Você pode definir o número de destino de saudação de nós de computação para VMs dedicadas e de baixa prioridade. Olá, número de nós de destino Especifica Olá número de VMs que você deseja toohave no pool de saudação.

Por exemplo, toocreate um pool usando o serviço de nuvem do Azure VMs com um destino de 5 dedicado VMs e 20 VMs de baixa prioridade:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

toocreate um pool de máquinas virtuais do Azure (no caso VMs do Linux) com um destino de 5 dedicado VMs e 20 VMs de baixa prioridade:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Você pode obter o número atual de saudação de nós para VMs dedicadas e de baixa prioridade:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Nós de pool tem uma propriedade tooindicate se nó Olá é uma VM dedicada ou de baixa prioridade:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Quando um ou mais nós em um pool são capturadas, uma operação de lista de nós no pool ainda retornará os nós, Olá o número atual de nós de baixa prioridade permanece inalterado, mas esses nós terá seu estado definido toothe **admitiu preempção**estado. Lote tentará toofind substituição VMs e, se for bem-sucedido, nós Olá passará por **criando** e **iniciando** estados antes de se tornar disponível para execução de tarefas, como novos nós.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Dimensionar um pool que contém VMs de baixa prioridade

Como ocorre com pools consiste exclusivamente em VMs dedicadas, é possível tooscale uma pool que contém baixa prioridade VMs chamando o método de redimensionamento hello, ou usando o dimensionamento automático.

operação de redimensionamento do pool Hello usa um parâmetro opcional segundo que atualiza o valor de **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

fórmula de dimensionamento automático do pool de saudação dá suporte a VMs de baixa prioridade da seguinte maneira:

-   Você pode obter ou definir o valor de saudação da variável definida pelo serviço de saudação **$TargetLowPriorityNodes**.

-   Você pode obter o valor de saudação da variável definida pelo serviço de saudação **$CurrentLowPriorityNodes**.

-   Você pode obter o valor de saudação da variável definida pelo serviço de saudação **$PreemptedNodeCount**. 
    Essa variável retorna o número de saudação de nós no hello preempção estado e permite que você expandir ou reduzir o número de saudação de nós dedicado, dependendo do número de saudação de admitiu preempção nós que não estão disponíveis.

## <a name="jobs-and-tasks"></a>Trabalhos e tarefas

Trabalhos e tarefas exigem muito pouco suporte para nós de baixa prioridade. suporte apenas para Olá é o seguinte:

-   Olá JobManagerTask propriedade de um trabalho tem uma nova propriedade, **AllowLowPriorityNode**. 
    Quando essa propriedade é true, a tarefa do Gerenciador de trabalho Olá pode ser agendada em um nó dedicado ou de baixa prioridade. Se essa propriedade for falsa, tarefa do Gerenciador de trabalho Olá será agendado tooa nó dedicado.

-   Um [variável de ambiente](batch-compute-node-environment-variables.md) é o aplicativo de tarefa tooa disponíveis para que ele possa determinar se ele está em execução em um nó de baixa prioridade ou dedicado. variável de ambiente Olá é AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Tratamento de preempções

Ocasionalmente, podem ser impedidas VMs; Quando isso acontece, o lote Olá a seguir:

-   VMs admitiu preempção Hello têm seu estado atualizado muito**admitiu preempção**.
-   Se estavam executando tarefas hello preempção VMs do nó, essas tarefas são retirada da fila e execute novamente.
-   Olá VM efetivamente é excluído, à esquerda tooany dados armazenados localmente no hello VM sejam perdido.
-   pool de saudação continuamente número de tentativas tooreach Olá destino de baixa prioridade nós disponíveis. Quando a capacidade de substituição for encontrada, os nós manterão suas IDs, mas serão reinicializados, passando pelos estados **Criando** e **Inicial** antes que fiquem disponíveis para o agendamento de tarefas.
-   Contagens de preempção estão disponíveis como uma métrica de saudação portal do Azure.

## <a name="metrics"></a>Métricas

Novas métricas estão disponíveis no hello [portal do Azure](https://portal.azure.com) para nós de baixa prioridade. Essas métricas são:

- Contagem de nós de baixa prioridade
- Contagem de núcleos de baixa prioridade 
- Contagem de nós com preempção

métricas de tooview em Olá portal do Azure:

1. Navegue tooyour conta de lote no portal de saudação e exibir configurações de saudação para sua conta do lote.
2. Selecione **métricas** de saudação **monitoramento** seção.
3. Selecione métricas Olá desejar Olá **métricas disponíveis** lista.

![Métricas para nós de baixa prioridade](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Próximas etapas

* Saudação de leitura [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md), informações essenciais para qualquer pessoa toouse lote de preparação. artigo Olá contém informações mais detalhadas sobre os recursos de serviço de lote como pools, nós, trabalhos e tarefas e Olá muitos recursos da API que você pode usar ao criar seu aplicativo de lote.
* Saiba mais sobre Olá [ferramentas e APIs de lote](batch-apis-tools.md) disponíveis para criar soluções de lote.
