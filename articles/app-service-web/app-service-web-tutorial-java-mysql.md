---
title: aaaBuild um aplicativo web Java e MySQL no Azure
description: "Saiba como tooget um aplicativo Java que se conecta serviço de banco de dados MySQL Azure toohello trabalhando no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Compilar um aplicativo Web Java e MySQL no Azure

Este tutorial mostra como toocreate um Java aplicativo no Azure da web e conectá-lo tooa banco de dados MySQL. Quando tiver terminado, você terá um aplicativo [Spring Boot](https://projects.spring.io/spring-boot/) armazenando dados no [Banco de dados do Azure para MySQL](https://docs.microsoft.com/azure/mysql/overview) em execução em [Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um banco de dados MySQL no Azure
> * Conectar a um banco de dados de toohello de aplicativo de exemplo
> * Implantar Olá aplicativo tooAzure
> * Atualize e reimplante o aplicativo hello
> * Transmitir logs de diagnóstico do Azure
> * Monitorar o aplicativo hello Olá portal do Azure


## <a name="prerequisites"></a>Pré-requisitos

1. [Baixe e instale o Git](https://git-scm.com/)
1. [Baixe e instale Olá Java JDK de 7 ou superior](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Baixe, instale e inicie o MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Preparar o MySQL local 

Nesta etapa, você criará um banco de dados em um servidor local do MySQL para uso no aplicativo de teste Olá localmente no seu computador.

### <a name="connect-toomysql-server"></a>Conecte-se o servidor tooMySQL

Em uma janela de terminal, conecte-se tooyour local MySQL server. Você pode usar essa janela do terminal toorun todos os comandos de saudação neste tutorial.

```bash
mysql -u root -p
```

Se você for solicitado a fornecer uma senha, digite a senha de saudação para Olá `root` conta. Se você não lembrar a senha da conta raiz, consulte [MySQL: como tooReset Olá senha raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Se o comando for executado com êxito, o servidor MySQL já estará sendo executado. Se não, certifique-se de que o servidor MySQL local é iniciado por seguir Olá [etapas de pós-instalação do MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Criar um banco de dados 

Em Olá `mysql` solicitar, crie um banco de dados e uma tabela para Olá itens pendentes.

```sql
CREATE DATABASE tododb;
```

Saia da conexão do servidor digitando `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Criar e executar o aplicativo de exemplo hello 

Nesta etapa, você clonar amostra de aplicativo de inicialização de Spring, configurá-lo toouse Olá MySQL banco de dados local e executá-lo em seu computador. 

### <a name="clone-hello-sample"></a>Exemplo de saudação do clone

Na janela do terminal hello, navegue tooa trabalhando repositório de exemplo hello diretório e clone. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Configurar o banco de dados do hello aplicativo toouse Olá MySQL

Saudação de atualização `spring.datasource.password` e o valor no *spring-boot-mysql-todo/src/main/resources/application.properties* com hello a mesma senha de raiz usada prompt do tooopen Olá MySQL:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Compilar e executar o exemplo hello

Compilar e executar o exemplo hello usando Olá Maven wrapper incluído no repositório de saudação:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Abra seu toosee toohttp://localhost:8080 de navegador no exemplo hello em ação. Como adicionar tarefas toohello lista, use Olá comandos do SQL a seguir no hello MySQL dados de saudação do prompt tooview armazenados no MySQL.

```SQL
use testdb;
select * from todo_item;
```

Parar o aplicativo hello atingindo `Ctrl` + `C` em Olá terminal. 

## <a name="create-an-azure-mysql-database"></a>Criar um banco de dados MySQL do Azure

Nesta etapa, você criará uma [banco de dados do Azure para MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instância usando Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli). Configure toouse de aplicativo de exemplo hello esse banco de dados posteriormente no tutorial hello.

Olá use 2.0 do CLI do Azure em um terminal toocreate Olá recursos necessários toohost seu aplicativo Java no serviço de aplicativo do Azure. Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual recursos relacionados do Azure, como aplicativos Web, bancos de dados e contas de armazenamento são implantados e gerenciados. 

Olá exemplo a seguir cria um grupo de recursos na região do Norte da Europa hello:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

valores possíveis do hello toosee você pode usar para `--location`, use Olá [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) comando.

### <a name="create-a-mysql-server"></a>Criar um servidor MySQL

Criar um servidor de banco de dados do Azure para MySQL (visualização) com hello [az mysql server criar](/cli/azure/mysql/server#create) comando.    
Substituir seu próprio nome do servidor MySQL exclusivo onde você pode ver Olá `<mysql_server_name>` espaço reservado. Esse nome faz parte do nome de host do servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, portanto, ele precisa toobe globalmente exclusivo. Substitua também `<admin_user>` e `<admin_password>` por seus próprios valores.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Quando o servidor do hello MySQL é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Configurar o firewall do servidor

Criar uma regra de firewall para o cliente do MySQL server tooallow conexões usando Olá [criar regra de firewall de servidor de mysql de az](/cli/azure/mysql/server/firewall-rule#create) comando. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Atualmente, o Banco de Dados do Azure para MySQL (Visualização) não habilita automaticamente conexões de serviços do Azure. Como os endereços IP no Azure são atribuídos dinamicamente, é melhor tooenable todos os endereços IP agora. Como o serviço de saudação continua sua visualização, melhores métodos para proteger seu banco de dados serão habilitados.

## <a name="configure-hello-azure-mysql-database"></a>Configurar o banco de dados do hello Azure MySQL

Na janela do terminal Olá em seu computador, conecte-se toohello MySQL server no Azure. Usar valor Olá especificado anteriormente para `<admin_user>` e `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Criar um banco de dados 

Em Olá `mysql` solicitar, crie um banco de dados e uma tabela para Olá itens pendentes.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Criar um usuário com permissões

Criar um usuário de banco de dados e dê a ele todos os privilégios em Olá `tododb` banco de dados. Substitua os espaços reservados de saudação `<Javaapp_user>` e `<Javaapp_password>` com seu próprio nome exclusivo do aplicativo.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Saia da conexão do servidor digitando `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Implantar Olá exemplo tooAzure do serviço de aplicativo

Criar um plano de serviço de aplicativo do Azure com hello **livre** preço usando Olá [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando CLI. plano de serviço de aplicativo Hello define Olá recursos físicos usados toohost seus aplicativos. Todos os aplicativos atribuídos plano de serviço de aplicativo tooan compartilham esses recursos, permitindo que você toosave custo ao hospedar vários aplicativos. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Quando o plano de saudação estiver pronto, Olá que CLI do Azure mostra semelhante saída toohello exemplo a seguir:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Criar um aplicativo Web do Azure

 Saudação de uso [az webapp criar](/cli/azure/appservice/web#create) toocreate de comando CLI uma definição de aplicativo da web em Olá `myAppServicePlan` plano de serviço de aplicativo. definição de aplicativo da web Hello fornece um URL tooaccess seu aplicativo com e configura toodeploy de várias opções tooAzure seu código. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Olá substituto `<app_name>` espaço reservado com seu próprio nome exclusivo do aplicativo. Esse nome exclusivo faz parte saudação padrão do nome de domínio de aplicativo da web hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no Azure. Você pode mapear um aplicativo web do domínio personalizado nome entrada toohello antes de você expor tooyour usuários.

Quando a definição de aplicativo da web hello estiver pronta, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Configurar o Java 

Definir a configuração de tempo de execução do Java Olá precisa de seu aplicativo com hello [atualização da configuração az serviço de aplicativo web](/cli/azure/appservice/web/config#update) comando.

Olá comando a seguir configura Olá web aplicativo toorun em um recente Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Configurar banco de dados do hello aplicativo toouse Olá SQL Azure

Antes de executar o aplicativo de exemplo hello, defina configurações de aplicativo no Olá web aplicativo toouse hello Azure banco de dados MySQL criado no Azure. Essas propriedades são expostos toohello aplicativo de web como variáveis de ambiente e substituem os valores hello definidos em application.properties hello dentro Olá web empacotado aplicativo. 

Definir configurações de aplicativo usando [az webapp configuração appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) em Olá CLI:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>Obter credenciais de implantação FTP 
Você pode implantar o serviço de aplicativo de tooAzure aplicativo de várias maneiras, incluindo o FTP, local Git, GitHub, Visual Studio Team Services e BitBucket. Por exemplo, Olá de toodeploy FTP. Arquivo WAR criado anteriormente na tooAzure sua máquina local do serviço de aplicativo.

toodetermine quais credenciais toopass ao longo de um toohello comando ftp aplicativo Web, Use [az serviço de aplicativo web implantação lista publicação perfis-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Carregar o aplicativo hello usando FTP

Use a saudação de toodeploy de ferramenta FTP favorita. Toohello de arquivo WAR */site/wwwroot/webapps* pasta no endereço do servidor de saudação obtido Olá `URL` campo no comando anterior hello. Remover o diretório de aplicativo padrão (raiz) existente hello e substitua Olá existente ROOT.war com hello. Arquivo WAR incorporado Olá anteriormente no tutorial de saudação.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Aplicativo de web de saudação do teste

Procurar muito`http://<app_name>.azurewebsites.net/` e adicionar a lista de toohello algumas tarefas. 

![Aplicativo Java em execução no serviço de aplicativo do Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Parabéns!** Você está executando um aplicativo Java controlado por dados no Serviço de Aplicativo do Azure.

## <a name="update-hello-app-and-redeploy"></a>Aplicativo de saudação de atualização e reimplantação

Atualize Olá aplicativo tooinclude uma coluna adicional na lista de tarefas Olá para o item de saudação dia foi criado. Inicialização de Spring trata atualizar esquema de banco de dados de saudação para você como Olá alterações do modelo de dados sem alterar os registros do banco de dados existente.

1. Em seu sistema local, abra o *src/main/java/com/example/fabrikam/TodoItem.java* e adicione a seguinte Olá importa toohello classe:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Adicionar um `String` propriedade `timeCreated` muito*src/main/java/com/example/fabrikam/TodoItem.java*, inicializá-la com um carimbo de hora na criação do objeto. Adicionar getters/setters Olá novo `timeCreated` propriedade enquanto você estiver editando o arquivo.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Atualização *src/main/java/com/example/fabrikam/TodoDemoController.java* com uma linha no hello `updateTodo` método tooset Olá timestamp:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Adicione suporte para o novo campo de saudação no modelo de Thymeleaf hello. Atualização *src/main/resources/templates/index.html* com um novo cabeçalho de tabela para Olá timestamp e um novo valor de saudação toodisplay do campo de carimbo de hora de saudação em cada linha de dados de tabela.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Recompile o aplicativo hello:

    ```bash
    mvnw clean package 
    ```

6. Saudação FTP atualizada. WAR como antes, removendo Olá existente *site/wwwroot/webapps/ROOT* diretório e *ROOT.war*, e em seguida, carregar Olá atualizado. Arquivo WAR como ROOT.war. 

Quando você atualiza o aplicativo hello, um **tempo criado** coluna agora está visível. Quando você adiciona uma nova tarefa, o aplicativo hello preencherá automaticamente Olá timestamp. As tarefas existentes permanecem inalterada e trabalhar com o aplicativo hello, mesmo que Olá subjacente do modelo de dados foi alterado. 

![Aplicativo Java atualizado com uma nova coluna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Logs de diagnóstico de fluxo 

Enquanto seu aplicativo Java é executado no serviço de aplicativo do Azure, você pode obter console Olá logs diretamente conectados tooyour terminal. Dessa forma, você pode obter Olá mensagens de diagnóstico mesmo toohelp depurar erros de aplicativo.

log toostart streaming use Olá [final de log webapp az](/cli/azure/appservice/web/log#tail) comando.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Gerenciar seu aplicativo Web do Azure

Vá toohello toosee portal do Azure Olá web aplicativo que você criou.

toodo isso, entrar muito[https://portal.azure.com](https://portal.azure.com).

No menu à esquerda do hello, clique em **do serviço de aplicativo**, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Por padrão, a folha do seu aplicativo web mostra Olá **visão geral** página. Esta página fornece uma visão de como está seu aplicativo. Aqui, você também pode executar tarefas de gerenciamento como parar, iniciar, reiniciar e excluir. guias de Olá no lado esquerdo de saudação da folha de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Essas guias na folha de saudação mostram Olá vários recursos excelentes, você pode adicionar o aplicativo da web de tooyour. Olá lista a seguir fornece apenas algumas possibilidades de saudação:
* mapear um nome DNS personalizado
* associar um certificado SSL personalizado
* configurar uma implantação contínua
* Escalar vertical e horizontalmente
* adicionar a autenticação do usuário

## <a name="clean-up-resources"></a>Limpar recursos

Se você não precisa desses recursos para outro tutorial (consulte [próximas etapas](#next)), você pode excluí-los executando Olá comando a seguir: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Próximas etapas

> [!div class="checklist"]
> * Criar um banco de dados MySQL no Azure
> * Conecte-se um toohello de aplicativo de Java de exemplo MySQL
> * Implantar Olá aplicativo tooAzure
> * Atualize e reimplante o aplicativo hello
> * Transmitir logs de diagnóstico do Azure
> * Gerenciar o aplicativo hello em Olá portal do Azure

Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome toohello aplicativo.

> [!div class="nextstepaction"] 
> [Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md)
