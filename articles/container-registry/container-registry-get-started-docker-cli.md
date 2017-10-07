---
title: aaaPush Docker imagem tooprivate do registro do Azure | Microsoft Docs
description: "Enviar por push e pull Docker registro de contêiner privado tooa imagens no Azure usando Olá CLI do Docker"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Enviar por push o seu primeiro imagem tooa privada Docker registro de contêiner usando Olá CLI do Docker
Um registro de contêiner do Azure armazena e gerencia privado [Docker](http://hub.docker.com) imagens de contêiner, semelhante toohello maneira [Docker Hub](https://hub.docker.com/) armazena imagens públicas do Docker. Use Olá [Interface de linha de comando do Docker](https://docs.docker.com/engine/reference/commandline/cli/) (CLI do Docker) para [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/)e outras operações em seu contêiner Registro.

Para obter mais informações e conceitos, consulte [Olá visão geral](container-registry-intro.md)



## <a name="prerequisites"></a>Pré-requisitos
* **Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure. Por exemplo, usar Olá [portal do Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **CLI do docker** -tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instalar [mecanismo do Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Faça logon no registro tooa
Executar `docker login` toolog tooyour registro de contêiner com o [credenciais de registro](container-registry-authentication.md).

Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md). Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Verifique o nome de registro totalmente qualificado de Olá de toospecify se (todas as minúsculas). Neste exemplo, é `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Etapas toopull e enviar por push uma imagem
Olá seguir exemplo downloads Olá imagem Nginx de registro de Hub do Docker público hello, marcas de registro do contêiner do Azure privado, push tooyour registro, em seguida, extrair novamente.

**1. Pull imagem oficial do Docker Olá para Nginx**

Primeiro pull Olá pública Nginx imagem tooyour computador local.

```
docker pull nginx
```
**2. Inicie o contêiner de Nginx Olá**

Olá comando a seguir inicia Olá local Nginx contêiner interativamente na porta 8080, permitindo que você saída toosee Nginx. Ele remove Olá executando contêiner uma vez interrompida.

```
docker run -it --rm -p 8080:80 nginx
```

Procurar muito[http://localhost:8080](http://localhost:8080) tooview Olá executando o contêiner. Você verá um toohello semelhante de tela a seguir um.

![Nginx no computador local](./media/container-registry-get-started-docker-cli/nginx.png)

toostop Olá contêiner em execução, pressione [CTRL] + [C].

**3. Criar um alias de imagem Olá no registro**

Olá comando a seguir cria um alias de imagem hello, com um registro de tooyour caminho totalmente qualificado. Este exemplo especifica Olá `samples` namespace tooavoid desordem na raiz de saudação do registro hello.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Push Olá imagem tooyour registro**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Baixe a imagem de saudação do registro**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Inicie o contêiner de Nginx de saudação do registro**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Procurar muito[http://localhost:8080](http://localhost:8080) tooview Olá executando o contêiner.

toostop Olá contêiner em execução, pressione [CTRL] + [C].

**7. (Opcional) Remover imagem Olá**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Limites simultâneos
Em alguns cenários, a execução simultânea de chamadas pode resultar em erros. Olá, a tabela a seguir contém os limites de saudação de chamadas simultâneas com operações de "Push" e "Pull" no registro de contêiner do Azure:

| Operação  | Limite                                  |
| ---------- | -------------------------------------- |
| PULL       | Backup too10 simultâneos recebe por registro |
| PUSH       | Backup too5 simultâneos envia por registro |

## <a name="next-steps"></a>Próximas etapas
Agora que você sabe os fundamentos de saudação, você está pronto toostart usando seu registro! Por exemplo, iniciar a implantação de contêiner imagens tooan [serviço de contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
