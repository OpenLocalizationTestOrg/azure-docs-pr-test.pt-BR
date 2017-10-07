---
title: "aaaApplication ou específicas do usuário maratona serviço | Microsoft Docs"
description: "Criar um aplicativo ou serviço do Marathon específico do usuário"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Marathon, microsserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Criar um aplicativo ou serviço do Marathon específico do usuário
O Serviço de Contêiner do Azure fornece um conjunto de servidores mestres no qual podemos pré-configurar o Apache Mesos e o Marathon. Eles podem ser usado tooorchestrate seus aplicativos no cluster hello, mas recomendada não toouse Olá servidores mestres para essa finalidade. Por exemplo, ajuste a configuração de saudação do maratona requer logon em servidores mestres de saudação próprios e fazer alterações – isso incentiva servidores mestres exclusivos que estão um pouco diferente do padrão de saudação e necessidade toobe cuidado e gerenciados de forma independente. Além disso, configuração de saudação exigida por uma equipe pode não ser uma configuração ideal para outra equipe hello.

Neste artigo, vamos explicar como tooadd um serviço de aplicativo ou usuário específico maratona.

Como esse serviço pertencerão tooa único usuário ou equipe, eles são tooconfigure livre-lo de qualquer forma que desejar. Além disso, o serviço de contêiner do Azure assegurará que o serviço de saudação continue toorun. Se o serviço de saudação falhar, o serviço de contêiner do Azure reiniciará para você. A maioria do tempo de saudação você mesmo não irá notar que tinha o tempo de inatividade.

## <a name="prerequisites"></a>Pré-requisitos
[Implantar uma instância do serviço de contêiner do Azure](container-service-deployment.md) com o orchestrator digite DC/OS e [Certifique-se de que o cliente pode se conectar a cluster tooyour](../container-service-connect.md). Além disso, Olá seguintes etapas.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Criar um aplicativo ou serviço do Marathon específico do usuário
Comece criando um arquivo de configuração JSON que define o nome de saudação do serviço de aplicativo hello que você deseja toocreate. Aqui usamos `marathon-alice` como o nome da estrutura hello. Salvar arquivo hello como algo como `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Em seguida, use a instância de maratona de saudação do hello CLI DC/OS tooinstall com opções de saudação que são definidas no arquivo de configuração:

```bash
dcos package install --options=marathon-alice.json marathon
```

Agora você verá sua `marathon-alice` serviço em execução no guia de serviços de saudação da interface de usuário do controlador de domínio/OS. Olá interface do usuário será `http://<hostname>/service/marathon-alice/` se você quiser tooaccess-lo diretamente.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Definir Olá CLI DC/OS tooaccess serviço Olá
Opcionalmente você pode configurar seu tooaccess CLI DC/sistema operacional desse novo serviço por configuração Olá `marathon.url` propriedade toopoint toohello `marathon-alice` instância da seguinte maneira:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Você pode verificar qual instância de maratona sua CLI está trabalhando em relação a saudação `dcos config show` comando. Você pode reverter toousing seu serviço maratona mestre com o comando Olá `dcos config unset marathon.url`.

