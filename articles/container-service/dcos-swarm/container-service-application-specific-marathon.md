---
title: "Aplicativo ou serviço do Marathon específico do usuário"
description: "Criar um aplicativo ou serviço do Marathon específico do usuário"
services: container-service
author: rgardler
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 61cc379bf32f3e0db11d8fd9dae36d9ecb6b1a6c
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Criar um aplicativo ou serviço do Marathon específico do usuário

O Serviço de Contêiner do Azure fornece um conjunto de servidores mestres no qual podemos pré-configurar o Apache Mesos e o Marathon. Eles podem ser usados para orquestrar seus aplicativos no cluster, mas é melhor não usar os servidores mestres para essa finalidade. Por exemplo, para fazer o ajuste da configuração do Marathon é necessário fazer o logon nos próprios servidores mestres e então fazer as alterações; isso incentiva a existência de servidores mestres exclusivos que sejam um pouco diferentes do padrão e que precisam ser cuidados e gerenciados de forma independente. Além disso, a configuração exigida por uma equipe pode não ser a configuração ideal para outra equipe.

Neste artigo, explicaremos como adicionar um aplicativo ou serviço do Marathon específico do usuário.

Como esse serviço pertencerá a um único usuário ou a uma única equipe, poderá ser configurado de qualquer forma desejada. Além disso, o Serviço de Contêiner do Azure fará com que o serviço continue a ser executado. Se o serviço falhar, o Serviço de Contêiner do Azure reiniciará para você. Na maioria das vezes, você nem mesmo perceberá o tempo de inatividade.

## <a name="prerequisites"></a>Pré-requisitos
[Implantar uma instância do Serviço de Contêiner do Azure](container-service-deployment.md) com o tipo de orquestrador DC/OS e [garantir que o cliente possa se conectar ao cluster](../container-service-connect.md). Execute as etapas a seguir.

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Criar um aplicativo ou serviço do Marathon específico do usuário
Comece pela criação de um arquivo de configuração JSON que defina o nome do serviço de aplicativo que você deseja criar. Aqui usamos `marathon-alice` como o nome da estrutura. Salve o arquivo com um nome como `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Em seguida, use a CLI do DC/OS para instalar a instância do Marathon com as opções que estão definidas no arquivo de configuração:

```bash
dcos package install --options=marathon-alice.json marathon
```

Agora você deverá ver seu serviço `marathon-alice` em execução na guia Serviços da interface do usuário do DC/OS. A interface do usuário estará `http://<hostname>/service/marathon-alice/` caso você queira acessá-la diretamente.

## <a name="set-the-dcos-cli-to-access-the-service"></a>Configurar a CLI do DC/OS para acessar o serviço
Opcionalmente, você pode configurar a CLI do DC/OS para acessar esse novo serviço, definindo a propriedade `marathon.url` para apontar para a instância `marathon-alice` da seguinte maneira:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Você pode verificar em qual instância do Marathon a CLI está funcionando com o comando `dcos config show` . Você pode voltar a usar o serviço Marathon mestre com o comando `dcos config unset marathon.url`.

