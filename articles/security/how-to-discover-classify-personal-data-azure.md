---
title: aaaDiscover, identificar e classificar os dados pessoais no Microsoft Azure | Microsoft Docs
description: Saiba mais sobre como pesquisar, classificar, descobrir e identificar dados
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Descobrir, identificar e classificar dados pessoais no Microsoft Azure

Este artigo fornece orientação sobre como toodiscover, identificar e classificar os dados pessoais em várias ferramentas do Azure e serviços, incluindo o uso do Data Catalog do Azure, o Active Directory do Azure, o banco de dados SQL, o Power Query para clusters Hadoop em HDInsight do Azure, o Azure Consultas de proteção de informações, pesquisa do Azure e SQL para o banco de dados do Azure Cosmos.

## <a name="scenario-problem-statement-and-goal"></a>Cenário, declaração do problema e meta

Uma empresa de material esportivo localizada nos EUA coleta uma variedade de dados pessoais e outros dados. Isso inclui dados de clientes e funcionários. Olá empresa mantém em vários bancos de dados e armazena em vários locais em seu ambiente do Azure. Além disso tooselling tem equipamento, também hospedar e gerenciar o registro de eventos esportiva elite Olá, mundo, inclusive em Olá da Europa, e Olá alguns casos coletam os dados do cliente incluem informações médicas.

Como a empresa Olá hospeda muitas viagens bicycling internacionais de cada ano e tem terceirizados em locais em todo o mundo de saudação, alguns conjuntos de dados de saudação são muito grandes. empresa de saudação também tem criados pelo desenvolvedor de aplicativos que são usados por clientes e funcionários.

empresa de saudação deseja Olá tooaddress os problemas a seguir:

- Dados pessoais de clientes e funcionários devem ser classificado/distintos de saudação coleta de outra empresa Olá de dados em ordem tooensure adequado acesso e segurança.
- Olá, administrador de dados precisa tooeasily descobrir o local de saudação pessoal de dados do cliente em várias áreas da saudação ambiente do Azure.
- Dados pessoais de clientes e funcionários que aparece de documentos compartilhados e comunicações por email devem ser rotuladas toohelp Certifique-se de que ele é mantido seguro.
- os desenvolvedores de aplicativos da empresa Olá precisam de uma pesquisa de tooeasily de maneira para clientes e funcionários dados pessoais em seus aplicativos web e móveis.
- Os desenvolvedores também precisam tooquery seu banco de dados de documento para dados pessoais.

### <a name="company-goals"></a>Metas da empresa

- Todos os dados pessoais de clientes e funcionários devem ser marcados/anotados no Catálogo de Dados do Azure, de modo que possam ser encontrados com facilidade. O ideal é que os dados pessoais de clientes e funcionários sejam marcados/anotados separadamente.
- Os dados pessoais de perfis do usuário e as informações de trabalho de clientes e funcionários que residem no Azure Active Directory devem ser localizados com facilidade.
- Os dados pessoais que residem em vários bancos de dados SQL devem ser consultados com facilidade. 
- Algumas das grandes conjuntos de dados da empresa Olá são gerenciadas por meio do Azure HDInsight e armazenadas no Hadoop. Eles devem ser importados para o Excel, de modo que possam ser consultados para obter dados pessoais.
- Os dados pessoais compartilhados em documentos e comunicações por email devem ser classificados, rotulados e mantidos em segurança com a Proteção de Informações do Azure.
- Olá os desenvolvedores de aplicativos da empresa devem ser capaz de toodiscover clientes e funcionários dados pessoais em aplicativos de saudação desenvolvidas, que pode ser feito com a pesquisa do Azure.
- Os desenvolvedores devem ser capaz de toofind dados pessoais em seu banco de dados do documento.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: descoberta de dados

