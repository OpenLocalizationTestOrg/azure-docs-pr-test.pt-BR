---
title: Usar o Python para consultar banco de dados SQL do Azure | Microsoft Docs
description: "Este tópico mostra como usar Python para criar um programa que se conecta a um banco de dados SQL do Azure e consultá-lo usando instruções Transact-SQL."
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
ms.openlocfilehash: afffcb9a4938bf97626f182bb4f4d099d807d411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-python-to-query-an-azure-sql-database"></a><span data-ttu-id="0edd0-103">Usar Python para consultar um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0edd0-103">Use Python to query an Azure SQL database</span></span>

 <span data-ttu-id="0edd0-104">Este guia de início rápido demonstra como usar o [Python](https://python.org) para se conectar a um banco de dados SQL do Azure e usar instruções Transact-SQL para consultar dados.</span><span class="sxs-lookup"><span data-stu-id="0edd0-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0edd0-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0edd0-105">Prerequisites</span></span>

<span data-ttu-id="0edd0-106">Para concluir este tutorial de início rápido, tenha o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0edd0-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="0edd0-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0edd0-107">An Azure SQL database.</span></span> <span data-ttu-id="0edd0-108">Este início rápido usa os recursos criados em um destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="0edd0-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="0edd0-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="0edd0-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="0edd0-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="0edd0-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="0edd0-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0edd0-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="0edd0-112">Uma [regra de firewall no nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público do computador usado neste tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="0edd0-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="0edd0-113">Você instalou o Python e o software relacionado para seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="0edd0-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="0edd0-114">**MacOS**: instale o Homebrew e o Python, instale o driver ODBC e o SQLCMD e, em seguida, instale o Driver Python para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0edd0-114">**MacOS**: Install Homebrew and Python, install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0edd0-115">Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="0edd0-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="0edd0-116">**Ubuntu**: instale o Python e outros pacotes necessários e, em seguida, instale o Driver Python para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0edd0-116">**Ubuntu**:  Install Python and other required packages, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0edd0-117">Consulte [Etapas 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0edd0-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="0edd0-118">**Windows**: instale a versão mais recente do Python (a variável de ambiente agora está configurada para você), instale o driver ODBC e o SQLCMD e então instale o Driver Python para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0edd0-118">**Windows**: Install the newest version of Python (environment variable is now configured for you), install the ODBC driver and SQLCMD, and then install the Python Driver for SQL Server.</span></span> <span data-ttu-id="0edd0-119">Veja a [Etapa 1.2, 1.3 e 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="0edd0-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="0edd0-120">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="0edd0-120">SQL server connection information</span></span>

<span data-ttu-id="0edd0-121">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0edd0-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="0edd0-122">Você precisará do nome totalmente qualificado do servidor, nome do banco de dados e informações de logon nos próximos procedimentos.</span><span class="sxs-lookup"><span data-stu-id="0edd0-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="0edd0-123">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0edd0-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0edd0-124">Selecione **Bancos de Dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="0edd0-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="0edd0-125">Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor, como mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="0edd0-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="0edd0-126">Você pode passar o mouse sobre o nome do servidor para abrir a opção **Clique para copiar**.</span><span class="sxs-lookup"><span data-stu-id="0edd0-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="0edd0-128">Se você se esquecer das informações de logon do servidor, navegue até a página do servidor do Banco de Dados SQL para exibir o nome de administrador do servidor e, se necessário, redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="0edd0-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="0edd0-129">Inserir código para consultar o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="0edd0-129">Insert code to query SQL database</span></span> 

1. <span data-ttu-id="0edd0-130">Em seu editor de texto favorito, crie um novo arquivo, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="0edd0-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="0edd0-131">Substitua o conteúdo pelo código a seguir e adicione os valores apropriados para seu servidor, banco de dados, usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="0edd0-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="0edd0-132">Executar o código</span><span class="sxs-lookup"><span data-stu-id="0edd0-132">Run the code</span></span>

1. <span data-ttu-id="0edd0-133">No prompt de comando, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="0edd0-133">At the command prompt, run the following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="0edd0-134">Verifique se as 20 linhas superiores são retornadas e, em seguida, feche a janela do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0edd0-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0edd0-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0edd0-135">Next steps</span></span>

- [<span data-ttu-id="0edd0-136">Projetar seu primeiro banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0edd0-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="0edd0-137">Drivers Python da Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0edd0-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="0edd0-138">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="0edd0-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

