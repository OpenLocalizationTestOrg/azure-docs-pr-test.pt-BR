---
title: "aaaDeploy Deis 3 nós cluster | Microsoft Docs"
description: "Este artigo descreve como toocreate 3 nós Deis cluster no Azure usando um modelo do Gerenciador de recursos do Azure"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="5769c-103">Implantar e configurar um cluster Deis de 3 nós no Azure</span><span class="sxs-lookup"><span data-stu-id="5769c-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="5769c-104">Este artigo percorre o provisionamento de um cluster [Deis](http://deis.io/) no Azure.</span><span class="sxs-lookup"><span data-stu-id="5769c-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="5769c-105">Ele abrange todas as etapas de saudação criem Olá toodeploying de certificados necessários e dimensionamento de um exemplo **vá** aplicativo no cluster recentemente provisionados hello.</span><span class="sxs-lookup"><span data-stu-id="5769c-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="5769c-106">Olá diagrama a seguir mostra arquitetura de saudação do sistema Olá implantado.</span><span class="sxs-lookup"><span data-stu-id="5769c-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="5769c-107">Um administrador do sistema gerencia Olá cluster usando Deis ferramentas como **deis** e **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="5769c-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="5769c-108">As conexões são estabelecidas por meio de um balanceador de carga do Azure, que encaminha Olá conexões tooone de membro Olá nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5769c-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="5769c-109">o acesso de clientes do Hello implantado aplicativos por meio do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="5769c-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="5769c-110">Nesse caso, o balanceador de carga Olá encaminha Olá tráfego tooa Deis malha do roteador, o que mais routs contêineres do Docker toocorresponding tráfego hospedados no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5769c-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Diagrama da arquitetura do cluster Deis implantado](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="5769c-112">Ordem toorun por meio de saudação etapas a seguir, você precisará:</span><span class="sxs-lookup"><span data-stu-id="5769c-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="5769c-113">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5769c-113">An active Azure subscription.</span></span> <span data-ttu-id="5769c-114">Se você não tiver uma, é possível obter uma avaliação gratuita em [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5769c-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="5769c-115">Um trabalho ou escola id toouse recursos do Azure grupos.</span><span class="sxs-lookup"><span data-stu-id="5769c-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="5769c-116">Se você tiver uma conta pessoal e faça logon com uma id da Microsoft, será necessário muito[criar uma id de trabalho do seu personal](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5769c-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5769c-117">O - dependendo do seu sistema operacional de cliente - Olá [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [CLI do Azure para Mac, Linux e Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5769c-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="5769c-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="5769c-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="5769c-119">OpenSSL é usado toogenerate Olá necessários certificados.</span><span class="sxs-lookup"><span data-stu-id="5769c-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="5769c-120">Um cliente Git como o [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="5769c-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="5769c-121">aplicativo de exemplo hello tootest, também será necessário um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="5769c-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="5769c-122">Você pode usar quaisquer servidores DNS ou serviços que dão suporte a registros de curinga A.</span><span class="sxs-lookup"><span data-stu-id="5769c-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="5769c-123">Um computador toorun Deis ferramentas de cliente.</span><span class="sxs-lookup"><span data-stu-id="5769c-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="5769c-124">Você pode usar um computador local ou uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5769c-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="5769c-125">Você pode executar essas ferramentas em praticamente qualquer distribuição de Linux, mas instruções a seguir hello usam Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5769c-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="5769c-126">Cluster de saudação de provisão</span><span class="sxs-lookup"><span data-stu-id="5769c-126">Provision hello cluster</span></span>
<span data-ttu-id="5769c-127">Nesta seção, você usará um [do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modelo do repositório de código-fonte aberto Olá [modelos de início rápido do azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5769c-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="5769c-128">Primeiro, você copiará para o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5769c-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="5769c-129">Em seguida, criará um novo par de chaves SSH para autenticação.</span><span class="sxs-lookup"><span data-stu-id="5769c-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="5769c-130">Depois, você configurará um novo identificador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="5769c-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="5769c-131">E, finalmente, você usará o script de Shell hello ou cluster de Olá Olá PowerShell script tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5769c-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="5769c-132">Repositório de saudação do clone: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5769c-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="5769c-133">Acesse a pasta do modelo de toohello:</span><span class="sxs-lookup"><span data-stu-id="5769c-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="5769c-134">Crie um novo par de chaves SSH usando ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="5769c-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="5769c-135">Gere um certificado usando Olá acima da chave privada:</span><span class="sxs-lookup"><span data-stu-id="5769c-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="5769c-136">Vá muito[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate um novo token de cluster, que se parece algo como:</span><span class="sxs-lookup"><span data-stu-id="5769c-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="5769c-137">Cada cluster CoreOS precisa toohave um token exclusivo desse serviço gratuito.</span><span class="sxs-lookup"><span data-stu-id="5769c-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="5769c-138">Veja a [documentação do CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="5769c-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="5769c-139">Modificar Olá **nuvem config.yaml** tooreplace Olá existente de arquivos **descoberta** token com um novo token de saudação:</span><span class="sxs-lookup"><span data-stu-id="5769c-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="5769c-140">Modificar Olá **azuredeploy parameters.json** arquivo: certificado Olá aberto criado na etapa 4 em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="5769c-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="5769c-141">Copiar todo o texto entre `----BEGIN CERTIFICATE-----` e `-----END CERTIFICATE-----` em Olá **sshKeyData** parâmetro (você precisará tooremove todos os caracteres de nova linha).</span><span class="sxs-lookup"><span data-stu-id="5769c-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="5769c-142">Modificar Olá **newStorageAccountName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5769c-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="5769c-143">Esta é a conta de armazenamento de saudação para discos de sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="5769c-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="5769c-144">Este nome de conta tem toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5769c-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="5769c-145">Modificar Olá **publicDomainName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5769c-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="5769c-146">Isso se tornará parte do nome DNS Olá associado com o IP público do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="5769c-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="5769c-147">Olá FQDN final terá o formato de saudação do *[valor desse parâmetro]*. *[Região]* . cloudapp.azure.com. Por exemplo, se você especificar o nome hello como deishbai32 e grupo de recursos de saudação for região Oeste dos EUA de toohello implantado, Olá final balanceador de carga do FQDN tooyour será deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5769c-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="5769c-148">Salve o arquivo de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="5769c-148">Save hello parameter file.</span></span> <span data-ttu-id="5769c-149">E, em seguida, você pode provisionar o cluster hello usando o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5769c-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="5769c-150">ou o CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="5769c-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="5769c-151">Quando o grupo de recursos Olá é provisionado, você pode ver todos os recursos de saudação em grupo Olá no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5769c-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="5769c-152">Conforme mostrado no hello seguinte captura de tela, hello grupo de recursos contém uma rede virtual com três VMs, que são unidas toohello mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5769c-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="5769c-153">grupo de saudação também contém um balanceador de carga, que tem um IP público associado.</span><span class="sxs-lookup"><span data-stu-id="5769c-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Olá provisionado o grupo de recursos no portal clássico do Azure](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="5769c-155">Instalar o cliente Olá</span><span class="sxs-lookup"><span data-stu-id="5769c-155">Install hello client</span></span>
<span data-ttu-id="5769c-156">Você precisa **deisctl** toocontrol sua Deis cluster.</span><span class="sxs-lookup"><span data-stu-id="5769c-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="5769c-157">Embora deisctl é instalado automaticamente em todos os nós de cluster Olá, é um deisctl toouse de prática recomendada em um computador administrativo separado.</span><span class="sxs-lookup"><span data-stu-id="5769c-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="5769c-158">Além disso, como todos os nós são configurados com apenas os endereços IP privados, será necessário toouse SSH túnel por meio do balanceador de carga hello, que tem um IP público, máquinas de nó toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5769c-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="5769c-159">Olá, estas são as etapas de saudação de configuração de deisctl em uma máquina virtual ou Ubuntu físico separado.</span><span class="sxs-lookup"><span data-stu-id="5769c-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="5769c-160">Instale o deis deisctl:mkdir</span><span class="sxs-lookup"><span data-stu-id="5769c-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="5769c-161">Adicione o agente toossh chave privada:</span><span class="sxs-lookup"><span data-stu-id="5769c-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="5769c-162">Configure o deisctl:</span><span class="sxs-lookup"><span data-stu-id="5769c-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="5769c-163">modelo Hello define regras de NAT de entrada que mapeiam 2223 tooinstance 1, 2224 tooinstance 2 e 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="5769c-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="5769c-164">Isso fornece redundância para usar a ferramenta de deisctl hello.</span><span class="sxs-lookup"><span data-stu-id="5769c-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="5769c-165">Você pode examinar essas regras no portal clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="5769c-165">You can examine these rules on Azure classic portal:</span></span>

![Regras NAT no balanceador de carga Olá](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="5769c-167">Atualmente o modelo Olá só dá suporte a clusters de 3 nós.</span><span class="sxs-lookup"><span data-stu-id="5769c-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="5769c-168">Isso se deve a uma limitação na definição da regra NAT do modelo do Gerenciador de Recursos do Azure, que não dá suporte à sintaxe de loop.</span><span class="sxs-lookup"><span data-stu-id="5769c-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="5769c-169">Instale e inicie Olá Deis plataforma</span><span class="sxs-lookup"><span data-stu-id="5769c-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="5769c-170">Agora você pode usar deisctl tooinstall e iniciar Olá Deis plataforma:</span><span class="sxs-lookup"><span data-stu-id="5769c-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="5769c-171">Plataforma de saudação inicial leva um tempo (até 10 minutos).</span><span class="sxs-lookup"><span data-stu-id="5769c-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="5769c-172">Especialmente, iniciando o serviço de construtor Olá pode levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="5769c-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="5769c-173">E, às vezes, leva alguns toosucceed de tentativas: se a operação de saudação parecer toohang, tente digitar `ctrl+c` toobreak a execução do comando hello e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="5769c-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="5769c-174">Você pode usar `deisctl list` tooverify se todos os serviços estão em execução:</span><span class="sxs-lookup"><span data-stu-id="5769c-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="5769c-175">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="5769c-175">Congratulations!</span></span> <span data-ttu-id="5769c-176">Agora, você tem um cluster Deis em execução no Azure!</span><span class="sxs-lookup"><span data-stu-id="5769c-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="5769c-177">Em seguida, vamos implantar um cluster de saudação do Go aplicativo toosee na ação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5769c-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="5769c-178">Implantar e dimensionar um aplicativo Hello World</span><span class="sxs-lookup"><span data-stu-id="5769c-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="5769c-179">Olá etapas a seguir mostram como toodeploy "Hello World" Vá cluster toohello de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5769c-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="5769c-180">Olá etapas são baseadas na [Deis documentação](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="5769c-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="5769c-181">Para Olá roteamento malha toowork corretamente, você precisará toohave um curinga um registro para o seu domínio apontando toohello o IP público saudação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5769c-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="5769c-182">Olá seguinte captura de tela mostra Olá um registro para um registro de domínio de exemplo em GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="5769c-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Registro A do GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="5769c-184">Instalar e o deis:</span><span class="sxs-lookup"><span data-stu-id="5769c-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="5769c-185">Crie uma nova chave SSH e depois adicione Olá tooGitHub de chave pública (é claro, também é possível reutilizar suas chaves existentes).</span><span class="sxs-lookup"><span data-stu-id="5769c-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="5769c-186">toocreate um par de chaves de SSH novo, use:</span><span class="sxs-lookup"><span data-stu-id="5769c-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="5769c-187">Adicione id_rsa.pub ou a chave pública Olá de sua escolha, tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="5769c-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="5769c-188">Você pode fazer isso usando Olá adicionar SSH botão da chave em sua tela de configuração de chaves SSH:</span><span class="sxs-lookup"><span data-stu-id="5769c-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Chave do GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="5769c-190">Registrar um novo usuário:</span><span class="sxs-lookup"><span data-stu-id="5769c-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="5769c-191">Adicione a chave SSH hello:</span><span class="sxs-lookup"><span data-stu-id="5769c-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="5769c-192">Crie um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5769c-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="5769c-193">
8.push do git Olá irão disparar Docker imagens toobe criado e implantado, que o levará alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5769c-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="5769c-194">Na minha experiência, ocasionalmente, pode travar etapa 10 (repositório de tooprivate de imagem Pushing).</span><span class="sxs-lookup"><span data-stu-id="5769c-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="5769c-195">Quando isso acontece, você pode interromper o processo de hello, usando o aplicativo hello remover ' deis aplicativos: destruir – um <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nome de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5769c-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="5769c-196">Se tudo funcionar, você verá algo parecido com a seguinte Olá final Olá das saídas de comando:</span><span class="sxs-lookup"><span data-stu-id="5769c-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="5769c-197">Verifique se o aplicativo hello está funcionando:</span><span class="sxs-lookup"><span data-stu-id="5769c-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="5769c-198">Você deverá ver:</span><span class="sxs-lookup"><span data-stu-id="5769c-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="5769c-199">Escala Olá aplicativo too3 instâncias:</span><span class="sxs-lookup"><span data-stu-id="5769c-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="5769c-200">Opcionalmente, você pode usar deis info tooexamine detalhes do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5769c-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="5769c-201">Olá seguintes saídas são de minha implantação de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5769c-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="5769c-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5769c-202">Next Steps</span></span>
<span data-ttu-id="5769c-203">Este artigo analisou todos os tooprovision de etapas de saudação Deis um novo cluster no Azure usando um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5769c-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="5769c-204">modelo de saudação dá suporte a redundância em ferramentas de conexões, bem como o balanceamento de carga para aplicativos implantados.</span><span class="sxs-lookup"><span data-stu-id="5769c-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="5769c-205">modelo de saudação também evita usando IPs públicos em nós de membro, que salva preciosos recursos IP públicos e fornece um ambiente mais seguro toohost aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5769c-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="5769c-206">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5769c-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="5769c-207">[Visão Geral do Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="5769c-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="5769c-208">[Como toouse Olá CLI do Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="5769c-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="5769c-209">[Usando o Azure PowerShell com o Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="5769c-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
