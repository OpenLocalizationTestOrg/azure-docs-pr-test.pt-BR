---
title: "dados de aaaImport no estúdio de aprendizado de máquina de fontes de dados online | Microsoft Docs"
description: "Como tooimport seus dados de treinamento estúdio de aprendizado de máquina do Azure de várias fontes online."
keywords: importar dados, formato de dados, tipos de dados, fontes de dados, dados de treinamento
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Importar dados no estúdio de aprendizado de máquina do Azure de várias fontes de dados online com o módulo de importação de dados de saudação
Este artigo descreve o suporte de saudação de importação de dados online de várias fontes e informações de saudação necessárias toomove dados dessas fontes em uma experiência de aprendizado de máquina do Azure.

> [!NOTE]
> Este artigo fornece informações gerais sobre Olá [importar dados] [ import-data] módulo. Para obter mais informações sobre tipos de saudação de dados que você pode acessar, formatos, parâmetros e as respostas toocommon perguntas, consulte o tópico de referência de módulo Olá para Olá [importar dados] [ import-data] módulo.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Introdução
Usando Olá [importar dados] [ import-data] módulo, você pode acessar dados de uma das várias fontes de dados online enquanto sua experiência é executado no [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/Home):

* Uma URL da Web usando HTTP
* Hadoop usando HiveQL
* Armazenamento do blob do Azure
* Tabela do Azure
* Banco de dados SQL do Azure ou SQL Server na VM do Azure
* Banco de dados local do SQL Server
* Um provedor de feed de dados, atualmente OData
* Azure CosmosDB (anteriormente chamado de DocumentDB)

tooaccess fontes de dados online em sua experiência Studio, adicione Olá [importar dados] [ import-data] tooyour do módulo, selecione Olá **fonte de dados**e, em seguida, fornecer parâmetros Olá necessários dados de saudação tooaccess. fontes de dados online Olá com suporte são discriminados na tabela de saudação abaixo. Esta tabela também resume os formatos de arquivo hello que têm suporte e parâmetros que são usados tooaccess Olá dados.

Observe que, como os dados deste treinamento são acessados enquanto seu experimento está em execução, eles só estão disponíveis nesse experimento. Por comparação, os dados que foram armazenados em um módulo de conjunto de dados estão experimento tooany disponíveis no espaço de trabalho.

