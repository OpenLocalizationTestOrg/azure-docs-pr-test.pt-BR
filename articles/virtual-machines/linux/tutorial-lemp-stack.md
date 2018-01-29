---
title: "Implantar LEMP em uma máquina virtual do Linux no Azure | Microsoft Docs"
description: "Tutorial – instalar a pilha LEMP em uma VM do Linux no Azure"
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
ms.topic: tutorial
ms.date: 11/27/2017
ms.author: danlep
ms.openlocfilehash: c77cd0148a7e3e7b99e90e29bc1499dae8f95028
ms.sourcegitcommit: 651a6fa44431814a42407ef0df49ca0159db5b02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Instalar um servidor Web LEMP em uma VM do Azure
Este artigo explica como implantar um servidor Web NGINX, MySQL e PHP (a pilha LEMP) em uma VM do Ubuntu no Azure. A pilha LEMP é uma alternativa para a popular [pilha LAMP](tutorial-lamp-stack.md), que você também pode instalar no Azure. Para ver o servidor LEMP em ação, opcionalmente, você pode instalar e configurar um site de WordPress. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar uma VM Ubuntu (o "L" na pilha de LEMP)
> * Abra a porta 80 para tráfego da Web
> * Instalar NGINX, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress no servidor LEMP


Essa configuração destina-se a testes rápidos ou provas de conceito.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Instalar NGINX, MySQL e PHP

Execute o seguinte comando para atualizar as fontes de pacote do Ubuntu e instalar NGINX, MySQL e PHP. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Você será solicitado a instalar os pacotes e outras dependências. Quando solicitado, defina uma senha raiz para o MySQL e, em seguida, pressione [Enter] para continuar. Avance pelas solicitações restantes. Esse processo instala as extensões PHP mínimas obrigatórias e necessárias para usar o PHP com o MySQL. 

![Página de senha raiz do MySQL][1]

## <a name="verify-installation-and-configuration"></a>Verificar a instalação e a configuração


### <a name="nginx"></a>NGINX

Verifique a versão do NGINX com o seguinte comando:
```bash
nginx -v
```

Com o NGINX instalado e a porta 80 aberta para a sua VM, o servidor Web agora pode ser acessado através da Internet. Para exibir a página inicial do NGINX, abra um navegador da Web e digite o endereço IP público da VM. Insira o endereço IP público que você usou para o SSH para a VM:

![Página padrão do NGINX][3]


### <a name="mysql"></a>MySQL

Verifique a versão do MySQL com o seguinte comando (observe o parâmetro `V` em letra maiúscula):

```bash
mysql -V
```

Para proteger a instalação do MySQL, execute o script `mysql_secure_installation`. Se estiver configurando um servidor temporário, você poderá ignorar essa etapa. 

```bash
mysql_secure_installation
```

Digite a senha raiz do MySQL e defina as configurações de segurança do seu ambiente.

Se você quiser experimentar os recursos MySQL (criar um banco de dados MySQL, adicionar usuários ou alterar as definições de configuração), faça logon no MySQL. Esta etapa não é necessária para concluir este tutorial. 


```bash
mysql -u root -p
```

Quando terminar, saia do prompt do MySQL digitando `\q`.

### <a name="php"></a>PHP

Verifique a versão do PHP com o seguinte comando:

```bash
php -v
```

Configure o NGINX para usar o PHP FPM (Gerenciador de Processos FastCGI do PHP). Execute os seguintes comandos para fazer backup do arquivo de configuração do bloco de servidor NGINX original e, em seguida, edite o arquivo original em um editor à sua escolha:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

No editor, substitua o conteúdo de `/etc/nginx/sites-available/default` pelo seguinte. Consulte os comentários para obter explicação sobre as configurações. Substitua o endereço IP público da sua VM por *yourPublicIPAddress* e deixe as configurações restantes. Em seguida, salve o arquivo.

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

Verifique a configuração do NGINX para ver se há erros de sintaxe:

```bash
sudo nginx -t
```

Se a sintaxe estiver correta, reinicie o NGINX com o seguinte comando:

```bash
sudo service nginx restart
```

Se você deseja realizar mais testes, crie uma página de informações rápida de PHP para exibição em um navegador. O comando a seguir cria a página de informações de PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Agora você pode verificar a página de informações de PHP que você criou. Abra um navegador e acesse `http://yourPublicIPAddress/info.php`. Substitua o endereço IP público de sua VM. A página deve ser semelhante a esta imagem.

![Página de informações de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você implantou um servidor LEMP no Azure. Você aprendeu como:

> [!div class="checklist"]
> * Criar uma VM do Ubuntu
> * Abra a porta 80 para tráfego da Web
> * Instalar NGINX, MySQL e PHP
> * Verificar a instalação e a configuração
> * Instalar o WordPress na pilha LEMP

Vá para o próximo tutorial para saber como proteger servidores Web com certificados SSL.

> [!div class="nextstepaction"]
> [Proteger servidor Web com SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
