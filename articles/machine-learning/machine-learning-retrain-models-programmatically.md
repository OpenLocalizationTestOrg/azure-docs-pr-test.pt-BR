---
title: "modelos de aprendizado de máquina do aaaRetrain programaticamente | Microsoft Docs"
description: "Saiba como tooprogrammatically treinar novamente um modelo e a atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Readaptar os modelos de Machine Learning de forma programática
Este passo a passo, você aprenderá como tooprogrammatically treinar novamente um serviço Web do Azure Machine Learning usando c# e hello serviço de execução de lote de aprendizado de máquina.

Depois de você ter retreinados modelo hello, Olá explicações passo a passo a seguir mostra como tooupdate Olá modelo em seu serviço web de previsão:

* Se você implantou um serviço da web clássico no portal de serviços de Web do aprendizado de máquina hello, consulte [treinar novamente um serviço da web clássico](machine-learning-retrain-a-classic-web-service.md). 
* Se você implantou um novo serviço da web, consulte [treinar novamente um novo serviço da web usando cmdlets de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).

Para obter uma visão geral de Olá processo de treinamento, consulte [treinar novamente um modelo de aprendizado de máquina](machine-learning-retrain-machine-learning-model.md).

Se você quiser toostart com seu novo Gerenciador de recursos do Azure baseada em serviço web, consulte [treinar novamente um serviço web de previsão existente](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Criar um teste de treinamento
Neste exemplo, você usará "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados adulto" exemplos de aprendizado de máquina do Microsoft Azure hello. 

experiência de saudação toocreate:

1. Entrar no tooMicrosoft estúdio de aprendizado de máquina do Azure. 
2. No hello canto inferior direito do painel de saudação, clique em **novo**.
3. Selecione Olá Microsoft Samples, 5 de exemplo.
4. experiência de saudação toorename, na parte superior de saudação da tela de experimento Olá, selecione o nome de teste de hello "exemplo 5: avaliar de treinamento, teste, para classificação binária: conjunto de dados somente para adultos".
5. Tipo de modelo de censo.
6. Na parte inferior de saudação da tela de experimento hello, clique em **executar**.
7. Clique em **Configurar o Serviço Web** e selecione **Readaptação do Serviço Web**. 

Veja a seguir de Olá experiência inicial de saudação.
   
   ![Experimento inicial.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Criar um Teste de Preditivo e publicar como um serviço Web
Em seguida, crie um Experimento Predicativo.

1. Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **previsão Web Service**. Isso economiza modelo hello como um modelo treinado e adiciona módulos do serviço web de entrada e saída. 
2. Clique em **Executar**. 
3. Depois de experiência de saudação concluiu a execução, clique em **implantar o serviço Web [clássico]** ou **implantar o serviço de Web [novo]**.

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Implantar a experiência de treinamento hello como um serviço da web de treinamento
tooretrain Olá treinado, você deve implantar a experiência de treinamento Olá criado como um serviço da web Retraining. Esse serviço da web precisa um *saída do serviço Web* módulo conectado toohello  *[treinar modelo] [ train-model]*  tooproduce capaz de toobe novo, de módulo modelos treinados.

1. experiência de treinamento de toohello tooreturn, ícone de experiências de saudação no painel esquerdo do hello clique experimento Olá chamado modelo de censo.  
2. Na caixa de pesquisa de itens de experiência de pesquisa hello, tipo de serviço da web. 
3. Arraste um *entrada de serviço Web* módulo no hello experiências de tela e conecte-se sua saída toohello *limpar dados ausentes* módulo.  Isso garante que os dados novos treinamentos seja processados Olá mesma maneira como os dados de treinamento original.
4. Arraste dois *saída do serviço web* módulos para Olá experimentar a tela. Conecte a saída de saudação do hello *treinar modelo* tooone e Olá saída de hello módulo *avaliar modelo* módulo toohello outros. Olá saída do serviço web para **treinar modelo** nos dá novo modelo treinado de saudação. Olá saída anexada muito**avaliar modelo** retorna a saída desse módulo, que é resultados de desempenho de saudação.
5. Clique em **Executar**. 

Em seguida, você deve implantar Olá experiência de treinamento como um serviço web que produz um modelo treinado e resultados de avaliação do modelo. tooaccomplish isso, o próximo conjunto de ações dependem se você estiver trabalhando com um serviço da web clássico ou um novo serviço web.  

**Serviço Web Clássico**

Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **implantar o serviço Web [clássico]**. Olá Web Service **painel** é exibido com a página de ajuda Olá chave de API e hello API para execução em lotes. Olá método de execução em lote pode ser usado para criar modelos treinados.

**Novo Serviço Web**

Na parte inferior de saudação da tela de experimento hello, clique em **configurar o serviço Web** e selecione **implantar o serviço de Web [novo]**. portal de serviços da Web de aprendizado de máquina do Web Service Azure Olá abre toohello página de serviço de web de implantação. Digite um nome para o serviço Web, escolha um plano de pagamento clique em **Implantar**. Olá método de execução de lote pode ser usado para criar modelos treinados

Em ambos os casos, após o teste foi concluído em execução, fluxo de trabalho resultante Olá se assemelhar ao seguinte:

![Fluxo de trabalho resultante após a execução.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Treinar novamente o modelo de saudação com novos dados usando BES
Neste exemplo, você está usando o c# toocreate Olá treinamento de aplicativo. Você também pode usar Olá Python ou tooaccomplish de código de exemplo R Esta tarefa.

toocall Olá APIs de treinamento:

1. Crie um aplicativo de console C# no Visual Studio: **Novo** > **Projeto** > **Visual C#** > **Área de Trabalho Clássica do Windows** > **Aplicativo de Console (.NET Framework)**.
2. Entrar toohello portal do serviço de Web de aprendizado de máquina.
3. Se você estiver trabalhando com um serviço Web Clássico, clique em **Serviços Web Clássicos**.
   1. Clique em Olá web service que você está trabalhando.
   2. Clique em ponto de extremidade saudação padrão.
   3. Clique em **Consumo**.
   4. Na parte inferior de saudação do hello **consumir** página Olá **código de exemplo** seção, clique em **lote**.
   5. Continue toostep 5 deste procedimento.
4. Se você estiver trabalhando com um Novo serviço Web, clique em **Serviços Web**.
   1. Clique em Olá web service que você está trabalhando.
   2. Clique em **Consumo**.
   3. Na parte inferior da saudação de Olá consumir da página Olá **código de exemplo** seção, clique em **lote**.
5. Copie Olá c# código de exemplo para execução em lotes e cole-o no arquivo Program.cs de hello, certificando-se de namespace Olá permanece intacto.

Adicione o pacote de Nuget Olá Microsoft.AspNet.WebApi.Client conforme especificado nos comentários de saudação. tooadd Olá referência tooMicrosoft.WindowsAzure.Storage.dll, talvez seja necessário primeiro biblioteca de cliente tooinstall Olá para serviços de armazenamento do Microsoft Azure. Para obter mais informações, consulte [Serviços de Armazenamento do Windows](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Atualizar a declaração de apikey Olá
Localizar Olá **apikey** declaração.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Em Olá **informações básicas de consumo** seção Olá **consumir** página, localize a chave primária hello e copiá-lo toohello **apikey** declaração.

### <a name="update-hello-azure-storage-information"></a>Atualizar informações de armazenamento do Azure Olá
Olá, código de exemplo do BES carrega um arquivo de um armazenamento de tooAzure de disco local (por exemplo "C:\temp\CensusIpnput.csv"), processa e grava tooAzure armazenamento do retorno de resultados de saudação.  

tooaccomplish nesta tarefa, você deve recuperar informações de contêiner, chave e nome de conta de armazenamento do Olá para sua conta de armazenamento do portal do Azure clássico de saudação e atualização Olá correspondente valores no código de saudação. 

1. Faça logon no portal do Azure clássico de toohello.
2. Na coluna de navegação à esquerda hello, clique em **armazenamento**.
3. Na lista de saudação de contas de armazenamento, selecione uma toostore saudação retreinados modelo.
4. Final Olá Olá página, clique em **gerenciar chaves de acesso**.
5. Copie e salve Olá **chave de acesso primária** e caixa de diálogo fechar hello. 
6. Na parte superior de saudação da página de saudação, clique em **contêineres**.
7. Selecione um contêiner existente ou crie um novo e salve o nome hello.

Localizar Olá *StorageAccountName*, *StorageAccountKey*, e *StorageContainerName* declarações e atualizar valores de saudação salvo do hello portal do Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Você também deve garantir o arquivo de entrada hello está disponível no local Olá especificado no código de saudação. 

### <a name="specify-hello-output-location"></a>Especifique o local de saída Olá
Ao especificar local de saída Olá Olá carga de solicitação, Olá a extensão do arquivo hello especificado na *RelativeLocation* devem ser especificados como ilearner. 

Consulte Olá exemplo a seguir:

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> nomes de saudação de seus locais de saída podem ser diferentes da saudação aqueles neste passo a passo com base na ordem de saudação em que você adicionou Olá módulos de saída de serviço de web. Como configurar esse teste de treinamento com duas saídas, resultados da saudação incluem informações de local de armazenamento para ambos.  
> 
> 

![Saída da readaptação][6]

Diagrama 4:Saída da readaptação.

## <a name="evaluate-hello-retraining-results"></a>Avaliar os resultados de treinamento Olá
Quando você executa o aplicativo hello, saída de hello inclui a URL de saudação e tooaccess necessário do token SAS Olá resultados da avaliação.

Você pode ver os resultados de desempenho de saudação do modelo Olá treinados novamente combinando Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída para *output2* (conforme mostrado no hello anterior de treinamento a imagem de saída) e colando URL completa Olá na barra de endereços do navegador hello.  

Examine Olá resultados toodetermine se Olá recentemente treinado executa também suficiente Olá tooreplace existente a um.

Saudação de cópia *BaseLocation*, *RelativeLocation*, e *SasBlobToken* Olá resultados de saída, você usará-los durante a saudação processo de treinamento.

## <a name="next-steps"></a>Próximas etapas
Se você implantou o serviço web de previsão de saudação clicando **implantar o serviço Web [clássico]**, consulte [treinar novamente um serviço da web clássico](machine-learning-retrain-a-classic-web-service.md).

Se você implantou o serviço web de previsão de saudação clicando **implantar o serviço de Web [novo]**, consulte [treinar novamente um novo serviço da web usando cmdlets de gerenciamento de aprendizado de máquina Olá](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
