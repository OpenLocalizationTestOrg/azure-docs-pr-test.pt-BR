---
title: "cluster de aaaDeploy um contêiner do Docker no Azure | Microsoft Docs"
description: "Implante uma solução Kubernetes, o controlador de domínio/sistema operacional ou o Docker Swarm no serviço de contêiner do Azure usando Olá portal do Azure ou um modelo do Gerenciador de recursos."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure, dcos, swarm, kubernetes, serviço de contêiner do azure, acs"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="b065d-104">Implantar um contêiner do Docker usando o portal do Azure de saudação de solução de hospedagem</span><span class="sxs-lookup"><span data-stu-id="b065d-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="b065d-105">O Serviço de Contêiner do Azure fornece implantação rápida de soluções populares de orquestração e clustering de contêiner de software livre.</span><span class="sxs-lookup"><span data-stu-id="b065d-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="b065d-106">Este documento orienta a implantar um cluster do serviço de contêiner do Azure usando Olá portal do Azure ou um modelo de início rápido do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b065d-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="b065d-107">Você também pode implantar um cluster do serviço de contêiner do Azure usando Olá [2.0 do CLI do Azure](container-service-create-acs-cluster-cli.md) ou Olá APIs de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="b065d-108">Para obter informações, consulte [Introdução ao Serviço de Contêiner do Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b065d-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b065d-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b065d-109">Prerequisites</span></span>

