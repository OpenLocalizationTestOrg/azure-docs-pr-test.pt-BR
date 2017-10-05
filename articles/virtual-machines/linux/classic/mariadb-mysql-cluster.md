---
title: Executar um cluster MariaDB (MySQL) no Azure | Microsoft Docs
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
ms.openlocfilehash: 53e9bf18b26338212411ea7c4f260eb308486738
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="6a5ac-103">Cluster MariaDB (MySQL): tutorial do Azure</span><span class="sxs-lookup"><span data-stu-id="6a5ac-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6a5ac-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e Clássico.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="6a5ac-105">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-105">This article covers the classic deployment model.</span></span> <span data-ttu-id="6a5ac-106">A Microsoft recomenda que a maioria das novas implantações use o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-106">Microsoft recommends that most new deployments use the Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="6a5ac-107">O cluster MariaDB Enterprise agora está disponível no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-107">MariaDB Enterprise cluster is now available in the Azure Marketplace.</span></span> <span data-ttu-id="6a5ac-108">A nova oferta implantará automaticamente um cluster MariaDB Galera no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-108">The new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="6a5ac-109">Você deve usar a nova oferta do [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="6a5ac-109">You should use the new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="6a5ac-110">Este artigo mostra como criar um cluster [Galera](http://galeracluster.com/products/) multimestre de [MariaDBs](https://mariadb.org/en/about/), (uma substituição robusta, escalonável e confiável para o MySQL) que funciona em um ambiente altamente disponível em Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-110">This article shows you how to create a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) to work in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="6a5ac-111">Visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="6a5ac-111">Architecture overview</span></span>
<span data-ttu-id="6a5ac-112">Este artigo descreve como concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-112">This article describes how to complete the following steps:</span></span>

- <span data-ttu-id="6a5ac-113">Crie um cluster de três nós.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="6a5ac-114">Separe os discos de dados do disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-114">Separate the data disks from the OS disk.</span></span>
- <span data-ttu-id="6a5ac-115">Criar os discos de dados na configuração RAID-0/distribuído para aumentar o IOPS.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-115">Create the data disks in RAID-0/striped setting to increase IOPS.</span></span>
- <span data-ttu-id="6a5ac-116">Use o Azure Load Balancer para balancear a carga dos três nós.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-116">Use Azure Load Balancer to balance the load for the three nodes.</span></span>
- <span data-ttu-id="6a5ac-117">Para minimizar o trabalho repetitivo, crie uma imagem de VM contendo MariaDB+Galera e use-a para criar as outras VMs do cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-117">To minimize repetitive work, create a VM image that contains MariaDB + Galera and use it to create the other cluster VMs.</span></span>

