---
title: "aaaUse Olá a extensão CustomScript em uma VM do Linux | Microsoft Docs"
description: "Saiba como aplicativos de toodeploy toouse Olá CustomScript extensão em máquinas virtuais Linux no Azure criados usando o modelo de implantação clássico hello."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Implantar um aplicativo de LÂMPADA usando Olá extensão de CustomScript do Azure para Linux
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre como implantar uma pilha LAMP usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Olá extensão de CustomScript do Microsoft Azure para Linux fornece uma maneira toocustomize suas máquinas virtuais (VMs) executando código arbitrário escrito em qualquer linguagem de script hello VM (por exemplo, Python e Bash) com suporte. Isso fornece uma maneira muito flexível tooautomate máquinas de toomultiple de implantação do aplicativo.

Você pode implantar Olá extensão CustomScript usando Olá portal do Azure, do Windows PowerShell ou hello Azure Interface de linha de comando (CLI do Azure).

Neste artigo, que vamos usar Olá CLI do Azure toodeploy um tooan de aplicativo de LÂMPADA Ubuntu VM simple criado usando o modelo de implantação clássico hello.

## <a name="prerequisites"></a>Pré-requisitos
Para este exemplo, primeiro crie duas VMs do Azure executando o Ubuntu 14.04 ou posterior. Olá VMs são chamadas *script vm* e *vm de lâmpada*. Quando você criar VMs hello, use nomes exclusivos. Uma é usado toorun Olá CLI comandos e um é usado toodeploy Olá LÂMPADA aplicativo.

Você também precisa de uma conta de armazenamento do Azure e uma chave tooaccess it (você pode obter isso de saudação portal do Azure).

Se precisar de ajuda para criar VMs do Linux no Azure, consulte muito[criar uma máquina Virtual executando o Linux](createportal.md).

comandos de instalação de saudação pressupõem Ubuntu, mas você pode adaptar a instalação Olá para qualquer suporte a distribuição de Linux.

Olá script vm VM precisa toohave que CLI do Azure instalado, com um tooAzure de conexão do trabalho. Para obter ajuda sobre isso, consulte muito[instalar e configurar Olá Interface de linha de comando do Azure](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Carregar um script
Vamos usar Olá extensão CustomScript toorun um script em uma pilha de LÂMPADA Olá remota VM tooinstall e criar uma página do PHP. No script de saudação tooaccess ordem de qualquer lugar, poderá carregá-lo como um blob do Azure.

### <a name="script-overview"></a>Visão geral do script
exemplo de script Hello instala um tooUbuntu de pilha LAMP (incluindo a configuração de uma instalação silenciosa do MySQL), grava um arquivo simple do PHP e Apache é iniciado.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Carregar o script
Salve o script hello como um arquivo de texto, por exemplo *install_lamp.sh*e, em seguida, carregá-lo tooAzure armazenamento. Você pode fazer isso facilmente com o Azure CLI. Olá, exemplo a seguir carrega contêiner de armazenamento Olá arquivo tooa chamado "scripts". Se contêiner Olá não existir, será necessário toocreate-lo primeiro.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Crie também um arquivo JSON que descreve como toodownload Olá script do armazenamento do Azure. Salvar como *public_config.json* (substituindo "mystorage" com o nome de saudação da sua conta de armazenamento):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Implantar a extensão de saudação
Agora você pode usar o hello próximo comando toodeploy Olá extensão de CustomScript Linux toohello remoto VM usando Olá CLI do Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

comando anterior Olá baixa e executa Olá *install_lamp.sh* script hello VM chamada *vm de lâmpada*.

Desde que o aplicativo hello inclui um servidor web, lembre-se tooopen um HTTP de porta de escuta em Olá VM remoto com o próximo comando de saudação.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Monitoramento e solução de problemas
Você pode verificar como execuções de script personalizado Olá examinando o arquivo de log de saudação Olá VM remoto. SSH muito*vm de lâmpada* e arquivo de log final Olá com o próximo comando de saudação.

    cd /var/log/azure/customscript
    tail -f handler.log

Depois de executar Olá extensão CustomScript, você pode procurar a página do PHP toohello criado para obter informações. Olá PHP página exemplo hello neste artigo é *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Recursos adicionais
Você pode usar o mesmo toodeploy de etapas básicas de hello aplicativos mais complexos. Neste exemplo, o script de instalação Olá foi salvo como um blob público no armazenamento do Azure. Uma opção mais segura seria o script de instalação Olá toostore como um blob seguro com um [assinatura de acesso seguro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Recursos adicionais para a CLI do Azure, Linux e hello extensão CustomScript são listados a seguir.

[Automatizar tarefas de personalização de VM do Linux usando a extensão CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Extensões Linux do Azure (GitHub)](https://github.com/Azure/azure-linux-extensions)