---
title: aaaClusterize MySQL com conjuntos com balanceamento de carga | Microsoft Docs
description: "Configurar uma balanceamento de carga e alta disponibilidade Linux MySQL cluster criado com o modelo de implantação clássico Olá no Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Use conjuntos com balanceamento de carga tooclusterize MySQL no Linux
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Um [modelo do Gerenciador de recursos](https://azure.microsoft.com/documentation/templates/mysql-replication/) estará disponível se você precisa toodeploy um cluster do MySQL.

Este artigo explora e ilustra Olá abordagens diferentes disponíveis toodeploy serviços altamente disponíveis com base em Linux no Microsoft Azure, exploração de alta disponibilidade do servidor MySQL como um livro de instruções. Há um vídeo ilustrando essa abordagem disponível no [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Descrevemos uma solução de alta disponibilidade do MySQL de mestre único, dois nós e sem compartilhar nada, com base em DRBD, Corosync e Pacemaker. Apenas um nó executa o MySQL por vez. Leitura e gravação da saudação recurso DRBD também são limitado tooonly um nó por vez.

Não é necessário para uma solução de VIP como LVS, porque você usará conjuntos com balanceamento de carga em recuperação normal de saudação VIP, remoção e detecção de funcionalidade e o ponto de extremidade de round-robin tooprovide Microsoft Azure. Olá VIP é um endereço IPv4 roteado globalmente atribuído pelo Microsoft Azure quando você cria o serviço de nuvem hello.

Existem outras arquiteturas possíveis para MySQL, inclusive NBD Cluster, Percona e Galera, bem como diversas soluções de middleware, incluindo pelo menos uma disponível como uma VM no [Repositório de VM](http://vmdepot.msopentech.com). Como essas soluções podem replicar unicast e multicast ou difusão e não contam com armazenamento compartilhado ou várias interfaces de rede, cenários de saudação devem ser fácil toodeploy no Microsoft Azure.

Essas arquiteturas de cluster podem ser estendidas produtos tooother como PostgreSQL e OpenLDAP de maneira semelhante. Por exemplo, esse procedimento de balanceamento de carga sem compartilhar nada foi testado com êxito com o OpenLDAP multimestres e é possível ver isso em nosso blog Channel 9.

## <a name="get-ready"></a>Prepare-se
Você precisa seguir Olá recursos e capacidades:

  - Conta de um Microsoft Azure com uma assinatura válida, toocreate capaz de pelo menos duas VMs (XS foi usado neste exemplo)
  - Uma rede e uma sub-rede
  - Um grupo de afinidades
  - Um conjunto de disponibilidade
  - Olá capacidade toocreate VHDs em Olá mesma região que o serviço de nuvem hello e anexá-los em VMs do Linux toohello

### <a name="tested-environment"></a>Ambiente testado
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync e Pacemaker

### <a name="affinity-group"></a>Grupo de afinidade
Criar um grupo de afinidade para a solução de saudação entrando no toohello portal clássico do Azure, selecionando **configurações**e criar um grupo de afinidade. Recursos alocados criados posteriormente serão atribuídos toothis grupo de afinidade.

### <a name="networks"></a>Redes
Uma nova rede é criada e uma sub-rede é criada dentro da rede de saudação. Este exemplo usa uma rede 10.10.10.0/24 com apenas uma sub-rede /24 interna.

### <a name="virtual-machines"></a>Máquinas virtuais
Olá primeira Ubuntu 13.10 VM é criada usando uma imagem da Galeria de Ubuntu Endorsed e é chamado `hadb01`. Um novo serviço de nuvem é criado no processo de hello, chamado hadb. Esse nome ilustra Olá compartilhado, a natureza de balanceamento de carga que o serviço de saudação terá quando mais recursos são adicionados. Olá criação de `hadb01` é normal e concluídas usando o portal de saudação. Um ponto de extremidade para SSH é criado automaticamente e rede nova hello está selecionada. Agora você pode criar uma conjunto de disponibilidade para Olá VMs.

Olá primeira máquina virtual é criado (tecnicamente, quando o serviço de nuvem Olá é criado), depois de criar hello segunda VM, `hadb02`. Para Olá segundo VM, use Ubuntu 13.10 VM da Galeria de saudação usando o portal de saudação, mas usar um serviço de nuvem existente, `hadb.cloudapp.net`, em vez de criar um novo. conjunto de disponibilidade e rede Olá deve ser selecionado automaticamente. Também será criado um ponto de extremidade SSH.

Depois que as duas máquinas virtuais foram criadas, tome nota da porta SSH Olá `hadb01` (TCP 22) e `hadb02` (atribuído automaticamente pelo Azure).

### <a name="attached-storage"></a>Armazenamento anexado
Anexar um novo tooboth de disco VMs e criar discos de 5 GB no processo de saudação. discos de saudação são hospedados no contêiner VHD Olá em uso para os discos do sistema operacional principal. Depois que os discos são criados e anexados, não há nenhuma necessidade toorestart Linux porque kernel Olá verá o novo dispositivo de saudação. Este dispositivo é normalmente `/dev/sdc`. Verificar `dmesg` para saída de hello.

Em cada VM, criar uma partição usando `cfdisk` (partição primária, do Linux) e gravar Olá nova tabela de partição. Não crie um sistema de arquivos nessa partição.

## <a name="set-up-hello-cluster"></a>Configurar o cluster Olá
Use APT tooinstall Corosync, Pacemaker e DRBD em ambas as VMs do Ubuntu. toodo com `apt-get`, execute hello seguinte código:

    sudo apt-get install corosync pacemaker drbd8-utils.

Não instale o MySQL neste momento. Debian e Ubuntu scripts de instalação inicializar um diretório de dados MySQL em `/var/lib/mysql`, mas como diretório hello serão ser substituído por um sistema de arquivos DRBD, é necessário tooinstall MySQL mais tarde.

Verifique se (usando `/sbin/ifconfig`) que as duas máquinas virtuais estão usando endereços na sub-rede de 10.10.10.0/24 hello e que eles podem executar ping por nome. Você também pode usar `ssh-keygen` e `ssh-copy-id` toomake-se de que as duas máquinas virtuais podem se comunicar por meio do SSH sem exigir uma senha.

### <a name="set-up-drbd"></a>Configurar DRBD
Criar um recurso DRBD que usa Olá subjacente `/dev/sdc1` partição tooproduce um `/dev/drbd1` recursos que podem ser formatados usando ext3 e usados em nós primários e secundários.

1. Abra `/etc/drbd.d/r0.res` e Olá cópia após a definição de recurso em ambas as máquinas virtuais:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Inicializar o recurso hello usando `drbdadm` em ambas as máquinas virtuais:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Em Olá VM primária (`hadb01`), forçar (primária) da propriedade de recurso DRBD hello:

        sudo drbdadm primary --force r0

Se você examinar o conteúdo de saudação do proc/drbd (`sudo cat /proc/drbd`) em ambas as VMs, você deve ver `Primary/Secondary` na `hadb01` e `Secondary/Primary` em `hadb02`, consistente com a solução de saudação neste momento. disco de 5 GB de saudação é sincronizado pela rede de 10.10.10.0/24 Olá em toocustomers sem custos.

Depois disco Olá é sincronizado, você pode criar o sistema de arquivos de saudação em `hadb01`. Para fins de teste, usamos ext2, mas Olá código a seguir cria um sistema de arquivos ext3:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Montar Olá DRBD recurso
Você está agora pronto toomount recursos DRBD Olá `hadb01`. Debian e derivativos usam `/var/lib/mysql` como diretório de dados do MySQL. Porque você não instalou o MySQL, criar diretório hello e montar Olá DRBD recurso. tooperform essa opção, execute Olá código a seguir `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Configurar MySQL
Agora você está pronto tooinstall MySQL em `hadb01`:

    sudo apt-get install mysql-server

Você tem duas opções para `hadb02`. Você pode instalar o mysql-servidor, o que criará /var/lib/mysql, preencha-o com um novo diretório de dados e, em seguida, remover o conteúdo de saudação. tooperform essa opção, execute Olá código a seguir `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

Olá segunda opção é toofailover muito`hadb02` e, em seguida, instalar o servidor mysql existe. Scripts de instalação vai notar a instalação existente do hello e não toque nele.

Execução hello seguinte código em `hadb01`:

    sudo drbdadm secondary –force r0

Execução hello seguinte código em `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Se você não planeja toofailover DRBD agora, Olá primeira opção é mais fácil, embora indiscutivelmente menos elegante. Depois de configurá-lo, você pode começar a trabalhar no banco de dados do MySQL. Execução hello seguinte código em `hadb02` (ou qualquer um dos servidores de saudação está ativo, de acordo com o tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Esta última instrução efetivamente desabilita a autenticação para o usuário raiz de saudação nesta tabela. Ela deve ser substituída pelas instruções GRANT de nível de produção e só é incluída para fins de ilustração.

Se você deseja que as consultas de toomake de VMs Olá externa (que é a finalidade deste guia Olá), também será preciso tooenable de rede para MySQL. Em ambas as VMs, abra `/etc/mysql/my.cnf` e vá muito`bind-address`. Alterar o endereço de saudação de 127.0.0.1 too0.0.0.0. Depois de salvar o arquivo hello, emitir um `sudo service mysql restart` no principal atual.

### <a name="create-hello-mysql-load-balanced-set"></a>Criar conjunto de balanceamento de carga do hello MySQL
Voltar toohello portal, vá muito`hadb01`e escolha **pontos de extremidade**. toocreate um ponto de extremidade, escolha MySQL (TCP 3306) na lista suspensa de saudação e selecione **conjunto com balanceamento de carga novo criar**. Nome hello ponto de extremidade com balanceamento de carga `lb-mysql`. Definir **tempo** too5 segundos, mínimo.

Depois de criar o ponto de extremidade hello, ir muito`hadb02`, escolha **pontos de extremidade**e criar um ponto de extremidade. Escolha `lb-mysql`e selecione MySQL na lista suspensa de saudação. Você também pode usar o hello CLI do Azure para esta etapa.

Agora você tem tudo o que é necessário para uma operação manual do cluster hello.

### <a name="test-hello-load-balanced-set"></a>Olá conjunto de balanceamento de carga de teste
É possível executar testes de um computador externo usando qualquer cliente do MySQL ou por meio de determinados aplicativos, como phpMyAdmin em execução como um site do Azure. Nesse caso, você usou a ferramenta de linha de comando do MySQL em outra caixa do Linux:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Executando failover manualmente
Você pode simular failovers desativando o MySQL, alternando o primário do DRBD e reiniciando o MySQL.

tooperform nesta tarefa, execute Olá código a seguir em hadb01:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Em seguida, em hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Depois de executar failover manualmente, você poderá repetir a consulta remota e ela deverá funcionar perfeitamente.

## <a name="set-up-corosync"></a>Configurar Corosync
Corosync é infraestrutura de cluster subjacente Olá necessária para Pacemaker toowork. De pulsação (e outras metodologias como Ultramonkey), Corosync é uma divisão de funcionalidades CRM hello, enquanto Pacemaker permanece tooHeartbeat mais semelhante na funcionalidade.

Olá principal restrição para Corosync no Azure é que Corosync prefere multicast transmissão em unicast comunicações, mas o sistema de rede do Microsoft Azure somente dá suporte a unicast.

Felizmente, o Corosync tem um modo unicast funcional. Olá única restrição real é que, como todos os nós não estão se comunicando entre si, é necessário nós de saudação toodefine nos arquivos de configuração, incluindo seus endereços IP. Podemos usar arquivos de exemplo hello Corosync para Unicast e alteração de associar o endereço, listas de nó e os diretórios de log (Ubuntu usa `/var/log/corosync` enquanto o uso de arquivos de exemplo hello `/var/log/cluster`) e habilitar as ferramentas de quorum.

> [!NOTE]
> Use os seguintes Olá `transport: udpu` diretiva e hello definidas manualmente os endereços IP para ambos os nós.

Execução hello seguinte código em `/etc/corosync/corosync.conf` para ambos os nós:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Copie esse arquivo de configuração em ambas as VMs e inicie o Corosync em ambos os nós:

    sudo service start corosync

Logo depois de iniciar o serviço hello, cluster Olá deve ser estabelecido em anel atual hello e quorum deve ser constituído. Podemos verificar essa funcionalidade por revisar os logs ou executando Olá código a seguir:

    sudo corosync-quorumtool –l

Você verá a saída toohello semelhante imagem a seguir:

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Configurando o Pacemaker
Usa pacemaker Olá toomonitor de cluster para recursos, define quando atingem primárias e alterna toosecondaries esses recursos. Os recursos podem ser definidos com base em um conjunto de scripts disponíveis ou de scripts LSB (init-like), entre outras opções.

Queremos Pacemaker muito "próprios" hello DRBD recurso, o ponto de montagem Olá e serviço do MySQL hello. Se Pacemaker pode ativar e desativar DRBD, montar e desmontar e, em seguida, iniciar e parar o MySQL no hello direita ordem quando algo ruim acontece com hello primário, a instalação for concluída.

Ao instalar o Pacemaker pela primeira vez, a configuração deve ser bem simples, algo como:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Verifique a configuração de saudação executando `sudo crm configure show`.
2. Em seguida, crie um arquivo (como `/tmp/cluster.conf`) com hello recursos a seguir:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Carregar arquivo de saudação em configuração hello. Você só precisa toodo isso em um nó.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Verifique se o Pacemaker é iniciado durante a inicialização em ambos os nós:

        sudo update-rc.d pacemaker defaults

5. Usando `sudo crm_mon –L`, verifique se um dos seus nós tornou mestre Olá para cluster hello e está executando todos os recursos de saudação. Você pode usar a montagem e ps toocheck recursos Olá em execução.

Olá captura de tela mostra a seguir `crm_mon` com um nó interrompido (saída selecionando Ctrl + C):

![crm_mon node stopped](./media/mysql-cluster/image002.png)

Essa captura de tela mostra ambos os nós, um mestre e um subordinado:

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Testando
Você está pronto para uma simulação de failover automático. Há dois toodo de maneiras isso: flexíveis e rígidos.

maneira flexível Hello usa função de desligamento do cluster Olá: ``crm_standby -U `uname -n` -v on``. Se você usar isso no mestre hello, escravo Olá assume. Lembre-se de tooset este toooff voltar. Caso contrário, o crm_mon mostrará um nó em espera.

Olá arduamente está sendo pressionada Olá VM primária (hadb01) por meio do portal de saudação ou alterando Olá runlevel em Olá VM (ou seja, interromper, desligamento). Isso ajuda a Corosync e Pacemaker por sinalização contínuo desse mestre Olá para baixo. Você pode testar isso (útil para as janelas de manutenção), mas você também pode forçar o cenário de saudação congelando Olá VM.

## <a name="stonith"></a>STONITH
Ele deve ser possível tooissue um desligamento da VM por meio de saudação CLI do Azure em vez de um script STONITH que controla um dispositivo físico. Você pode usar `/usr/lib/stonith/plugins/external/ssh` como uma base e habilitar STONITH na configuração do cluster hello. CLI do Azure deve ser instalado globalmente e configurações de publicação hello e perfil deve ser carregado para o usuário de saudação do cluster.

Exemplo de código para o recurso de saudação está disponível em [GitHub](https://github.com/bureado/aztonith). Alterar configuração do cluster Olá adicionando Olá muito a seguir`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> script Hello não executa verificações para cima/para baixo. Olá original SSH apresentava 15 verificações de ping, mas o tempo de recuperação para uma VM do Azure pode ser mais variáveis.

## <a name="limitations"></a>Limitações
Olá seguintes limitações se aplicam:

* Olá script de recurso DRBD linbit que gerencia DRBD como um recurso usa Pacemaker `drbdadm down` ao desligar um nó, mesmo se o nó de saudação será apenas no modo de espera. Isso não é ideal porque subordinado Olá não sincronizará recursos DRBD Olá enquanto mestre Olá obtém gravações. Se o mestre de saudação não falhar generosamente, escravo Olá pode assumir um estado de sistema de arquivos mais antigo. Existem duas maneiras em potencial de resolver isso:
  * Impor um `drbdadm up r0` a todos os nós de cluster por meio de um watchdog local (não clusterizado)
  * Editar script DRBD linbit hello, certificando-se de que `down` não for chamado no`/usr/lib/ocf/resource.d/linbit/drbd`
* Balanceador de carga de saudação precisa toorespond de pelo menos cinco segundos, para que os aplicativos devem estar ciente do cluster e aumentar a tolerância de tempo limite. Outras arquiteturas, como filas no aplicativo e middleware de consulta também podem ajudar.
* Ajuste do MySQL é necessário tooensure escrita feita em um ritmo gerenciável e caches são liberado toodisk com tanta frequência como toominimize possíveis perdas de memória.
* Desempenho de gravação é dependente na VM interconexão no comutador virtual Olá porque esse é o mecanismo de saudação usado por DRBD tooreplicate Olá dispositivo.
