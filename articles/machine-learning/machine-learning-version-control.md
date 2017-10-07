---
title: "aaaALM no aprendizado de máquina do Azure | Microsoft Docs"
description: "Aplicar práticas recomendadas do Gerenciamento do Ciclo de Vida do Aplicativo no Azure Machine Learning Studio"
keywords: "ALM, AML, Azure ML, Gerenciamento do Ciclo de Vida do Aplicativo, Controle de Versão"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Gerenciamento do Ciclo de Vida do Aplicativo no Azure Machine Learning Studio
O estúdio de aprendizado de máquina do Azure é uma ferramenta para desenvolver experiências de aprendizado de máquina que são operacionalizadas na plataforma de nuvem do Azure hello. É como Olá IDE do Visual Studio e mesclados em uma única plataforma de serviço de nuvem escalonáveis. É possível incorporar práticas Application Lifecycle Management (ALM) padrão de controle de versão de implantação e execução de tooautomated ativos vários estúdio de aprendizado de máquina do Azure. Este artigo aborda algumas das opções de saudação e abordagens.

## <a name="versioning-experiment"></a>Teste de controle de versão
Há dois tooversion de maneiras recomendadas suas experiências. Você pode confiar no histórico de execução interno, ou exportar Olá experimento no formato JavaScript Object Notation (JSON) e gerenciá-lo externamente. Cada abordagem tem seus prós e contras.

### <a name="experiment-snapshots-using-run-history"></a>Instantâneos de teste usando o Histórico de Execução
No modelo de execução de saudação do hello experiência de aprendizado do estúdio de aprendizado de máquina do Azure, sempre que você clicar em Olá **executar** botão no editor de teste de hello, um instantâneo imutável do experimento Olá é enviado toohello Agendador de trabalhos. Você pode exibir essa lista de instantâneos clicando Olá **histórico de execução** botão na barra de comandos de saudação na exibição do editor de teste de saudação.

![Botão Histórico de Execução](media/machine-learning-version-control/runhistory.png)

Você pode, em seguida, instantâneo Olá aberto no modo bloqueado clicando no nome de saudação do experimento Olá na experiência de saudação do tempo Olá foi enviado toorun e Olá instantâneo foi tirado. Observe que apenas Olá primeiro item na lista de saudação, que representa a experiência atual hello, está em um estado editável. Observe também que cada instantâneo pode apresentar diversos estados de Status, incluindo Concluído (Execução parcial), Falha, Falha (Execução parcial) ou Rascunho.

![Lista do Histórico de Execução](media/machine-learning-version-control/runhistorylist.png)

Depois que ele foi aberto, você pode salvar Olá instantâneo experiência como uma nova experiência e modificá-lo. Se o instantâneo de teste contém ativos como um modelo treinado, transformação ou conjunto de dados que têm versões atualizadas, o instantâneo Olá retém versão original do hello referências toohello quando Olá instantâneo foi tirado. Se você salvar Olá bloqueado de instantâneo como uma nova experiência, estúdio de aprendizado de máquina do Azure detecta a existência de saudação de uma versão mais recente desses ativos e atualiza automaticamente no experimento novo hello.

Se você excluir a experiência de hello, todos os instantâneos desse experimento são excluídos.

