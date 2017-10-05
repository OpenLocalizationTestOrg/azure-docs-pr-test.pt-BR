---
title: Configurando um cluster do Service Fabric usando o Visual Studio | Microsoft Docs
description: Descreve como configurar um cluster do Service Fabric usando o modelo do Azure Resource Manager criado por um projeto de Grupo de Recursos do Azure no Visual Studio
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
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="ea9d2-103">Configurar um cluster do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea9d2-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="ea9d2-104">Este artigo descreve como configurar um cluster do Service Fabric do Azure usando o Visual Studio e um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="ea9d2-105">Usaremos o projeto de grupo de recursos do Azure do Visual Studio para criar o modelo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="ea9d2-106">Depois que o modelo tiver sido criado, ele pode ser implantado diretamente no Azure a partir do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="ea9d2-107">Ele também pode ser usado em um script, ou como parte do recurso de CI (integração contínua).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="ea9d2-108">Criar um modelo de cluster do Service Fabric usando um projeto de grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea9d2-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="ea9d2-109">Para começar, abra o Visual Studio e crie um projeto de grupo de recursos do Azure (ele está disponível na pasta **Nuvem** ):</span><span class="sxs-lookup"><span data-stu-id="ea9d2-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Caixa de diálogo Novo Projeto com o projeto do Grupo de Recursos do Azure selecionado][1]

<span data-ttu-id="ea9d2-111">Você pode criar uma nova solução do Visual Studio para este projeto ou adicioná-lo a uma solução existente.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9d2-112">Se você não vir o projeto do grupo de recursos do Azure sob o nó da Nuvem, o SDK do Azure não estará instalado.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="ea9d2-113">Inicie o Web Platform Installer ([instale-o agora](http://www.microsoft.com/web/downloads/platform.aspx) caso ainda não tenha feito isso), pesquise "SDK do Azure para .NET" e instale a versão compatível com sua versão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="ea9d2-114">Depois que pressionar o botão OK, Visual Studio solicitará que você selecione o modelo do Gerenciador de Recursos que deseja criar:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Selecione a caixa de diálogo do Modelo do Azure com o modelo de Cluster do Service Fabric selecionado][2]

<span data-ttu-id="ea9d2-116">Selecione o modelo Cluster do Service Fabric e pressione o botão OK novamente.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="ea9d2-117">O projeto e o modelo do Gerenciador de Recursos foram criados agora.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="ea9d2-118">Preparar o modelo para implantação</span><span class="sxs-lookup"><span data-stu-id="ea9d2-118">Prepare the template for deployment</span></span>
<span data-ttu-id="ea9d2-119">Antes da implantação do modelo para a criação do cluster, você deve fornecer valores para os parâmetros necessários do modelo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="ea9d2-120">Esses valores de parâmetro são lidos no arquivo `ServiceFabricCluster.parameters.json`, que está na pasta `Templates` do projeto de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="ea9d2-121">Abra o arquivo e forneça os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="ea9d2-122">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="ea9d2-122">Parameter name</span></span> | <span data-ttu-id="ea9d2-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="ea9d2-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea9d2-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="ea9d2-124">adminUserName</span></span> |<span data-ttu-id="ea9d2-125">O nome da conta de administrador para máquinas do Service Fabric (nós).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="ea9d2-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="ea9d2-126">certificateThumbprint</span></span> |<span data-ttu-id="ea9d2-127">A impressão digital do certificado que protege o cluster.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="ea9d2-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="ea9d2-128">sourceVaultResourceId</span></span> |<span data-ttu-id="ea9d2-129">A *ID do recurso* do cofre da chave no qual o certificado que protege o cluster é armazenado.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="ea9d2-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="ea9d2-130">certificateUrlValue</span></span> |<span data-ttu-id="ea9d2-131">A URL do certificado de segurança do cluster.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="ea9d2-132">O modelo do Gerenciador de Recursos do Service Fabric do Visual Studio cria um cluster seguro que é protegido por um certificado.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="ea9d2-133">Esse certificado é identificado pelos três últimos parâmetros do modelo (`certificateThumbprint`, `sourceVaultValue`, e `certificateUrlValue`), e ele deve existir em um **Cofre de Chaves do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="ea9d2-134">Para saber mais sobre como criar o certificado de segurança do cluster, veja o artigo [Cenários de segurança do cluster do Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) .</span><span class="sxs-lookup"><span data-stu-id="ea9d2-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="ea9d2-135">Opcional: alterar o nome do cluster</span><span class="sxs-lookup"><span data-stu-id="ea9d2-135">Optional: change the cluster name</span></span>
<span data-ttu-id="ea9d2-136">Cada cluster do Service Fabric tem um nome.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="ea9d2-137">Quando um cluster do Fabric é criado no Azure, o nome do cluster determina (com a região do Azure) o nome DNS (Sistema de Nomes de Domínio) para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="ea9d2-138">Por exemplo, se você nomear seu cluster `myBigCluster` e o local (região do Azure) do grupo de recursos que hospedará o novo cluster for o Leste dos EUA, o nome DNS do cluster será `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ea9d2-139">Por padrão, o nome do cluster é gerado automaticamente e se torna exclusivo pelo acréscimo de um sufixo aleatório a um prefixo "cluster".</span><span class="sxs-lookup"><span data-stu-id="ea9d2-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="ea9d2-140">Isso facilita o uso do modelo como parte de um sistema de **integração contínua** (CI).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="ea9d2-141">Se quiser usar um nome específico para seu cluster, um que seja significativo para você, defina o valor da variável `clusterName` no arquivo de modelo do Resource Manager (`ServiceFabricCluster.json`) para o nome de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="ea9d2-142">É a primeira variável definida nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="ea9d2-143">Opcional: adicionar portas públicas do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ea9d2-143">Optional: add public application ports</span></span>
<span data-ttu-id="ea9d2-144">Talvez você queira alterar as portas públicas de aplicativos do cluster antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="ea9d2-145">Por padrão, o modelo abre apenas duas portas TCP públicas (80 e 8081).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="ea9d2-146">Se você precisar de mais para seus aplicativos, modifique a definição de Balanceador de Carga do Azure no modelo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="ea9d2-147">A definição é armazenada no arquivo de modelo principal (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="ea9d2-148">Abra o arquivo e procure por `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="ea9d2-149">Cada porta está associada a três artefatos:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="ea9d2-150">Uma variável de modelo que define o valor da porta TCP para a porta:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="ea9d2-151">Uma *investigação* que define com que frequência, e por quanto tempo, o Azure load balancer tenta usar um nó específico do Service Fabric antes de executar o failover para outro nó.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="ea9d2-152">As investigações fazem parte do recurso de Balanceador de Carga.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="ea9d2-153">Esta é a definição de investigação para a primeira porta de aplicativo padrão:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-153">Here is the probe definition for the first default application port:</span></span>
   
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
3. <span data-ttu-id="ea9d2-154">Uma *regra de balanceamento de carga* que vincula a porta e a investigação, o que permite o balanceamento de carga em um conjunto de nós de cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="ea9d2-155">Se os aplicativos que planeja implantar no cluster precisarem de mais portas, você poderá adicioná-las criando mais definições de investigação e de regra de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="ea9d2-156">Para saber mais sobre como trabalhar com o Azure Load Balancer por meio de modelos do Gerenciador de Recursos, veja [Introdução à criação de um balanceador de carga interno usando um modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="ea9d2-157">Implantar o modelo usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea9d2-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="ea9d2-158">Após salvar todos os valores de parâmetro necessários no arquivo`ServiceFabricCluster.param.dev.json` , você está pronto para implantar o modelo e criar o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="ea9d2-159">Clique com botão direito no projeto de grupo de recursos no Gerenciador de Soluções do Visual Studio e escolha **Implantar | Nova Implantação...**.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="ea9d2-160">Se necessário, o Visual Studio mostrará a caixa de diálogo **Implantar no Grupo de Recursos**, solicitando a autenticação do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea9d2-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Caixa de diálogo Implantar no Grupo de Recursos][3]

