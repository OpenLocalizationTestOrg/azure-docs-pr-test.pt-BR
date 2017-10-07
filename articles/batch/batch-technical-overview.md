---
title: "aaaAzure lote executa soluções de computação paralelas em grande escala na nuvem Olá | Microsoft Docs"
description: "Saiba mais sobre como usar o serviço de lote do Azure Olá para cargas de trabalho do HPC e paralelo em larga escala"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Executar cargas de trabalho intrinsecamente paralelas com o Lote

Lote do Azure é um serviço de plataforma para a execução de aplicativos em larga escala paralelas e alto desempenho HPC (computação) com eficiência na nuvem hello. Lote do Azure agenda de trabalho de computação intensa toorun em uma coleção gerenciada de máquinas virtuais, e pode automaticamente escala de computação necessidades de saudação toomeet recursos de seus trabalhos.

Com o lote do Azure, você pode facilmente definir tooexecute de recursos de computação do Azure seus aplicativos em paralelo e em escala. Não há nenhuma necessidade toomanually criar, configurar e gerenciar um cluster de HPC, máquinas virtuais, redes virtuais ou um trabalho complexo e infraestrutura de agendamento de tarefas. O Lote do Azure automatiza ou simplifica essas tarefas para você.

## <a name="use-cases-for-batch"></a>Casos de uso para o Lote
O Lote é um serviço do Azure gerenciado que é usado para *processamento em lotes* ou *computação em lotes*, executando grandes volumes de tarefas semelhantes para obter o resultado desejado. A computação em lote é mais comumente usada por organizações que processam, transformam e analisam grandes volumes de dados regularmente.

O Lote funciona bem com cargas de trabalho e aplicativos intrinsecamente paralelos (também conhecidos como "excessivamente paralelos"). Cargas de trabalho intrinsecamente paralelas são aquelas divididas com facilidade em várias tarefas que executam o trabalho simultaneamente em vários computadores.

![Tarefas paralelas][1]<br/>

Alguns exemplos de cargas de trabalho que normalmente são processadas usando essa técnica são:

* Modelagem de riscos financeiros
* Análise de dados de clima e hidrologia
* Processamento, análise e renderização de imagens
* Codificação e transcodificação de mídia
* Análise de sequência genética
* Análise de estresse de engenharia
* Teste de software

Lote também pode executar cálculos paralelos com uma etapa reduza final hello e executar cargas de trabalho do HPC mais complexas, como [Interface MPI (Message Passing)](batch-mpi.md) aplicativos.

Para obter uma comparação entre o Lote e outras opções de solução HPC no Azure, confira [Soluções do Lote e HPC](batch-hpc-solutions.md).

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Cenário: escalar horizontalmente uma carga de trabalho paralela
Uma solução comum que usa o toointeract de APIs de lote Olá Olá serviço de lote envolve expansão trabalho intrinsecamente paralelo – como a renderização de saudação de imagens para cenas 3D – em um pool de nós de computação. Este conjunto de nós de computação pode ser "renderização farm" que fornece dezenas, centenas ou milhares de trabalho de processamento de tooyour núcleos, por exemplo.

Olá diagrama a seguir mostra o trabalho em lotes comuns, com um aplicativo cliente ou um serviço hospedado usando o lote toorun uma carga de trabalho paralela.

![Fluxo de trabalho da solução do Lote][2]

Nesse cenário comum, o aplicativo ou serviço processa uma carga de trabalho computacional em lote do Azure executando Olá etapas a seguir:

