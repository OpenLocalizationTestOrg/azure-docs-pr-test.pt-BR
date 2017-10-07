---
title: aaaConnect tooAzure banco de dados PostgreSQL usando linguagem Go | Microsoft Docs
description: "Este guia de início rápido fornece um Go idioma programação exemplo você pode usar tooconnect e consultar dados do banco de dados PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Banco de dados do Azure para PostgreSQL: vá usar linguagem tooconnect e consultar dados
Este guia de início rápido demonstra como tooconnect tooan banco de dados do Azure para PostgreSQL usando código escrito em hello [vá](https://golang.org/) idioma (golang). Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação. Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando Go, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.

## <a name="prerequisites"></a>Pré-requisitos
Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:
- [Criar Banco de dados - Portal](quickstart-create-server-database-portal.md)
- [Criar Banco de dados - CLI do Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Instalar o conector pq e o Go
Instalar [vá](https://golang.org/doc/install) e hello [puro Postgres vá driver (pq)](https://github.com/lib/pq) em seu próprio computador. Dependendo de sua plataforma, siga as etapas de saudação:

### <a name="windows"></a>Windows
1. [Baixar](https://golang.org/dl/) e instale a ir para o Microsoft Windows de acordo com o toohello [instruções de instalação](https://golang.org/doc/install).
2. Inicie o prompt de comando Olá Olá do menu de início.
3. Crie uma pasta para o seu projeto, como. `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Altere o diretório na pasta de projeto hello, como `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Definir variável de ambiente Olá para o diretório de código de origem do GOPATH toopoint toohello. `set GOPATH=%USERPROFILE%\go`.
6. Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.

   Em resumo, instalar Go, execute estes comandos no prompt de comando hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Inicie o shell Bash hello. 
2. Instale o Go executando `sudo apt-get install golang-go`.
3. Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.
4. Altere o diretório para pasta hello, como `cd ~/go/src/postgresqlgo/`.
5. Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta. No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.
6. Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.

   Em resumo, execute estes comandos bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. Baixe e instale ir de acordo com o toohello [instruções de instalação](https://golang.org/doc/install) sua plataforma de correspondência. 
2. Inicie o shell Bash hello. 
3. Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.
4. Altere o diretório para pasta hello, como `cd ~/go/src/postgresqlgo/`.
5. Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta. No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.
6. Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.

   Em resumo, instale o Go e, em seguida, execute esses comandos bash:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Obter informações de conexão
Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL. Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
2. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.
3. Clique em nome do servidor de saudação **mypgserver 20170401**.
4. Servidor de saudação selecione **visão geral** página. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-go/1-connection-string.png)
5. Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página e o nome de logon do modo de exibição Olá servidor admin. Se necessário, Olá redefinição da senha.

## <a name="build-and-run-go-code"></a>Compilar e executar o código Go 
1. toowrite Golang código, você pode usar um editor de texto simples, como o bloco de notas no Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) no Ubuntu ou editor de texto no macOS. Se você preferir IDE (Ambiente de Desenvolvimento Integrado) mais avançado, experimente o [Gogland](https://www.jetbrains.com/go/) da Jetbrains, o [Visual Studio Code](https://code.visualstudio.com/) da Microsoft ou o [Atom](https://atom.io/).
2. Colar o código de Golang de saudação do seções Olá abaixo para arquivos de texto e salve em sua pasta de projeto com a extensão de arquivo \*vá, como o caminho do Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ou caminho do Linux `~/go/src/postgresqlgo/createtable.go`.
3. Localizar Olá `HOST`, `DATABASE`, `USER`, e `PASSWORD` constantes em código hello e substituir valores de exemplo hello com seus próprios valores.  
4. Inicie o prompt de comando hello ou bash shell. Altere o diretório na pasta do seu projeto. Por exemplo, no Windows `cd %USERPROFILE%\go\src\postgresqlgo\`. No Linux `cd ~/go/src/postgresqlgo/`. Alguns dos ambientes de IDE Olá mencionados oferecem recursos de depuração e tempo de execução sem a necessidade de comandos do shell.
5. Execute o código de saudação digitando o comando Olá `go run createtable.go` toocompile Olá aplicativo e executá-lo. 
6. Como alternativa, o código de saudação toobuild em um aplicativo nativo, `go build createtable.go`, em seguida, inicie `createtable.exe` aplicativo hello de toorun.

## <a name="connect-and-create-a-table"></a>Conectar-se e criar uma tabela
A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) método toorun várias vezes vários comandos SQL. Cada vez que um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se ocorrer um erro.

Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>Ler dados
A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. consulta select Olá é executada chamando o método [banco de dados. Query ()](https://golang.org/pkg/database/sql/#DB.Query), e as linhas resultantes da saudação é mantido em uma variável do tipo [linhas](https://golang.org/pkg/database/sql/#Rows). código de saudação lê valores de dados de coluna Olá na linha atual do hello usando o método [linhas. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) e loops em linhas de saudação usando iterador Olá [linhas. Next ()](https://golang.org/pkg/database/sql/#Rows.Next) até que não há mais linhas existem. Valores de coluna de cada linha são impressos toohello console out. Cada vez que um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se ocorrer um erro.

Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>Atualizar dados
A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) saudação do método toorun instrução SQL que atualiza a tabela de saudação. Um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se um erro ocorrerá.

Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>Excluir dados
A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL. 

código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.

Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação. saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) saudação do método toorun instrução SQL que atualiza a tabela de saudação. Um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se um erro ocorrerá.

Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
