---
title: "hospeda aaaCreate Docker no Azure com o Docker máquina | Microsoft Docs"
description: "Descreve o uso de hosts de docker toocreate Docker máquina no Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Criar hosts do Docker no Azure com docker-machine
Executando [Docker](https://www.docker.com/) contêineres requer um daemon do docker host VM em execução hello.
Este tópico descreve como Olá toouse [docker máquina](https://docs.docker.com/machine/) comando toocreate novas VMs do Linux, configurada com hello daemon do Docker, em execução no Azure. 

**Observação:** 

* *Este artigo depende do docker-machine 0.9.0-rc2 ou superior*
* *Contêineres do Windows terá suporte por meio de docker-máquina no hello futuro próximo*

## <a name="create-vms-with-docker-machine"></a>Criar VMs com o computador Docker
Criar docker host VMs no Azure com hello `docker-machine create` comando usando Olá `azure` driver. 

Olá driver do Azure requer sua ID de assinatura. Você pode usar o hello [CLI do Azure](cli-install-nodejs.md) ou hello [Portal do Azure](https://portal.azure.com) tooretrieve sua assinatura do Azure. 

**Usando Olá Portal do Azure**

* Selecione **assinaturas** Olá navegação esquerdo página e cópia Olá da id de assinatura.

**Usando Olá CLI do Azure**

* Tipo ```azure account list``` e id de assinatura de saudação de cópia.

Tipo `docker-machine create --driver azure` toosee Olá opções e seus valores padrão.
Você também pode ver Olá [documentação do Driver do Docker do Azure](https://docs.docker.com/machine/drivers/azure/) para obter mais informações. 

Olá exemplo a seguir se baseia Olá [valores padrão](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mas ele se desejar definir esses valores: 

* dns do Azure para nome hello associado com o IP público hello e certificados gerados. Esse é o nome DNS de saudação de sua máquina virtual. Olá VM pode, em seguida, com segurança parar, versão IP dinâmico Olá e fornecer Olá capacidade tooreconnect após Olá vm começa novamente com um novo IP. prefixo do nome Hello deve ser exclusivo para essa região UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Abra a porta 80 no hello VM para acesso de saída à internet
* tamanho da saudação um armazenamento VM tooutilize mais rápido premium
* armazenamento Premium usado para o disco de vm Olá

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Escolha um host docker com docker-machine
Depois que você tem uma entrada na máquina de docker para o host, você pode definir o host de padrão de saudação ao executar os comandos.

## <a name="using-powershell"></a>Usando o PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Como usar o Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Agora você pode executar os comandos no host especificado Olá

```
docker ps
docker info
```

## <a name="run-a-container"></a>Executar um contêiner
Com um host configurado, agora você pode executar um tootest de servidor da web simples se o host foi configurado corretamente.
Aqui é usar uma imagem padrão nginx, especificar que ele deve escutar na porta 80 e que se reinicia a VM do host hello, contêiner Olá reiniciem também (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

saída de Hello deve ser semelhante a saudação a seguir:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Contêiner de saudação do teste
Examine os contêineres em execução usando `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

E, Olá toosee executando o contêiner, tipo `docker-machine ip <VM name>` toofind Olá IP endereço tooenter no navegador de saudação:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Contêiner ngnix em execução](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Resumo
Com o docker-machine você pode provisionar hosts do docker facilmente no Azure para suas validações individuais de host do docker.
Para a produção de hospedagem de contêineres, consulte Olá [serviço de contêiner do Azure](http://aka.ms/AzureContainerService)

toodevelop .NET Core aplicativos com o Visual Studio, consulte [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)

