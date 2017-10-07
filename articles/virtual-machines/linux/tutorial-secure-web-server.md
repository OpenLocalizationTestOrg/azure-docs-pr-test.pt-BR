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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Proteger um servidor Web com certificados SSL em uma máquina virtual do Linux no Azure
servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser usado tooencrypt o tráfego da web. Esses certificados SSL podem ser armazenados no cofre de chaves do Azure e permitem implantações seguras de certificados tooLinux (máquinas virtuais) no Azure. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma máquina virtual e instalar o servidor de web NGINX Olá
> * Injetar certificado Olá Olá VM e configurar NGINX com uma associação de SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Visão geral
O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas. Cofre de chaves ajuda a simplificar o processo de gerenciamento de certificado hello e permite que você controle toomaintain de chaves que acessam esses certificados. Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.

Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução. Esse processo garante que os certificados de mais atualizados de saudação são instalados em um servidor web durante a implantação. Se você renova ou substituir um certificado, você não tem também toocreate uma nova imagem VM personalizada. certificados mais recentes Olá são automaticamente inseridos ao criar VMs adicionais. Durante todo o processo Olá, certificados de saudação nunca deixam Olá plataforma Windows Azure ou são expostos em um modelo, histórico de linha de comando ou script.


## <a name="create-an-azure-key-vault"></a>Criar um Cofre de chaves do Azure
Antes de criar um Key Vault e os certificados, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupSecureWeb* em Olá *eastus* local:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Em seguida, crie um Key Vault com o [az keyvault create](/cli/azure/keyvault#create) e habilite-o para ser usado quando você implantar uma VM. Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas. Substituir  *<mykeyvault>*  em Olá exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Gerar um certificado e armazenar no Key Vault
Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/certificate#import). Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/certificate#create) que usa a política de certificado saudação padrão:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Preparar um certificado para usar com uma VM
certificado de saudação toouse durante a saudação VM criar processo, obter ID de saudação do seu certificado com [az keyvault secreta listar versões](/cli/azure/keyvault/secret#list-versions). Converter certificado Olá com [az formato vm secreta](/cli/azure/vm#format-secret). saudação de exemplo a seguir atribui saída Olá toovariables esses comandos para facilidade de uso em Olá próximas etapas:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Criar uma configuração de nuvem init toosecure NGINX
[Nuvem init](https://cloudinit.readthedocs.io) é toocustomize uma abordagem amplamente usado em uma VM do Linux conforme ele é inicializado para Olá primeira vez. Você pode usar pacotes de tooinstall init de nuvem e gravar arquivos, ou usuários tooconfigure e segurança. Como init de nuvem é executado durante o processo de inicialização hello, não há nenhuma etapa adicional ou necessários agentes tooapply sua configuração.

Quando você cria uma VM, certificados e chaves são armazenadas no hello protegido */var/lib/waagent/* directory. adicionando tooautomate Olá certificado toohello VM e configuração de servidor web hello, use init de nuvem. Neste exemplo, vamos instalar e configurar o servidor de web NGINX hello. Você pode usar o hello mesmo processo tooinstall e configurar o Apache. 

Crie um arquivo chamado *nuvem-init-web-server.txt* e colar Olá seguinte configuração:

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

### <a name="create-a-secure-vm"></a>Criar uma VM segura
Agora, crie uma VM com [az vm create](/cli/azure/vm#create). dados de certificado de saudação são injetados do Cofre de chaves com hello `--secrets` parâmetro. Você passa na configuração de nuvem init Olá com hello `--custom-data` parâmetro:

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

Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello. Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure. Este endereço é usado tooaccess seu site em um navegador da web.

tooallow proteger tooreach de tráfego da web sua VM, abra a porta 443 de saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Aplicativo de teste na web segura de Olá
Agora você pode abrir um navegador da web e digite *https://<publicIpAddress>*  na barra de endereços de saudação. Fornecer seu próprio público endereço IP da saudação VM criar processo. Aceite o aviso de segurança de saudação se você usou um certificado autoassinado:

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

Seu site NGINX protegido é exibido como Olá exemplo a seguir:

![Exibir o site NGINX em execução](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você protegeu um servidor Web NGINX com um certificado SSL armazenado no Azure Key Vault. Você aprendeu como:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma máquina virtual e instalar o servidor de web NGINX Olá
> * Injetar certificado Olá Olá VM e configurar NGINX com uma associação de SSL

Siga este toosee link pré-criadas exemplos de script da máquina virtual.

> [!div class="nextstepaction"]
> [Exemplos de script de máquina virtual do Windows](./cli-samples.md)