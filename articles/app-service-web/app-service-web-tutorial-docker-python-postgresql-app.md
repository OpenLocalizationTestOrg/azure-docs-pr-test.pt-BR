---
title: aaaBuild um aplicativo web Python Docker e PostgreSQL no Azure | Microsoft Docs
description: "Saiba como tooget um aplicativo de Docker Python trabalhando no Azure, com conexão tooa PostgreSQL de banco de dados."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Compilar um aplicativo Web Docker Python e PostgreSQL no Azure

Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches. Este tutorial mostra como toocreate um Python Docker básica web aplicativo no Azure. Você vai se conectar a esse banco de dados do aplicativo tooa PostgreSQL. Quando terminar, você terá um aplicativo Python Flask em execução dentro de um contêiner do Docker nos [Aplicativos Web do Serviço de Aplicativo do Azure](app-service-web-overview.md).

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

Você pode seguir as etapas de saudação abaixo em macOS. Instruções do Linux e Windows são Olá mesmo na maioria dos casos, mas as diferenças de saudação não são detalhadas neste tutorial.
 
## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

1. [Instalar o Git](https://git-scm.com/)
1. [Instalar o Python](https://www.python.org/downloads/)
1. [Instale e execute o PostgreSQL](https://www.postgresql.org/download/)
1. [Instale o Docker Community Edition](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Testar a instalação do PostgreSQL local e criar um banco de dados

Abra a janela do terminal hello e execute `psql postgres` tooconnect tooyour local PostgreSQL server.

```bash
psql postgres
```

Se sua conexão tiver êxito, o banco de dados PostgreSQL já estará em execução. Se não, certifique-se de que o banco de dados PostgresQL local é iniciado, seguindo as etapas de saudação em [Downloads - PostgreSQL Core distribuição](https://www.postgresql.org/download/).

Crie um banco de dados chamado *eventregistration* e configure um usuário de banco de dados separado chamado *manager* com a senha *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Tipo *\q* cliente do tooexit Olá PostgreSQL. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Criar um aplicativo Python Flask local

Nesta etapa, você configura Olá local Python bulbo projeto.

### <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Janela do terminal Olá aberta, e `CD` tooa diretório de trabalho.  

Seguinte Olá executar comandos tooclone Olá exemplo repositório e ir toohello *initialapp 0.1* de versão.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Esse repositório de exemplo contém um aplicativo [Flask](http://flask.pocoo.org/). 

### <a name="run-hello-application"></a>Executar o aplicativo hello

> [!NOTE] 
> Em uma etapa posterior, você simplificar esse processo criando um toouse de contêiner do Docker com o banco de dados de produção de hello.

Instalar pacotes de saudação necessários e iniciar o aplicativo hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Navegue toohttp://127.0.0.1:5000 em um navegador. Clique em **Registrar!** e crie um usuário de teste.

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

Olá aplicativo de exemplo do bulbo armazena dados de usuário no banco de dados de saudação. Se você estiver com êxito no registro de um usuário, seu aplicativo está gravando dados toohello PostgreSQL banco de dados local.

toostop Olá bulbo servidor a qualquer momento, digite Ctrl + C Olá terminal. 

## <a name="create-a-production-postgresql-database"></a>Criar um banco de dados PostgreSQL de produção

Nesta etapa, você cria um banco de dados PostgreSQL no Azure. Quando seu aplicativo é implantado tooAzure, ele usará esse banco de dados de nuvem.

### <a name="log-in-tooazure"></a>Faça logon no tooAzure

Você está agora necessários de recursos de saudação do contínuo toouse hello Azure CLI 2.0 toocreate toohost seu aplicativo Python no serviço de aplicativo do Azure.  Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um [grupo de recursos](../azure-resource-manager/resource-group-overview.md) com hello [criar grupo az](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Olá exemplo a seguir cria um grupo de recursos na região Oeste dos EUA de saudação:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Saudação de uso [locais de lista do serviço de aplicativo az](/cli/azure/appservice#list-locations) locais disponíveis toolist de comando CLI do Azure.

### <a name="create-an-azure-database-for-postgresql-server"></a>Criar um Banco de Dados do Azure para o servidor PostgreSQL

Criar um servidor PostgreSQL com hello [az postgres server criar](/cli/azure/documentdb#create) comando.

Olá a seguir de comando, substitua um nome de servidor exclusivo para Olá  *\<postgresql_name >* espaço reservado e um nome de usuário para Olá  *\<admin_username >* espaço reservado . nome do servidor de saudação for usado como parte de seu ponto de extremidade PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), portanto, o nome do hello deve toobe exclusivo em todos os servidores no Azure. nome de usuário Olá destina-se a conta de usuário do administrador de banco de dados inicial de saudação. Você está toopick solicitada uma senha para este usuário.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Quando Olá banco de dados PostgreSQL servidor é criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Criar uma regra de firewall para hello banco de dados do Azure para servidor PostgreSQL

Execute Olá seguir CLI do Azure comando tooallow toohello banco de dados de todos os endereços IP.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Olá CLI do Azure confirma a criação de regra de firewall de saudação com saída toohello semelhante exemplo a seguir:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Conecte-se o seu banco de dados do Python bulbo aplicativo toohello

Nesta etapa, você se conectar a servidor PostgreSQL que você criou seu bulbo Python exemplo aplicativo toohello banco de dados do Azure.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Criando um banco de dados vazio e configurando um novo usuário do aplicativo de banco de dados

Crie um usuário de banco de dados com tooa único banco de dados somente. Você usará esses tooavoid credenciais entregar Olá aplicativo acesso completo toohello servidor.

Conecte o banco de dados de toohello (você for solicitado a fornecer sua senha de administrador).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Crie banco de dados de saudação e usuário de saudação PostgreSQL CLI.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Tipo *\q* cliente do tooexit Olá PostgreSQL.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Testar o aplicativo hello localmente no banco de dados PostgreSQL do Azure Olá 

Voltando agora toohello *aplicativo* pasta da saudação clonado repositório Github, você pode executar o aplicativo de Python bulbo hello atualizando variáveis de ambiente de banco de dados de saudação.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Quando o aplicativo hello está totalmente carregado, você verá algo semelhante toohello seguinte mensagem:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Navegue toohttp://127.0.0.1:5000 em um navegador. Clique em **Registrar!** e crie um registro de teste. Agora você está criando o banco de dados de toohello de dados no Azure.

![Aplicativo Python Flask em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Executando o aplicativo hello de um contêiner de Docker

Crie imagem de contêiner do Docker hello.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker exibirá uma confirmação contêiner Olá criou com êxito.

```bash
Successfully built 7548f983a36b
```

Adicionar arquivo da variável de ambiente banco de dados ambiente variáveis tooan *db.env*. aplicativo Hello conectará o banco de dados de produção PostgreSQL de toohello no Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Execute o aplicativo de saudação de dentro do contêiner do Docker hello. Olá comando a seguir especifica o arquivo de variável de ambiente hello e mapeia saudação padrão bulbo 5000 toolocal porta 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

saída de Hello é toowhat semelhante que vimos anteriormente. No entanto, a migração do banco de dados inicial de saudação não precisa mais toobe executada e, portanto, é ignorada.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

banco de dados de saudação já contém o registro Olá criado anteriormente.

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Carregar o registro de contêiner tooa do contêiner de Docker Olá

Nesta etapa, você deve carregar o registro de contêiner do hello Docker contêiner tooa. Você utilizará o Registro de Contêiner do Azure, mas também pode usar outros registros populares, como o Hub do Docker.

### <a name="create-an-azure-container-registry"></a>Criar um Registro de Contêiner do Azure

Olá após o comando toocreate um registro de contêiner substitua  *\<registry_name >* com um nome de registro do contêiner do Azure exclusivo de sua escolha.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Saída
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Recuperar as credenciais de registro hello para enviar por push e pull imagens do Docker

credenciais de registro tooshow, habilite o modo de administração pela primeira vez.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Você verá duas senhas. Anote o nome de usuário hello e senha primeiro hello.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Carregue seu contêiner de Docker tooAzure registro de contêiner

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Implantar Olá Docker Python bulbo aplicativo tooAzure

Nesta etapa, você deve implantar o tooAzure de aplicativo de Python bulbo de baseado no contêiner de Docker do serviço de aplicativo.

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

Criar um plano de serviço de aplicativo com hello [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Olá, exemplo a seguir cria um plano de serviço de aplicativo baseado em Linux chamado *myAppServicePlan* usando Olá S1 preço:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Quando Olá plano de serviço de aplicativo é criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Criar um aplicativo Web

Criar um aplicativo web no hello *myAppServicePlan* plano de serviço de aplicativo com hello [az webapp criar](/cli/azure/webapp#create) comando. 

Fornece de aplicativo de web Hello você hospedagem espaço toodeploy seu código e fornece uma URL para você Olá tooview aplicativo implantado. Use toocreate Olá web app. 

Olá a seguir de comando, substitua Olá  *\<app_name >* espaço reservado com um nome exclusivo do aplicativo. Esse nome faz parte da URL de padrão de saudação do aplicativo da web de Olá, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no serviço de aplicativo do Azure. 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando o aplicativo da web de saudação tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir: 

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

### <a name="configure-hello-database-environment-variables"></a>Configurar variáveis de ambiente de banco de dados de saudação

Anteriormente no tutorial hello, definido pelo banco de dados do ambiente variáveis tooconnect tooyour PostgreSQL.

No serviço de aplicativo, você definir variáveis de ambiente como _configurações do aplicativo_ usando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config#set) comando. 

Olá exemplo a seguir especifica detalhes de conexão de banco de dados de saudação como configurações de aplicativo. Ele também usa Olá *porta* variável toomap PORT 5000 seu tráfego de tooreceive HTTP do contêiner do Docker na porta 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Configurar a implantação do contêiner do Docker 

O Serviço de Aplicativo pode baixar e executar automaticamente um contêiner do Docker.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Sempre que você atualiza o contêiner de Docker hello, ou alterar configurações de hello, reinicie o aplicativo hello. Reiniciar garante que todas as configurações são aplicadas e contêiner mais recente Olá retirado do registro hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Procurar o aplicativo web do Azure de toohello 

Procurar toohello implantado um aplicativo da web usando um navegador da web. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Olá web app leva mais tooload como contêiner de saudação tem toobe baixados e iniciados após a alteração de configuração do contêiner hello.

Você verá convidados registrados anteriormente que foram salvos o banco de dados de produção do Azure toohello na etapa anterior hello.

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Parabéns!** Você está executando um aplicativo Python Flask baseado em um contêiner do Docker no Serviço de Aplicativo do Azure.

## <a name="update-data-model-and-redeploy"></a>Atualizar o modelo de dados e reimplantar

Nesta etapa, você pode adicionar número Olá participantes tooeach de registro de eventos atualizando o modelo de convidado hello.

Check-out Olá *0,2 migração* versão com hello git comando a seguir:

```bash
git checkout tags/0.2-migration
```

Esta versão já feitas Olá modelo, controladores e tooviews as alterações necessárias. Ela também inclui uma migração de banco de dados gerada por meio de *alembic* (`flask db migrate`). Você pode ver todas as alterações feitas por meio da saudação git comando a seguir:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Testar suas alterações localmente

Execute Olá tootest comandos a seguir as alterações localmente pelo servidor de bulbo Olá em execução.

Mac / Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Navegue toohttp://127.0.0.1:5000 suas alterações de saudação do navegador tooview. Crie um registro de teste.

![Aplicativo Python Flask baseado em contêiner do Docker em execução localmente](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Publicar alterações tooAzure

Criar nova imagem do docker hello, por push do registro de contêiner toohello e reiniciar o aplicativo hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Navegue tooyour aplicativo de web do Azure e experimente a nova funcionalidade de saudação novamente. Crie outro registro de evento.

```bash 
http://<app_name>.azurewebsites.net 
```

![Aplicativo Docker Python Flask no Serviço de Aplicativo do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Gerenciar seu aplicativo Web do Azure

Vá toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicativo que você criou.

No menu à esquerda do hello, clique em **serviços de aplicativos**, clique em nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Por padrão, o portal de saudação mostra seu aplicativo de web **visão geral** página. Esta página fornece uma visão de como está seu aplicativo. Aqui, você também pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. guias de Olá no lado esquerdo de saudação da página de saudação mostram páginas de configuração diferentes de hello, que você pode abrir.

![Página Serviço de Aplicativo no portal do Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Próximas etapas

Avançar toolearn tutorial do próximo toohello como toomap um DNS personalizado nome tooyour web app.

> [!div class="nextstepaction"] 
> [Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md)
