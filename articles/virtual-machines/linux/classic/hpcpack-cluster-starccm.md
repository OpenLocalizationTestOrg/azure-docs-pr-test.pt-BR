---
title: aaaRun ESTRELA-CCM + com HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e execute um trabalho do STAR-CCM+ em vários nós de computação do Linux em uma rede RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Executar o STAR-CCM+ com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure
Este artigo mostra como toodeploy um Microsoft HPC Pack cluster no Azure e execute um [adapco CD ESTRELA-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) trabalho em vários nós de computação de Linux que estão interconectados com InfiniBand.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack fornece recursos toorun uma variedade de HPC em larga escala e aplicativos em paralelo, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure. O HPC Pack também dá suporte à execução de aplicativos de HPC do Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack. Para uma introdução toousing Linux nós com o HPC Pack de computação, consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Configurar um cluster do HPC Pack
Fazer o download de scripts de implantação IaaS do HPC Pack Olá Olá [Centro de Download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) e extraia-os localmente.

O Azure PowerShell é um pré-requisito. Se o PowerShell não está configurado no seu computador local, leia o artigo da saudação [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Em tempo de saudação da redação deste artigo, imagens Linux Olá Olá Azure Marketplace (que contém os drivers de InfiniBand de saudação do Azure) são para 12 SLES, CentOS 6.5 e CentOS 7.1. Este artigo é com base no uso de saudação de 12 SLES. nome de saudação tooretrieve de todas as imagens do Linux que dão suporte a HPC Olá Marketplace, você pode executar Olá comando PowerShell a seguir:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

saída de Hello lista local de saudação em que essas imagens estão disponíveis em Olá nome da imagem (**ImageName**) toobe usado no modelo de implantação de hello mais tarde.

Antes de implantar o cluster hello, você tem toobuild um arquivo de modelo de implantação do HPC Pack. Porque estamos visando um pequeno cluster, o nó principal Olá Olá controlador de domínio e hospedar um banco de dados local do SQL.

Olá modelo a seguir será implantar tal um nó principal, crie um arquivo XML denominado **MyCluster.xml**e substitua os valores de saudação do **SubscriptionId**, **StorageAccount**,  **Local**, **VMName**, e **ServiceName** com as suas.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Inicie criação de nó de cabeçalho de saudação executando Olá comando do PowerShell em um prompt de comando elevado:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Depois de 20 minutos too30 nó principal Olá deve estar pronto. Você pode se conectar tooit de saudação portal do Azure clicando Olá **conectar** ícone da máquina virtual de saudação.

Eventualmente, você pode ter o encaminhador de DNS Olá toofix. toodo caso, inicie o Gerenciador de DNS.

1. Nome do servidor Olá com o botão direito no Gerenciador DNS, selecione **propriedades**e, em seguida, clique em Olá **encaminhadores** guia.
2. Clique em Olá **editar** botão tooremove os encaminhadores e, em seguida, clique em **Okey**.
3. Certifique-se de que Olá **usar dicas de raiz, não se houver nenhuma encaminhadores** caixa de seleção está selecionada e, em seguida, clique em **Okey**.

## <a name="set-up-linux-compute-nodes"></a>Configurar nós de computação do Linux
Implantar nós de computação Linux hello usando Olá mesmo modelo de implantação que você usou o nó principal do toocreate hello.

Copiar o arquivo de saudação **MyCluster.xml** no nó principal do computador local toohello e atualização Olá **NodeCount** marcar com número de saudação de nós que você deseja toodeploy (< = 20). Ser cuidadoso toohave núcleos suficientes disponíveis em sua cota do Azure, porque cada instância A9 consumirá 16 núcleos em sua assinatura. Você pode usar instâncias A8 (8 núcleos) em vez de A9 se você quiser toouse mais VMs no hello mesmo orçamento.

No nó de cabeçalho hello, copie os scripts de implantação IaaS do HPC Pack hello.

Olá executar comandos do PowerShell do Azure em um prompt de comando a seguir:

1. Executar **Add-AzureAccount** tooconnect tooyour assinatura do Azure.
2. Se você tiver várias assinaturas, execute **Get-AzureSubscription** toolist-los.
3. Defina uma assinatura padrão executando Olá **Select-AzureSubscription - SubscriptionName xxxx-padrão** comando.
4. Executar **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart implantar nós de computação do Linux.
   
   ![Implantação do nó principal em ação][hndeploy]

Abra a ferramenta de Gerenciador de Cluster do HPC Pack hello. Após alguns minutos, os nós de computação do Linux aparecerão regularmente na lista de nós de computação do cluster. Com o modo de implantação clássico hello, as VMs de IaaS são criadas em sequência. Então se o número de saudação de nós é importante, obter todos implantado pode levar uma quantidade significativa de tempo.

![Nós do Linux no Gerenciador de Cluster do HPC Pack][clustermanager]

Agora que todos os nós estão em execução no cluster hello, há toomake de configurações de infraestrutura adicional.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Configurar um compartilhamento de arquivos do Azure para nós do Windows e Linux
Você pode usar scripts de toostore de serviços de arquivo do Azure hello, pacotes de aplicativos e arquivos de dados. O arquivo do Azure fornece funcionalidades CIFS sobre o Armazenamento de Blobs do Azure como um repositório persistente. Lembre-se de que isso não é solução mais dimensionável do hello, mas é Olá um mais simples e não requer VMs dedicadas.

Criar um compartilhamento de arquivos do Azure seguindo as instruções de saudação artigo Olá [Introdução ao armazenamento de arquivo do Azure no Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).

Manter Olá nome da sua conta de armazenamento como **saname**, nome de compartilhamento de arquivo hello como **sharename**e a chave de conta de armazenamento hello como **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Compartilhamento de arquivo do Azure Olá montagem no nó de cabeçalho Olá
Abra um prompt de comando com privilégios elevados e execute Olá credenciais de saudação do comando toostore no cofre do computador local Olá a seguir:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Em seguida, toomount hello Azure compartilhamento de arquivos, execute:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Montar o compartilhamento de arquivo do Azure Olá em nós de computação do Linux
Uma ferramenta útil que vem com o HPC Pack é a ferramenta de clusrun de saudação. Você pode usar este Olá toorun de ferramenta de linha de comando mesmo comando simultaneamente em um conjunto de nós de computação. Em nosso caso, ele usou o compartilhamento de arquivo do Azure Olá toomount e mantê-lo toosurvive reinicializações.
Em um prompt de comando elevado no nó principal do hello, execute Olá comandos a seguir.

diretório de montagem Olá toocreate:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

Olá toomount compartilhamento de arquivos do Azure:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

compartilhamento de montagem de saudação toopersist:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Instalar o STAR-CCM+
As instâncias de VM do Azure A8 e A9 dão suporte ao InfiniBand e funcionalidades de RDMA. drivers de kernel Olá habilitam esses recursos estão disponíveis para o Windows Server 2012 R2, SUSE 12, CentOS 6.5 e imagens CentOS 7.1 hello Azure Marketplace. Microsoft MPI e Intel MPI (versão 5. x) são Olá duas MPI bibliotecas que dão suporte a esses drivers no Azure.

O STAR-CCM+ da CD-adapco versão 11.x e posterior é fornecido com o Intel MPI versão 5.x, portanto o suporte do InfiniBand para Azure está incluído.

Obter Olá Linux64 ESTRELA-CCM + pacote de saudação [CD adapco portal](https://steve.cd-adapco.com). Em nosso caso, usamos a versão 11.02.010 com precisão mista.

No nó de cabeçalho hello, em Olá **/hpcdata** arquivo do Azure compartilham, crie um script de shell chamado **setupstarccm.sh** com hello conteúdo a seguir. Esse script será executado em cada tooset do nó de computação backup ESTRELA-CCM + localmente.

#### <a name="sample-setupstarcmsh-script"></a>Script setupstarcm.sh de exemplo
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Agora, tooset backup ESTRELA-CCM + no seu Linux todos os nós de computação, abra um prompt de comando com privilégios elevados e execute Olá comando a seguir:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Enquanto estiver executando o comando hello, você pode monitorar o uso de CPU hello usando o mapa de calor de saudação do Gerenciador de Cluster. Depois de alguns minutos, todos os nós devem estar instalados corretamente.

## <a name="run-star-ccm-jobs"></a>Executar trabalhos do STAR-CCM+
HPC Pack é usado para suas capacidades de Agendador de trabalho em ordem toorun ESTRELA-CCM + trabalhos. toodo, portanto, é necessário Olá suporte de alguns scripts que são usados toostart trabalho de saudação e execute ESTRELA-CCM +. dados de entrada Hello são mantidos em um compartilhamento de arquivo do Azure Olá primeiro para manter a simplicidade.

saudação de script do PowerShell a seguir é usado tooqueue uma ESTRELA-CCM + trabalho. Ele usa três argumentos:

* nome do modelo Olá
* número de saudação de nós toobe usado
* número de saudação de núcleos em cada toobe de nó usado

Porque ESTRELA-CCM + pode preencher largura de banda de memória Olá, é geralmente melhor toouse menos núcleos por nós de computação e adicionar novos nós. número exato de saudação de núcleos por nó dependerá da família de processadores hello e velocidade de interconexão de saudação.

nós de saudação são alocados exclusivamente para trabalho hello e não podem ser compartilhadas com outros trabalhos. trabalho de saudação não será iniciado como um trabalho MPI diretamente. Olá **runstarccm.sh** script de shell iniciará o iniciador MPI hello.

saudação de entrada de modelo e Olá **runstarccm.sh** script são armazenados no hello **/hpcdata** compartilhamento anteriormente foi montado.

Arquivos de log são nomeados com a ID do trabalho hello e são armazenados no hello **/hpcdata compartilhamento**, juntamente com hello ESTRELA-CCM + arquivos de saída.

#### <a name="sample-submitstarccmjobps1-script"></a>Script SubmitStarccmJob.ps1 de exemplo
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Substitua **runner.java** por seu código de registro em log e código do iniciador de modelo Java do STAR-CCM+ preferidos.

#### <a name="sample-runstarccmsh-script"></a>Script runstarccm.sh de exemplo
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

Em nosso teste, usamos um token de licença do tipo Power-On-Demand. Para esse token, você tem Olá tooset **$CDLMD_LICENSE_FILE** variável de ambiente muito **1999@flex.cd-adapco.com**  e chave Olá Olá **- podkey** opção de linha de comando Olá .

Após a inicialização de alguns, extrai script hello – de saudação **CCP_NODES_CORES $** variáveis de ambiente que defina HPC Pack - Olá lista de nós toobuild usa um arquivo de host que Olá iniciador MPI. Esse arquivo de host vai conter uma lista de saudação dos nomes de nó de computação que são usados para trabalho hello, um nome por linha.

formato de saudação do **CCP_NODES_CORES $** segue este padrão:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Em que:

* `<Number of nodes>`é o número de saudação de nós alocada toothis trabalho.
* `<Name of node_n_...>`é o nome de saudação de cada nó alocada toothis trabalho.
* `<Cores of node_n_...>`é o número de saudação de núcleos no nó Olá alocada toothis trabalho.

Olá número de núcleos (**$NBCORES**) também é calculada Olá com base no número de nós (**$NBNODES**) e o número de saudação de núcleos por nó (fornecido como parâmetro **$NBCORESPERNODE**).

Para obter opções de MPI hello, Olá aqueles que são usados com Intel MPI no Azure são:

* `-mpi intel`toospecify Intel MPI.
* `-fabric UDAPL`verbos toouse InfiniBand do Azure.
* `-cpubind bandwidth,v`largura de banda toooptimize de MPI com ESTRELA-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI trabalhar com o Azure InfiniBand e tooset Olá obrigatório número de núcleos por nó.
* `-batch`toostart ESTRELA-CCM + em modo de lote com nenhuma interface do usuário.

Por fim, toostart um trabalho, certifique-se de que os nós estão funcionando e estão online no Gerenciador de Cluster. Em seguida, de um prompt de comando do PowerShell execute:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Parar os nós
Posteriormente em, depois de concluir os testes, você pode usar o hello toostop de comandos do PowerShell do HPC Pack a seguir e iniciar os nós:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Próximas etapas
Tentar executar outras cargas de trabalho do Linux. Por exemplo, consulte:

* [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md)
* [Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
