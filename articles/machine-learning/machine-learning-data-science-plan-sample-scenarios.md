---
title: "aaaIdentify avançado cenários de análise para o aprendizado de máquina do Azure | Microsoft Docs"
description: "Selecione os cenários de saudação apropriados para fazer avançadas de análise preditiva com hello processo de ciência de dados de equipe."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Cenários para análises avançadas no Azure Machine Learning
Este artigo descreve vários Olá fontes de dados de exemplo e cenários de destino que podem ser tratados pelo Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md). Olá TDSP fornece uma abordagem sistemática para equipes toocollaborate na criação de aplicativos inteligentes. Olá apresentadas aqui ilustram opções disponíveis no fluxo de trabalho de processamento de dados de saudação que dependem de características de dados hello, locais de origem e repositórios de destino no Azure.

Olá **árvore de decisão** para selecionar os cenários de exemplo hello apropriado para seus dados e o objetivo é apresentada na última seção do hello.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Cada uma das seguintes seções de saudação apresenta um cenário de exemplo. Para cada cenário, são listados uma possível ciência de dados ou fluxo de análise avançada e os recursos de suporte do Azure.

> [!NOTE]
> **Para todos os seguintes cenários de saudação, você precisa:**
> <br/>
> 
> * [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md)
>   <br/>
> * 
            [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Cenário \#1: pequeno toomedium o conjunto de dados tabulares em um local de arquivos
![Arquivos locais toomedium pequeno][1]

#### <a name="additional-azure-resources-none"></a>Recursos adicionais do Azure: nenhum
1. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
2. Carregue um conjunto de dados.
3. Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados carregados.

## <a name="smalllocalprocess"></a>Cenário \#2: toomedium pequeno conjunto de dados de arquivos locais que exigem processamento
![Toomedium pequenos arquivos de locais com processamento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa o IPython Notebook.
2. Carregar o contêiner de armazenamento do Azure de tooan de dados.
3. Pré-processe e limpe dados no IPython Notebook, acessando dados no contêiner de armazenamento do Azure.
4. Transforme dados toocleaned, formato de tabela.
5. Salve os dados transformados nos blobs do Azure.
6. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
7. Ler dados de saudação de blobs do Azure usando Olá [importar dados] [ import-data] módulo.
8. Crie um fluxo experimental do Azure Machine Learning começando com os conjuntos de dados ingeridos.

## <a name="largelocal"></a>Cenário \#3: conjunto de dados grande em arquivos locais, com blobs do Azure como destino
![Arquivos locais grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa o IPython Notebook.
2. Carregar o contêiner de armazenamento do Azure de tooan de dados.
3. Pré-processe e limpe dados no IPython Notebook, acessando dados nos blobs do Azure.
4. Transforme dados toocleaned, formato de tabela, se necessário.
5. Explore dados e crie recursos conforme for necessário.
6. Extraia um exemplo de dados de pequeno a médio porte.
7. Salve dados de amostra de saudação em blobs do Azure.
8. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
9. Ler dados de saudação de blobs do Azure usando Olá [importar dados] [ import-data] módulo.
10. Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.

## <a name="smalllocaltodb"></a>Cenário \#4: toomedium pequeno conjunto de dados de arquivos locais, voltados para o SQL Server em uma máquina Virtual do Azure
![Toomedium pequenos arquivos locais tooSQL banco de dados no Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa SQL Server + IPython Notebook.
2. Carregar o contêiner de armazenamento do Azure de tooan de dados.
3. Pré-processe e limpe dados no contêiner de armazenamento do Azure usando o IPython Notebook.
4. Transforme dados toocleaned, formato de tabela, se necessário.
5. Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).
6. Carrega dados tooSQL banco de dados Server em execução em uma VM do Azure.
   
   Opção \#1: usar o SQL Server Management Studio.
   
   * Logon tooSQL VM do servidor
   * Execute o SQL Server Management Studio.
   * Crie o banco de dados e as tabelas de destino.
   * Use um em massa de saudação importar dados de saudação do tooload de métodos de arquivos de VM local.
   
   Opção \#2: usar o IPython Notebook – não é aconselhável para conjuntos de dados médios e maiores
   
   <!-- -->    
   * Use tooaccess de cadeia de caracteres de conexão do ODBC SQL Server na máquina virtual.
   * Crie o banco de dados e as tabelas de destino.
   * Use um em massa de saudação importar dados de saudação do tooload de métodos de arquivos de VM local.
7. Explore dados e crie recursos conforme necessário. Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação. Apenas Observe Olá consulta necessária toocreate-los.
8. Escolha um tamanho de amostra de dados, se necessário e/ou desejado.
9. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
10. Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo. Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.
11. Crie um fluxo experimental do Azure Machine Learning, começando com os conjuntos de dados ingeridos.

## <a name="largelocaltodb"></a>Cenário \#5: conjunto de dados grande em arquivos locais, com o SQL Server na VM do Azure
![Locais de arquivos grandes tooSQL banco de dados no Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.
2. Carregar o contêiner de armazenamento do Azure de tooan de dados.
3. (Opcional) Pré-processe e limpe os dados.
   
   a.  Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure
   
       blobs.
   
   b.  Transforme dados toocleaned, formato de tabela, se necessário.
   
   c.  Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).
4. Carrega dados tooSQL banco de dados Server em execução em uma VM do Azure.
   
   a.  Logon tooSQL VM do servidor.
   
   b.  Se os dados já não estiverem salvos, baixe arquivos de dados do Azure
   
       storage container toolocal-VM folder.
   
   c.  Execute o SQL Server Management Studio.
   
   d.  Crie o banco de dados e as tabelas de destino.
   
   e.  Use um em massa de saudação importar dados de saudação do tooload de métodos.
   
   f.  Se as junções de tabela são necessárias, crie índices tooexpedite junções.
   
   > [!NOTE]
   > Para carregamento mais rápido de tamanhos de dados grande, é recomendável que você crie tabelas particionadas e importar dados de saudação em paralelo em massa. Para obter mais informações, consulte [tooSQL de importação de dados paralela Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Explore dados e crie recursos conforme necessário. Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação. Apenas Observe Olá consulta necessária toocreate-los.
6. Escolha um tamanho de amostra de dados, se necessário e/ou desejado.
7. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
8. Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo. Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.
9. Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado

## <a name="largedbtodb"></a>Cenário \#6: conjunto de dados grande em um banco de dados do SQL Server local, com o SQL Server em uma Máquina Virtual do Azure como destino
![Grande tooSQL de local de banco de dados SQL banco de dados no Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa SQL Server e o servidor IPython Notebook.
2. Use um dos dados de saudação exportar dados de saudação do tooexport de métodos de arquivos de toodump do SQL Server.
   
   > [!NOTE]
   > Se você decidir toomove todos os dados do banco de dados de local de hello, uma alternativa (mais rápido) método toomove Olá banco de dados completo toothe instância do SQL Server no Azure. Ignorar dados de tooexport etapas hello, criar banco de dados e banco de dados de destino do carregamento/importar dados toohello e siga o método alternativo de saudação.
   > 
   > 
3. Carregar o contêiner de armazenamento de tooAzure de arquivos de despejo de memória.
4. Carregar Olá dados tooa de dados SQL Server em execução em uma máquina Virtual do Azure.
   
   a.  Logon toohello VM do SQL Server.
   
   b.  Baixe arquivos de dados de uma pasta de VM local de toohello de contêiner de armazenamento do Azure.
   
   c.  Execute o SQL Server Management Studio.
   
   d.  Crie o banco de dados e as tabelas de destino.
   
   e.  Use um em massa de saudação importar dados de saudação do tooload de métodos.
   
   f.  Se as junções de tabela são necessárias, crie índices tooexpedite junções.
   
   > [!NOTE]
   > Para carregamento mais rápido de tamanhos de dados grande, crie tabelas particionadas e toobulk importar Olá dados em paralelo. Para obter mais informações, consulte [tooSQL de importação de dados paralela Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Explore dados e crie recursos conforme necessário. Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação. Apenas Observe Olá consulta necessária toocreate-los.
6. Escolha um tamanho de amostra de dados, se necessário e/ou desejado.
7. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
8. Dados de leitura Olá diretamente do SQL Server usando Olá Olá [importar dados] [ import-data] módulo. Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.
9. Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Método alternativo toocopy um banco de dados completo de um tooAzure do SQL Server local banco de dados SQL
![Desanexe o banco de dados local e anexar tooSQL banco de dados no Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Recursos adicionais do Azure: Máquina Virtual do Azure (SQL Server/ servidor IPython Notebook)
tooreplicate Olá todo banco de dados SQL na VM do SQL Server, você deve copiar um banco de dados de tooanother de um servidor do local, supondo que esse banco de dados de saudação pode ficar temporariamente offline. Você pode fazer isso no hello Pesquisador de objetos do SQL Server Management Studio ou usando os comandos de Transact-SQL equivalentes hello.

1. Desanexe o banco de dados de saudação no local de origem hello. Para saber mais, veja [Desanexar um banco de dados](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. Na janela do Windows Explorer ou Prompt de comando do Windows, a saudação de cópia desanexado arquivo de banco de dados ou arquivos e arquivo de log ou local de destino de toohello de arquivos no hello VM do SQL Server no Azure.
3. Anexe a instância do SQL Server de destino do hello copiado arquivos toohello. Para saber mais, veja [Anexar um banco de dados](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Mover um Banco de Dados utilizando Desanexar e Anexar (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Cenário \#7: Big Data em arquivos locais, com um banco de dados Hive em clusters Hadoop do Azure HDInsight como destino
![Big Data no Hive local de destino][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Recursos adicionais do Azure: cluster Hadoop do Azure HDInsight e Máquina Virtual do Azure (servidor IPython Notebook)
1. Crie uma Máquina Virtual do Azure que executa o servidor IPython Notebook.
2. Personalize um cluster Hadoop do Azure HDInsight.
3. (Opcional) Pré-processe e limpe os dados.
   
   a.  Pré-processe e limpe dados no IPython Notebook, acessando dados do Azure
   
       blobs.
   
   b.  Transforme dados toocleaned, formato de tabela, se necessário.
   
   c.  Salvar os arquivos de dados local tooVM (bloco de anotações do IPython está em execução na máquina virtual, unidades locais Consulte tooVM drives).
4. Carregar o contêiner do cluster de Hadoop Olá selecionado na etapa 2 do hello padrão de toohello de dados.
5. Carregar o banco de dados do data tooHive no cluster Hadoop de HDInsight do Azure.
   
   a.  Faça logon no toohello o nó principal do cluster de Hadoop Olá
   
   b.  Abra Olá linha de comando do Hadoop.
   
   c.  Insira o diretório raiz da saudação Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.
   
   d.  Executar o banco de dados do hello Hive consultas toocreate e tabelas e carregar dados de tabelas de tooHive de armazenamento de blob.
   
   > [!NOTE]
   > Se dados saudação forem grandes, os usuários podem criar tabela de Hive Olá com partições. Em seguida, os usuários podem usar um `for` loop na saudação de linha de comando do Hadoop em dados de tooload de nó principal Olá Olá Hive tabela particionada por partição.
   > 
   > 
6. Explore dados e crie recursos conforme necessário na linha de comando do Hadoop. Observe que os recursos de saudação não necessário toobe materializada nas tabelas de banco de dados de saudação. Apenas Observe Olá consulta necessária toocreate-los.
   
   a.  Faça logon no toohello o nó principal do cluster de Hadoop Olá
   
   b.  Abra Olá linha de comando do Hadoop.
   
   c.  Insira o diretório raiz da saudação Hive pelo comando `cd %hive_home%\bin` na linha de comando do Hadoop.
   
   d.  Executar consultas de Hive Olá na linha de comando do Hadoop no nó de cabeçalho Olá dos dados de Olá Olá Hadoop cluster tooexplore e criar recursos conforme necessário.
7. Se necessário e/ou desejado, exemplo hello dados toofit no estúdio de aprendizado de máquina do Azure.
8. Entrar toohello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/).
9. Ler dados saudação diretamente da saudação `Hive Queries` usando Olá [importar dados] [ import-data] módulo. Colar Olá consulta necessária que extrai os campos, cria recursos e exemplos de dados se necessário diretamente no hello [importar dados] [ import-data] consulta.
10. Fluxo experimental simples do Azure Machine Learning começando com o conjunto de dados carregado.

## <a name="decisiontree"></a>Árvore de decisão para a seleção do cenário
- - -
Olá diagrama a seguir resume cenários Olá descritos acima e escolhas processo de análise avançada e tecnologia de saudação feitas que levar tooeach dos cenários de saudação especificado. Observe que podem levar o processamento de dados, exploração, engenharia de recurso e amostragem colocar em um ou mais método/ambiente – na fonte hello, intermediário, e/ou ambientes de destino e podem continuar iterativamente conforme necessário. diagrama de saudação só serve como uma ilustração de alguns fluxos de possíveis e não fornece uma enumeração completa.

![Cenários de passo a passo de exemplo do processo de Ciência de Dados][8]

### <a name="advanced-analytics-in-action-examples"></a>Exemplos de análise avançada em ação
Para orientações de aprendizado de máquina do Azure de ponta a ponta que empregam hello tecnologia e o processo de análise avançada usando conjuntos de dados públicos, consulte:

* [Processo de Ciência de Dados de Equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
* [Processo de Ciência de Dados de Equipe em ação: usando clusters Hadoop do HDInsight](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
