---
title: aaaSetting um cluster do Service Fabric usando o Visual Studio | Microsoft Docs
description: "Descreve como tooset a uma malha de serviço de cluster usando o modelo do Gerenciador de recursos do Azure criado por um projeto do grupo de recursos do Azure no Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="8c08b-103">Configurar um cluster do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c08b-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="8c08b-104">Este artigo descreve como tooset a uma malha de serviço do Azure de cluster usando o Visual Studio e um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c08b-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="8c08b-105">Vamos usar um modelo de saudação do Azure do Visual Studio recurso grupo projeto toocreate.</span><span class="sxs-lookup"><span data-stu-id="8c08b-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="8c08b-106">Depois de saudação modelo foi criado, ele pode ser implantado diretamente tooAzure do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c08b-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="8c08b-107">Ele também pode ser usado em um script, ou como parte do recurso de CI (integração contínua).</span><span class="sxs-lookup"><span data-stu-id="8c08b-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="8c08b-108">Criar um modelo de cluster do Service Fabric usando um projeto de grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="8c08b-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="8c08b-109">tooget iniciado, abra o Visual Studio e criar um projeto do grupo de recursos do Azure (está disponível no hello **nuvem** pasta):</span><span class="sxs-lookup"><span data-stu-id="8c08b-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![Caixa de diálogo Novo Projeto com o projeto do Grupo de Recursos do Azure selecionado][1]

