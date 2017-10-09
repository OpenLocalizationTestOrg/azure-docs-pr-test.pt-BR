---
title: "aaaDeploy LEMP em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial - pilha LEMP Olá instalar em uma VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Instalar um servidor Web LEMP em uma VM do Azure
Este artigo o orienta como toodeploy uma NGINX web server, MySQL e PHP (pilha LEMP Olá) em uma VM Ubuntu no Azure. pilha LEMP Olá é uma alternativa toohello popular [pilha LAMP](tutorial-lamp-stack.md), que você também pode instalar no Azure. servidor LEMP Olá toosee em ação, opcionalmente, você pode instalar e configurar um site de WordPress. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar uma VM Ubuntu (Olá 'L' na pilha LEMP Olá)
> * Abra a porta 80 para tráfego da Web
> * Instalar NGINX, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress no servidor LEMP Olá


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Instalar NGINX, MySQL e PHP

Execute Olá comando tooupdate Ubuntu pacote origens a seguir e instalar o PHP, MySQL e NGINX. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Você está tooinstall solicitadas Olá pacotes e outras dependências. Quando solicitado, defina uma senha de raiz para o MySQL e toocontinue [Enter]. Siga Olá restantes prompts. Esse processo instala Olá mínimo necessário PHP extensões necessário toouse PHP com o MySQL. 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificar a instalação e a configuração


### <a name="nginx"></a>NGINX

Verifique a versão de saudação do NGINX com hello comando a seguir:
```bash
nginx -v
```

Com NGINX instalado e a porta 80 abra tooyour VM, servidor de web hello agora pode ser acessado de saudação à internet. página inicial do tooview Olá NGINX, abra um navegador da web e digite o endereço IP público de saudação do hello VM. Use o endereço IP público Olá usado tooSSH toohello VM:

![Página padrão do NGINX][3]


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

Configure a saudação de toouse NGINX o Gerenciador de processo de FastCGI do PHP (PHP FPM). Execute Olá tooback servidor NGINX original de saudação bloquear o arquivo de configuração e edite o arquivo original de saudação em um editor de sua escolha de comandos a seguir:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

No editor de hello, substitua o conteúdo de saudação do `/etc/nginx/sites-available/default` com os seguintes hello. Consulte Olá comentários para obter explicação das configurações de saudação. Substitua o endereço IP público de saudação da VM para *yourPublicIPAddress*e deixe Olá restantes configurações. Salve arquivo hello.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Verifique a configuração de NGINX Olá erros de sintaxe:

```bash
sudo nginx -t
```

Se a sintaxe de saudação estiver correto, reinicie o NGINX com hello comando a seguir:

```bash
sudo service nginx restart
```

Se você quiser mais tootest, crie um tooview de página de informações rápida do PHP em um navegador. Olá comando a seguir cria uma página de informações do PHP hello:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Agora você pode verificar a página de informações do PHP Olá criado por você. Abra um navegador e vá muito`http://yourPublicIPAddress/info.php`. Substitua o endereço IP público de saudação da VM. Ela deve ser a imagem toothis semelhante.

![Página de informações de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você implantou um servidor LEMP no Azure. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM do Ubuntu
> * Abra a porta 80 para tráfego da Web
> * Instalar NGINX, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress na pilha LEMP Olá

Avançar toohello toolearn de tutorial Avançar como servidores de web toosecure com certificados SSL.

> [!div class="nextstepaction"]
> [Proteger servidor Web com SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
