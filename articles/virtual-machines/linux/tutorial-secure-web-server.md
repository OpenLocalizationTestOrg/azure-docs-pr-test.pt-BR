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
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Proteger um servidor Web com certificados SSL em uma máquina virtual do Linux no Azure
Para proteger servidores Web, um certificado SSL (protocolo SSL) pode ser usado para criptografar o tráfego da Web. Esses certificados SSL podem ser armazenados no Azure Key Vault e permitem implantações seguras de certificados em VMs (máquinas virtuais) do Linux no Azure. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado para o Cofre da Chave
> * Criar uma VM e instalar o servidor Web NGINX
> * Inserir o certificado na VM e configurar o NGINX com uma associação de SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Visão geral
O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas. O Key Vault simplifica o processo de gerenciamento de certificados e permite que você mantenha o controle das chaves que acessam esses certificados. Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.

Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução. Esse processo garante que os certificados mais recentes sejam instalados em um servidor Web durante a implantação. Se você renova ou substitui um certificado, também não precisa criar uma nova imagem de VM personalizada. Os certificados mais recentes são inseridos automaticamente, conforme você cria outras VMs. Durante todo o processo, os certificados nunca deixam a plataforma do Azure ou são expostos em um script, no histórico da linha de comando ou no modelo.


## <a name="create-an-azure-key-vault"></a>Criar um Cofre de chaves do Azure
Antes de criar um Key Vault e os certificados, crie um grupo de recursos com [az group create](/cli/azure/group#create). O exemplo a seguir cria um grupo de recursos chamado *myResourceGroupSecureWeb* no local *eastus*:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Em seguida, crie um Key Vault com o [az keyvault create](/cli/azure/keyvault#create) e habilite-o para ser usado quando você implantar uma VM. Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas. Substitua *<mykeyvault>* no exemplo a seguir com seu próprio nome exclusivo do Key Vault:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Gerar um certificado e armazenar no Key Vault
Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/certificate#import). Para este tutorial, o exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/certificate#create) que usa a política de certificado padrão:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Preparar um certificado para usar com uma VM
Para usar o certificado durante o processo de criação de VM, obtenha a identificação do seu certificado com as [ versões secretas de az keyvault](/cli/azure/keyvault/secret#list-versions). Converter o certificado com [az vm format-secret](/cli/azure/vm#format-secret). O exemplo a seguir atribui a saída desses comandos variáveis de facilidade de uso nas próximas etapas:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a>Criar uma configuração de cloud-init para proteger o NGINX
[Inicialização de nuvem](https://cloudinit.readthedocs.io) é uma abordagem amplamente utilizada para personalizar uma VM do Linux, quando ela é inicializada pela primeira vez. Você pode utilizar a inicialização de nuvem para instalar pacotes e gravar arquivos, ou para configurar usuários e segurança. Como a inicialização de nuvem é executada durante o processo de inicialização inicial, não há etapa adicional ou agentes necessários para aplicar a configuração.

Quando você cria uma VM, certificados e chaves são armazenados no diretório protegido */var/lib/waagent/*. Para automatizar a adição do certificado à VM e configurar o servidor Web, use o cloud-init. Neste exemplo, instalamos e configuramos o servidor Web NGINX. Você pode usar o mesmo processo para instalar e configurar o Apache. 

Crie um arquivo chamado *cloud-init-web-server.txt* e cole a seguinte configuração:

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
Agora, crie uma VM com [az vm create](/cli/azure/vm#create). Os dados do certificado são injetados no cofre da chave com o `--secrets` parâmetro. Você passa a configuração cloud-init com o parâmetro `--custom-data`:

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

Demora alguns minutos para que a VM seja criada, os pacotes para instalar e iniciar o aplicativo. Quando a VM tiver sido criada, observe o `publicIpAddress` exibido pela CLI do Azure. Este endereço é usado para acessar seu site em um navegador da Web.

Para permitir o tráfego da web para acessar sua VM, abra a porta 443 da Internet com [az vm open-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a>Testar o aplicativo Web protegido
Agora, abra um navegador da Web e digite *https://<publicIpAddress>* na barra de endereços. Forneça seu próprio endereço de IP público do processo de criação da máquina virtual. Se você usou um certificado autoassinado, aceite o aviso de segurança:

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

Seu site de NGINX protegido é exibido, como no exemplo a seguir:

![Exibir o site NGINX em execução](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você protegeu um servidor Web NGINX com um certificado SSL armazenado no Azure Key Vault. Você aprendeu como:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado para o Cofre da Chave
> * Criar uma VM e instalar o servidor Web NGINX
> * Inserir o certificado na VM e configurar o NGINX com uma associação de SSL

Siga este link para ver exemplos de script de máquina virtual predefinido.

> [!div class="nextstepaction"]
> [Exemplos de script de máquina virtual do Windows](./cli-samples.md)