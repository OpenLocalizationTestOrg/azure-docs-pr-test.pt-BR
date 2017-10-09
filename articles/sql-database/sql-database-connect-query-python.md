---
title: aaaUse Python tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse Python toocreate um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="8fae4-103">Usar o Python tooquery um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8fae4-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="8fae4-104">Este guia rápido demonstra como toouse [Python](https://python.org) tooconnect tooan SQL do Azure do banco de dados e usar dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8fae4-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fae4-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8fae4-105">Prerequisites</span></span>

<span data-ttu-id="8fae4-106">toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="8fae4-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="8fae4-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8fae4-107">An Azure SQL database.</span></span> <span data-ttu-id="8fae4-108">Esse início rápido usa recursos de saudação criados em um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="8fae4-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8fae4-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="8fae4-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8fae4-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="8fae4-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8fae4-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fae4-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8fae4-112">Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="8fae4-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="8fae4-113">Você instalou o Python e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8fae4-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="8fae4-114">**MacOS**: instalar o Homebrew Python, instalar o driver ODBC hello e SQLCMD e, em seguida, instale o hello Python Driver para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fae4-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="8fae4-115">Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="8fae4-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="8fae4-116">**Ubuntu**: instalar o Python e outros necessários pacotes e, em seguida, instalar Olá Python Driver para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fae4-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="8fae4-117">Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="8fae4-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="8fae4-118">**Windows**: instalar a versão mais recente de saudação do Python (variável de ambiente agora está configurada para você), instale o driver ODBC hello e SQLCMD e, em seguida, instale o hello Python Driver para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fae4-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="8fae4-119">Veja a [Etapa 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="8fae4-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="8fae4-120">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="8fae4-120">SQL server connection information</span></span>

<span data-ttu-id="8fae4-121">Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8fae4-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8fae4-122">Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8fae4-123">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8fae4-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8fae4-124">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="8fae4-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8fae4-125">Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="8fae4-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="8fae4-126">Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="8fae4-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8fae4-128">Se você esquecer suas informações de logon de servidor, navegar toohello banco de dados do SQL server página tooview Olá administrador nome do servidor e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="8fae4-129">Insira o banco de dados SQL do código tooquery</span><span class="sxs-lookup"><span data-stu-id="8fae4-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="8fae4-130">Em seu editor de texto favorito, crie um novo arquivo, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="8fae4-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="8fae4-131">Substitua o conteúdo de saudação com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="8fae4-132">Executar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="8fae4-132">Run hello code</span></span>

1. <span data-ttu-id="8fae4-133">No prompt de comando hello, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8fae4-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="8fae4-134">Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8fae4-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fae4-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fae4-135">Next steps</span></span>

- [<span data-ttu-id="8fae4-136">Projetar seu primeiro banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8fae4-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="8fae4-137">Drivers Python da Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="8fae4-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="8fae4-138">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="8fae4-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

