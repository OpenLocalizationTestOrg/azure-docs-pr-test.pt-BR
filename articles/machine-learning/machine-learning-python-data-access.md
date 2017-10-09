---
title: "conjuntos de dados aaaAccess com biblioteca de cliente do Python de aprendizado de máquina | Microsoft Docs"
description: "Instalar e usar o hello tooaccess de biblioteca de cliente do Python e gerenciar dados de aprendizado de máquina do Azure com segurança de um ambiente local do Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Conjuntos de dados do Access com Python usando a biblioteca de cliente do Python de aprendizado de máquina do Azure Olá
visualização de saudação da biblioteca de cliente do Python de aprendizado de máquina do Microsoft Azure pode habilitar o acesso seguro tooyour conjuntos de dados de aprendizado de máquina do Azure de um ambiente local do Python e permite a criação de saudação e o gerenciamento de conjuntos de dados em um espaço de trabalho.

Este tópico fornece instruções sobre como:

* instalar a biblioteca de cliente do Python de aprendizado de máquina Olá 
* acessar e carregar conjuntos de dados, incluindo instruções sobre como tooget autorização tooaccess conjuntos de dados de aprendizado de máquina do Azure do seu ambiente local do Python
* acessar conjuntos de dados intermediários por meio de testes
* usar Olá Python cliente biblioteca tooenumerate conjuntos de dados, acessar os metadados, ler o conteúdo de saudação do conjunto de dados, criar novos conjuntos de dados e atualizar conjuntos de dados existentes

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Pré-requisitos
biblioteca de cliente do Python Olá foi testada em Olá ambientes a seguir:

* Windows, Mac e Linux
* Python 2.7, 3.3 e 3.4

Ele tem uma dependência em Olá pacotes a seguir:

* solicitações
* python-dateutil
* pandas

