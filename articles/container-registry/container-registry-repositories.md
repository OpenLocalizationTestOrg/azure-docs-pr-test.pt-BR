---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repositórios de Registro de contêiner do Azure

Registro de contêiner do Azure permite que você toostore imagens de contêiner em repositórios. Armazenando imagens em repositórios, você poderá ter grupos de imagens (ou versão de imagens) em ambientes isolados. Você pode especificar esses repositórios quando você enviar por push do registro tooyour de imagens.


## <a name="prerequisites"></a>Pré-requisitos
* **Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure. Por exemplo, usar Olá [portal do Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **CLI do docker** -tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instalar [mecanismo do Docker](https://docs.docker.com/engine/installation/).
* **Baixe uma imagem** - efetuar o Pull de uma imagem de registro de Hub do Docker público Olá rotulá-lo e por push tooyour registro. Para obter orientação sobre como enviar por push e pull imagens, consulte [registro particular do Docker Push imagem tooAzure](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Exibir os repositórios em Olá Portal

Depois de ter enviado do registro de contêiner de tooyour de imagens, você pode ver uma lista de repositórios de saudação hospedagem imagens Olá Olá portal do Azure.

Se você seguiu as etapas de Olá Olá [registro particular do Docker Push imagem tooAzure](container-registry-get-started-docker-cli.md) artigo, agora você deve ter uma imagem Nginx no registro do contêiner. Como parte das instruções Olá, você deve ter especificado um namespace para a imagem de saudação. O exemplo hello abaixo, o comando de saudação envia repositório de "exemplos" hello NGinx imagens toohello:

```
docker push myregistry.azurecr.io/samples/nginx
```
 O Registro de Contêiner do Azure dá suporte a namespaces do repositório de vários níveis. Esse recurso permite que você toogroup coleções de aplicativo específico de tooa relacionados de imagens, ou uma coleção de desenvolvimento de toospecific aplicativos ou equipes operacionais. tooread mais sobre repositórios nos registros de contêiner, consulte [registros de contêiner do Docker privada no Azure](container-registry-intro.md).

repositórios de registro de contêiner de saudação tooview:

1. Faça logon no toohello portal do Azure
2. Em Olá **registro de contêiner do Azure** folha, registro de saudação selecione desejar tooinspect
3. Na folha de registro de saudação, clique em **repositórios** toosee uma lista de todos os repositórios de saudação e suas imagens
4. (Opcional) Selecione marcas toosee a imagem específica

![Repositórios no portal de saudação](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Próximas etapas
Agora que você sabe os fundamentos de saudação, você está pronto toostart usando seu registro! Por exemplo, iniciar a implantação de contêiner imagens tooan [serviço de contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.
