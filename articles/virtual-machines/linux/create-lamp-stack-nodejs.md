---
title: "aaaDeploy LÂMPADA em uma máquina virtual Linux Olá 1.0 da CLI do Azure | Microsoft Docs"
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Implantar a pilha LAMP com hello 1.0 da CLI do Azure
Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) no Azure. Você precisa de uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e hello [CLI do Azure](../../cli-install-nodejs.md) que é [conectado tooyour conta do Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [Azure CLI 1.0] – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Implantar LAMP em VM existente

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Passo a passo da implantação da LAMP em uma nova VM
Você pode começar criando um [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que irá conter Olá nova VM:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate Olá própria máquina virtual, você pode usar um modelo do Azure Resource Manager já escrito encontrado [aqui no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Você deverá ver uma resposta solicitando mais algumas entradas:

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

Agora você criou uma VM Linux com LAMP já instalada. Se desejar, você pode verificar a instalação Olá saltando para baixo demais[verificar o LAMP instalado com êxito](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Passo a passo da implantação da LAMP em uma VM existente
Se você precisar de ajuda para criar uma VM do Linux, você pode head [toolearn aqui como toocreate uma VM do Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Em seguida, você precisa tooSSH em Olá VM do Linux. Se você precisar de ajuda com a criação de uma chave SSH, você pode head [toolearn aqui como toocreate uma chave SSH no Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Se você já tiver uma chave SSH, prossiga e use o SSH na linha de comando da sua VM Linux com `ssh exampleUsername@exampleDNS`.

Agora que você estiver trabalhando em sua VM do Linux, podemos pode percorrer instalando pilha LAMP de saudação em distribuições de Debian. comandos exato Olá podem ser diferentes para outras distribuições de Linux.

#### <a name="installing-on-debianubuntu"></a>Instalação no Debian/Ubuntu
Você precisa Olá pacotes instalados a seguir: `apache2`, `mysql-server`, `php5`, e `php5-mysql`. Você pode instalar esses pacotes ao obtê-los diretamente ou usando o Tasksel. As instruções para as duas opções estão listadas abaixo.
Antes de instalar, você precisa toodownload e listas de pacote de atualização.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Pacotes individuais
Como usar apt-get:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Usando o Tasksel
Como alternativa, você pode baixar o Tasksel, uma ferramenta do Debian/Ubuntu que instala vários pacotes relacionados como uma “tarefa” coordenada em seu sistema.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Depois de executar qualquer uma das opções anteriores hello, você vai ser solicitado tooinstall esses pacotes e várias outras dependências. Pressione 'y' e 'Enter' toocontinue e execute qualquer tooset outros solicita uma senha administrativa para MySQL. Isso instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL. 

![][1]

Execute outras extensões PHP que estão disponíveis como pacotes de Olá toosee de comando a seguir:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Criar documento info.php
Você agora deve ser capaz de toocheck qual versão do PHP, MySQL e Apache ter pela linha de comando Olá digitando `apache2 -v`, `mysql -v`, ou `php -v`.

Se você como tootest ainda mais, você pode criar um tooview de página de informações rápida do PHP em um navegador. Crie um arquivo com o editor de texto Nano usando este comando:

    user@ubuntu$ sudo nano /var/www/html/info.php

No editor de texto do GNU Nano hello, adicione Olá linhas seguintes:

    <?php
    phpinfo();
    ?>

Em seguida, salve e feche o editor de texto de saudação.

Reinicie o Apache com este comando para que todas as novas instalações entrem em vigor.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Verifique se a LAMP foi instalada com êxito
Agora você pode verificar a página de informações do PHP Olá criado abrindo um navegador e indo toohttp://youruniqueDNS/info.php. Ela deve ser a imagem toothis semelhante.

![][2]

Você pode verificar a instalação do Apache exibindo saudação do Apache2 Ubuntu padrão página indo tooyou http://youruniqueDNS/. Você deverá ver algo parecido com esta imagem.

![][3]

Parabéns, você instalou uma pilha LAMP em sua VM do Azure!

## <a name="next-steps"></a>Próximas etapas
Check-out Olá Ubuntu documentação na pilha de LÂMPADA hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png