<span data-ttu-id="8c08b-111">Você pode criar uma nova solução do Visual Studio para este projeto ou adicioná-lo a solução existente de tooan.</span><span class="sxs-lookup"><span data-stu-id="8c08b-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="8c08b-112">Se você não vir o projeto de grupo de recursos do Azure Olá no nó de nuvem hello, você não tem Olá SDK do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="8c08b-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="8c08b-113">Inicie o Web Platform Installer ([instalá-lo agora](http://www.microsoft.com/web/downloads/platform.aspx) se você ainda não tiver) e, em seguida, pesquise por "Azure SDK para .NET" e instalar a versão de saudação que é compatível com sua versão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c08b-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="8c08b-114">Depois de pressionar o botão Okey hello, o Visual Studio solicitará que você tooselect modelo de Gerenciador de recursos de saudação desejado toocreate:</span><span class="sxs-lookup"><span data-stu-id="8c08b-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![Selecione a caixa de diálogo do Modelo do Azure com o modelo de Cluster do Service Fabric selecionado][2]

<span data-ttu-id="8c08b-116">Selecione o modelo de Cluster do Service Fabric hello e botão de ocorrências Olá Okey novamente.</span><span class="sxs-lookup"><span data-stu-id="8c08b-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="8c08b-117">projeto Hello e modelo do Gerenciador de recursos de saudação agora foram criados.</span><span class="sxs-lookup"><span data-stu-id="8c08b-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="8c08b-118">Prepare o modelo de saudação para implantação</span><span class="sxs-lookup"><span data-stu-id="8c08b-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="8c08b-119">Antes de modelo de saudação é cluster de saudação toocreate implantado, você deve fornecer valores hello necessário para parâmetros de modelo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="8c08b-120">Esses valores de parâmetro são lidos da saudação `ServiceFabricCluster.parameters.json` arquivo, que está na saudação `Templates` pasta do projeto de grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c08b-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="8c08b-121">Abra o arquivo hello e fornecer Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c08b-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="8c08b-122">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="8c08b-122">Parameter name</span></span> | <span data-ttu-id="8c08b-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="8c08b-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c08b-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="8c08b-124">adminUserName</span></span> |<span data-ttu-id="8c08b-125">nome de Olá Olá da conta de administrador para máquinas de malha do serviço (nós).</span><span class="sxs-lookup"><span data-stu-id="8c08b-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="8c08b-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="8c08b-126">certificateThumbprint</span></span> |<span data-ttu-id="8c08b-127">Olá a impressão digital do certificado Olá protege cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c08b-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="8c08b-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="8c08b-128">sourceVaultResourceId</span></span> |<span data-ttu-id="8c08b-129">Olá *ID de recurso* do Cofre de chaves Olá onde Olá certificado que protege cluster hello está armazenado.</span><span class="sxs-lookup"><span data-stu-id="8c08b-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="8c08b-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="8c08b-130">certificateUrlValue</span></span> |<span data-ttu-id="8c08b-131">URL de Olá Olá cluster do certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="8c08b-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="8c08b-132">modelo do Gerenciador de recursos de malha de serviço do Visual Studio Olá cria um cluster seguro que é protegido por um certificado.</span><span class="sxs-lookup"><span data-stu-id="8c08b-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="8c08b-133">Esse certificado é identificado pelo Olá último três parâmetros de modelo (`certificateThumbprint`, `sourceVaultValue`, e `certificateUrlValue`), e ela deve existir em um **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="8c08b-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="8c08b-134">Para obter mais informações sobre como toocreate Olá certificado de segurança de cluster, consulte [cenários de segurança de cluster do Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artigo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="8c08b-135">Opcional: altere o nome do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="8c08b-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="8c08b-136">Cada cluster do Service Fabric tem um nome.</span><span class="sxs-lookup"><span data-stu-id="8c08b-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="8c08b-137">Quando um cluster de malha é criado no Azure, o nome do cluster determina (junto com hello região do Azure) nome de sistema de nome de domínio (DNS) Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c08b-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="8c08b-138">Por exemplo, se você nomear seu cluster `myBigCluster`e o local de hello (região do Azure) saudação do grupo de recursos que hospedará o novo cluster de saudação é Leste dos EUA, Olá nome DNS de cluster Olá será `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8c08b-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="8c08b-139">Por padrão nome do cluster Olá é gerado automaticamente e tornará exclusivo, anexando um prefixo de "cluster" tooa sufixo aleatório.</span><span class="sxs-lookup"><span data-stu-id="8c08b-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="8c08b-140">Isso torna muito fácil toouse modelo de saudação como parte de um **integração contínua** system (CI).</span><span class="sxs-lookup"><span data-stu-id="8c08b-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="8c08b-141">Se você quiser toouse um nome específico para o cluster, o que é significativo tooyou, defina o valor de saudação de saudação `clusterName` variável no arquivo de modelo do Gerenciador de recursos de saudação (`ServiceFabricCluster.json`) nome tooyour escolhido.</span><span class="sxs-lookup"><span data-stu-id="8c08b-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="8c08b-142">É a variável primeiro Olá definida no arquivo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="8c08b-143">Opcional: adicionar portas públicas do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8c08b-143">Optional: add public application ports</span></span>
<span data-ttu-id="8c08b-144">Também convém portas de aplicativo pública Olá toochange para cluster Olá antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="8c08b-145">Por padrão, o modelo de saudação abre apenas duas portas TCP públicas (80 e 8081).</span><span class="sxs-lookup"><span data-stu-id="8c08b-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="8c08b-146">Se você precisar de mais de seus aplicativos, modificar a definição de Balanceador de carga do Azure de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c08b-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="8c08b-147">Olá definição é armazenada no arquivo de modelo principal de saudação (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="8c08b-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="8c08b-148">Abra o arquivo e procure por `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="8c08b-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="8c08b-149">Cada porta está associada a três artefatos:</span><span class="sxs-lookup"><span data-stu-id="8c08b-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="8c08b-150">Uma variável de modelo que define o valor da porta TCP Olá para a porta de saudação:</span><span class="sxs-lookup"><span data-stu-id="8c08b-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="8c08b-151">Um *investigação* que define a frequência e de quanto tempo Olá balanceador de carga do Azure tenta toouse um nó específico do Service Fabric antes de falhar em tooanother um.</span><span class="sxs-lookup"><span data-stu-id="8c08b-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="8c08b-152">Olá investigações fazem parte da saudação recursos do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8c08b-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="8c08b-153">Esta é a definição de investigação de saudação para Olá primeiro aplicativo porta:</span><span class="sxs-lookup"><span data-stu-id="8c08b-153">Here is hello probe definition for hello first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="8c08b-154">Um *regra de balanceamento de carga* que une porta hello e investigação hello, que permite a balanceamento de carga em um conjunto de nós de cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="8c08b-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="8c08b-155">Se aplicativos Olá que você planeje toodeploy toohello cluster precisam de mais portas, pode adicioná-los, criar investigação adicional e definições de regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="8c08b-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="8c08b-156">Para obter mais informações sobre como toowork com o balanceador de carga do Azure por meio de modelos do Gerenciador de recursos, consulte [começar a criar um balanceador de carga interno usando um modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8c08b-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="8c08b-157">Implante o modelo de saudação usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c08b-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="8c08b-158">Depois que você salvou todos Olá valores de parâmetros necessários no`ServiceFabricCluster.param.dev.json` arquivo, são o modelo de saudação toodeploy pronto e criar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c08b-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="8c08b-159">Clique em projeto saudação do grupo de recursos no Gerenciador de soluções do Visual Studio e escolha **implantar | Nova implantação...** . Se necessário, o Visual Studio mostrará Olá **implantar tooResource grupo** caixa de diálogo solicitando que você tooauthenticate tooAzure:</span><span class="sxs-lookup"><span data-stu-id="8c08b-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![Implantar a caixa de diálogo de grupo tooResource][3]

<span data-ttu-id="8c08b-161">caixa de diálogo Olá permite escolher um grupo de recursos do Gerenciador de recursos existente para cluster hello e permite que você Olá opção toocreate um novo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="8c08b-162">Normalmente faz sentido toouse um grupo de recursos separado para um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c08b-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="8c08b-163">Depois de tocar Olá implantar botão, o Visual Studio solicitará que você tooconfirm valores de parâmetro de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c08b-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="8c08b-164">Olá ocorrência **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="8c08b-164">Hit hello **Save** button.</span></span> <span data-ttu-id="8c08b-165">Um parâmetro não tem um valor persistente: senha da conta administrativa Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c08b-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="8c08b-166">Você precisará tooprovide um valor de senha ao Visual Studio solicitará um.</span><span class="sxs-lookup"><span data-stu-id="8c08b-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="8c08b-167">Começando com o Azure SDK 2.9, o Visual Studio oferece suporte à leitura de senhas do **Cofre de Chaves do Azure** durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="8c08b-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="8c08b-168">Na caixa de diálogo de parâmetros de modelo Olá, observe que Olá `adminPassword` caixa de texto de parâmetro tem um pequeno ícone de "chave" na saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="8c08b-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="8c08b-169">Esse ícone permite que você tooselect um segredo do Cofre de chaves existente como a senha administrativa Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c08b-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="8c08b-170">Verifique toofirst-se de habilitar o acesso do Gerenciador de recursos do Azure para implantação de modelo em Olá avançada políticas de acesso de seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8c08b-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="8c08b-171">Você pode monitorar o progresso de saudação do processo de implantação de saudação na janela de saída do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="8c08b-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="8c08b-172">Concluída a implantação de modelo hello, o novo cluster é toouse pronto!</span><span class="sxs-lookup"><span data-stu-id="8c08b-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="8c08b-173">Se o PowerShell nunca foi usado tooadminister Azure da máquina de saudação que você está usando agora, será necessário toodo housekeeping um pouco.</span><span class="sxs-lookup"><span data-stu-id="8c08b-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="8c08b-174">Habilitar o PowerShell script executando Olá [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) comando.</span><span class="sxs-lookup"><span data-stu-id="8c08b-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="8c08b-175">Para os computadores de desenvolvimento a política "irrestrita" é geralmente aceitável.</span><span class="sxs-lookup"><span data-stu-id="8c08b-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="8c08b-176">Decidir se tooallow coleta de dados de diagnóstico de comandos do PowerShell do Azure e execute [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) ou [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8c08b-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="8c08b-177">Isso evitará solicitações desnecessárias durante a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="8c08b-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="8c08b-178">Se houver erros, vá toohello [portal do Azure](https://portal.azure.com/) Olá Abrir grupo de recursos implantados em e.</span><span class="sxs-lookup"><span data-stu-id="8c08b-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="8c08b-179">Clique em **todas as configurações**, em seguida, clique em **implantações** na folha de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c08b-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="8c08b-180">Uma implantação com falha do grupo de recursos deixa informações detalhadas sobre o diagnóstico nesse local.</span><span class="sxs-lookup"><span data-stu-id="8c08b-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="8c08b-181">Clusters Service Fabric exigem um determinado número de nós toobe toomaintain disponibilidade e preservam o estado - tooas chamado "mantêm o quórum."</span><span class="sxs-lookup"><span data-stu-id="8c08b-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="8c08b-182">Portanto, não é seguro tooshut para baixo de todas as máquinas de saudação em cluster hello, a menos que você executou antes um [backup completo do estado do seu](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="8c08b-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8c08b-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c08b-183">Next steps</span></span>
* [<span data-ttu-id="8c08b-184">Saiba mais sobre como configurar o cluster do Service Fabric usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8c08b-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="8c08b-185">Saiba como toomanage e implantar aplicativos do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c08b-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
