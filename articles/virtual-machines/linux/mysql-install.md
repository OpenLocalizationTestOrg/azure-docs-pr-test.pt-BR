---
title: aaaSet o MySQL em uma VM do Linux no Azure | Microsoft Docs
description: "Saiba como tooinstall Olá MySQL de pilha em uma máquina virtual do Linux (Ubuntu ou RedHat família SO) no Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Como tooinstall MySQL no Azure
Neste artigo, você aprenderá como tooinstall e configurar o MySQL em uma máquina virtual do Azure executando o Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Instalar o MySQL em sua máquina virtual
> [!NOTE]
> Você já deve ter uma máquina virtual do Microsoft Azure executando o Linux em ordem toocomplete neste tutorial. Consulte o [tutorial de VM do Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate e configurar uma VM do Linux com `mysqlnode` como nome da VM hello e `azureuser` como usuário antes de continuar.
> 
> 

Nesse caso, use a porta de 3306 como Olá porta MySQL.  

Conecte-se toohello VM do Linux criado por meio do putty. Se esse for Olá pela primeira vez que você usar a VM do Linux do Azure, consulte como o putty toouse conectar tooa VM Linux [aqui](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Usaremos repositório pacote tooinstall MySQL5.6 como exemplo neste artigo. Na verdade, o MySQL5.6 demonstra melhoria de desempenho superior ao MySQL5.5.  Mais informações [aqui](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Como tooinstall MySQL5.6 no Ubuntu
Usaremos uma VM do Linux com o Ubuntu do Azure aqui.

* Etapa 1: Instalar o MySQL Server 5.6 alternar muito`root` usuário:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Instalar o mysql-server 5.6:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Durante a instalação, você verá um poping de janela da caixa de diálogo backup tooask você tooset MySQL senha raiz abaixo e você precisa definir Olá senha aqui.
  
    ![imagem](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Senha de entrada hello tooconfirm novamente.

    ![imagem](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Etapa 2: logon no MySQL Server
  
    Quando terminar a instalação do MySQL Server, o serviço do MySQL será iniciado automaticamente. Você pode fazer o logon no MySQL Server com o usuário `root` .
    Use Olá abaixo comando toologin e entrada de senha.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Etapa 3: Gerenciar Olá executando o serviço do MySQL
  
    (a) Obter o status do serviço MySQL
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) Iniciar o serviço MySQL
  
             #[root@mysqlnode ~]# service mysql start
  
    (b) Parar o serviço MySQL
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) reinicie o serviço do MySQL Olá
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Como tooinstall MySQL na família de sistemas operacionais do Red Hat como CentOS, Oracle Linux
Usaremos uma VM do Linux com CentOS ou Oracle Linux aqui.

* Etapa 1: Adicionar Olá MySQL Yum repositório comutador muito`root` usuário:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Baixe e instale o pacote de versão do MySQL hello:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Etapa 2: Edite abaixo repositório do arquivo tooenable Olá MySQL para baixar o pacote de MySQL5.6 hello.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Atualize cada valor de toobelow este arquivo:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Etapa 3: instale o MySQL por meio do repositório de MySQL Instalar MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    O pacote RPM MySQL e todos os pacotes relacionados serão instalados.
* Etapa 4: Gerenciar Olá executando o serviço do MySQL
  
    (a) Verifique o status do serviço de saudação do MySQL hello:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) Verifique se o saudação padrão porta do MySQL server está em execução:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) início Olá MySQL server:

           #[root@mysqlnode ~]#service mysqld start

    (d) pare Olá MySQL server:

           #[root@mysqlnode ~]#service mysqld stop

    (e) defina MySQL toostart quando a inicialização do sistema Olá para:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Como tooinstall MySQL no SUSE Linux
Usaremos a VM do Linux com OpenSUSE aqui.

* Etapa 1: baixar e instalar o MySQL Server
  
    Alternar muito`root` usuário através do comando abaixo:  
  
           #sudo su -
  
    Baixe e instale o pacote de MySQL:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Etapa 2: Gerenciar Olá executando o serviço do MySQL
  
    (a) Verifique o status de saudação do MySQL hello:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) Verifique se Olá porta padrão do MySQL hello:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) início Olá MySQL server:

           #[root@mysqlnode ~]# rcmysql start

    (d) pare Olá MySQL server:

           #[root@mysqlnode ~]# rcmysql stop

    (e) defina MySQL toostart quando a inicialização do sistema Olá para:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Próxima etapa
Encontre mais informações e uso sobre o MySQL [aqui](https://www.mysql.com/).

