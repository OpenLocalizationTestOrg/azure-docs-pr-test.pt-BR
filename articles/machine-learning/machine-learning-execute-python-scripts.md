---
title: "scripts de aprendizado de máquina de Python de aaaExecute | Microsoft Docs"
description: "Descreve princípios de design subjacentes ao suporte a Python no Azure Machine Learning e seus cenários de uso básico, recursos e limitações."
keywords: "aprendizado de máquina em python, pandas, python pandas, scripts python, executar scripts python"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Executar scripts Python de aprendizado de máquina no Azure Machine Learning Studio

Este tópico descreve os princípios de design Olá Olá de suporte atual para scripts Python no aprendizado de máquina do Azure subjacente. recursos principais do Hello fornecidos também são descritos, incluindo:

- executar cenários de uso básico
- pontuação de um experimento em um serviço Web
- suporte para importação de código existente
- exportar visualizações
- executar seleção de recursos supervisionada
- entender algumas limitações

[Python](https://www.python.org/) é uma ferramenta indispensável no conjunto de ferramentas de saudação de muitos cientistas de dados. Ele tem:

* uma sintaxe elegante e concisa, 
* suporte de plataforma cruzada, 
* uma grande coleção de bibliotecas eficientes, e 
* ferramentas de desenvolvimento sólidas. 

O Python está sendo usado em todas as fases de um fluxo de trabalho normalmente usado na modelagem de aprendizado de máquina:

- ingestão de dados e processamento 
- construção de recurso
- treinamento do modelo 
- validação de modelo
- implantação de modelos de saudação

O Azure Machine Learning Studio dá suporte à inclusão de scripts de Python em várias partes de um experimento de aprendizado de máquina, bem como à sua publicação integrada como serviços Web no Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Princípios de design de scripts Python no Machine Learning

Olá principal interface tooPython no estúdio de aprendizado de máquina do Azure é por meio de saudação [Executar Script Python] [ execute-python-script] módulo mostrado na Figura 1.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Figura 1. Olá **Executar Script Python** módulo.

Olá [Executar Script Python] [ execute-python-script] módulo no Azure ML Studio aceita backup toothree entradas e produz o tootwo saídas (discutidas Olá seção a seguir), como seu análogo de R, hello [ Executar Script R] [ execute-r-script] módulo. Hello toobe de código Python executado é inserido na caixa de parâmetro hello como uma nomeada chamada de função de ponto de entrada `azureml_main`. Aqui estão os princípios usado tooimplement esse módulo de design principais do hello:

1. *Devem ser expressões idiomáticas para usuários de Python.* A maioria dos usuários de Python fatora o código como funções em módulos. Portanto, colocar um lote de instruções executáveis em um módulo de nível superior é relativamente raro. Como resultado, caixa de script hello também usa uma função de Python especialmente nomeada como toojust contrário uma sequência de instruções. Olá objetos expostos na função hello são tipos de biblioteca do Python padrão como [Pandas](http://pandas.pydata.org/) quadros de dados e [NumPy](http://www.numpy.org/) matrizes.
2. *Deve ter alta fidelidade entre execuções locais e na nuvem.* Olá Olá tooexecute de back-end usado código Python baseia [Anaconda](https://store.continuum.io/cshop/anaconda/), um amplamente usada distribuição de Python científica de plataforma cruzada. Ele acompanha fechar too200 dos pacotes Python mais comuns de saudação. Portanto, os cientistas de dados podem depurar e qualificar seu código no ambiente Anaconda compatível com o Azure Machine Learning. Em seguida, usar um ambiente de desenvolvimento existente, como [IPython](http://ipython.org/) notebook ou [ferramentas Python para Visual Studio](http://aka.ms/ptvs), toorun-lo como parte de um experimento ML do Azure. Olá `azureml_main` ponto de entrada é uma função de Python baunilha e, portanto * pode ser criado sem código específico do ML do Azure ou Olá SDK instalado.
3. 
            *Deve ser totalmente combinável com outros módulos do Azure Machine Learning.* Olá [Executar Script Python] [ execute-python-script] módulo aceita, como entradas e saídas, conjuntos de dados de aprendizado de máquina do Azure padrão. estrutura subjacente Olá modo transparente e eficiente preenche Olá tempos de execução de ML do Azure e Python. Portanto, o Python pode ser usado em conjunto com fluxos de trabalho do Azure ML existentes, incluindo aqueles que chamam o R e o SQLite. Como resultado, um cientista de dados pôde compor fluxos de trabalho que:
   * usam o Python e o Pandas para pré-processando e limpeza de dados
   * transformação de SQL do feed Olá dados tooa, unir vários conjuntos de dados tooform recursos
   * treinar modelos usando algoritmos de saudação no aprendizado de máquina do Azure 
   * Avalie e pós-processamento resultados hello usando R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Cenários de uso básico no ML para scripts Python

Nesta seção, podemos pesquisa alguns dos usos básicos Olá Olá [Executar Script Python] [ execute-python-script] módulo. Módulo de Python toohello entradas são expostos como quadros de dados Pandas. Olá função deve retornar uma única estrutura de dados Pandas empacotada dentro de um Python [sequência](https://docs.python.org/2/c-api/sequence.html) como uma tupla, lista ou matriz NumPy. primeiro elemento Olá dessa sequência, em seguida, é retornado em hello, a primeira porta de saída do módulo de saudação. O esquema é mostrado na Figura 2.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Figura 2. Mapeamento de porta de toooutput de valor de retorno e de tooparameters de portas de entrada.

Mais detalhadas a semântica de como portas de entrada hello obtém tooparameters mapeada de saudação `azureml_main` função são mostrados na tabela 1:

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabela 1. Mapeamento de parâmetros de toofunction portas de entrada.

mapeamento de saudação entre as portas de entrada e os parâmetros de função é posicional:

- porta de entrada conectado primeiro Olá é mapeada toohello primeiro parâmetro da função de saudação. 
- Olá segunda entrada (se conectado) é mapeado toohello segundo parâmetro de função hello.

Consulte *Python para análise de dados* (o ' Reilly, 2012) por McKinney Oeste para saber mais sobre Pandas Python e como ele pode ser usado toomanipulate dados eficaz e eficiente. 


## <a name="translation-of-input-and-output-types"></a>Conversão de tipos de entrada e saída 
Conjuntos de dados de entrada no Azure ML são quadros toodata convertido em Pandas. Quadros de dados de saída são convertidos tooAzure back ML conjuntos de dados. Olá conversões a seguir é executada:

1. Colunas de cadeia de caracteres e numéricos são convertidas como-é e valores ausentes em um conjunto de dados são convertidos too'NA' valores em Pandas. Olá mesmo conversão ocorre no hello antigos (NA valores na Pandas são convertidos toomissing no ML do Azure).
2. Os vetores de índice no Pandas não têm suporte no Azure ML. Todos os quadros de dados de entrada na função de Python Olá sempre tem um índice numérico de 64 bits do número de 0 toohello de linhas menos 1. 
3. Conjuntos de dados do Azure ML não podem ter nomes de coluna duplicados e nomes de coluna que não são cadeias de caracteres. Se um quadro de dados de saída contém colunas não numéricas, Olá estrutura chama `str` em nomes de coluna hello. Da mesma forma, os nomes de coluna duplicados são automaticamente danificado tooinsure Olá nomes são exclusivos. sufixo de saudação (2) é adicionado a duplicata primeiro toohello, (3) toohello duplicata de segundo e assim por diante.


## <a name="operationalizing-python-scripts"></a>Operacionalizando scripts Python

Quaisquer módulos [Executar Script Python][execute-python-script] usados em um teste de pontuação são chamados quando publicados como um serviço Web. Por exemplo, a Figura 3 mostra um experimento de pontuação que contém o código de saudação tooevaluate uma única expressão de Python. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Figura 3. Serviço Web para avaliar uma expressão de Python.

Um serviço Web criado com base neste teste:

- aceita como entrada uma expressão Python (como uma cadeia de caracteres)
- envia o interpretador do Python toohello 
- Retorna uma tabela que contém a expressão hello e resultado Olá avaliada.


## <a name="importing-existing-python-script-modules"></a>Importando módulos de script Python existentes

Um caso de uso comum para muitos cientistas de dados é tooincorporate scripts existentes do Python em experiências de ML do Azure. Em vez de exigir que todos os códigos de ser concatenados e colados em uma caixa de script simples, Olá [Executar Script Python] [ execute-python-script] módulo aceita um arquivo zip que contém módulos Python na porta de entrada terceiro hello. arquivo Hello é descompactado pelo framework de execução de saudação em tempo de execução e conteúdo de saudação é adicionado toohello caminho da biblioteca do interpretador do Python hello. Olá `azureml_main` função pode importar esses módulos diretamente do ponto de entrada.

Por exemplo, considere a possibilidade de arquivo hello Hello.py que contém uma função simples "Olá, mundo".

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Figura 4. Função definida pelo usuário no arquivo Hello.py.

Em seguida, criamos um arquivo Hello.zip que contenha o Hello.py:

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Figura 5. Arquivo zip que contém o código Python definido pelo usuário.

Carregar arquivo zip de saudação como um conjunto de dados no estúdio de aprendizado de máquina do Azure. Em seguida, criar e executar um teste que usa código Python a saudação Olá Hello arquivo anexando-porta de entrada terceiro toohello de saudação **Executar Script Python** módulo, conforme mostrado na figura.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Figura 6. Exemplo de experimento com código Python definido pelo usuário carregado como um arquivo zip.

saída de módulo Hello mostra o arquivo zip Olá foi descompactado e essa função hello `print_hello` foi executado.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Figura 7. Função definida pelo usuário em uso dentro de saudação [Executar Script Python] [ execute-python-script] módulo.


## <a name="working-with-visualizations"></a>Trabalhando com visualizações

Os gráficos criados usando MatplotLib que pode ser visualizado no navegador de saudação podem ser retornados por hello [Executar Script Python][execute-python-script]. Mas Olá gráficos não são automaticamente redirecionado tooimages quando forem ao usar R. Para que usuário Olá deve explicitamente salvar qualquer gráficos tooPNG arquivos se eles estiverem toobe retornou tooAzure back aprendizado de máquina. 

imagens de toogenerate de MatplotLib, você deve concluir Olá procedimento a seguir:

* comutador hello back-end muito "AGG" da saudação padrão com base em Qt renderizador 
* criar um novo objeto de figura 
* obter eixo hello e gerar todos os gráficos para ele 
* Salve o arquivo PNG do hello Figura tooa 

Esse processo é ilustrado no hello Figura 8 que cria uma matriz de gráfico de dispersão usando a função de scatter_matrix hello em Pandas a seguir.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Figura 8. O código de toosave que matplotlib figuras tooimages.

A Figura 9 mostra um experimento que use o script hello mostrada anteriormente tooreturn plota via hello segunda porta de saída.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Figura 9. Visualizando gráficos de plotagem gerados por meio do código Python.

É tooreturn possíveis múltiplas figuras salvando-os em diferentes imagens, Olá em tempo de execução do aprendizado de máquina do Azure capta todas as imagens e os concatena para visualização.


## <a name="advanced-examples"></a>Exemplos avançados

ambiente de Anaconda Olá instalado no aprendizado de máquina do Azure contém pacotes comuns como NumPy, SciPy e Scikits-Learn. Esses pacotes podem ser usados com eficiência para várias tarefas de processamento de dados em um pipeline de aprendizado de máquina. Como exemplo, hello script e experiência seguinte ilustram Olá uso de aprendizes ensemble em Scikits-Learn pontuações de importância de recurso toocompute um conjunto de dados. pontuações de saudação podem ser usado tooperform supervisionado de seleção de recursos antes de ser alimentado no outro modelo ML.

Aqui está o pontuações de importância de Olá Olá Python função usada toocompute e recursos de saudação de ordem com base em pontuações hello:

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

Figura 10. Função toorank recursos pontuações.
 Olá experimento seguinte, em seguida, calcula e retorna pontuações de importância de saudação de recursos no conjunto de dados do hello "Pima índico Diabetes" no aprendizado de máquina do Azure:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Figura 11. Experiência toorank recursos Olá Pima índico Diabetes dataset.

## <a name="limitations"></a>Limitações
Olá [Executar Script Python] [ execute-python-script] atualmente tem Olá seguintes limitações:

1. *Execução em modo seguro.* tempo de execução do Python Hello está atualmente em modo seguro e, como resultado, não permite sistema de arquivos local acesso toohello toohello ou de rede de maneira persistente. Todos os arquivos salvos localmente são isolados e excluídos depois de termina de módulo de saudação. Olá código Python não pode acessar a maioria dos diretórios na máquina de saudação em que é executado, Olá exceção sendo Olá diretório atual e seus subdiretórios.
2. *Falta de suporte para desenvolvimento e depuração sofisticados.* módulo de Python Olá atualmente não suporta recursos IDE como intellisense e depuração. Além disso, se o módulo de saudação falhar em tempo de execução, hello rastreamento de pilha de Python completo está disponível. Mas, ela deve ser exibida no log de saída Olá para o módulo de saudação. Atualmente, é recomendável desenvolver e depurar scripts Python em um ambiente, como IPython e, em seguida, Importar código Olá para módulo de saudação.
3. *Saída de estruturas de dados únicas.* ponto de entrada Hello Python é tooreturn permitido somente um quadro de dados único como saída. Não é possível no momento tooreturn que Python arbitrário objetos como modelos treinados diretamente fazer toohello tempo de execução do aprendizado de máquina do Azure. Como [Executar Script R][execute-r-script], que tem Olá mesma limitação, é possível em muitos casos toopickle objetos em um byte de matriz e, em seguida, retornam que dentro de um quadro de dados.
4. *Incapacidade toocustomize instalação Python*. Atualmente, hello somente modo tooadd Python módulos personalizados é por meio do mecanismo de arquivo zip Olá descrito anteriormente. Embora isso seja viável para pequenos módulos, é complicado para módulos grandes (especialmente aqueles com DLLs nativos) ou um grande número de módulos. 

## <a name="conclusions"></a>Conclusões
Olá [Executar Script Python] [ execute-python-script] módulo permite código Python existente de tooincorporate um cientista de dados em fluxos de trabalho de aprendizado de máquina hospedados em nuvem no aprendizado de máquina do Azure e tooseamlessly operacionalizá-los como parte de um serviço web. módulo de script de Python Olá naturalmente interage com outros módulos no aprendizado de máquina do Azure. módulo de saudação pode ser usado para uma variedade de tarefas de processamento de toopre de exploração de dados e extração de um recurso e, em seguida, tooevaluation e pós-processamento de resultados de saudação. Olá back-end em tempo de execução usado para a execução se baseia em Anaconda, uma distribuição de Python bem testada e amplamente usada. Essa back-end torna simples para você ativos de código existente do quadro tooon em nuvem hello.

Esperamos que tooprovide funcionalidade adicional toohello [Executar Script Python] [ execute-python-script] módulo como Olá tootrain de capacidade e colocar os modelos no Python e tooadd melhor suporte para Olá desenvolvimento e depuração de código no estúdio de aprendizado de máquina do Azure.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