### <a name="exportimport-experiment-in-json-format"></a>Importar/exportar teste no formato JSON
instantâneos de histórico de saudação executar manter uma versão imutável do experimento Olá no estúdio de aprendizado de máquina do Azure sempre que é enviado toorun. Você pode também salvar uma cópia local do experimento hello e check-in do sistema de controle de origem favorito tooyour, como Team Foundation Server e posteriormente criar novamente um experimento do arquivo local. Você pode usar o hello [PowerShell de aprendizado de máquina do Azure](http://aka.ms/amlps) commandlets [ *AmlExperimentGraph de exportação* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [  *Importação AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish que.

arquivo JSON de saudação é uma representação textual do hello experimentar gráfico, que pode incluir uma referência tooassets no espaço de trabalho hello como um conjunto de dados ou um modelo treinado. Ele não contém uma versão serializada de ativo de saudação. Se você tentar documento JSON Olá tooimport novamente no espaço de trabalho hello, ativos Olá referenciada já devem existir com hello mesmo IDs que são referenciados na experiência de saudação do ativo. Caso contrário, não será capaz de tooaccess Olá importado experimento.

## <a name="versioning-trained-model"></a>Controle de versão do modelo treinado
Um modelo treinado no aprendizado de máquina do Azure é serializado em um formato conhecido como um arquivo .iLearner e é armazenado na conta de armazenamento de BLOBs do Azure Olá associada Olá espaço de trabalho. Uma maneira tooget uma cópia do arquivo de .iLearner Olá é por meio de Olá treinamento API. [Este artigo](machine-learning-retrain-models-programmatically.md) explica como funciona a saudação treinamento API. etapas de alto nível Hello:

1. Configurar seu teste de treinamento.
2. Adicione um módulo de treinar modelo de toohello de porta de saída de serviço de web ou módulo Olá que gera o modelo treinado hello, como ajustar o modelo Hyperparameter ou criar modelo R.
3. Executar seu teste de treinamento e, depois, implantá-lo como o serviço Web de treinamento de um modelo.
4. Chame Olá ponto de extremidade BES do serviço de web de treinamento hello e especificar o nome de arquivo hello .iLearner desejado e o local de conta de armazenamento de Blob onde ele será armazenado.
5. Coleta Olá produzido .iLearner arquivo depois de chamar hello BES termina.

Outro arquivo .iLearner tooretrieve saudação de forma é por meio de saudação do PowerShell commandlet [ *Download AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Isso pode ser mais fácil se você quiser apenas tooget uma cópia da saudação .iLearner arquivo sem modelo de Olá Olá necessidade tooretrain programaticamente.

Depois que você tiver Olá .iLearner arquivo que contém o modelo treinado hello, em seguida, você pode usar sua própria estratégia de controle de versão. Olá estratégia pode ser tão simple quanto a aplicação de um versão anterior/sufixo como uma convenção de nomenclatura e deixando apenas o arquivo de .iLearner de saudação no armazenamento de Blob ou copiando/importá-los para o sistema de controle de versão.

arquivo de .iLearner salvo do Hello, em seguida, pode ser usado para classificar por meio de serviços web implantados.

## <a name="versioning-web-service"></a>Controle de versão do serviço Web
Você pode implantar dois tipos de serviços Web a partir de um teste do Azure Machine Learning. serviço de web clássico Hello está acoplado ao experimento hello, bem como o espaço de trabalho de saudação. novo serviço de web Hello usa do framework do hello Azure Resource Manager, e ele não é associado experimento original hello ou espaço de trabalho de saudação.

### <a name="classic-web-service"></a>Serviço Web clássico
tooversion um serviço web clássico, você pode tirar proveito de construção de ponto de extremidade de serviço Olá web. Este é um fluxo típico:

1. De seu teste de previsão, implante um novo serviço Web clássico, que contém um ponto de extremidade padrão.
2. Criar um novo ponto de extremidade chamado ep2, que exibe a versão atual de saudação do modelo de teste/treinamento hello.
3. Volte e atualize seu teste de previsão e modelo treinado.
4. Você reimplantar experiência previsível hello, que, em seguida, irá atualizar o ponto de extremidade saudação padrão. Mas isso não alterará o ep2.
5. Criar um ponto de extremidade adicional denominado ep3, que expõe a nova versão de saudação do experimento hello e treinado.
6. Volte toostep 3 se necessário.

Ao longo do tempo, você pode ter vários pontos de extremidade criados no hello mesmo serviço de web. Cada ponto de extremidade representa uma cópia point-in-time do experimento Olá contendo Olá point-in-time versão treinado hello. Você pode usar lógica externa toodetermine toocall qual ponto de extremidade, o que efetivamente significa selecionar uma versão de hello treinou o modelo para a execução da pontuação de saudação.

Você também pode criar vários pontos de extremidade de serviço de web idênticos e, em seguida, patch versões diferentes do hello .iLearner arquivo toohello ponto de extremidade tooachieve efeito semelhante. [Este artigo](machine-learning-create-models-and-endpoints-with-powershell.md) explica detalhadamente como tooaccomplish que.

### <a name="new-web-service"></a>Novo serviço Web
Se você criar um novo serviço web baseado em Gerenciador de recursos do Azure, Olá construção de ponto de extremidade não está mais disponível. Em vez disso, você pode gerar arquivos de definição (WSD) do serviço web, no formato JSON, de sua experiência de previsão usando Olá [AmlWebServiceDefinitionFromExperiment de exportação](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) commandlet PowerShell, ou usando Olá [ *AzureRmMlWebservice de exportação* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) PowerShell commandlet de um serviço web implantado com base no Gerenciador de recursos.

Depois de ter hello exportada versão e o arquivo WSD controlá-lo, você também pode implantar Olá WSD como um novo serviço da web em um plano de serviço web diferente em uma região do Azure diferente. Verifique se que você fornecer a conta de armazenamento adequado Olá configuração, bem como Olá web novo ID do plano de serviço. toopatch nos arquivos de .iLearner diferente, você pode modificar o arquivo WSD de saudação e modelo de atualização Olá referência ao local de saudação treinada e implantá-lo como um novo serviço web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatizar a implantação e a execução do teste
Um aspecto importante do ALM é a execução de saudação do toobe tooautomate capaz e processo de implantação de aplicativo hello. No aprendizado de máquina do Azure, você pode fazer isso usando Olá [módulo PowerShell](http://aka.ms/amlps). Aqui está um exemplo de ponta a ponta etapas de processo de implantação/execução ALM automatizada padrão tooa relevantes usando Olá [módulo de aprendizado de máquina do Azure Studio PowerShell](http://aka.ms/amlps). Cada etapa é vinculado tooone ou mais cmdlets do PowerShell que você pode usar tooaccomplish etapa.

1. [Carregar um conjunto de dados](https://github.com/hning86/azuremlps#upload-amldataset).
2. Copie uma experiência de treinamento no espaço de trabalho de saudação de um [espaço de trabalho](https://github.com/hning86/azuremlps#copy-amlexperiment) ou [galeria](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), ou [importar](https://github.com/hning86/azuremlps#import-amlexperimentgraph) um [exportado](https://github.com/hning86/azuremlps#export-amlexperimentgraph) experiências de disco local.
3. [Atualizar o conjunto de dados Olá](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) na experiência de treinamento hello.
4. [Executar teste de treinamento Olá](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Promover treinado Olá](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Copiar um experimento previsão](https://github.com/hning86/azuremlps#copy-amlexperiment) no espaço de trabalho de saudação.
7. [Treinado atualização Olá](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) experimento previsão hello.
8. [Executar teste de previsão Olá](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Implantar um serviço web](https://github.com/hning86/azuremlps#new-amlwebservice) de experiência de previsão hello.
10. Testar o serviço web de saudação [RRS](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) ou [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) ponto de extremidade.

## <a name="next-steps"></a>Próximas etapas
* Baixar Olá [PowerShell de Studio de aprendizado de máquina do Azure](http://aka.ms/amlps) tooautomate módulo e iniciar as tarefas ALM.
* Saiba como muito[criar e gerenciar um grande número de modelos ML usando apenas uma única experiência](machine-learning-create-models-and-endpoints-with-powershell.md) por meio do PowerShell e a API de treinamento.
* Saiba mais sobre [como implantar serviços Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
