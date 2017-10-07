---
title: "módulo aaaPowerShell para aprendizado de máquina | Microsoft Docs"
description: "módulo do PowerShell Olá para o aprendizado de máquina do Azure está disponível no modo de visualização pública. Use o PowerShell toocreate e gerenciar espaços de trabalho, experiências, serviços web e muito mais."
keywords: "teste,regressão linear,algoritmos de aprendizado de máquina,tutorial de aprendizado de máquina,técnicas de modelos de previsão, teste de ciência de dados"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Módulo do PowerShell para o Microsoft Azure Machine Learning
módulo do PowerShell Olá para o aprendizado de máquina do Azure é uma ferramenta poderosa que permite que você toouse espaços de trabalho do Windows PowerShell toomanage, experiências, conjuntos de dados, os serviços da web clássico e muito mais.

Você pode exibir a documentação de saudação e baixar o módulo hello, juntamente com o código-fonte completo hello, em [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> módulo de aprendizado de máquina do Azure PowerShell Hello está atualmente em modo de visualização. módulo de saudação continuará toobe aprimorado e expandido durante esse período de visualização. Fique atento Olá [Intelligence Cortana e o Blog de aprendizado de máquina](https://blogs.technet.microsoft.com/machinelearning/) notícias e informações.

## <a name="what-is-hello-machine-learning-powershell-module"></a>O que é o módulo do PowerShell de aprendizado de máquina Olá?
módulo do PowerShell de aprendizado de máquina Olá é um. Módulo DLL com base em rede que permite que você toofully gerenciar espaços de trabalho do aprendizado de máquina do Azure, experiências, conjuntos de dados, os serviços da web clássico e pontos de extremidade de serviço de web clássico do Windows PowerShell. 

Junto com o módulo hello, você pode baixar o código-fonte completo Olá que inclui um corretamente separados [camada da API de C#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). É possível referenciar essa DLL no próprio projeto do .NET e gerenciar o Azure Machine Learning por meio do código .NET. Além disso, Olá DLL depende das APIs REST subjacente que pode ser usado diretamente do seu cliente favorito.

## <a name="what-can-i-do-with-hello-powershell-module"></a>O que pode fazer com o módulo do PowerShell Olá?
Aqui estão algumas das tarefas de saudação que podem ser executadas com este módulo do PowerShell. Check-out Olá [completo documentação](https://aka.ms/amlps) para essas e muitas mais funções.

* Provisionar um novo espaço de trabalho usando um certificado de gerenciamento ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Exportar e importar um arquivo JSON que representa um gráfico de experimento ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Executar um experimento ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Criar um serviço Web de um experimento de previsão ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Criar um ponto de extremidade em um serviço Web publicado ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Invocar um ponto de extremidade de serviço Web RRS e/ou BES ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) e [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Aqui está um exemplo rápido de usar o PowerShell toorun um experimento existente:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Para um caso de uso mais detalhado, consulte este artigo sobre como usar o hello PowerShell módulo tooautomate uma tarefa normalmente solicitado: [criar vários modelos de aprendizado de máquina e web pontos de extremidade do serviço de um experimento usando o PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Como começar?
tooget iniciado com o PowerShell de aprendizado de máquina, baixe Olá [versão pacote](https://github.com/hning86/azuremlps/releases) de saudação do GitHub e siga [as instruções para instalação](https://github.com/hning86/azuremlps/blob/master/README.md). instruções de saudação explicam como toounblock Olá baixado/descompactou DLL e, em seguida, importação-lo para o ambiente do PowerShell. A maioria das Olá cmdlets exigem que você forneça a ID do espaço de trabalho hello, token de autorização do espaço de trabalho Olá e Olá região do Azure que Olá espaço de trabalho está em. valores de saudação do Hello mais simples maneira tooprovide é através de um arquivo de config. JSON padrão. instruções de saudação também explicam como tooconfigure esse arquivo. 

E, se desejar, você pode clonar a árvore de git hello, modificar código hello e compilá-lo localmente usando o Visual Studio.

## <a name="next-steps"></a>Próximas etapas
Você pode encontrar a documentação completa Olá para o módulo PowerShell Olá [https://aka.ms/amlps](https://aka.ms/amlps). 

Para obter um exemplo estendido como toouse Olá módulo em um cenário do mundo real, o check-out Olá detalhada caso de uso, [criar vários modelos de aprendizado de máquina e web pontos de extremidade do serviço de um experimento usando o PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
