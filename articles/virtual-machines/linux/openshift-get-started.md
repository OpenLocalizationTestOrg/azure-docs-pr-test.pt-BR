---
title: aaaDeploy tooAzure OpenShift origem | Microsoft Docs
description: "Saiba mais máquinas virtuais do toodeploy OpenShift origem tooAzure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="3c851-103">Implantar origem OpenShift tooAzure máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3c851-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="3c851-104">[OpenShift Origin](https://www.openshift.org/) é uma plataforma de contêiner de software livre criada em [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="3c851-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="3c851-105">Ele simplifica o processo de saudação da implantação, escala e operação de aplicativos de multilocação.</span><span class="sxs-lookup"><span data-stu-id="3c851-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="3c851-106">Este guia descreve como toodeploy OpenShift origem em máquinas virtuais do Azure usando Olá CLI do Azure e modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c851-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="3c851-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="3c851-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c851-108">Crie um toomanage KeyVault chaves SSH para cluster de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="3c851-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="3c851-109">Implante um cluster OpenShift em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c851-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="3c851-110">Instalar e configurar Olá [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c851-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="3c851-111">Personalize a implantação de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="3c851-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="3c851-112">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="3c851-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="3c851-113">Este guia rápido requer Olá CLI do Azure versão 2.0.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3c851-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="3c851-114">versão de hello toofind, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="3c851-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="3c851-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3c851-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="3c851-116">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="3c851-116">Log in tooAzure</span></span> 
<span data-ttu-id="3c851-117">Login tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela ou clique em **Experimente** toouse Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3c851-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="3c851-118">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3c851-118">Create a resource group</span></span>

<span data-ttu-id="3c851-119">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3c851-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3c851-120">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3c851-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="3c851-121">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="3c851-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="3c851-122">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="3c851-122">Create a Key Vault</span></span>
<span data-ttu-id="3c851-123">Criar uma saudação de toostore KeyVault chaves SSH para cluster Olá com hello [keyvault az criar](/cli/azure/keyvault#create) comando.</span><span class="sxs-lookup"><span data-stu-id="3c851-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="3c851-124">Criar uma chave SSH</span><span class="sxs-lookup"><span data-stu-id="3c851-124">Create an SSH key</span></span> 
<span data-ttu-id="3c851-125">Uma chave SSH é necessário toosecure acesso toohello cluster OpenShift origem.</span><span class="sxs-lookup"><span data-stu-id="3c851-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="3c851-126">Criar um par de chaves SSH usando Olá `ssh-keygen` comando.</span><span class="sxs-lookup"><span data-stu-id="3c851-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="3c851-127">Olá par de chaves SSH, você cria não deve ter uma senha.</span><span class="sxs-lookup"><span data-stu-id="3c851-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="3c851-128">Para obter mais informações sobre as chaves de SSH no Windows, [como chaves de toocreate SSH no Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="3c851-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="3c851-129">Armazenar chave privada SSH no Key Vault</span><span class="sxs-lookup"><span data-stu-id="3c851-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="3c851-130">Olá OpenShift implantação usa chave SSH Olá criados acesso toosecure toohello OpenShift mestre.</span><span class="sxs-lookup"><span data-stu-id="3c851-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="3c851-131">tooenable Olá implantação toosecurely recuperar a chave SSH hello, chave de saudação do repositório no cofre de chaves usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c851-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="3c851-132">Habilitado para implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="3c851-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="3c851-133">Criar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="3c851-133">Create a service principal</span></span> 
<span data-ttu-id="3c851-134">O OpenShift se comunica com o Azure usando um nome de usuário e i,a senha ou uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c851-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="3c851-135">Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o OpenShift.</span><span class="sxs-lookup"><span data-stu-id="3c851-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="3c851-136">Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c851-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="3c851-137">segurança de tooimprove por apenas fornecer um nome de usuário e uma senha, este exemplo cria um serviço básico principal.</span><span class="sxs-lookup"><span data-stu-id="3c851-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="3c851-138">Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que OpenShift precisa:</span><span class="sxs-lookup"><span data-stu-id="3c851-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="3c851-139">Tome nota da saudação appId propriedade retornada pelo comando hello.</span><span class="sxs-lookup"><span data-stu-id="3c851-139">Take note of hello appId property returned from hello command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="3c851-140">Não crie uma senha não segura.</span><span class="sxs-lookup"><span data-stu-id="3c851-140">Don't create an insecure password.</span></span>  <span data-ttu-id="3c851-141">Execute a orientação [Restrições e regras de senha do Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="3c851-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="3c851-142">Para obter mais informações sobre entidades de serviço, confira [Criar entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="3c851-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="3c851-143">Implantar Olá modelo de origem OpenShift</span><span class="sxs-lookup"><span data-stu-id="3c851-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="3c851-144">Em seguida, implante o OpenShift Origin usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3c851-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="3c851-145">comando a seguir Hello requer az CLI 2.0.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3c851-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="3c851-146">Você pode verificar Olá az CLI versão com hello `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="3c851-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="3c851-147">Olá tooupdate versão CLI, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3c851-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="3c851-148">Saudação de uso `appId` valor da entidade de serviço Olá criado anteriormente para Olá `aadClientId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3c851-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="3c851-149">implantação de saudação pode levar too20 toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="3c851-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="3c851-150">Olá URL do console de OpenShift hello e o nome DNS do hello OpenShift mestre é impressa toohello terminal quando Olá implantação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="3c851-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="3c851-151">Conecte-se toohello OpenShift cluster</span><span class="sxs-lookup"><span data-stu-id="3c851-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="3c851-152">Quando a conclusão da implantação hello, conecte-se toohello OpenShift console usando o navegador hello usando Olá `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="3c851-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="3c851-153">Como alternativa, você pode conectar toohello OpenShift mestre usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c851-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="3c851-154">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="3c851-154">Clean up resources</span></span>
<span data-ttu-id="3c851-155">Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster OpenShift e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="3c851-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="3c851-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c851-156">Next steps</span></span>

<span data-ttu-id="3c851-157">Neste tutorial, vimos como:</span><span class="sxs-lookup"><span data-stu-id="3c851-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="3c851-158">Crie um toomanage KeyVault chaves SSH para cluster de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="3c851-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="3c851-159">Implante um cluster OpenShift em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c851-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="3c851-160">Instalar e configurar Olá [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c851-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="3c851-161">Agora esse cluster de origem OpenShift é implantado.</span><span class="sxs-lookup"><span data-stu-id="3c851-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="3c851-162">Você pode seguir OpenShift tutoriais toolearn como toodeploy seu primeiro aplicativo e use Olá OpenShift ferramentas.</span><span class="sxs-lookup"><span data-stu-id="3c851-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="3c851-163">Consulte [Introdução à origem OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="3c851-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
