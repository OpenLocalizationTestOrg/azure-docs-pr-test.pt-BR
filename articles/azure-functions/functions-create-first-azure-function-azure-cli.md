---
title: "aaaCreate sua primeira função da saudação CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate do Azure a primeira função para a execução sem servidor usando Olá CLI do Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Criar sua primeira função usando Olá CLI do Azure

Este tutorial de início rápido orienta como toouse toocreate de funções do Azure a primeira função. Usar o hello CLI do Azure toocreate um aplicativo de função, que é Olá infraestrutura sem servidor que hospeda a função. código de função Hello em si é implantado de um repositório de exemplo do GitHub.    

Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux. 

## <a name="prerequisites"></a>Pré-requisitos 

Antes de executar este exemplo, você deve ter o seguinte hello:

+ Uma conta do [GitHub](https://github.com) ativa. 
+ Uma assinatura ativa do Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure, como os aplicativos de funções, bancos de dados e contas de armazenamento, são implantados e gerenciados.

Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup`.  
Se você não estiver usando o Cloud Shell, primeiro você deve entrar usando `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Criar uma conta de Armazenamento do Azure

Funções usa um estado de toomaintain de conta de armazenamento do Azure e outras informações sobre suas funções. Criar uma conta de armazenamento no grupo de recursos de saudação criado usando Olá [criar conta de armazenamento az](/cli/azure/storage/account#create) comando.

Olá a seguir de comando, substitua seu próprio nome de conta de armazenamento exclusivo onde você pode ver Olá `<storage_name>` espaço reservado. Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Depois que tiver sido criada a conta de armazenamento hello, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Criar um aplicativo de funções

Você deve ter uma função aplicativo toohost Olá a execução das funções. Olá função aplicativo fornece um ambiente de execução sem servidor do seu código de função. Ele permite que você agrupe funções como uma unidade lógica para facilitar o gerenciamento, a implantação e o compartilhamento de recursos. Criar um aplicativo de função usando Olá [functionapp az criar](/cli/azure/functionapp#create) comando. 

Olá a seguir de comando, substitua seu próprio nome de aplicativo de função exclusiva onde você pode ver Olá `<app_name>` espaço reservado e hello nome de conta de armazenamento para `<storage_name>`. Olá `<app_name>` é usado como o domínio DNS à saudação padrão de saudação função aplicativo e o nome de saudação caso precisa toobe exclusivo entre todos os aplicativos no Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Por padrão, um função de aplicativo é criado com hello consumo plano de hospedagem, que significa que os recursos são adicionados dinamicamente conforme exigido por funções, e você paga apenas quando funções estão em execução. Para obter mais informações, consulte [plano de hospedagem correto escolha Olá](functions-scale.md). 

Após Olá função aplicativo foi criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Agora que você tem um aplicativo de função, você pode implantar o código de função real de saudação do repositório de exemplo hello GitHub.

## <a name="deploy-your-function-code"></a>Implantar o código de função  

Há várias toocreate de maneiras seu código de função em seu novo aplicativo de função. Este tópico se conecta tooa repositório de exemplo no GitHub. Como antes, Olá código a seguir substitua Olá `<app_name>` espaço reservado com o nome de saudação do aplicativo de função hello criado por você. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Após a implantação de saudação origem foi definido, Olá CLI do Azure mostra informações toohello semelhantes (valores nulos removidos para facilitar a leitura) de exemplo a seguir:

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Função de saudação do teste

Use ondulação tootest Olá implantado função em um computador Mac ou Linux ou usando o Bash no Windows. Executar Olá após a rotação de comando, substituindo Olá `<app_name>` espaço reservado com o nome de saudação do seu aplicativo de função. Acrescente a cadeia de caracteres de consulta Olá `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Se você não tiver ondulação disponível na linha de comando, digite Olá a mesma URL no endereço de saudação do navegador da web. Novamente, substitua Olá `<app_name>` espaço reservado com o nome de saudação do seu aplicativo de função e acrescenta a cadeia de caracteres de consulta Olá `&name=<yourname>` toohello URL e executar a solicitação de saudação. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Resposta de função mostrada em um navegador.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Limpar recursos

Outros inícios rápidos nessa coleção aproveitam esse início rápido. Se você planeja toocontinue toowork com tutoriais subsequentes ou com os tutoriais hello, faça não limpar os recursos de saudação criados neste guia de início rápido. Se você não planeja toocontinue, use Olá toodelete de comando a seguir todos os recursos criados por este guia de início rápido:

```azurecli-interactive
az group delete --name myResourceGroup
```
Quando solicitado, digite `y`.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