1. Carregar Olá **arquivos de entrada** e hello **aplicativo** que processará os arquivos tooyour conta de armazenamento do Azure. arquivos de entrada Hello podem ser qualquer dado que seu aplicativo será processado como dados de modelagem financeira ou arquivos de vídeo toobe transcodificado. arquivos de aplicativo Hello podem ser qualquer aplicativo que é usado para processar dados hello, como um aplicativo de renderização 3D ou transcodificador de mídia.
2. Criar um lote **pool** de nós de computação em sua conta de lote – esses nós são máquinas virtuais Olá que irá executar suas tarefas. Especifique propriedades como Olá [tamanho de nó](../cloud-services/cloud-services-sizes-specs.md), seu sistema operacional e o local de saudação no armazenamento do Azure do hello aplicativo tooinstall quando nós Olá unir pool hello (aplicativo hello que você carregou na etapa 1 #). Você também pode configurar o pool de saudação muito[dimensionar automaticamente](batch-automatic-scaling.md) na carga de trabalho de toohello de resposta que geram suas tarefas. Dimensionamento automático dinamicamente ajusta o número de saudação de nós de computação no pool de saudação.
3. Criar um lote **trabalho** toorun carga de trabalho de Olá no pool de saudação de nós de computação. Ao criar um trabalho, você pode associá-lo a um pool do Lote.
4. Adicionar **tarefas** toohello trabalho. Quando você adiciona o trabalho de tooa de tarefas, Olá serviço de lote agenda automaticamente tarefas Olá para execução em nós de computação Olá no pool de saudação. Cada tarefa usa o aplicativo hello que você carregou tooprocess arquivos de entrada hello.
   
   * 4a. Antes de uma tarefa é executada, ele pode baixar dados de saudação (arquivos de entrada hello) é tooprocess toohello do nó de computação a que é atribuído. Se aplicativo hello já não foi instalado no nó da saudação (consulte a etapa 2 #), ele pode ser baixado aqui em vez disso. Quando a saudação downloads forem concluídos, tarefas de saudação executar em seus nós atribuído.
5. Como executar tarefas de hello, você pode consultar o progresso de saudação toomonitor lote de trabalho hello e suas tarefas. Seu aplicativo cliente ou serviço se comunica com serviço de lote de saudação via HTTPS. Como você pode monitorar milhares de tarefas em execução em milhares de nós de computação, certifique-se muito[consultar o serviço de lote de saudação com eficiência](batch-efficient-list-queries.md).
6. Como concluir tarefas Olá, eles podem carregar seu dados de resultado tooAzure armazenamento. Você também pode recuperar arquivos diretamente do sistema de arquivos de saudação em um nó de computação.
7. Quando o monitoramento detecta que concluiu a tarefas de saudação em seu trabalho, seu aplicativo cliente ou serviço pode baixar dados de saída Olá para processamento adicional ou de avaliação.

Mantenha em mente essa é uma maneira toouse lote e este cenário descreve apenas alguns de seus recursos disponíveis. Por exemplo, você pode executar [várias tarefas em paralelo](batch-parallel-node-tasks.md) em cada nó de computação, e você pode usar [tarefas de preparação e a conclusão do trabalho](batch-job-prep-release.md) tooprepare Olá nós para os seus trabalhos e limpar posteriormente.

## <a name="next-steps"></a>Próximas etapas
Agora que você tem uma visão geral do serviço de lote de hello, é hora toodig mais toolearn como você pode usá-lo tooprocess suas cargas de trabalho com uso intensivo de computação paralelas.

* Saudação de leitura [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md), informações essenciais para qualquer pessoa toouse lote de preparação. artigo Olá contém informações mais detalhadas sobre os recursos de serviço de lote como pools, nós, trabalhos e tarefas e Olá muitos recursos da API que você pode usar ao criar seu aplicativo de lote.
* Saiba mais sobre Olá [ferramentas e APIs de lote](batch-apis-tools.md) disponíveis para criar soluções de lote.
* [Introdução à biblioteca do lote do Azure de saudação para .NET](batch-dotnet-get-started.md) toolearn como toouse c# e Olá tooexecute de biblioteca do .NET em lotes uma carga de trabalho simple usando um fluxo de trabalho comuns do lote. Este artigo deve ser um de seu primeiro interrompido enquanto aprende como toouse Olá serviço de lote. Também há um [versão do Python](batch-python-tutorial.md) tutorial hello.
* Baixar Olá [código amostras no GitHub] [ github_samples] toosee como c# e Python pode fazer a interface com lote tooschedule e processo de exemplo cargas de trabalho.
* Check-out Olá [de aprendizado em lotes] [ learning_path] tooget uma ideia de recursos de saudação tooyou disponíveis que você saiba toowork com o lote.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
