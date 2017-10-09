---
title: aaaConnect tooSQL usando C e C++ do banco de dados | Microsoft Docs
description: "Exemplo hello de uso de código em toobuild esse início rápido um aplicativo moderno com C++ e com o apoio de um poderoso banco de dados relacional na nuvem Olá com o banco de dados do SQL Azure."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Conecte-se tooSQL banco de dados usando C e C++
Esta postagem é destinada a desenvolvedores de C e C++ tentar tooconnect tooAzure banco de dados SQL. Ele é dividido em seções que você possa passar toohello seção que captura melhor seu interesse. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Pré-requisitos para o tutorial do hello C/C++
Certifique-se de que ter Olá itens a seguir:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/). Você deve instalar Olá C++ language componentes toobuild e executar esse exemplo.
* [Desenvolvimento no Linux para Visual Studio](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Se você estiver desenvolvendo no Linux, você também deve instalar extensão de Linux do Visual Studio de saudação. 

## <a id="AzureSQL"></a>Banco de dados SQL do Azure e SQL Server em máquinas virtuais
SQL Azure baseia-se no Microsoft SQL Server e é projetado tooprovide uma alta disponibilidade, alto desempenho e serviço escalonável. Há muitos benefícios toousing SQL Azure em seu banco de dados proprietário em execução no local. Com o SQL Azure, você não tem tooinstall, configurar, manter ou gerenciar o banco de dados, mas somente conteúdo hello e estrutura de saudação do banco de dados. Causas de preocupação típicas de bancos de dados como redundância e tolerância a falhas estão incluídos. 

O Azure atualmente tem duas opções para hospedar cargas de trabalho do SQL Server: Banco de Dados SQL do Azure, banco de dados como um serviço e o SQL Server em Máquinas Virtuais (VM). Nós não obterá detalhes sobre as diferenças de saudação entre esses dois exceto que o banco de dados do SQL Azure é a melhor opção para novos aplicativos baseados em nuvem tootake aproveitar Olá redução de custos e fornecem otimização de desempenho que os serviços de nuvem. Se você estiver considerando a migração ou estender seus locais de nuvem de toohello de aplicativos, do SQL server na máquina virtual do Azure pode funcionar melhor para você. tookeep coisas simples para este artigo, vamos criar um banco de dados do SQL Azure. 

## <a id="ODBC"></a>Tecnologias de acesso a dados: ODBC e OLE DB
Conexão tooAzure banco de dados SQL não é diferente e atualmente há duas maneiras tooconnect toodatabases: ODBC (Open Database connectivity) e OLE DB (banco de dados vinculação e incorporação de objetos). Nos últimos anos, a Microsoft tem se alinhado com o [ODBC para acesso a dados relacionais nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). O ODBC é relativamente simples e também muito mais rápido que o OLE DB. Olá aqui a única limitação é que o ODBC usar uma API de estilo C antiga. 

## <a id="Create"></a>Etapa 1: Criando seu Banco de Dados SQL do Azure
Consulte Olá [página de Introdução](sql-database-get-started-portal.md) toolearn como toocreate um banco de dados de exemplo.  Como alternativa, você pode seguir este [breve vídeo de dois minutos](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate um banco de dados SQL do Azure usando Olá portal do Azure.

## <a id="ConnectionString"></a>Etapa 2: Obter a cadeia de conexão
Depois que o banco de dados do SQL Azure foi provisionado, você precisa toocarry out Olá informações de conexão do toodetermine as etapas a seguir e adicione o IP do cliente para acesso de firewall. 

Em [portal do Azure](https://portal.azure.com/), acesse a cadeia de conexão ODBC do banco de dados de SQL do Azure tooyour usando Olá **Mostrar cadeias de conexão de banco de dados** listado como parte da seção de visão geral de saudação do banco de dados: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Copiar conteúdo Olá Olá **ODBC (inclui Node. js) [autenticação do SQL]** cadeia de caracteres. Podemos usar essa cadeia de caracteres tooconnect mais recente do nosso interpretador de linha de comando C++ ODBC. Essa cadeia de caracteres fornece detalhes como o driver hello, server e outros parâmetros de conexão de banco de dados. 

## <a id="Firewall"></a>Etapa 3: Adicionar seu firewall toohello IP
Vá toohello seção de firewall para o servidor de banco de dados e adicione seu [usando estas etapas de firewall do cliente IP toohello](sql-database-configure-firewall-settings.md) toomake-se de que podemos pode estabelecer uma conexão bem-sucedida: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

Neste ponto, você configurou seu banco de dados do SQL Azure e é tooconnect pronto do seu código C++. 

## <a id="Windows"></a>Etapa 4: Conectando de um aplicativo Windows C/C++
Você pode facilmente conectar tooyour [banco de dados do SQL Azure usando o ODBC no Windows usando este exemplo](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) que cria com o Visual Studio. exemplo Hello implementa um interpretador de linha de comando ODBC que pode ser usados tooconnect tooour DB do SQL Azure. Este exemplo usa o um arquivo de arquivo (DSN) de nome de origem do banco de dados como um argumento de linha de comando ou cadeia de caracteres de conexão detalhado de saudação que são copiados anteriormente do hello portal do Azure. Abrir página de propriedade Olá para este projeto e cole a cadeia de caracteres de conexão Olá como um argumento de comando, conforme mostrado aqui: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Certifique-se de que fornecer detalhes de autenticação adequado Olá para seu banco de dados como parte dessa cadeia de caracteres de conexão do banco de dados. 

Iniciar Olá aplicativo toobuild-lo. Você deve ver Olá janela Validando uma conexão bem-sucedida a seguir. Você pode até mesmo executar alguns comandos básicos do SQL como **criar tabela** toovalidate a conectividade de banco de dados:

![Comandos SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Como alternativa, você pode criar um arquivo DSN usando o Assistente de saudação que é iniciado quando nenhum argumento de comando é fornecido. É recomendável que você também experimente usar essa opção. Você pode usar esse arquivo DSN para automação e para proteger suas configurações de autenticação: 

![Criar um arquivo DSN](./media/sql-database-develop-cplusplus-simple/datasource.png)

Parabéns! Você agora se conectou com êxito tooAzure SQL usando o C++ e o ODBC no Windows. Você pode continuar a ler toodo hello mesmo para plataforma Linux também. 

## <a id="Linux"></a>Etapa 5: Conectando de um aplicativo Linux C/C++
Caso você ainda não ouvido notícias Olá ainda, o Visual Studio agora permite que você toodevelop aplicativo C++ Linux. Você pode ler sobre esse cenário de novo no hello [Visual C++ para desenvolvimento Linux](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog. toobuild para Linux, você precisa de um computador remoto onde sua distribuição Linux está em execução. Se você não tiver um disponível, poderá definir um rapidamente usando [máquinas virtuais Azure Linux](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Para este tutorial, vamos supor que você tenha uma distribuição do Ubuntu 16.04 Linux configurada. etapas de saudação aqui também devem aplicar tooUbuntu 15.10, Red Hat 6 e 7 do Red Hat. 

Olá etapas a seguir instalar bibliotecas de saudação necessárias para SQL e ODBC para a distribuição:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Inicie o Visual Studio. Em Ferramentas -> Opções -> plataforma cruzada -> Gerenciador de Conexão, adicione uma caixa de Linux tooyour conexão: 

![Opções de Ferramentas](./media/sql-database-develop-cplusplus-simple/tools.png)

Depois de estabelecer a conexão via SSH, crie um modelo de projeto Vazio (Linux): 

![Novo modelo do projeto](./media/sql-database-develop-cplusplus-simple/template.png)

Você pode adicionar um [novo arquivo de origem C e substituí-lo por este conteúdo](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Usando Olá ODBC APIs SQLAllocHandle SQLSetConnectAttr e SQLDriverConnect, você deve ser capaz de tooinitialize e estabelecer um banco de dados de tooyour de conexão. Como com exemplo de ODBC do Windows hello, você precisa tooreplace Olá SQLDriverConnect chamada detalhes de saudação do seu parâmetros de cadeia de conexão de banco de dados copiados da saudação portal do Azure anteriormente. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Olá toodo de última coisa antes de compilar é tooadd **odbc** como uma dependência de biblioteca: 

![Adicionando o ODBC como uma biblioteca de entrada](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch seu aplicativo, exibir hello Linux Console de saudação **depurar** menu: 

![Console do Linux](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Se a conexão for bem-sucedida, você verá agora nome de banco de dados atual Olá impresso na Olá Linux Console: 

![Saída da Janela de Console do Linux](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Parabéns! Você concluiu com êxito o tutorial hello e agora pode conectar tooyour Azure SQL DB de C++ em plataformas Windows e Linux.

## <a id="GetSolution"></a>Obter a solução completa de tutorial de C/C++ Olá
Você pode encontrar a solução de GetStarted Olá que contém todos os exemplos de saudação neste artigo no github:

* [Exemplo de ODBC C++ Windows](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), baixar Olá Windows C++ ODBC exemplo tooconnect tooAzure SQL
* [Exemplo de ODBC C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), baixar Olá Linux C++ ODBC exemplo tooconnect tooAzure SQL

## <a name="next-steps"></a>Próximas etapas
* Saudação de revisão [visão geral do desenvolvimento de banco de dados SQL](sql-database-develop-overview.md)
* Para obter mais informações sobre Olá [referência de API de ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Recursos adicionais
* [Padrões de design para aplicativos SaaS multilocatários com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Explorar todos os Olá [recursos do banco de dados SQL](https://azure.microsoft.com/services/sql-database/)

