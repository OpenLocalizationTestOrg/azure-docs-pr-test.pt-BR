---
title: "aaaWhat é uma máquina de Virtual de ciência de dados? | Microsoft Docs"
description: "Como tooget iniciada fazendo principais cenários de análise com máquinas de virtuais de ciência de dados."
keywords: "ferramentas de ciência de dados, máquina virtual de ciência de dados, ferramentas para ciência de dados, ciência de dados do linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Introdução toohello baseado em nuvem Máquina Virtual de ciência de dados para Linux e Windows
saudação de máquina Virtual de ciência de dados (DSVM) é uma imagem VM personalizada na nuvem do Azure da Microsoft desenvolvido especificamente para fazer a ciência de dados. Tem muitos ciência de dados populares e outras ferramentas previamente instalado e configurado previamente toojump-Iniciar criação de aplicativos inteligentes para análises avançadas. Ela está disponível no Windows Server e no Linux. Oferecemos a edição do Windows do DSVM no Server 2016 e no Server 2012. Oferecemos a edição de Linux do hello DSVM Ubuntu 16.04 LTS e distribuições do Linux com base em OpenLogic 7.2 CentOS. 

Este tópico discute o que você pode fazer com hello VM de ciência de dados, descreve algumas das principais cenários de saudação para usar o hello VM, relaciona Olá principais recursos disponíveis no hello Windows e versões do Linux e fornece instruções sobre como tooget começar a usá-los.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>O que pode fazer com hello máquina de Virtual de ciência de dados?
objetivo Olá Olá máquina de Virtual de ciência de dados é tooprovide profissionais de dados em todos os níveis de habilidade e funções com um ambiente de ciência de dados descomplicado. Com essa VM, você economiza tempo considerável que gastaria se tivesse distribuído um ambiente comparável por conta própria. Em vez disso, inicie seu projeto de ciência de dados imediatamente em uma instância de VM recentemente criada. 

Olá VM de ciência de dados foi criado e configurado para trabalhar com um cenários de uso amplo. Você pode reduzir ou aumentar o ambiente de acordo com as necessidades do seu projeto. Você é toouse capaz de tarefas de ciência de dados de tooprogram seu idioma preferencial. Você pode instalar outras ferramentas e personalizar o sistema Olá para suas necessidades exatas.

## <a name="key-scenarios"></a>Principais cenários
Esta seção sugere alguns cenários principais para qual Olá VM de ciência de dados pode ser implantado.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Área de trabalho de análise na nuvem de saudação de pré-configurado
Olá VM de ciência de dados fornece uma configuração de linha de base para equipes de ciência de dados, procurando tooreplace suas áreas de trabalho locais com uma área de trabalho de nuvem gerenciado. Esta linha de base garante que todos os cientistas de dados de saudação em uma equipe tem uma configuração consistente com as experiências de tooverify e promovem a colaboração. Ela também reduz os custos, reduzindo a carga de sysadmin hello e salvar no tempo de saudação necessário tooevaluate, instalar e manter Olá vários pacotes de software necessária toodo análise avançada.  

### <a name="data-science-training-and-education"></a>Educação e treinamento de ciência de dados
Instrutores da empresa e aos educadores que ensinam a classes de ciência de dados geralmente fornecem um tooensure de imagem de máquina virtual seus alunos têm uma configuração consistente e que os exemplos de saudação trabalhar previsível. Olá VM de ciência de dados cria um ambiente de sob demanda com uma configuração consistente que facilita a desafios de incompatibilidade e suporte de saudação. Casos em que esses ambientes necessário toobe com frequência, criado especialmente para classes de treinamento menores, se beneficiar substancialmente.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Capacidade elástica sob demanda para projetos em larga escala
As maratonas/competições de ciência de dados ou modelagem e exploração de dados em larga escala exigem que a capacidade de hardware seja escalada horizontalmente, geralmente por um curto período. Olá VM de ciência de dados pode ajudar a replicar Olá dados ciência ambiente rapidamente sob demanda, nos servidores de expansão que permite experiências que requerem alta capacidade toobe de recursos de computação execute.

