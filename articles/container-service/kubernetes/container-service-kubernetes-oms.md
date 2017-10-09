---
title: "cluster do Azure Kubernetes aaaMonitor - gerenciamento de operações | Microsoft Docs"
description: "Monitoramento do cluster Kubernetes no serviço de contêiner do Azure usando o Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="605b9-103">Monitorar um cluster do Serviço de Contêiner do Azure com o Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="605b9-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="605b9-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="605b9-104">Prerequisites</span></span>
<span data-ttu-id="605b9-105">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="605b9-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="605b9-106">Ele também pressupõe que você tenha Olá `az` cli do Azure e `kubectl` ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="605b9-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="605b9-107">Você pode testar se você tiver Olá `az` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="605b9-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="605b9-108">Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="605b9-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="605b9-109">Como alternativa, você pode usar [Shell de nuvem do Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tem Olá `az` cli do Azure e `kubectl` ferramentas já instaladas para você.</span><span class="sxs-lookup"><span data-stu-id="605b9-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="605b9-110">Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="605b9-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="605b9-111">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="605b9-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="605b9-112">tootest se você tiver chaves kubernetes instaladas em sua ferramenta kubectl que você pode executar:</span><span class="sxs-lookup"><span data-stu-id="605b9-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="605b9-113">Se hello acima erros de comando out, você precisa chaves do cluster kubernetes tooinstall em sua ferramenta kubectl.</span><span class="sxs-lookup"><span data-stu-id="605b9-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="605b9-114">Você pode fazer isso com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="605b9-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="605b9-115">Contêineres de monitoramentos no Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="605b9-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="605b9-116">O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e em nuvem.</span><span class="sxs-lookup"><span data-stu-id="605b9-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="605b9-117">Contêiner é uma solução de análise de logs do OMS, que ajuda a exibir o inventário de contêiner hello, desempenho e logs em um único local.</span><span class="sxs-lookup"><span data-stu-id="605b9-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="605b9-118">Você pode auditar, solucionar problemas de contêineres exibindo Olá logs em um local centralizado e encontrar ruidosas consumindo em excesso contêiner em um host.</span><span class="sxs-lookup"><span data-stu-id="605b9-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="605b9-119">Para obter mais informações sobre solução de contêiner, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="605b9-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="605b9-120">Instalando o OMS em Kubernetes</span><span class="sxs-lookup"><span data-stu-id="605b9-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="605b9-121">Obter sua ID do espaço de trabalho e a chave</span><span class="sxs-lookup"><span data-stu-id="605b9-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="605b9-122">Saudação de serviço do OMS agente tootalk toohello necessárias toobe configurado com uma id do espaço de trabalho e uma chave do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="605b9-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="605b9-123">tooget Olá id e a chave é necessário toocreate um OMS conta em <https://mms.microsoft.com>. Siga etapas de saudação toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="605b9-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="605b9-124">Quando você terminar de criar conta de saudação, você precisa tooobtain sua id e a chave clicando **configurações**, em seguida, **fontes conectadas**e, em seguida, **servidores Linux**, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="605b9-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="605b9-125">Instalar o agente do OMS hello usando um DaemonSet</span><span class="sxs-lookup"><span data-stu-id="605b9-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="605b9-126">DaemonSets são usados por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="605b9-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="605b9-127">Eles são perfeitos para a execução de agentes de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="605b9-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="605b9-128">Aqui está a saudação [arquivo YAML DaemonSet](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="605b9-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="605b9-129">Salve-o arquivo tooa chamado `oms-daemonset.yaml` e substitua os valores de espaço reservado de saudação para `WSID` e `KEY` com a id do espaço de trabalho e a chave no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="605b9-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="605b9-130">Depois de adicionar a ID do espaço de trabalho e a chave toohello DaemonSet configuração, você pode instalar o agente do OMS Olá em seu cluster com hello `kubectl` ferramenta de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="605b9-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="605b9-131">Instalando o agente do OMS hello usando um segredo Kubernetes</span><span class="sxs-lookup"><span data-stu-id="605b9-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="605b9-132">tooprotect a ID do espaço de trabalho do OMS e a chave que você pode usar o segredo Kubernetes como parte do arquivo DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="605b9-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="605b9-133">Copie o script hello, arquivo de modelo de segredo e hello arquivo DaemonSet YAML (de [repositório](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e certifique-se de que elas estão no hello mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="605b9-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="605b9-134">script de geração de segredo – secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="605b9-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="605b9-135">modelo de segredo – secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="605b9-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="605b9-136">Arquivo YAML do DaemonSet – omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="605b9-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="605b9-137">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="605b9-137">Run hello script.</span></span> <span data-ttu-id="605b9-138">Olá script pedirá Olá ID do espaço de trabalho do OMS e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="605b9-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="605b9-139">Insira o que e script hello criará um arquivo yaml segredo para que você pode executá-lo.</span><span class="sxs-lookup"><span data-stu-id="605b9-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="605b9-140">Crie pod de segredos Olá executando Olá seguinte:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="605b9-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="605b9-141">toocheck, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="605b9-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="605b9-142">Criar o omsagent daemon-set executando ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="605b9-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="605b9-143">Conclusão</span><span class="sxs-lookup"><span data-stu-id="605b9-143">Conclusion</span></span>
<span data-ttu-id="605b9-144">É isso!</span><span class="sxs-lookup"><span data-stu-id="605b9-144">That's it!</span></span> <span data-ttu-id="605b9-145">Após alguns minutos, você deve ser capaz de toosee dados fluindo tooyour painel do OMS.</span><span class="sxs-lookup"><span data-stu-id="605b9-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
