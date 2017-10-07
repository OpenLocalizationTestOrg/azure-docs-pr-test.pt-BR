---
title: "Olá de aaaTen coisas que você pode fazer na máquina de Virtual de ciência de dados | Microsoft Docs"
description: "Execute várias exploração de dados e tarefas de modelagem em ciência de dados Olá Máquina Virtual."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Dez coisas que você pode fazer na ciência de dados Olá Máquina Virtual
saudação de máquina Virtual de ciência de dados da Microsoft (DSVM) é um ambiente de desenvolvimento de ciência de dados avançados que permite que você tooperform várias tarefas de modelagem e exploração de dados. Olá ambiente vem já construído e agrupado com dados populares várias ferramentas de análise que tornam mais fácil tooget familiarizar rapidamente com a análise para local, de nuvem ou híbrida implantações. Olá DSVM trabalha em conjunto com muitos serviços do Azure e é capaz de tooread e processar os dados que já esteja armazenados no Azure, no Azure SQL Data Warehouse, o Azure Data Lake, o armazenamento do Azure ou no banco de dados do Azure Cosmos. Ela também aproveita outras ferramentas de análise, como o Azure Machine Learning e o Azure Data Factory.

Neste artigo, mostrarei como toouse tooperform sua DSVM ciência de dados de várias tarefas e interagir com outros serviços do Azure. Aqui estão algumas das coisas Olá que você pode fazer no hello DSVM:

1. Explorar dados e desenvolver modelos localmente em Olá DSVM usando o Microsoft R Server, Python
2. Usar um tooexperiment de notebook Jupyter com seus dados em um navegador usando uma versão pronta enterprise do R criado para escalabilidade e desempenho de Python 2, 3 de Python, Microsoft R
3. Operacionalizar modelos criados usando R e Python no Azure Machine Learning para que os aplicativos cliente possam acessar seus modelos usando uma interface simples de serviços Web
4. Administrar os recursos do Azure usando o portal do Azure ou o Powershell
5. Estender o espaço de armazenamento e compartilhar conjuntos de dados/códigos em grande escala com toda sua equipe criando um armazenamento de Arquivos do Azure como uma unidade montável na DSVM
6. Compartilhar código com sua equipe usando GitHub e acessar o repositório usando Olá pré-instalados Git clientes - Git Bash GUI do Git.
7. Acessar vários serviços de análise e dados do Azure, como armazenamento de blobs do Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, SQL Data Warehouse do Azure e bancos de dados
8. Criar relatórios e painel usando Olá pré-instalado Olá DSVM do Power BI Desktop e implantá-los na nuvem Olá
9. Dimensionar dinamicamente seu toomeet DSVM que precisa de seu projeto
10. Instalar ferramentas adicionais na sua máquina virtual   

