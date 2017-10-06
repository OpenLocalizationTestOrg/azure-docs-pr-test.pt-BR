---
title: "Olá aaaProvision máquina de Virtual de ciência de dados do Microsoft | Microsoft Docs"
description: "Configure e crie uma Máquina Virtual de Ciência de Dados no Azure para realizar a análise e o aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Provisionar Olá máquina de Virtual de ciência de dados Microsoft
Olá máquina de Virtual de ciência de dados Microsoft é uma imagem de máquina virtual (VM) do Windows Azure previamente instalado e configurado com diversas ferramentas populares que são normalmente usadas para análise de dados e aprendizado de máquina. Olá ferramentas incluídas são:

* Microsoft R Server Developer Edition
* Distribuição do Anaconda Python
* Bloco de anotações do Jupyter (com R, kernels Python)
* Visual Studio Community Edition
* Power BI Desktop
* SQL Server 2016 Developer Edition
* Ferramentas Machine learning e Data Analytics
  * [CNTK (Kit de Ferramentas de Rede Computacional)](https://github.com/Microsoft/CNTK): um software de aprendizado aprofundado da Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): um sistema de machine learning rápido com suporte a técnicas como online, hash, allreduce, reduções, learning2search, ativo e aprendizado interativo.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): uma ferramenta que fornece implementação de árvore aumentada rápida e precisa.
  * [Rattle](http://rattle.togaware.com/) (Olá ferramenta analíticos R tooLearn facilmente): uma ferramenta que facilita a introdução à análise de dados e de máquina em R fácil, com a exploração de dados baseado em GUI de aprendizado e modelagem com a geração automática de código R.
  * [mxnet](https://github.com/dmlc/mxnet): uma estrutura de aprendizado profunda criada para eficiência e flexibilidade
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): um software de mineração de dados visual e machine learning em Java.
  * [Apache Drill](https://drill.apache.org/): um Mecanismo de consulta SQL, livre de esquema, para Hadoop, NoSQL e Armazenamento em Nuvem.  Dá suporte a ODBC e JDBC tooenable interfaces consultando NoSQL e arquivos de ferramentas padrão de BI como Tableau, Excel, Power BI.
* Bibliotecas em R e Python para uso em Azure Machine Learning e outros serviços do Azure
* Git incluindo toowork Git Bash com repositórios de código de origem, incluindo GitHub, Visual Studio Team Services
* Portas do Windows de vários utilitários de linha de comando populares do Linux (incluindo awk, sed, perl, grep, find, wget, curl, etc.) acessíveis pelo prompt de comando. 

Fazer a ciência de dados envolve a iteração em uma sequência de tarefas:

1. Localizar, carregar e pré-processar dados
2. Compilar e testar modelos
3. Implantando modelos de saudação para consumo de aplicativos inteligentes

Cientistas de dados usam uma variedade de ferramentas toocomplete essas tarefas. Ele pode ser bastante demorada toofind versões apropriadas de saudação do software Olá e, em seguida, baixar e instalá-los. Olá máquina de Virtual de ciência de dados do Microsoft pode facilitar essa carga, fornecendo uma imagem de prontos para uso que pode ser provisionada no Azure com todas as ferramentas populares várias previamente instalado e configurado. 

Olá máquina de Virtual de ciência de dados do Microsoft impulsiona seu projeto de análise. Ele permite toowork nas tarefas em vários idiomas, incluindo R, Python, SQL e c#. Visual Studio fornece um IDE toodevelop e testar seu código que é fácil toouse. Olá incluídos na VM de saudação do SDK do Azure permite que você toobuild seus aplicativos usando vários serviços na plataforma de nuvem da Microsoft. 

Não há encargos de software para esta imagem da VM de ciência de dados. Você só paga pelo taxas de uso do Azure Olá quais dependentes de tamanho de saudação da máquina virtual de saudação que provisionar. Mais detalhes sobre Olá computação taxas podem ser encontradas no hello seção de detalhes de preços Olá [máquina de Virtual de ciência de dados](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) página. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Outras versões do hello máquina de Virtual de ciência de dados
Um [CentOS](machine-learning-data-science-linux-dsvm-intro.md) imagem também está disponível, com muitos Olá mesmo ferramentas como Olá a imagem do Windows. Uma imagem do [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) também está disponível, com muitas ferramentas semelhantes além de estruturas de aprendizado aprofundado.

## <a name="prerequisites"></a>Pré-requisitos
Antes de criar uma máquina Virtual de ciência de dados de Microsoft, você deve ter o seguinte hello:

* **Uma assinatura do Azure**: um, consulte tooobtain [avaliação gratuita do Azure obter](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Uma conta de armazenamento do Azure**: um, consulte toocreate [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Como alternativa, a conta de armazenamento de saudação pode ser criada como parte do processo de saudação de criação de saudação VM se você não quiser toouse uma conta existente.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Criar sua Máquina Virtual de Ciência de Dados da Microsoft
Aqui está Olá etapas toocreate uma instância do hello máquina de Virtual de ciência de dados Microsoft:

1. Navegue de máquina virtual de toohello no [portal do Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Selecione Olá **criar** botão no hello inferior toobe levada em um assistente.![ Configurar-data-ciência-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Olá assistente usado toocreate Olá requer a máquina de Virtual de ciência de dados do Microsoft **entradas** para cada Olá **cinco etapas** enumerados na saudação à direita da figura. Aqui estão Olá entradas necessárias tooconfigure cada destas etapas:
   
   1. **Noções básicas**
      
      1. **Nome**: o nome do servidor de ciência de dados que você está criando.
      2. **Nome de Usuário**: ID de logon da conta de administrador.
      3. **Senha**: senha da conta de administrador.
      4. **Assinatura**: se você tiver mais de uma assinatura, selecione Olá um no qual Olá máquina é toobe criadas e cobradas.
      5. **Grupo de Recursos**: é possível criar um novo grupo ou usar um existente.
      6. **Local**: Olá selecione data center que é mais apropriado. Geralmente, é Olá data center que tem a maioria dos seus dados ou é o local físico mais próximo do tooyour para acesso de rede mais rápido.
   2. **Tamanho**: selecione um dos tipos de servidor de saudação que atenda aos seus requisitos funcionais e restrições de custo. Você pode obter mais opções de tamanhos de VM selecionando “Exibir Tudo”.
   3. **Configurações**:
      
      1. **Tipo de disco**: escolha Premium se você preferir uma SSD (unidade de estado sólido); caso contrário, escolha "Padrão".
      2. **Conta de armazenamento**: você pode criar uma nova conta de armazenamento do Azure em sua assinatura ou use uma existente no hello mesmo *local* que foi escolhido no hello **Noções básicas sobre** etapa do Assistente de saudação.
      3. **Outros parâmetros**: normalmente usar apenas valores padrão de saudação. Você pode focalizar link informativo de saudação para obter ajuda sobre campos específicos Olá caso você deseje que o uso de saudação do tooconsider de valores não padrão.
   4. **Resumo**: verifique se todas as informações inseridas estão corretas.
   5. **Comprar**: clique em **comprar** toostart Olá provisionamento. Um link será fornecido toohello termos de transação de saudação. Olá VM não tem quaisquer encargos adicionais além da computação Olá para tamanho do servidor de saudação escolhida na Olá **tamanho** etapa. 

> [!NOTE]
> saudação de provisionamento deve levar cerca de 10 a 20 minutos. status de saudação do provisionamento de saudação é exibido na Olá portal do Azure.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Como tooaccess Olá máquina de Virtual de ciência de dados Microsoft
Uma vez Olá VM é criada, você pode área de trabalho remota para ela usando credenciais de conta de administrador Olá configurada na saudação anterior **Noções básicas de** seção. 

Depois que a VM é criada e provisionada, você está pronto toostart usando as ferramentas de saudação que estão instaladas e configuradas. Há blocos do menu Iniciar e ícones de área de trabalho para muitas das ferramentas de saudação. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Como toocreate uma senha forte para Jupyter e início Olá servidor de notebook
Por padrão, o servidor de notebook Jupyter Olá é pré-configurado mas desabilitado no hello VM até que você defina uma senha Jupyter. toocreate uma senha forte para o servidor de notebook Jupyter Olá instalado na máquina hello, Olá execução seguinte comando em um prompt de comando no hello dados ciência da máquina Virtual ou clique duas vezes no atalho da área de trabalho hello, fornecemos chamado  **Definir senha de Jupyter & início** de uma conta de administrador da VM local.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Execute as mensagens de saudação e escolha uma senha forte quando solicitado.

Olá script anterior cria um hash de senha e o repositório no arquivo de configuração do Jupyter Olá localizado em: **C:\ProgramData\jupyter\jupyter_notebook_config.py** em nome do parâmetro hello ***c. NotebookApp.password***.

script Hello também permite e execute o servidor de Jupyter Olá no plano de fundo de saudação. Servidor Jupyter é criada como uma tarefa do windows hello Agendador de tarefas do WIndows chamado **Start_IPython_Notebook**.  Você pode ter toowait por alguns segundos depois de definir a senha de saudação antes de abrir o bloco de anotações de saudação em seu navegador. Consulte Olá seção intitulada **Jupyter Notebook** em como tooaccess Olá servidor de notebook Jupyter. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Ferramentas instaladas no hello máquina de Virtual de ciência de dados Microsoft

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Se você quiser toouse R para sua análise, Olá VM tem edição de desenvolvedor do Microsoft R Server instalada. O Microsoft R Server é uma plataforma de análise empresarial amplamente implementável com base em R e com suporte, escalonável e segura. Dando suporte a uma variedade de estatísticas de dados grande, modelagem de previsão e recursos de aprendizado de máquina, o R Server oferece suporte a toda a gama de análise – exploração, análise, visualização e modelagem hello. Usando e estendendo R de software livre, o Microsoft R Server é totalmente compatível com scripts R, funções e pacotes CRAN, tooanalyze dados em escala empresarial. Ele também aborda limitações de memória de saudação de R de código-fonte aberto adicionando paralelas e em partes de processamento de dados. Isso permite que você toorun análise em dados muito maiores do que o que couber na memória principal.  Visual Studio Community Edition está incluído na Olá que VM contém ferramentas de R Olá para extensão do Visual Studio que fornece um IDE completo para trabalhar com R. Você também pode baixar e usar outros IDEs, bem como [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Para o desenvolvimento com Python, as distribuições 2.7 e 3.5 do Anaconda Python foram instaladas. Essa distribuição contém Olá Python junto com cerca de 300 hello mais populares matemática, engenharia e dados de análise de pacotes de base. Você pode usar as ferramentas Python para Visual Studio (PTVS) que é instalado dentro de saudação Visual Studio 2015 Community edition ou uma saudação que IDEs agrupado com Anaconda como ocioso ou Spyder. Você pode iniciar um por meio de pesquisa na barra de pesquisa da saudação (**Win** + **S** chave).

> [!NOTE]
> Olá toopoint ferramentas Python para Visual Studio ao Anaconda Python 2.7 e 3.5, é necessário ambientes personalizado toocreate para cada versão. tooset esses caminhos de ambiente no hello Visual Studio 2015 Community Edition, navegue muito**ferramentas** -> **ferramentas Python** -> **Python ambientes** e, em seguida, clique em **+ personalizado**. 
> 
> 

O Anaconda Python 2.7 é instalado em C:\Anaconda e o Anaconda Python 3.5 é instalado em c:\Anaconda\envs\py35. Consulte a [documentação do PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para obter as etapas detalhadas. 

### <a name="jupyter-notebook"></a>Bloco de anotações do Jupyter
Distribuição anaconda também vem com um bloco de anotações do Jupyter, um código de tooshare do ambiente e análise. Um servidor de notebook Jupyter foi previamente configurado com os kernels do Python 2.7, Python 3.4, Python 3.5 e R. Há um ícone de área de trabalho denominado "tooaccess de navegador de anotações do Jupyter toolaunch Olá Olá servidor de Notebook. Se você estiver usando Olá VM por meio da área de trabalho remota, você também pode visitar [https://localhost:9999 /](https://localhost:9999/) tooaccess Olá servidor de notebook Jupyter quando conectado toohello VM.

> [!NOTE]
> Continue se você obtiver quaisquer avisos de certificado. 
> 
> 

Podemos empacotar vários blocos de anotações de exemplo em Python e em R. Olá Mostrar de blocos de anotações do Jupyter como toowork com o Microsoft R Server, SQL Server 2016 R Services (análise no banco de dados), Python, Microsoft cognitivas ToolKit (CNTK) para o aprendizado e outros do Azure tecnologias depois de fazer logon em tooJupyter. Você pode ver exemplos de toohello link Olá Olá notebook home page depois de autenticar o bloco de anotações do Jupyter toohello usando senha Olá criada em uma etapa anterior. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition instalado na VM de saudação. É uma versão gratuita do hello IDE popular da Microsoft que você pode usar para fins de avaliação e pequenas equipes. Você pode conferir Olá termos de licenciamento [aqui](https://www.visualstudio.com/support/legal/mt171547).  Abra o Visual Studio por duas vezes no ícone de área de trabalho hello ou Olá **iniciar** menu. Você também pode pesquisar programas com **Win** + **S** e inserindo “Visual Studio”. Nesse local, você pode criar projetos em linguagens como C#, Python, R e node.js. Plug-ins também são instalados que tornam mais conveniente toowork com serviços do Azure como o catálogo de dados do Azure, HDInsight do Azure (Hadoop, Spark) e Azure Data Lake. 

> [!NOTE]
> Você poderá receber uma mensagem informando que seu período de avaliação expirou. Insira suas credenciais de conta da Microsoft ou crie uma nova conta gratuita tooget acesso toohello Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
Uma versão de desenvolvedor do SQL Server 2016 com a análise do R Services toorun no banco de dados é fornecida em Olá VM. Os Serviços do R fornecem uma plataforma para desenvolver e implantar aplicativos inteligentes. Você pode usar a linguagem R avançada e poderosa hello e Olá muitos pacotes de modelos de toocreate de comunidade hello e gerar previsões para os dados do SQL Server. Você pode manter dados de análise de fechar toohello porque o idioma Olá R integrar o R Services (no banco de dados) com o SQL Server. Isso elimina os custos de saudação e riscos de segurança associados à movimentação de dados.

> [!NOTE]
> Olá SQL Server 2016 developer edition só pode ser usado para desenvolvimento e fins de teste. Você precisa de uma licença toorun-lo em produção. 
> 
> 

Você pode acessar Olá SQL server iniciando **SQL Server Management Studio**. O nome da VM é populado como nome do servidor de saudação. Use autenticação do Windows quando conectado como Olá administrador no Windows. Quando estiver no SQL Server Management Studio, você pode criar outros usuários, criar bancos de dados, importar dados e executar consultas SQL. 

análise de tooenable no banco de dados usando o Microsoft R, execute Olá após o comando como uma ação no SQL Server management studio após o logon como administrador do servidor de saudação. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>As tabelas
Várias ferramentas do Azure são instaladas no hello VM:

* Há um atalho da área de trabalho tooaccess documentação do SDK do Azure hello. 
* **AzCopy**: usado toomove dados dentro e fora de sua conta de armazenamento do Microsoft Azure. uso de toosee, tipo **Azcopy** um uso de saudação do prompt de comando toosee. 
* **Microsoft Azure Storage Explorer**: usado toobrowse por meio de objetos de saudação que você tenha armazenado em sua conta de armazenamento do Azure e transferência tooand de dados do armazenamento do Azure. Você pode digitar **Storage Explorer** em pesquisa ou localize-o em Olá tooaccess do menu Iniciar do Windows essa ferramenta. 
* **Adlcopy**: usado toomove dados tooAzure Data Lake. uso de toosee, tipo **adlcopy** em um prompt de comando. 
* **dtui**: usado toomove tooand de dados do Azure Cosmos DB, um banco de dados NoSQL nuvem hello. Digite **dtui** no prompt de comando. 
* **Gateway de Gerenciamento de Dados da Microsoft**: permite a movimentação de dados entre fontes de dados locais e a nuvem. É usado em ferramentas como o Azure Data Factory. 
* **Microsoft Azure Powershell**: uma ferramenta usada tooadminister seus recursos do Azure Olá Powershell linguagem de script também é instalada na sua VM. 

### <a name="power-bi"></a>Power BI
toohelp criar painéis e visualizações excelentes, hello **Power BI Desktop** foi instalado. Use esses dados de toopull ferramenta de origens diferentes, tooauthor seus painéis e relatórios e toopublish-los toohello nuvem. Para obter informações, consulte Olá [Power BI](http://powerbi.microsoft.com) site. Você pode encontrar a área de trabalho do Power BI no menu de início de saudação. 

> [!NOTE]
> Você precisa de um tooaccess de conta do Office 365 Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Ferramentas de desenvolvimento adicionais da Microsoft
Olá [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx) pode ser usado toodiscover e fazer o download de outras ferramentas de desenvolvimento da Microsoft. Também é uma ferramenta de toohello atalho fornecida na área de trabalho de máquina de Virtual de ciência de dados do Microsoft hello.  

## <a name="important-directories-on-hello-vm"></a>Diretórios importantes em Olá VM
| Item | Diretório |
| --- | --- |
| Configurações de servidor do bloco de anotações do Jupyter |C:\ProgramData\jupyter |
| Diretório base de amostras do Bloco de Anotações do Jupyter |c:\dsvm\notebooks |
| Outras amostras |c:\dsvm\samples |
| Anaconda (padrão: Python 2.7) |c:\Anaconda |
| Ambiente do Anaconda Python 3.5 |c:\Anaconda\envs\py35 |
| Diretório de instância do R Server Autônomo (instância padrão do R baseada em R3.2.2) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| Diretório de instância do R Server no banco de dados (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Diretório de instância do Microsoft R Open (R3.3.1) |C:\Arquivos de Programas\Microsoft\MRO-3.3.1 |
| Ferramentas diversas |c:\dsvm\tools |

> [!NOTE]
> Instâncias de Olá que Microsoft máquina de Virtual de ciência de dados criado antes 1.5.0 (antes de 3 de setembro de 2016) usadas uma estrutura de diretório ligeiramente diferente do especificado no hello anterior da tabela. 
> 
> 

## <a name="next-steps"></a>Próximas etapas
Aqui está alguns toocontinue etapas Avançar o aprendizado e a exploração. 

* Explore Olá várias ferramentas de ciência de dados na ciência de dados Olá VM clicando Olá menu Iniciar e fazer check-out Olá ferramentas listadas no menu de saudação.
* Navegue muito**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** para obter exemplos usando Olá RevoScaleR biblioteca em R que dá suporte à análise de dados em escala empresarial.  
* Leia o artigo Olá: [10 coisas que você pode fazer no hello Máquina Virtual de ciência de dados](http://aka.ms/dsvmtenthings)
* Saiba como toobuild tooend analíticos soluções fim sistematicamente usando Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Visite Olá [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com) para análise de dados e aprendizado de máquina exemplos Olá que use Cortana Intelligence Suite. Nós também fornecemos um ícone na Olá **iniciar** menu e na área de trabalho de saudação da Galeria de toothis Olá máquina virtual.

