---
title: Conectar-se ao Banco de Dados do Azure para PostgreSQL usando a linguagem Go | Microsoft Docs
description: "Este guia de início rápido fornece um exemplo em linguagem de programação Go que você pode usar para se conectar e consultar dados do Banco de Dados do Azure para PostgreSQL."
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
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="f6bf9-103">Banco de dados do Azure para PostgreSQL: usar a linguagem Go para se conectar e consultar dados</span><span class="sxs-lookup"><span data-stu-id="f6bf9-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="f6bf9-104">Este guia de início rápido demonstra como se conectar a um banco de dados do Azure para PostgreSQL usando código escrito na linguagem [Go](https://golang.org/) (golang).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="f6bf9-105">Ele mostra como usar instruções SQL para consultar, inserir, atualizar e excluir dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="f6bf9-106">Este artigo pressupõem que você está familiarizado com o desenvolvimento usando Go, mas que começou recentemente a trabalhar com o Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6bf9-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6bf9-107">Prerequisites</span></span>
<span data-ttu-id="f6bf9-108">Este guia de início rápido usa os recursos criados em um destes guias como ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="f6bf9-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="f6bf9-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="f6bf9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="f6bf9-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f6bf9-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="f6bf9-111">Instalar o conector pq e o Go</span><span class="sxs-lookup"><span data-stu-id="f6bf9-111">Install Go and pq connector</span></span>
<span data-ttu-id="f6bf9-112">Instale o [Go](https://golang.org/doc/install) e o [driver de Postgres Go puro(pq)](https://github.com/lib/pq) em seu próprio computador.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="f6bf9-113">Dependendo da sua plataforma, siga as etapas:</span><span class="sxs-lookup"><span data-stu-id="f6bf9-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="f6bf9-114">Windows</span><span class="sxs-lookup"><span data-stu-id="f6bf9-114">Windows</span></span>
1. <span data-ttu-id="f6bf9-115">[Baixe](https://golang.org/dl/) e instale o Go para Microsoft Windows de acordo com as [instruções de instalação](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="f6bf9-116">Inicie o prompt de comando no menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="f6bf9-117">Crie uma pasta para o seu projeto, como.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-117">Make a folder for your project such.</span></span> <span data-ttu-id="f6bf9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="f6bf9-119">Altere o diretório na pasta do projeto, como `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="f6bf9-120">Defina a variável de ambiente para GOPATH apontar para o diretório de código de origem.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="f6bf9-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="f6bf9-122">Instale o [driver de Postgres Go puro (pq)](https://github.com/lib/pq) executando o comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f6bf9-123">Em resumo, instale o Go e execute esses comandos no prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="f6bf9-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="f6bf9-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f6bf9-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="f6bf9-125">Abra o shell do Bash.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="f6bf9-126">Instale o Go executando `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="f6bf9-127">Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="f6bf9-128">Altere o diretório na pasta, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="f6bf9-129">Defina a variável de ambiente GOPATH para apontar para um diretório de origem válido, como a pasta atual inicial do diretório do Go.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="f6bf9-130">No shell bash, execute `export GOPATH=~/go` para adicionar o diretório do Go como GOPATH para a sessão atual do shell.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="f6bf9-131">Instale o [driver de Postgres Go puro (pq)](https://github.com/lib/pq) executando o comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f6bf9-132">Em resumo, execute estes comandos bash:</span><span class="sxs-lookup"><span data-stu-id="f6bf9-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="f6bf9-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="f6bf9-133">Apple macOS</span></span>
1. <span data-ttu-id="f6bf9-134">Baixe e instale o Go de acordo com as [instruções de instalação](https://golang.org/doc/install) correspondentes à plataforma.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="f6bf9-135">Abra o shell do Bash.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="f6bf9-136">Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="f6bf9-137">Altere o diretório na pasta, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="f6bf9-138">Defina a variável de ambiente GOPATH para apontar para um diretório de origem válido, como a pasta atual inicial do diretório do Go.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="f6bf9-139">No shell bash, execute `export GOPATH=~/go` para adicionar o diretório do Go como GOPATH para a sessão atual do shell.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="f6bf9-140">Instale o [driver de Postgres Go puro (pq)](https://github.com/lib/pq) executando o comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="f6bf9-141">Em resumo, instale o Go e, em seguida, execute esses comandos bash:</span><span class="sxs-lookup"><span data-stu-id="f6bf9-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="f6bf9-142">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="f6bf9-142">Get connection information</span></span>
<span data-ttu-id="f6bf9-143">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="f6bf9-144">Você precisa das credenciais de logon e do nome do servidor totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="f6bf9-145">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f6bf9-146">No menu à esquerda no Portal do Azure, clique em **Todos os recursos** e pesquise pelo servidor que você criou, como **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="f6bf9-147">Clique no nome do servidor **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="f6bf9-148">Selecione a página **Visão geral** do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="f6bf9-149">Anote o **Nome do servidor** e o **Nome de logon de administrador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="f6bf9-150">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="f6bf9-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="f6bf9-151">Se você se esquecer das informações de logon do servidor, navegue até a página **Visão Geral** para exibir o nome de logon do Administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="f6bf9-152">Se necessário, redefina a senha.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="f6bf9-153">Compilar e executar o código Go</span><span class="sxs-lookup"><span data-stu-id="f6bf9-153">Build and run Go code</span></span> 
1. <span data-ttu-id="f6bf9-154">Para escrever código Golang, você pode usar um editor de texto simples, como o Bloco de Notas no Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) no Ubuntu ou Editor de Texto no macOS.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="f6bf9-155">Se você preferir IDE (Ambiente de Desenvolvimento Integrado) mais avançado, experimente o [Gogland](https://www.jetbrains.com/go/) da Jetbrains, o [Visual Studio Code](https://code.visualstudio.com/) da Microsoft ou o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="f6bf9-156">Cole o código Golang das seções abaixo em arquivos de texto e salve-os em sua pasta de projeto com a extensão de arquivo \*.go, como caminho do Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ou caminho do Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="f6bf9-157">Localize as constantes `HOST`, `DATABASE`, `USER`, e `PASSWORD` no código e substitua os valores de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="f6bf9-158">Inicie o prompt de comando ou shell Bash.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="f6bf9-159">Altere o diretório na pasta do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-159">Change directory into your project folder.</span></span> <span data-ttu-id="f6bf9-160">Por exemplo, no Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="f6bf9-161">No Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="f6bf9-162">Alguns dos ambientes IDE mencionados oferecem recursos de depuração e tempo de execução sem a necessidade de comandos do shell.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="f6bf9-163">Execute o código, digitando o comando `go run createtable.go` para compilar o aplicativo e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="f6bf9-164">Como alternativa, para compilar o código em um aplicativo nativo, `go build createtable.go`, inicie `createtable.exe` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="f6bf9-165">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="f6bf9-165">Connect and create a table</span></span>
<span data-ttu-id="f6bf9-166">Use o código a seguir para se conectar e criar uma tabela usando a instrução SQL **CREATE TABLE**, seguida por instruções SQL **INSERT INTO** para adicionar linhas à tabela.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="f6bf9-167">O código importa três pacotes: o [pacote sql](https://golang.org/pkg/database/sql/), o [pacote pq](http://godoc.org/github.com/lib/pq) como driver para se comunicar com o servidor Postgres e o [fmt pacote](https://golang.org/pkg/fmt/) para impressão de entrada e saída na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f6bf9-168">O código chama o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) para se conectar ao Banco de Dados do Azure para PostgreSQL e verifica a conexão usando o método [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f6bf9-169">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado em todo o processo, mantendo o pool de conexão para o servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f6bf9-170">O código chama o método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) várias vezes para executar vários comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="f6bf9-171">A cada ocorrência, um método personalizado checkError() para verificar se ocorreu um erro e pane para sair em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f6bf9-172">Substitua os parâmetros `HOST`, `DATABASE`, `USER`, e `PASSWORD` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="read-data"></a><span data-ttu-id="f6bf9-173">Ler dados</span><span class="sxs-lookup"><span data-stu-id="f6bf9-173">Read data</span></span>
<span data-ttu-id="f6bf9-174">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="f6bf9-175">O código importa três pacotes: o [pacote sql](https://golang.org/pkg/database/sql/), o [pacote pq](http://godoc.org/github.com/lib/pq) como driver para se comunicar com o servidor Postgres e o [fmt pacote](https://golang.org/pkg/fmt/) para impressão de entrada e saída na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f6bf9-176">O código chama o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) para se conectar ao Banco de Dados do Azure para PostgreSQL e verifica a conexão usando o método [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f6bf9-177">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado em todo o processo, mantendo o pool de conexão para o servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f6bf9-178">A consulta select é executada chamando o método [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), e as linhas resultantes são mantidas em uma variável do tipo [linhas](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="f6bf9-179">O código lê a coluna de valores de dados na linha atual usando o método [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) e loops em relação às linhas usando o iterador [rows.Next ()](https://golang.org/pkg/database/sql/#Rows.Next) até que não haja mais linhas.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="f6bf9-180">Os valores de coluna de cada linha são impressos no console de saída. A cada ocorrência, um método personalizado checkError() para verificar se ocorreu um erro e pane para sair em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f6bf9-181">Substitua os parâmetros `HOST`, `DATABASE`, `USER`, e `PASSWORD` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="update-data"></a><span data-ttu-id="f6bf9-182">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="f6bf9-182">Update data</span></span>
<span data-ttu-id="f6bf9-183">Use o código a seguir para conectar-se e atualizar os dados usando uma instrução SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="f6bf9-184">O código importa três pacotes: o [pacote sql](https://golang.org/pkg/database/sql/), o [pacote pq](http://godoc.org/github.com/lib/pq) como driver para se comunicar com o servidor Postgres e o [fmt pacote](https://golang.org/pkg/fmt/) para impressão de entrada e saída na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f6bf9-185">O código chama o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) para se conectar ao Banco de Dados do Azure para PostgreSQL e verifica a conexão usando o método [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f6bf9-186">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado em todo o processo, mantendo o pool de conexão para o servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f6bf9-187">O código chama o método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) para executar a instrução SQL que atualiza a tabela.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="f6bf9-188">Um método personalizado checkError() para verificar se ocorreu um erro e pane para sair em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f6bf9-189">Substitua os parâmetros `HOST`, `DATABASE`, `USER`, e `PASSWORD` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="f6bf9-190">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="f6bf9-190">Delete data</span></span>
<span data-ttu-id="f6bf9-191">Use o código a seguir para conectar-se e ler os dados usando uma instrução SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="f6bf9-192">O código importa três pacotes: o [pacote sql](https://golang.org/pkg/database/sql/), o [pacote pq](http://godoc.org/github.com/lib/pq) como driver para se comunicar com o servidor Postgres e o [fmt pacote](https://golang.org/pkg/fmt/) para impressão de entrada e saída na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="f6bf9-193">O código chama o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) para se conectar ao Banco de Dados do Azure para PostgreSQL e verifica a conexão usando o método [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="f6bf9-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="f6bf9-194">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado em todo o processo, mantendo o pool de conexão para o servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="f6bf9-195">O código chama o método [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) para executar a instrução SQL que atualiza a tabela.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="f6bf9-196">Um método personalizado checkError() para verificar se ocorreu um erro e pane para sair em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="f6bf9-197">Substitua os parâmetros `HOST`, `DATABASE`, `USER`, e `PASSWORD` pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="f6bf9-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="f6bf9-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6bf9-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f6bf9-199">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="f6bf9-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
