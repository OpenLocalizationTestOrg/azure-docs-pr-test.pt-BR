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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="d62c9-103">Como tooinstall MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="d62c9-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="d62c9-104">Neste artigo, você aprenderá como tooinstall e configurar o MySQL em uma máquina virtual do Azure executando o Linux.</span><span class="sxs-lookup"><span data-stu-id="d62c9-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="d62c9-105">Instalar o MySQL em sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d62c9-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="d62c9-106">Você já deve ter uma máquina virtual do Microsoft Azure executando o Linux em ordem toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d62c9-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="d62c9-107">Consulte o [tutorial de VM do Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate e configurar uma VM do Linux com `mysqlnode` como nome da VM hello e `azureuser` como usuário antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d62c9-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="d62c9-108">Nesse caso, use a porta de 3306 como Olá porta MySQL.</span><span class="sxs-lookup"><span data-stu-id="d62c9-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="d62c9-109">Conecte-se toohello VM do Linux criado por meio do putty.</span><span class="sxs-lookup"><span data-stu-id="d62c9-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="d62c9-110">Se esse for Olá pela primeira vez que você usar a VM do Linux do Azure, consulte como o putty toouse conectar tooa VM Linux [aqui](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d62c9-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d62c9-111">Usaremos repositório pacote tooinstall MySQL5.6 como exemplo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d62c9-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="d62c9-112">Na verdade, o MySQL5.6 demonstra melhoria de desempenho superior ao MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="d62c9-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="d62c9-113">Mais informações [aqui](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="d62c9-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="d62c9-114">Como tooinstall MySQL5.6 no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d62c9-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="d62c9-115">Usaremos uma VM do Linux com o Ubuntu do Azure aqui.</span><span class="sxs-lookup"><span data-stu-id="d62c9-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="d62c9-116">Etapa 1: Instalar o MySQL Server 5.6 alternar muito`root` usuário:</span><span class="sxs-lookup"><span data-stu-id="d62c9-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d62c9-117">Instalar o mysql-server 5.6:</span><span class="sxs-lookup"><span data-stu-id="d62c9-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="d62c9-118">Durante a instalação, você verá um poping de janela da caixa de diálogo backup tooask você tooset MySQL senha raiz abaixo e você precisa definir Olá senha aqui.</span><span class="sxs-lookup"><span data-stu-id="d62c9-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![imagem](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="d62c9-120">Senha de entrada hello tooconfirm novamente.</span><span class="sxs-lookup"><span data-stu-id="d62c9-120">Input hello password again tooconfirm.</span></span>

    ![imagem](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="d62c9-122">Etapa 2: logon no MySQL Server</span><span class="sxs-lookup"><span data-stu-id="d62c9-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="d62c9-123">Quando terminar a instalação do MySQL Server, o serviço do MySQL será iniciado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d62c9-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="d62c9-124">Você pode fazer o logon no MySQL Server com o usuário `root` .</span><span class="sxs-lookup"><span data-stu-id="d62c9-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="d62c9-125">Use Olá abaixo comando toologin e entrada de senha.</span><span class="sxs-lookup"><span data-stu-id="d62c9-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="d62c9-126">Etapa 3: Gerenciar Olá executando o serviço do MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d62c9-127">(a) Obter o status do serviço MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="d62c9-128">(b) Iniciar o serviço MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="d62c9-129">(b) Parar o serviço MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="d62c9-130">(d) reinicie o serviço do MySQL Olá</span><span class="sxs-lookup"><span data-stu-id="d62c9-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="d62c9-131">Como tooinstall MySQL na família de sistemas operacionais do Red Hat como CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="d62c9-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="d62c9-132">Usaremos uma VM do Linux com CentOS ou Oracle Linux aqui.</span><span class="sxs-lookup"><span data-stu-id="d62c9-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="d62c9-133">Etapa 1: Adicionar Olá MySQL Yum repositório comutador muito`root` usuário:</span><span class="sxs-lookup"><span data-stu-id="d62c9-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="d62c9-134">Baixe e instale o pacote de versão do MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="d62c9-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="d62c9-135">Etapa 2: Edite abaixo repositório do arquivo tooenable Olá MySQL para baixar o pacote de MySQL5.6 hello.</span><span class="sxs-lookup"><span data-stu-id="d62c9-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="d62c9-136">Atualize cada valor de toobelow este arquivo:</span><span class="sxs-lookup"><span data-stu-id="d62c9-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="d62c9-137">Etapa 3: instale o MySQL por meio do repositório de MySQL Instalar MySQL:</span><span class="sxs-lookup"><span data-stu-id="d62c9-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="d62c9-138">O pacote RPM MySQL e todos os pacotes relacionados serão instalados.</span><span class="sxs-lookup"><span data-stu-id="d62c9-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="d62c9-139">Etapa 4: Gerenciar Olá executando o serviço do MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d62c9-140">(a) Verifique o status do serviço de saudação do MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="d62c9-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="d62c9-141">(b) Verifique se o saudação padrão porta do MySQL server está em execução:</span><span class="sxs-lookup"><span data-stu-id="d62c9-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="d62c9-142">(c) início Olá MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d62c9-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="d62c9-143">(d) pare Olá MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d62c9-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="d62c9-144">(e) defina MySQL toostart quando a inicialização do sistema Olá para:</span><span class="sxs-lookup"><span data-stu-id="d62c9-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="d62c9-145">Como tooinstall MySQL no SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="d62c9-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="d62c9-146">Usaremos a VM do Linux com OpenSUSE aqui.</span><span class="sxs-lookup"><span data-stu-id="d62c9-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="d62c9-147">Etapa 1: baixar e instalar o MySQL Server</span><span class="sxs-lookup"><span data-stu-id="d62c9-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="d62c9-148">Alternar muito`root` usuário através do comando abaixo:</span><span class="sxs-lookup"><span data-stu-id="d62c9-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="d62c9-149">Baixe e instale o pacote de MySQL:</span><span class="sxs-lookup"><span data-stu-id="d62c9-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="d62c9-150">Etapa 2: Gerenciar Olá executando o serviço do MySQL</span><span class="sxs-lookup"><span data-stu-id="d62c9-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="d62c9-151">(a) Verifique o status de saudação do MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="d62c9-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="d62c9-152">(b) Verifique se Olá porta padrão do MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="d62c9-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="d62c9-153">(c) início Olá MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d62c9-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="d62c9-154">(d) pare Olá MySQL server:</span><span class="sxs-lookup"><span data-stu-id="d62c9-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="d62c9-155">(e) defina MySQL toostart quando a inicialização do sistema Olá para:</span><span class="sxs-lookup"><span data-stu-id="d62c9-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="d62c9-156">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d62c9-156">Next Step</span></span>
<span data-ttu-id="d62c9-157">Encontre mais informações e uso sobre o MySQL [aqui](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="d62c9-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

