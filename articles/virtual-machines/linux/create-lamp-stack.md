---
title: "aaaDeploy LÂMPADA em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Saiba como tooinstall Olá LÂMPADA de pilha em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Implantar pilha LAMP no Azure
Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) no Azure. Você precisa de uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Você também pode executar essas etapas com hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Resumo rápido do comando

1. Salvar e editar Olá [azuredeploy.parameters.json arquivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preferência em seu computador local.
2. Executar Olá toocreate de dois comandos a seguir em um grupo de recursos e, em seguida, implante o modelo:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Implantar LAMP em VM existente
a seguir Olá comandos pacotes de atualizações, instala o Apache, MySQL e PHP:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Passo a passo da implantação da LAMP em uma nova VM

1. Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) toocontain Olá nova VM:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate Olá própria máquina virtual, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Salvar Olá [azuredeploy.parameters.json arquivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) máquina local tooyour.
3. Editar saudação **azuredeploy.parameters.json** tooyour arquivo preferencial entradas.
4. Implantar o modelo de saudação com [implantação do grupo az criar] referência Olá baixado o arquivo json:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

saudação de saída é similar toohello exemplo a seguir:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

Agora você criou uma VM Linux com LAMP já instalada. Se desejar, você pode verificar a instalação Olá saltando para baixo demais[verificar o LAMP instalado com êxito](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Passo a passo da implantação da LAMP em uma VM existente
Se você precisar de ajuda para criar uma VM do Linux, você pode head [toolearn aqui como toocreate uma VM do Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Em seguida, você precisa tooSSH em Olá VM do Linux. Se você precisar de ajuda com a criação de uma chave SSH, você pode head [toolearn aqui como toocreate uma chave SSH no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Agora que você estiver trabalhando em sua VM do Linux, podemos pode percorrer instalando pilha LAMP de saudação em distribuições de Debian. comandos exato Olá podem ser diferentes para outras distribuições de Linux.

#### <a name="installing-on-debianubuntu"></a>Instalação no Debian/Ubuntu
Você precisa Olá pacotes instalados a seguir: `apache2`, `mysql-server`, `php5`, e `php5-mysql`. Você pode instalar esses pacotes ao obtê-los diretamente ou usando o Tasksel.
Antes de instalar, você precisa toodownload e listas de pacote de atualização.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Pacotes individuais
Como usar apt-get:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Usando o Tasksel
Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Depois de executar qualquer uma das opções anteriores hello, você vai ser solicitado tooinstall esses pacotes e várias outras dependências. tooset uma senha administrativa para MySQL, pressione 'y' e 'Enter' toocontinue e siga os outros avisos. Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL. 

![][1]

Execute outras extensões PHP que estão disponíveis como pacotes de Olá toosee de comando a seguir:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Criar documento info.php
Você agora deve ser capaz de toocheck qual versão do PHP, MySQL e Apache ter pela linha de comando Olá digitando `apache2 -v`, `mysql -v`, ou `php -v`.

Se você como tootest ainda mais, você pode criar um tooview de página de informações rápida do PHP em um navegador. Crie um arquivo com o editor de texto Nano usando este comando:

```bash
sudo nano /var/www/html/info.php
```

No editor de texto do GNU Nano hello, adicione Olá linhas seguintes:

```php
<?php
phpinfo();
?>
```

Em seguida, salve e feche o editor de texto de saudação.

Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Verifique se a LAMP foi instalada com êxito
Agora você pode verificar a página de informações do PHP Olá criado abrindo um navegador e indo toohttp://youruniqueDNS/info.php. Ela deve ser a imagem toothis semelhante.

![][2]

Você pode verificar a instalação do Apache exibindo saudação do Apache2 Ubuntu padrão página indo tooyou http://youruniqueDNS/. saudação de saída é similar toohello exemplo a seguir:

![][3]

Parabéns, você instalou uma pilha LAMP em sua VM do Azure!

## <a name="next-steps"></a>Próximas etapas
Check-out Olá Ubuntu documentação na pilha de LÂMPADA hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
