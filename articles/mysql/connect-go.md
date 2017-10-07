---
title: "TooAzure banco de dados de conexão para MySQL usando Go | Microsoft Docs"
description: "Este guia de início rápido fornece vários exemplos de código Go use tooconnect e consultar dados do banco de dados MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a>Banco de dados do Azure para MySQL: vá usar linguagem tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan banco de dados do Azure para MySQL usando código escrito em hello [vá](https://golang.org/) idioma do Windows, Ubuntu Linux e Apple plataformas de macOS. Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando Go, mas que são novos tooworking com o banco de dados do Azure para MySQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar um Banco de Dados do Azure para servidor MySQL usando o portal do Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Criar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a>Instalar o conector MySQL e Go
Instalar [vá](https://golang.org/doc/install) e hello [go--driver do sql para MySQL](https://github.com/go-sql-driver/mysql#installation) em seu próprio computador. Dependendo de sua plataforma, siga as etapas de saudação:

### <a name="windows"></a>Windows
1. [Baixar](https://golang.org/dl/) e instale a ir para o Microsoft Windows de acordo com o toohello [instruções de instalação](https://golang.org/doc/install).
2. Inicie o prompt de comando Olá Olá do menu de início.
3. Crie uma pasta para o seu projeto, como. `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Altere o diretório na pasta de projeto hello, como `cd %USERPROFILE%\go\src\mysqlgo`.
5. Definir variável de ambiente Olá para o diretório de código de origem do GOPATH toopoint toohello. `set GOPATH=%USERPROFILE%\go`.
6. Instalar Olá [go--driver do sql para mysql](https://github.com/go-sql-driver/mysql#installation) executando Olá `go get github.com/go-sql-driver/mysql` comando.

   Em resumo, instalar Go, execute estes comandos no prompt de comando hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Inicie o shell Bash hello. 
2. Instale o Go executando `sudo apt-get install golang-go`.
3. Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/mysqlgo/`.
4. Altere o diretório para pasta hello, como `cd ~/go/src/mysqlgo/`.
5. Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta. No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.
6. Instalar Olá [go--driver do sql para mysql](https://github.com/go-sql-driver/mysql#installation) executando Olá `go get github.com/go-sql-driver/mysql` comando.

   Em resumo, execute estes comandos bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>Apple macOS
1. Baixe e instale ir de acordo com o toohello [instruções de instalação](https://golang.org/doc/install) sua plataforma de correspondência. 
2. Inicie o shell Bash hello. 
3. Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/mysqlgo/`.
4. Altere o diretório para pasta hello, como `cd ~/go/src/mysqlgo/`.
5. Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta. No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.
6. Instalar Olá [go--driver do sql para mysql](https://github.com/go-sql-driver/mysql#installation) executando Olá `go get github.com/go-sql-driver/mysql` comando.

   Em resumo, instale o Go e, em seguida, execute esses comandos bash:
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados MySQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e procure o servidor de saudação você ter creased, como **myserver4demo**.
3. Clique em nome do servidor de saudação **myserver4demo**.
4. Servidor de saudação selecione **propriedades** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para MySQL – Logon de administrador do servidor](./media/connect-go/1_server-properties-name-login.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página nome de logon de administrador de servidor do tooview hello e, se necessário, Redefinir senha hello.
   

## <a name="build-and-run-go-code"></a>Compilar e executar o código Go 
1. toowrite Golang código, você pode usar um editor de texto simples, como o bloco de notas no Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) no Ubuntu ou editor de texto no macOS. Se você preferir IDE (Ambiente de Desenvolvimento Integrado) mais avançado, experimente o [Gogland](https://www.jetbrains.com/go/) da Jetbrains, o [Visual Studio Code](https://code.visualstudio.com/) da Microsoft ou o [Atom](https://atom.io/).
2. Colar Olá Go código das seções Olá abaixo em arquivos de texto e salve em sua pasta de projeto com a extensão de arquivo \*vá, como o caminho do Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` ou caminho do Linux `~/go/src/mysqlgo/createtable.go`.
3. Localizar Olá `HOST`, `DATABASE`, `USER`, e `PASSWORD` constantes em código hello e substituir valores de exemplo hello com seus próprios valores. 
4. Inicie o prompt de comando hello ou bash shell. Altere o diretório na pasta do seu projeto. Por exemplo, no Windows `cd %USERPROFILE%\go\src\mysqlgo\`. No Linux `cd ~/go/src/mysqlgo/`.  Alguns editores de IDE Olá mencionados oferecem recursos de depuração e tempo de execução sem a necessidade de comandos do shell.
5. Execute o código de saudação digitando o comando Olá `go run createtable.go` toocompile Olá aplicativo e executá-lo. 
6. Como alternativa, o código de saudação toobuild em um aplicativo nativo, `go build createtable.go`, em seguida, inicie `createtable.exe` aplicativo hello de toorun.

## <a name="connect-create-table-and-insert-data"></a>Conectar-se, criar tabela e inserir dados
A seguir use Olá código tooconnect toohello servidor, criar uma tabela e carregar Olá dados usando um **inserir** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [driver sql vá para mysql](https://github.com/go-sql-driver/mysql#installation) como toocommunicate um driver com hello banco de dados do Azure para MySQL e hello [fmt pacote](https://golang.org/pkg/fmt/)para impressa de entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure banco de dados MySQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) método toorun várias vezes vários comandos DDL. código Olá também usa Olá [Prepare()](http://go-database-sql.org/prepared.html) e EXEC () toorun preparadas com parâmetros diferentes tooinsert três linhas. Cada vez que um método personalizado checkError() é toocheck usado se ocorreu um erro e pane tooexit.

Substituir saudação `host`, `database`, `user`, e `password` constantes com seus próprios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [driver sql vá para mysql](https://github.com/go-sql-driver/mysql#installation) como toocommunicate um driver com hello banco de dados do Azure para MySQL e hello [fmt pacote](https://golang.org/pkg/fmt/)para impressa de entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure banco de dados MySQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [Query ()](https://golang.org/pkg/database/sql/#DB.Query) comando select do método toorun hello. Em seguida, ele é executado [Next ()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate por meio do conjunto de resultados de saudação e [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) valores de coluna Olá tooparse, salvar o valor de saudação em variáveis. Cada vez que um método personalizado checkError() é toocheck usado se ocorreu um erro e pane tooexit.

Substituir saudação `host`, `database`, `user`, e `password` constantes com seus próprios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [driver sql vá para mysql](https://github.com/go-sql-driver/mysql#installation) como toocommunicate um driver com hello banco de dados do Azure para MySQL e hello [fmt pacote](https://golang.org/pkg/fmt/)para impressa de entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure banco de dados MySQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) comando de atualização de saudação do método toorun. Cada vez que um método personalizado checkError() é toocheck usado se ocorreu um erro e pane tooexit.

Substituir saudação `host`, `database`, `user`, e `password` constantes com seus próprios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e remover dados usando um **excluir** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [driver sql vá para mysql](https://github.com/go-sql-driver/mysql#installation) como toocommunicate um driver com hello banco de dados do Azure para MySQL e hello [fmt pacote](https://golang.org/pkg/fmt/)para impressa de entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure banco de dados MySQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) saudação do método toorun excluir comando. Cada vez que um método personalizado checkError() é toocheck usado se ocorreu um erro e pane tooexit.

Substituir saudação `host`, `database`, `user`, e `password` constantes com seus próprios valores. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./concepts-migrate-import-export.md)