### <a name="short-term-experimentation-and-evaluation"></a>Avaliação e experimento de curto prazo
Olá VM de ciência de dados pode ser usado tooevaluate ou aprender ferramentas como o Microsoft R Server, SQL Server, ferramentas do Visual Studio, Jupyter, profundidade de aprendizado / ML kits de ferramentas e as novas ferramentas comuns em Olá comunidade com esforço mínimo de instalação. Como Olá VM de ciência de dados pode ser definido rapidamente, ele pode ser aplicado em outros cenários de uso de curto prazo como replicar experiências publicadas, demonstrações, seguir instruções passo a passo em sessões on-line ou tutoriais de conferência em execução.

### <a name="deep-learning"></a>Aprendizado
ciência de dados Olá VM pode ser usada para o modelo de treinamento usando algoritmos de aprendizado em GPU (unidades de processamento gráfico) baseado em hardware. Utilizando a VM dimensionamento de recursos de nuvem do Azure, DSVM ajuda você a usar o hardware da GPU com base na nuvem de saudação de acordo com a necessidade. Uma possível alternar tooa GPU com base em VM durante o treinamento de modelos grandes ou precisam cálculos de alta velocidade e manter Olá mesmo disco do sistema operacional.  edição do Windows Server 2016 de saudação do DSVM vem pré-instalado com drivers de GPU, estruturas e versão GPU do hello profundo de algoritmos de aprendizagem. Em Olá Linux, profundo de aprendizado na GPU só está habilitado em Olá [máquina de Virtual de ciência de dados para a edição do Linux (Ubuntu)](http://aka.ms/dsvm/ubuntu). Você pode implantar a edição do Windows/Ubuntu-2016 Olá da máquina virtual para Azure do VM de ciência de dados toonon GPU com base caso em que todas as estruturas de aprendizado hello serão modo fallback toohello da CPU. Anteriormente, para o Windows Server 2012, publicamos um [Kit de ferramentas de aprendizagem profunda](http://aka.ms/dsvm/deeplearning), mas agora é recomendável usar o Windows Server 2016 para cargas de trabalho de aprendizagem profunda baseadas em Windows. edição de baseado em CentOS Linux de saudação do hello DSVM contém somente Olá CPU cria alguns Olá profundo de ferramentas (CNTK, Tensorflow, MXNet) de aprendizado, mas não vem pré-instalado com estruturas e os drivers de GPU hello. 

## <a name="whats-included-in-hello-data-science-vm"></a>O que está incluído no hello VM de ciência de dados?
Olá máquina de Virtual de ciência de dados tem muitas ciência de dados populares e profundo aprendizado ferramentas já instalado e configurado. Ele também inclui ferramentas que tornam mais fácil toowork com vários produtos de dados e análise do Azure. Você pode explorar e criar modelos de previsão em conjuntos de dados em larga escala usando Olá Microsoft R Server ou SQL Server 2016. Um host de outras ferramentas da comunidade de código-fonte aberto hello e da Microsoft também são incluído, bem como exemplo de código e notebooks. Olá tabela a seguir relaciona e compara os componentes principais do hello incluídos no hello Windows e Linux edições de saudação máquina de Virtual de ciência de dados.


| **Ferramenta**                                                           | **Edição do Windows** | **Edição do Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R Open](https://mran.microsoft.com/open/) com pacotes populares pré-instalados   |S                      | S             |
| O [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition inclui <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) paralelo e distribuído de alto desempenho na estrutura R<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) – Novos algoritmos de AM de última geração da Microsoft <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [Operacionalização de R](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |S                      | S <br/> (MicrosoftML ainda não disponível)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro Plus com ativação compartilhada – Excel, Word e PowerPoint   |S                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 com pacotes populares pré-instalados    |S                      |S              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) com pacotes populares para linguagem Julia pré-instalados                         |S                      |S              |
| Bancos de dados relacionais                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Ferramentas de Banco de Dados                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> Drivers * ODBC/JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (ferramenta de consultas), <br /> * bcp, sqlcmd <br /> Drivers * ODBC/JDBC|
| Análise no banco de dados escalonável com o SQL Server R Services | S     |N              |
| **[Jupyter Notebook Server](http://jupyter.org/) com os kernels a seguir,**                                  | S     | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 e 3.5 | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (somente Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | S |
| JupyterHub (Servidor com vários notebooks)| N | S |
| **Ferramentas de desenvolvimento, IDEs e editores de código**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) > com Git Plugin, Azure HDInsight (Hadoop), Data Lake, SQL Server Data Tools, [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs) e [RTVS (Ferramentas do R para Visual Studio)](http://microsoft.github.io/RTVS-docs/) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio Code](https://code.visualstudio.com/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (IDE de Julia)](http://junolab.org/)| S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim e Emacs | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git e GitBash | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | S | N |
| PowerBI Desktop | S | N |
| Tooaccess SDKs do Azure e o pacote de inteligência de Cortana de serviços | S | S |
| **Ferramentas de movimentação de dados e gerenciamento** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Gerenciador de Armazenamento do Azure | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CLI do Azure](https://docs.microsoft.com/cli/azure/overview) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure PowerShell | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy(Azure Data Lake Storage)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Ferramenta de Migração de Dados do DocDB](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Gateway de Gerenciamento de Dados da Microsoft](https://msdn.microsoft.com/library/dn879362.aspx): mover dados entre o local e a nuvem | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Utilitários de linha de comando Unix/Linux | S | S |
| [Apache Drill](http://drill.apache.org) para Exploração de dados | S | S |
| **Machine Learning Tools** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* Integração com [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R, Python) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (somente Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | N | Y (somente Ubuntu) |
| **Ferramentas de Aprendizado baseadas em GPU** |Edição do Windows Server 2016  |Edição do Ubuntu |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | S | S|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe e Caffe2](https://github.com/caffe2/caffe2) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CUDA, CUDNN, Nvidia Driver](https://developer.nvidia.com/cuda-toolkit) | S | S |
| **Plataforma Big Data (somente Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* [Spark](http://spark.apache.org/) autônomo local | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Hadoop](http://hadoop.apache.org/) local (HDFS, YARN) | N | S |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Como tooget iniciada com hello VM de ciência de dados do Windows
* Criar uma instância da edição do Windows DSVM Olá desejado, navegando para
  * [DSVM baseado em Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  ou o 
  * [DSVM baseado em Windows Server 2012](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Clique em Olá **obter TI agora** botão.
* Entrar toohello VM da área de trabalho remota usando as credenciais de saudação você especificou quando criou Olá VM.
* toodiscover e iniciar ferramentas de saudação disponíveis, clique em Olá **iniciar** menu.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Introdução ao Olá VM de ciência de dados do Linux
* Criar uma instância de saudação desejada edição Linux DSVM navegando muito
  * [DSVM baseado em Ubuntu](http://aka.ms/dsvm/ubuntu)

  ou o

  * [DSVM baseado em OpenLogic CentOS](http://aka.ms/dsvm/centos)

  
* Clique em Olá **obtê-lo agora** botão.
* Entre em toohello VM em um cliente SSH, como Putty ou comando SSH, usando credenciais de saudação você especificou quando criou Olá VM.
* No prompt de shell hello, insira informações de mais de dsvm.
* Para uma área de trabalho gráfica, baixe o cliente de saudação X2Go para sua plataforma de cliente [aqui](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) e siga as instruções de saudação no documento de VM de ciência de dados do Linux Olá [Olá provisionar máquina de Virtual de ciência de dados de Linux](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Próximas etapas
### <a name="for-hello-windows-data-science-vm"></a>Para Olá VM de ciência de dados do Windows
* Para obter mais informações sobre como toorun específico das ferramentas disponível na versão do Windows hello, consulte [Olá provisionar máquina de Virtual de ciência de dados do Microsoft](machine-learning-data-science-provision-vm.md) e
* Para obter mais informações sobre como tooperform várias tarefas necessárias para o seu projeto de ciência de dados em Olá VM do Windows, consulte [dez coisas que você pode fazer na máquina Virtual de ciência de dados de saudação](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Para Olá VM de ciência de dados do Linux
* Para obter mais informações sobre como toorun específico das ferramentas disponível na versão do Linux hello, consulte [Olá provisionar máquina de Virtual de ciência de dados do Linux](machine-learning-data-science-linux-dsvm-intro.md).
* Para uma explicação passo a passo que mostra como tooperform ciência de dados comum várias tarefas com hello VM do Linux, consulte [ciência de dados na máquina de Virtual de ciência de dados do Linux de saudação](machine-learning-data-science-linux-dsvm-walkthrough.md).

