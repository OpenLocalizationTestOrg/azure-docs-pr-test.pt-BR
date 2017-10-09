---
title: "aaaCustomize uma VM do Linux na primeira inicialização no Azure | Microsoft Docs"
description: "Saiba como toouse nuvem-init e saudação de VMs do Linux do Cofre de chaves toocustomze primeira vez que eles são iniciados no Azure"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="65c74-103">Como toocustomize uma máquina virtual do Linux na primeira inicialização</span><span class="sxs-lookup"><span data-stu-id="65c74-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="65c74-104">Um tutorial anterior, você aprendeu como tooSSH tooa VM (máquina virtual) e instale manualmente NGINX.</span><span class="sxs-lookup"><span data-stu-id="65c74-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="65c74-105">toocreate VMs de uma maneira rápida e consistente, alguma forma de automação geralmente é desejado.</span><span class="sxs-lookup"><span data-stu-id="65c74-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="65c74-106">Um toocustomize de abordagem comum uma VM na primeira inicialização é toouse [init nuvem](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="65c74-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="65c74-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="65c74-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65c74-108">Criar um arquivo de configuração cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="65c74-109">Criar uma VM que usa um arquivo cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="65c74-110">Exibir um aplicativo Node. js em execução depois da saudação que VM é criada</span><span class="sxs-lookup"><span data-stu-id="65c74-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="65c74-111">Usar o Cofre de chaves toosecurely repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="65c74-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="65c74-112">Automatizar implantações seguras de NGINX com cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="65c74-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="65c74-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="65c74-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c74-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="65c74-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="65c74-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="65c74-116">Visão geral da inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="65c74-116">Cloud-init overview</span></span>
<span data-ttu-id="65c74-117">[Nuvem init](https://cloudinit.readthedocs.io) é toocustomize uma abordagem amplamente usado em uma VM do Linux conforme ele é inicializado para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="65c74-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="65c74-118">Você pode usar pacotes de tooinstall init de nuvem e gravar arquivos, ou usuários tooconfigure e segurança.</span><span class="sxs-lookup"><span data-stu-id="65c74-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="65c74-119">Como init de nuvem é executado durante o processo de inicialização hello, não há nenhuma etapa adicional ou necessários agentes tooapply sua configuração.</span><span class="sxs-lookup"><span data-stu-id="65c74-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="65c74-120">A inicialização de nuvem também funciona em distribuições.</span><span class="sxs-lookup"><span data-stu-id="65c74-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="65c74-121">Por exemplo, você não usar **apt get install** ou **yum instalar** tooinstall um pacote.</span><span class="sxs-lookup"><span data-stu-id="65c74-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="65c74-122">Em vez disso, você pode definir uma lista de pacotes tooinstall.</span><span class="sxs-lookup"><span data-stu-id="65c74-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="65c74-123">Init de nuvem usa automaticamente a ferramenta de gerenciamento de pacote nativo Olá para distribuição Olá que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="65c74-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="65c74-124">Estamos trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhar com imagens Olá que eles fornecem tooAzure.</span><span class="sxs-lookup"><span data-stu-id="65c74-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="65c74-125">Olá, a tabela a seguir descreve disponibilidade de nuvem init atual Olá nas imagens da plataforma Windows Azure:</span><span class="sxs-lookup"><span data-stu-id="65c74-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="65c74-126">Alias</span><span class="sxs-lookup"><span data-stu-id="65c74-126">Alias</span></span> | <span data-ttu-id="65c74-127">Editor</span><span class="sxs-lookup"><span data-stu-id="65c74-127">Publisher</span></span> | <span data-ttu-id="65c74-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="65c74-128">Offer</span></span> | <span data-ttu-id="65c74-129">SKU</span><span class="sxs-lookup"><span data-stu-id="65c74-129">SKU</span></span> | <span data-ttu-id="65c74-130">Versão</span><span class="sxs-lookup"><span data-stu-id="65c74-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="65c74-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="65c74-131">UbuntuLTS</span></span> |<span data-ttu-id="65c74-132">Canônico</span><span class="sxs-lookup"><span data-stu-id="65c74-132">Canonical</span></span> |<span data-ttu-id="65c74-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="65c74-133">UbuntuServer</span></span> |<span data-ttu-id="65c74-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="65c74-134">16.04-LTS</span></span> |<span data-ttu-id="65c74-135">mais recente</span><span class="sxs-lookup"><span data-stu-id="65c74-135">latest</span></span> |
| <span data-ttu-id="65c74-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="65c74-136">UbuntuLTS</span></span> |<span data-ttu-id="65c74-137">Canônico</span><span class="sxs-lookup"><span data-stu-id="65c74-137">Canonical</span></span> |<span data-ttu-id="65c74-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="65c74-138">UbuntuServer</span></span> |<span data-ttu-id="65c74-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="65c74-139">14.04.5-LTS</span></span> |<span data-ttu-id="65c74-140">mais recente</span><span class="sxs-lookup"><span data-stu-id="65c74-140">latest</span></span> |
| <span data-ttu-id="65c74-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="65c74-141">CoreOS</span></span> |<span data-ttu-id="65c74-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="65c74-142">CoreOS</span></span> |<span data-ttu-id="65c74-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="65c74-143">CoreOS</span></span> |<span data-ttu-id="65c74-144">Estável</span><span class="sxs-lookup"><span data-stu-id="65c74-144">Stable</span></span> |<span data-ttu-id="65c74-145">mais recente</span><span class="sxs-lookup"><span data-stu-id="65c74-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="65c74-146">Criar arquivo de configuração cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-146">Create cloud-init config file</span></span>
<span data-ttu-id="65c74-147">nuvem toosee-init em ação, crie uma VM que instala NGINX e executa um aplicativo simples do 'Hello World' Node. js.</span><span class="sxs-lookup"><span data-stu-id="65c74-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="65c74-148">Olá seguinte configuração de nuvem init instala os pacotes de saudação necessário, cria um aplicativo Node. js, em seguida, inicializar e inicia o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="65c74-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="65c74-149">No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração.</span><span class="sxs-lookup"><span data-stu-id="65c74-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="65c74-150">Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="65c74-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="65c74-151">Você pode usar qualquer editor que queira.</span><span class="sxs-lookup"><span data-stu-id="65c74-151">You can use any editor you wish.</span></span> <span data-ttu-id="65c74-152">Digite `sensible-editor cloud-init.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="65c74-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="65c74-153">Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="65c74-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="65c74-154">Para obter mais informações sobre opções de configuração de inicialização de nuvem, consulte [exemplos de configuração de inicialização de nuvem](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="65c74-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="65c74-155">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="65c74-155">Create virtual machine</span></span>
<span data-ttu-id="65c74-156">Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="65c74-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="65c74-157">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAutomate* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="65c74-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="65c74-158">Agora, crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="65c74-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="65c74-159">Saudação de uso `--custom-data` toopass de parâmetro no arquivo de configuração de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="65c74-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="65c74-160">Fornecer Olá caminho completo toohello *init.txt nuvem* configuração se você salvou o arquivo hello fora de seu diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="65c74-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="65c74-161">Olá, exemplo a seguir cria uma VM denominada *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="65c74-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="65c74-162">Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="65c74-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="65c74-163">Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="65c74-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="65c74-164">Pode ser outro alguns minutos antes de poder acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="65c74-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="65c74-165">Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="65c74-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="65c74-166">Esse endereço é usado tooaccess Olá Node. js aplicativo por meio de um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="65c74-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="65c74-167">tooallow web tooreach tráfego sua VM, abra a porta 80 da saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="65c74-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="65c74-168">Testar o aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="65c74-168">Test web app</span></span>
<span data-ttu-id="65c74-169">Agora você pode abrir um navegador da web e digite *http://<publicIpAddress>*  na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c74-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="65c74-170">Fornecer seu próprio público endereço IP da saudação VM criar processo.</span><span class="sxs-lookup"><span data-stu-id="65c74-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="65c74-171">Seu aplicativo Node. js é exibido como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="65c74-171">Your Node.js app is displayed as in hello following example:</span></span>

![Exibir o site NGINX em execução](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="65c74-173">Injetar certificados do Cofre de chave</span><span class="sxs-lookup"><span data-stu-id="65c74-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="65c74-174">Essa seção mostra como você pode armazenar certificados no cofre de chaves do Azure e colocá-los durante a saudação implantação da VM com segurança.</span><span class="sxs-lookup"><span data-stu-id="65c74-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="65c74-175">Em vez de usar uma imagem personalizada que inclui certificados Olá baked-in, esse processo garante que certificados mais recentes Olá são injetados tooa VM na primeira inicialização.</span><span class="sxs-lookup"><span data-stu-id="65c74-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="65c74-176">Durante o processo de hello, o certificado de Olá nunca deixa Olá plataforma Windows Azure ou é exposto em um modelo, histórico de linha de comando ou script.</span><span class="sxs-lookup"><span data-stu-id="65c74-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="65c74-177">O Azure Key Vault protege chaves e segredos criptográficos, como certificados ou senhas.</span><span class="sxs-lookup"><span data-stu-id="65c74-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="65c74-178">Cofre de chaves ajuda a simplificar o processo de gerenciamento de chaves hello e permite que você controle toomaintain de chaves que acessam e criptografar os dados.</span><span class="sxs-lookup"><span data-stu-id="65c74-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="65c74-179">Este cenário apresenta algumas toocreate de conceitos de Cofre de chaves e usar um certificado, embora não é uma visão geral detalhada sobre como toouse Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="65c74-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="65c74-180">Olá, as etapas a seguir mostra como você pode:</span><span class="sxs-lookup"><span data-stu-id="65c74-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="65c74-181">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="65c74-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="65c74-182">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="65c74-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="65c74-183">Criar um segredo de saudação certificado tooinject em tooa VM</span><span class="sxs-lookup"><span data-stu-id="65c74-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="65c74-184">Criar uma máquina virtual e injetar certificado Olá</span><span class="sxs-lookup"><span data-stu-id="65c74-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="65c74-185">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="65c74-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="65c74-186">Primeiro, crie um Cofre de Chaves com o [az keyvault create](/cli/azure/keyvault#create) e habilitá-lo para uso quando você implanta uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65c74-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="65c74-187">Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="65c74-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="65c74-188">Substituir *mykeyvault* em Olá exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:</span><span class="sxs-lookup"><span data-stu-id="65c74-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="65c74-189">Gerar certificado e armazenar no Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="65c74-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="65c74-190">Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="65c74-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="65c74-191">Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/keyvault/certificate#create) que usa a política de certificado saudação padrão:</span><span class="sxs-lookup"><span data-stu-id="65c74-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="65c74-192">Preparar o certificado para uso com a VM</span><span class="sxs-lookup"><span data-stu-id="65c74-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="65c74-193">certificado de saudação toouse durante a saudação VM criar processo, obter ID de saudação do seu certificado com [az keyvault secreta listar versões](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="65c74-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="65c74-194">Olá VM precisa certificado Olá em um determinado tooinject de formato-lo na inicialização, portanto converter certificado Olá com [az formato vm secreta](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="65c74-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="65c74-195">saudação de exemplo a seguir atribui saída Olá toovariables esses comandos para facilidade de uso em Olá próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="65c74-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="65c74-196">Criar a configuração de nuvem init toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="65c74-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="65c74-197">Quando você cria uma VM, certificados e chaves são armazenadas no hello protegido */var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="65c74-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="65c74-198">tooautomate adicionando Olá certificado toohello VM e configurar NGINX, você pode usar uma configuração de nuvem-init atualizado do exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c74-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="65c74-199">Crie um arquivo chamado *secured.txt de inicialização de nuvem* e colar Olá seguinte configuração.</span><span class="sxs-lookup"><span data-stu-id="65c74-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="65c74-200">Novamente, se você usar Olá Shell de nuvem, crie o arquivo de configuração de nuvem init Olá lá e não em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="65c74-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="65c74-201">Use `sensible-editor cloud-init-secured.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="65c74-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="65c74-202">Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="65c74-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="65c74-203">Criar VM segura</span><span class="sxs-lookup"><span data-stu-id="65c74-203">Create secure VM</span></span>
<span data-ttu-id="65c74-204">Agora, crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="65c74-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="65c74-205">dados de certificado de saudação são injetados do Cofre de chaves com hello `--secrets` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="65c74-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="65c74-206">Exemplo hello anterior, você também passar na configuração de nuvem init Olá com hello `--custom-data` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="65c74-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="65c74-207">Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="65c74-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="65c74-208">Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="65c74-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="65c74-209">Pode ser outro alguns minutos antes de poder acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="65c74-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="65c74-210">Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="65c74-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="65c74-211">Esse endereço é usado tooaccess Olá Node. js aplicativo por meio de um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="65c74-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="65c74-212">tooallow proteger tooreach de tráfego da web sua VM, abra a porta 443 de saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="65c74-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="65c74-213">Testar o aplicativo da Web protegido</span><span class="sxs-lookup"><span data-stu-id="65c74-213">Test secure web app</span></span>
<span data-ttu-id="65c74-214">Agora você pode abrir um navegador da web e digite *https://<publicIpAddress>*  na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c74-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="65c74-215">Fornecer seu próprio público endereço IP da saudação VM criar processo.</span><span class="sxs-lookup"><span data-stu-id="65c74-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="65c74-216">Aceite o aviso de segurança de saudação se você usou um certificado autoassinado:</span><span class="sxs-lookup"><span data-stu-id="65c74-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Aceite o aviso de segurança do navegador da web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="65c74-218">Seu site NGINX protegido e o Node. js aplicativo é exibido como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="65c74-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Exibir o site NGINX em execução](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="65c74-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65c74-220">Next steps</span></span>
<span data-ttu-id="65c74-221">Neste tutorial, você configurou as VMs na primeira inicialização com cloud-init.</span><span class="sxs-lookup"><span data-stu-id="65c74-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="65c74-222">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="65c74-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65c74-223">Criar um arquivo de configuração cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="65c74-224">Criar uma VM que usa um arquivo cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="65c74-225">Exibir um aplicativo Node. js em execução depois da saudação que VM é criada</span><span class="sxs-lookup"><span data-stu-id="65c74-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="65c74-226">Usar o Cofre de chaves toosecurely repositório de certificados</span><span class="sxs-lookup"><span data-stu-id="65c74-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="65c74-227">Automatizar implantações seguras de NGINX com cloud-init</span><span class="sxs-lookup"><span data-stu-id="65c74-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="65c74-228">Avançar toohello toolearn de tutorial Avançar como imagens VM personalizadas toocreate.</span><span class="sxs-lookup"><span data-stu-id="65c74-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65c74-229">Criar imagens de VM personalizada</span><span class="sxs-lookup"><span data-stu-id="65c74-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
