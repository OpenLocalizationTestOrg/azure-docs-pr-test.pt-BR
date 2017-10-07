---
title: "aaaDeploy LÂMPADA em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial - pilha de LÂMPADA Olá instalar em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Instalar um servidor Web LAMP em uma VM do Azure
Este artigo o orienta como toodeploy um Apache web server, MySQL e PHP (pilha de LÂMPADA Olá) em uma VM Ubuntu no Azure. Se preferir que o servidor de web NGINX hello, consulte Olá [pilha LEMP](tutorial-lemp-stack.md) tutorial. servidor de LÂMPADA Olá toosee em ação, opcionalmente, você pode instalar e configurar um site de WordPress. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar uma VM Ubuntu (Olá 'L' na pilha de LÂMPADA Olá)
> * Abra a porta 80 para tráfego da Web
> * Instalar Apache, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress no servidor de LÂMPADA Olá


Para obter mais informações sobre a pilha de LÂMPADA hello, incluindo recomendações para um ambiente de produção, consulte Olá [Ubuntu documentação](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Instalar Apache, MySQL e PHP

Execute Olá comando tooupdate Ubuntu pacote origens a seguir e instalar o PHP, MySQL e Apache. Observe o circunflexo (^) do hello no final de saudação do comando hello.


```bash
sudo apt update && sudo apt install lamp-server^
```



Você está tooinstall solicitadas Olá pacotes e outras dependências. Quando solicitado, defina uma senha de raiz para o MySQL e toocontinue [Enter]. Siga Olá restantes prompts. Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL. 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificar a instalação e a configuração


### <a name="apache"></a>Apache

Verifique a versão de saudação do Apache com hello comando a seguir:
```bash
apache2 -v
```

Com o Apache instalado e a porta 80 abra tooyour VM, servidor de web hello agora pode ser acessado de saudação à internet. Olá tooview do Apache2 Ubuntu padrão página, abra um navegador da web e digite o endereço IP público de saudação do hello VM. Use o endereço IP público Olá usado tooSSH toohello VM:

![Página padrão do Apache][3]


### <a name="mysql"></a>MySQL

Verificar a versão de saudação do MySQL com o comando a seguir de saudação (Observe maiuscula Olá `V` parâmetro):

```bash
msql -V
```

É recomendável executar Olá após a instalação do script toohelp Olá segura do MySQL:

```bash
mysql_secure_installation
```

Digite sua senha de raiz de MySQL e definir configurações de segurança Olá para o seu ambiente.

Se você quiser toocreate um banco de dados MySQL, adicionar usuários ou alterar definições de configuração, tooMySQL de logon:

```bash
mysql -u root -p
```

Quando terminar, saia Olá mysql prompt digitando `\q`.

### <a name="php"></a>PHP

Verifique a versão de saudação do PHP com hello comando a seguir:

```bash
php -v
```

Se você quiser mais tootest, crie um tooview de página de informações rápida do PHP em um navegador. Olá comando a seguir cria uma página de informações do PHP hello:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Agora você pode verificar a página de informações do PHP Olá criado por você. Abra um navegador e vá muito`http://yourPublicIPAddress/info.php`. Substitua o endereço IP público de saudação da VM. Ela deve ser a imagem toothis semelhante.

![Página de informações de PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você implantou um servidor LAMP no Azure. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM do Ubuntu
> * Abra a porta 80 para tráfego da Web
> * Instalar Apache, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress no servidor de LÂMPADA Olá

Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.

> [!div class="nextstepaction"]
> [Proteger servidor Web com SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png