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
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Como toocustomize uma máquina virtual do Linux na primeira inicialização
Um tutorial anterior, você aprendeu como tooSSH tooa VM (máquina virtual) e instale manualmente NGINX. toocreate VMs de uma maneira rápida e consistente, alguma forma de automação geralmente é desejado. Um toocustomize de abordagem comum uma VM na primeira inicialização é toouse [init nuvem](https://cloudinit.readthedocs.io). Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um arquivo de configuração cloud-init
> * Criar uma VM que usa um arquivo cloud-init
> * Exibir um aplicativo Node. js em execução depois da saudação que VM é criada
> * Usar o Cofre de chaves toosecurely repositório de certificados
> * Automatizar implantações seguras de NGINX com cloud-init


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Visão geral da inicialização de nuvem
[Nuvem init](https://cloudinit.readthedocs.io) é toocustomize uma abordagem amplamente usado em uma VM do Linux conforme ele é inicializado para Olá primeira vez. Você pode usar pacotes de tooinstall init de nuvem e gravar arquivos, ou usuários tooconfigure e segurança. Como init de nuvem é executado durante o processo de inicialização hello, não há nenhuma etapa adicional ou necessários agentes tooapply sua configuração.

A inicialização de nuvem também funciona em distribuições. Por exemplo, você não usar **apt get install** ou **yum instalar** tooinstall um pacote. Em vez disso, você pode definir uma lista de pacotes tooinstall. Init de nuvem usa automaticamente a ferramenta de gerenciamento de pacote nativo Olá para distribuição Olá que você selecionar.

Estamos trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhar com imagens Olá que eles fornecem tooAzure. Olá, a tabela a seguir descreve disponibilidade de nuvem init atual Olá nas imagens da plataforma Windows Azure:

| Alias | Editor | Oferta | SKU | Versão |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canônico |UbuntuServer |16.04-LTS |mais recente |
| UbuntuLTS |Canônico |UbuntuServer |14.04.5-LTS |mais recente |
| CoreOS |CoreOS |CoreOS |Estável |mais recente |


## <a name="create-cloud-init-config-file"></a>Criar arquivo de configuração cloud-init
nuvem toosee-init em ação, crie uma VM que instala NGINX e executa um aplicativo simples do 'Hello World' Node. js. Olá seguinte configuração de nuvem init instala os pacotes de saudação necessário, cria um aplicativo Node. js, em seguida, inicializar e inicia o aplicativo hello.

No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração. Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local. Você pode usar qualquer editor que queira. Digite `sensible-editor cloud-init.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis. Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:

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

Para obter mais informações sobre opções de configuração de inicialização de nuvem, consulte [exemplos de configuração de inicialização de nuvem](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Criar máquina virtual
Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAutomate* em Olá *eastus* local:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Agora, crie uma VM com [az vm create](/cli/azure/vm#create). Saudação de uso `--custom-data` toopass de parâmetro no arquivo de configuração de inicialização de nuvem. Fornecer Olá caminho completo toohello *init.txt nuvem* configuração se você salvou o arquivo hello fora de seu diretório de trabalho atual. Olá, exemplo a seguir cria uma VM denominada *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello. Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt. Pode ser outro alguns minutos antes de poder acessar o aplicativo hello. Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure. Esse endereço é usado tooaccess Olá Node. js aplicativo por meio de um navegador da web.

tooallow web tooreach tráfego sua VM, abra a porta 80 da saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Testar o aplicativo da web
Agora você pode abrir um navegador da web e digite *http://<publicIpAddress>*  na barra de endereços de saudação. Fornecer seu próprio público endereço IP da saudação VM criar processo. Seu aplicativo Node. js é exibido como Olá exemplo a seguir:

![Exibir o site NGINX em execução](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Injetar certificados do Cofre de chave
Essa seção mostra como você pode armazenar certificados no cofre de chaves do Azure e colocá-los durante a saudação implantação da VM com segurança. Em vez de usar uma imagem personalizada que inclui certificados Olá baked-in, esse processo garante que certificados mais recentes Olá são injetados tooa VM na primeira inicialização. Durante o processo de hello, o certificado de Olá nunca deixa Olá plataforma Windows Azure ou é exposto em um modelo, histórico de linha de comando ou script.

O Azure Key Vault protege chaves e segredos criptográficos, como certificados ou senhas. Cofre de chaves ajuda a simplificar o processo de gerenciamento de chaves hello e permite que você controle toomaintain de chaves que acessam e criptografar os dados. Este cenário apresenta algumas toocreate de conceitos de Cofre de chaves e usar um certificado, embora não é uma visão geral detalhada sobre como toouse Cofre de chaves.

Olá, as etapas a seguir mostra como você pode:

- Criar um Cofre de chaves do Azure
- Gerar ou carregar um certificado toohello Cofre de chaves
- Criar um segredo de saudação certificado tooinject em tooa VM
- Criar uma máquina virtual e injetar certificado Olá

### <a name="create-an-azure-key-vault"></a>Criar um Cofre de chaves do Azure
Primeiro, crie um Cofre de Chaves com o [az keyvault create](/cli/azure/keyvault#create) e habilitá-lo para uso quando você implanta uma máquina virtual. Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas. Substituir *mykeyvault* em Olá exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Gerar certificado e armazenar no Cofre da Chave
Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com o [az keyvault certificate import](/cli/azure/keyvault/certificate#import). Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [criar certificado de keyvault az](/cli/azure/keyvault/certificate#create) que usa a política de certificado saudação padrão:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Preparar o certificado para uso com a VM
certificado de saudação toouse durante a saudação VM criar processo, obter ID de saudação do seu certificado com [az keyvault secreta listar versões](/cli/azure/keyvault/secret#list-versions). Olá VM precisa certificado Olá em um determinado tooinject de formato-lo na inicialização, portanto converter certificado Olá com [az formato vm secreta](/cli/azure/vm#format-secret). saudação de exemplo a seguir atribui saída Olá toovariables esses comandos para facilidade de uso em Olá próximas etapas:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Criar a configuração de nuvem init toosecure NGINX
Quando você cria uma VM, certificados e chaves são armazenadas no hello protegido */var/lib/waagent/* directory. tooautomate adicionando Olá certificado toohello VM e configurar NGINX, você pode usar uma configuração de nuvem-init atualizado do exemplo anterior de saudação.

Crie um arquivo chamado *secured.txt de inicialização de nuvem* e colar Olá seguinte configuração. Novamente, se você usar Olá Shell de nuvem, crie o arquivo de configuração de nuvem init Olá lá e não em seu computador local. Use `sensible-editor cloud-init-secured.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis. Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:

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

### <a name="create-secure-vm"></a>Criar VM segura
Agora, crie uma VM com [az vm create](/cli/azure/vm#create). dados de certificado de saudação são injetados do Cofre de chaves com hello `--secrets` parâmetro. Exemplo hello anterior, você também passar na configuração de nuvem init Olá com hello `--custom-data` parâmetro:

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

Leva alguns minutos para Olá VM toobe criado, Olá pacotes tooinstall e toostart de aplicativo hello. Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt. Pode ser outro alguns minutos antes de poder acessar o aplicativo hello. Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure. Esse endereço é usado tooaccess Olá Node. js aplicativo por meio de um navegador da web.

tooallow proteger tooreach de tráfego da web sua VM, abra a porta 443 de saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Testar o aplicativo da Web protegido
Agora você pode abrir um navegador da web e digite *https://<publicIpAddress>*  na barra de endereços de saudação. Fornecer seu próprio público endereço IP da saudação VM criar processo. Aceite o aviso de segurança de saudação se você usou um certificado autoassinado:

![Aceite o aviso de segurança do navegador da web](./media/tutorial-automate-vm-deployment/browser-warning.png)

Seu site NGINX protegido e o Node. js aplicativo é exibido como Olá exemplo a seguir:

![Exibir o site NGINX em execução](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você configurou as VMs na primeira inicialização com cloud-init. Você aprendeu como:

> [!div class="checklist"]
> * Criar um arquivo de configuração cloud-init
> * Criar uma VM que usa um arquivo cloud-init
> * Exibir um aplicativo Node. js em execução depois da saudação que VM é criada
> * Usar o Cofre de chaves toosecurely repositório de certificados
> * Automatizar implantações seguras de NGINX com cloud-init

Avançar toohello toolearn de tutorial Avançar como imagens VM personalizadas toocreate.

> [!div class="nextstepaction"]
> [Criar imagens de VM personalizada](./tutorial-custom-images.md)
