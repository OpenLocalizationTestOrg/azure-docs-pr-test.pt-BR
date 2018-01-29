---
title: "Tutorial das Instâncias de Contêiner do Azure - Preparar seu aplicativo"
description: "Tutorial das Instâncias de Contêiner do Azure parte 1 de 3 – Preparar um aplicativo para implantação nas Instâncias de Contêiner do Azure"
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: tutorial
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: fc16be80e776d1472be775fa32354ba157d16545
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="create-container-for-deployment-to-azure-container-instances"></a>Criar contêiner para implantação nas Instâncias de Contêiner do Azure

As Instâncias de Contêiner do Azure permitem a implantação de contêineres do Docker na infraestrutura do Azure sem o provisionamento de máquinas virtuais ou a adoção de serviço de nível superior. Neste tutorial, você criará um aplicativo Web pequeno no Node.js e o empacotará em um contêiner que pode ser executado usando as Instâncias de Contêiner do Azure.

Neste artigo, a primeira parte da série, você:

> [!div class="checklist"]
> * Clonar código-fonte do aplicativo do GitHub
> * Cria uma imagem de contêiner da origem do aplicativo
> * Testa a imagem em um ambiente de Docker local

Nos tutoriais subsequentes, você carregará sua imagem em um Registro de Contêiner do Azure e os implantará nas Instâncias de Contêiner do Azure.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial requer a execução da CLI do Azure versão 2.0.23 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure][azure-cli-install].

Este tutorial assume uma compreensão básica dos conceitos fundamentais do Docker como contêineres, imagens de contêiner e comandos básicos do `docker`. Se necessário, consulte [Introdução ao Docker][docker-get-started] para conhecer os conceitos básicos de contêiner.

Para concluir este tutorial, você precisa de um ambiente de desenvolvimento do Docker instalado localmente. O Docker fornece pacotes que o configuram facilmente em qualquer sistema [Mac][docker-mac], [Windows][docker-windows] ou [Linux][docker-linux].

Azure Cloud Shell não inclui os componentes de Docker necessários para concluir cada etapa neste tutorial. Você precisa instalar o ambiente de desenvolvimento do Docker e a CLI do Azure no computador local para concluir este tutorial.

## <a name="get-application-code"></a>Obter o código de aplicativo

O exemplo neste tutorial inclui um aplicativo Web simples criado no [Node.js][nodejs]. O aplicativo serve a uma página HTML estática e tem esta aparência:

![Aplicativo de tutorial mostrado no navegador][aci-tutorial-app]

Use o git para baixar o exemplo:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-the-container-image"></a>Criar a imagem de contêiner

O Dockerfile fornecido no repositório de exemplo mostra como o contêiner é criado. Ele inicia de uma [imagem oficial do Node.js][docker-hub-nodeimage] com base no [Alpine Linux][alpine-linux], uma distribuição pequena que é adequada para usar com contêineres. Em seguida, ele copia os arquivos do aplicativo para o contêiner, instala dependências usando o Gerenciador de Pacotes do Node e inicia o aplicativo.

```Dockerfile
FROM node:8.9.3-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Use o comando [docker build][docker-build] para criar a imagem de contêiner, marcando-o como *aci-tutorial-app*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

A saída do comando [docker build][docker-build] é semelhante ao seguinte (truncado para legibilidade):

```bash
Sending build context to Docker daemon  119.3kB
Step 1/6 : FROM node:8.9.3-alpine
8.9.3-alpine: Pulling from library/node
88286f41530e: Pull complete
84f3a4bf8410: Pull complete
d0d9b2214720: Pull complete
Digest: sha256:c73277ccc763752b42bb2400d1aaecb4e3d32e3a9dbedd0e49885c71bea07354
Status: Downloaded newer image for node:8.9.3-alpine
 ---> 90f5ee24bee2
...
Step 6/6 : CMD node /usr/src/app/index.js
 ---> Running in f4a1ea099eec
 ---> 6edad76d09e9
Removing intermediate container f4a1ea099eec
Successfully built 6edad76d09e9
Successfully tagged aci-tutorial-app:latest
```

Use o comando [docker images][docker-images] para ver a imagem interna:

```bash
docker images
```

Saída:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-the-container-locally"></a>Executar o contêiner localmente

Antes de tentar implantar o contêiner nas Instâncias de Contêiner do Azure, execute-o localmente para confirmar se ele funciona. A opção `-d` permite que o contêiner seja executado em segundo plano, enquanto `-p` permite mapear uma porta aleatória em seu computador para a porta 80 no contêiner.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Abra o navegador http://localhost:8080 para confirmar que o contêiner está sendo executado.

![Executando o aplicativo localmente no navegador][aci-tutorial-app-local]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou uma imagem de contêiner que pode ser implantada nas Instâncias de Contêiner do Azure. As etapas a seguir foram concluídas:

> [!div class="checklist"]
> * A fonte do aplicativo foi clonada do GitHub
> * As imagens de contêiner foram criadas da fonte do aplicativo
> * O contêiner foi testado localmente

Avance para o próximo tutorial para saber mais sobre como armazenar imagens de contêiner em um Registro de Contêiner do Azure.

> [!div class="nextstepaction"]
> [Enviar imagens por push ao Registro de Contêiner do Azure](./container-instances-tutorial-prepare-acr.md)

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png

<!-- LINKS - External -->
[alpine-linux]: https://alpinelinux.org/
[docker-build]: https://docs.docker.com/engine/reference/commandline/build/
[docker-get-started]: https://docs.docker.com/get-started/
[docker-hub-nodeimage]: https://store.docker.com/images/node
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/
[nodejs]: http://nodejs.org

<!-- LINKS - Internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
