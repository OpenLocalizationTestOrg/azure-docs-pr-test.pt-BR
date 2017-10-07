---
title: "Olá aaaProvision máquina de Virtual de ciência de dados do Linux | Microsoft Docs"
description: "Configurar e criar uma máquina Virtual de ciência de dados de Linux no Azure toodo análise e aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 81dfa90f6cd4b4f33535a20fb97442bf9152d829
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-linux-data-science-virtual-machine"></a>Provisionar Olá máquina de Virtual de ciência de dados do Linux
Olá Linux máquina de Virtual de ciência de dados é uma CentOS com base em máquina virtual do Azure que vem com um conjunto de ferramentas pré-instalado. Essas ferramentas normalmente são usadas para fazer análises de dados e machine learning. componentes de software chave Olá incluídos são:

* Sistema operacional: Distribuição CentOS Linux.
* Microsoft R Server Developer Edition
* Distribuição do Anaconda Python (versões 2.7 e 3.5), incluindo bibliotecas de análise de dados populares
* JuliaPro - uma distribuição curada da linguagem Julia, com bibliotecas populares de análise de dados e científicas
* Instância autônoma de Spark e Hadoop de nó único (HDFS, Yarn)
* JupyterHub - um servidor de notebook Jupyter multiusuário com suporte para kernels R, Python, PySpark, Julia
* Gerenciador de Armazenamento do Azure
* CLI (interface de linha de comando) do Azure para gerenciar recursos do Azure
* Banco de dados PostgresSQL
* Ferramentas de Machine Learning
  * [CNTK (Kit de Ferramentas de Rede Computacional)](https://github.com/Microsoft/CNTK): um software de aprendizado aprofundado da Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): um sistema de machine learning rápido com suporte a técnicas como online, hash, allreduce, reduções, learning2search, ativo e aprendizado interativo.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): uma ferramenta que fornece implementação de árvore aumentada rápida e precisa.
  * [Rattle](http://rattle.togaware.com/) (Olá ferramenta analíticos R tooLearn facilmente): uma ferramenta que facilita a introdução à análise de dados e de máquina em R fácil, com a exploração de dados baseado em GUI de aprendizado e modelagem com a geração automática de código R.
* SDK do Azure em Java, Python, node.js, Ruby, PHP
* Bibliotecas em R e Python para uso no Azure Machine Learning e outros serviços do Azure
* Ferramentas de desenvolvimento e editores (RStudio, PyCharm, IntelliJ, Emacs, gedit, vi)


Fazer a ciência de dados envolve a iteração em uma sequência de tarefas:

1. Localizar, carregar e pré-processar dados
2. Compilar e testar modelos
3. Implantando modelos de saudação para consumo de aplicativos inteligentes

Os cientistas de dados usam toocomplete de várias ferramentas essas tarefas. Pode ser versões apropriadas do hello toofind consome muito tempo do software hello e, em seguida, toodownload, compilar e instalar essas versões.

Olá Linux máquina de Virtual de ciência de dados pode facilitar essa carga substancialmente. Usá-lo toojump iniciar seu projeto de análise. Ele permite toowork nas tarefas em vários idiomas, incluindo R, Python, SQL, Java e C++. Eclipse fornece um IDE toodevelop e testar seu código que é fácil toouse. Olá incluídos na VM de saudação do SDK do Azure permite que você toobuild seus aplicativos usando vários serviços no Linux para a plataforma de nuvem do Microsoft hello. Além disso, você tem acesso tooother idiomas como Ruby, Perl, PHP e Node. js também previamente instalados.

Não há encargos de software para esta imagem da VM de ciência de dados. Você paga Olá taxas são avaliadas com base no tamanho de saudação da máquina virtual Olá provisionado com a imagem da VM Olá de uso de hardware do Azure. Mais detalhes sobre Olá computação taxas podem ser encontradas no hello [página de listagem de VM no hello Azure Marketplace ](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Outras versões do hello máquina de Virtual de ciência de dados
Um [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) imagem também está disponível, com muitos Olá mesmo ferramentas como Olá imagem CentOS mais estruturas de aprendizado. Uma imagem do [Windows](machine-learning-data-science-provision-vm.md) também está disponível.

## <a name="prerequisites"></a>Pré-requisitos
Antes de criar uma máquina Virtual de ciência de dados de Linux, você deve ter o seguinte hello:

* **Uma assinatura do Azure**: um, consulte tooobtain [avaliação gratuita do Azure obter](https://azure.microsoft.com/free/).
* **Uma conta de armazenamento do Azure**: um, consulte toocreate [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Como alternativa, a conta de armazenamento de saudação pode ser criada como parte do processo de saudação de criação de saudação VM, se você não quiser toouse uma conta existente.

## <a name="create-your-linux-data-science-virtual-machine"></a>Criar sua Máquina Virtual de Ciência de Dados Linux
Aqui está Olá etapas toocreate uma instância do hello máquina de Virtual de ciência de dados do Linux:

1. Navegue de máquina virtual de toohello no hello [portal do Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vmlinuxdsvm).
2. Clique em **criar** (na parte inferior da saudação) toobring Assistente hello.![ Configurar-data-ciência-vm](./media/machine-learning-data-science-linux-dsvm-intro/configure-linux-data-science-virtual-machine.png)
3. Olá seções a seguir fornece entradas Olá para cada uma das etapas Olá no Assistente de saudação (enumerados no hello direito da saudação anterior figura) usado toocreate Olá máquina de Virtual de ciência de dados do Microsoft. Aqui estão Olá entradas necessárias tooconfigure cada destas etapas:
   
   a. **Noções básicas**:
   
   * **Nome**: o nome do servidor de ciência de dados que você está criando.
   * **Nome de Usuário**: primeira ID de entrada da conta.
   * **Senha**: primeira senha da conta (você pode usar a chave pública SSH, em vez de senha).
   * **Assinatura**: se você tiver mais de uma assinatura, selecione Olá um no qual Olá máquina é toobe criadas e cobradas. Você deve ter privilégios de criação de recurso nessa assinatura.
   * **Grupo de Recursos**: é possível criar um novo grupo ou usar um existente.
   * **Local**: Olá selecione data center que é mais apropriado. Geralmente, é Olá data center que tem a maioria dos seus dados, ou é o local físico mais próximo do tooyour para acesso de rede mais rápido.
   
   b. **Tamanho**:
   
   * Selecione um dos tipos de servidor de saudação que atenda aos seus requisitos funcionais e restrições de custo. Selecione **exibir tudo** toosee mais opções de tamanhos de VM.
   
   c. **Configurações**:
   
   * **Tipo de disco**: escolha **Premium** se você preferir uma SSD (unidade de estado sólido). Caso contrário, escolha **Standard**.
   * **Conta de armazenamento**: você pode criar uma nova conta de armazenamento do Azure em sua assinatura, ou use uma existente no hello mesmo local que foi escolhido no hello **Noções básicas sobre** etapa do Assistente de saudação.
   * **Outros parâmetros**: na maioria dos casos, você apenas usar valores padrão de saudação. valores não padrão de tooconsider, passe o mouse sobre o link de informação Olá para ajudam em campos específicos de saudação.
   
   d. **Resumo**:
   
   * Verifique se todas as informações inseridas estão corretas.
   
   e. **Comprar**:
   
   * toostart Olá provisionamento, clique em **comprar**. Um link será fornecido toohello termos de transação de saudação. Olá VM não tem quaisquer encargos adicionais além da computação Olá para tamanho do servidor de saudação escolhida na Olá **tamanho** etapa.

saudação de provisionamento deve levar cerca de 10 a 20 minutos. status de saudação do provisionamento de saudação é exibido na Olá portal do Azure.

## <a name="how-tooaccess-hello-linux-data-science-virtual-machine"></a>Como tooaccess Olá máquina de Virtual de ciência de dados do Linux
Depois de Olá que VM é criada, você pode entrar tooit usando o SSH. Usar as credenciais de conta de saudação que você criou no hello **Noções básicas de** seção da etapa 3 para a interface de shell do texto de saudação. No Windows, você pode baixar uma ferramenta de cliente SSH como o [Putty](http://www.putty.org). Se você preferir uma área de trabalho gráfica (X Windows System), você pode usar X11 Putty de encaminhamento ou instalar Olá X2Go cliente.

> [!NOTE]
> cliente Olá X2Go realizadas significativamente melhor do que X11 encaminhamento no teste. É recomendável usar o cliente de X2Go Olá para uma interface gráfica de área de trabalho.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Instalando e configurando o cliente X2Go
Olá VM Linux já está provisionada com servidor X2Go e conexões de cliente tooaccept pronto. tooconnect toohello desktop gráfica da VM do Linux, Olá no seu cliente a seguir:

1. Baixar e instalar o cliente Olá X2Go para sua plataforma de cliente de [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Execute o cliente Olá X2Go e selecione **nova sessão**. Ele abrirá uma janela de configuração com várias guias. Digite hello parâmetros de configuração a seguir:
   * **Guia Sessão**:
     * **Host**: nome de host de saudação ou endereço IP do seu VM de ciência de dados do Linux.
     * **Logon**: nome de usuário no hello VM do Linux.
     * **Porta SSH**: deixar 22, valor padrão de saudação.
     * **Tipo de sessão**: alteração Olá valor tooXFCE. No momento Olá VM Linux suporta apenas a área de trabalho XFCE.
   * **Guia de mídia**: você pode desativar som suporte e se você não precisa toouse de impressão de cliente-los.
   * **Pastas compartilhadas**: diretórios de suas máquinas cliente montadas em Olá VM do Linux, adicione diretórios da máquina cliente Olá que você deseja tooshare com hello VM nesta guia.

Depois de entrar no toohello VM usando o cliente do SSH hello ou área de trabalho gráfica por meio do cliente X2Go Olá XFCE, você está pronto toostart usando as ferramentas de saudação que são instaladas e configuradas no hello VM. Em XFCE, você pode ver os atalhos de aplicativos do menu e ícones da área de trabalho para muitas das ferramentas de saudação.

## <a name="tools-installed-on-hello-linux-data-science-virtual-machine"></a>Ferramentas instaladas no hello máquina de Virtual de ciência de dados do Linux
### <a name="microsoft-r-server"></a>Servidor R da Microsoft
R é uma das linguagens mais populares de saudação para análise de dados e aprendizado de máquina. Se você quiser toouse R para sua análise, Olá VM tem o Microsoft R Server (SRTA) com hello Microsoft R Open (MRO) e a biblioteca de Kernel de matemática (MKL). Olá MKL otimiza as operações matemáticas comuns em algoritmos analíticos. MRO é de 100% compatível com CRAN R e qualquer uma das bibliotecas de saudação R publicadas no CRAN pode ser instalado em Olá MRO. O MRS fornece dimensionamento e operacionalização de modelos R em serviços Web. Você pode editar seus programas de R em um dos editores de padrão de saudação, como RStudio, vi, Emacs ou gedit. Se você estiver usando o editor de Emacs Olá, observe que esse pacote de Emacs Olá ESS (Emacs fala estatísticas), que simplifica o trabalho com arquivos de R no editor de Emacs hello, foi pré-instalado.

console toolaunch R, basta digitar **R** no shell de saudação. Isso leva ambiente interativo tooan. toodevelop seu programa de R, você normalmente usa um editor como Emacs vi ou gedit e, em seguida, executar scripts de saudação no R. Com o RStudio, você tem um gráfico completo toodevelop de ambiente IDE seu programa de R.

Também há um script R para você Olá tooinstall [pacotes R de 20 principais](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) se desejar. Esse script pode ser executado depois que estiverem na interface interativa Olá R, que pode ser inserido (conforme mencionado) digitando **R** no shell de saudação.  

### <a name="python"></a>Python
Para o desenvolvimento com Python, as distribuições 2.7 e 3.5 do Anaconda Python foram instaladas. Essa distribuição contém Olá Python junto com cerca de 300 hello mais populares matemática, engenharia e dados de análise de pacotes de base. Você pode usar os editores de texto saudação padrão. Além disso, você pode usar o Spyder, um IDE do Python que é fornecido com distribuições do Anaconda Python. O Spyder precisa de uma área de trabalho gráfica ou de encaminhamento X11. Um atalho tooSpyder é fornecido na área de trabalho gráfica hello.

Como temos Python 2.7 e 3.5, você precisa toospecifically ativar versão do Python Olá desejado (conda ambiente) você deseja toowork em Olá a sessão atual. o processo de ativação Olá define a versão desejada de toohello variável do caminho de saudação do Python.

ambiente de conda em Olá Python 2.7 tooactivate, execute o seguinte de saudação do shell hello:

    source /anaconda/bin/activate root

O Python 2.7 está instalado em */anaconda/bin*.

ambiente de conda em Olá 3.5 Python tooactivate, execute o seguinte de saudação do shell hello:

    source /anaconda/bin/activate py35


O Python 3.5 está instalado em */anaconda/envs/py35/bin*.

tooinvoke uma sessão interativa do Python, basta digitar **python** no shell de saudação. Se você estiver em uma interface gráfica ou ter X11 encaminhamento de conjunto de backup, você pode digitar **pycharm** toolaunch Olá PyCharm Python IDE.

bibliotecas adicionais de Python tooinstall, você precisa toorun ```conda``` ou ````pip```` em sudo de comando e forneça o caminho completo do Gerenciador de pacotes do Python hello (conda ou pip) tooinstall toohello Python ambiente correto. Por exemplo:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Notebook Jupyter
Olá distribuição Anaconda também vem com um bloco de anotações do Jupyter, um código de tooshare do ambiente e análise. anotações do Jupyter Olá é acessada por meio de JupyterHub. Entre usando seu nome de usuário e senha locais do Linux.

servidor de notebook Jupyter Olá pré-configurada com Python 2, 3 de Python e kernels R. Há um ícone de área de trabalho chamado "Anotações do Jupyter" toolaunch Olá navegador tooaccess Olá notebook server. Se você estiver usando Olá VM por meio do cliente SSH ou X2Go, você também pode visitar [https://localhost:8000 /](https://localhost:8000/) tooaccess Olá servidor de notebook Jupyter.

> [!NOTE]
> Continue se você obtiver quaisquer avisos de certificado.
> 
> 

Você pode acessar o servidor de notebook Jupyter Olá de qualquer host. Basta digitar *https://\<endereço IP ou nome DNS da VM\>:8000/*

> [!NOTE]
> Porta 8000 é aberta no firewall de saudação por padrão quando Olá VM é provisionada.
> 
> 

Podemos empacotar blocos de anotações do exemplo – Python em um e outro em R. Você pode ver exemplos de toohello link Olá na home page do hello notebook após a autenticação de anotações do Jupyter toohello usando seu nome de usuário local do Linux e a senha. Você pode criar um novo bloco de anotações selecionando **novo**e, em seguida, kernel de idioma apropriado hello. Se você não vir Olá **novo** , clique em Olá **Jupyter** ícone Olá toogo esquerda superior toohello home page de servidor de notebook hello.

### <a name="apache-spark-standalone"></a>Apache Spark autônomo 
Uma instância autônoma do Apache Spark foi pré-instalado no hello toohelp Linux DSVM desenvolver aplicativos do Spark localmente primeiro antes de testar e implantar em clusters grandes. Você pode executar programas PySpark por meio do kernel do Jupyter hello. Quando você abrir Jupyter e botão de "Novo" Olá, você verá uma lista de kernels disponíveis. Olá "Spark – Python" é Olá PySpark kernel permite que você crie Spark usando linguagem Python. Você também pode usar um IDE Python como PyCharm ou Spyder toobuild você despertar programa. Como isso é uma instância autônoma, pilha de Spark Olá é executado dentro de saudação chamando o programa cliente. Isso torna mais rápido e mais fácil problemas de tootroubleshoot com toodeveloping em um cluster Spark. 

Um bloco de anotações de PySpark de exemplo é fornecido no Jupyter que você pode encontrar no diretório de "SparkML" hello no diretório de base de saudação do Jupyter ($HOME/anotações/SparkML/pySpark). 

Se você estiver programando em R para Spark, use o Microsoft R Server, SparkR ou sparklyr. 

Antes de executar no contexto do Spark no Microsoft R Server, é necessário toodo um um tempo instalação etapa tooenable um único nó local Hadoop HDFS e uma instância de Yarn. Por padrão, os serviços Hadoop são instalados mas desabilitados em Olá DSVM. Em ordem tooenable, é necessário toorun Olá seguir comandos como Olá raiz primeira vez:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Você pode parar Olá Hadoop serviços relacionados quando você não precisa deles, executando ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` um exemplo que demonstra como SRTA toodevelop e teste no contexto do Spark remoto (que é a instância do Spark Olá independente em Olá DSVM) é fornecido e está disponível em Olá `/dsvm/samples/MRS` directory. 

### <a name="ides-and-editors"></a>IDEs e editores
Você tem a opção de vários editores de código. Isso inclui vi/VIM, Emacs, gEdit, PyCharm, RStudio, Eclipse e IntelliJ. gEdit, Eclipse, IntelliJ, RStudio e PyCharm são editores gráficos e você precisa toobe conectado tooa toouse gráficos de área de trabalho-los. Esses editores tem área de trabalho e aplicativo toolaunch de atalhos de menu-los.

**VIM** e **Emacs** são editores baseados em texto. Em Emacs, podemos ter instalado um pacote complementar chamado Emacs fala estatísticas (ESS) que facilita o trabalho com R no editor de Emacs hello. Mais informações podem ser encontradas em: [ESS](http://ess.r-project.org/).

**Eclipse** é um IDE de software livre, extensível e que dá suporte a vários idiomas. edição de desenvolvedores de Java Olá é instância Olá Olá VM instalada. Plug-ins estão disponíveis para vários idiomas populares que podem ser o ambiente de saudação tooextend instalado. Também temos um plug-in instalado no Eclipse chamado **Kit de Ferramentas para Eclipse do Azure**. Ele permite toocreate, desenvolver, testar e implantar aplicativos do Azure usando o ambiente de desenvolvimento do Eclipse Olá que oferece suporte a idiomas como Java. Também há um **SDK do Azure para Java** que permite acesso toodifferent serviços do Azure de dentro de um ambiente Java. É possível encontrar mais informações sobre o kit de ferramentas do Azure para Eclipse em [Kit de ferramentas do Azure para Eclipse](../azure-toolkit-for-eclipse.md).

**Látex** é instalado por meio do pacote de texlive Olá junto com um complemento de Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) pacote, que simplifica a criação de seus documentos látex dentro de Emacs.  

### <a name="databases"></a>Bancos de dados
#### <a name="postgres"></a>Postgres
banco de dados de código-fonte aberto Olá **Postgres** está disponível no hello VM, com serviços Olá em execução e initdb já foi concluída. Você ainda precisa usuários e bancos de dados toocreate. Para obter mais informações, consulte Olá [Postgres documentação](https://www.postgresql.org/docs/).  

#### <a name="graphical-sql-client"></a>Cliente gráfico do SQL
**Esquilo SQL**, um cliente SQL gráfico, foi fornecido tooconnect toodifferent bancos de dados (como Microsoft SQL Server, Postgres e MySQL) e consultas SQL toorun. Você pode executar isso em uma sessão de área de trabalho gráfica (usando o cliente de X2Go hello, por exemplo). tooinvoke esquilo SQL, você pode iniciá-lo do ícone Olá na área de trabalho de saudação ou executar Olá comando a seguir no shell de saudação.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Antes de saudação primeiro uso, configurar os drivers e os aliases de banco de dados. drivers JDBC Olá estão localizados em:

*/usr/share/java/jdbcdrivers*

Para saber mais, confira [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Ferramentas de linha de comando para acessar o Microsoft SQL Server
pacote de driver ODBC Olá para o SQL Server também vem com duas ferramentas de linha de comando:

**BCP**: Olá bcp copia dados entre uma instância do Microsoft SQL Server e um arquivo de dados em um formato especificado pelo usuário. utilitário bcp de saudação pode ser usado tooimport grandes números de novas linhas em tabelas do SQL Server ou tooexport dados de tabelas para arquivos de dados. tooimport dados em uma tabela, você deve usar um arquivo de formato criado para aquela tabela ou entender a estrutura da tabela hello e tipos de saudação de dados que são válidos para suas colunas hello.

Para saber mais, confira [Conectando-se com o bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**Sqlcmd**: você pode digitar instruções Transact-SQL com o utilitário sqlcmd hello, bem como os procedimentos de sistema e arquivos no prompt de comando de saudação do script. Esse utilitário usa ODBC tooexecute Transact-SQL lotes.

Para saber mais, confira [Conectando-se com o sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Há algumas diferenças nesse utilitário entre as plataformas Linux e Windows. Consulte a documentação de saudação para obter detalhes.
> 
> 

#### <a name="database-access-libraries"></a>Bibliotecas de acesso do banco de dados
Bibliotecas estão disponíveis em bancos de dados tooaccess R e Python.

* Em R, Olá **RODBC** pacote ou **dplyr** pacote permite que você tooquery ou executar instruções SQL no servidor de banco de dados de saudação.
* Em Python, Olá **pyodbc** biblioteca fornece acesso de banco de dados com ODBC como Olá camada subjacente.  

tooaccess **Postgres**:

* De r: Use o pacote de saudação **RPostgreSQL**.
* Saudação de uso do Python: **psycopg2** biblioteca.

### <a name="azure-tools"></a>Ferramentas do Azure
Olá ferramentas do Azure a seguir é instalado no hello VM:

* **Interface de linha de comando do Azure**: hello CLI do Azure permite que você toocreate e gerenciar recursos do Azure por meio de comandos de shell. tooinvoke Olá ferramentas do Azure, basta digitar **do azure ajuda**. Para obter mais informações, consulte Olá [página da documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Explorer**: Microsoft Azure Storage Explorer é uma ferramenta gráfica que é usado toobrowse por meio de objetos de saudação que você tenha armazenado em sua conta de armazenamento do Azure e o download e tooupload tooand de dados de blobs do Azure. Você pode acessar o Gerenciador de armazenamento do ícone de atalho da área de trabalho de saudação. Você pode invocá-lo de um prompt do shell digitando **StorageExplorer**. Você precisa toobe entrou em um cliente X2Go, ou tiver X11 encaminhamento de conjunto de backup.
* **Bibliotecas do Azure**: Olá seguir estão algumas bibliotecas pré-instalados hello.
  
  * **Python**: Olá das bibliotecas relacionadas ao Azure em Python instalados **azure**, **azureml**, **pydocumentdb**, e **pyodbc** . Com hello primeiro três bibliotecas, você pode acessar os serviços de armazenamento do Azure, aprendizado de máquina do Azure e banco de dados do Azure Cosmos (um banco de dados NoSQL no Azure). biblioteca de quarto Hello, pyodbc (junto com hello Microsoft ODBC driver para SQL Server), permite acesso tooSQL servidor, banco de dados do SQL Azure e o Azure SQL Data Warehouse do Python usando uma interface ODBC. Digite **lista pip** toosee todos Olá listados bibliotecas. Ser toorun-se de que esse comando em ambos os Olá Python 2.7 e 3.5 ambientes.
  * **R**: Olá relacionadas ao Azure bibliotecas em R instalados estão **AzureML** e **RODBC**.
  * **Java**: lista de saudação das bibliotecas de Java do Azure pode ser encontrada no diretório Olá **/dsvm/sdk/AzureSDKJava** em Olá VM. bibliotecas de chave Olá são Azure gerenciamento APIs, o banco de dados do Azure Cosmos e JDBC drivers de armazenamento e para o SQL Server.  

Você pode acessar Olá [portal do Azure](https://portal.azure.com) do navegador Firefox pré-instalados de saudação. Olá portal do Azure, você pode criar, gerenciar e monitorar recursos do Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
O aprendizado de máquina do Azure é um serviço de nuvem totalmente gerenciado que permite que você toobuild, implantar e compartilhar soluções de análise preditiva. Você compila seus modelos e experimentos do Azure Machine Learning Studio. Pode ser acessado de um navegador da web na máquina de virtual de ciência de dados Olá visitando [aprendizado de máquina do Microsoft Azure](https://studio.azureml.net).

Depois que você entra no tooAzure estúdio de aprendizado de máquina, você tem acesso tooan experimentação tela onde você pode criar um fluxo lógico para algoritmos de aprendizado de máquina hello. Você também tem as anotações do Jupyter tooa acesso hospedadas no aprendizado de máquina do Azure e pode funcionar perfeitamente com experiências de saudação no estúdio de aprendizado de máquina. Colocar os modelos que você criou encapsulando-os em uma interface de serviço web de aprendizado de máquina hello. Isso permite que clientes escritos em qualquer previsões tooinvoke de idioma de modelos de aprendizado de máquina hello. Para obter mais informações, consulte Olá [documentação de aprendizado de máquina](https://azure.microsoft.com/documentation/services/machine-learning/).

Você pode também criar seus modelos em R ou Python no hello VM e, em seguida, implantá-lo em produção em aprendizado de máquina do Azure. Podemos instalou bibliotecas de R (**AzureML**) e Python (**azureml**) tooenable essa funcionalidade.

Para obter informações sobre como toodeploy modelos em R e Python no aprendizado de máquina do Azure, consulte [dez coisas que você pode fazer na máquina Virtual de ciência de dados de saudação](machine-learning-data-science-vm-do-ten-things.md) (em particular, Olá seção "criar modelos usando o R ou Python e Operacionalizá-los usando o aprendizado de máquina do Azure").

> [!NOTE]
> Estas instruções foram desenvolvidas para a versão do Windows hello de saudação VM de ciência de dados. Mas informações Olá fornecidas sobre a implantação de modelos tooAzure aprendizado de máquina são aplicável toohello VM do Linux.
> 
> 

### <a name="machine-learning-tools"></a>Ferramentas de Machine Learning
Olá VM vem com alguns algoritmos que foram previamente compilados e previamente instalados localmente e ferramentas de aprendizado de máquina. Estão incluídos:

* **CNTK** (Kit de Ferramentas de Rede Computacional da Microsoft Research): um software de aprendizado aprofundado.
* **Vowpal Wabbit**: um algoritmo de aprendizado rápido online.
* **xgboost**: uma ferramenta que fornece algoritmos de árvore aumentados e otimizados.
* **Python**: o Anaconda Python é fornecido com os algoritmos de aprendizado de máquina com bibliotecas como Scikit-learn. Você pode instalar outras bibliotecas usando Olá `pip install` comando.
* **R**: uma rica biblioteca de funções de aprendizado de máquina está disponível para R. Algumas das bibliotecas de saudação previamente instalados são lm, glm, randomForest, rpart. Outras bibliotecas podem ser instaladas, executando:
  
        install.packages(<lib name>)

Eis algumas informações adicionais sobre Olá primeiro três ferramentas de aprendizado de máquina na lista de saudação.

#### <a name="cntk"></a>CNTK
Este é um kit de ferramentas de aprendizado aprofundado de software livre. Ele é uma ferramenta de linha de comando (cntk) e já está no caminho de saudação.

toorun um exemplo básico, execute Olá comandos no shell Olá a seguir:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Para obter mais informações, consulte Olá seção CNTK [GitHub](https://github.com/Microsoft/CNTK)e hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit é um sistema de aprendizado de máquina rápido que usa técnicas como online, hash, allreduce, reduções, learning2search, ativo e aprendizado interativo.

ferramenta de saudação toorun em um exemplo muito básico, Olá a seguir:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Há outras demonstrações maiores nesse diretório. Para obter mais informações sobre VW, consulte [essa seção do GitHub](https://github.com/JohnLangford/vowpal_wabbit)e hello [wiki Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>XGBoost
Essa é uma biblioteca que é projetada e otimizada para algoritmos aumentados (de árvore). Olá objetivo essa biblioteca é toopush limites de computação Olá de extremos de toohello máquinas necessário tooprovide aumento da árvore de larga escala escalonável, portátil e precisas.

Ele é fornecido como uma linha de comando, bem como uma biblioteca do R.

toouse nessa biblioteca em R, você pode iniciar uma sessão interativa de R (apenas digitando **R** no shell de saudação) e o carregamento da biblioteca hello.

Aqui está um exemplo simples, que você pode executar no prompt do R:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

linha de comando do toorun Olá xgboost, aqui estão Olá tooexecute de comandos do shell hello:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Um arquivo. Model é gravado toohello diretório especificado. Mais informações sobre este exemplo de demonstração podem ser encontradas [no GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Para obter mais informações sobre xgboost, consulte Olá [página de documentação xgboost](https://xgboost.readthedocs.org/en/latest/)e sua [repositório GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Rattle (Olá **R** **um**nalytical **T**ferramenta **T**o **L**ganhar **E** asily) usa modelagem e exploração de dados baseadas em GUI. Apresenta estatísticas e resumos visual dos dados, transformações que podem ser modelados prontamente, compilações supervisionados e supervisionados modelos de dados de saudação, apresenta Olá desempenho dos modelos graficamente e conjuntos de dados novo pontuações. Ela também gera o código de R, replicando as operações de saudação em Olá da interface do usuário que podem ser executadas diretamente em R ou usadas como um ponto de partida para análise posterior.

toorun chocalho, você precisa toobe em uma gráfico da área de trabalho sessão de entrada. No terminal hello, digite ```R``` tooenter ambiente de saudação R. No prompt de saudação R, digite Olá comandos a seguir:

    library(rattle)
    rattle()

Agora, uma interface gráfica é aberta com um conjunto de guias. Aqui estão Olá início rápido etapas chocalho necessário toouse um conjunto de dados de tempo de exemplo e criar um modelo. Em algumas das etapas de saudação abaixo, você está tooautomatically solicitados a instalar e carregar alguns pacotes de R necessários que não ainda estão no sistema de saudação.

> [!NOTE]
> Se você não tiver o pacote de saudação do access tooinstall no diretório de sistema do hello (Olá padrão), você verá um prompt no seu console janela tooinstall pacotes tooyour pessoal biblioteca R. Caso veja essas solicitações, responda *s* .
> 
> 

1. Clique em **Executar**.
2. Uma caixa de diálogo é exibido, perguntando se você deseja que o conjunto de dados de clima toouse Olá exemplo. Clique em **Sim** exemplo hello de tooload.
3. Clique em Olá **modelo** guia.
4. Clique em **Execute** toobuild uma árvore de decisão.
5. Clique em **desenhar** toodisplay árvore de decisão de saudação.
6. Clique em Olá **floresta** botão de opção e, em seguida, clique em **Execute** toobuild aleatória de floresta.
7. Clique em Olá **avaliar** guia.
8. Clique em Olá **risco** botão de opção e, em seguida, clique em **Execute** toodisplay dois gráficos de desempenho de risco (cumulativo).
9. Clique em Olá **Log** saudação do guia tooshow gerar código de R para Olá operações precedentes.
   (Devido a erro tooa na versão atual de saudação do chocalho, você precisa tooinsert um  *#*  caractere na frente do *exportar este log...*  no texto de saudação do log hello.)
10. Clique em Olá **exportar** arquivo de script do botão toosave Olá R chamado *weather_script. R* pasta base toohello.

Você pode sair chocalho e R. Agora você pode modificar o script de R Olá gerado ou usá-la como é toorun-lo a qualquer momento toorepeat tudo o que foi feito em Olá Rattle da interface do usuário. Especialmente para iniciantes em R, isso é uma maneira fácil tooquickly fazer análise e aprendizado em uma interface gráfica simple, ao gerar automaticamente o código em R toomodify de máquina e/ou saber mais.

## <a name="next-steps"></a>Próximas etapas
Veja como você pode continuar seu aprendizado e exploração:

* Olá [ciência de dados na máquina de Virtual de ciência de dados do Linux de saudação](machine-learning-data-science-linux-dsvm-walkthrough.md) passo a passo mostra como tooperform ciência de dados comum várias tarefas com hello VM de ciência de dados do Linux provisionado aqui. 
* Explore Olá várias ferramentas de ciência de dados em Olá ciência de dados VM experimentando ferramentas Olá descritas neste artigo. Você também pode executar *informações de mais dsvm* no shell de saudação em máquina virtual de saudação para um Introdução e ponteiros toomore obter informações básicas sobre ferramentas Olá Olá VM instalado.  
* Saiba como soluções analíticos de ponta a ponta de toobuild sistematicamente usando Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Visite Olá [Cortana análise galeria](http://gallery.cortanaanalytics.com) para análise de dados e aprendizado de máquina exemplos Olá que use Cortana Analytics Suite.

