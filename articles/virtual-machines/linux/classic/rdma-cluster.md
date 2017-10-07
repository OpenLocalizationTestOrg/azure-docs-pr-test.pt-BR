---
title: aaaSet um aplicativos de MPI Linux RDMA cluster toorun | Microsoft Docs
description: "Criar um cluster do Linux de toouse H16r, H16mr, A8 ou A9 VMs de tamanho Olá RDMA do Azure rede toorun MPI aplicativos"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Configurar um aplicativo de MPI toorun Linux RDMA cluster
Saiba como tooset a um RDMA Linux cluster no Azure com [tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun aplicativos de Interface MPI (Message Passing) paralelos. Este artigo fornece etapas tooprepare um toorun de imagem do Linux HPC MPI Intel em um cluster. Após a preparação, é possível implantar um cluster de VMs usando essa imagem e um dos tamanhos de máquina virtual do Azure compatíveis com RDMA hello (atualmente H16r, H16mr, A8 ou A9). Use Olá cluster toorun MPI aplicativos que se comunicam com eficiência em uma rede de baixa latência, alta taxa de transferência com base na tecnologia de acesso (RDMA) de memória direta remota.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="cluster-deployment-options"></a>Opções de implantação de cluster
Estes são métodos que você pode usar toocreate um cluster Linux RDMA com ou sem um agendador de trabalho.

* **Scripts CLI do Azure**: conforme mostrado neste artigo, use Olá [interface de linha de comando do Azure](../../../cli-install-nodejs.md) implantação de saudação tooscript (CLI) de um cluster de VMs compatíveis com RDMA. Olá CLI no modo de gerenciamento de serviço cria Olá nós de cluster em série no modelo de implantação clássico hello, para que implantar vários nós de computação pode levar vários minutos. Olá tooenable conexão de rede RDMA quando você usa o modelo de implantação clássico hello, implantar VMs Olá no hello mesmo serviço de nuvem.
* **Modelos do Gerenciador de recursos do Azure**: você também pode usar toodeploy de modelo de implantação do hello Gerenciador de recursos um cluster de VMs compatíveis com RDMA que se conecta a rede RDMA toohello. Você pode [criar seu próprio modelo](../../../resource-group-authoring-templates.md), ou verifique Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) para modelos de contribuição pela Microsoft ou hello comunidade toodeploy Olá solução desejada. Modelos do Gerenciador de recursos podem fornecer uma maneira rápida e confiável toodeploy um cluster do Linux. Olá tooenable conexão de rede RDMA quando você usa o modelo de implantação do Gerenciador de recursos de hello, implantar VMs de saudação em Olá mesmo conjunto de disponibilidade.
* **HPC Pack**: criar um cluster do Microsoft HPC Pack no Azure e adicionar nós de computação compatíveis com RDMA que executam uma rede com suporte Linux distribuição tooaccess Olá RDMA. Para saber mais, confira [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>As etapas de implantação de exemplo no modelo clássico Olá
Olá etapas a seguir mostram como toouse Olá CLI do Azure toodeploy uma VM do SUSE Linux Enterprise Server (SLES) 12 SP1 HPC de saudação do Azure Marketplace, personalizá-lo e criar uma imagem VM personalizada. Em seguida, você pode usar implantação da saudação tooscript Olá imagem de um cluster de VMs compatíveis com RDMA.

> [!TIP]
> Use semelhante toodeploy etapas que um cluster de VMs compatíveis com RDMA baseado nas imagens com base em CentOS HPC hello Azure Marketplace. Algumas etapas são ligeiramente diferentes, conforme observado. 
>
>

### <a name="prerequisites"></a>Pré-requisitos
* **Computador cliente**: É necessário um toocommunicate de computador cliente Mac, Linux ou Windows com o Azure. Essas etapas pressupõem que você esteja usando um cliente Linux.
* **Assinatura do Azure**: se não tiver uma assinatura, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos. Para clusters maiores, considere uma assinatura pré-paga ou outras opções de compra.
* **Disponibilidade de tamanho VM**: Olá tamanhos de instância a seguir é capazes de RDMA: H16r, H16mr, A8 e A9. Confira [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/) para ver a disponibilidade nas regiões do Azure.
* **Cota de núcleos**: você pode precisar de uma cota de saudação tooincrease de núcleos toodeploy um cluster de computação intensa VMs. Por exemplo, você precisa, pelo menos, 128 núcleos, se você deseja toodeploy 8 A9 VMs conforme mostrado neste artigo. Sua assinatura também pode limitar o número de saudação de núcleos que podem ser implantados em determinadas famílias de tamanho VM, incluindo Olá H-series. aumentar a cota toorequest, [abrir uma solicitação de suporte do cliente online](../../../azure-supportability/how-to-create-azure-support-request.md) sem custo adicional.
* **CLI do Azure**: [instalar](../../../cli-install-nodejs.md) Olá CLI do Azure e [conectar tooyour assinatura do Azure](../../../xplat-cli-connect.md) do computador do cliente de saudação.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Provisionar uma VM do HPC para SLES 12 SP1
Depois de entrar no tooAzure com hello CLI do Azure, execute `azure config list` tooconfirm que Olá a saída mostra o modo de gerenciamento de serviço. Se não estiver, defina o modo de saudação executando este comando:

    azure config mode asm


Digite hello toolist a seguir todas as assinaturas de saudação são toouse autorizado:

    azure account list

assinatura ativa atual de saudação é identificada com `Current` definido muito`true`. Se esta assinatura não for Olá você deseja toouse toocreate Olá cluster, defina ID de assinatura apropriada Olá como assinatura ativa hello:

    azure account set <subscription-Id>

toosee Olá disponíveis publicamente imagens SLES 12 SP1 HPC no Azure, execute um comando como Olá a seguir, supondo que seu ambiente de shell oferece suporte à **grep**:

    azure vm image list | grep "suse.*hpc"

Provisione uma VM compatíveis com RDMA com uma imagem de HPC de SP1 12 SLES executando um comando como Olá a seguir:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Em que:

* Olá tamanho (A9 neste exemplo) é um dos tamanhos de VM Olá compatíveis com RDMA.
* Olá externo número da porta SSH (22 neste exemplo, o que é o saudação padrão SSH) é qualquer número de porta válido. número da porta SSH interno Olá é definido too22.
* Um novo serviço de nuvem é criado no hello região do Azure especificada pelo Olá local. Especifique um local no qual Olá VM tamanho escolhido está disponível.
* Para suporte de prioridade SUSE (que implica em custo adicional), nome da imagem Olá SP1 de 12 SLES atualmente pode ser uma destas duas opções: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Personalizar Olá VM
Após a conclusão da saudação VM provisionamento, SSH toohello VM usando Olá endereço IP externo da VM (ou nome DNS) e Olá número da porta externa configurado e, em seguida, personalizá-lo. Para obter detalhes de conexão, consulte [como toolog na máquina virtual de tooa executando o Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Execute comandos como usuário Olá configurado no hello VM, a menos que o acesso à raiz é necessário toocomplete uma etapa.

> [!IMPORTANT]
> Microsoft Azure não fornece acesso à raiz tooLinux VMs. acesso administrativo de toogain quando conectado como um usuário toohello VM, execute comandos usando `sudo`.
>
>

* **Atualizações**: instale atualizações usando o zypper. Você também poderá tooinstall utilitários NFS.

  > [!IMPORTANT]
  > Em uma VM de HPC SLES 12 SP1, é recomendável que você não aplicar as atualizações de kernel, que podem causar problemas com hello Linux RDMA drivers.
  >
  >
* **Intel MPI**: Concluir instalação de saudação do Intel MPI no hello SLES 12 SP1 HPC VM executando Olá comando a seguir:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Bloquear memória**: MPI códigos toolock Olá memória disponível para o RDMA, adicionar ou alterar Olá configurações no arquivo de /etc/security/limits.conf Olá a seguir. Você precisa raiz acesso tooedit esse arquivo.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > Para fins de teste, você também pode definir memlock toounlimited. Por exemplo: `<User or group name>    hard    memlock unlimited`. Para saber mais, confira [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size) (Métodos mais conhecidos para definir o tamanho da memória bloqueada).
  >
  >
* **As chaves de SSH para VMs SLES**: gerar SSH chaves tooestablish confiança para sua conta de usuário entre Olá nós de computação no cluster do SLES hello quando executar trabalhos MPI. Se você tiver implantado uma VM do HPC baseado em CentOS, não execute esta etapa. Consulte as instruções posteriormente tooset este artigo a relação de confiança SSH passwordless entre nós de cluster Olá depois de capturar a imagem de saudação e implantar um cluster de saudação.

    chaves SSH toocreate, executadas Olá comando a seguir. Quando você for solicitado para a entrada, selecione **Enter** toogenerate chaves de saudação no local padrão de saudação sem definir uma senha.

        ssh-keygen

    Anexar o arquivo de authorized_keys Olá toohello de chave pública para chaves públicas conhecidas.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    No diretório de ~/.ssh hello, editar ou criar o arquivo de configuração de saudação. Forneça o intervalo de endereços IP hello de rede privada Olá que você planeje toouse no Azure (10.32.0.0/16 neste exemplo):

        host 10.32.0.*
        StrictHostKeyChecking no

    Como alternativa, lista o endereço IP de rede privada de saudação de cada VM no seu cluster da seguinte maneira:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > A configuração de `StrictHostKeyChecking no` pode criar um risco de segurança potencial quando um determinado endereço IP ou intervalo não for especificado.
  >
  >
* **Aplicativos**: instalar os aplicativos necessários ou executar outras personalizações antes de capturar a imagem de saudação.

### <a name="capture-hello-image"></a>Capturar imagem Olá
imagem toocapture hello, primeiro execute Olá comando a seguir no hello VM do Linux. Esse comando deprovisions Olá VM, mas mantém a contas de usuário e as chaves de SSH que você configurou.

```
sudo waagent -deprovision
```

No computador cliente, execute Olá após a imagem de saudação do toocapture de comandos de CLI do Azure. Para obter mais informações, consulte [como uma máquina de virtual do Linux clássica como uma imagem de toocapture](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Depois de executar esses comandos, a imagem da VM Olá é capturada para seu uso e Olá VM é excluído. Agora você tem o toodeploy pronto de imagem personalizada um cluster.

### <a name="deploy-a-cluster-with-hello-image"></a>Implantar um cluster com a imagem de saudação
Modificar Olá Bash script com valores apropriados para o seu ambiente a seguir e executá-lo do computador cliente. Porque o Azure implanta VMs Olá em série no modelo de implantação clássico hello, ele leva alguns minutos toodeploy Olá oito VMs A9 sugerido neste script.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Considerações para um cluster de HPC do CentOS
Se você quiser tooset um cluster com base em uma das imagens HPC com base em CentOS Olá no hello Azure Marketplace em vez de 12 SLES para HPC, siga etapas gerais Olá Olá anterior da seção. Observe Olá diferenças a seguir quando você provisionar e configurar Olá VM:

- O Intel MPI já está instalado em uma VM provisionada de uma imagem do HPC baseado em CentOS.
- Configurações de memória de bloqueio já foram adicionadas no arquivo de /etc/security/limits.conf de saudação da VM.
- Não gere chaves SSH no hello VM provisionar para captura. Em vez disso, é recomendável configurar a autenticação baseada em usuário após a implantação de cluster de saudação. Para obter mais informações, consulte Olá seção a seguir.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Configurar confiança passwordless do SSH no cluster Olá
Em um cluster HPC com base em CentOS, há dois métodos para estabelecer confiança entre nós de computação Olá: autenticação baseada em host e a autenticação baseada em usuário. Autenticação baseada em host está fora do escopo deste artigo hello e geralmente deve ser feita por meio de um script de extensão durante a implantação. Autenticação baseada em usuário é conveniente para estabelecer confiança após a implantação e requer o compartilhamento de chaves SSH entre hello e geração de saudação nós de computação em cluster hello. Esse método é conhecido como logon SSH sem senha e é necessário na execução de trabalhos MPI.

Está disponível em um script de exemplo a contribuição da comunidade Olá [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) autenticação de usuário fácil tooenable em um cluster HPC com base em CentOS. Baixar e usar esse script usando Olá etapas a seguir. Você também pode modificar o script ou usar qualquer outra método tooestablish passwordless autenticação SSH entre nós de computação de cluster hello.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

script de saudação toorun, é necessário tooknow prefixo de saudação para seus endereços IP de sub-rede. Obtenha o prefixo Olá executando Olá comando a seguir em um de nós de cluster de saudação. A saída deve ser algo como 10.1.3.5 e prefixo Olá é parte de saudação 10.1.3.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Agora execute o script hello usando três parâmetros: nome de usuário comuns Olá no hello nós de computação, senha comum Olá para nós de computação do usuário em hello e prefixo de sub-rede Olá que foi retornada do comando anterior hello.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Esse script hello a seguir:

* Cria um diretório no nó de host Olá denominado .ssh, que é necessário para logon passwordless.
* Cria um arquivo de configuração no diretório de .ssh Olá que instrui o logon de tooallow passwordless logon de qualquer nó no cluster de saudação.
* Cria arquivos que contêm nomes de nó hello e endereços IP do nó de todos os nós de saudação em cluster hello. Esses arquivos são deixados após a execução de script hello para referência posterior.
* Cria um par de chaves público e privado para cada nó de cluster (incluindo o nó do host Olá) e cria entradas no arquivo de authorized_keys hello.

> [!WARNING]
> A execução desse script pode criar um potencial risco de segurança. Certifique-se de que as informações de chave pública do hello em ~/.ssh não são distribuídas.
>
>

## <a name="configure-intel-mpi"></a>Configurar o Intel MPI
aplicativos de MPI toorun em RDMA de Linux do Azure, você precisa tooconfigure determinado tooIntel da específico de variáveis de ambiente MPI. Aqui está um exemplo Bash script tooconfigure Olá variáveis necessárias toorun um aplicativo. Altere Olá caminho toompivars.sh conforme necessário para a instalação do Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

formato de Olá Olá do arquivo do host é o seguinte. Adicione uma linha para cada nó no cluster. Especifique os endereços IP privados da rede virtual Olá definido anteriormente, não os nomes DNS. Por exemplo, para dois hosts com endereços IP 10.32.0.1 e 10.32.0.2, o arquivo hello contém seguinte hello:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Executar MPI em um cluster de dois nós básico
Se você ainda não fez isso, primeiro defina o ambiente de saudação para Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Executar um comando MPI
Execute um comando MPI em uma saudação tooshow de nós de computação que MPI está instalado corretamente e pode se comunicar entre pelo menos dois nós de computação. a seguir Olá **mpirun** comando executa Olá **hostname** comando em dois nós.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
A saída deve listar os nomes de saudação de todos os nós de saudação passado como entrada para `-hosts`. Por exemplo, um **mpirun** comando com dois nós retorna a saída como Olá seguinte:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Executar um parâmetro de comparação de MPI
Olá Intel MPI comando a seguir executa uma pingpong benchmark tooverify Olá configuração e conexão toohello RDMA rede de cluster.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

Em um cluster com dois nós de trabalho, você deve ver a saída como Olá seguinte. Na rede de RDMA do Azure Olá, espere latência ou abaixo 3 microssegundos de tamanhos de mensagem too512 bytes.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Próximas etapas
* Implantar e executar os aplicativos MPI do Linux no cluster do Linux.
* Consulte Olá [documentação da Intel MPI biblioteca](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) para obter orientação sobre Intel MPI.
* Tente uma [quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate um Lustre Intel cluster usando uma imagem com base em CentOS HPC. Para obter detalhes, confira [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Implantando o Intel Cloud Edition for Lustre no Microsoft Azure).
