---
title: "Configuração do Serviço de Experimentação do Azure Machine Learning | Microsoft Docs"
description: "Este artigo fornece uma visão geral de alto nível do Serviço de Experimentação do Azure Machine Learning com instruções sobre como configurá-lo."
services: machine-learning
author: gokhanuluderya-msft
ms.author: gokhanu
manager: haining
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 09/28/2017
ms.openlocfilehash: bd152cc79c08124a1acab2aefc8652c7d162ea2c
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="configuring-azure-machine-learning-experimentation-service"></a>Configuração do Serviço de Experimentação do Azure Machine Learning

## <a name="overview"></a>Visão geral
O Serviço de Experimentação do Azure Machine Learning permite que os cientistas de dados executem seus experimentos usando os recursos de execução e de gerenciamento de execução do Azure Machine Learning. Ele fornece uma estrutura para experimentação agile com iterações rápidas. O Azure Machine Learning Workbench permite que você comece com execuções locais em seu computador, e fornece um caminho fácil para escalar verticalmente e horizontalmente para outros ambientes, como VMs de Ciência de Dados remotas com GPU ou Clusters do HDInsight executando Spark.

O Serviço de Experimentação foi criado para fornecer execuções consistentes, isoladas e reproduzíveis de seus experimentos. Ele ajuda a gerenciar seus destinos de computação, ambientes de execução e configurações de execução. Com os recursos de execução e de gerenciamento de execução do Azure Machine Learning Workbench você pode alternar facilmente entre ambientes diferentes. 

Você pode executar um script do Python ou do PySpark em um projeto do Workbench localmente ou em escala na nuvem. 

Você pode executar os scripts em: 

* Ambiente Python (3.5.2) no computador local instalado pelo Workbench.
* Ambiente Conda Python dentro de um contêiner do Docker no computador local
* Ambiente Conda Python dentro de um contêiner do Docker em um computador Linux remoto. Por exemplo, um [DSVM com base em Ubuntu no Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)
* [HDInsight para Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/) no Azure

>[!IMPORTANT]
>O Serviço de Experimentação do Azure Machine Learning atualmente dá suporte a Python 3.5.2 e Spark 2.1.11 como versões de tempo de execução do Python e do Spark, respectivamente. 


### <a name="key-concepts-in-experimentation-service"></a>Principais conceitos no Serviço de Experimentação
É importante entender os conceitos a seguir na execução do experimento do Azure Machine Learning. Nas seções subsequentes, discutiremos como usar esses conceitos em detalhes. 

#### <a name="compute-target"></a>Destino de computação
Um _destino de computação_ especifica em que local executar o programa, como a área de trabalho, o Docker remoto em uma VM ou um cluster. Um destino de computação precisa ser endereçável e acessível por você. O Workbench oferece a capacidade de criar destinos de computação e gerenciá-los usando o aplicativo Workbench e a CLI. 

O comando _az ml computetarget attach_ na CLI permite que você crie um destino de computação que possa usar em suas execuções.