* <span data-ttu-id="b065d-110">**Assinatura do Azure**: se não tiver uma, inscreva-se em uma [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="b065d-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="b065d-111">Para um cluster maior, considere uma assinatura pré-paga ou outras opções de compra.</span><span class="sxs-lookup"><span data-stu-id="b065d-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b065d-112">O uso de assinatura do Azure e [cotas de recursos](../../azure-subscription-service-limits.md), como cotas de núcleos, pode limitar o tamanho de saudação do cluster Olá implantar.</span><span class="sxs-lookup"><span data-stu-id="b065d-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="b065d-113">toorequest um aumento de cota, abra um [solicitação de suporte do cliente online](../../azure-supportability/how-to-create-azure-support-request.md) sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="b065d-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="b065d-114">**Chave pública RSA SSH**: durante a implantação por meio do portal hello ou um dos modelos de início rápido do Azure hello, você precisará chave pública do tooprovide Olá para autenticação em máquinas virtuais de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="b065d-115">chaves RSA Secure Shell (SSH) toocreate, consulte Olá [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md) orientação.</span><span class="sxs-lookup"><span data-stu-id="b065d-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="b065d-116">**ID do cliente principal e o segredo de serviço** (Kubernetes): para mais informações e diretrizes toocreate uma entidade de serviço do Active Directory do Azure, consulte [sobre a entidade de serviço Olá para um cluster Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b065d-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="b065d-117">Criar um cluster usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b065d-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="b065d-118">Entrar toohello portal do Azure, selecione **novo**e a pesquisa hello Azure Marketplace para **serviço de contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b065d-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Serviço de contêiner do Azure no Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="b065d-120">Clique em **Serviço de Contêiner do Azure** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b065d-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="b065d-121">Em Olá **Noções básicas sobre** folha, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b065d-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="b065d-122">**Orchestrator**: selecione uma saudação contêiner orchestrators toodeploy no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="b065d-123">**DC/OS**: implanta um cluster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="b065d-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="b065d-124">**Swarm**: implanta um cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="b065d-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="b065d-125">**Kubernetes**: implanta um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b065d-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="b065d-126">**Assinatura**: selecione uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="b065d-127">**Grupo de recursos**: Insira nome de saudação de um novo grupo de recursos para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="b065d-128">**Local**: selecione uma região do Azure para a implantação do serviço de contêiner do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="b065d-129">Para disponibilidade, verifique [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="b065d-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Configurações Básicas](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="b065d-131">Clique em **Okey** quando estiver pronto tooproceed.</span><span class="sxs-lookup"><span data-stu-id="b065d-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="b065d-132">Em Olá **mestre configuração** folha, digite Olá configurações de nó mestre do Linux hello ou nós de cluster de saudação (algumas configurações são específicas tooeach orchestrator) a seguir:</span><span class="sxs-lookup"><span data-stu-id="b065d-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="b065d-133">**Nome DNS mestre**: Olá prefixo usado toocreate um exclusivo totalmente qualificado (FQDN) do nome de domínio para o mestre de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="b065d-134">Olá FQDN mestre tem formato Olá *prefixo*gerenciamento*local*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b065d-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="b065d-135">**Nome de usuário**: nome de usuário Olá para uma conta em cada uma das máquinas de virtuais de Linux Olá no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="b065d-136">**Chave pública RSA SSH**: Adicionar Olá toobe chave pública usado para autenticação em relação a saudação máquinas de virtuais de Linux.</span><span class="sxs-lookup"><span data-stu-id="b065d-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="b065d-137">É importante que essa chave contém sem quebras de linha e inclui Olá `ssh-rsa` prefixo.</span><span class="sxs-lookup"><span data-stu-id="b065d-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="b065d-138">Olá `username@domain` sufixo é opcional.</span><span class="sxs-lookup"><span data-stu-id="b065d-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="b065d-139">Olá chave deve ser semelhante a seguir Olá: **AAAAB3Nz de ssh-rsa... <>...... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="b065d-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="b065d-140">**Entidade de serviço**: se você selecionou orchestrator de Kubernetes hello, insira um Azure Active Directory **ID principal do cliente de serviço** (também chamado de hello appId) e **segredo do cliente principal do serviço** (senha).</span><span class="sxs-lookup"><span data-stu-id="b065d-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="b065d-141">Para obter mais informações, consulte [sobre a entidade de serviço Olá para um cluster Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b065d-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="b065d-142">**Contagem de mestre**: Olá número de mestres em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="b065d-143">**Diagnóstico VM**: para alguns orchestrators, você pode habilitar o diagnóstico VM no mestre de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Configuração de mestre](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="b065d-145">Clique em **Okey** quando estiver pronto tooproceed.</span><span class="sxs-lookup"><span data-stu-id="b065d-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="b065d-146">Em Olá **configuração do agente** folha, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b065d-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="b065d-147">**Contagem de agentes**: para por nuvem do Docker e Kubernetes, esse valor é número de saudação inicial de agentes no conjunto de escala de agente Olá.</span><span class="sxs-lookup"><span data-stu-id="b065d-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="b065d-148">Para o controlador de domínio/sistema operacional, é número de saudação inicial de agentes em um conjunto de escala privada.</span><span class="sxs-lookup"><span data-stu-id="b065d-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="b065d-149">Além disso, é criado um conjunto de escala pública para DC/OS, que contém um número predeterminado de agentes.</span><span class="sxs-lookup"><span data-stu-id="b065d-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="b065d-150">Olá número de agentes neste conjunto de escala público é determinado pelo número de saudação de mestres no cluster Olá: um agente de público para um mestre e dois agentes públicos para três ou cinco mestres.</span><span class="sxs-lookup"><span data-stu-id="b065d-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="b065d-151">**Tamanho da máquina virtual agente**: Olá tamanho das máquinas de virtuais de agente hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="b065d-152">**Sistema operacional**: essa configuração está disponível atualmente apenas se você selecionou orchestrator de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="b065d-153">Escolha uma distribuição de Linux ou um toorun de sistema operacional Windows Server em agentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="b065d-154">Essa configuração determina se seu cluster pode executar aplicativos de contêiner do Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b065d-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="b065d-155">O suporte ao contêiner do Windows está em versão prévia para clusters Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b065d-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="b065d-156">Atualmente há suporte somente para agentes Linux no Serviço de Contêiner do Azure nos clusters DC/SO e Swarm.</span><span class="sxs-lookup"><span data-stu-id="b065d-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="b065d-157">**As credenciais de agente**: se você selecionou o sistema de operacional do Windows hello, insira um administrador **nome de usuário** e **senha** para agente Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="b065d-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Configuração do agente](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="b065d-159">Clique em **Okey** quando estiver pronto tooproceed.</span><span class="sxs-lookup"><span data-stu-id="b065d-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="b065d-160">Após a conclusão da validação de serviço, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b065d-160">After service validation finishes, click **OK**.</span></span>

    ![Validação](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="b065d-162">Examine os termos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-162">Review hello terms.</span></span> <span data-ttu-id="b065d-163">processo de implantação de saudação toostart, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b065d-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="b065d-164">Se você tiver optado toopin Olá implantação toohello portal do Azure, você pode ver o status de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Status da Implantação](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="b065d-166">implantação de saudação leva vários toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="b065d-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="b065d-167">Em seguida, o cluster do serviço de contêiner do Azure hello está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="b065d-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="b065d-168">Criar um cluster usando um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="b065d-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="b065d-169">Modelos de início rápido do Azure estão disponível toodeploy um cluster no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="b065d-170">Olá fornecidos modelos quickstart podem ser modificado tooinclude adicionais ou avançadas configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="b065d-171">toocreate um cluster do serviço de contêiner do Azure usando um modelo de início rápido do Azure, você precisa de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="b065d-172">Se não tiver uma, inscreva-se para obter uma [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="b065d-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="b065d-173">Siga estas etapas toodeploy um cluster usando um modelo e hello Azure CLI 2.0 (consulte [instruções de instalação e](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="b065d-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="b065d-174">Se você estiver em um sistema Windows, você pode usar toodeploy de etapas semelhantes em um modelo usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="b065d-175">Consulte as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b065d-175">See steps later in this section.</span></span> <span data-ttu-id="b065d-176">Você também pode implantar um modelo por meio de saudação [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) ou outros métodos.</span><span class="sxs-lookup"><span data-stu-id="b065d-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="b065d-177">toodeploy um cluster Kubernetes, Docker Swarm ou SO/controlador de domínio, selecione um dos modelos de início rápido disponível de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="b065d-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="b065d-178">Veja uma lista parcial.</span><span class="sxs-lookup"><span data-stu-id="b065d-178">A partial list follows.</span></span> <span data-ttu-id="b065d-179">Olá DC/sistema operacional e por nuvem modelos são Olá mesmo, exceto para a seleção de orchestrator saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="b065d-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="b065d-180">Modelo DC/OS</span><span class="sxs-lookup"><span data-stu-id="b065d-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="b065d-181">Modelo do Swarm</span><span class="sxs-lookup"><span data-stu-id="b065d-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="b065d-182">Modelo Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b065d-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="b065d-183">Faça logon na conta do Azure de tooyour (`az login`) e certifique-se de que Olá CLI do Azure é conectado tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b065d-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="b065d-184">Você pode ver a assinatura de padrão de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b065d-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="b065d-185">Se você tiver mais de um tooset de assinatura e a necessidade de uma assinatura diferente do padrão, execute `az account set --subscription` e especifique o nome ou ID de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="b065d-186">Como prática recomendada, use um novo grupo de recursos para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="b065d-187">toocreate um grupo de recursos, use Olá `az group create` comando Especifica um nome de grupo de recursos e local:</span><span class="sxs-lookup"><span data-stu-id="b065d-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="b065d-188">Crie um arquivo contendo Olá necessário modelo JSON parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b065d-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="b065d-189">Arquivo de parâmetros de saudação download chamado `azuredeploy.parameters.json` que acompanha o modelo de serviço de contêiner do Azure Olá `azuredeploy.json` no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b065d-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="b065d-190">Insira valores de parâmetros necessários para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b065d-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="b065d-191">Por exemplo, toouse Olá [modelo DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), fornecer valores de parâmetro para `dnsNamePrefix` e `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="b065d-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="b065d-192">Consulte as descrições de saudação em `azuredeploy.json` e opções para outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b065d-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="b065d-193">Criar um cluster do serviço de contêiner, passando o arquivo de parâmetros de implantação de saudação com hello após o comando, onde:</span><span class="sxs-lookup"><span data-stu-id="b065d-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="b065d-194">**RESOURCE_GROUP** é nome Olá Olá do grupo de recursos que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="b065d-195">**DEPLOYMENT_NAME** (opcional) é um nome que você fornecer toohello implantação.</span><span class="sxs-lookup"><span data-stu-id="b065d-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="b065d-196">**TEMPLATE_URI** é local Olá Olá do arquivo de implantação `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="b065d-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="b065d-197">Esse URI deve ser um arquivo bruto hello, não um ponteiro toohello GitHub UI.</span><span class="sxs-lookup"><span data-stu-id="b065d-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="b065d-198">toofind esse URI, selecione Olá `azuredeploy.json` arquivo no GitHub e, em seguida, clique em Olá **Raw** botão.</span><span class="sxs-lookup"><span data-stu-id="b065d-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="b065d-199">Você também pode fornecer parâmetros como uma cadeia de caracteres formatada em JSON na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="b065d-200">Use uma comando semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b065d-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="b065d-201">implantação de saudação leva vários toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="b065d-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="b065d-202">Comandos equivalentes do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b065d-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="b065d-203">Você também pode implantar um modelo do Serviço de Contêiner do Azure com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b065d-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="b065d-204">Este documento é baseado na versão 1.0 do hello [módulo Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="b065d-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="b065d-205">toodeploy um cluster Kubernetes, Docker Swarm ou SO/controlador de domínio, selecione um dos modelos de início rápido disponível de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="b065d-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="b065d-206">Veja uma lista parcial.</span><span class="sxs-lookup"><span data-stu-id="b065d-206">A partial list follows.</span></span> <span data-ttu-id="b065d-207">Observe que hello DC/sistema operacional e por nuvem modelos são Olá iguais, com exceção de saudação da seleção de orchestrator saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="b065d-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="b065d-208">Modelo DC/OS</span><span class="sxs-lookup"><span data-stu-id="b065d-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="b065d-209">Modelo do Swarm</span><span class="sxs-lookup"><span data-stu-id="b065d-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="b065d-210">Modelo Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b065d-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="b065d-211">Antes de criar um cluster em sua assinatura do Azure, verifique se sua sessão do PowerShell foi assinado em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b065d-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="b065d-212">Você pode fazer isso com hello `Get-AzureRMSubscription` comando:</span><span class="sxs-lookup"><span data-stu-id="b065d-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="b065d-213">Se você precisar toosign em tooAzure, use Olá `Login-AzureRMAccount` comando:</span><span class="sxs-lookup"><span data-stu-id="b065d-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="b065d-214">Como prática recomendada, use um novo grupo de recursos para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="b065d-215">toocreate um grupo de recursos, use Olá `New-AzureRmResourceGroup` de comando e especifique uma região nome e o destino do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b065d-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="b065d-216">Depois de criar um grupo de recursos, você pode criar o cluster com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b065d-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="b065d-217">Olá URI da saudação desejado de modelo é especificado com hello `-TemplateUri` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b065d-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="b065d-218">Quando você executar esse comando, o PowerShell solicitará os valores de parâmetros de implantação.</span><span class="sxs-lookup"><span data-stu-id="b065d-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="b065d-219">Fornecer parâmetros de modelo</span><span class="sxs-lookup"><span data-stu-id="b065d-219">Provide template parameters</span></span>
<span data-ttu-id="b065d-220">Se você estiver familiarizado com o PowerShell, você sabe que você pode percorrer parâmetros de saudação disponíveis para um cmdlet, digite um sinal de subtração (-) e, em seguida, pressionar a tecla TAB a saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="b065d-221">Essa mesma funcionalidade também funciona com os parâmetros definidos no modelo.</span><span class="sxs-lookup"><span data-stu-id="b065d-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="b065d-222">Assim que você digitar o nome do modelo hello, Olá cmdlet busca modelo hello, analisa os parâmetros de saudação e adiciona o comando de toohello de parâmetros de modelo Olá dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="b065d-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="b065d-223">Isso torna fácil toospecify valores de parâmetro de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="b065d-224">E, se você esquecer a um valor de parâmetro obrigatório, PowerShell solicitará sua valor hello.</span><span class="sxs-lookup"><span data-stu-id="b065d-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="b065d-225">Aqui está o comando completo hello, com parâmetros incluídos.</span><span class="sxs-lookup"><span data-stu-id="b065d-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="b065d-226">Forneça seus próprios valores para nomes de saudação de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b065d-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="b065d-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b065d-227">Next steps</span></span>
<span data-ttu-id="b065d-228">Agora que você tem um cluster em funcionamento, confira estes documentos para obter detalhes sobre conexão e gerenciamento:</span><span class="sxs-lookup"><span data-stu-id="b065d-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="b065d-229">Conecte-se o cluster do serviço de contêiner do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="b065d-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="b065d-230">Trabalhar com o Serviço de Contêiner do Azure e o DC/SO</span><span class="sxs-lookup"><span data-stu-id="b065d-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="b065d-231">Trabalhar com o Serviço de Contêiner do Azure e o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b065d-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="b065d-232">Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b065d-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
