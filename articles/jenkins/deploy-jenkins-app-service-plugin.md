---
title: "aaaDeploy tooAzure do serviço de aplicativo com Jenkins Plugin | Microsoft Docs"
description: "Saiba como toouse Jenkins de serviço de aplicativo do Azure plug-in toodeploy um Java web tooAzure de aplicativo em Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Implantar tooAzure do serviço de aplicativo com Jenkins plug-in 
toodeploy um tooAzure de aplicativo web Java, você pode usar a CLI do Azure em [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) ou você pode fazer uso de saudação [Jenkins de serviço de aplicativo do Azure plug-in](https://plugins.jenkins.io/azure-app-service). Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Configurar Jenkins toodeploy tooAzure do serviço de aplicativo por meio de FTP 
> * Configurar Jenkins toodeploy tooAzure do serviço de aplicativo no Linux por meio do Docker 

## <a name="create-and-configure-jenkins-instance"></a>Criar e configurar uma instância do Jenkins
Se você ainda não tiver um mestre Jenkins, comece com hello [solução modelo](install-jenkins-solution-template.md), que inclui JDK8 e hello plug-ins necessários a seguir:

* [Plug-in de cliente Git do Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Credenciais do Azure](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Serviço de Aplicativo do Azure](https://plugins.jenkins.io/azure-app-server) v.0.1

Você pode usar o hello toodeploy aplicativo Web do plug-in do serviço de aplicativo em todos os idiomas (por exemplo, c#, PHP, Java e node.js, etc.) tem suportada pelo serviço de aplicativo do Azure. Neste tutorial, estamos usando Olá amostra de aplicativo Java, [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample). toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.  

JDK de Java e Maven são necessários para compilar o projeto de Java hello. Verifique se que você instalar componentes de saudação em mestre do hello Jenkins ou agente de VM Olá se você usar uma para a integração contínua. 

tooinstall, faça logon em toohello Jenkins instância usando o SSH e execute Olá comandos a seguir:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Para implantar tooApp serviço no Linux, você também precisa tooinstall Docker no mestre de Jenkins de saudação ou agente de VM Olá usado para compilação. Consulte o artigo de toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Adicionar a credencial de tooJenkins principal de serviço do Azure

Uma entidade de serviço do Azure é necessário toodeploy tooAzure. 

<ol>
<li>Use [CLI do Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou [portal do Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate uma entidade de serviço do Azure</li>
<li>No painel do Jenkins hello, clique em **credenciais -> sistema ->**. Clique em **Credenciais globais (irrestrito)**.</li>
<li>Clique em **adicionar credenciais** tooadd uma entidade de serviço do Microsoft Azure preenchendo Olá ID da assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0. Forneça uma ID, **mySp**, para uso na próxima etapa.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Plug-in do Serviço de Aplicativo do Azure

V 1.0 plug-in de serviço de aplicativo do Azure oferece suporte à implantação contínua tooAzure aplicativo Web por meio de:

* Git e FTP
* Docker para Aplicativo Web no Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Configurar toodeploy Jenkins aplicativo Web por meio de FTP usando Olá Jenkins painel

toodeploy tooAzure seu project Web App, você pode carregar seus artefatos de compilação (por exemplo, o arquivo. war em Java) usando o Git ou FTP.

Antes de configurar o trabalho de saudação em Jenkins, é necessário um plano de serviço de aplicativo do Azure e um aplicativo Web para aplicativo de Java Olá em execução.


1. Criar um plano de serviço de aplicativo do Azure com hello **livre** preço usando Olá [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando CLI. plano de serviço de aplicativo Hello define Olá recursos físicos usados toohost seus aplicativos. Todos os aplicativos atribuídos plano de serviço de aplicativo tooan compartilham esses recursos, permitindo que você toosave custo ao hospedar vários aplicativos.
2. Crie um aplicativo Web. Pode hello ou use [portal do Azure](/azure/app-service-web/web-sites-configure) ou use Olá comando CLI Az a seguir:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Certifique-se de que definir a configuração de tempo de execução do Java Olá seu aplicativo precisa. Olá após o comando CLI do Azure configura Olá web aplicativo toorun em um recente Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Configurar Olá Jenkins trabalho


1. Criar um novo projeto de **estilo livre** no painel do Jenkins
2. Configurar **código-fonte gerenciamento** toouse seu local bifurcação de [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) fornecendo Olá **URL do repositório**. Por exemplo: http://github.com/&lt;yourID>/aplicativowebjavadeexemplo.
3. Adicione um projeto de saudação do Build etapa toobuild usando Maven. Faça isso adicionando um **Executar shell**. Neste exemplo, podemos precisará de um arquivo de *.war do etapa adicional toorename Olá no tooROOT.war da pasta de destino.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.
5. Fonte, "mySp", entidade de serviço do Azure Olá armazenados na etapa anterior.
6. Em **configuração do aplicativo** , escolha Olá recurso grupo e o aplicativo web em sua assinatura. plug-in de saudação detecta automaticamente se Olá Web App for Windows ou Linux. Para um aplicativo Web baseado em Windows, é apresentada a opção hello "Publicar os arquivos".
7. Preenchimento nos arquivos de saudação desejado toodeploy (por exemplo, um pacote war se você estiver usando o Java.) O Diretório de Origem e o Diretório de Destino são opcionais. Olá parâmetros permitem toospecify pastas de origem e de destino quando o carregamento de arquivos. O aplicativo Web Java no Azure é executado em um servidor Tomcat. Desse modo, você carrega o pacote war para a pasta webapps. Neste exemplo, defina **diretório de origem** muito "destino" e fornecer "webapps" de **diretório de destino**.
8. Se você quiser toodeploy tooa slot que não seja de produção, você também pode definir **Slot** nome.
9. Salve o projeto hello e compilá-lo. Seu aplicativo web é implantado tooAzure quando a compilação for concluída.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Implantar o aplicativo Web via FTP usando o pipeline do Jenkins

Olá plug-in está preparado para o pipeline. Você pode consultar o exemplo tooa no repositório do GitHub hello.

1. Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_ftp_plugin**. Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 11 e 12 respectivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Alterar a identificação da credencial tooupdate 14 linha em sua instância Jenkins.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Crie um pipeline do Jenkins

1. Abra o Jenkins em um navegador da Web, clique em **Novo Item**.
2. Forneça um nome para o trabalho de saudação e selecione **Pipeline**. Clique em **OK**.
3. Clique em Olá **Pipeline** próxima guia.
4. Para **Definição**, selecione **Script de pipeline do SCM**.
5. Para **SCM**, selecione **Git**. Digite hello GitHub URL para seu repositório bifurcado: https:&lt;seu repositório bifurcado > .git
6. Atualização **caminho de Script** muito "Jenkinsfile_ftp_plugin"
7. Clique em **salvar** e trabalho de execução hello.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Configurar toodeploy Jenkins aplicativo Web no Linux por meio do Docker

Além de Git/FTP, o aplicativo Web no Linux dá suporte à implantação usando o Docker. toodeploy usando o Docker, você precisa tooprovide um Dockerfile que os pacotes de aplicativos web com o tempo de execução do serviço em uma imagem do docker. Em seguida, Olá plug-in compila imagem hello, envia-registro de docker tooa e implanta o aplicativo web do hello imagem tooyour.

O aplicativo Web no Linux também dá suporte a modos tradicionais, como Git e FTP, mas somente para linguagens internas (.NET Core, Node.js, PHP e Ruby). Para outros idiomas, você precisa de toopackage o tempo de execução de código e o serviço de aplicativo juntos em uma imagem do docker e usar toodeploy docker.

Antes de configurar o trabalho de saudação em Jenkins, você precisa de um serviço de aplicativo do Azure em Linux. Um registro de contêiner também é necessário toostore e gerenciar suas imagens de contêiner do Docker particulares. Você pode usar o DockerHub; estamos usando o Registro de Contêiner do Azure para este exemplo.

* Você pode seguir as etapas de saudação [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate um aplicativo Web no Linux 
* Registro de contêiner do Azure é um gerenciados [Docker registro] serviço (https://docs.docker.com/registry/) com base no hello 2.0 do código-fonte aberto Docker do registro. Execute as etapas de saudação [aqui] (/ azure/container-registry/container-registry-get-started-azure-cli) para obter instruções sobre como toodo para. Você também pode usar o DockerHub.

### <a name="toodeploy-using-docker"></a>toodeploy usando o docker:

1. Crie um novo projeto de estilo livre no painel do Jenkins.
2. Configurar **código-fonte gerenciamento** toouse seu local bifurcação de [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) fornecendo Olá **URL do repositório**. Por exemplo: http://github.com/&lt;yourid>/aplicativowebjavadeexemplo.
Adicione um projeto de saudação do Build etapa toobuild usando Maven. Faça isso adicionando um **executar shell** e adicione Olá a seguinte linha no **comando**:    
```bash
mvn clean package
```

3. Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.
4. Fornecer, **mySp**, entidade de serviço do Azure Olá armazenada na etapa anterior como credenciais do Azure.
5. Em **configuração do aplicativo** , escolha o grupo de recursos de saudação e um aplicativo web do Linux em sua assinatura.
6. Escolha Publicar por meio do Docker.
7. Preencha o caminho de **Dockerfile**. Você pode manter saudação padrão "/ Dockerfile" para **URL de registro de Docker**, forneça no formato de saudação do https://&lt;myRegistry >. azurecr.io se você usar o registro de contêiner do Azure. Deixe-a em branco se você usar o DockerHub.
8. Para **credenciais de registro**, adicione a credencial Olá de saudação do registro de contêiner do Azure. Você pode obter Olá ID de usuário e senha executando Olá seguintes comandos em CLI do Azure. comando primeiro Olá permite que a conta de administrador de saudação.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Olá, nome de imagem do docker e a marca no **avançado** guia são opcionais. Por padrão, o nome da imagem é obtido da imagem Olá nome configurado na marca de saudação portal (no contêiner do Docker configuração.) do Azure é gerado a partir de $ número do_build. Verifique se você especifica o nome da imagem Olá no portal do Azure ou fornece um valor para **Docker imagem** na **avançado** guia. Neste exemplo, forneça "&lt;yourRegistry>.azurecr.io/calculator" para a **Imagem do Docker** e deixe a **Marca da Imagem do Docker** em branco.
10. Observe que a implantação falhará se você usar uma configuração de imagem do Docker interna. Verifique se que você alterar a imagem personalizada do docker config toouse na configuração do contêiner do Docker no portal do Azure. Para a imagem interna, use toodeploy de abordagem de carregamento de arquivo.
11. Método de carregamento toofile semelhante, você pode escolher um slot diferente que não seja de produção.
12. Salve e compile o projeto de saudação. Você verá sua imagem de contêiner é enviada por push do registro de tooyour e aplicativo web é implantado.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Implantar tooWeb aplicativo no Linux por meio do Docker usando o pipeline Jenkins

1. Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_container_plugin**. Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 11 e 12 respectivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Alterar o servidor de registro de contêiner de tooyour 13 de linha    
```java
def registryServer = '<registryURL>'
```    

3. Alterar a identificação da credencial tooupdate 16 linha em sua instância Jenkins    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Criar pipeline do Jenkins    

1. Abra o Jenkins em um navegador da Web, clique em **Novo Item**.
2. Forneça um nome para o trabalho de saudação e selecione **Pipeline**. Clique em **OK**.
3. Clique em Olá **Pipeline** próxima guia.
4. Para **Definição**, selecione **Script de pipeline do SCM**.
5. Para **SCM**, selecione **Git**.
6. Digite hello GitHub URL para seu repositório bifurcado: https:&lt;seu repositório bifurcado > .git</li>
Atualização 7, **caminho de Script** muito "Jenkinsfile_container_plugin"
8. Clique em **salvar** e trabalho de execução hello.

## <a name="verify-your-web-app"></a>Verifique seu aplicativo Web

1. arquivo do tooverify Olá WAR seja implantado com êxito tooyour web app. Abra um navegador da Web.
2. Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping você verá:    
     Bem-vindo tooJava aplicativo Web!!! Ele está atualizado!
   Domingo, 17 de junho de 2017, 16:39:10 UTC
3. Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y        
    ![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Para o Serviço de Aplicativo no Linux

* tooverify, na CLI do Azure, execute:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Você obtém Olá resultados a seguir:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping. Você verá a mensagem de saudação: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y
    
## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você deve usar Olá tooAzure de toodeploy de plug-in de serviço de aplicativo do Azure.

Você aprendeu como:

> [!div class="checklist"]
> * Configurar Jenkins toodeploy do serviço de aplicativo do Azure por meio de FTP 
> * Configurar Jenkins toodeploy tooAzure do serviço de aplicativo no Linux por meio do Docker 