O [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft. Você pode localizar os perfis de usuário do cliente e do funcionário e informações de trabalho do usuário que contêm dados pessoais em sua [Active Directory do Azure](https://azure.microsoft.com/services/active-directory/) ambiente (AAD) usando Olá [portal do Azure](https://portal.azure.com/).

Isso é particularmente útil se você quiser toofind ou altera os dados pessoais de um usuário específico. Também adicione ou altere o perfil do usuário e as informações de trabalho. Você deve entrar com uma conta que seja um administrador global para o diretório de saudação.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Como fazer para localizar ou exibir o perfil do usuário e as informações de trabalho?

1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.

2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![como fazer para localizar o perfil do usuário e as informações de trabalho](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Em Olá **usuários e grupos** folha, selecione **usuários**.

  ![Abrindo usuários e grupos](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Em Olá **usuários e grupos, usuários** folha, selecione um usuário na lista de saudação e, em seguida, na folha de saudação do usuário selecionado hello, selecione **perfil** tooview informações de perfil de usuário que podem conter dados pessoais .

  ![selecionar usuário](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Se você precisa tooadd ou alterar as informações de perfil de usuário, você pode fazê-lo e, na barra de comandos hello, selecione **salvar.**
6. Na folha de saudação do usuário selecionado hello, selecione **informações de trabalho** tooview informações de trabalho de usuário que podem conter dados pessoais.

 ![exibindo informações de trabalho](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Se você precisa tooadd ou alterar informações de trabalho do usuário, você pode fazê-lo e, em seguida, na barra de comandos hello, selecione **salvar.**

## <a name="azure-sql-database-data-discovery"></a>Banco de Dados SQL do Azure: descoberta de dados

O [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) é um banco de dados de nuvem que ajuda os desenvolvedores a criar e manter aplicativos. Os dados pessoais podem ser encontrados no [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando consultas SQL padrão. Consulta elástica de SQL do Azure (visualização) permite consultas de bancos de dados de tooperform de usuários.

Um detalhadas [banco de dados SQL](../sql-database/sql-database-technical-overview.md) tutorial explica os vários aspectos do uso de um banco de dados SQL, incluindo como toobuild um e como toorun consultas de dados. a seguir Olá é um resumo das informações de saudação disponíveis no tutorial de saudação com seções de toospecific links.

### <a name="how-do-i-build-a-sql-database"></a>Como fazer para criar um banco de dados SQL?

Há três toodo de maneiras-lo:

- Um banco de dados do SQL Azure pode ser criado em Olá [portal do Azure](https://portal.azure.com/). Tutorial de saudação, você usará um conjunto específico de recursos de computação e armazenamento em um grupo de recursos e o servidor lógico. Você usará dados de exemplo de uma empresa fictícia chamada AdventureWorks. Você também criará uma regra de firewall no nível do servidor. toolearn como toodo hello, visite [criar um banco de dados do SQL Azure no portal do Azure de saudação](../sql-database/sql-database-get-started-portal.md) tutorial.

  ![Criar um Banco de Dados SQL do Azure](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Um banco de dados SQL também pode ser criado em Olá [Shell de nuvem do Azure](https://azure.microsoft.com/features/cloud-shell/) CLI, uma ferramenta de linha de comando baseada em navegador. ferramenta de saudação está disponível no portal do Azure de saudação e pode ser executada diretamente desse local. Neste tutorial, você inicie a ferramenta de saudação, define variáveis de script, crie um grupo de recursos e o servidor lógico e configurar uma regra de firewall de servidor. Em seguida, você cria um banco de dados com os dados de exemplo. toolearn como toocreate seu banco de dados dessa forma, visite Olá [criar um único banco de dados SQL do Azure usando Olá CLI do Azure](../sql-database/sql-database-get-started-cli.md) tutorial.

  ![Tutorial da CLI](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
A CLI do Azure é normalmente usada por desenvolvedores e administradores do Linux. Alguns usuários consideram a CLI mais fácil e intuitiva que o PowerShell, que é a terceira opção.

- Finalmente, você pode criar um banco de dados SQL usando o PowerShell, que é um toocreate da ferramenta usada de linha de comando/script e gerenciar o Azure e outros recursos. Neste tutorial, você inicie a ferramenta de saudação, define variáveis de script, crie um grupo de recursos e o servidor lógico e configurar uma regra de firewall de servidor. Em seguida, você criará um banco de dados com os dados de exemplo.

tutorial de saudação requer hello Azure PowerShell versão 4.0 ou posterior do módulo. Execute Get-Module - ListAvailable AzureRM toofind sua versão. Se você precisar tooinstall ou atualização, consulte o módulo de instalar o Azure PowerShell.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn como toocreate seu banco de dados dessa forma, visite Olá [criar um único banco de dados SQL do Azure usando o Powershell](../sql-database/sql-database-get-started-powershell.md) tutorial.

>[!Note]
Administradores do Windows tendem toouse PowerShell, mas alguns deles preferem CLI do Azure.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Como procurar dados pessoais no banco de dados do SQL no portal do Azure de saudação? * *

Você pode usar a ferramenta de editor de consulta interna hello dentro Olá toosearch portal do Azure para dados pessoais. Você vai fazer logon na ferramenta toohello usando o logon de administrador do SQL server e a senha e, em seguida, digite uma consulta.

  ![Pesquisar usando o portal de saudação do sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Etapa 5 do tutorial de saudação mostra um exemplo de consulta no painel do editor de consultas hello, mas ele não se concentre em informações pessoais ou confidenciais (também combina dados de duas tabelas e cria aliases de coluna de origem Olá no conjunto de dados Olá sendo retornado). Olá seguinte captura de tela mostra Olá consulta da etapa 5, bem como Olá painel de resultados que é retornado:

  ![editor de consultas](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Se o banco de dados era chamado MyTable, uma consulta de exemplo de informações pessoais poderá incluir o nome, o número do seguro social e o número de identificação e terá esta aparência:

“SELECT nome, SSN, número de identificação FROM MyTable”

Você executará a consulta hello e, em seguida, ver os resultados de saudação em Olá **resultados** painel.

Para obter mais informações sobre como tooquery um SQL banco de dados em Olá portal do Azure, visite Olá [banco de dados do SQL consulta Olá](../sql-database/sql-database-get-started-portal.md) seção do tutorial de saudação.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Como fazer para pesquisar dados em vários bancos de dados?

Consulta elástica do SQL (visualização) permite que você tooperform entre bancos de dados e várias consultas de banco de dados e retornar um único resultado. Olá [visão geral do tutorial](../sql-database/sql-database-elastic-query-overview.md) inclui uma descrição detalhada dos cenários e explica a diferença de saudação entre particionamento vertical e horizontal de banco de dados. O particionamento horizontal é chamado “fragmentação”.

  ![Particionamento vertical](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![particionamento horizontal](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget iniciado, visite Olá [visão geral de consulta Elástico de banco de dados SQL (visualização)](../sql-database/sql-database-elastic-query-overview.md) página.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (para importação de clusters Hadoop do Azure HDInsight): descoberta de dados para conjuntos de dados grandes

O Hadoop é um serviço de armazenamento e processamento de software livre do Apache para conjuntos de dados grandes, que são analisados e armazenados em clusters Hadoop. [HDInsight do Azure](https://azure.microsoft.com/services/hdinsight/) permite que os usuários toowork com Hadoop clusters no Azure. O Power Query é um suplemento do Excel que, entre outras coisas, ajuda os usuários a descobrir dados de origens diferentes.

Dados pessoais associados com clusters Hadoop em HDInsight do Azure podem ser importado tooExcel com o Power Query. Quando Olá dados estiverem no Excel você pode usar uma consulta tooidentify-lo.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Como usar clusters de Hadoop tooimport Excel Power Query no Azure HDInsight para o Excel?

Um tutorial do HDInsight orientará você durante todo esse processo. Ele explica os pré-requisitos e inclui um link tooa [Introdução ao Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) tutorial. Instruções abordam Excel 2016, bem como 2013 e 2010 (etapas são ligeiramente diferentes para as versões mais antigas de saudação do Excel). Se você não tiver o suplemento do Excel Power Query hello, Olá tutorial mostra como tooget-lo. Você começará tutorial Olá no Excel e precisará toohave uma conta de armazenamento de BLOBs do Azure associada ao cluster.

  ![Consulta no Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn como toodo hello, visite [tooHadoop Excel se conectar usando o Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) tutorial.

Fonte: [tooHadoop Excel conectar usando o Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Proteção de Informações do Azure: classificação de dados pessoais para emails e documentos

[O Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) pode ajudar os clientes do Azure aplicar tooclassify rótulos e proteger os documentos compartilhados interna ou externamente e comunicações de email. Alguns desses itens podem conter informações pessoais de clientes ou funcionários. As regras e as condições podem ser definidas automática ou manualmente, pelos administradores ou usuários. Por exemplo, se um usuário está salvando um documento que inclui informações de cartão de crédito, ele verá uma recomendação de rótulo que foi configurada pelo administrador de saudação.

### <a name="how-do-i-try-it"></a>Como fazer para experimentá-la?

Se você quiser toogive Azure Information Protection um toosee tente se ele pode ser uma opção para sua organização, visite Olá [tutorial de início rápido](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Orienta você pelas etapas básicas cinco — da instalação tooconfiguring política tooseeing classificação rotulação e compartilhamento em ação e devem levar menos de meia hora.

### <a name="how-do-i-deploy-it"></a>Como fazer para implantá-la?

Se você desejar toodeploy Azure Information Protection para sua organização, visite Olá [roteiro de implantação para classificação, rotulação e proteção](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Há mais alguma coisa que devo saber?

Para obter informações complementares que ajudarão você a considerar como tooset-lo, visite Olá [pronto, definir, proteger!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
. E seleção Olá Saiba mais links abaixo para obter mais informações sobre o Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure Search: descoberta de dados para aplicativos do desenvolvedor

O [Azure Search](https://azure.microsoft.com/services/search/) é uma solução de pesquisa em nuvem para desenvolvedores e fornece uma experiência avançada de pesquisa de dados para os aplicativos. A pesquisa do Azure permite que você toolocate dados entre os índices definidos pelo usuário, originados do banco de dados do Azure Cosmo, banco de dados do SQL Azure, armazenamento de BLOBs do Azure, armazenamento de tabela do Azure ou cliente personalizado dados JSON. Você também pode estruturar consultas Lucene usando Olá toosearch de API de REST de pesquisa do Azure para tipos de dados pessoais ou dados pessoais de saudação de indivíduos específicos. Os recursos incluem a pesquisa de texto completo, a sintaxe de consulta simples e a sintaxe de consulta Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Como usar o tooquery de dados do SQL?

toobegin com noções básicas sobre hello, visite Olá [o banco de dados do Azure CosmosD: como tooquery usando SQL](../cosmos-db/tutorial-query-documentdb.md) tutorial. tutorial de saudação fornece um documento de exemplo e dois exemplos de consultas SQL e resultados.

Para obter diretrizes detalhadas sobre como criar consultas SQL, visite [Consultas SQL para a API do DocumentDB do Azure Cosmos DB.](../cosmos-db/documentdb-sql-query.md)

Se você for novo tooAzure Cosmos DB e seria como toolearn como toocreate um banco de dados, adicionar uma coleção e adicionar dados, visite Olá [o banco de dados do Azure Cosmos: criar um aplicativo da web API DocumentDB](../cosmos-db/create-documentdb-dotnet.md) tutorial de início rápido. Se você gostaria que toodo isso em um idioma diferente do .NET, como Java ou Python, basta escolher seu idioma preferencial depois de obter toohello site.

## <a name="next-steps"></a>Próximas etapas

[Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50)

[O que é o Banco de Dados SQL?](../sql-database/sql-database-technical-overview.md)

[Editor de Consultas do Banco de Dados SQL disponível no portal do Azure] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[O que é a Proteção de Informações do Azure?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[O que é o Azure Rights Management?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Proteção de Informações do Azure: Atenção, preparar, proteger!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