<span data-ttu-id="ea9d2-162">A caixa de diálogo permite que você escolha um grupo de recursos existente do Gerenciador de Recursos para o cluster e oferece uma opção para criar um novo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="ea9d2-163">Normalmente, faz sentido usar um grupo de recursos separado para um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="ea9d2-164">Após pressionar o botão Implantar, o Visual Studio solicitará a confirmação dos valores de parâmetro do modelo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="ea9d2-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ea9d2-165">Hit the **Save** button.</span></span> <span data-ttu-id="ea9d2-166">Um parâmetro não tem um valor persistente: a senha da conta administrativa para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="ea9d2-167">Você precisa fornecer um valor de senha quando o Visual Studio solicitar um.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9d2-168">Começando com o Azure SDK 2.9, o Visual Studio oferece suporte à leitura de senhas do **Cofre de Chaves do Azure** durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="ea9d2-169">Na caixa de diálogo de parâmetros de modelo, observe que a caixde texto `adminPassword` de parâmetro tem um pequeno ícone de "chave" à direita.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="ea9d2-170">Esse ícone permite que você selecione um segredo do cofre de chaves existente como a senha administrativa para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="ea9d2-171">Apenas certifique-se primeiro de habilitar o acesso do Azure Resource Manager para implantação do modelo nas Políticas de Acesso Avançado do seu Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="ea9d2-172">Você pode monitorar o andamento do processo de implantação na janela de saída do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="ea9d2-173">Após a conclusão da implantação do modelo, o novo cluster estará pronto para uso!</span><span class="sxs-lookup"><span data-stu-id="ea9d2-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="ea9d2-174">Se o PowerShell nunca tiver sido usado para administrar o Azure no computador que você está usando no momento, é necessário fazer uma pequena limpeza.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="ea9d2-175">Habilite o script do PowerShell executando o comando [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ea9d2-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="ea9d2-176">Para os computadores de desenvolvimento a política "irrestrita" é geralmente aceitável.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="ea9d2-177">Decida se deseja permitir a coleta de dados de diagnóstico de comandos do Azure PowerShell e execute [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) ou [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx), conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="ea9d2-178">Isso evitará solicitações desnecessárias durante a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="ea9d2-179">Em caso de erros, vá para o [portal do Azure](https://portal.azure.com/) e abra o grupo de recursos que você implantou.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="ea9d2-180">Clique em **Todas as configurações** e, em seguida, clique em **Implantações** na folha de configurações.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="ea9d2-181">Uma implantação com falha do grupo de recursos deixa informações detalhadas sobre o diagnóstico nesse local.</span><span class="sxs-lookup"><span data-stu-id="ea9d2-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9d2-182">Os clusters de Service Fabric exigem um determinado número de nós esteja ativo para manter a disponibilidade e preservar o estado – conhecido como "manter o quórum".</span><span class="sxs-lookup"><span data-stu-id="ea9d2-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="ea9d2-183">Portanto, não é seguro desligar todos os computadores no cluster, a menos que você tenha primeiro executado um [backup completo do estado](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ea9d2-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ea9d2-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea9d2-184">Next steps</span></span>
* [<span data-ttu-id="ea9d2-185">Saiba mais sobre como configurar o cluster do Service Fabric usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ea9d2-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="ea9d2-186">Saiba mais sobre como gerenciar e implantar aplicativos do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea9d2-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
