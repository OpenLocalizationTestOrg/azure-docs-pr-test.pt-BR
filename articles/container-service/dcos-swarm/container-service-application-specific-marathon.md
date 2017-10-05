---
title: "Aplicativo ou serviço do Marathon específico do usuário | Microsoft Docs"
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
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="e1bf9-104">Criar um aplicativo ou serviço do Marathon específico do usuário</span><span class="sxs-lookup"><span data-stu-id="e1bf9-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="e1bf9-105">O Serviço de Contêiner do Azure fornece um conjunto de servidores mestres no qual podemos pré-configurar o Apache Mesos e o Marathon.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="e1bf9-106">Eles podem ser usados para orquestrar seus aplicativos no cluster, mas é melhor não usar os servidores mestres para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="e1bf9-107">Por exemplo, para fazer o ajuste da configuração do Marathon é necessário fazer o logon nos próprios servidores mestres e então fazer as alterações; isso incentiva a existência de servidores mestres exclusivos que sejam um pouco diferentes do padrão e que precisam ser cuidados e gerenciados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="e1bf9-108">Além disso, a configuração exigida por uma equipe pode não ser a configuração ideal para outra equipe.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="e1bf9-109">Neste artigo, explicaremos como adicionar um aplicativo ou serviço do Marathon específico do usuário.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="e1bf9-110">Como esse serviço pertencerá a um único usuário ou a uma única equipe, poderá ser configurado de qualquer forma desejada.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="e1bf9-111">Além disso, o Serviço de Contêiner do Azure fará com que o serviço continue a ser executado.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="e1bf9-112">Se o serviço falhar, o Serviço de Contêiner do Azure reiniciará para você.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="e1bf9-113">Na maioria das vezes, você nem mesmo perceberá o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1bf9-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1bf9-114">Prerequisites</span></span>
<span data-ttu-id="e1bf9-115">[Implantar uma instância do Serviço de Contêiner do Azure](container-service-deployment.md) com o tipo de orquestrador DC/OS e [garantir que o cliente possa se conectar ao cluster](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e1bf9-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="e1bf9-116">Execute as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="e1bf9-117">Criar um aplicativo ou serviço do Marathon específico do usuário</span><span class="sxs-lookup"><span data-stu-id="e1bf9-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="e1bf9-118">Comece pela criação de um arquivo de configuração JSON que defina o nome do serviço de aplicativo que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="e1bf9-119">Aqui usamos `marathon-alice` como o nome da estrutura.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="e1bf9-120">Salve o arquivo com um nome como `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="e1bf9-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="e1bf9-121">Em seguida, use a CLI do DC/OS para instalar a instância do Marathon com as opções que estão definidas no arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="e1bf9-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="e1bf9-122">Agora você deverá ver seu serviço `marathon-alice` em execução na guia Serviços da interface do usuário do DC/OS.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="e1bf9-123">A interface do usuário estará `http://<hostname>/service/marathon-alice/` caso você queira acessá-la diretamente.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="e1bf9-124">Configurar a CLI do DC/OS para acessar o serviço</span><span class="sxs-lookup"><span data-stu-id="e1bf9-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="e1bf9-125">Opcionalmente, você pode configurar a CLI do DC/OS para acessar esse novo serviço, definindo a propriedade `marathon.url` para apontar para a instância `marathon-alice` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1bf9-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="e1bf9-126">Você pode verificar em qual instância do Marathon a CLI está funcionando com o comando `dcos config show` .</span><span class="sxs-lookup"><span data-stu-id="e1bf9-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="e1bf9-127">Você pode voltar a usar o serviço Marathon mestre com o comando `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="e1bf9-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

