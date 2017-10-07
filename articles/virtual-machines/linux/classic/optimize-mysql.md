---
title: aaaOptimize desempenho do MySQL no Linux | Microsoft Docs
description: "Saiba como toooptimize MySQL em execução em uma máquina virtual do Azure (VM) executando o Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Otimizar o desempenho do MySQL em VMs Linux do Azure
Há muitos fatores que afetam o desempenho do MySQL no Azure, tanto na configuração de software como na seleção de hardware virtual. Este artigo se concentra na otimização de desempenho por meio de armazenamento, sistema e configurações de banco de dados.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre as otimizações de VM do Linux com o modelo do Gerenciador de recursos de hello, consulte [otimizar sua VM do Linux no Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Utilizar RAID em uma máquina virtual do Azure
O armazenamento é um fator-chave Olá que afeta o desempenho do banco de dados em ambientes de nuvem. Tooa em comparação com o único disco, RAID pode fornecer acesso mais rápido por meio de simultaneidade. Para obter mais informações, consulte [Níveis de RAID padrão](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

A taxa de transferência de E/S de disco e o tempo de resposta de E/S no Azure podem ser melhorados significativamente com o RAID. Nossos testes de laboratório mostram que a taxa de transferência de e/s de disco pode ser duplicada e tempo de resposta de e/s pode ser reduzido pela metade em média quando o número de saudação de discos RAID é duplicado (de toofour duas, quatro tooeight, etc.). Confira o [Apêndice A](#AppendixA) para obter detalhes.  

Além de e/s toodisk, desempenho do MySQL melhora quando você aumenta o nível de RAID de saudação.  Confira o [Apêndice B](#AppendixB) para obter detalhes.  

Você também poderá tamanho da parte tooconsider hello. Em geral, quando você tem um grande parte, haverá uma sobrecarga mais baixa, especialmente para grandes gravações. No entanto, quando o tamanho da parte Olá é muito grande, pode adicionar uma sobrecarga adicional que impede que você aproveite o RAID. tamanho padrão atual de saudação é 512 KB, que é aprovada toobe ideal para ambientes de produção mais gerais. Confira o [Apêndice C](#AppendixC) para obter detalhes.   

Há limites para quantos discos você pode adicionar para diferentes tipos de máquinas virtuais. Esses limites são detalhados em [Tamanhos de máquinas virtuais e serviço de nuvem para o Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Você precisará de quatro dados anexados discos toofollow Olá RAID exemplos neste artigo, embora você possa escolher tooset RAID com menos discos.  

Este artigo pressupõe que você já criou uma máquina virtual Linux e já tenha o MYSQL instalado e configurado. Para obter mais informações sobre como começar, consulte como tooinstall MySQL no Azure.  

### <a name="set-up-raid-on-azure"></a>Configurar o RAID no Azure
Olá etapas a seguir mostram como toocreate RAID no Azure usando Olá portal do Azure. Você também pode configurar o RAID usando scripts do Windows PowerShell.
Neste exemplo, configuraremos o RAID 0 com quatro discos.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Adicionar uma máquina virtual de tooyour de disco de dados
No hello portal do Azure, vá toohello painel e selecione Olá toowhich de máquina virtual você deseja tooadd um disco de dados. Neste exemplo, a máquina virtual de saudação é mysqlnode1.  

<!--![Virtual machines][1]-->

Clique em **Discos** e depois em **Anexar Novo**.

![Máquinas virtuais - adicionar disco](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Crie um novo disco de 500 GB. Verifique se **preferência de Cache do Host** está definido muito**nenhum**.  Quando tiver terminado, clique em **OK**.

![Anexar disco vazio](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Isso adiciona um disco vazio à sua máquina virtual. Repita essa etapa mais três vezes para que você tenha quatro discos de dados para o RAID.  

Você pode ver Olá adicionado unidades na máquina virtual de saudação examinando o log de mensagens do kernel hello. Por exemplo, toosee isso no Ubuntu, use Olá comando a seguir:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Criar RAID com hello discos adicionais
Olá etapas a seguir descrevem como muito[configurar software RAID no Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Se você estiver usando o sistema de arquivos XFS hello, execute Olá etapas a seguir depois que você criou RAID.
>
>

tooinstall XFS no Debian, Ubuntu ou Menta Linux, Olá use comandos a seguir:  

    apt-get -y install xfsprogs  

tooinstall XFS em Fedora, CentOS ou RHEL, Olá use comandos a seguir:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Configurar um novo caminho de armazenamento
Use Olá comando tooset um novo caminho de armazenamento a seguir:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Copiar Olá original dados toohello novo caminho de armazenamento
Use Olá comando toocopy dados toohello novo caminho de armazenamento a seguir:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Modificar permissões para que possa acessar MySQL (leitura e gravação) em disco de dados Olá
Olá Use as seguintes permissões de toomodify de comando:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Olá e/s disco agendando o algoritmo de ajuste
O Linux implementa quatro tipos de algoritmos de agendamento de e/s:  

* Algoritmo NOOP (nenhuma operação)
* Algoritmo de prazo (prazo)
* Algoritmo de fila completamente justa (CFQ)
* Algoritmo de período de orçamento (antecipado)  

Você pode selecionar diferentes agendadores de e/s em desempenho de toooptimize cenários diferentes. Em um ambiente de acesso aleatório completamente, não há uma diferença significativa entre hello CFQ e algoritmos de prazo para o desempenho. É recomendável que você defina tooDeadline de ambiente de banco de dados Olá MySQL para estabilidade. Se houver muita E/S sequencial, o CFQ poderá reduzir o desempenho de E/S do disco.   

Para SSD e outros equipamentos, NOOP ou prazo pode alcançar desempenho melhor do que o Agendador de saudação padrão.   

Toohello anterior kernel 2.5, Olá padrão e/s agendamento algoritmo é prazo. A partir do kernel Olá 2.6.18, CFQ se tornou algoritmo de programação saudação padrão e/s.  Você pode especificar essa configuração no momento da inicialização do kernel ou dinamicamente modificar essa configuração quando o sistema hello está sendo executado.  

saudação de exemplo a seguir demonstra como toocheck e defina Olá algoritmo do padrão Agendador toohello NOOP na família de distribuição Debian hello.  

### <a name="view-hello-current-io-scheduler"></a>Agendador do modo de exibição Olá atual e/s
tooview Olá Olá de Agendador executar comando a seguir:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Você verá a seguinte saída, que indica o Agendador de saudação atual:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Alterar Olá dispositivo (dev/sda) atual do algoritmo de programação hello e/s
Execute Olá dispositivo atual de saudação de toochange de comandos a seguir:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Configurar este somente para /dev/sda não é útil. Ele deve ser definido em todos os discos de dados onde reside o banco de dados de saudação.  
>
>

Você deve ver Olá saída a seguir, indicando que grub.cfg foi recriado com êxito e que o Agendador de saudação padrão tiver sido atualizada tooNOOP:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Para Olá família de distribuição do Red Hat, você só precisa Olá comando a seguir:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Definir as configurações de operações de arquivos do sistema
Uma prática recomendada é Olá toodisable *atime* recurso de log no sistema de arquivo hello. Atime é o último tempo de acesso de arquivo hello. Sempre que um arquivo é acessado, registros de sistema de arquivo Olá Olá carimbo de hora no log de saudação. No entanto, essas informações raramente são usadas. Você pode desabilitá-lo se não precisar dele, o que reduzirá o tempo de acesso total do disco.  

toodisable atime log, você precisa toomodify Olá arquivo sistema configuração arquivo /etc/ fstab e adicionar Olá **noatime** opção.  

Por exemplo, edite o arquivo de /etc/fstab de vim do hello, adicionando noatime hello, conforme mostrado no hello exemplo a seguir:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Em seguida, remonte o sistema de arquivos de saudação com hello comando a seguir:  

    mount -o remount /RAID0

Saudação de teste modificado resultado. Quando você modifica o arquivo de teste hello, tempo de acesso de saudação não é atualizado. Olá seguintes exemplos mostram quais código Olá aparência antes e depois da modificação.

Antes:        

![Código antes da modificação de acesso][5]

Depois:

![Código depois da modificação de acesso][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Aumentar o número máximo de saudação de identificadores do sistema de alta simultaneidade
O MySQL é um banco de dados de alta simultaneidade. número de identificadores simultâneas do Hello padrão é 1024 para Linux, que sempre não é suficiente. Use Olá seguindo as etapas tooincrease Olá máximo simultâneas identificadores de simultaneidade alta de toosupport do sistema de saudação do MySQL.

### <a name="modify-hello-limitsconf-file"></a>Modificar o arquivo de limits.conf Olá
tooincrease Olá máximo permitido identificadores simultâneas, adicione Olá quatro linhas no arquivo de /etc/security/limits.conf Olá a seguir. Observe que 65536 é o número máximo de saudação que pode dar suporte a sistema de saudação.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Atualizar sistema Olá para novos limites de saudação
sistema tooupdate hello, executar Olá comandos a seguir:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Certifique-se de que os limites de saudação são atualizados no momento da inicialização
Coloque Olá comandos de inicialização no arquivo de /etc/rc.local Olá a seguir para que ele entrará em vigor no momento da inicialização.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Otimização de banco de dados do MySQL
tooconfigure MySQL no Azure, você pode usar Olá a mesma estratégia de ajuste de desempenho você pode usar em uma máquina local.  

Olá principais regras de otimização de e/s são:   

* Aumente o tamanho do cache de saudação.
* Reduza o tempo de resposta de E/S.  

configurações do servidor MySQL toooptimize, você pode atualizar o arquivo my.cnf hello, o que é o arquivo de configuração saudação padrão para computadores cliente e servidor.  

Olá seguintes itens de configuração são fatores principais de saudação que afetam o desempenho do MySQL:  

* **innodb_buffer_pool_size**: pool de buffers Olá contém dados armazenados em buffer e o índice de saudação. Isso geralmente é definido too70% da memória física.
* **innodb_log_file_size**: Este é o tamanho do log de refazer hello. Use o tooensure de logs de refazer que operações de gravação são rápida, confiável e recuperável após uma falha. Isso é definido too512 MB, o que lhe dará bastante espaço para log de operações de gravação.
* **max_connections**: às vezes, os aplicativos não fecham as conexões corretamente. Um valor maior dará servidor hello mais tempo toorecycle ociosos conexões. Olá o número máximo de conexões é 10.000, mas Olá recomendado máximo é 5.000.
* **Innodb_file_per_table**: essa configuração habilita ou desabilita a capacidade de saudação de InnoDB toostore tabelas em arquivos separados. Ative Olá opção tooensure que várias operações de administração avançados podem ser aplicadas com eficiência. De um ponto de vista de desempenho, ele pode acelerar a transmissão de espaço de tabela hello e otimizar o desempenho de gerenciamento de resíduos hello. Olá recomendado configuração desta opção é ON.</br></br>
Do MySQL 5.6, a configuração padrão de saudação for ON, portanto, nenhuma ação é necessária. Para versões anteriores, a configuração padrão de saudação é OFF. configuração de Olá deve ser alterada antes do carregamento de dados, porque somente tabelas recém-criadas são afetadas.
* **innodb_flush_log_at_trx_commit**: valor de padrão de saudação é 1, com hello escopo definido too0 ~ 2. valor padrão de saudação é a opção mais adequada Olá para o banco de dados MySQL. configuração de saudação do 2 habilita o hello mais integridade de dados e é adequada para mestre no Cluster do MySQL. configuração de Olá 0 permite que a perda de dados, que pode afetar a confiabilidade (em alguns casos com melhor desempenho) e é adequado para subordinado em MySQL Cluster.
* **Innodb_log_buffer_size**: o buffer de log Olá permite toorun transações sem ter que tooflush Olá log toodisk antes das transações são confirmadas hello. No entanto, se houver objetos binários grandes ou campo de texto, cache hello será consumido rapidamente e e/s de disco frequentes será disparado. É melhor aumentar o tamanho do buffer de saudação se a variável de estado Innodb_log_waits não é 0.
* **query_cache_size**: Olá melhor opção é toodisable-lo desde o início de saudação. Defina too0 query_cache_size (Isso é configuração do padrão de saudação do MySQL 5.6) e use toospeed outros métodos as consultas.  

Consulte [Apêndice D](#AppendixD) para obter uma comparação de desempenho antes e depois da otimização de saudação.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Ativar o log de consultas lentas Olá MySQL para analisar um afunilamento de desempenho Olá
log de consultas lentas MySQL Olá pode ajudar a identificar consultas lentas Olá para MySQL. Depois de habilitar o log de consultas lentas Olá MySQL, você pode usar ferramentas de MySQL como **mysqldumpslow** tooidentify afunilamento de desempenho de saudação.  

Por padrão, isso não está habilitado. Ativar o log de consultas lentas hello, alguns recursos da CPU pode consumir. É recomendável que você habilite isso temporariamente para solucionar problemas de afunilamento de desempenho. tooturn no log de consultas lentas hello:

1. Modifique o arquivo de my.cnf de saudação adicionando Olá final de toohello linhas a seguir:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Reinicie o hello MySQL server.

        service  mysql  restart

3. Verifique se configuração de saudação é entrar em vigor usando Olá **Mostrar** comando.

![Slow-query-log ON][7]   

![Slow-query-log results][8]

Neste exemplo, você pode ver que esse recurso de consultas lentas Olá foi ativado. Você pode usar Olá **mysqldumpslow** ferramenta toodetermine afunilamentos de desempenho e otimizar o desempenho, como a adição de índices.

## <a name="appendices"></a>Anexos
Olá seguem dados de teste de desempenho de amostra produzidos em um ambiente de laboratório de destino. Eles fornecem gerais sobre a tendência de dados de desempenho de saudação com diferente abordagens de ajuste de desempenho. Olá resultados poderão variar em versões diferentes do ambiente ou produto.

### <a name="AppendixA"></a>Apêndice A  
**Desempenho de disco (IOPS) com diferentes níveis de RAID**

![IOPS de Disco com diferentes níveis de RAID][9]

**Comandos de teste**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> carga de trabalho Olá desse teste usa 64 threads, tentar tooreach Olá limite de RAID.
>
>

### <a name="AppendixB"></a>Apêndice B  
**Comparação de desempenho (taxa de transferência) do MySQL com diferentes níveis de RAID**   
(sistema de arquivos XFS)

![Comparação de desempenho do MySQL com diferentes níveis de RAID][10]  
![Comparação de desempenho do MySQL com diferentes níveis de RAID][11]

**Comandos de teste**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Comparação de desempenho (OLTP) do MySQL com diferentes níveis de RAID**  
![Comparação de desempenho (OLTP) do MySQL com diferentes níveis de RAID][12]

**Comandos de teste**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Apêndice C   
**Comparação de desempenho de disco (IOPS) para diferentes tamanhos de partes**  
(sistema de arquivos XFS)

![][13]

**Comandos de teste**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

tamanhos de arquivo Hello usados para este teste são 30 GB e 1 GB, respectivamente, com RAID 0 (4 discos) XFS do sistema de arquivos.

### <a name="AppendixD"></a>Apêndice D  
**Comparação de desempenho do MySQL (taxa de transferência) antes e depois da otimização**  
(sistema de arquivos XFS)

![Comparação de desempenho do MySQL (taxa de transferência) antes e depois da otimização][14]

**Comandos de teste**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Olá configuração padrão e a otimização é o seguinte:**

| parâmetros | Padrão | Otimização |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Nenhum |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5.000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Para obter mais [parâmetros de configuração de otimização](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consulte toohello [instruções oficiais do MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Ambiente de teste**  

| Hardware | Detalhes |
| --- | --- |
| CPU |Processador AMD Opteron(tm) 4171 HE/4 cores |
| Memória |14 GB |
| Disco |10 GB/disco |
| SO |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