> [!NOTE]
> Encargos de uso adicionais se aplicam para muitos dos produtos de serviços de armazenamento e análise de dados adicionais hello listados neste artigo. Consulte toohello [preços do Azure](https://azure.microsoft.com/pricing/) página para obter detalhes.
> 
> 

**Pré-requisitos**

* É necessária uma assinatura do Azure. Você pode se inscrever para uma avaliação gratuita [aqui](https://azure.microsoft.com/free/).
* Instruções para o provisionamento de uma máquina Virtual de ciência de dados Olá portal do Azure estão disponíveis em [criar uma máquina virtual](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Explorar dados e desenvolver modelos usando o Microsoft R Server ou Python
Você pode usar linguagens como R e Python toodo sua análise de dados à direita na Olá DSVM.

Para R, você pode usar um IDE chamado "Revolution R Enterprise 8.0" que pode ser encontrado no menu de início de saudação ou área de trabalho de saudação. A Microsoft forneceu bibliotecas adicionais sobre os Olá abrir tooenable de fonte/CRAN-R escalonáveis análise e hello capacidade tooanalyze dados maior do que o tamanho da memória Olá permitido ao fazer a análise em paralelo. Você também pode instalar um IDE do R que quiser, por exemplo, [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Para Python, você pode usar um IDE como Visual Studio Community Edition que tem Olá ferramentas Python para a extensão do Visual Studio (PTVS) pré-instalado. Por padrão, somente um Python 2.7 básico está configurado no PTVS (sem nenhuma biblioteca de análise como SciKit, Pandas). Em ordem tooenable Anaconda Python 2.7 e 3.5, você precisa fazer toodo Olá seguinte:

* Criar ambientes personalizados para cada versão navegando muito**ferramentas** -> **ferramentas Python** -> **Python ambientes** e, em seguida, clicando em " **+ Personalizado**"em Olá Visual Studio 2015 Community Edition
* Forneça uma descrição e definir caminhos de prefixo, como o ambiente de saudação *c:\anaconda* Anaconda Python 2.7 ou *c:\anaconda\envs\py35* Anaconda Python 3.5
* Clique em **detecção automática** e **aplicar** toosave ambiente de saudação.

É aqui que configuração de ambiente personalizado Olá aparência no Visual Studio.

![Configuração do PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Consulte Olá [documentação PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para obter detalhes adicionais sobre como toocreate ambientes de Python.

Agora você está pronto toocreate um novo projeto de Python. Navegue muito**arquivo** -> **novo** -> **projeto** -> **Python** e selecione o tipo de saudação do Você está criando um aplicativo de Python. Você pode definir o ambiente de Python Olá Olá projeto toohello desejado versão atual (Anaconda 2.7 ou 3.5): Olá do botão direito do mouse **ambiente Python**, selecione **Adicionar/remover Python ambientes**, e em seguida, selecione Olá desejado ambiente tooassociate com projeto hello. Você pode encontrar mais informações sobre como trabalhar com PTVS no produto Olá [documentação](https://github.com/Microsoft/PTVS/wiki) página.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Usando um modelo e anotações do Jupyter tooexplore seus dados com Python ou R
saudação de anotações do Jupyter é um ambiente poderoso que fornece um baseado em navegador "IDE" para modelagem e exploração de dados. Você pode usar o Python 2, 3 de Python ou R (código-fonte aberto e Olá Microsoft R Server) em um bloco de anotações do Jupyter.

Olá toolaunch Jupyter Notebook clique no ícone do menu Iniciar Olá / ícone da área de trabalho denominada **Jupyter Notebook**. Em Olá DSVM você também pode procurar muito "https://localhost:9999 /" tooaccess Olá Jupiter Notebook. Se ele solicitará a senha, use instruções fornecidas na Olá ***como toocreate uma senha forte no servidor de notebook Jupyter Olá*** seção Olá [Olá provisionar máquina de Virtual de ciência de dados da Microsoft](machine-learning-data-science-provision-vm.md)toocreate de tópico de anotações do Jupyter uma senha forte tooaccess hello. 

Depois de abrir o bloco de anotações hello, você deverá ver um diretório que contém alguns blocos de anotações de exemplo que são predefinidos no hello DSVM. Agora você pode:

* Clique no código de Olá Olá notebook toosee.
* executar cada célula pressionando **SHIFT-ENTER**.
* Execute o bloco de anotações inteiro Olá clicando no **célula** -> **executar**
* Crie um novo bloco clicando na Olá Jupyter ícone (canto superior esquerdo) e, em seguida, clicando em **novo** botão hello à direita e, em seguida, escolher o idioma de bloco de anotações de saudação (também conhecido como kernels).   

> [!NOTE]
> Atualmente suportamos Python 2.7, kernel de saudação R 3.5 Python e R. dá suporte à programação no R de software livre como enterprise Olá escalonável Microsoft R Server.   
> 
> 

Quando estiver no bloco de anotações de saudação pode explorar seus dados, criar modelo hello, testar Olá modelo usando a opção de bibliotecas.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Compilar os modelos usando R e Python e operacionalizá-los usando o Machine Learning do Azure
Quando você tiver criado e validado a próxima etapa do modelo Olá geralmente é toodeploy-lo em produção. Isso permite que o cliente de previsões de modelo aplicativos tooinvoke Olá em um tempo real ou em uma base de modo de lote. O aprendizado de máquina do Azure fornece um mecanismo toooperationalize um modelo incorporado em R ou Python.

Quando você colocar o modelo no aprendizado de máquina do Azure, um serviço web é exposto que permite que os clientes toomake chamadas REST que passam parâmetros de entrada e receber previsões do modelo hello como saídas.   

> [!NOTE]
> Se você não ainda inscreveram para o aprendizado de máquina do Azure, você pode obter um espaço de trabalho livre ou um espaço de trabalho padrão visitando Olá [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/) home page e clicar em "Introdução".   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Compilar e operacionalizar modelos em Python
Aqui está um trecho de código desenvolvido em um bloco de anotações do Jupyter de Python cria um modelo simple usando Olá Saiba SciKit biblioteca.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

método Hello usado toodeploy seu modelos de python tooAzure aprendizado de máquina encapsula Olá previsão do modelo de saudação em uma função e decora-lo com os atributos fornecidos pela biblioteca de python de aprendizado de máquina do Azure pré-instalado Olá que indicam sua máquina do Azure ID do espaço de trabalho de aprendizado, chave de API e saudação de entrada e retornam parâmetros.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Um cliente pode agora fazer chamadas toohello web service. Existem wrappers de conveniência que constroem Olá solicitações da API REST. Aqui está um exemplo código tooconsume Olá web de serviço.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> biblioteca de aprendizado de máquina do Azure Olá só tem suporte em Python 2.7 no momento.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Criar e operacionalizar modelos R
Você pode implantar os modelos de R criados no hello máquina de Virtual de ciência de dados ou em outro lugar no aprendizado de máquina do Azure de forma que seja semelhante toohow que é feito para Python. O hello etapas:

* Crie um tooprovide de arquivo settings.json a ID do espaço de trabalho e a autenticação de token conforme Olá exemplo de código a seguir.
* grave um wrapper para a função de previsão do modelo de saudação.
* chamar ```publishWebService``` em Olá toopass de biblioteca de aprendizado de máquina do Azure no wrapper de função hello.  

Aqui está a saudação procedimento e trechos de código que podem ser usado tooset up, criar, publicar e consumir um modelo como um serviço web no aprendizado de máquina do Azure.

#### <a name="setup"></a>Configuração
1. Instalar o pacote de R de aprendizado de máquina Olá digitando ```install.packages("AzureML")``` no IDE do Revolution R Enterprise 8.0 ou seu IDE de R.
2. Baixe o RTools [daqui](https://cran.r-project.org/bin/windows/Rtools/). Você precisa Olá zip utilitário no caminho de saudação (e nomeado zip.exe) toooperationalize seu pacote de R no aprendizado de máquina.
3. Criar um arquivo settings.json em um diretório chamado ```.azureml``` em seu diretório base e insira parâmetros de saudação do seu espaço de trabalho do aprendizado de máquina do Azure:

Estrutura do arquivo settings.json:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Compilar um modelo em R e publicá-lo no Azure Machine Learning
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Consumir Olá modelo implantado no aprendizado de máquina do Azure
tooconsume o modelo de saudação de um aplicativo cliente, usamos Olá toolook de biblioteca de aprendizado de máquina do Azure backup Olá publicado o serviço web por nome usando Olá `services` ponto de extremidade Olá toodetermine de chamada de API. Em seguida, você simplesmente chama hello `consume` de função e passar Olá toobe de quadro de dados previsto.
saudação de código a seguir é o modelo de saudação de tooconsume usado publicado como um serviço web de aprendizado de máquina do Azure.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Para obter mais informações sobre a biblioteca de R de aprendizado de máquina do Azure Olá podem ser encontradas [aqui](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Administrar os recursos do Azure usando o portal do Azure ou o Powershell
Olá DSVM não só permite que você toobuild sua solução de análise localmente no Olá a máquina virtual, mas também permite que você tooaccess serviços em nuvem do Azure da Microsoft. O Azure fornece vários serviços de análise de dados, armazenamento e computação, além de outros serviços que você pode administrar e acessar da DSVM.

tooadminister seus recursos de assinatura e na nuvem do Azure, você pode usar o navegador e o ponto toothe [portal do Azure](https://portal.azure.com). Você também pode usar o Azure Powershell tooadminister sua assinatura do Azure e seus recursos por meio de um script.
Você pode executar o Powershell do Azure de um atalho na área de trabalho de saudação ou de saudação iniciar menu intitulada "Microsoft Azure Powershell". Consulte a [documentação do Microsoft Azure Powershell](../powershell-azure-resource-manager.md) para obter mais informações sobre como você pode administrar seus recursos e assinatura do Azure usando os scripts do Windows Powershell.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Estender o espaço de armazenamento com um sistema de arquivos compartilhado
Os cientistas de dados podem compartilhar grandes conjuntos de dados, código ou outros recursos em equipe hello. Olá DSVM em si tem cerca de 70GB de espaço disponível. tooextend seu armazenamento, você pode usar o hello Azure File Service e montá-lo em Olá DSVM ou acessá-lo por meio de uma API REST.   

> [!NOTE]
> máximo de espaço de compartilhamento do Azure File Service Olá Olá é 5TB e limite de tamanho de arquivo individual é 1TB.   
> 
> 

Você pode usar o Azure Powershell toocreate um compartilhamento de serviço de arquivo do Azure. Aqui está o hello script toorun no Azure PowerShell toocreate um compartilhamento de serviço de arquivo do Azure.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Agora que você criou um compartilhamento de arquivos do Azure, é possível montá-lo em qualquer máquina virtual no Azure. É altamente recomendável que Olá VM está no mesmo data center do Azure como latência de tooavoid de conta de armazenamento hello e dados de encargos de transferência. Aqui estão as unidade de Olá Olá comandos toomount em Olá DSVM que pode ser executado no Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Agora você pode acessar essa unidade como faria com qualquer unidade normal Olá VM.

## <a name="6-share-code-with-your-team-using-github"></a>6. Compartilhar código com sua equipe usando o GitHub
O GitHub é um repositório de código onde você pode encontrar muitas fontes e código de exemplo para diferentes ferramentas usando diversas tecnologias compartilhadas pela comunidade de desenvolvedores de saudação. Ele usa o Git como Olá versões tootrack e repositório de tecnologia Olá de arquivos de código. O GitHub é também uma plataforma de onde você pode criar seu próprio repositório toostore código compartilhado e a documentação da sua equipe implementar o controle de versão e também controlar quem tem acesso tooview e colaboração de código. Visite Olá [páginas de Ajuda do GitHub](https://help.github.com/) para obter mais informações sobre como usar o Git. Você pode usar GitHub como uma saudação maneiras toocollaborate com sua equipe, em seguida, use o código desenvolvido pela comunidade Olá e colaboração da comunidade do código toohello back.

Olá DSVM já vem carregado com ferramentas de cliente em linha de comando como bem GUI tooaccess repositório GitHub. Olá ferramenta de linha de comando toowork com Git e GitHub é chamado de Git Bash. Visual Studio instalado Olá DSVM tem extensões de Git hello. Você pode encontrar ícones de inicialização para essas ferramentas no menu de início do hello e área de trabalho de saudação.

código de toodownload de um repositório GitHub é usar Olá ```git clone``` comando. Por exemplo repositório de ciência de dados toodownload publicado pela Microsoft no diretório atual Olá você pode executar Olá comando a seguir quando estiver no ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

No Visual Studio, você pode fazer Olá a mesma operação de clonagem. Olá captura de tela a seguir mostra como tooaccess Git e GitHub ferramentas no Visual Studio.

![Git no Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Você pode encontrar mais informações sobre como usar o Git toowork com o repositório do GitHub de vários recursos disponíveis em github.com. Olá [roteiro](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) é uma referência útil.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Acessar vários serviços de análise e dados do Azure
### <a name="azure-blob"></a>Blob do Azure
O blob do Azure é um armazenamento em nuvem confiável e econômico para pequenos e grandes volumes de dados. Vamos dar uma olhada em como você pode mover dados tooAzure Blob e acessar dados armazenados em um Blob do Azure.

**Pré-requisito**

* **Crie sua conta de Armazenamento de Blobs do Azure no [portal do Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Confirmar essa ferramenta de linha de comando pré-instalados AzCopy do hello é encontrada em ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Ao executar essa ferramenta, você pode adicionar Olá contendo Olá azcopy.exe tooyour caminho ambiente tooavoid variável digitando Olá completo comando caminho do diretório. Para obter mais informações sobre a ferramenta AzCopy, consulte muito[AzCopy documentação](../storage/common/storage-use-azcopy.md)
* Inicie a ferramenta de Gerenciador de armazenamento do Azure de saudação. Ele pode ser baixado em [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Mover dados de VM tooAzure Blob: AzCopy**

dados de toomove entre seus arquivos locais e o armazenamento de blob, você pode usar o AzCopy na linha de comando ou o PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Substituir **C:\myfolder** toohello caminho onde o arquivo está armazenado, **mystorageaccount** nome de conta de armazenamento de blob tooyour, **mycontainer** toohello o nome do contêiner, **chave da conta de armazenamento** tooyour chave de acesso de armazenamento de blob. Você pode encontrar as credenciais da conta de armazenamento no [portal do Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Execute o comando AzCopy no PowerShell ou em um prompt de comando. Veja um exemplo de uso do comando AzCopy:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Depois que você executar o tooan de toocopy AzCopy comando BLOBs do Azure, consulte o arquivo aparece no Gerenciador de armazenamento do Azure em breve.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Mover dados de VM tooAzure Blob: Azure Storage Explorer**

Você também pode carregar dados de arquivo local Olá em sua VM usando o Gerenciador de armazenamento do Azure:

* contêiner de tooa tooupload dados, selecione Olá Olá de contêiner e clique em do destino **carregar** botão.![ Carregar no Gerenciador de armazenamento](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Clique em Olá **...**  toohello direito da saudação **arquivos** caixa, selecione um ou vários tooupload de arquivos do sistema de arquivos hello e clique em **carregar** toobegin carregando arquivos hello.![ Carregar arquivos tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Ler dados de Blobs do Azure: módulo de leitor do Machine Learning**

No estúdio de aprendizado de máquina do Azure, você pode usar um **módulo de importação de dados** tooread dados do seu blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Ler dados do Blob do Azure: ODBC do Python**

Você pode usar **BlobService** dados da biblioteca tooread diretamente do blob em um programa de anotações do Jupyter ou Python.

Primeiro, importe os pacotes necessários:

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Em seguida, conecte suas credenciais de conta do Blob do Azure e leia os dados no Blob:

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

dados de saudação é lido em um quadro de dados:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
O Armazenamento do Azure Data Lake é um repositório de grande escala para cargas de trabalho de análise de big data e é compatível com HDFS (Hadoop Distributed File System). Ele funciona com o ecossistema de Hadoop hello e Olá análise Azure Data Lake. Vamos mostrar como você pode mover dados para Olá repositório Azure Data Lake e executar análise usando a análise do Azure Data Lake.

**Pré-requisito**

* Crie seu Azure Data Lake Analytics no [portal do Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Olá **ferramentas do Azure Data Lake** na **Visual Studio** encontrada nesse [link](https://www.microsoft.com/download/details.aspx?id=49504) já está instalado no Visual Studio Community Edition que está na máquina virtual de saudação do hello. Depois de iniciar o Visual Studio e log em sua assinatura do Azure, você verá a sua conta de análise de dados do Azure e armazenamento no painel esquerdo de saudação do Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Mover dados de VM tooData Lake: Azure Data Lake Explorer**

Você pode usar **Azure Data Lake Explorer** dados tooupload de arquivos locais de saudação em seu armazenamento de máquina Virtual tooData Lake.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

Você também pode criar um tooproductionize de pipeline de dados o tooor de movimentação de dados do Azure Data Lake usando Olá [Factory(ADF) de dados do Azure](https://azure.microsoft.com/services/data-factory/). Nós nos referimos toothis [artigo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide você por meio de dados de saudação do hello etapas toobuild pipelines.

**Ler dados do Azure Blob tooData Lake: U-SQL**

Se os dados residirem no Armazenamento de Blobs, você poderá lê-los diretamente no blob do armazenamento do Azure na consulta U-SQL. Antes de escrever a consulta U-SQL, certifique-se de que sua conta de armazenamento de blob é tooyour vinculado do Azure Data Lake. Vá muito**portal do Azure**, localizar seu painel de análise do Azure Data Lake, clique em **adicionar fonte de dados**, selecione o tipo de armazenamento muito**armazenamento do Azure** e conecte o armazenamento do Azure Nome da conta e chave. Você estará tooreference capaz de dados de saudação armazenados na conta de armazenamento hello.

![Insira a conta de armazenamento e a chave](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

No Visual Studio, você pode ler dados de armazenamento de blob, que algumas manipulação de dados, a engenharia de recurso e a saída Olá resultante dados tooeither Azure Data Lake ou o armazenamento de BLOBs do Azure. Ao fazer referência a dados Olá no armazenamento de blob, use **wasb: / /**; quando você faz referência a dados hello Azure Data Lake, use **swbhdfs: / /**

![Quadro de dados](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Você pode usar o hello consultas U-SQL no Visual Studio a seguir:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Depois de sua consulta é enviada toohello server, um diagrama que mostra o status de saudação do seu trabalho será exibido.

![Diagrama de status do trabalho](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Dados da consulta no Data Lake: U-SQL**

Depois que o dataset Olá é incluído no Azure Data Lake, você pode usar [linguagem U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery e explorar dados saudação. Linguagem U-SQL é tooT-SQL semelhante, mas combina alguns recursos do c# para que os usuários possam gravar módulos personalizados, funções definidas pelo usuário e etc. Você pode usar scripts de saudação na etapa anterior hello.

Após a consulta Olá tooserver enviado, tripdata_summary. CSV pode ser encontrado em breve **Azure Data Lake Explorer**, você pode visualizar dados de saudação pelo arquivo de saudação do botão direito do mouse.

![Arquivo no Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

informações do arquivo hello toosee:

![Resumo do arquivo](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Clusters HDInsight Hadoop
HDInsight do Azure é um serviço gerenciado de Apache Hadoop, Spark, HBase e Storm na nuvem hello. Você pode trabalhar facilmente com clusters de HDInsight do Azure de saudação máquina de virtual de ciência de dados.

**Pré-requisito**

* Crie sua conta de Armazenamento de Blobs do Azure no [portal do Azure](https://portal.azure.com). Esta conta de armazenamento é dados toostore usada para clusters de HDInsight.

![Criar uma conta de Armazenamento de Blobs do Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Personalize os Clusters do Azure HDInsight Hadoop no [portal do Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Você deve vincular a conta de armazenamento Olá criada com o cluster HDInsight quando ele é criado. Esta conta de armazenamento é usada para acessar os dados que podem ser processados em cluster hello.

![Vincular toostorage conta criada com o cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Você deve habilitar **acesso remoto** toohello o nó principal do cluster Olá depois que ele é criado. Lembre-se de credenciais de acesso remoto Olá você especificar aqui (diferentes das especificadas para cluster Olá em sua criação): necessário no procedimento subsequente hello.

![Habilitar o acesso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Criar um Espaço de Trabalho do Azure Machine Learning. Seus Testes de Machine Learning são armazenados neste espaço de trabalho do Machine Learning. Selecione opções de saudação realçada no Portal, conforme mostrado na Olá captura de tela a seguir:

![Criar um espaço de trabalho de Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Em seguida, digite os parâmetros de saudação do seu espaço de trabalho

![Insira os parâmetros do Espaço de Trabalho do Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Carregue os dados usando o IPython Notebook. Primeiro importar pacotes necessários, plug-in de credenciais, crie um banco de dados em sua conta de armazenamento e dados tooHDI clusters de carga.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* Como alternativa, você pode seguir esta [passo a passo](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster do táxi NYC dados tooHDI. As principais etapas incluem:
  
  * AzCopy: download compactado CSV na pasta local do blob público tooyour
  * AzCopy: carregar descompactado CSV do cluster de tooHDI de pasta local
  * Faça logon no nó principal de saudação do cluster de Hadoop e preparar para análise de dados exploratório

Após dados saudação cluster tooHDI carregado, você pode verificar seus dados no Gerenciador de armazenamento do Azure. Um banco de dados nyctaxidb é criado no cluster HDI.

**Exploração de dados: consultas Hive no Python**

Como dados de saudação são em cluster Hadoop, você pode usar o hello pyodbc pacote tooconnect tooHadoop Clusters e banco de dados de consulta usando Hive toodo exploração e engenharia de recurso. Você pode exibir as tabelas existentes Olá criada na etapa de pré-requisito hello.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Exibir tabelas existentes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Vamos dar uma olhada no número de saudação de registros em cada mês e hello o frequências de Oblíquo ou não na tabela de viagem de saudação:

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Gráfico do número de registros a cada mês](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Gráfico das frequências de dicas](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

Podemos também distância Olá entre o local de recebimento e o local de redução de computação e, em seguida, compare-toohello trip distância.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabela de coleta e entrega](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Plotagem de distância de tootrip de distância de entrega/redução](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Agora, vamos preparar uma conjunto reduzido de dados (1%) para modelagem. Podemos usar esses dados no módulo de leitor do Machine Learning.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Após alguns instantes, você pode ver dados saudação foi carregados em clusters de Hadoop:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabela de dados](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Ler dados do HDI usando o Machine Learning: módulo de leitor**

Você também pode usar o hello **leitor** módulo no banco de dados do estúdio de aprendizado de máquina tooaccess Olá no cluster Hadoop. Plug-in credenciais Olá seus clusters de HDI e conta de armazenamento do Azure tooenable criar modelos usando o banco de dados em clusters HDI do aprendizado de máquina usando o.

![Propriedades do módulo de leitor](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Olá conjunto de dados pode ser exibido:

![Exibir o conjunto de dados pontuado](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL Data Warehouse e bancos de dados
O SQL Data Warehouse do Azure é um data warehouse elástico como um serviço, com experiência em SQL Server de nível corporativo.

Você pode provisionar o SQL Data Warehouse do Azure seguindo Olá instruções fornecidas neste [artigo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Depois de provisionar o SQL Data Warehouse do Azure, você pode usar isso [passo a passo](machine-learning-data-science-process-sqldw-walkthrough.md) toodo para carregar dados, exploração e modelagem de dados dentro de saudação do SQL Data Warehouse.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Banco de dados do Azure Cosmos é um banco de dados NoSQL na nuvem hello. Ele permite que você toowork com documentos como JSON e permite que os documentos de saudação toostore e consulta.

Você precisa de saudação toodo seguir por requisitos etapas tooaccess Azure Cosmos DB de saudação DSVM.

1. Instalar o SDK do Python para DocumentDB (Execute ```pip install pydocumentdb``` no prompt de comando)
2. Criar uma conta do Azure Cosmos DB e um banco de dados no [Portal do Azure](https://portal.azure.com)
3. Baixar "Ferramenta de migração de banco de dados do Azure Cosmos" de [aqui](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) e extrair tooa diretório de sua escolha
4. Importar dados JSON (dados vulcões) armazenados em um [blob público](https://cahandson.blob.core.windows.net/samples/volcano.json) no banco de dados do Cosmos com o seguinte comando parâmetros toohello ferramenta de migração (dtui.exe do diretório Olá onde você instalou Olá, ferramenta de migração de banco de dados do Cosmos). Insira o local de origem e destino de saudação com estes parâmetros:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

Quando você importa dados hello, você pode ir tooJupyter e notebook Olá abrir intitulada *DocumentDBSample* que contém o python tooaccess documentos de código e fazer algumas consultas básicas. Você pode aprender mais sobre o banco de dados do Cosmos visitando o serviço Olá [página de documentação](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Criar relatórios e painel usando Olá Power BI Desktop
Vamos visualize arquivos de JSON vulcões Olá que vimos no hello precedem Cosmos banco de dados de exemplo em informações visuais do Power BI toogain nos dados de saudação. Etapas detalhadas estão disponíveis no hello [artigo do Power BI](../cosmos-db/powerbi-visualize.md). Aqui estão as etapas de alto nível hello:

1. Abra o Power BI Desktop e execute "Obter Dados". Especifique a URL hello como: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Você deve ver os registros JSON de saudação importados como uma lista
3. Converter a tabela de tooa de lista de saudação para que Power BI possa trabalhar com hello mesmo
4. Expanda colunas Olá clicando em Olá expanda ícone (Olá um com ícone "seta para a esquerda e uma seta à direita" Olá Olá à direita da coluna de saudação)
5. Perceba que o local é um campo "Registro". Expanda registro hello e selecione apenas as coordenadas de saudação. A coordenada é uma coluna de lista
6. Adicionar uma nova coluna tooconvert Olá lista coordenada de colunas em uma coluna de LatLong separada por vírgulas concatenando elementos Olá dois no campo de coordenada lista hello usando a fórmula de saudação ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Por fim, converter Olá ```Elevation``` tooDecimal de coluna e selecione Olá **fechar** e **aplicar**.

Em vez de etapas anteriores, você pode colar Olá após código scripts Olá etapas usadas em Olá Editor Avançado no Power BI que permite transformações de dados Olá toowrite em uma linguagem de consulta.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Agora você tem dados saudação em seu modelo de dados do Power BI. A área de trabalho do Power BI deve aparecer da seguinte maneira:

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Você pode iniciar a criação de relatórios e visualizações usando o modelo de dados de saudação. Você pode seguir as etapas de saudação neste [artigo do Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild um relatório. resultado final de saudação é um relatório semelhante ao seguinte hello.

![Exibição de relatório do Power BI Desktop — conector do Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Dimensionar dinamicamente seu toomeet DSVM que precisa de seu projeto
Você pode dimensionar para cima e Olá DSVM toomeet que precisa de seu projeto. Se não precisar Olá toouse VM em finais de semana ou saudação da noite, você pode desligar Olá VM de saudação [portal do Azure](https://portal.azure.com).

> [!NOTE]
> Incorre em encargos de computação se você usar apenas Olá botão de desligamento de sistema operacional em Olá VM.  
> 
> 

Se você precisar toohandle algumas análises de grande escala e precisa de mais capacidade de CPU ou memória ou disco, você pode encontrar uma grande variedade de tamanhos VM em termos de núcleos de CPU, capacidade de memória e tipos de disco (incluindo unidades de estado sólido) que atendem suas necessidades de orçamento e de computação. Olá lista completa de VMs junto com seus preços por hora de computação está disponível em Olá [preços de máquinas virtuais do Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) página.

Da mesma forma, se reduz a necessidade de capacidade de processamento de VM (por exemplo: você moveu tooa uma grande carga de trabalho Hadoop ou um cluster Spark), você pode reduzir o cluster de saudação do hello [portal do Azure](https://portal.azure.com) e toohello configurações da VM instância. Veja uma captura de tela.

![Configurações da instância VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Instalar ferramentas adicionais na sua máquina virtual
Podemos empacotar várias ferramentas que acreditamos que são tooaddress capaz de muitas das necessidades de análise de dados comuns hello e que devem economizar tempo, evitando a necessidade de tooinstall configurar ambientes de uma e economizar dinheiro por pagar apenas para os recursos que você Use.

Você pode aproveitar os outros dados do Azure e serviços de análise descritos neste artigo tooenhance seu ambiente de análise. Entendemos que, em alguns casos, suas necessidades podem exigir ferramentas adicionais, incluindo algumas ferramentas de terceiros. Você tem acesso administrativo completo em Olá máquina virtual tooinstall novas ferramentas que você precisa. Também é possível instalar pacotes adicionais no Python e no R que não foram pré-instalados. Para Python, você pode usar ```conda``` ou ```pip```. Para R, você pode usar o hello ```install.packages()``` na Olá R console ou usar Olá IDE e escolha "**pacotes** -> **pacotes de instalação...** ".

## <a name="summary"></a>Resumo
Essas são apenas algumas das coisas Olá que você pode fazer no hello máquina de Virtual de ciência de dados do Microsoft. Há muitas outras coisas que você pode fazer toomake-lo um ambiente de análise efetiva.

