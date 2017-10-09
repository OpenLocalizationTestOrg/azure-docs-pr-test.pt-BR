---
title: "aaaDedicated capacidade para trabalhos de serviço de execução do máquina aprendizado em lotes | Microsoft Docs"
description: "Visão geral dos serviços do Lote do Azure para trabalhos do Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Serviço do Lote do Azure para trabalhos do Machine Learning

Processamento de Pool de lote do aprendizado de máquina fornece escala gerenciada pelo cliente para hello Azure Machine Learning lote execução serviço. Clássico processamento em lotes para aprendizado de máquina ocorre em um ambiente multilocatário, o número da saudação limites de trabalhos simultâneos, você pode enviar e trabalhos é enfileirado em uma base de primeiro a entrar, primeiro a sair. Essa incerteza significa que você não pode prever com exatidão quando seu trabalho será executado.

Processamento em lote do Pool permite pools toocreate no qual você pode enviar trabalhos de lote. Controlar o tamanho de saudação do pool de saudação e toowhich pool Olá trabalho é enviado. Seu trabalho BES é executado em seu próprio processamento fornecendo espaço desempenho previsível e Olá capacidade toocreate pools de recursos que correspondem a carga de processamento de toohello que você enviar.

## <a name="how-toouse-batch-pool-processing"></a>Como o processamento em lotes Pool toouse

Configuração de lote Pool de processamento não está disponível atualmente por meio de saudação portal do Azure. toouse Pool do lote de processamento, você deve:

-   Chamar CSS toocreate uma conta de Pool de lote e obter uma URL de serviço de Pool e uma chave de autorização
-   Criar um serviço Web baseado no novo Resource Manager e um plano de cobrança

toocreate sua conta, chame o atendimento ao cliente Microsoft e suporte (CSS) e fornecer sua ID de assinatura. CSS funcionará com você toodetermine Olá capacidade apropriada para seu cenário. CSS, em seguida, configura sua conta com número de máximo de saudação de pools, você pode criar e Olá número máximo de máquinas virtuais (VMs) que você pode colocar em cada pool. Assim que sua conta estiver configurada, você receberá a URL de Serviço do Pool e uma chave de autorização.

Depois que a conta é criada, você pode usar Olá URL do serviço de Pool e autorização tooperform chave pool operações de gerenciamento em seu Pool de lote.

![Arquitetura do serviço do pool do lote.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Você pode criar pools chamando a operação de criar Pool de saudação na URL do serviço de pool de saudação que tooyou CSS fornecido. Quando você cria um pool, especifique número Olá de VMs e URL de saudação do hello swagger. JSON de um novo Gerenciador de recursos com base em serviço web de aprendizado de máquina. Esse serviço da web é fornecido a associação de cobrança de saudação do tooestablish. Olá serviço de Pool do lote usa pool de Olá Olá swagger. JSON tooassociate com um plano de cobrança. Você pode executar qualquer BES serviço da web, ambos os novo Gerenciador de recursos com base e clássico, escolha no pool de saudação.

Você pode usar qualquer serviço do novo Gerenciador de recursos com base na web, mas lembre-se de que a cobrança Olá para trabalhos de saudação é cobrado em relação ao plano de cobrança Olá associado ao serviço. Talvez você queira toocreate um serviço web e cobrança novo plano especificamente para executar trabalhos do Pool do lote.

Para saber mais sobre como criar serviços Web, confira [Implantar um serviço Web do Machine Learning do Azure](machine-learning-publish-a-machine-learning-web-service.md).

Depois de criar um pool, enviar Olá BES trabalho usando hello URL de solicitações em lote para o serviço da web de saudação. Você pode escolher toosubmit-tooa tooclassic ou pool de processamento de lote. toosubmit um processamento de Pool de tooBatch de trabalho, você adiciona Olá corpo de solicitação de envio do parâmetro toohello trabalho a seguir:

"AzureBatchPoolId":"&lt;pool ID&gt;"

Se você não adicionar o parâmetro hello, o trabalho de saudação é executado no ambiente de processo de lote clássico hello. Se o pool de saudação tiver recursos disponíveis, o trabalho de saudação começa a ser executado imediatamente. Se o pool Olá não tem recursos gratuitos, seu trabalho está na fila até que um recurso está disponível.

Se você descobrir que você regularmente alcançar a capacidade de saudação de seus pools, e você precisar de maior capacidade, pode chamar CSS e trabalhar com um representante tooincrease suas cotas.

Solicitação de exemplo:

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Considerações ao usar o processamento Pool do Lote

Processamento de Pool do lote é um serviço de faturável sempre ativa e que exige que você tooassociate-lo com um Gerenciador de recursos com base em plano de cobrança. Você só será cobrado por número de saudação de horas de computação pool hello está sendo executado. independentemente do número de saudação de trabalhos executados durante esse pool de tempo. Se você criar um pool, você será cobrado por horas de computação de saudação de cada máquina virtual no pool de saudação até que o pool de saudação é excluído, mesmo que nenhum trabalho em lotes está em execução no pool de saudação. Cobrança para máquinas virtuais de saudação inicia quando terminarem de provisionamento e interrompida quando eles foram excluídos. Você pode usar qualquer um dos planos de saudação encontrados no hello [página de preços de aprendizado de máquina](https://azure.microsoft.com/pricing/details/machine-learning/).

Exemplo de cobrança:

Caso você crie um Pool do Lote com 2 máquinas virtuais e o exclua após 24 horas, serão debitadas 48 horas de computação do seu plano de cobrança, independentemente de quantos trabalhos foram executados durante esse período.

Caso você crie um Pool do Lote com 4 máquinas virtuais e o exclua após 12 horas, também serão debitadas 48 horas de computação do seu plano de cobrança.

É recomendável que você sondar Olá toodetermine de status de trabalho quando os trabalhos são concluídos. Quando todos os trabalhos de terminar de executar, chamada hello redimensionar Pool operação tooset Olá número de máquinas virtuais em Olá pool toozero. Se você for curto em recursos do pool e é necessário toocreate um novo pool, por exemplo toobill em relação a um plano de cobrança diferente, é possível excluir o pool de saudação em vez disso, quando tem terminado de todos os trabalhos em execução.


| **Use o Processamento Pool do Lote quando**    | **Use o processamento em lotes clássico quando**  |
|---|---|
|Você precisa toorun um grande número de trabalhos<br>Ou<br/>Você precisa tooknow os trabalhos serão executados imediatamente<br/>Ou<br/>Você precisar de taxa de transferência garantida. Por exemplo, você precisa toorun um número de trabalhos em um determinado período de tempo e deseja tooscale out seu toomeet de recursos de computação às suas necessidades.    | Você estiver executando apenas alguns trabalhos<br/>e<br/> Você não precisa Olá trabalhos toorun imediatamente |