> [!IMPORTANT]
> Atualmente, Olá [importar dados] [ import-data] e [exportar dados] [ export-data] módulos podem ler e gravar dados apenas do armazenamento do Azure criado usando Olá Modelo de implantação clássico. Olá em outras palavras, o novo tipo de conta de armazenamento de BLOBs do Azure que oferece um nível de acesso de armazenamento ativa ou camada de acesso de armazenamento moderado ainda não é suportada. 
> 
> De modo geral, as contas de armazenamento do Azure que você possa ter criado antes de essa opção se tornar disponível não deverão ser afetadas. 
> Se você precisar toocreate uma nova conta, selecione **clássico** para Olá implantação de modelo, ou use o Gerenciador de recursos e selecione **geral** em vez de **armazenamento de Blob** para **Conta tipo**. 
> 
> Para saber mais, confira [Armazenamento de Blobs do Azure: camadas de armazenamento dinâmica e estática](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Fontes de dados online com suporte
O aprendizado de máquina do Azure **importar dados** módulo oferece suporte a saudação fontes de dados a seguir:

| Fonte de dados | Descrição | Parâmetros |
| --- | --- | --- |
| URL da Web via HTTP |Lê dados nos formatos de valores separados por vírgula (CSV), de valores separados por tabulação (TSV), de arquivo de relação de atributo (ARFF) e de Máquinas de Vetores de Suporte (SVM-light), de qualquer URL da Web que use HTTP |<b>URL</b>: Especifica o nome completo do arquivo hello, incluindo Olá URL do site e o nome de arquivo hello, com qualquer extensão de saudação. <br/><br/><b>Formato de dados</b>: especifica um dos dados com suporte de saudação formatos: CSV, TSV, ARFF ou SVM-light. Se dados saudação tem uma linha de cabeçalho, é usado tooassign nomes de coluna. |
| Hadoop/HDFS |Lê dados do armazenamento distribuído no Hadoop. Especifique Olá dados que você deseja usando HiveQL, uma linguagem de consulta como SQL. HiveQL também pode ser usado tooaggregate dados e executar a filtragem de dados antes de você adicionar Olá dados tooMachine estúdio de aprendizado. |<b>Consulta de banco de dados de hive</b>: Especifica a consulta de Hive Olá usado toogenerate dados de saudação.<br/><br/><b>URI do servidor HCatalog </b> : nome de saudação especificado do cluster usando o formato de saudação  *&lt;nome do seu cluster&gt;. n e t.*<br/><br/><b>Nome de conta de usuário do Hadoop</b>: Especifica o conta de usuário do Hadoop Olá tooprovision cluster de saudação do nome usado.<br/><br/><b>Senha de conta de usuário do Hadoop</b> : especifica Olá credenciais usadas durante o provisionamento de cluster hello. Para obter mais informações, veja [Criar clusters Hadoop no HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Local dos dados de saída</b>: Especifica se os dados de saudação são armazenados em um sistema de arquivos distribuído de Hadoop (HDFS) ou no Azure. <br/><ul>Se você armazenar dados de saída no HDFS, especifique o URI do servidor HDFS hello. (Estar se toouse Olá nome do cluster HDInsight sem o prefixo HTTPS:// de saudação). <br/><br/>Se você armazenar os dados de saída no Azure, você deve especificar o nome de conta de armazenamento do Azure hello, chave de acesso de armazenamento e o nome de contêiner de armazenamento.</ul> |
| Banco de dados SQL |Lê os dados armazenados em um banco de dados SQL do Azure ou em um banco de dados do SQL Server em execução em uma máquina virtual do Azure. |<b>Nome do servidor de banco de dados</b>: Especifica o nome de saudação do servidor de saudação no qual Olá banco de dados está em execução.<br/><ul>No caso de banco de dados do SQL Azure insira o nome do servidor de saudação que é gerado. Geralmente, ela contém o formulário de saudação  *&lt;generated_identifier&gt;. t.* <br/><br/>No caso de um SQL server hospedado em uma máquina virtual do Azure, digite *tcp:&lt;nome DNS da máquina virtual&gt;, 1433*</ul><br/><b>Nome do banco de dados </b>: Especifica o nome de saudação do banco de dados de saudação no servidor de saudação. <br/><br/><b>Nome de conta de usuário do servidor</b>: especifica um nome de usuário para uma conta que tenha permissões de acesso para o banco de dados de saudação. <br/><br/><b>Senha de conta de usuário do servidor</b>: Especifica a senha Olá Olá conta de usuário.<br/><br/><b>Aceitar qualquer certificado de servidor</b>: Use esta opção (menos segura), se você quiser tooskip revisando o certificado de saudação do site antes de ler os dados.<br/><br/><b>Consulta de banco de dados</b>: insira uma instrução SQL que descreve dados Olá deseja tooread. |
| Banco de dados SQL local |Lê dados armazenados em um banco de dados SQL local. |<b>Gateway de dados</b>: Especifica o nome de saudação do hello Data Management Gateway instalado em um computador onde ele pode acessar o banco de dados do SQL Server. Para obter informações sobre como configurar o gateway hello, consulte [executar análise avançada com o aprendizado de máquina do Azure usando os dados de um SQL server no local](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Nome do servidor de banco de dados</b>: Especifica o nome de saudação do servidor de saudação no qual Olá banco de dados está em execução.<br/><br/><b>Nome do banco de dados </b>: Especifica o nome de saudação do banco de dados de saudação no servidor de saudação. <br/><br/><b>Nome de conta de usuário do servidor</b>: especifica um nome de usuário para uma conta que tenha permissões de acesso para o banco de dados de saudação. <br/><br/><b>Nome de usuário e senha</b>: clique em <b>inserir valores</b> tooenter suas credenciais de banco de dados. Você pode usar a Autenticação Integrada do Windows ou Autenticação do SQL Server dependendo de como o SQL Server local está configurado.<br/><br/><b>Consulta de banco de dados</b>: insira uma instrução SQL que descreve dados Olá deseja tooread. |
| tabela do Azure |Lê dados de saudação serviço de tabela no armazenamento do Azure.<br/><br/>Se você ler grandes quantidades de dados raramente, use Olá serviço tabela do Azure. Ele fornece uma solução de armazenamento flexível, não relacional (NoSQL), massivamente escalonável, barata e de alta disponibilidade. |Olá opções Olá **importar dados** mudam dependendo se você estiver acessando informações públicas ou uma conta de armazenamento privada que exige credenciais de logon. Isso é determinado pelo Olá <b>tipo de autenticação</b> que pode ter um valor de "PublicOrSAS" ou "Conta", cada qual com seu próprio conjunto de parâmetros. <br/><br/><b>Público ou compartilhado assinatura de acesso (SAS) URI</b>: Olá parâmetros são:<br/><br/><ul><b>Tabela URI</b>: especifica Olá público ou URL SAS para a tabela de saudação.<br/><br/><b>Especifica Olá linhas tooscan para nomes de propriedade</b>: os valores hello são <i>TopN</i> tooscan Olá número especificado de linhas, ou <i>ScanAll</i> tooget todas as linhas na tabela de saudação. <br/><br/>Se dados saudação forem homogêneos e previsíveis, é recomendável que você selecione *TopN* e insira um número para N. Para tabelas grandes, isso pode resultar em tempos de leitura mais rápidos.<br/><br/>Se Olá dados são estruturados com conjuntos de propriedades que podem variar com base em profundidade hello e a posição da tabela de saudação, escolha Olá *ScanAll* opção tooscan todas as linhas. Isso garante a integridade de saudação de sua propriedade resultante e a conversão de metadados.<br/><br/></ul><b>Conta de armazenamento privada</b>: Olá parâmetros são: <br/><br/><ul><b>Nome da conta</b>: especifica nome de saudação da conta de saudação que contém a saudação tooread de tabela.<br/><br/><b>Chave de conta</b>: especifica Olá chave de armazenamento associado à conta de saudação.<br/><br/><b>Nome da tabela</b> : Especifica o nome de saudação da tabela de saudação que contém a saudação tooread de dados.<br/><br/><b>Linhas tooscan para nomes de propriedade</b>: os valores hello são <i>TopN</i> tooscan Olá número especificado de linhas, ou <i>ScanAll</i> tooget todas as linhas na tabela de saudação.<br/><br/>Se dados saudação forem homogêneos e previsíveis, é recomendável que você selecione *TopN* e insira um número para N. Para tabelas grandes, isso pode resultar em tempos de leitura mais rápidos.<br/><br/>Se Olá dados são estruturados com conjuntos de propriedades que podem variar com base em profundidade hello e a posição da tabela de saudação, escolha Olá *ScanAll* opção tooscan todas as linhas. Isso garante a integridade de saudação de sua propriedade resultante e a conversão de metadados.<br/><br/> |
| Armazenamento do Blobs do Azure |Lê os dados armazenados no serviço de Blob Olá no armazenamento do Azure, incluindo imagens, textos não estruturados ou dados binários.<br/><br/>Você pode usar o hello Blob serviço toopublicly expõe dados ou tooprivately armazenar dados de aplicativo. Você pode acessar seus dados de qualquer lugar usando as conexões HTTP ou HTTPS. |Olá opções Olá **importar dados** alteração módulo dependendo se você estiver acessando informações públicas ou uma conta de armazenamento privada que exige credenciais de logon. Isso é determinado pelo Olá <b>tipo de autenticação</b> que pode ter um valor de "PublicOrSAS" ou "Conta".<br/><br/><b>Público ou compartilhado assinatura de acesso (SAS) URI</b>: Olá parâmetros são:<br/><br/><ul><b>URI</b>: especifica Olá público ou URL SAS para blob de armazenamento hello.<br/><br/><b>Formato de arquivo</b>: Especifica o formato de saudação de dados de saudação em Olá serviço Blob. formatos de saudação com suporte são CSV, TSV e ARFF.<br/><br/></ul><b>Conta de armazenamento privada</b>: Olá parâmetros são: <br/><br/><ul><b>Nome da conta</b>: especifica nome de saudação da conta de saudação que contém o blob Olá deseja tooread.<br/><br/><b>Chave de conta</b>: especifica Olá chave de armazenamento associado à conta de saudação.<br/><br/><b>Caminho toocontainer, diretório ou blob </b> : Especifica o nome de saudação do blob de saudação que contém a saudação tooread de dados.<br/><br/><b>Formato de arquivo blob</b>: Especifica o formato de saudação de dados de saudação no serviço de blob hello. Olá formatos de dados com suporte são CSV, TSV, ARFF, CSV com uma codificação especificada e o Excel. <br/><br/><ul>Se o formato de saudação é CSV ou TSV, se tooindicate-se de que se o arquivo hello contém uma linha de cabeçalho.<br/><br/>Você pode usar o hello Excel opção tooread dados de pastas de trabalho do Excel. Em Olá <i>formato de dados do Excel</i> opção, indique se os dados de saudação estão em um intervalo de planilha do Excel ou em uma tabela do Excel. Em Olá <i>planilha do Excel ou tabela inserida </i>opção, especifique o nome de saudação do hello ou tabela que você deseja tooread de.</ul><br/> |
| Provedor de feed de dados |Lê dados de um provedor de feeds com suporte. Formato de Open Data Protocol (OData) Olá atualmente só é suportado. |<b>Tipo de conteúdo de dados</b>: Especifica o formato do OData hello.<br/><br/><b>URL de origem</b>: Especifica a URL completa para feed de dados Olá Olá. <br/>Por exemplo, Olá leituras de URL a seguir do banco de dados de exemplo Northwind Olá: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Próximas etapas

[Implantação de serviços Web do Azure AM que usam módulos Importar Dados e Exportar Dados](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
