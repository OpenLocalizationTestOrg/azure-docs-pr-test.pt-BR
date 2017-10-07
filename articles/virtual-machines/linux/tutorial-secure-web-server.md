---
title: aaaSecure certificados de um servidor web com SSL no Azure | Microsoft Docs
description: "Saiba como certificados de servidor da web NGINX toosecure Olá com SSL em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f3874-103">Proteger um servidor Web com certificados SSL em uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="f3874-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="f3874-104">servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser usado tooencrypt o tráfego da web.</span><span class="sxs-lookup"><span data-stu-id="f3874-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="f3874-105">Esses certificados SSL podem ser armazenados no cofre de chaves do Azure e permitem implantações seguras de certificados tooLinux (máquinas virtuais) no Azure.</span><span class="sxs-lookup"><span data-stu-id="f3874-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="f3874-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f3874-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3874-107">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="f3874-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f3874-108">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="f3874-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="f3874-109">Criar uma máquina virtual e instalar o servidor de web NGINX Olá</span><span class="sxs-lookup"><span data-stu-id="f3874-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="f3874-110">Injetar certificado Olá Olá VM e configurar NGINX com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="f3874-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f3874-111">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f3874-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f3874-112">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3874-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f3874-113">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f3874-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="f3874-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f3874-114">Overview</span></span>
<span data-ttu-id="f3874-115">O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas.</span><span class="sxs-lookup"><span data-stu-id="f3874-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="f3874-116">Cofre de chaves ajuda a simplificar o processo de gerenciamento de certificado hello e permite que você controle toomaintain de chaves que acessam esses certificados.</span><span class="sxs-lookup"><span data-stu-id="f3874-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="f3874-117">Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.</span><span class="sxs-lookup"><span data-stu-id="f3874-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="f3874-118">Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="f3874-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="f3874-119">Esse processo garante que os certificados de mais atualizados de saudação são instalados em um servidor web durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="f3874-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="f3874-120">Se você renova ou substituir um certificado, você não tem também toocreate uma nova imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="f3874-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="f3874-121">certificados mais recentes Olá são automaticamente inseridos ao criar VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="f3874-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="f3874-122">Durante todo o processo Olá, certificados de saudação nunca deixam Olá plataforma Windows Azure ou são expostos em um modelo, histórico de linha de comando ou script.</span><span class="sxs-lookup"><span data-stu-id="f3874-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="f3874-123">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="f3874-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="f3874-124">Antes de criar um Key Vault e os certificados, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f3874-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f3874-125">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupSecureWeb* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="f3874-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="f3874-126">Em seguida, crie um Key Vault com o [az keyvault create](/cli/azure/keyvault#create) e habilite-o para ser usado quando você implantar uma VM.</span><span class="sxs-lookup"><span data-stu-id="f3874-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="f3874-127">Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f3874-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="f3874-128">Substituir  *<mykeyvault>*  em Olá exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3874-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="f3874-129">Gerar um certificado e armazenar no Key Vault</span><span class="sxs-lookup"><span data-stu-id="f3874-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="f3874-130">Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="f3874-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="f3874-131">Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/certificate#create) que usa a política de certificado saudação padrão:</span><span class="sxs-lookup"><span data-stu-id="f3874-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="f3874-132">Preparar um certificado para usar com uma VM</span><span class="sxs-lookup"><span data-stu-id="f3874-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="f3874-133">certificado de saudação toouse durante a saudação VM criar processo, obter ID de saudação do seu certificado com [az keyvault secreta listar versões](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="f3874-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="f3874-134">Converter certificado Olá com [az formato vm secreta](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="f3874-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="f3874-135">saudação de exemplo a seguir atribui saída Olá toovariables esses comandos para facilidade de uso em Olá próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="f3874-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="f3874-136">Criar uma configuração de nuvem init toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="f3874-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="f3874-137">[Nuvem init](https://cloudinit.readthedocs.io) é toocustomize uma abordagem amplamente usado em uma VM do Linux conforme ele é inicializado para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="f3874-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="f3874-138">Você pode usar pacotes de tooinstall init de nuvem e gravar arquivos, ou usuários tooconfigure e segurança.</span><span class="sxs-lookup"><span data-stu-id="f3874-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="f3874-139">Como init de nuvem é executado durante o processo de inicialização hello, não há nenhuma etapa adicional ou necessários agentes tooapply sua configuração.</span><span class="sxs-lookup"><span data-stu-id="f3874-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="f3874-140">Quando você cria uma VM, certificados e chaves são armazenadas no hello protegido */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="f3874-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="f3874-141">adicionando tooautomate Olá certificado toohello VM e configuração de servidor web hello, use init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f3874-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="f3874-142">Neste exemplo, vamos instalar e configurar o servidor de web NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="f3874-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="f3874-143">Você pode usar o hello mesmo processo tooinstall e configurar o Apache.</span><span class="sxs-lookup"><span data-stu-id="f3874-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="f3874-144">Crie um arquivo chamado *nuvem-init-web-server.txt* e colar Olá seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="f3874-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="f3874-145">Criar uma VM segura</span><span class="sxs-lookup"><span data-stu-id="f3874-145">Create a secure VM</span></span>
<span data-ttu-id="f3874-146">Agora, crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f3874-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f3874-147">dados de certificado de saudação são injetados do Cofre de chaves com hello `--secrets` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f3874-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="f3874-148">Você passa na configuração de nuvem init Olá com hello `--custom-data` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="f3874-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="f3874-149">Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f3874-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="f3874-150">Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3874-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="f3874-151">Este endereço é usado tooaccess seu site em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f3874-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="f3874-152">tooallow proteger tooreach de tráfego da web sua VM, abra a porta 443 de saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="f3874-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="f3874-153">Aplicativo de teste na web segura de Olá</span><span class="sxs-lookup"><span data-stu-id="f3874-153">Test hello secure web app</span></span>
<span data-ttu-id="f3874-154">Agora você pode abrir um navegador da web e digite *https://<publicIpAddress>*  na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3874-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="f3874-155">Fornecer seu próprio público endereço IP da saudação VM criar processo.</span><span class="sxs-lookup"><span data-stu-id="f3874-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="f3874-156">Aceite o aviso de segurança de saudação se você usou um certificado autoassinado:</span><span class="sxs-lookup"><span data-stu-id="f3874-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="f3874-158">Seu site NGINX protegido é exibido como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3874-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Exibir o site NGINX em execução](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="f3874-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f3874-160">Next steps</span></span>

<span data-ttu-id="f3874-161">Neste tutorial, você protegeu um servidor Web NGINX com um certificado SSL armazenado no Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f3874-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="f3874-162">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="f3874-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3874-163">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="f3874-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f3874-164">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="f3874-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="f3874-165">Criar uma máquina virtual e instalar o servidor de web NGINX Olá</span><span class="sxs-lookup"><span data-stu-id="f3874-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="f3874-166">Injetar certificado Olá Olá VM e configurar NGINX com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="f3874-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="f3874-167">Siga este toosee link pré-criadas exemplos de script da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f3874-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3874-168">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="f3874-168">Windows virtual machine script samples</span></span>](./cli-samples.md)