![Arquitetura do sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="6a5ac-119">Este tópico usa as ferramentas da [CLI do Azure](../../../cli-install-nodejs.md), certifique-se de baixá-las e conectá-las à sua assinatura do Azure de acordo com as instruções.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-119">This topic uses the [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure to download them and connect them to your Azure subscription according to the instructions.</span></span> <span data-ttu-id="6a5ac-120">Se você precisar de uma referência aos comandos disponíveis na CLI do Azure, confira a [Referência de comando da CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6a5ac-120">If you need a reference to the commands available in the Azure CLI, see the [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="6a5ac-121">Você também precisará [criar uma chave SSH para autenticação] e anotar o local do arquivo .pem.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-121">You will also need to [create an SSH key for authentication] and make note of the .pem file location.</span></span>
>
>

## <a name="create-the-template"></a><span data-ttu-id="6a5ac-122">Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="6a5ac-122">Create the template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="6a5ac-123">Infraestrutura</span><span class="sxs-lookup"><span data-stu-id="6a5ac-123">Infrastructure</span></span>
1. <span data-ttu-id="6a5ac-124">Crie um grupo de afinidades para manter os recursos juntos.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-124">Create an affinity group to hold the resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="6a5ac-125">Crie uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="6a5ac-126">Crie uma conta de armazenamento para hospedar todos os nossos discos.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-126">Create a storage account to host all our disks.</span></span> <span data-ttu-id="6a5ac-127">Você não deve colocar mais de 40 discos muito usados na mesma conta de armazenamento para evitar atingir o limite de 20.000 IOPS da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-127">You shouldn't place more than 40 heavily used disks on the same storage account to avoid hitting the 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="6a5ac-128">Nesse caso, estamos muito abaixo desse limite, por isso vamos armazenar tudo na mesma conta por fins de simplicidade.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-128">In this case, you're well below that limit, so you'll store everything on the same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="6a5ac-129">Localize o nome da imagem da máquina virtual CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-129">Find the name of the CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="6a5ac-130">A saída será algo como `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-130">The output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="6a5ac-131">Use esse nome na etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-131">Use that name in the following step.</span></span>
5. <span data-ttu-id="6a5ac-132">Crie o modelo de VM e substitua /path/to/key.pem pelo caminho em que você armazenou a chave SSH .pem gerada.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-132">Create the VM template and replace /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="6a5ac-133">Anexe quatro discos de dados de 500 GB à VM para uso na configuração RAID.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-133">Attach four 500-GB data disks to the VM for use in the RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="6a5ac-134">Use o SSH para entrar na VM de modelo que você criou em mariadbhatemplate.cloudapp.net:22 e conecte-se usando sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-134">Use SSH to sign in to the template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="6a5ac-135">Software</span><span class="sxs-lookup"><span data-stu-id="6a5ac-135">Software</span></span>
1. <span data-ttu-id="6a5ac-136">Obtenha a raiz.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-136">Get the root.</span></span>

        sudo su

2. <span data-ttu-id="6a5ac-137">Instale o suporte RAID:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-137">Install RAID support:</span></span>

    <span data-ttu-id="6a5ac-138">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-138">a.</span></span> <span data-ttu-id="6a5ac-139">Instalar mdadm.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="6a5ac-140">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-140">b.</span></span> <span data-ttu-id="6a5ac-141">Crie a configuração RAID0/faixa com um sistema de arquivos EXT4.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-141">Create the RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="6a5ac-142">c.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-142">c.</span></span> <span data-ttu-id="6a5ac-143">Crie o diretório de ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-143">Create the mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="6a5ac-144">d.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-144">d.</span></span> <span data-ttu-id="6a5ac-145">Recupere o UUID do dispositivo RAID recém-criado.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-145">Retrieve the UUID of the newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="6a5ac-146">e.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-146">e.</span></span> <span data-ttu-id="6a5ac-147">Edite /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="6a5ac-148">f.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-148">f.</span></span> <span data-ttu-id="6a5ac-149">Adicione o dispositivo para habilitar a montagem automática na reinicialização, substituindo o UUID pelo valor obtido do comando **blkid** anterior.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-149">Add the device to enable auto mounting on reboot, replacing the UUID with the value obtained from the previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="6a5ac-150">g.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-150">g.</span></span> <span data-ttu-id="6a5ac-151">Monte a nova partição.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-151">Mount the new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="6a5ac-152">Instale o MariaDB.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-152">Install MariaDB.</span></span>

    <span data-ttu-id="6a5ac-153">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-153">a.</span></span> <span data-ttu-id="6a5ac-154">Crie o arquivo MariaDB.repo.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-154">Create the MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="6a5ac-155">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-155">b.</span></span> <span data-ttu-id="6a5ac-156">Atualize o arquivo de repositório com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-156">Fill the repo file with the following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="6a5ac-157">c.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-157">c.</span></span> <span data-ttu-id="6a5ac-158">Para evitar conflitos, remova os mariadb-libs e pós-fixados existentes.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-158">To avoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="6a5ac-159">d.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-159">d.</span></span> <span data-ttu-id="6a5ac-160">Instale o MariaDB com Galera.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="6a5ac-161">Mova o diretório de dados MySQL para o dispositivo de blocos RAID.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-161">Move the MySQL data directory to the RAID block device.</span></span>

    <span data-ttu-id="6a5ac-162">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-162">a.</span></span> <span data-ttu-id="6a5ac-163">Copie o diretório atual do MySQL para o novo local e remova o diretório antigo.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-163">Copy the current MySQL directory into its new location and remove the old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="6a5ac-164">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-164">b.</span></span> <span data-ttu-id="6a5ac-165">Defina as permissões para o novo diretório adequadamente.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-165">Set permissions for the new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="6a5ac-166">c.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-166">c.</span></span> <span data-ttu-id="6a5ac-167">Crie um symlink que aponta o diretório antigo para o novo local na partição do RAID.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-167">Create a symlink that points the old directory to the new location on the RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="6a5ac-168">Como o [SELinux interfere nas operações de cluster](http://galeracluster.com/documentation-webpages/configuration.html#selinux), é necessário desabilitá-lo para a sessão atual.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-168">Because [SELinux interferes with the cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary to disable it for the current session.</span></span> <span data-ttu-id="6a5ac-169">Edite `/etc/selinux/config` para desabilitá-lo para reinicializações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-169">Edit `/etc/selinux/config` to disable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` to set `SELINUX=permissive`
6. <span data-ttu-id="6a5ac-170">Valide as execuções do MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="6a5ac-171">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-171">a.</span></span> <span data-ttu-id="6a5ac-172">Inicie o MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="6a5ac-173">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-173">b.</span></span> <span data-ttu-id="6a5ac-174">Proteja a instalação do MySQL, defina a senha raiz, remova usuários anônimos para desabilitar o logon de raiz remoto e remova o banco de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-174">Secure the MySQL installation, set the root password, remove anonymous users to disable remote root login, and remove the test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="6a5ac-175">c.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-175">c.</span></span> <span data-ttu-id="6a5ac-176">Crie um usuário no banco de dados para as operações de cluster e, opcionalmente, para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-176">Create a user on the database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* TO 'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="6a5ac-177">d.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-177">d.</span></span> <span data-ttu-id="6a5ac-178">Pare o MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="6a5ac-179">Crie espaço reservado para configuração.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="6a5ac-180">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-180">a.</span></span> <span data-ttu-id="6a5ac-181">Edite a configuração do MySQL para criar um espaço reservado para as configurações de cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-181">Edit the MySQL configuration to create a placeholder for the cluster settings.</span></span> <span data-ttu-id="6a5ac-182">Não substitua o **`<Variables>`** nem remova as marcas de comentários agora.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-182">Do not replace the **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="6a5ac-183">Isso acontecerá depois de criar uma VM com base neste modelo.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="6a5ac-184">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-184">b.</span></span> <span data-ttu-id="6a5ac-185">Edite a seção **[galera]** e limpe-a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-185">Edit the **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="6a5ac-186">c.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-186">c.</span></span> <span data-ttu-id="6a5ac-187">Edite a seção **[mariadb]**.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-187">Edit the **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set to 0.0.0.0, the server listens to remote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for the SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set the node name of this server
8. <span data-ttu-id="6a5ac-188">Abra as portas necessárias no firewall usando FirewallD no CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-188">Open required ports on the firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="6a5ac-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="6a5ac-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="6a5ac-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="6a5ac-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="6a5ac-193">Recarregue o firewall: `firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-193">Reload the firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="6a5ac-194">Otimize o sistema para o desempenho.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-194">Optimize the system for performance.</span></span> <span data-ttu-id="6a5ac-195">Para obter mais informações, consulte [estratégia de ajuste de desempenho](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6a5ac-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="6a5ac-196">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-196">a.</span></span> <span data-ttu-id="6a5ac-197">Edite o arquivo de configuração do MySQL novamente.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-197">Edit the MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="6a5ac-198">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-198">b.</span></span> <span data-ttu-id="6a5ac-199">Edite a seção **[mariadb]** e acrescente o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-199">Edit the **[mariadb]** section and append the following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a5ac-200">É recomendável que innodb\_buffer\_pool_size seja 70% da memória da VM.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="6a5ac-201">Neste exemplo, ele foi definido como 2,45 GB para a VM do Azure média com 3,5 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-201">In this example, it has been set at 2.45 GB for the medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # The buffer pool contains buffered data and the index. This is usually set to 70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give the server more time to recycle idled connections
           innodb_file_per_table = 1 # Speed up the table space transmission and optimize the debris management performance
           innodb_log_buffer_size = 128M # The log buffer allows transactions to run without having to flush the log to disk before the transactions commit
           innodb_flush_log_at_trx_commit = 2 # The setting of 2 enables the most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="6a5ac-202">Pare o MySQL, desabilite o serviço MySQL para que não seja executado na inicialização a fim de evitar a interrupção do cluster ao adicionar um novo nó e desprovisione o computador.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-202">Stop MySQL, disable MySQL service from running on startup to avoid disrupting the cluster when adding a node, and deprovision the machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="6a5ac-203">Capture a VM por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-203">Capture the VM through the portal.</span></span> <span data-ttu-id="6a5ac-204">(Atualmente, as ferramentas do [problema #1268 na CLI do Azure](https://github.com/Azure/azure-xplat-cli/issues/1268) descrevem o fato de que as imagens capturadas pelas ferramentas da CLI do Azure não capturam os discos de dados anexados.)</span><span class="sxs-lookup"><span data-stu-id="6a5ac-204">(Currently, [issue #1268 in the Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes the fact that images captured by the Azure CLI tools do not capture the attached data disks.)</span></span>

    <span data-ttu-id="6a5ac-205">a.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-205">a.</span></span> <span data-ttu-id="6a5ac-206">Desligue o computador por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-206">Shut down the machine through the portal.</span></span>

    <span data-ttu-id="6a5ac-207">b.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-207">b.</span></span> <span data-ttu-id="6a5ac-208">Clique em **Capturar** e especifique o nome da imagem como **mariadb-galera-image**.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-208">Click **Capture** and specify the image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="6a5ac-209">Forneça uma descrição e marque “Executei o waagent”.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Capturar a máquina virtual](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-the-cluster"></a><span data-ttu-id="6a5ac-211">Criar o cluster</span><span class="sxs-lookup"><span data-stu-id="6a5ac-211">Create the cluster</span></span>
<span data-ttu-id="6a5ac-212">Crie três VMs com o modelo criado e configure e inicie o cluster.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-212">Create three VMs with the template you created, and then configure and start the cluster.</span></span>

1. <span data-ttu-id="6a5ac-213">Crie sua primeira VM do CentOS 7 da imagem mariadb-galera-image que você criou, fornecendo as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-213">Create the first CentOS 7 VM from the mariadb-galera-image image you created, providing the following information:</span></span>

 - <span data-ttu-id="6a5ac-214">Nome da rede virtual: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="6a5ac-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="6a5ac-215">Sub-rede: mariadb</span><span class="sxs-lookup"><span data-stu-id="6a5ac-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="6a5ac-216">Tamanho do computador: médio</span><span class="sxs-lookup"><span data-stu-id="6a5ac-216">Machine size: medium</span></span>
 - <span data-ttu-id="6a5ac-217">Nome do serviço de nuvem: mariadbha (ou qualquer nome que desejar para ser acessado por mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="6a5ac-217">Cloud service name: mariadbha (or whatever name you want to be accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="6a5ac-218">Nome do computador: mariadb1</span><span class="sxs-lookup"><span data-stu-id="6a5ac-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="6a5ac-219">Nome de usuário: azureuser</span><span class="sxs-lookup"><span data-stu-id="6a5ac-219">Username: azureuser</span></span>
 - <span data-ttu-id="6a5ac-220">Acesso SSH: habilitado</span><span class="sxs-lookup"><span data-stu-id="6a5ac-220">SSH access: enabled</span></span>
 - <span data-ttu-id="6a5ac-221">Passe o arquivo .pem de certificado SSH e substitua /path/to/key.pem pelo caminho em que você armazenou a chave SSH .pem gerada.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-221">Passing the SSH certificate .pem file and replacing /path/to/key.pem with the path where you stored the generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6a5ac-222">Os comandos a seguir são divididos em várias linhas para maior clareza, mas você deve inserir cada um como uma única linha.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-222">The following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="6a5ac-223">Crie duas outas máquinas virtuais conectando-as ao serviço de nuvem mariadbha.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-223">Create two more virtual machines by connecting them to the mariadbha cloud service.</span></span> <span data-ttu-id="6a5ac-224">Altere o nome da VM e a porta SSH para uma porta exclusiva que não esteja em conflito com outras VMs no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-224">Change the VM name and the SSH port to a unique port not conflicting with other VMs in the same cloud service.</span></span>

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
  <span data-ttu-id="6a5ac-225">Para MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="6a5ac-226">Você precisará obter o endereço IP interno de cada uma das três VMs para a próxima etapa:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-226">You will need to get the internal IP address of each of the three VMs for the next step:</span></span>

    ![Obtendo o endereço de IP](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="6a5ac-228">Use SSH para entrar nas três VMs e edite o arquivo de configuração em cada um delas.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-228">Use SSH to sign in to the three VMs and edit the configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="6a5ac-229">Remova as marcas de comentário **`wsrep_cluster_name`** e **`wsrep_cluster_address`** removendo o **#** no início da linha.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing the **#** at the beginning of the line.</span></span>
    <span data-ttu-id="6a5ac-230">Além disso, substitua **`<ServerIP>`** em **`wsrep_node_address`** e **`<NodeName>`** em **`wsrep_node_name`** pelo endereço IP e o nome da VM, respectivamente, removendo também as marcas de comentário nessas linhas.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with the VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="6a5ac-231">Inicie o cluster em MariaDB1 e deixe-o em execução na inicialização.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-231">Start the cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="6a5ac-232">Inicie o MySQL em MariaDB2 e MariaDB3 e deixe-o em execução na inicialização.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-the-cluster"></a><span data-ttu-id="6a5ac-233">Balancear carga do cluster</span><span class="sxs-lookup"><span data-stu-id="6a5ac-233">Load balance the cluster</span></span>
<span data-ttu-id="6a5ac-234">Ao criar as VMs clusterizadas, você as adicionou em um conjunto de disponibilidade chamado clusteravset para garantir que sejam colocadas em diferentes domínios de falha e atualização, e que o Azure nunca faça manutenção em todos as máquinas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-234">When you created the clustered VMs, you added them into an availability set called clusteravset to ensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="6a5ac-235">Essa configuração atende aos requisitos para ter suporte pelo SLA (Contrato de Nível de Serviço) do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-235">This configuration meets the requirements to be supported by the Azure service level agreement (SLA).</span></span>

<span data-ttu-id="6a5ac-236">Agora, use o Azure Load Balancer para balancear as solicitações entre os três nós.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-236">Now use Azure Load Balancer to balance requests between the three nodes.</span></span>

<span data-ttu-id="6a5ac-237">Execute os comandos a seguir no seu computador usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-237">Run the following commands on your machine by using the Azure CLI.</span></span>

<span data-ttu-id="6a5ac-238">A estrutura dos parâmetros de comando é: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="6a5ac-238">The command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="6a5ac-239">A CLI define o intervalo da investigação do balanceador de carga para 15 segundos, o que pode ser um tanto longo demais.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-239">The CLI sets the load balancer probe interval to 15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="6a5ac-240">Altere-o no portal em **Pontos de Extremidade** para qualquer uma das VMs.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-240">Change it in the portal under **Endpoints** for any of the VMs.</span></span>

![Editar ponto de extremidade](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="6a5ac-242">Selecione **Reconfigurar o conjunto de balanceamento de carga**.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-242">Select **Reconfigure the Load-Balanced Set**.</span></span>

![Reconfigurar o conjunto de balanceamento de carga](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="6a5ac-244">Altere o **Intervalo de Investigação** para 5 segundos e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-244">Change **Probe Interval** to 5 seconds and save your changes.</span></span>

![Alterar intervalo de investigação](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-the-cluster"></a><span data-ttu-id="6a5ac-246">Validar o cluster</span><span class="sxs-lookup"><span data-stu-id="6a5ac-246">Validate the cluster</span></span>
<span data-ttu-id="6a5ac-247">O trabalho pesado está feito.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-247">The hard work is done.</span></span> <span data-ttu-id="6a5ac-248">O cluster agora deve estar acessível em `mariadbha.cloudapp.net:3306`, que atinge o balanceador de carga e redireciona as solicitações entre as três VMs de forma fluente e eficaz.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-248">The cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits the load balancer and route requests between the three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="6a5ac-249">Use seu cliente MySQL favorito para conectar ou conecte-se de uma VMs para verificar se o cluster está funcionando.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-249">Use your favorite MySQL client to connect, or connect from one of the VMs to verify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="6a5ac-250">Em seguida, crie um novo banco de dados e popule-o com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="6a5ac-251">O banco de dados que você criou retorna a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a5ac-251">The database you created returns the following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6a5ac-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a5ac-252">Next steps</span></span>
<span data-ttu-id="6a5ac-253">Neste artigo, você criou um cluster MariaDB + Galera de três nós altamente disponível nas Máquinas Virtuais do Azure que executa o CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="6a5ac-254">As VMs passaram pelo balanceamento de carga com o Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6a5ac-254">The VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="6a5ac-255">Pode ser interessante ver [outra maneira de clusterizar o MySQL no Linux](mysql-cluster.md) e nas formas de [otimizar e testar o desempenho do MySQL nas VMs Linux do Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6a5ac-255">You might want to look at [another way to cluster MySQL on Linux](mysql-cluster.md) and ways to [optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating the template]:#creating-the-template
[Creating the cluster]:#creating-the-cluster
[Load balancing the cluster]:#load-balancing-the-cluster
[Validating the cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
<span data-ttu-id="6a5ac-256">[Galera]:http://galeracluster.com/products/</span><span class="sxs-lookup"><span data-stu-id="6a5ac-256">[Galera]:http://galeracluster.com/products/</span></span>
[MariaDBs]:https://mariadb.org/en/about/
<span data-ttu-id="6a5ac-257">[criar uma chave SSH para autenticação]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span><span class="sxs-lookup"><span data-stu-id="6a5ac-257">[create an SSH key for authentication]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/</span></span>
[issue #1268 in the Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
