---
title: "aaaUse rascunho com o serviço de contêiner do Azure e o registro de contêiner do Azure | Microsoft Docs"
description: "Crie um cluster ACS Kubernetes e um registro de contêiner do Azure toocreate seu primeiro aplicativo no Azure com o rascunho."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, Contêineres, microsserviços, Kubernetes, Rascunho, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Use rascunho com toobuild serviço de contêiner do Azure e o registro de contêiner do Azure e implantar um aplicativo tooKubernetes

[Rascunho](https://aka.ms/draft) é uma nova ferramenta de código-fonte aberto que torna mais fácil toodevelop com base em contêiner aplicativos e implantá-las tooKubernetes clusters sem saber muito sobre o Docker e Kubernetes – ou até mesmo instalá-los. Usando ferramentas como o rascunho permitem que você e seu foco equipes compilar o aplicativo hello com Kubernetes, não pagar tooinfrastructure tanta atenção.

Você pode usar o Rascunho com qualquer registro de imagem do Docker e qualquer cluster Kubernetes, incluindo os locais. Este tutorial mostra como toouse ACS com toocreate Kubernetes ACR e DNS do Azure ao vivo desenvolvedor CI/CD pipeline usando o rascunho.


## <a name="create-an-azure-container-registry"></a>Criar um Registro de Contêiner do Azure
Você pode facilmente [criar um novo registro de contêiner do Azure](../../container-registry/container-registry-get-started-azure-cli.md), mas Olá etapas são as seguintes:

1. Crie um toomanage do grupo de recursos do Azure ACR do registro e hello Kubernetes cluster no ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Criar um registro de imagem ACR usando [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Criar um Serviço de Contêiner do Azure com Kubernetes

Agora você está pronto toouse [az acs criar](/cli/azure/acs#create) toocreate um ACS cluster usando Kubernetes Olá `--orchestrator-type` valor.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Como Kubernetes não é um tipo de orchestrator saudação padrão, certifique-se de usar o hello `--orchestrator-type kubernetes` alternar.

saída de Hello quando tem êxito pesquisa a seguir toohello semelhante.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Agora que você tem um cluster, você pode importar as credenciais de saudação usando Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando. Agora você tem um arquivo de configuração local para seu cluster, o que é que o comando e rascunho precisam tooget seu trabalho.

## <a name="install-and-configure-draft"></a>Instalar e configurar o Rascunho
instruções de instalação Olá rascunho estão em Olá [repositório rascunho](https://github.com/Azure/draft/blob/master/docs/install.md). Eles são relativamente simples, mas exige alguma configuração, pois ele depende [comando](https://aka.ms/helm) toocreate e implantar um gráfico de comando no cluster de Kubernetes hello.

1. [Baixe e instale o Helm](https://aka.ms/helm#install).
2. Use o comando toosearch para e instale `stable/traefik`e o ingresso controlador tooenable as solicitações para as compilações de entrada.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Definir agora um observador Olá `ingress` controlador toocapture Olá IP valor externo quando ele é implantado. Esse endereço IP será Olá um [mapear domínio de implantação tooyour](#wire-up-deployment-domain) na próxima seção, Olá.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    Nesse caso, Olá IP externo para o domínio de implantação de saudação é `13.64.108.240`. Agora você pode mapear o IP de toothat do domínio.

## <a name="wire-up-deployment-domain"></a>Configurar domínio de implantação

O Rascunho cria uma versão para cada gráfico do Helm criado, ou seja, cada aplicativo em que você está trabalhando. Cada um obtém um nome gerado que é usado pelo rascunho como um _subdomínio_ sobre raiz Olá _domínio implantação_ que você controle. (Neste exemplo, usamos `squillace.io` como domínio de implantação hello.) tooenable esse comportamento de subdomínio, você deve criar um registro a para `'*'` em suas entradas DNS para o domínio de implantação, para que cada gerado subdomínio é roteado toohello Kubernetes controlador de entrada do cluster.

Seu próprio provedor de domínio tem seus próprios servidores DNS de tooassign de maneira; muito[delegar tooAzure de nameservers seu domínio DNS](../../dns/dns-delegate-domain-azure-dns.md), levar Olá etapas a seguir:

1. Crie um grupo de recursos para a zona.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Crie uma zona DNS para seu domínio.
Saudação de uso [zona de dns de rede az criar](/cli/azure/network/dns/zone#create) comando tooobtain Olá nameservers toodelegate DNS controlar tooAzure DNS para seu domínio.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Adicione servidores DNS Olá que recebem toohello provedor de domínio para seu domínio de implantação, que permite que o toorepoint DNS do Azure toouse seu domínio conforme desejado.
4. Crie uma entrada de conjunto de registros A para seu toohello de mapeamento de domínio de implantação `ingress` IP da etapa 2 da seção anterior hello.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
saída de Hello parecida com:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Configurar o registro de rascunho toouse e criar subdomínios para cada gráfico de comando, que ele cria. tooconfigure rascunho, você precisa:
  - do nome do Registro de Contêiner do Azure (neste exemplo, `draft`)
  - da chave do registro, ou senha, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.
  - domínio de implantação do Hello raiz que você tenha configurado toomap toohello Kubernetes entrada endereço IP externo (aqui, `squillace.io`)

  Chamar `draft init` e o processo de configuração de saudação solicitará Olá valores acima. processo de saudação parece algo seguinte Olá Olá primeira vez você executá-lo.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Agora você está pronto toodeploy um aplicativo.


## <a name="build-and-deploy-an-application"></a>Criar e implantar um aplicativo

No repositório de rascunho Olá são [seis aplicativos de exemplo simples](https://github.com/Azure/draft/tree/master/examples). Clone o repositório de saudação e vamos usar Olá [exemplo Python](https://github.com/Azure/draft/tree/master/examples/python). Alterar para o diretório de exemplos/Python hello e digite `draft create` toobuild aplicativo de hello. Deve se parecer com o exemplo a seguir de saudação.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

saída de Hello inclui um Dockerfile e um gráfico de comando. toobuild e implantar, basta digitar `draft up`. saída de Hello é abrangente, mas começa como Olá exemplo a seguir.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

e quando termina com êxito com algo parecido toohello exemplo a seguir.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

O nome do gráfico é, agora você pode `curl http://gangly-bronco.squillace.io` tooreceive resposta do hello, `Hello World!`.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um cluster ACS Kubernetes, você pode investigar o uso de [registro de contêiner do Azure](../../container-registry/container-registry-intro.md) toocreate implantações mais e diferentes deste cenário. Por exemplo, você pode criar um conjunto de registro DNS de domínio de rascunho _basedomain.toplevel_ que controla coisas de um subdomínio mais profundo para implantações específicas do ACS.






