---
title: "aaaAzure amostras de CLI - serviço de aplicativo | Microsoft Docs"
description: "Exemplos de CLI do Azure - Serviço de aplicativo"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Exemplos de CLI do Azure

Olá, tabela a seguir inclui scripts de toobash links criados usando Olá CLI do Azure.

| | |
|-|-|
|**Como criar o aplicativo**||
| [Criar um aplicativo web e implantar o código do GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo Web e implanta o código de um repositório do GitHub público. |
| [Como criar um aplicativo Web com a implantação contínua do GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo Web com a publicação contínua de um repositório do GitHub que você possui. |
| [Como criar um aplicativo Web e implantar o código de um repositório Git local](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo Web do Azure e configura o push de código de um repositório Git local. |
| [Criar um aplicativo web e implantar código tooa ambiente de preparo](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo Web do Azure com um slot de implantação para alterações de código de preparo. |
| [Criar um aplicativo web do ASP.NET Core em um contêiner do Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo Web do Azure no Linux e carrega uma imagem do Docker do Docker Hub. |
|**Como configurar o aplicativo**||
| [Mapa de um aplicativo web do domínio personalizado tooa](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo web do Azure e mapeia um tooit de nome de domínio personalizado. |
| [Associar um certificado SSL personalizado, tooa aplicativo da web](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo web do Azure e associa o certificado SSL de saudação de um tooit de nome de domínio personalizado. |
|**Como escalar um aplicativo**||
| [Como escalar manualmente um aplicativo Web](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo Web do Azure e pode ser dimensionado em 2 instâncias. |
| [Como escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Cria dois aplicativos Web do Azure em duas regiões geográficas diferentes e os disponibiliza por meio de um único ponto de extremidade usando o Gerenciador de tráfego do Azure. |
|**Conecte-se o aplicativo tooresources**||
| [Conecte-se um aplicativo de web tooa banco de dados SQL](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo web do Azure e um banco de dados do SQL e, em seguida, adiciona configurações de aplicativo toohello do cadeia de caracteres de conexão de banco de dados hello. |
| [Conecte-se a uma conta de armazenamento do tooa de aplicativo web](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Cria um aplicativo web do Azure e uma conta de armazenamento e, em seguida, adiciona configurações de aplicativo toohello do cadeia de caracteres de conexão de armazenamento hello. |
| [Conecte-se a um cache de redis de tooa de aplicativo web](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo web do Azure e um cache redis, em seguida, adiciona as configurações de aplicativo hello redis conexão detalhes toohello.) |
| [Conecte-se um aplicativo de web tooCosmos DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo web do Azure e um banco de dados do Cosmos e, em seguida, adiciona as configurações de aplicativo hello Cosmos DB conexão detalhes toohello. |
|**Como monitorar o aplicativo**||
| [Como monitorar um aplicativo Web com logs do servidor Web](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um aplicativo web do Azure, habilita o log para ele e downloads do computador local do tooyour Olá logs. |
| | |