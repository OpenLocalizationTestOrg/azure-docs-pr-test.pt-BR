---
title: aaaBuild um aplicativo web PHP e MySQL no Azure | Microsoft Docs
description: "Saiba como tooget um aplicativo PHP trabalhando no Azure, com tooa de conexão MySQL do banco de dados no Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Compilar um aplicativo Web PHP e MySQL no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches. Este tutorial mostra como toocreate um PHP aplicativo no Azure da web e conectá-lo tooa banco de dados MySQL. Quando terminar, você terá um aplicativo [Laravel](https://laravel.com/) em execução nos Aplicativos Web do Serviço de Aplicativo do Azure.

![Aplicativo PHP em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um banco de dados MySQL no Azure
> * Conecte-se um tooMySQL do aplicativo PHP
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Transmitir logs de diagnóstico do Azure
> * Gerenciar o aplicativo hello em Olá portal do Azure

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

* [Instalar o Git](https://git-scm.com/)
* [Instalar o PHP 5.6.4 ou posterior](http://php.net/downloads.php)
* [Instalar o Composer](https://getcomposer.org/doc/00-intro.md)
* Habilitar Olá extensões PHP Laravel necessidades a seguir: OpenSSL PDO MySQL, Mbstring, Tokenizer, XML
* [Instalar e iniciar o MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Preparar o MySQL local

Nesta etapa, você cria um banco de dados em seu servidor MySQL local para uso neste tutorial.

### <a name="connect-toolocal-mysql-server"></a>Conecte-se toolocal MySQL server

Em uma janela de terminal, conecte-se tooyour local MySQL server. Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.

```bash
mysql -u root -p
```

Se você for solicitado a fornecer uma senha, digite a senha de saudação para Olá `root` conta. Se você não lembrar a senha da conta raiz, consulte [MySQL: como tooReset Olá senha raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Se o comando for executado com êxito, o MySQL Server estará em execução. Se não, certifique-se de que o servidor MySQL local é iniciado por seguir Olá [etapas de pós-instalação do MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Criar um banco de dados localmente

Em Olá `mysql` solicitar, crie um banco de dados.

```sql 
CREATE DATABASE sampledb;
```

Saia da conexão do servidor digitando `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Criar um aplicativo PHP localmente
Nesta etapa, você obtém um aplicativo de exemplo Laravel, configura sua conexão de banco de dados e o executa localmente. 

### <a name="clone-hello-sample"></a>Exemplo de saudação do clone

Na janela do terminal hello, `cd` tooa diretório de trabalho.

Execute Olá repositório de exemplo do comando tooclone Olá a seguir.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`diretório de tooyour clonado.
Instale pacotes de saudação necessário.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Configurar a conexão do MySQL

Na raiz do repositório hello, crie um arquivo chamado *.env*. Saudação de cópia variáveis a seguir em hello *.env* arquivo. Substituir saudação  _&lt;root_password >_ espaço reservado com a senha do usuário do hello MySQL raiz.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Para obter informações sobre como Laravel usa Olá _.env_ de arquivos, consulte [configuração do ambiente Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Executar o exemplo hello localmente

Executar [migrações de banco de dados de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Olá tabelas Olá as necessidades do aplicativo. toosee quais tabelas são criadas em migrações hello, procure no hello _banco de dados/migrações_ diretório no repositório do Git hello.

```bash
php artisan migrate
```

Gere uma nova chave de aplicativo do Laravel.

```bash
php artisan key:generate
```

Execute o aplicativo hello.

```bash
php artisan serve
```

Navegue muito`http://localhost:8000` em um navegador. Adicione algumas tarefas na página de saudação.

![PHP se conecta com êxito tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Digite toostop PHP, `Ctrl + C` em Olá terminal.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Criar o MySQL no Azure

Nesta etapa, você cria um banco de dados MySQL no [Banco de dados do Azure para MySQL (versão prévia)](/azure/mysql). Posteriormente, você pode configurar Olá PHP aplicativo tooconnect toothis banco de dados.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Criar um servidor MySQL

Criar um servidor de banco de dados do Azure para MySQL (visualização) com hello [az mysql server criar](/cli/azure/mysql/server#create) comando.

Olá a seguir de comando, substitua o nome do servidor MySQL onde você pode ver Olá  _&lt;mysql_server_name >_ espaço reservado (caracteres válidos são `a-z`, `0-9`, e `-`). Esse nome faz parte do nome do host do servidor de saudação MySQL (`<mysql_server_name>.database.windows.net`), ele precisa toobe globalmente exclusivo.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Quando o servidor do hello MySQL é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Configurar o firewall do servidor

Criar uma regra de firewall para o cliente do MySQL server tooallow conexões usando Olá [criar regra de firewall de servidor de mysql de az](/cli/azure/mysql/server/firewall-rule#create) comando.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Banco de dados do Azure para MySQL (visualização) atualmente não limita os serviços tooAzure somente conexões. Como os endereços IP no Azure são atribuídos dinamicamente, é melhor tooenable todos os endereços IP. serviço de saudação está em visualização. Estamos planejando melhores métodos para proteger o banco de dados.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Conecte-se tooproduction do MySQL server localmente

Na janela do terminal hello, conecte-se toohello MySQL server no Azure. Usar valor Olá especificado anteriormente para  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Quando for solicitada uma senha, use _tr0ngPa $$ w0rd!_, que você especificou quando criou o banco de dados de saudação.

### <a name="create-a-production-database"></a>Criar um banco de dados de produção

Em Olá `mysql` solicitar, crie um banco de dados.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Criar um usuário com permissões

Crie um usuário de banco de dados chamado _phpappuser_ e dê a ele todos os privilégios em Olá `sampledb` banco de dados.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Saia de conexão do servidor de saudação digitando `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Conecte-se o aplicativo tooAzure MySQL

Nesta etapa, você pode se conectar Olá PHP aplicativo toohello banco de dados MySQL que é criado no banco de dados do Azure para MySQL (visualização).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Configurar conexão do banco de dados de saudação

Na raiz do repositório hello, crie um _. env.production_ arquivo e cópia Olá variáveis a seguir para ele. Substitua o espaço reservado de saudação  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Salve alterações de saudação.

> [!TIP]
> toosecure suas informações de conexão do MySQL, esse arquivo já foi excluídas do repositório do Git de saudação (consulte _. gitignore_ na raiz do repositório de saudação). Posteriormente, você aprenderá como variáveis de ambiente tooconfigure no serviço de aplicativo tooconnect tooyour banco de dados no banco de dados do Azure para MySQL (visualização). Com variáveis de ambiente, você não precisa Olá *.env* arquivo no serviço de aplicativo.
>

### <a name="configure-ssl-certificate"></a>Configurar o certificado SSL

Por padrão, o Banco de Dados do Azure para MySQL impõe conexões SSL de clientes. tooconnect tooyour banco de dados MySQL no Azure, você deve usar um _. PEM_ certificado SSL.

Abra _config/database.php_ e adicione Olá _sslmode_ e _opções_ parâmetros muito`connections.mysql`, conforme mostrado na saudação de código a seguir.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn como toogenerate isso _certificate.pem_, consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> caminho de saudação _/ssl/certificate.pem_ aponta existente tooan _certificate.pem_ arquivo no repositório do Git de saudação. Esse arquivo é fornecido para conveniência neste tutorial. Como melhor prática, você não deve confirmar os certificados _.pem_ no controle do código-fonte. 
>

### <a name="test-hello-application-locally"></a>Testar o aplicativo hello localmente

Executar migrações de banco de dados Laravel com _. env.production_ como hello tabelas de saudação do ambiente arquivo toocreate no banco de dados MySQL no banco de dados do Azure para MySQL (visualização). Lembre-se de que _. env.production_ tem o banco de dados do hello conexão informações tooyour MySQL no Azure.

```bash
php artisan migrate --env=production --force
```

_.env.production_ ainda não tem uma chave de aplicativo válida. Gere um novo para ele no hello terminal.

```bash
php artisan key:generate --env=production --force
```

Execute o aplicativo de exemplo hello com _. env.production_ como arquivo de saudação do ambiente.

```bash
php artisan serve --env=production
```

Navegue muito`http://localhost:8000`. Se a página de saudação carregado sem erros, Olá aplicativo PHP está se conectando toohello banco de dados MySQL no Azure.

Adicione algumas tarefas na página de saudação.

![PHP se conecta com êxito tooAzure banco de dados MySQL (visualização)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Digite toostop PHP, `Ctrl + C` em Olá terminal.

### <a name="commit-your-changes"></a>Confirmar as alterações

Execute seguinte Olá Git comandos toocommit suas alterações:

```bash
git add .
git commit -m "database.php updates"
```

Seu aplicativo estiver pronto toobe implantado.

## <a name="deploy-tooazure"></a>Implantar tooAzure

Nesta etapa, você deve implantar Olá conectado MySQL PHP aplicativo tooAzure do serviço de aplicativo.

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Criar um aplicativo Web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Versão do PHP Olá conjunto

Versão do PHP Olá conjunto que Olá aplicativo requer usando Olá [az webapp config conjunto](/cli/azure/webapp/config#set) comando.

Olá comando a seguir define Olá PHP versão too_7.0_.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Definir configurações de banco de dados

Como apontado anteriormente, você pode conectar o banco de dados do Azure MySQL tooyour usando variáveis de ambiente do serviço de aplicativo.

No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.

Olá, comando a seguir define as configurações de aplicativo de Olá `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`. Substitua os espaços reservados de saudação  _&lt;appname >_ e  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Você pode usar o hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess método hello configurações. Olá Laravel código usa um [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper Olá PHP `getenv`. Por exemplo, configuração de MySQL Olá em _config/database.php_ aparência Olá código a seguir:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Configurar variáveis de ambiente do Laravel

O Laravel precisa de uma chave de aplicativo no Serviço de Aplicativo. É possível configurá-la com as configurações do aplicativo.

Use `php artisan` toogenerate uma nova chave de aplicativo sem salvá-la too_.env_.

```bash
php artisan key:generate --show
```

Definir chave de aplicativo hello em saudação do serviço de aplicativo aplicativo web usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando. Substitua os espaços reservados de saudação  _&lt;appname >_ e  _&lt;outputofphpartisankey: gerar >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`informa Laravel tooreturn informações de depuração quando Olá implantado o aplicativo web encontram erros. Ao executar um aplicativo de produção, defina-o muito`false`, que é mais seguro.

### <a name="set-hello-virtual-application-path"></a>Definir caminho de aplicativo virtual Olá

Definir caminho de aplicativo virtual Olá para o aplicativo web de saudação. Esta etapa é necessária porque Olá [Laravel ciclo de vida do aplicativo](https://laravel.com/docs/5.4/lifecycle) começa em Olá _pública_ diretório em vez do diretório raiz do aplicativo hello. Outras estruturas PHP cujo ciclo de vida iniciar no diretório raiz de saudação podem trabalhar sem configuração manual do caminho de aplicativo virtual hello.

Definir caminho de aplicativo virtual hello usando Olá [atualização de recurso az](/cli/azure/resource#update) comando. Substituir saudação  _&lt;appname >_ espaço reservado.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

Por padrão, o serviço de aplicativo do Azure pontos de caminho de aplicativo virtual raiz hello (_/_) toohello diretório de raiz de saudação implantado arquivos de aplicativo (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Configurar um usuário de implantação

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Configurar a implantação do git local

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>TooAzure de envio por push do Git

Adicione um repositório Git local do Azure tooyour remoto.

```bash
git remote add azure <paste_copied_url_here>
```

Enviar por push o aplicativo de PHP de hello toohello toodeploy remoto do Azure. Você será solicitado para senha Olá fornecidas anteriormente como parte da criação de saudação do usuário de implantação de saudação.

```bash
git push azure master
```

Durante a implantação, o Serviço de Aplicativo do Azure comunica seu andamento com o Git.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Você pode perceber que o processo de implantação de saudação instala [criador](https://getcomposer.org/) pacotes final hello. Serviço de aplicativo não executa esses automações durante a implantação padrão, para que este repositório de exemplo tem três adicionais arquivos no seu tooenable de diretório raiz-lo:
>
> - `.deployment`-Este arquivo informa ao serviço de aplicativo toorun `bash deploy.sh` como script de implantação personalizada hello.
> - `deploy.sh`-Olá script de implantação personalizada. Se você revisar o arquivo hello, você verá que ele seja executado `php composer.phar install` depois `npm install`.
> - `composer.phar`-Gerenciador de pacote de criador de saudação.
>
> Você pode usar essa abordagem tooadd tooApp de implantação com base em Git de tooyour qualquer etapa serviço. Para obter mais informações, consulte [Script de implantação personalizado](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Procurar o aplicativo web do Azure de toohello

Procurar muito`http://<app_name>.azurewebsites.net` e adicionar a lista de toohello algumas tarefas.

![Aplicativo PHP em execução no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Parabéns! Você está executando um aplicativo PHP controlado por dados no Serviço de Aplicativo do Azure.

## <a name="update-model-locally-and-redeploy"></a>Atualizar o modelo localmente e reimplantar

Nesta etapa, você fizer uma alteração simples toohello `task` dados de modelo e Olá webapp e, em seguida, publicar Olá tooAzure de atualização.

Para o cenário de tarefas hello, você deve modificar um aplicativo hello para que você possa marcar uma tarefa como concluída.

### <a name="add-a-column"></a>Adicionar uma coluna

No hello terminal, navegue toohello raiz do repositório do Git de saudação.

Gerar uma nova migração de banco de dados para Olá `tasks` tabela:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Este comando mostra Olá o nome do arquivo de migração de saudação que é gerado. Localize esse arquivo em _database/migrations_ e abra-o.

Substituir saudação `up` método com hello código a seguir:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Olá código acima adiciona uma coluna booleana Olá `tasks` tabela chamada `complete`.

Substituir saudação `down` método com hello código para a ação de reversão Olá a seguir:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

No Olá terminal, execute Laravel banco de dados migrações toomake Olá de alterações no banco de dados local Olá.

```bash
php artisan migrate
```

Com base em Olá [convenção de nomenclatura Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo Olá `Task` (consulte _app/Task.php_) mapeia toohello `tasks` tabela por padrão.

### <a name="update-application-logic"></a>Atualizar a lógica do aplicativo

Olá abrir *routes/web.php* arquivo. aplicativo Hello define sua rotas e a lógica de negócios aqui.

No final de saudação do arquivo hello, adicione uma rota com hello código a seguir:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Olá código anterior faz com que um modelo de dados simples atualização toohello alternando o valor de saudação do `complete`.

### <a name="update-hello-view"></a>Atualizar exibição Olá

Olá abrir *resources/views/tasks.blade.php* arquivo. Localize Olá `<tr>` marca de abertura e substituí-lo:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Olá anterior a cor de linha do código alterações Olá dependendo se a tarefa de saudação é concluída.

Na próxima linha de saudação, você tem Olá código a seguir:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Substitua linha inteira Olá Olá código a seguir:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Olá código acima adiciona botão de envio de saudação que faz referência a rota Olá definido anteriormente.

### <a name="test-hello-changes-locally"></a>Teste as mudanças de saudação localmente

Diretório raiz de saudação do repositório do Git hello, execute o servidor de desenvolvimento hello.

```bash
php artisan serve
```

Olá toosee alteração de status de tarefas, navegue até muito`http://localhost:8000` e Olá selecione caixa de seleção.

![Caixa de seleção adicionado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

Digite toostop PHP, `Ctrl + C` em Olá terminal.

### <a name="publish-changes-tooazure"></a>Publicar alterações tooAzure

Olá terminal, execute Laravel migrações de banco de dados com Olá Olá de toomake de cadeia de caracteres de conexão de produção alterar no hello banco de dados do Azure.

```bash
php artisan migrate --env=production --force
```

Confirmar todas as alterações de saudação no Git e, em seguida, enviar por push Olá tooAzure de alterações de código.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Uma vez Olá `git push` é concluída, navegue até toohello web do Azure aplicativo e teste Olá nova funcionalidade.

![Alterações de modelo e o banco de dados publicado tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Se você tiver adicionado todas as tarefas, eles são mantidos no banco de dados de saudação. Esquema de atualizações de dados toohello deixar os dados existentes intactas.

## <a name="stream-diagnostic-logs"></a>Logs de diagnóstico de fluxo

Enquanto Olá aplicativo PHP é executado no serviço de aplicativo do Azure, você pode obter Olá console logs canalizado tooyour terminal. Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.

log toostart streaming use Olá [final de log webapp az](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Depois de iniciado o fluxo de log, atualização de aplicativo web do Azure Olá Olá navegador tooget parte do tráfego da web. Agora você pode ver o terminal do console logs toohello indicada. Se você não vir os logs do console imediatamente, verifique novamente após 30 segundos.

log toostop streaming a qualquer momento, tipo `Ctrl` + `C`.

> [!TIP]
> Um aplicativo PHP pode usar o padrão de saudação [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console. aplicativo de exemplo Hello usa essa abordagem em _app/Http/routes.php_.
>
> Como uma estrutura de web, [Laravel usa Monolog](https://laravel.com/docs/5.4/errors) como provedor de log hello. toosee como tooget Monolog toooutput mensagens toohello console, consulte [PHP: como toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Gerenciar o aplicativo da web do Azure de saudação

Vá toohello [portal do Azure](https://portal.azure.com) toomanage Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-php-mysql/access-portal.png)

A página Visão Geral do seu aplicativo Web é exibida. Aqui, você pode executar tarefas básicas de gerenciamento, como parar, iniciar, reiniciar, procurar e excluir.

menu esquerdo Olá fornece páginas de configuração do aplicativo.

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Criar um banco de dados MySQL no Azure
> * Conecte-se um tooMySQL do aplicativo PHP
> * Implantar Olá aplicativo tooAzure
> * Atualizar o modelo de dados hello e reimplantar o aplicativo hello
> * Transmitir logs de diagnóstico do Azure
> * Gerenciar o aplicativo hello em Olá portal do Azure

Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooa web app.

> [!div class="nextstepaction"]
> [Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md)
