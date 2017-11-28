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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="e338e-103">Banco de dados do Azure para PostgreSQL: vá usar linguagem tooconnect e consultar dados</span><span class="sxs-lookup"><span data-stu-id="e338e-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="e338e-104">Este guia de início rápido demonstra como tooconnect tooan banco de dados do Azure para PostgreSQL usando código escrito em hello [vá](https://golang.org/) idioma (golang).</span><span class="sxs-lookup"><span data-stu-id="e338e-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="e338e-105">Ele mostra como toouse tooquery de instruções SQL, inserir, atualizar e excluir dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="e338e-106">Este artigo pressupõe que você esteja familiarizado com o desenvolvimento usando Go, mas que são novos tooworking com o banco de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e338e-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e338e-107">Prerequisites</span></span>
<span data-ttu-id="e338e-108">Este guia de início rápido usa recursos de saudação criados em qualquer um desses guias como um ponto de partida:</span><span class="sxs-lookup"><span data-stu-id="e338e-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e338e-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="e338e-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="e338e-110">Criar Banco de dados - CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e338e-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="e338e-111">Instalar o conector pq e o Go</span><span class="sxs-lookup"><span data-stu-id="e338e-111">Install Go and pq connector</span></span>
<span data-ttu-id="e338e-112">Instalar [vá](https://golang.org/doc/install) e hello [puro Postgres vá driver (pq)](https://github.com/lib/pq) em seu próprio computador.</span><span class="sxs-lookup"><span data-stu-id="e338e-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="e338e-113">Dependendo de sua plataforma, siga as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="e338e-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="e338e-114">Windows</span><span class="sxs-lookup"><span data-stu-id="e338e-114">Windows</span></span>
1. <span data-ttu-id="e338e-115">[Baixar](https://golang.org/dl/) e instale a ir para o Microsoft Windows de acordo com o toohello [instruções de instalação](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="e338e-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="e338e-116">Inicie o prompt de comando Olá Olá do menu de início.</span><span class="sxs-lookup"><span data-stu-id="e338e-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="e338e-117">Crie uma pasta para o seu projeto, como.</span><span class="sxs-lookup"><span data-stu-id="e338e-117">Make a folder for your project such.</span></span> <span data-ttu-id="e338e-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="e338e-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="e338e-119">Altere o diretório na pasta de projeto hello, como `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="e338e-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="e338e-120">Definir variável de ambiente Olá para o diretório de código de origem do GOPATH toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="e338e-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="e338e-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="e338e-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="e338e-122">Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="e338e-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="e338e-123">Em resumo, instalar Go, execute estes comandos no prompt de comando hello:</span><span class="sxs-lookup"><span data-stu-id="e338e-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="e338e-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e338e-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="e338e-125">Inicie o shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="e338e-126">Instale o Go executando `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="e338e-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="e338e-127">Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="e338e-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="e338e-128">Altere o diretório para pasta hello, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="e338e-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="e338e-129">Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta.</span><span class="sxs-lookup"><span data-stu-id="e338e-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="e338e-130">No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="e338e-131">Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="e338e-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="e338e-132">Em resumo, execute estes comandos bash:</span><span class="sxs-lookup"><span data-stu-id="e338e-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="e338e-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="e338e-133">Apple macOS</span></span>
1. <span data-ttu-id="e338e-134">Baixe e instale ir de acordo com o toohello [instruções de instalação](https://golang.org/doc/install) sua plataforma de correspondência.</span><span class="sxs-lookup"><span data-stu-id="e338e-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="e338e-135">Inicie o shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="e338e-136">Crie uma pasta para o seu projeto em seu diretório inicial, como `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="e338e-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="e338e-137">Altere o diretório para pasta hello, como `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="e338e-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="e338e-138">Conjunto Olá GOPATH ambiente variável toopoint tooa válido diretório de origem, como a página inicial atual do diretório acesse a pasta.</span><span class="sxs-lookup"><span data-stu-id="e338e-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="e338e-139">No shell bash de hello, execute `export GOPATH=~/go` tooadd Olá vá diretório como hello GOPATH para a sessão atual de shell hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="e338e-140">Instalar Olá [puro Postgres vá driver (pq)](https://github.com/lib/pq) executando Olá `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="e338e-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="e338e-141">Em resumo, instale o Go e, em seguida, execute esses comandos bash:</span><span class="sxs-lookup"><span data-stu-id="e338e-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="e338e-142">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="e338e-142">Get connection information</span></span>
<span data-ttu-id="e338e-143">Obter Olá conexão informações necessárias tooconnect toohello banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e338e-144">Você precisa Olá credenciais de logon e de nome totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e338e-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e338e-145">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e338e-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e338e-146">No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos** e pesquisa para o servidor de saudação que você criou, como **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="e338e-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="e338e-147">Clique em nome do servidor de saudação **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="e338e-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="e338e-148">Servidor de saudação selecione **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="e338e-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="e338e-149">Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="e338e-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e338e-150">![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="e338e-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="e338e-151">Se você esquecer suas informações de logon de servidor, navegue toohello **visão geral** página e o nome de logon do modo de exibição Olá servidor admin.</span><span class="sxs-lookup"><span data-stu-id="e338e-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="e338e-152">Se necessário, Olá redefinição da senha.</span><span class="sxs-lookup"><span data-stu-id="e338e-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="e338e-153">Compilar e executar o código Go</span><span class="sxs-lookup"><span data-stu-id="e338e-153">Build and run Go code</span></span> 
1. <span data-ttu-id="e338e-154">toowrite Golang código, você pode usar um editor de texto simples, como o bloco de notas no Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) no Ubuntu ou editor de texto no macOS.</span><span class="sxs-lookup"><span data-stu-id="e338e-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="e338e-155">Se você preferir IDE (Ambiente de Desenvolvimento Integrado) mais avançado, experimente o [Gogland](https://www.jetbrains.com/go/) da Jetbrains, o [Visual Studio Code](https://code.visualstudio.com/) da Microsoft ou o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="e338e-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="e338e-156">Colar o código de Golang de saudação do seções Olá abaixo para arquivos de texto e salve em sua pasta de projeto com a extensão de arquivo \*vá, como o caminho do Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ou caminho do Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="e338e-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="e338e-157">Localizar Olá `HOST`, `DATABASE`, `USER`, e `PASSWORD` constantes em código hello e substituir valores de exemplo hello com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e338e-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="e338e-158">Inicie o prompt de comando hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="e338e-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="e338e-159">Altere o diretório na pasta do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e338e-159">Change directory into your project folder.</span></span> <span data-ttu-id="e338e-160">Por exemplo, no Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="e338e-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="e338e-161">No Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="e338e-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="e338e-162">Alguns dos ambientes de IDE Olá mencionados oferecem recursos de depuração e tempo de execução sem a necessidade de comandos do shell.</span><span class="sxs-lookup"><span data-stu-id="e338e-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="e338e-163">Execute o código de saudação digitando o comando Olá `go run createtable.go` toocompile Olá aplicativo e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="e338e-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="e338e-164">Como alternativa, o código de saudação toobuild em um aplicativo nativo, `go build createtable.go`, em seguida, inicie `createtable.exe` aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="e338e-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="e338e-165">Conectar-se e criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="e338e-165">Connect and create a table</span></span>
<span data-ttu-id="e338e-166">A seguir use Olá tooconnect de código e criar uma tabela usando **CREATE TABLE** instrução SQL, seguida por **INSERT INTO** linhas de tooadd de instruções SQL em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="e338e-167">código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="e338e-168">Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="e338e-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="e338e-169">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="e338e-170">saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) método toorun várias vezes vários comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="e338e-171">Cada vez que um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="e338e-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="e338e-172">Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e338e-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="e338e-173">Ler dados</span><span class="sxs-lookup"><span data-stu-id="e338e-173">Read data</span></span>
<span data-ttu-id="e338e-174">A seguir use Olá código tooconnect e ler Olá dados usando um **selecione** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="e338e-175">código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="e338e-176">Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="e338e-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="e338e-177">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="e338e-178">consulta select Olá é executada chamando o método [banco de dados. Query ()](https://golang.org/pkg/database/sql/#DB.Query), e as linhas resultantes da saudação é mantido em uma variável do tipo [linhas](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="e338e-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="e338e-179">código de saudação lê valores de dados de coluna Olá na linha atual do hello usando o método [linhas. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) e loops em linhas de saudação usando iterador Olá [linhas. Next ()](https://golang.org/pkg/database/sql/#Rows.Next) até que não há mais linhas existem.</span><span class="sxs-lookup"><span data-stu-id="e338e-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="e338e-180">Valores de coluna de cada linha são impressos toohello console out. Cada vez que um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="e338e-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="e338e-181">Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e338e-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="e338e-182">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="e338e-182">Update data</span></span>
<span data-ttu-id="e338e-183">A seguir use Olá tooconnect de código e atualizar Olá dados usando um **atualizar** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="e338e-184">código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="e338e-185">Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="e338e-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="e338e-186">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="e338e-187">saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) saudação do método toorun instrução SQL que atualiza a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="e338e-188">Um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se um erro ocorrerá.</span><span class="sxs-lookup"><span data-stu-id="e338e-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="e338e-189">Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e338e-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="delete-data"></a><span data-ttu-id="e338e-190">Excluir dados</span><span class="sxs-lookup"><span data-stu-id="e338e-190">Delete data</span></span>
<span data-ttu-id="e338e-191">A seguir use Olá código tooconnect e ler Olá dados usando um **excluir** instrução SQL.</span><span class="sxs-lookup"><span data-stu-id="e338e-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e338e-192">código Olá importa três pacotes: Olá [pacote sql](https://golang.org/pkg/database/sql/), Olá [pacote pq](http://godoc.org/github.com/lib/pq) como toocommunicate um driver com hello Postgres server e Olá [fmt pacote](https://golang.org/pkg/fmt/) por impressos entrada e saída na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="e338e-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="e338e-193">Olá código chamar o método [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure banco de dados PostgreSQL e verificações de saudação conexão usando o método [banco de dados. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="e338e-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="e338e-194">Um [identificador de banco de dados](https://golang.org/pkg/database/sql/#DB) é usado no todo, mantendo o pool de conexão Olá para o servidor de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="e338e-195">saudação de chamadas de código Olá [EXEC ()](https://golang.org/pkg/database/sql/#DB.Exec) saudação do método toorun instrução SQL que atualiza a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e338e-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="e338e-196">Um toocheck do método checkError() personalizado se ocorreu um erro e pane tooexit se um erro ocorrerá.</span><span class="sxs-lookup"><span data-stu-id="e338e-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="e338e-197">Substituir saudação `HOST`, `DATABASE`, `USER`, e `PASSWORD` parâmetros com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e338e-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="e338e-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e338e-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e338e-199">Migre seu banco de dados usando Exportar e Importar</span><span class="sxs-lookup"><span data-stu-id="e338e-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
