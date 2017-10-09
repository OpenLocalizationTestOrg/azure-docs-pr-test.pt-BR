---
title: "aaaCreate vários modelos de um experimento | Microsoft Docs"
description: "Usar o PowerShell toocreate vários modelos de aprendizado de máquina e web pontos de extremidade de serviço com hello mesmo algoritmo, mas conjuntos de dados de treinamento diferentes."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Criar vários modelos do Machine Learning e pontos de extremidade de serviço Web com base em um teste usando o PowerShell
Este é um problema comum de aprendizado de máquina: deseja toocreate muitos modelos que têm Olá mesmo fluxo de trabalho de treinamento e use Olá mesmo algoritmo, mas têm conjuntos de dados de treinamento diferentes como entrada. Este artigo mostra como toodo isso em grande escala no estúdio de aprendizado de máquina do Azure usando apenas uma única experiência.

Por exemplo, digamos que você tenha um negócio de franquia mundial de aluguel de bicicletas. Você deseja toobuild uma demanda de aluguel regressão modelo toopredict Olá com base em dados históricos. Você tem 1.000 locais de aluguel em Olá, mundo e coletados um conjunto de dados para cada local que inclui recursos importantes, como data, hora, clima e tráfego local tooeach específico.

Você pode treinar seu modelo uma vez usando uma versão mesclada de todos os conjuntos de dados de saudação em todos os locais. Mas como cada um dos seus locais tem um ambiente exclusivo, uma abordagem melhor seria ser tootrain seu modelo de regressão separadamente usando o conjunto de dados Olá para cada local. Dessa forma, cada modelo treinado pode levar em tamanhos de armazenamento diferente do conta hello, volume, geografia, população, ambiente de tráfego de bicicleta amigável, *etc.*.

Que pode ser uma abordagem melhor hello, mas não desejar toocreate 1.000 experiências de treinamento no aprendizado de máquina do Azure com cada um representando um local exclusivo. Além de ser uma tarefa difícil, também é parece muito ineficiente, pois cada teste teria que todos os Olá mesmos componentes, exceto o conjunto de dados de treinamento de saudação.

Felizmente, é possível fazer isso usando Olá [treinamento API de aprendizado de máquina do Azure](machine-learning-retrain-models-programmatically.md) e automatizar tarefas de saudação com [PowerShell de aprendizado de máquina do Azure](machine-learning-powershell-module.md).

