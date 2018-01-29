---
title: "Os repositórios do Registro de Contêiner do Azure no Portal do Azure"
description: "Como exibir os repositórios do Registro de Contêiner do Azure no Portal do Azure."
services: container-registry
author: cristy
manager: timlt
ms.service: container-registry
ms.topic: article
ms.date: 01/05/2018
ms.author: cristyg
ms.openlocfilehash: 593972e972207a27d1232fcb0c1bf220ac3a8def
ms.sourcegitcommit: 1d423a8954731b0f318240f2fa0262934ff04bd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="view-container-registry-repositories-in-the-azure-portal"></a>Exibir os repositórios do registro de contêiner no Portal do Azure

O Registro de Contêiner do Azure permite armazenar imagens de contêiner do Docker em repositórios. Ao armazenar imagens de armazenamento em repositórios, você poderá ter grupos de imagens (ou versões de imagens) em ambientes isolados. Você pode especificar esses repositórios quando enviar imagens por push para o registro e exibir seus conteúdos no portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos

* **Registro de contêiner**: Crie um Registro de contêiner em sua assinatura do Azure. Por exemplo, use o [Portal do Azure](container-registry-get-started-portal.md) ou a [CLI do Azure](container-registry-get-started-azure-cli.md).
* **CLI do Docker**: instale o [Docker] [ docker-install] em seu computador local, que fornece a interface de linha de comando do Docker.
* **Imagem de contêiner**: enviar por push uma imagem para o registro de contêiner. Para obter orientação sobre como efetuar push e pull de imagens, consulte [Efetuar push e pull de imagem](container-registry-get-started-docker-cli.md).

## <a name="view-repositories-in-azure-portal"></a>Exibir repositórios de exibição no portal do Azure

Você pode ver uma lista de repositórios que hospedam suas imagens, bem como as marcas de imagem, no portal do Azure.

Se você seguiu as etapas em [Efetuar push e pull de imagem](container-registry-get-started-docker-cli.md) (e não excluiu a imagem posteriormente), você deve ter uma imagem Nginx no registro de contêiner. As instruções no artigo especificaram que você deve marcar a imagem com um namespace, os "exemplos" em `/samples/nginx`. Para relembrar, o comando de [push do Docker] [ docker-push] especificado no artigo foi:

```Bash
docker push myregistry.azurecr.io/samples/nginx
```

 Como o Registro de Contêiner do Azure oferece suporte a esses namespaces de repositório de vários níveis, você pode definir o escopo das coleções de imagens relacionadas a um aplicativo específico, ou a um conjunto de aplicativos, para diversas equipes de desenvolvimento ou operacionais. Para saber mais sobre repositórios em registros de contêiner, consulte [Registros de contêiner do Docker privado no Azure](container-registry-intro.md).

Para exibir um repositório:

1. Entre no [portal do Azure][portal]
1. Selecione o **Registro de Contêiner do Azure** para o qual você enviou por push a imagem Nginx
1. Selecione **Repositórios** para ver uma lista dos repositórios que contêm imagens no registro
1. Selecione um repositório para ver as marcas de imagem dentro desse repositório

Por exemplo, se você enviou por push a imagem Nginx como indicado em [Efetuar push e pull de imagem](container-registry-get-started-docker-cli.md), você verá algo semelhante a:

![Repositórios no portal](./media/container-registry-repositories/container-registry-repositories.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você conhece as noções básicas sobre como exibir e trabalhar com repositórios no portal, experimente usar o Registro de Contêiner do Azure com um cluster do [Serviço de Contêiner do Azure (AKS)](../aks/tutorial-kubernetes-prepare-app.md).

<!-- LINKS - External -->
[docker-install]: https://docs.docker.com/engine/installation/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[portal]: https://portal.azure.com