É recomendável usar uma distribuição de Python como [Anaconda](http://continuum.io/downloads#all) ou [abóbada](https://store.enthought.com/downloads/), que acompanham o Python, IPython e instalados Olá três pacotes listados acima. Embora o IPython não seja estritamente necessário, é um ótimo ambiente para manipular e visualizar dados interativamente.

### <a name="installation"></a>Como tooinstall Olá biblioteca de cliente do Python de aprendizado de máquina do Azure
biblioteca de cliente do Python de aprendizado de máquina do Azure Olá também deve ser instalado toocomplete tarefas de saudação descritas neste tópico. Ele está disponível no hello [índice de pacote do Python](https://pypi.python.org/pypi/azureml). tooinstall-lo em seu ambiente de Python, executar Olá seguinte comando do seu ambiente local do Python:

    pip install azureml

Como alternativa, você pode baixar e instalar de origens de saudação em [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Se você tiver o git instalado em seu computador, você pode usar o pip tooinstall diretamente do repositório do git hello:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Usar conjuntos de dados de tooaccess do Studio Code trechos de código
biblioteca de cliente do Python Olá fornece conjuntos de dados existentes do tooyour acesso programático em experiências que foram executadas.

Na interface de web do hello Studio, você pode gerar trechos de código que incluem todos os toodownload de informações necessárias de saudação e desserializar os conjuntos de dados como objetos Pandas DataFrame em seu computador local.

### <a name="security"></a>Segurança para acesso a dados
Olá trechos de código fornecidos pelo Studio para uso com a biblioteca de cliente do Python Olá inclui a id do espaço de trabalho e a autorização token. Esses fornecem espaço de trabalho de tooyour acesso completo e devem ser protegidos, como uma senha.

Por motivos de segurança, funcionalidade de trecho de código Olá só está disponível toousers com sua função definida como **proprietário** de espaço de trabalho de saudação. Sua função é exibida no estúdio de aprendizado de máquina do Azure em Olá **usuários** página em **configurações**.

![Segurança][security]

Se sua função não está definida como **proprietário**, você pode solicitar toobe novamente convidado como um proprietário ou peça ao proprietário de saudação do hello tooprovide de espaço de trabalho com o trecho de código hello.

token de autorização do tooobtain Olá, você pode fazer um dos seguintes hello:

* Solicitar um token de um proprietário. Os proprietários podem acessar seus tokens de autorização na página de configurações de saudação do seu espaço de trabalho no Studio. Selecione **configurações** de saudação à esquerda o painel e clique em **TOKENS de autorização** toosee Olá tokens primários e secundários.  Embora Olá primário ou tokens de autorização secundário Olá podem ser usados no trecho de código Olá, é recomendável que proprietários de compartilham somente tokens de autorização secundário hello.

![Tokens de autorização](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Peça toorole toobe promovido do proprietário.  toodo isso, um proprietário atual do toofirst de necessidades de espaço de trabalho Olá removê-lo da área de trabalho de saudação e convidá-lo novamente tooit como proprietário.

Assim que os desenvolvedores tem obtido Olá id e a autorização de token, eles são espaço de trabalho do hello capaz de tooaccess usando Olá trecho de código, independentemente de sua função.

Tokens de autorização são gerenciados no hello **TOKENS de autorização** página em **configurações**. Você pode gerá-los novamente, mas esse procedimento revoga anterior token de acesso de toohello.

### <a name="accessingDatasets"></a>Conjuntos de dados de acesso de um aplicativo Python local
1. No estúdio de aprendizado de máquina, clique em **conjuntos de dados** na barra de navegação Olá Olá esquerda.
2. Selecione o conjunto de dados de saudação você gostaria que tooaccess. Você pode selecionar qualquer um dos conjuntos de dados Olá Olá **Meus conjuntos de dados** lista ou de saudação **exemplos** lista.
3. Na barra de ferramentas do hello inferior, clique em **gerar código de acesso a dados**. Se dados saudação estão em um formato incompatível com a biblioteca de cliente do Python hello, esse botão será desabilitado.
   
    ![CONJUNTOS DE DADOS][datasets]
4. Selecione o trecho de código Olá da janela de saudação que aparece e copiá-lo na área de transferência tooyour.
   
    ![Código de acesso][dataset-access-code]
5. Cole o código de saudação no bloco de anotações de saudação do seu aplicativo local do Python.
   
    ![Bloco de notas][ipython-dataset]

## 
            <a name="accessingIntermediateDatasets">
            </a>Acesse os conjuntos intermediários de testes de Machine Learning
Após a execução de um experimento no hello estúdio de aprendizado de máquina, é possível tooaccess Olá intermediário conjuntos de dados de saudação nós de saída dos módulos. Os conjuntos de dados intermediários são dados que foram criados e usados para etapas intermediárias quando uma ferramenta de modelo tiver sido executada.

Conjuntos de dados intermediários podem ser acessados como formato de dados de saudação é compatível com a biblioteca de cliente do Python hello.

Olá formatos a seguir são suportados (constantes para eles estão em Olá `azureml.DataTypeIds` classe):

* Texto sem formatação
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

Você pode determinar o formato de saudação focalizando um nó de saída do módulo. Ele é exibido junto com o nome de nó hello, em uma dica de ferramenta.

Alguns dos módulos de saudação, como Olá [divisão] [ split] módulo, o formato da saída tooa chamado `Dataset`, que não é suportado pela biblioteca de cliente do Python hello.

![Formato de conjunto de dados][dataset-format]

Você precisa toouse um módulo de conversão, como [converter tooCSV][convert-to-csv], tooget uma saída em um formato com suporte.

![Formato de GenericCSV][csv-format]

Olá, etapas a seguir mostram um exemplo que cria um experimento, executa e acessa o conjunto de dados intermediário hello.

1. Criar um novo teste.
2. Inserir um módulo **Conjunto de dados de Classificação Binária de Renda de Censo de Adulto** .
3. Inserir uma [divisão] [ split] módulo e conecte-se a sua saída de módulo de conjunto de dados de entrada toohello.
4. Inserir uma [converter tooCSV] [ convert-to-csv] módulo e conecte-se a sua entrada tooone de saudação [divisão] [ split] saídas do módulo.
5. Salvar experimento hello, executá-lo e aguardar toofinish em execução.
6. Clique no nó Olá saída em Olá [converter tooCSV] [ convert-to-csv] módulo.
7. Quando o menu de contexto Olá for exibida, selecione **gerar código de acesso a dados**.
   
    ![Menu de contexto][experiment]
8. Selecione o trecho de código hello e copiá-lo na área de transferência tooyour da janela de saudação que aparece.
   
    ![Código de acesso][intermediate-dataset-access-code]
9. Cole o código de saudação do bloco de anotações.
   
    ![Bloco de notas][ipython-intermediate-dataset]
10. Você pode visualizar dados hello usando matplotlib. Isso exibe um histograma para a coluna de idade hello:
    
    ![Histograma][ipython-histogram]

## <a name="clientApis"></a>Saudação de uso tooaccess de biblioteca de cliente do Python de aprendizado de máquina, ler, criar e gerenciar conjuntos de dados
### <a name="workspace"></a>Espaço de trabalho
espaço de trabalho de saudação é o ponto de entrada de saudação para a biblioteca de cliente do Python hello. Fornecer Olá `Workspace` uma instância de classe com o espaço de trabalho id e a autorização toocreate token:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Enumerar conjuntos de dados
tooenumerate todos os conjuntos de dados em um determinado espaço de trabalho:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate Olá apenas criados pelo usuário conjuntos de dados:

    for ds in ws.user_datasets:
        print(ds.name)

conjuntos de dados de tooenumerate Olá apenas exemplo:

    for ds in ws.example_datasets:
        print(ds.name)

Você pode acessar um conjunto de dados por nome (que diferencia maiúsculas de minúsculas):

    ds = ws.datasets['my dataset name']

Ou você pode acessá-lo pelo índice:

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadados
Conjuntos de dados contêm metadados, adição toocontent. (Conjuntos de dados intermediários são uma regra de exceção de toothis e não tem nenhum metadado.)

Alguns valores de metadados são atribuídos pelo usuário Olá no momento da criação:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Outros são valores atribuídos pelo Azure ML:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Consulte Olá `SourceDataset` classe para mais em Olá os metadados disponíveis.

### <a name="read-contents"></a>Ler conteúdo
trechos de código Olá fornecidos pelo estúdio de aprendizado de máquina automaticamente baixar e desserializar um objeto de Pandas DataFrame de tooa Olá conjunto de dados. Isso é feito com hello `to_dataframe` método:

    frame = ds.to_dataframe()

Se você preferir dados brutos do toodownload hello e executar a desserialização de saudação, que é uma opção. No momento de hello, isso é Olá única opção para formatos como 'ARFF', não é possível desserializar a biblioteca de cliente do Python que hello.

conteúdo de saudação tooread como texto:

    text_data = ds.read_as_text()

conteúdo de saudação tooread como binários:

    binary_data = ds.read_as_binary()

Você também pode abrir um conteúdo toohello:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Criar um novo conjunto de dados
biblioteca de cliente do Python Olá permite tooupload conjuntos de dados em seu programa de Python. Esses conjuntos de dados ficarão disponíveis para uso em seu espaço de trabalho.

Se você tiver dados em um DataFrame Pandas, use Olá código a seguir:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Se os seus dados já estiverem serializados, você pode usar:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

biblioteca de cliente do Python Hello é capaz de tooserialize uma DataFrame de Pandas toohello a seguir formata (constantes para eles estão em Olá `azureml.DataTypeIds` classe):

* Texto sem formatação
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Atualizar um conjunto de dados existente
Se você tentar tooupload um novo conjunto de dados com um nome que corresponda a um conjunto de dados existente, você deve obter um erro de conflito.

tooupdate um conjunto de dados existente, você precisa primeiro tooget um conjunto de dados referência toohello existente:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Em seguida, use `update_from_dataframe` tooserialize e substituir conteúdo Olá Olá conjunto de dados no Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Se você quiser tooserialize Olá dados tooa outro formato, especifique um valor para Olá opcional `data_type_id` parâmetro.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Opcionalmente, você pode definir uma nova descrição especificando um valor para Olá `description` parâmetro.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Opcionalmente, você pode definir um novo nome especificando um valor para Olá `name` parâmetro. De agora em diante, você vai recuperar Olá dataset usando Olá nome novo. saudação de código a seguir atualiza a descrição, nome e os dados de saudação.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Olá `data_type_id`, `name` e `description` parâmetros são opcionais e o valor anterior tootheir padrão. Olá `dataframe` parâmetro sempre é necessário.

Se os seus dados já estiverem serializados, use `update_from_raw_data` em vez de `update_from_dataframe`. Se você simplesmente passar `raw_data` em vez de `dataframe`, ele funcionará da mesma forma.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