> [!NOTE]
> toomake nossa amostra executado mais rapidamente, podemos será reduzir o número de Olá dos locais de too10 1.000. Mas hello mesmos princípios e procedimentos se aplicam too1, 000 locais. Olá única diferença é que se você quiser tootrain de 1.000 conjuntos de dados provavelmente deseja toothink da execução Olá scripts do PowerShell em paralelo a seguir. Como toodo está além do escopo de saudação neste artigo, mas você pode encontrar exemplos do PowerShell multi-thread na saudação da Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Configurar a experiência de treinamento Olá
Vamos toouse um exemplo [experiência de treinamento](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que já criamos em Olá [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Abra esse teste em seu espaço de trabalho do [Azure Machine Learning Studio](https://studio.azureml.net) .

> [!NOTE]
> Ordem toofollow junto com este exemplo, convém toouse um espaço de trabalho padrão em vez de um espaço de trabalho grátis. Podemos criará um ponto de extremidade para cada cliente - para um total de 10 pontos de extremidade - e isso, é necessário um espaço de trabalho padrão como um espaço de trabalho gratuito é limitada too3 pontos de extremidade. Se você tiver apenas um espaço de trabalho grátis, modifique os scripts de saudação abaixo tooallow para apenas 3 locais apenas.
> 
> 

experiência de saudação usa um **importar dados** conjunto de dados de treinamento do módulo tooimport Olá *customer001.csv* de uma conta de armazenamento do Azure. Vamos supor que temos coletados conjuntos de dados de treinamento de todos os locais de aluguel de bicicleta e armazenou em Olá mesmo local de armazenamento de blob com nomes de arquivo que variam de *rentalloc001.csv* muito*rentalloc10.csv* .

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Observe que uma **saída do serviço Web** módulo foi adicionado toohello **treinar modelo** módulo.
Quando esse teste é implantado como um serviço web, o ponto de extremidade de saudação associado a essa saída retornará treinado Olá no formato de saudação de um arquivo de .ilearner.

Observe também que configuramos um parâmetro de serviço da web para a URL de saudação que Olá **importar dados** módulo usa. Isso nos permite toouse Olá parâmetro toospecify individuais conjuntos de dados tootrain Olá modelo de treinamento para cada local.
Existem outras maneiras poderíamos ter feito isso, como usando uma consulta SQL com um web serviço parâmetro tooget os dados de um banco de dados do SQL Azure, ou simplesmente um **entrada de serviço Web** toopass de módulo em um conjunto de dados toohello de serviço da web.

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Agora, vamos executar esse teste de treinamento usando o valor padrão de saudação *rental001.csv* como Olá conjunto de dados de treinamento. Se você exibir saída Olá Olá **avaliar** módulo (clique em saída hello e selecione **visualizar**), você pode ver, obtemos um desempenho razoável de *AUC* = 0.91. Neste ponto, estamos pronto toodeploy um serviço web sem esse teste de treinamento.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Implantar serviços web de classificação e treinamento Olá
Olá toodeploy treinamento de serviço da web, clique em Olá **configurar o serviço Web** abaixo da tela de experimento hello e selecione **implantar o serviço da Web**. Chame esse serviço Web de “Treinamento do Aluguel de Bicicletas”.

Agora precisamos de serviço de web toodeploy Olá pontuação.
toodo, clicamos **configurar o serviço Web** abaixo Olá tela e selecione **previsão Web Service**. Isso criará um teste de pontuação.
Vamos precisar toomake alguns toomake pequenos ajustes ele funciona como um serviço web, tais como dados de entrada a remoção de coluna de rótulo hello "cnt" hello e limitar Olá correspondente e o id da instância Olá Olá saída tooonly previu o valor.

toosave que trabalhar, basta abrir Olá [experimento previsão](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) em Olá Galeria já foi preparado.

serviço de web hello toodeploy, executar teste de previsão hello, clique em Olá **implantar o serviço da Web** botão abaixo tela hello. Saudação de nome serviço web "Bicicleta aluguel de pontuação" de pontuação ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Criar 10 pontos de extremidade de serviço Web idênticos com o PowerShell
Este serviço Web é fornecido com um ponto de extremidade padrão. Mas não estamos tão interessados no ponto de extremidade saudação padrão porque ele não pode ser atualizado. O que devemos toodo é toocreate 10 pontos de extremidade adicionais, uma para cada local. Faremos isso com o PowerShell.

Primeiro, configuramos nosso ambiente do PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Em seguida, execute Olá comando PowerShell a seguir:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Agora, criamos 10 pontos de extremidade e contiverem Olá mesmo modelo treinado treinado em *customer001.csv*. Você pode exibi-los no Portal de gerenciamento de saudação.

![imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Atualizar Olá pontos de extremidade toouse treinamento separado conjuntos de dados usando o PowerShell
Olá próxima etapa é tooupdate pontos de extremidade de saudação com modelos treinados exclusivamente nos dados de cada cliente individual. Mas primeiro é preciso tooproduce esses modelos de saudação **treinamento de aluguel de bicicleta** serviço web. Vamos voltar toohello **treinamento de aluguel de bicicleta** serviço web. Precisamos toocall seu ponto de extremidade do BES 10 vezes com 10 conjuntos de dados de treinamento diferentes em modelos diferentes de tooproduce 10 de ordem. Vamos usar Olá **InovkeAmlWebServiceBESEndpoint** toodo de cmdlet do PowerShell isso.

Você também precisará de credenciais tooprovide para sua conta de armazenamento de blob em `$configContent`, ou seja, os campos de saudação `AccountName`, `AccountKey` e `RelativeLocation`. Olá `AccountName` pode ser um dos seus nomes de conta, como visto no hello **Portal de gerenciamento clássico do Azure** (*armazenamento* guia). Depois que você clicar em uma conta de armazenamento, seu `AccountKey` podem ser encontrados ao pressionar Olá **gerenciar chaves de acesso** botão inferior hello e copiando Olá *chave de acesso primário*. Olá `RelativeLocation` é Olá caminho relativo tooyour armazenamento onde um novo modelo será armazenado. Por exemplo, o caminho Olá `hai/retrain/bike_rental/` no script hello abaixo pontos tooa contêiner nomeado `hai`, e `/retrain/bike_rental/` são subpastas. Atualmente, não é possível criar subpastas por meio da interface do usuário do portal hello, mas há [vários gerenciadores de armazenamento do Azure](../storage/common/storage-explorers.md) que permitem que você toodo assim. É recomendável que você crie um novo contêiner no seu Olá toostore de armazenamento novos modelos treinados (arquivos .ilearner) da seguinte maneira: sua página de armazenamento, clique em Olá **adicionar** botão na parte inferior do hello e nomeie-o `retrain`. Em resumo, o script do toohello alterações necessárias Olá abaixo pertencem muito`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> Olá ponto de extremidade do BES é Olá só tem suporte modo para esta operação. O RRS não pode ser usado para a produção de modelos treinados.
> 
> 

Como você pode ver acima, em vez de criar 10 diferentes BES trabalho json arquivos de configuração, criamos dinamicamente cadeia de caracteres de configuração de saudação em vez disso e inseri-la toohello *jobConfigString* parâmetro hello  **InvokeAmlWebServceBESEndpoint** cmdlet, porque não há realmente nenhum tookeep da necessidade de uma cópia em disco.

Se tudo correr bem, após alguns instantes verá 10 arquivos .ilearner, de *model001.ilearner* muito*model010.ilearner*, em sua conta de armazenamento do Azure. Agora estamos pronto tooupdate nosso 10 da web de pontuação pontos de extremidade de serviço com esses modelos usando Olá **AmlWebServiceEndpoint Patch** cmdlet do PowerShell. Lembre-se novamente de que podemos pode patch apenas pontos de extremidade não padrão Olá que programaticamente criamos anteriormente.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

Isso deverá ser executado rapidamente. Ao término da execução de hello, podemos será criou com êxito pontos de extremidade de serviço de web de previsão 10, cada uma contendo um modelo treinado exclusivamente treinado em Olá conjunto de dados específico tooa aluguel local, tudo a partir de uma experiência de treinamento único. tooverify isso, você pode tentar chamar esses pontos de extremidade usando Olá **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornecendo a eles com hello mesmo dados de entrada e você deve esperar resultados de previsão diferentes toosee como modelos de saudação são treinado com conjuntos de treinamento diferentes.

## <a name="full-powershell-script"></a>Script completo do PowerShell
Aqui está uma listagem de saudação do código-fonte completo hello:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
