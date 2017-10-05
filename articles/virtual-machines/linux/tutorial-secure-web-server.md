---
title: Proteger um servidor Web com certificados SSL no Azure | Microsoft Docs
description: Saiba como proteger o servidor Web NGINX com certificados SSL em uma VM do Linux no Azure
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
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="d0027-103">Proteger um servidor Web com certificados SSL em uma máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="d0027-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="d0027-104">Para proteger servidores Web, um certificado SSL (protocolo SSL) pode ser usado para criptografar o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="d0027-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="d0027-105">Esses certificados SSL podem ser armazenados no Azure Key Vault e permitem implantações seguras de certificados em VMs (máquinas virtuais) do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="d0027-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="d0027-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="d0027-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0027-107">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="d0027-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="d0027-108">Gerar ou carregar um certificado para o Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="d0027-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="d0027-109">Criar uma VM e instalar o servidor Web NGINX</span><span class="sxs-lookup"><span data-stu-id="d0027-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="d0027-110">Inserir o certificado na VM e configurar o NGINX com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="d0027-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d0027-111">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d0027-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d0027-112">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="d0027-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="d0027-113">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d0027-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="d0027-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d0027-114">Overview</span></span>
<span data-ttu-id="d0027-115">O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas.</span><span class="sxs-lookup"><span data-stu-id="d0027-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="d0027-116">O Key Vault simplifica o processo de gerenciamento de certificados e permite que você mantenha o controle das chaves que acessam esses certificados.</span><span class="sxs-lookup"><span data-stu-id="d0027-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="d0027-117">Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.</span><span class="sxs-lookup"><span data-stu-id="d0027-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="d0027-118">Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="d0027-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="d0027-119">Esse processo garante que os certificados mais recentes sejam instalados em um servidor Web durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="d0027-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="d0027-120">Se você renova ou substitui um certificado, também não precisa criar uma nova imagem de VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="d0027-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="d0027-121">Os certificados mais recentes são inseridos automaticamente, conforme você cria outras VMs.</span><span class="sxs-lookup"><span data-stu-id="d0027-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="d0027-122">Durante todo o processo, os certificados nunca deixam a plataforma do Azure ou são expostos em um script, no histórico da linha de comando ou no modelo.</span><span class="sxs-lookup"><span data-stu-id="d0027-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="d0027-123">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="d0027-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="d0027-124">Antes de criar um Key Vault e os certificados, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d0027-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d0027-125">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroupSecureWeb* no local *eastus*:</span><span class="sxs-lookup"><span data-stu-id="d0027-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="d0027-126">Em seguida, crie um Key Vault com o [az keyvault create](/cli/azure/keyvault#create) e habilite-o para ser usado quando você implantar uma VM.</span><span class="sxs-lookup"><span data-stu-id="d0027-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="d0027-127">Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d0027-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="d0027-128">Substitua *<mykeyvault>* no exemplo a seguir com seu próprio nome exclusivo do Key Vault:</span><span class="sxs-lookup"><span data-stu-id="d0027-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="d0027-129">Gerar um certificado e armazenar no Key Vault</span><span class="sxs-lookup"><span data-stu-id="d0027-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="d0027-130">Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="d0027-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="d0027-131">Para este tutorial, o exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/certificate#create) que usa a política de certificado padrão:</span><span class="sxs-lookup"><span data-stu-id="d0027-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="d0027-132">Preparar um certificado para usar com uma VM</span><span class="sxs-lookup"><span data-stu-id="d0027-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="d0027-133">Para usar o certificado durante o processo de criação de VM, obtenha a identificação do seu certificado com as [ versões secretas de az keyvault](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="d0027-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="d0027-134">Converter o certificado com [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="d0027-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="d0027-135">O exemplo a seguir atribui a saída desses comandos variáveis de facilidade de uso nas próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="d0027-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="d0027-136">Criar uma configuração de cloud-init para proteger o NGINX</span><span class="sxs-lookup"><span data-stu-id="d0027-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="d0027-137">[Inicialização de nuvem](https://cloudinit.readthedocs.io) é uma abordagem amplamente utilizada para personalizar uma VM do Linux, quando ela é inicializada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="d0027-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="d0027-138">Você pode utilizar a inicialização de nuvem para instalar pacotes e gravar arquivos, ou para configurar usuários e segurança.</span><span class="sxs-lookup"><span data-stu-id="d0027-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="d0027-139">Como a inicialização de nuvem é executada durante o processo de inicialização inicial, não há etapa adicional ou agentes necessários para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="d0027-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="d0027-140">Quando você cria uma VM, certificados e chaves são armazenados no diretório protegido */var/lib/waagent/*.</span><span class="sxs-lookup"><span data-stu-id="d0027-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="d0027-141">Para automatizar a adição do certificado à VM e configurar o servidor Web, use o cloud-init.</span><span class="sxs-lookup"><span data-stu-id="d0027-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="d0027-142">Neste exemplo, instalamos e configuramos o servidor Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="d0027-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="d0027-143">Você pode usar o mesmo processo para instalar e configurar o Apache.</span><span class="sxs-lookup"><span data-stu-id="d0027-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="d0027-144">Crie um arquivo chamado *cloud-init-web-server.txt* e cole a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="d0027-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="d0027-145">Criar uma VM segura</span><span class="sxs-lookup"><span data-stu-id="d0027-145">Create a secure VM</span></span>
<span data-ttu-id="d0027-146">Agora, crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d0027-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d0027-147">Os dados do certificado são injetados no cofre da chave com o `--secrets` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d0027-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="d0027-148">Você passa a configuração cloud-init com o parâmetro `--custom-data`:</span><span class="sxs-lookup"><span data-stu-id="d0027-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="d0027-149">Demora alguns minutos para que a VM seja criada, os pacotes para instalar e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0027-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="d0027-150">Quando a VM tiver sido criada, observe o `publicIpAddress` exibido pela CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0027-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="d0027-151">Este endereço é usado para acessar seu site em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="d0027-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="d0027-152">Para permitir o tráfego da web para acessar sua VM, abra a porta 443 da Internet com [az vm open-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="d0027-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="d0027-153">Testar o aplicativo Web protegido</span><span class="sxs-lookup"><span data-stu-id="d0027-153">Test the secure web app</span></span>
<span data-ttu-id="d0027-154">Agora, abra um navegador da Web e digite *https://<publicIpAddress>* na barra de endereços.</span><span class="sxs-lookup"><span data-stu-id="d0027-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="d0027-155">Forneça seu próprio endereço de IP público do processo de criação da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d0027-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="d0027-156">Se você usou um certificado autoassinado, aceite o aviso de segurança:</span><span class="sxs-lookup"><span data-stu-id="d0027-156">Accept the security warning if you used a self-signed certificate:</span></span>

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="d0027-158">Seu site de NGINX protegido é exibido, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0027-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![Exibir o site NGINX em execução](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="d0027-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0027-160">Next steps</span></span>

<span data-ttu-id="d0027-161">Neste tutorial, você protegeu um servidor Web NGINX com um certificado SSL armazenado no Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d0027-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="d0027-162">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="d0027-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0027-163">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="d0027-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="d0027-164">Gerar ou carregar um certificado para o Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="d0027-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="d0027-165">Criar uma VM e instalar o servidor Web NGINX</span><span class="sxs-lookup"><span data-stu-id="d0027-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="d0027-166">Inserir o certificado na VM e configurar o NGINX com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="d0027-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="d0027-167">Siga este link para ver exemplos de script de máquina virtual predefinido.</span><span class="sxs-lookup"><span data-stu-id="d0027-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0027-168">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="d0027-168">Windows virtual machine script samples</span></span>](./cli-samples.md)