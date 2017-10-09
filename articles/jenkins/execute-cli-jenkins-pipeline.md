---
title: "Olá aaaExecute CLI do Azure com Jenkins | Microsoft Docs"
description: Saiba como toouse CLI do Azure toodeploy um Java web tooAzure de aplicativo no Jenkins Pipeline
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Implantar tooAzure do serviço de aplicativo com Jenkins e Olá CLI do Azure
toodeploy um tooAzure de aplicativo web Java, você pode usar a CLI do Azure em [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/). Neste tutorial, você cria um pipeline de CI/CD em uma VM do Azure, incluindo como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Configurar o Jenkins
> * Criar um aplicativo Web no Azure
> * Preparar um repositório GitHub
> * Criar pipeline do Jenkins
> * Executar o pipeline de saudação e verifique se o aplicativo da web de saudação

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. versão de hello toofind, execute `az --version`. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Criar e configurar uma instância do Jenkins
Se você ainda não tiver um mestre Jenkins, comece com hello [solução modelo](install-jenkins-solution-template.md), que inclui a saudação necessária [as credenciais do Azure](https://plugins.jenkins.io/azure-credentials) plug-in por padrão. 

plug-in de credencial do Azure Olá permite credenciais do principais de serviço do Microsoft Azure toostore na Jenkins. Na versão 1.2, adicionamos suporte Olá para que esse Jenkins Pipeline possa obter Olá as credenciais do Azure. 

Verifique se você tem a versão 1.2 ou posterior:
* No painel do Jenkins hello, clique em **Jenkins Gerenciar -> Gerenciador de plug-in ->** e procure **Azure credencial**. 
* Atualize plug-in de saudação se Olá versão é anterior 1.2.

Java JDK e Maven também são necessários no mestre de Jenkins hello. tooinstall, faça logon no mestre tooJenkins usando SSH e execute Olá comandos a seguir:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Adicionar a credencial de tooJenkins principal de serviço do Azure

Uma credencial do Azure é necessário tooexecute CLI do Azure.

* No painel do Jenkins hello, clique em **credenciais -> sistema ->**. Clique em **Credenciais globais (irrestrito)**.
* Clique em **adicionar credenciais** tooadd um [entidade de serviço do Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) preenchendo Olá ID da assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0. Forneça uma ID para uso na próxima etapa.

![Adicionar Credenciais](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Criar um serviço de aplicativo do Azure para implantar o aplicativo de web de Java Olá

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

## <a name="prepare-a-github-repository"></a>Preparar um Repositório GitHub
Olá abrir [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) repositório. toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.

* Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile**. Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 20 e 21 respectivamente.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Alterar a linha 23 tooupdate identificação da credencial na sua instância Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Criar pipeline do Jenkins
Abra o Jenkins em um navegador da Web, clique em **Novo Item**. 

* Forneça um nome para o trabalho de saudação e selecione **Pipeline**. Clique em **OK**.
* Clique em Olá **Pipeline** próxima guia. 
* Para **Definição**, selecione **Script de pipeline do SCM**.
* Para **SCM**, selecione **Git**.
* Digite hello GitHub URL para seu repositório bifurcado: https:\<seu repositório bifurcado\>.git
* Clique em **Salvar**

## <a name="test-your-pipeline"></a>Testar o pipeline
* Vá pipeline toohello que você criou, clique em **criar agora**
* Uma compilação deve ter êxito em alguns segundos e você pode ir de compilação toohello e clique em **saída do Console** detalhes de saudação toosee

## <a name="verify-your-web-app"></a>Verifique seu aplicativo Web
arquivo do tooverify Olá WAR seja implantado com êxito tooyour web app. abra um navegador da Web:

* Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping  
Você verá:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y

![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Implantar tooAzure Web App no Linux
Agora que você sabe como toouse CLI do Azure no seu Jenkins pipeline, você pode modificar Olá script toodeploy tooan aplicativo Web do Azure no Linux.

Web App no Linux oferece suporte a uma implantação de saudação de toodo de maneira diferente, que é toouse Docker. toodeploy, é necessário tooprovide um Dockerfile que os pacotes de aplicativos web com o tempo de execução do serviço em uma imagem do Docker. Olá plug-in será, em seguida, criar imagem hello, por push do registro de Docker tooa e implantar o aplicativo web do hello imagem tooyour.

* Siga as etapas de saudação [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate um aplicativo Web do Azure em execução no Linux.
* Instalar o Docker em sua instância Jenkins seguindo as instruções de saudação neste [artigo](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Criar um registro de contêiner Olá portal do Azure usando as etapas de saudação [aqui](/azure/container-registry/container-registry-get-started-azure-cli).
* Em Olá mesmo [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) repositório você bifurcado, editar Olá **Jenkinsfile2** arquivo:
    * Linha 18-21, atualize os nomes de toohello de seu grupo de recursos, o aplicativo web e o ACR respectivamente. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Linha 24, atualização \<azsrvprincipal\> tooyour identificação da credencial
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Criar um novo pipeline Jenkins como você fez ao implantar o aplicativo da web de tooAzure no Windows, somente esse tempo, use **Jenkinsfile2** em vez disso.
* Execute seu novo trabalho.
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
Neste tutorial, você configurou um pipeline de Jenkins check-out do código-fonte Olá no repositório do GitHub. Executa Maven toobuild um arquivo war e, em seguida, usa a CLI do Azure toodeploy tooAzure do serviço de aplicativo. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Configurar o Jenkins
> * Criar um aplicativo Web no Azure
> * Preparar um repositório GitHub
> * Criar pipeline do Jenkins
> * Executar o pipeline de saudação e verifique se o aplicativo da web de saudação
