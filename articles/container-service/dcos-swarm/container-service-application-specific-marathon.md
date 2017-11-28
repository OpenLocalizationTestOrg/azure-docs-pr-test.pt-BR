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
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="33ac7-104">Criar um aplicativo ou serviço do Marathon específico do usuário</span><span class="sxs-lookup"><span data-stu-id="33ac7-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="33ac7-105">O Serviço de Contêiner do Azure fornece um conjunto de servidores mestres no qual podemos pré-configurar o Apache Mesos e o Marathon.</span><span class="sxs-lookup"><span data-stu-id="33ac7-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="33ac7-106">Eles podem ser usado tooorchestrate seus aplicativos no cluster hello, mas recomendada não toouse Olá servidores mestres para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="33ac7-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="33ac7-107">Por exemplo, ajuste a configuração de saudação do maratona requer logon em servidores mestres de saudação próprios e fazer alterações – isso incentiva servidores mestres exclusivos que estão um pouco diferente do padrão de saudação e necessidade toobe cuidado e gerenciados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="33ac7-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="33ac7-108">Além disso, configuração de saudação exigida por uma equipe pode não ser uma configuração ideal para outra equipe hello.</span><span class="sxs-lookup"><span data-stu-id="33ac7-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="33ac7-109">Neste artigo, vamos explicar como tooadd um serviço de aplicativo ou usuário específico maratona.</span><span class="sxs-lookup"><span data-stu-id="33ac7-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="33ac7-110">Como esse serviço pertencerão tooa único usuário ou equipe, eles são tooconfigure livre-lo de qualquer forma que desejar.</span><span class="sxs-lookup"><span data-stu-id="33ac7-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="33ac7-111">Além disso, o serviço de contêiner do Azure assegurará que o serviço de saudação continue toorun.</span><span class="sxs-lookup"><span data-stu-id="33ac7-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="33ac7-112">Se o serviço de saudação falhar, o serviço de contêiner do Azure reiniciará para você.</span><span class="sxs-lookup"><span data-stu-id="33ac7-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="33ac7-113">A maioria do tempo de saudação você mesmo não irá notar que tinha o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="33ac7-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33ac7-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33ac7-114">Prerequisites</span></span>
<span data-ttu-id="33ac7-115">[Implantar uma instância do serviço de contêiner do Azure](container-service-deployment.md) com o orchestrator digite DC/OS e [Certifique-se de que o cliente pode se conectar a cluster tooyour](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="33ac7-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="33ac7-116">Além disso, Olá seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="33ac7-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="33ac7-117">Criar um aplicativo ou serviço do Marathon específico do usuário</span><span class="sxs-lookup"><span data-stu-id="33ac7-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="33ac7-118">Comece criando um arquivo de configuração JSON que define o nome de saudação do serviço de aplicativo hello que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="33ac7-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="33ac7-119">Aqui usamos `marathon-alice` como o nome da estrutura hello.</span><span class="sxs-lookup"><span data-stu-id="33ac7-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="33ac7-120">Salvar arquivo hello como algo como `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="33ac7-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="33ac7-121">Em seguida, use a instância de maratona de saudação do hello CLI DC/OS tooinstall com opções de saudação que são definidas no arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="33ac7-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="33ac7-122">Agora você verá sua `marathon-alice` serviço em execução no guia de serviços de saudação da interface de usuário do controlador de domínio/OS.</span><span class="sxs-lookup"><span data-stu-id="33ac7-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="33ac7-123">Olá interface do usuário será `http://<hostname>/service/marathon-alice/` se você quiser tooaccess-lo diretamente.</span><span class="sxs-lookup"><span data-stu-id="33ac7-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="33ac7-124">Definir Olá CLI DC/OS tooaccess serviço Olá</span><span class="sxs-lookup"><span data-stu-id="33ac7-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="33ac7-125">Opcionalmente você pode configurar seu tooaccess CLI DC/sistema operacional desse novo serviço por configuração Olá `marathon.url` propriedade toopoint toohello `marathon-alice` instância da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="33ac7-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="33ac7-126">Você pode verificar qual instância de maratona sua CLI está trabalhando em relação a saudação `dcos config show` comando.</span><span class="sxs-lookup"><span data-stu-id="33ac7-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="33ac7-127">Você pode reverter toousing seu serviço maratona mestre com o comando Olá `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="33ac7-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

