---
title: aaaRun um MariaDB (MySQL) do cluster no Azure | Microsoft Docs
description: "Criar um cluster MariaDB + Galera MySQL nas Máquinas Virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="5c02f-103">Cluster MariaDB (MySQL): tutorial do Azure</span><span class="sxs-lookup"><span data-stu-id="5c02f-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5c02f-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico.</span><span class="sxs-lookup"><span data-stu-id="5c02f-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="5c02f-105">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5c02f-106">A Microsoft recomenda que mais novas implantações usam modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="5c02f-107">Cluster MariaDB Enterprise está disponível no hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5c02f-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="5c02f-108">nova oferta de saudação implantará automaticamente um cluster MariaDB Galera no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c02f-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="5c02f-109">Você deve usar a nova oferta de saudação do [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="5c02f-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="5c02f-110">Este artigo mostra como toocreate um multi-mestre de [Galera](http://galeracluster.com/products/) cluster de [MariaDBs](https://mariadb.org/en/about/) (uma substituição para soltar confiável, escalonável e robusta para MySQL) toowork em um ambiente altamente disponível no Azure máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5c02f-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="5c02f-111">Visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="5c02f-111">Architecture overview</span></span>
<span data-ttu-id="5c02f-112">Este artigo descreve como Olá toocomplete seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="5c02f-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="5c02f-113">Crie um cluster de três nós.</span><span class="sxs-lookup"><span data-stu-id="5c02f-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="5c02f-114">Discos de dados Olá separado do disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="5c02f-115">Crie discos de dados Olá configuração RAID-0/distribuídos tooincrease IOPS.</span><span class="sxs-lookup"><span data-stu-id="5c02f-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="5c02f-116">Use a carga do balanceador de carga do Azure toobalance Olá para nós de saudação três.</span><span class="sxs-lookup"><span data-stu-id="5c02f-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="5c02f-117">toominimize repetitiva de trabalho, crie uma imagem VM que contém MariaDB + Galera e usá-lo toocreate Olá outras máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="5c02f-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Arquitetura do sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="5c02f-119">Este tópico usa Olá [CLI do Azure](../../../cli-install-nodejs.md) ferramentas, então certifique-se de que toodownload-los e conectá-los em instruções de acordo toohello tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c02f-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="5c02f-120">Se você precisar de um comandos de toohello de referência disponíveis no hello CLI do Azure, consulte Olá [referência de comandos de CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5c02f-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="5c02f-121">Você também precisará de muito[criar uma chave SSH para autenticação] e anote o local do arquivo hello. PEM.</span><span class="sxs-lookup"><span data-stu-id="5c02f-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="5c02f-122">Criar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="5c02f-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="5c02f-123">Infraestrutura</span><span class="sxs-lookup"><span data-stu-id="5c02f-123">Infrastructure</span></span>
1. <span data-ttu-id="5c02f-124">Crie um grupo de afinidade toohold Olá recursos juntos.</span><span class="sxs-lookup"><span data-stu-id="5c02f-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="5c02f-125">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5c02f-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="5c02f-126">Crie um toohost de conta de armazenamento em todos os nossos discos.</span><span class="sxs-lookup"><span data-stu-id="5c02f-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="5c02f-127">Você não deve colocar mais de 40 discos muito usados em Olá mesmo tooavoid de conta de armazenamento atingir o limite de conta de armazenamento IOPS Olá 20.000.</span><span class="sxs-lookup"><span data-stu-id="5c02f-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="5c02f-128">Nesse caso, você está bem abaixo desse limite, para armazenar tudo na mesma conta para manter a simplicidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="5c02f-129">Localize o nome de saudação da imagem de máquina virtual Olá CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5c02f-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="5c02f-130">saída de Hello será algo como `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="5c02f-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="5c02f-131">Use este nome no hello etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="5c02f-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="5c02f-132">Criar modelo de VM hello e substitua /path/to/key.pem com caminho Olá onde você armazenou a chave SSH. PEM Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="5c02f-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="5c02f-133">Anexe quatro toohello de discos de dados de 500 GB VM para uso na configuração de RAID hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="5c02f-134">Usar SSH toosign toohello modelo VM que você criou no mariadbhatemplate.cloudapp.net:22 e conectar-se usando sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="5c02f-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="5c02f-135">Software</span><span class="sxs-lookup"><span data-stu-id="5c02f-135">Software</span></span>
1. <span data-ttu-id="5c02f-136">Obter a raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="5c02f-137">Instale o suporte RAID:</span><span class="sxs-lookup"><span data-stu-id="5c02f-137">Install RAID support:</span></span>

    <span data-ttu-id="5c02f-138">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-138">a.</span></span> <span data-ttu-id="5c02f-139">Instalar mdadm.</span><span class="sxs-lookup"><span data-stu-id="5c02f-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="5c02f-140">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-140">b.</span></span> <span data-ttu-id="5c02f-141">Crie a configuração de RAID0/faixa de saudação com um sistema de arquivos EXT4.</span><span class="sxs-lookup"><span data-stu-id="5c02f-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="5c02f-142">c.</span><span class="sxs-lookup"><span data-stu-id="5c02f-142">c.</span></span> <span data-ttu-id="5c02f-143">Crie diretório de ponto de montagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="5c02f-144">d.</span><span class="sxs-lookup"><span data-stu-id="5c02f-144">d.</span></span> <span data-ttu-id="5c02f-145">Recupere Olá UUID do dispositivo RAID Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="5c02f-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="5c02f-146">e.</span><span class="sxs-lookup"><span data-stu-id="5c02f-146">e.</span></span> <span data-ttu-id="5c02f-147">Edite /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="5c02f-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="5c02f-148">f.</span><span class="sxs-lookup"><span data-stu-id="5c02f-148">f.</span></span> <span data-ttu-id="5c02f-149">Adicionar automaticamente de tooenable dispositivo Olá montar na reinicialização, substituindo Olá UUID com valor de saudação obtido Olá anterior **blkid** comando.</span><span class="sxs-lookup"><span data-stu-id="5c02f-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="5c02f-150">g.</span><span class="sxs-lookup"><span data-stu-id="5c02f-150">g.</span></span> <span data-ttu-id="5c02f-151">Monte a nova partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="5c02f-152">Instale o MariaDB.</span><span class="sxs-lookup"><span data-stu-id="5c02f-152">Install MariaDB.</span></span>

    <span data-ttu-id="5c02f-153">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-153">a.</span></span> <span data-ttu-id="5c02f-154">Crie arquivo de MariaDB.repo hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="5c02f-155">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-155">b.</span></span> <span data-ttu-id="5c02f-156">Preencha o arquivo de repositório de saudação com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c02f-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="5c02f-157">c.</span><span class="sxs-lookup"><span data-stu-id="5c02f-157">c.</span></span> <span data-ttu-id="5c02f-158">tooavoid conflitos, remova o sufixo existente e bibliotecas mariadb.</span><span class="sxs-lookup"><span data-stu-id="5c02f-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="5c02f-159">d.</span><span class="sxs-lookup"><span data-stu-id="5c02f-159">d.</span></span> <span data-ttu-id="5c02f-160">Instale o MariaDB com Galera.</span><span class="sxs-lookup"><span data-stu-id="5c02f-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="5c02f-161">Mova o dispositivo de bloco Olá MySQL dados directory toohello RAID.</span><span class="sxs-lookup"><span data-stu-id="5c02f-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="5c02f-162">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-162">a.</span></span> <span data-ttu-id="5c02f-163">Copiar diretório MySQL atual de saudação para seu novo local e remover o diretório antigo hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="5c02f-164">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-164">b.</span></span> <span data-ttu-id="5c02f-165">Defina permissões para o novo diretório de saudação adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5c02f-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="5c02f-166">c.</span><span class="sxs-lookup"><span data-stu-id="5c02f-166">c.</span></span> <span data-ttu-id="5c02f-167">Crie um symlink que aponta Olá antigo toohello novo local de diretório em Olá partição RAID.</span><span class="sxs-lookup"><span data-stu-id="5c02f-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="5c02f-168">Porque [SELinux interfere com operações de cluster Olá](http://galeracluster.com/documentation-webpages/configuration.html#selinux), é necessário toodisable para Olá sessão atual.</span><span class="sxs-lookup"><span data-stu-id="5c02f-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="5c02f-169">Editar `/etc/selinux/config` toodisable para reinicializações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="5c02f-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="5c02f-170">Valide as execuções do MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c02f-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="5c02f-171">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-171">a.</span></span> <span data-ttu-id="5c02f-172">Inicie o MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c02f-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="5c02f-173">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-173">b.</span></span> <span data-ttu-id="5c02f-174">Proteger a instalação do MySQL hello, definir senha de raiz de saudação, remover usuários anônimos toodisable raiz remoto logon e remover o banco de dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="5c02f-175">c.</span><span class="sxs-lookup"><span data-stu-id="5c02f-175">c.</span></span> <span data-ttu-id="5c02f-176">Crie um usuário no banco de dados de saudação para operações de cluster e, opcionalmente, para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5c02f-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="5c02f-177">d.</span><span class="sxs-lookup"><span data-stu-id="5c02f-177">d.</span></span> <span data-ttu-id="5c02f-178">Pare o MySQL.</span><span class="sxs-lookup"><span data-stu-id="5c02f-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="5c02f-179">Crie espaço reservado para configuração.</span><span class="sxs-lookup"><span data-stu-id="5c02f-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="5c02f-180">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-180">a.</span></span> <span data-ttu-id="5c02f-181">Edite saudação MySQL configuração toocreate um espaço reservado para as configurações de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="5c02f-182">Não substitua Olá  **`<Variables>`**  ou remova-os agora.</span><span class="sxs-lookup"><span data-stu-id="5c02f-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="5c02f-183">Isso acontecerá depois de criar uma VM com base neste modelo.</span><span class="sxs-lookup"><span data-stu-id="5c02f-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="5c02f-184">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-184">b.</span></span> <span data-ttu-id="5c02f-185">Editar saudação  **[galera]**  seção e limpá-la.</span><span class="sxs-lookup"><span data-stu-id="5c02f-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="5c02f-186">c.</span><span class="sxs-lookup"><span data-stu-id="5c02f-186">c.</span></span> <span data-ttu-id="5c02f-187">Editar saudação **[mariadb]** seção.</span><span class="sxs-lookup"><span data-stu-id="5c02f-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="5c02f-188">Abrir as portas necessárias no firewall hello usando FirewallD CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5c02f-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="5c02f-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5c02f-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="5c02f-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5c02f-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="5c02f-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5c02f-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="5c02f-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="5c02f-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="5c02f-193">Recarregar Olá firewall:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="5c02f-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="5c02f-194">Otimize o sistema Olá para o desempenho.</span><span class="sxs-lookup"><span data-stu-id="5c02f-194">Optimize hello system for performance.</span></span> <span data-ttu-id="5c02f-195">Para obter mais informações, consulte [estratégia de ajuste de desempenho](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5c02f-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="5c02f-196">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-196">a.</span></span> <span data-ttu-id="5c02f-197">Edite o arquivo de configuração MySQL Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="5c02f-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="5c02f-198">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-198">b.</span></span> <span data-ttu-id="5c02f-199">Editar saudação **[mariadb]** seção e acrescente Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c02f-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c02f-200">É recomendável que innodb\_buffer\_pool_size seja 70% da memória da VM.</span><span class="sxs-lookup"><span data-stu-id="5c02f-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="5c02f-201">Neste exemplo, ele foi definido em GB 2,45 para médio Olá VM do Azure com 3,5 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="5c02f-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="5c02f-202">Parar MySQL, desabilitar o serviço MySQL seja executado na inicialização tooavoid interromper cluster Olá ao adicionar um nó e cancelar o provisionamento de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="5c02f-203">Capture Olá VM por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="5c02f-204">(Atualmente, [emitir &#1268; nas ferramentas de CLI do Azure Olá](https://github.com/Azure/azure-xplat-cli/issues/1268) descreve fatos Olá imagens capturadas por ferramentas de CLI do Azure Olá não captura Olá anexado discos de dados.)</span><span class="sxs-lookup"><span data-stu-id="5c02f-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="5c02f-205">a.</span><span class="sxs-lookup"><span data-stu-id="5c02f-205">a.</span></span> <span data-ttu-id="5c02f-206">Desligue a máquina Olá por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="5c02f-207">b.</span><span class="sxs-lookup"><span data-stu-id="5c02f-207">b.</span></span> <span data-ttu-id="5c02f-208">Clique em **capturar** e especifique o nome da imagem hello como **mariadb-galera-imagem**.</span><span class="sxs-lookup"><span data-stu-id="5c02f-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="5c02f-209">Forneça uma descrição e marque “Executei o waagent”.</span><span class="sxs-lookup"><span data-stu-id="5c02f-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Capturar a máquina virtual de saudação](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="5c02f-211">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5c02f-211">Create hello cluster</span></span>
<span data-ttu-id="5c02f-212">Crie três VMs com modelo Olá criado, configurar e iniciar o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="5c02f-213">Crie hello primeira CentOS 7 VM de saudação mariadb galera imagem imagem que você criou, fornecendo Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c02f-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="5c02f-214">Nome da rede virtual: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="5c02f-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="5c02f-215">Sub-rede: mariadb</span><span class="sxs-lookup"><span data-stu-id="5c02f-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="5c02f-216">Tamanho do computador: médio</span><span class="sxs-lookup"><span data-stu-id="5c02f-216">Machine size: medium</span></span>
 - <span data-ttu-id="5c02f-217">Nome do serviço de nuvem: mariadbha (ou qualquer nome que desejar toobe acessado por meio de mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="5c02f-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="5c02f-218">Nome do computador: mariadb1</span><span class="sxs-lookup"><span data-stu-id="5c02f-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="5c02f-219">Nome de usuário: azureuser</span><span class="sxs-lookup"><span data-stu-id="5c02f-219">Username: azureuser</span></span>
 - <span data-ttu-id="5c02f-220">Acesso SSH: habilitado</span><span class="sxs-lookup"><span data-stu-id="5c02f-220">SSH access: enabled</span></span>
 - <span data-ttu-id="5c02f-221">Passando o arquivo. PEM do hello SSH certificado e substituindo /path/to/key.pem com caminho Olá onde você armazenou Olá gerado a chave SSH. PEM.</span><span class="sxs-lookup"><span data-stu-id="5c02f-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c02f-222">Olá comandos a seguir são divididos em várias linhas para maior clareza, mas você deve inserir cada um como uma única linha.</span><span class="sxs-lookup"><span data-stu-id="5c02f-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="5c02f-223">Crie duas máquinas virtuais mais conectando-os serviços de nuvem mariadbha toohello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="5c02f-224">Alterar nome VM hello e hello porta tooa exclusiva porta SSH não em conflito com outras VMs no hello mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5c02f-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="5c02f-225">Para MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="5c02f-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="5c02f-226">Você precisará tooget Olá endereço IP interno de cada Olá três VMs para a próxima etapa do hello:</span><span class="sxs-lookup"><span data-stu-id="5c02f-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Obtendo o endereço de IP](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="5c02f-228">Use SSH toosign toohello três VMs e editar o arquivo de configuração de saudação em cada um deles.</span><span class="sxs-lookup"><span data-stu-id="5c02f-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="5c02f-229">Remova os comentários  **`wsrep_cluster_name`**  e  **`wsrep_cluster_address`**  removendo Olá  **#**  no início de saudação da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="5c02f-230">Além disso, substitua  **`<ServerIP>`**  na  **`wsrep_node_address`**  e  **`<NodeName>`**  na  **`wsrep_node_name`**  com hello IP da VM de endereço e o nome, respectivamente, remova essas linhas também.</span><span class="sxs-lookup"><span data-stu-id="5c02f-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="5c02f-231">Inicie o cluster Olá no MariaDB1 e permitem que ele seja executado na inicialização.</span><span class="sxs-lookup"><span data-stu-id="5c02f-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="5c02f-232">Inicie o MySQL em MariaDB2 e MariaDB3 e deixe-o em execução na inicialização.</span><span class="sxs-lookup"><span data-stu-id="5c02f-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="5c02f-233">Cluster de Olá balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="5c02f-233">Load balance hello cluster</span></span>
<span data-ttu-id="5c02f-234">Ao criar VMs Olá em cluster, você adicionou-los em um conjunto de disponibilidade chamado clusteravset tooensure que eles foram colocados em diferentes domínios de falha e atualização e que Azure nunca faz manutenção em todos os computadores de uma vez.</span><span class="sxs-lookup"><span data-stu-id="5c02f-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="5c02f-235">Essa configuração atende os requisitos de saudação toobe suporte Olá contrato de nível de serviço do Azure (SLA).</span><span class="sxs-lookup"><span data-stu-id="5c02f-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="5c02f-236">Agora use solicitações do balanceador de carga do Azure toobalance entre três nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c02f-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="5c02f-237">Execute Olá comandos a seguir em seu computador usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c02f-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="5c02f-238">Olá estrutura de parâmetros de comando é:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="5c02f-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="5c02f-239">Olá CLI define Olá carga balanceador investigação too15 segundos de intervalo, que podem ser um pouco longos demais.</span><span class="sxs-lookup"><span data-stu-id="5c02f-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="5c02f-240">Alterá-lo no portal de saudação em **pontos de extremidade** para qualquer uma das VMs hello.</span><span class="sxs-lookup"><span data-stu-id="5c02f-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Editar ponto de extremidade](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="5c02f-242">Selecione **Olá Reconfigure Load-Balanced definir**.</span><span class="sxs-lookup"><span data-stu-id="5c02f-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Reconfigurar Olá com balanceamento de carga conjunto](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="5c02f-244">Alterar **investigação intervalo** too5 segundos e salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="5c02f-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Alterar intervalo de investigação](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="5c02f-246">Validar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="5c02f-246">Validate hello cluster</span></span>
<span data-ttu-id="5c02f-247">Olá rígido o trabalho é realizado.</span><span class="sxs-lookup"><span data-stu-id="5c02f-247">hello hard work is done.</span></span> <span data-ttu-id="5c02f-248">Olá cluster deve ser agora podem ser acessada pela `mariadbha.cloudapp.net:3306`, que acessa o balanceador de carga hello e rotear solicitações entre Olá três VMs a maneira fácil e eficiente.</span><span class="sxs-lookup"><span data-stu-id="5c02f-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="5c02f-249">Usar seu favorito tooconnect de cliente do MySQL ou conectar-se de uma saudação VMs tooverify que esse cluster está funcionando.</span><span class="sxs-lookup"><span data-stu-id="5c02f-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="5c02f-250">Em seguida, crie um novo banco de dados e popule-o com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="5c02f-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="5c02f-251">banco de dados de saudação criado retorna Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c02f-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="5c02f-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c02f-252">Next steps</span></span>
<span data-ttu-id="5c02f-253">Neste artigo, você criou um cluster MariaDB + Galera de três nós altamente disponível nas Máquinas Virtuais do Azure que executa o CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="5c02f-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="5c02f-254">Olá VMs têm a carga balanceada com o balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c02f-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="5c02f-255">Talvez você queira toolook em [toocluster de outra maneira MySQL no Linux](mysql-cluster.md) e maneiras muito[otimizar e testar o desempenho do MySQL em VMs do Linux Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5c02f-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[criar uma chave SSH para autenticação]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
