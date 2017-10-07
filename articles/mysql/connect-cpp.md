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
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: usar conector/C++ tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan Azure banco de dados para MySQL usando um aplicativo C++. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Olá etapas neste artigo presumem que você esteja familiarizado com o desenvolvimento usando C++, e que você é novo tooworking com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

Você também precisará:
- Instalar o [.NET Framework](https://www.microsoft.com/net/download)
- Instalar o [Visual Studio](https://www.visualstudio.com/downloads/)
- Instalar o [Conector MySQL/C++](https://dev.mysql.com/downloads/connector/cpp/) 
- Instalar [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>Instalar o Visual Studio e o .NET
Olá etapas nesta seção pressupõem que você esteja familiarizado com o desenvolvimento usando o .NET.

### <a name="windows"></a>**Windows**
1. Instale a Comunidade do Visual Studio 2017, que é um IDE completo, extensível e gratuito para criar aplicativos modernos para Android, iOS, Windows, bem como aplicativos da Web e do banco de dados, e serviços de nuvem. Você pode instalar o hello .NET Framework completo ou apenas o .NET Core. trechos de código de saudação em Olá Quickstart funcionam com o. Se você já tiver o Visual Studio instalado em seu computador, ignore Olá próximas duas etapas.
   - Baixar Olá [instalador do Visual Studio de 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Execute o instalador hello e siga Olá instalação prompts toocomplete Olá instalação.

### <a name="configure-visual-studio"></a>**Configurar o Visual Studio**
1. Propriedade de projeto do Visual Studio, > Propriedades de configuração > C/C++ > vinculador > Geral > diretórios de biblioteca adicionais, adicione o diretório de lib\opt de saudação (ou seja: C:\Program Files (x86) \MySQL\MySQL conector C++ 1.1.9\lib\opt) de saudação c + + conector.
2. No Visual Studio, propriedade do projeto > propriedades da configuração > C/C++ > geral > diretórios adicionais de inclusão
   - Adicione o diretório include/ do conector do c++ (ou seja, C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - Adicione o diretório-raiz da biblioteca Boost (ou seja, C:\boost_1_64_0\)
3. Propriedade de projeto do Visual Studio, > Propriedades de configuração > C/C++ > vinculador > entrada > dependências adicionais, adicione mysqlcppconn.lib no campo de texto de saudação
4. Mysqlcppconn.dll a cópia da pasta de biblioteca conector Olá c + + na etapa 3 toohello mesmo diretório do executável de aplicativo hello ou Adicionar variável de ambiente toohello para seu aplicativo pode localizá-lo.

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **myserver4demo**.
3. Clique em nome do servidor de saudação.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Nome do servidor do Banco de Dados do Azure para MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá tooconnect de código e carregar Olá dados usando **CREATE TABLE** e **INSERT INTO** instruções SQL. código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão. Em seguida, o código de Olá usa o método Execute () e createStatement() toorun Olá comandos banco de dados. 

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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

## <a name="read-data"></a>Ler dados

A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão. Em seguida, código Olá usa o método prepareStatement() e ExecuteQuery () toorun Olá selecionar comandos. Por fim, código Olá usa Next () tooadvance toohello registros nos resultados de saudação. Em seguida, o código de saudação usa valores de saudação tooparse getInt() e GetString () no registro de saudação.

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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

## <a name="update-data"></a>Atualizar dados
A seguir use Olá código tooconnect e ler Olá dados usando um **atualização** instrução SQL. código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão. Em seguida, o código de saudação usa o método ExecuteQuery () e prepareStatement() toorun Olá comandos de atualização. 

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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


## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. código Olá usa a classe sql::Driver com Olá Connect () método tooestablish tooMySQL uma conexão. Código Olá usa prepareStatement() método ExecuteQuery () toorun Olá comandos e excluir.

Substitua parâmetros de Host, DBName, usuário e senha Olá com valores hello que você especificou quando criou o banco de dados e servidor de saudação. 

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

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migrar seu banco de dados de MySQL tooAzure banco de dados para MySQL usando dump e restore](concepts-migrate-dump-restore.md)