Os destinos de computação com suporte são:
* Ambiente Python (3.5.2) local no computador instalado pelo Workbench.
* Docker local no seu computador
* Docker remoto em VMs Linux-Ubuntu. Por exemplo, um [DSVM com base em Ubuntu no Azure](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu)
* [HDInsight para cluster do Spark](https://azure.microsoft.com/services/hdinsight/apache-spark/) no Azure

O Serviço de Experimentação atualmente dá suporte a Python 3.5.2 e Spark 2.1.11 como versões de tempo de execução do Python e do Spark, respectivamente. 

>[!IMPORTANT]
> VMs Windows executando o Docker **não** têm suporte como destinos de computação remota.

#### <a name="execution-environment"></a>Ambiente de execução
O _ambiente de execução_ define a configuração de tempo de execução e as dependências necessárias para executar o programa no Workbench.

Gerencie o ambiente de execução local usando suas ferramentas e gerenciadores de pacotes favoritos se estiver executando no tempo de execução padrão do Workbench. 

Conda é usado para gerenciar execuções locais e remotas do Docker, bem como execuções baseadas em HDInsight. Para esses destinos de computação, a configuração do ambiente de execução é gerenciada por meio do **Conda_dependencies.yml** e do **Spark_dependencies.yml arquivos**. Esses arquivos estão na pasta **aml_config** dentro do seu projeto.

**Os tempos de execução com suporte para os ambientes de execução são:**
* Python 3.5.2
* Spark 2.1.11

### <a name="run-configuration"></a>Configuração de execução
Além do ambiente de execução e de destino de computação, o Azure Machine Learning fornece uma estrutura para definir e alterar as *configurações de execução*. Diferentes execuções do seu experimento podem exigir uma configuração diferente como parte de experimentação iterativa. Você pode estar varrendo diferentes intervalos de parâmetros, usando diferentes fontes de dados e ajustando os parâmetros do Spark. O Serviço de Experimentação oferece uma estrutura para gerenciar as configurações de execução.

Executar o comando _az ml computetarget attach_ produz dois arquivos na sua pasta **aml_config** em seu projeto: um .compute e um .runconfig seguindo esta convenção: _<your_computetarget_name>.compute_ e _<your_computetarget_name>.runconfig_. O arquivo .runconfig é criado automaticamente para sua conveniência ao criar um destino de computação. Você pode criar e gerenciar outras configurações de execução usando o comando _az ml runconfigurations_ da CLI. Você também pode criá-las e editá-las no sistema de arquivos.

A configuração de execução no Workbench também permite especificar variáveis de ambiente. Você pode especificar variáveis de ambiente e usá-las em seu código adicionando a seção a seguir em seu arquivo .runconfig. 

```
EnvironmentVariables:
"EXAMPLE_ENV_VAR1": "Example Value1"
"EXAMPLE_ENV_VAR2": "Example Value2"
```

Essas variáveis de ambiente podem ser acessadas no seu código. Por exemplo, esse trecho de código phyton imprime a variável de ambiente chamada "EXAMPLE_ENV_VAR1"
```
print(os.environ.get("EXAMPLE_ENV_VAR1"))
```

_**A figura a seguir mostra o fluxo de alto nível de execução de experimento inicial.**_
![](media/experimentation-service-configuration/experiment-execution-flow.png)

## <a name="experiment-execution-scenarios"></a>Cenários de execução de experimento
Nesta seção, vamos nos aprofundar nos cenários de execução e saber mais sobre como o Azure Machine Learning executa experimentos, especificamente executando um experimento localmente, em uma VM remota e em um Cluster do HDInsight. Esta seção é um passo a passo que começa na criação de um destino de computação e vai até a execução dos seus experimentos.

>[!NOTE]
>Para o restante deste artigo, estamos usando os comandos da CLI (interface de linha de comando) para mostrar os conceitos e os recursos. Os recursos descritos aqui também podem ser usados no Workbench.

## <a name="launching-the-cli"></a>Inicialização da CLI
Uma maneira fácil de inicializar a CLI é abrir um projeto no Workbench e navegar até **Arquivo-->Abrir Prompt de Comando**.

![](media/experimentation-service-configuration/opening-cli.png)

Esse comando inicializa uma janela de terminal na qual você pode inserir comandos para executar scripts na pasta do projeto atual. Esta janela de terminal é configurada com o ambiente de Python 3.5.2 instalado pelo Workbench.

>[!NOTE]
> Quando você executa qualquer comando _az ml_ na janela Comando, precisa ser autenticado no Azure. A CLI usa um cache de autenticação independente e, em seguida, o aplicativo da área de trabalho. Assim, fazer logon no Workbench não significa que você esteja autenticado em seu ambiente da CLI. Para fazer a autenticação, siga as etapas abaixo. O token de autenticação é armazenado em cache localmente por um período, de modo que você apenas precisa repetir essas etapas quando o token expira. Quando o token expirar ou se você estiver vendo erros de autenticação, execute os seguintes comandos:

```
# to authenticate 
$ az login

# to list subscriptions
$ az account list -o table

# to set current subscription to a particular subscription ID 
$ az account set -s <subscription_id>

# to verify your current Azure subscription
$ az account show
```

>[!NOTE] 
>Quando você executa o comando _az ml_ dentro de uma pasta de projeto, verifique se o projeto pertence a uma conta de Experimentação do Azure Machine Learning na assinatura _atual_ do Azure. Caso contrário, você poderá encontrar erros de execução.


## <a name="running-scripts-and-experiments"></a>Execução de scripts e experimentos
Com o Workbench, você pode executar os scripts Python e PySpark de vários destinos de computação usando o comando _az ml experiment submit_. Este comando requer uma definição de configuração de execução. 

O Workbench cria um arquivo .runconfig correspondente quando você cria um destino de computação, mas você pode criar configurações de execução adicionais usando o comando _az ml runconfiguration create_. Você também pode editar manualmente os arquivos de configuração de execução.

As configurações de execução aparecem como parte da experiência de execução do experimento no Workbench. 

>[!NOTE]
>Você pode aprender mais sobre o arquivo de configuração de execução na seção [Referência de configuração de execução de experimento](experimentation-service-configuration-reference.md).

## <a name="running-a-script-locally-on-workbench-installed-runtime"></a>Como executar um script localmente no tempo de execução instalado pelo Workbench
O Workbench permite que você execute seus scripts diretamente no tempo de execução do Python 3.5.2 instalado pelo Workbench. Esse tempo de execução padrão é instalado no tempo de configuração do Workbench e inclui bibliotecas e dependências do Azure Machine Learning. Resultados e artefatos da execução para execuções locais ainda são salvos no Serviço de Histórico de Execução na nuvem.

Ao contrário das execuções baseadas em Docker, essa configuração _não_ é gerenciada pelo Conda. É preciso provisionar manualmente dependências do pacote para o seu ambiente do Workbench Python local.

Você pode executar o seguinte comando para executar o script localmente no ambiente Python instalado pelo Workbench. 

```
$az ml experiment submit -c local myscript.py
```

Você pode encontrar o caminho para o ambiente Python padrão digitando o seguinte comando na janela da CLI do Workbench.
```
$ conda env list
```

>[!NOTE]
>No momento, **não** há suporte para executar o PySpark diretamente no ambiente local do Spark. O Workbench dá suporte a scripts do PySpark em execução no Docker local. A imagem do Docker de base do Azure Machine Learning vem com o Spark 2.1.11 pré-instalado. 

_**Visão geral da execução local para um script Python:**_
![](media/experimentation-service-configuration/local-native-run.png)

## <a name="running-a-script-on-local-docker"></a>Como executar um script no Docker local
Você também pode executar seus projetos em um contêiner do Docker em seu computador local por meio do Serviço de Experimentação. O Workbench fornece uma imagem do Docker de base que vem com bibliotecas do Azure Machine Learning, bem como o tempo de execução do Spark 2.1.11, para facilitar execuções locais do Spark. O Docker precisa já estar em execução no computador local.

Para executar o script Python ou PySpark no Docker local, você pode executar os seguintes comandos na CLI.

```
$az ml experiment submit -c docker myscript.py
```
ou o
```
az ml experiment submit --run-configuration docker myscript.py
```

O ambiente de execução no Docker local é preparado usando a imagem base do Docker de base do Azure Machine Learning. O Workbench faz o download dessa imagem ao ser executado pela primeira vez e a sobrepõe a pacotes especificados em seu arquivo conda_dependencies.yml. Essa operação torna a execução inicial mais lenta, mas execuções subsequentes são consideravelmente mais rápidas, graças à reutilização de camadas em cache pelo Workbench. 

>[!IMPORTANT]
>Você precisa executar o comando _az ml experiment prepare -c docker_ primeiro para preparar a imagem do Docker para sua primeira execução. Você também pode definir o parâmetro **PrepareEnvironment** como true em seu arquivo docker.runconfig. Essa ação prepara automaticamente seu ambiente como parte da sua execução.  

>[!NOTE]
>Se você estiver executando um script PySpark no Spark, spark_dependencies.yml também será usado além dos conda_dependencies.yml.

Executar seus scripts em uma imagem do Docker oferece os seguintes benefícios:

1. Garante que o script possa ser executado com confiança em outros ambientes de execução. A execução em um contêiner do Docker ajuda a descobrir e evitar quaisquer referências locais que possam afetar a portabilidade. 

2. Permite testar rapidamente o código em tempos de execução e estruturas complexas de instalar e configurar, como Apache Spark, sem exigir que você mesmo faça a instalação.


_**Visão geral da execução do Docker local para um script Python:**_
![](media/experimentation-service-configuration/local-docker-run.png)

## <a name="running-a-script-on-a-remote-docker"></a>Como executar um script em um Docker remoto
Em alguns casos, os recursos disponíveis em seu computador local podem não ser suficientes para treinar o modelo desejado. Nessa situação, o Serviço de Experimentação permite uma maneira fácil de executar os scripts Python ou PySpark em VMs mais avançadas usando a execução remota do Docker. 

A VM remota deve atender aos seguintes requisitos:
* A VM remota deve estar em execução no Linux-Ubuntu e acessível por meio de SSH. 
* A VM remota precisa ter o Docker em execução.

>[!IMPORTANT]
> VMs do Windows executando o Docker **não** têm suporte como destinos de computação remota


Você pode usar o comando a seguir para criar tanto a definição de destino de computação quanto a configuração de execução para execuções baseadas em Docker remotas.

```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --password "sshpassword" 
```

Depois de configurar o destino de computação, você pode usar o seguinte comando para executar o script.
```
$ az ml experiment submit -c remotevm myscript.py
```
>[!NOTE]
>Lembre-se de que o ambiente de execução é configurado usando as especificações em conda_dependencies.yml. spark_dependencies.yml também será usado se a estrutura PySpark for especificada no arquivo .runconfig. 

O processo de construção do Docker para VMs remotas é exatamente o mesmo que o processo para execuções do Docker local, de modo que você pode esperar experiências de execução semelhantes.

>[!TIP]
>Se você preferir evitar a latência introduzida criando a imagem do Docker para a sua primeira execução, poderá usar o comando a seguir para preparar o destino de computação antes de executar o script. az ml experiment prepare -c remotedocker


_**Visão geral da execução da vm remota para um script Python:**_
![](media/experimentation-service-configuration/remote-vm-run.png)


## <a name="running-a-script-on-an-hdinsight-cluster"></a>Como executar um script em um cluster HDInsight
O HDInsight é uma plataforma popular para análise de Big Data com suporte para Apache Spark. O Workbench permite experimentação Big Data usando clusters HDInsight Spark. 

>[!NOTE]
>O cluster HDInsight deve usar o Blob do Azure como o armazenamento primário. O uso do armazenamento do Azure Data Lake ainda não tem suporte.

Você pode criar um destino de computação e uma configuração de execução para um cluster do HDInsight Spark usando o seguinte comando:

```
$ az ml computetarget attach cluster --name "myhdi" --address "<FQDN or IP address>" --username "sshuser" --password "sshpassword"  
```

>[!NOTE]
>Se você usar o FQDN, em vez de um endereço IP e seu cluster Spark HDI for denominado _foo_, o ponto de extremidade SSH estará no nó do driver chamado _ssh.azurehdinsight.net foo_. Não se esqueça do sufixo **-ssh** no nome do servidor ao usar FQDN para o parâmetro _--address_.


Depois que você tiver o contexto de computação, poderá executar o seguinte comando para executar o script do PySpark.

```
$ az ml experiment submit -c myhdi myscript.py
```

O Workbench prepara e gerencia o ambiente de execução no cluster HDInsight usando Conda. A configuração é gerenciada pelos arquivos de configuração _conda_dependencies.yml_ e _spark_dependencies.yml_. 

Você precisa de acesso SSH ao cluster HDInsight para executar experimentos nesse modo. 

>[!NOTE]
>A configuração com suporte é de clusters do HDInsight Spark executando Linux (Ubuntu com Python/PySpark 3.5.2 e Spark 2.1.11).

_**Visão geral da execução baseada em HDInsight para um script PySpark**_
![](media/experimentation-service-configuration/hdinsight-run.png)


## <a name="running-a-script-on-gpu"></a>Como executar um script na GPU
Para executar os scripts na GPU, você pode seguir as diretrizes neste artigo:[Como usar a GPU no Azure Machine Learning](how-to-use-gpu.md)

## <a name="using-ssh-key-based-authentication-for-creating-and-using-compute-targets"></a>Usar a autenticação baseada em chave SSH para criar e usar destinos de computação
O Azure Machine Learning Workbench permite criar e usar destinos de computação usando a autenticação baseada em chave SSH além do esquema baseado em nome de usuário/senha. Você pode usar essa funcionalidade com o remotedocker ou o cluster como o destino de computação. Quando você usa esse esquema, o Workbench cria um par de chaves pública/privada e relata a chave pública novamente. Você acrescenta a chave pública nos arquivos ~/.ssh/authorized_keys do seu nome de usuário. Em seguida, o Azure Machine Learning Workbench usa a autenticação baseada em chave SSH para acessar e executar neste destino de computação. Como a chave privada do destino de computação é salva no repositório de chaves do espaço de trabalho, outros usuários do espaço de trabalho podem usar o destino de computação da mesma forma, fornecendo o nome de usuário que foi usado para criar o destino de computação.  

Siga estas etapas para usar essa funcionalidade. 

- Crie um destino de computação usando um dos comandos a seguir.

```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --use-azureml-ssh-key
```
ou o
```
az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" -k
```
- Acrescente a chave pública gerada pelo Workbench no arquivo ~/.ssh/authorized_keys no destino de computação anexado. 

>[!IMPORTANT]
>Você precisa fazer logon no destino de computação com o mesmo nome de usuário que foi usado para criar o destino de computação. 

- Agora você pode preparar e usar o destino de computação usando a autenticação baseada em chave SSH.

```
az ml experiment prepare -c remotevm
```

## <a name="next-steps"></a>Próximas etapas
* [Criar e instalar o Azure Machine Learning](quickstart-installation.md)
* [Gerenciamento de Modelos](model-management-overview.md)
