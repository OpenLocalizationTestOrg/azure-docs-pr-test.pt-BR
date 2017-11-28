---
title: "TooAzure banco de dados de conexão para MySQL de C++ | Microsoft Docs"
description: "Este guia de início rápido fornece um exemplo de código C++, você pode usar tooconnect e consultar dados do banco de dados MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="884d3-103">Banco de dados do Azure para MySQL: usar conector/C++ tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="884d3-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="884d3-104">Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um aplicativo C++.</span><span class="sxs-lookup"><span data-stu-id="884d3-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="884d3-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="884d3-106">Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando C++, e que você é novo tooworking com o banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="884d3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="884d3-107">Prerequisites</span></span>
<span data-ttu-id="884d3-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="884d3-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="884d3-109">Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="884d3-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="884d3-110">Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="884d3-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="884d3-111">Você também precisará:</span><span class="sxs-lookup"><span data-stu-id="884d3-111">You also need to:</span></span>
- <span data-ttu-id="884d3-112">Instalar o [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="884d3-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="884d3-113">Instalar o [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="884d3-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="884d3-114">Instalar o [Conector MySQL/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="884d3-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="884d3-115">Instalar [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="884d3-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="884d3-116">Instalar o Visual Studio e o .NET</span><span class="sxs-lookup"><span data-stu-id="884d3-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="884d3-117">Olá etapas nesta seção pressupõem que você esteja familiarizado com o desenvolvimento usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="884d3-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="884d3-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="884d3-118">**Windows**</span></span>
1. <span data-ttu-id="884d3-119">Instale a Comunidade do Visual Studio 2017, que é um IDE completo, extensível e gratuito para criar aplicativos modernos para Android, iOS, Windows, bem como aplicativos da Web e do banco de dados, e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="884d3-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="884d3-120">Você pode instalar o hello .NET Framework completo ou apenas o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="884d3-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="884d3-121">trechos de código de saudação em Olá Quickstart funcionam com o.</span><span class="sxs-lookup"><span data-stu-id="884d3-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="884d3-122">Se você já tiver o Visual Studio instalado em seu computador, ignore Olá próximas duas etapas.</span><span class="sxs-lookup"><span data-stu-id="884d3-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="884d3-123">Baixar Olá [instalador do Visual Studio de 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="884d3-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="884d3-124">Execute o instalador hello e siga Olá instalação prompts toocomplete Olá instalação.</span><span class="sxs-lookup"><span data-stu-id="884d3-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="884d3-125">**Configurar o Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="884d3-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="884d3-126">Propriedade de projeto do Visual Studio, > Propriedades de configuração > C/C++ > vinculador > Geral > diretórios de biblioteca adicionais, adicione o diretório de lib\opt de saudação (ou seja: C:\Program Files (x86) \MySQL\MySQL conector C++ 1.1.9\lib\opt) de saudação c + + conector.</span><span class="sxs-lookup"><span data-stu-id="884d3-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="884d3-127">No Visual Studio, propriedade do projeto > propriedades da configuração > C/C++ > geral > diretórios adicionais de inclusão</span><span class="sxs-lookup"><span data-stu-id="884d3-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="884d3-128">Adicione o diretório include/ do conector do c++ (ou seja, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="884d3-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="884d3-129">Adicione o diretório-raiz da biblioteca Boost (ou seja, C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="884d3-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="884d3-130">Propriedade de projeto do Visual Studio, > Propriedades de configuração > C/C++ > vinculador > entrada > dependências adicionais, adicione mysqlcppconn.lib no campo de texto de saudação</span><span class="sxs-lookup"><span data-stu-id="884d3-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="884d3-131">Mysqlcppconn.dll a cópia da pasta de biblioteca conector Olá c + + na etapa 3 toohello mesmo diretório do executável de aplicativo hello ou Adicionar variável de ambiente toohello para seu aplicativo pode localizá-lo.</span><span class="sxs-lookup"><span data-stu-id="884d3-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="884d3-132">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="884d3-132">Get connection information</span></span>
<span data-ttu-id="884d3-133">Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="884d3-134">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="884d3-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="884d3-135">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="884d3-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="884d3-136">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="884d3-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="884d3-137">Clique em nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-137">Click hello server name.</span></span>
4. <span data-ttu-id="884d3-138">Servidor de saudação selecione **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="884d3-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="884d3-139">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="884d3-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="884d3-140">![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="884d3-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="884d3-141">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.</span><span class="sxs-lookup"><span data-stu-id="884d3-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="884d3-142">Conectar-se, criar tabela e inserir dados</span><span class="sxs-lookup"><span data-stu-id="884d3-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="884d3-143">A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="884d3-144">código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="884d3-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="884d3-145">Em seguida, o código de Olá usa o método Execute () e createStatement() toorun Olá comandos banco de dados.</span><span class="sxs-lookup"><span data-stu-id="884d3-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="884d3-146">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="884d3-147">Ler dados</span><span class="sxs-lookup"><span data-stu-id="884d3-147">Read data</span></span>

<span data-ttu-id="884d3-148">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="884d3-149">código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="884d3-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="884d3-150">Em seguida, código Olá usa o método prepareStatement() e ExecuteQuery () toorun Olá selecionar comandos.</span><span class="sxs-lookup"><span data-stu-id="884d3-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="884d3-151">Por fim, código Olá usa Next () tooadvance toohello registros nos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="884d3-152">Em seguida, o código de saudação usa valores de saudação tooparse getInt() e GetString () no registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="884d3-153">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="884d3-154">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="884d3-154">Update data</span></span>
<span data-ttu-id="884d3-155">A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="884d3-156">código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="884d3-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="884d3-157">Em seguida, o código de saudação usa o método ExecuteQuery () e prepareStatement() toorun Olá comandos de atualização.</span><span class="sxs-lookup"><span data-stu-id="884d3-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="884d3-158">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="884d3-159">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="884d3-159">Delete data</span></span>
<span data-ttu-id="884d3-160">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="884d3-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="884d3-161">código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão.</span><span class="sxs-lookup"><span data-stu-id="884d3-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="884d3-162">Código Olá usa prepareStatement() método ExecuteQuery () toorun Olá comandos e excluir.</span><span class="sxs-lookup"><span data-stu-id="884d3-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="884d3-163">Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="884d3-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="884d3-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="884d3-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="884d3-165">Migrar seu banco de dados de MySQL tooAzure banco de dados para MySQL usando dump e restore</span><span class="sxs-lookup"><span data-stu-id="884d3-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
