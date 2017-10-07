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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Cluster MariaDB (MySQL): tutorial do Azure
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico. Este artigo aborda o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações usam modelo do Azure Resource Manager hello.

> [!NOTE]
> Cluster MariaDB Enterprise está disponível no hello Azure Marketplace. nova oferta de saudação implantará automaticamente um cluster MariaDB Galera no Gerenciador de recursos do Azure. Você deve usar a nova oferta de saudação do [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

Este artigo mostra como toocreate um multi-mestre de [Galera](http://galeracluster.com/products/) cluster de [MariaDBs](https://mariadb.org/en/about/) (uma substituição para soltar confiável, escalonável e robusta para MySQL) toowork em um ambiente altamente disponível no Azure máquinas virtuais.

## <a name="architecture-overview"></a>Visão geral da arquitetura
Este artigo descreve como Olá toocomplete seguindo as etapas:

- Crie um cluster de três nós.
- Discos de dados Olá separado do disco do sistema operacional hello.
- Crie discos de dados Olá configuração RAID-0/distribuídos tooincrease IOPS.
- Use a carga do balanceador de carga do Azure toobalance Olá para nós de saudação três.
- toominimize repetitiva de trabalho, crie uma imagem VM que contém MariaDB + Galera e usá-lo toocreate Olá outras máquinas virtuais do cluster.

![Arquitetura do sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> Este tópico usa Olá [CLI do Azure](../../../cli-install-nodejs.md) ferramentas, então certifique-se de que toodownload-los e conectá-los em instruções de acordo toohello tooyour assinatura do Azure. Se você precisar de um comandos de toohello de referência disponíveis no hello CLI do Azure, consulte Olá [referência de comandos de CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Você também precisará de muito[criar uma chave SSH para autenticação] e anote o local do arquivo hello. PEM.
>
>

## <a name="create-hello-template"></a>Criar modelo Olá
### <a name="infrastructure"></a>Infraestrutura
1. Crie um grupo de afinidade toohold Olá recursos juntos.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Crie uma rede virtual.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Crie um toohost de conta de armazenamento em todos os nossos discos. Você não deve colocar mais de 40 discos muito usados em Olá mesmo tooavoid de conta de armazenamento atingir o limite de conta de armazenamento IOPS Olá 20.000. Nesse caso, você está bem abaixo desse limite, para armazenar tudo na mesma conta para manter a simplicidade de saudação.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Localize o nome de saudação da imagem de máquina virtual Olá CentOS 7.

        azure vm image list | findstr CentOS
   saída de Hello será algo como `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Use este nome no hello etapa a seguir.
5. Criar modelo de VM hello e substitua /path/to/key.pem com caminho Olá onde você armazenou a chave SSH. PEM Olá gerado.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Anexe quatro toohello de discos de dados de 500 GB VM para uso na configuração de RAID hello.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Usar SSH toosign toohello modelo VM que você criou no mariadbhatemplate.cloudapp.net:22 e conectar-se usando sua chave privada.

### <a name="software"></a>Software
1. Obter a raiz de saudação.

        sudo su

2. Instale o suporte RAID:

    a. Instalar mdadm.

              yum install mdadm

    b. Crie a configuração de RAID0/faixa de saudação com um sistema de arquivos EXT4.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Crie diretório de ponto de montagem de saudação.

              mkdir /mnt/data
    d. Recupere Olá UUID do dispositivo RAID Olá recém-criado.

              blkid | grep /dev/md0
    e. Edite /etc/fstab.

              vi /etc/fstab
    f. Adicionar automaticamente de tooenable dispositivo Olá montar na reinicialização, substituindo Olá UUID com valor de saudação obtido Olá anterior **blkid** comando.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Monte a nova partição de saudação.

              mount /mnt/data

3. Instale o MariaDB.

    a. Crie arquivo de MariaDB.repo hello.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Preencha o arquivo de repositório de saudação com hello conteúdo a seguir:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid conflitos, remova o sufixo existente e bibliotecas mariadb.

           yum remove postfix mariadb-libs-*
    d. Instale o MariaDB com Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Mova o dispositivo de bloco Olá MySQL dados directory toohello RAID.

    a. Copiar diretório MySQL atual de saudação para seu novo local e remover o diretório antigo hello.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Defina permissões para o novo diretório de saudação adequadamente.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Crie um symlink que aponta Olá antigo toohello novo local de diretório em Olá partição RAID.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Porque [SELinux interfere com operações de cluster Olá](http://galeracluster.com/documentation-webpages/configuration.html#selinux), é necessário toodisable para Olá sessão atual. Editar `/etc/selinux/config` toodisable para reinicializações subsequentes.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Valide as execuções do MySQL.

   a. Inicie o MySQL.

           service mysql start
   b. Proteger a instalação do MySQL hello, definir senha de raiz de saudação, remover usuários anônimos toodisable raiz remoto logon e remover o banco de dados de teste de saudação.

           mysql_secure_installation
   c. Crie um usuário no banco de dados de saudação para operações de cluster e, opcionalmente, para seus aplicativos.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Pare o MySQL.

            service mysql stop
7. Crie espaço reservado para configuração.

   a. Edite saudação MySQL configuração toocreate um espaço reservado para as configurações de cluster de saudação. Não substitua Olá  **`<Variables>`**  ou remova-os agora. Isso acontecerá depois de criar uma VM com base neste modelo.

            vi /etc/my.cnf.d/server.cnf
   b. Editar saudação  **[galera]**  seção e limpá-la.

   c. Editar saudação **[mariadb]** seção.

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
8. Abrir as portas necessárias no firewall hello usando FirewallD CentOS 7.

   * MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Recarregar Olá firewall:`firewall-cmd --reload`

9. Otimize o sistema Olá para o desempenho. Para obter mais informações, consulte [estratégia de ajuste de desempenho](optimize-mysql.md).

   a. Edite o arquivo de configuração MySQL Olá novamente.

            vi /etc/my.cnf.d/server.cnf
   b. Editar saudação **[mariadb]** seção e acrescente Olá conteúdo a seguir:

   > [!NOTE]
   > É recomendável que innodb\_buffer\_pool_size seja 70% da memória da VM. Neste exemplo, ele foi definido em GB 2,45 para médio Olá VM do Azure com 3,5 GB de RAM.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Parar MySQL, desabilitar o serviço MySQL seja executado na inicialização tooavoid interromper cluster Olá ao adicionar um nó e cancelar o provisionamento de máquina hello.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Capture Olá VM por meio do portal hello. (Atualmente, [emitir &#1268; nas ferramentas de CLI do Azure Olá](https://github.com/Azure/azure-xplat-cli/issues/1268) descreve fatos Olá imagens capturadas por ferramentas de CLI do Azure Olá não captura Olá anexado discos de dados.)

    a. Desligue a máquina Olá por meio do portal hello.

    b. Clique em **capturar** e especifique o nome da imagem hello como **mariadb-galera-imagem**. Forneça uma descrição e marque “Executei o waagent”.
      
      ![Capturar a máquina virtual de saudação](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Criar cluster Olá
Crie três VMs com modelo Olá criado, configurar e iniciar o cluster hello.

1. Crie hello primeira CentOS 7 VM de saudação mariadb galera imagem imagem que você criou, fornecendo Olá informações a seguir:

 - Nome da rede virtual: mariadbvnet
 - Sub-rede: mariadb
 - Tamanho do computador: médio
 - Nome do serviço de nuvem: mariadbha (ou qualquer nome que desejar toobe acessado por meio de mariadbha.cloudapp.net)
 - Nome do computador: mariadb1
 - Nome de usuário: azureuser
 - Acesso SSH: habilitado
 - Passando o arquivo. PEM do hello SSH certificado e substituindo /path/to/key.pem com caminho Olá onde você armazenou Olá gerado a chave SSH. PEM.

   > [!NOTE]
   > Olá comandos a seguir são divididos em várias linhas para maior clareza, mas você deve inserir cada um como uma única linha.
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
2. Crie duas máquinas virtuais mais conectando-os serviços de nuvem mariadbha toohello. Alterar nome VM hello e hello porta tooa exclusiva porta SSH não em conflito com outras VMs no hello mesmo serviço de nuvem.

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
  Para MariaDB3:

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
3. Você precisará tooget Olá endereço IP interno de cada Olá três VMs para a próxima etapa do hello:

    ![Obtendo o endereço de IP](./media/mariadb-mysql-cluster/IP.png)
4. Use SSH toosign toohello três VMs e editar o arquivo de configuração de saudação em cada um deles.

        sudo vi /etc/my.cnf.d/server.cnf

    Remova os comentários  **`wsrep_cluster_name`**  e  **`wsrep_cluster_address`**  removendo Olá  **#**  no início de saudação da linha de saudação.
    Além disso, substitua  **`<ServerIP>`**  na  **`wsrep_node_address`**  e  **`<NodeName>`**  na  **`wsrep_node_name`**  com hello IP da VM de endereço e o nome, respectivamente, remova essas linhas também.
5. Inicie o cluster Olá no MariaDB1 e permitem que ele seja executado na inicialização.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Inicie o MySQL em MariaDB2 e MariaDB3 e deixe-o em execução na inicialização.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Cluster de Olá balanceamento de carga
Ao criar VMs Olá em cluster, você adicionou-los em um conjunto de disponibilidade chamado clusteravset tooensure que eles foram colocados em diferentes domínios de falha e atualização e que Azure nunca faz manutenção em todos os computadores de uma vez. Essa configuração atende os requisitos de saudação toobe suporte Olá contrato de nível de serviço do Azure (SLA).

Agora use solicitações do balanceador de carga do Azure toobalance entre três nós de saudação.

Execute Olá comandos a seguir em seu computador usando Olá CLI do Azure.

Olá estrutura de parâmetros de comando é:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Olá CLI define Olá carga balanceador investigação too15 segundos de intervalo, que podem ser um pouco longos demais. Alterá-lo no portal de saudação em **pontos de extremidade** para qualquer uma das VMs hello.

![Editar ponto de extremidade](./media/mariadb-mysql-cluster/Endpoint.PNG)

Selecione **Olá Reconfigure Load-Balanced definir**.

![Reconfigurar Olá com balanceamento de carga conjunto](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Alterar **investigação intervalo** too5 segundos e salvar suas alterações.

![Alterar intervalo de investigação](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Validar cluster Olá
Olá rígido o trabalho é realizado. Olá cluster deve ser agora podem ser acessada pela `mariadbha.cloudapp.net:3306`, que acessa o balanceador de carga hello e rotear solicitações entre Olá três VMs a maneira fácil e eficiente.

Usar seu favorito tooconnect de cliente do MySQL ou conectar-se de uma saudação VMs tooverify que esse cluster está funcionando.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Em seguida, crie um novo banco de dados e popule-o com alguns dados.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

banco de dados de saudação criado retorna Olá a tabela a seguir:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
Neste artigo, você criou um cluster MariaDB + Galera de três nós altamente disponível nas Máquinas Virtuais do Azure que executa o CentOS 7. Olá VMs têm a carga balanceada com o balanceador de carga do Azure.

Talvez você queira toolook em [toocluster de outra maneira MySQL no Linux](mysql-cluster.md) e maneiras muito[otimizar e testar o desempenho do MySQL em VMs do Linux Azure](optimize-mysql.md).

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
