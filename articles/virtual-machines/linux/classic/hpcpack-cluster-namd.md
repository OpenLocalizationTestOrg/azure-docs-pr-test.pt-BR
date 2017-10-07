---
title: aaaNAMD com Microsoft HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e executar uma simulação do NAMD com charmrun em vários nós de computação do Linux."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure
Este artigo mostra uma maneira toorun uma carga de trabalho de computação de alto desempenho (HPC) do Linux em máquinas virtuais do Azure. Aqui, você configurar um [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de cluster no Azure conosco de computação do Linux e executar um [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulação e visualizar a estrutura de saudação de um sistema biomolecular grandes.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (para o programa do Dynamics moleculares Nanoscale) é um pacote paralelo dynamics moleculares destinado a simulação de alto desempenho dos sistemas de grande biomolecular que contém o toomillions de átomos. Vírus, estruturas de célula e grande proteínas são exemplos desses sistemas. NAMD dimensiona toohundreds de núcleos de simulações típicas e toomore de 500.000 núcleos para simulações maior hello.
* **Microsoft HPC Pack** fornece recursos toorun HPC em larga escala e aplicativos paralelos em clusters de computadores locais ou máquinas virtuais do Azure. Originalmente desenvolvido como uma solução para cargas de trabalho HPC, o HPC Pack agora permite a execução de aplicativos HPC Linux em VMs do nó de computação do Linux implantadas em um cluster do HPC Pack. Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para ver uma introdução.

Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para o lote e computação de alto desempenho](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Pré-requisitos
* **Cluster HPC Pack com nós de computação do Linux**: implante um cluster HPC Pack com nós de computação do Linux no Azure usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md). Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para pré-requisitos hello e as etapas para qualquer uma das opções. Se você escolher Olá opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo hello nos arquivos de exemplo hello final Olá deste artigo. Este arquivo configura um cluster de HPC Pack com base no Azure, que consiste em um nó principal do Windows Server 2012 R2 e quatro nós de computação grandes do CentOS 6.6. Personalize este arquivo conforme a necessidade para seu ambiente.
* **Arquivos de software e um tutorial NAMD** -software baixar NAMD para Linux Olá [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registro necessário). Este artigo se baseia em NAMD versão 2.10 e usa Olá [Linux-x86_64 (64 bits Intel/AMD com Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) arquivamento. Também baixar Olá [arquivos tutoriais NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Olá downloads são arquivos. tar, e você precisa de um arquivos de saudação Windows ferramenta tooextract no nó principal do cluster hello. arquivos de saudação tooextract, siga as instruções de saudação neste artigo. 
* **VMD** (opcional) - toosee resultados de saudação do seu trabalho NAMD, baixar e instalar o programa de visualização moleculares Olá [VMD](http://www.ks.uiuc.edu/Research/vmd/) em um computador de sua escolha. versão atual do Hello é 1.9.2. Consulte Olá VMD baixar tooget site iniciado.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configurar a relação de confiança mútua entre os nós de computação
Executar um trabalho de nó cruzado em vários nós do Linux requer Olá nós tootrust entre si (por **rsh** ou **ssh**). Quando você cria o cluster de HPC Pack Olá com hello script de implantação do Microsoft HPC Pack IaaS, o script hello configura automaticamente confiança mútua permanente da conta de administrador Olá que você especificar. Para usuários não-administrador que criar no domínio do cluster hello, você tem tooset a relação de confiança mútua temporária entre nós hello quando um trabalho é alocado toothem. Em seguida, destrua relação Olá após a conclusão do trabalho de saudação. toodo isso para cada usuário, fornecer um cluster de toohello do par de chaves RSA quais HPC Pack usa a relação de confiança tooestablish hello. Siga as instruções.

### <a name="generate-an-rsa-key-pair"></a>Gerar um par de chaves RSA
É fácil toogenerate um par de chaves RSA, que contém uma chave pública e uma chave privada, executando Olá Linux **ssh-keygen** comando.

1. Faça logon no tooa computador Linux.
2. Execute Olá comando a seguir:
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Pressione **Enter** toouse Olá configurações até que o comando Olá é concluído. Não insira uma frase secreta aqui. Quando for solicitada uma senha, basta pressionar **Enter**.
   > 
   > 
   
   ![Gerar um par de chaves RSA][keygen]
3. Altere o diretório de ~/.ssh toohello do diretório. chave privada Olá é armazenado na chave pública id_rsa e hello em id_rsa.pub.
   
   ![Chaves públicas e privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Adicionar um cluster de HPC Pack em toohello Olá par de chaves
1. [Conecte-se pela área de trabalho remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VM usando o nó principal toohello Olá credenciais de domínio que você forneceu quando você implantou o cluster hello (por exemplo, hpc\clusteradmin). Você gerencia o cluster de saudação do nó principal hello.
2. Use toocreate de procedimentos padrão do Windows Server uma conta de usuário de domínio no domínio do Active Directory do cluster hello. Por exemplo, use o hello usuário do Active Directory e a ferramenta de computadores no nó de cabeçalho hello. exemplos de saudação neste artigo presumem que você criar um usuário de domínio chamado hpcuser no domínio hpclab de saudação (hpclab\hpcuser).
3. Adicione o cluster de HPC Pack toohello do usuário de domínio hello como um usuário de cluster. Para obter instruções, consulte [Adicionar ou remover usuários de cluster](https://technet.microsoft.com/library/ff919330.aspx).
4. Crie um arquivo chamado C:\cred.xml e copiar Olá RSA chave dados nele. Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Abra um Prompt de comando e digite Olá Olá tooset credenciais dados da conta de hpclab\hpcuser de saudação do comando a seguir. Use Olá **extendeddata** toopass parâmetro hello nome do arquivo de C:\cred.xml Olá criado para dados de chave hello.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Esse comando é concluído com êxito sem resultados. Depois de definir credenciais Olá Olá para contas de usuário que é necessário toorun trabalhos, armazenar o arquivo de cred.xml Olá em um local seguro ou exclua-o.
6. Se você gerou Olá par de chaves RSA em um de seus nós do Linux, lembre-se as chaves de saudação toodelete depois de terminar de usá-los. O HPC Pack não define a relação de confiança mútua se ele encontrar um arquivo id_rsa ou id_rsa.pub existente.

> [!IMPORTANT]
> Não é recomendável executar um trabalho de Linux como um administrador de cluster em um cluster compartilhado, porque um trabalho enviada por um administrador é executado na conta de raiz de saudação em nós do Linux hello. Um trabalho enviada por um usuário não administrador é executado sob uma conta de usuário local do Linux com hello mesmo nome como usuário do trabalho de saudação. Nesse caso, HPC Pack define a relação de confiança mútua para esse usuário do Linux em todos os nós de saudação alocados toohello trabalho. Você pode configurar o usuário do Linux Olá manualmente em nós do Linux Olá antes de executar o trabalho de saudação ou HPC Pack cria usuário Olá automaticamente quando o trabalho de saudação é enviado. Se o HPC Pack cria usuário hello, HPC Pack excluirá Olá trabalho concluído. ameaça à segurança tooreduce, Olá chaves são removidas após a conclusão do trabalho de saudação em nós hello.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configurar um compartilhamento de arquivos para nós do Linux
Agora configurar um compartilhamento de arquivo SMB e montar a pasta compartilhada de saudação em todos os nós tooallow Olá Linux nós tooaccess NAMD arquivos Linux com um caminho comum. A seguir é etapas toomount uma pasta compartilhada no nó principal hello. Um compartilhamento é recomendado para distribuições como CentOS 6.6 que atualmente não há suporte para serviços de arquivo do Azure hello. Se os nós do Linux oferecem suporte a um compartilhamento de arquivos do Azure, consulte [como toouse armazenamento de arquivo do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md). Para opções de compartilhamento de arquivos adicionais com o HPC Pack, e as etapas em [Introdução aos nós de computação do Linux em um cluster do HPC Pack no Azure](hpcpack-cluster.md).

1. Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone Configurando os privilégios de leitura/gravação. Neste exemplo, \\ \\CentOS66HN\Namd é o nome de saudação da pasta de hello, onde CentOS66HN é o nome do host de saudação do nó principal hello.
2. Crie uma subpasta chamada namd2 na pasta compartilhada hello. No namd2, crie outra subpasta chamada namdsample.
3. Extraia os arquivos NAMD de saudação na pasta hello usando uma versão do Windows do **tar** ou outro utilitário do Windows que opera em arquivos mortos. tar. 
   
   * Extrair o arquivo de tar Olá NAMD muito\\\\CentOS66HN\Namd\namd2.
   * Extrair arquivos do tutorial de saudação em \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Abra uma janela do Windows PowerShell e execute Olá toomount Olá pasta compartilhada em nós do Linux Olá de comandos a seguir.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Olá primeiro comando cria uma pasta chamada /namd2 em todos os nós no grupo de LinuxNodes hello. comando segundo Olá monta Olá compartilhado pasta //CentOS66HN/Namd/namd2 na pasta de saudação com dir_mode e file_mode too777 de conjunto de bits. Olá *username* e *senha* Olá comando deve ser credenciais de saudação de um usuário no nó de cabeçalho hello.

> [!NOTE]
> Olá "\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell. "\`,"significa hello"," (vírgula) é uma parte do comando hello.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Criar um toorun de script Bash um trabalho NAMD
Precisa de seu trabalho NAMD um *nodelist* de arquivos para **charmrun** toodetermine número de saudação de nós toouse ao iniciar processos NAMD. Você usar um script de Bash que gera o arquivo de nodelist hello e executa **charmrun** com esse arquivo nodelist. Depois, você pode enviar um trabalho do NAMD no Gerenciador de Cluster do HPC que chama esse script.

Usando um editor de texto de sua escolha, criar um script de Bash na pasta de /namd2 Olá que contém arquivos de programa NAMD hello e nomeie-a como hpccharmrun.sh. Para uma rápida verificação de conceito, copie o script de hpccharmrun.sh de exemplo hello fornecido no final deste artigo hello e vá muito[enviar um trabalho NAMD](#submit-a-namd-job).

> [!TIP]
> Salve o script como um arquivo de texto com as terminações de linha do Linux (somente LF, não CR LF). Isso garante que ele seja executado corretamente em nós do Linux hello.
> 
> 

Veja a seguir os detalhes sobre a função desse script bash. 

1. Defina algumas variáveis.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Obter informações do nó de variáveis de ambiente hello. $NODESCORES armazena uma lista de palavras de divisão de $CCP_NODES_CORES. $COUNT é o tamanho de saudação do $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   Olá formato variável do hello $CCP_NODES_CORES é da seguinte maneira:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Essa variável lista o número total de saudação de nós, nomes de nós e número de núcleos em cada nó que estão alocados toohello trabalho. Por exemplo, se o trabalho de saudação precisar 10 toorun de núcleos, o valor de Olá de $CCP_NODES_CORES é semelhante a:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Se a variável CCP_NODES_CORES $ Olá não for definido, inicie **charmrun** diretamente. (Isso só deve ocorrer quando você executa esse script diretamente nos nós do Linux.)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Outra opção é criar um arquivo nodelist para **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Executar **charmrun** com o arquivo de nodelist hello, obter seu status de retorno e remover Olá nodelist arquivo final hello.
   
   ${CCP_NUMCPUS} é a outra variável de ambiente definido por nó principal do HPC Pack hello. Ele armazena o número de saudação de núcleos total alocada toothis trabalho. Nós usamos toospecify número de saudação de processos para charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Sair com hello **charmrun** status de retorno.
   
   ```
   exit ${RTNSTS}
   ```

O seguinte é informações Olá no arquivo de nodelist hello, gera o script hello:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Por exemplo:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Enviar um trabalho NAMD
Agora você está pronto toosubmit um trabalho NAMD no Gerenciador de Cluster de HPC.

1. Conecte-se o nó principal do cluster tooyour e iniciar o Gerenciador de Cluster de HPC.
2. Em **gerenciamento de recursos**, verifique se nós de computação Olá Linux estão em Olá **Online** estado. Se não estiverem, selecione-os e clique em **Colocar Online**.
3. Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.
4. Insira um nome para o trabalho como *hpccharmrun*.
   
   ![Novo trabalho do HPC][namd_job]
5. Em Olá **detalhes do trabalho** página em **recursos de trabalho**, selecione o tipo de saudação do recurso como **nó** e conjunto hello **mínimo** too3. , podemos executar o trabalho de saudação em três nós do Linux e cada nó tem quatro núcleos.
   
   ![Recursos de trabalho][job_resources]
6. Clique em **editar tarefas** Olá navegação esquerdo e, em seguida, clique em **adicionar** tooadd um trabalho de toohello de tarefa.    
7. Em Olá **detalhes da tarefa e redirecionamento de e/s** página saudação do conjunto de valores a seguir:
   
   * **Linha de comando** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Olá, linha de comando anterior é um único comando sem quebras de linha. Ele encapsula tooappear em várias linhas em **linha de comando**.
     > 
     > 
   * **Diretório de trabalho** - /namd2
   * **Mínimo** - 3
     
     ![Detalhes de tarefa][task_details]
     
     > [!NOTE]
     > Definir diretório de trabalho Olá aqui porque **charmrun** tenta toonavigate toohello mesmo diretório de trabalho em cada nó. Se o diretório de trabalho de saudação não for definido, o HPC Pack inicia o comando de saudação em uma pasta nomeada aleatoriamente criada em um de nós do Linux hello. Isso faz com que Olá erro a seguir no hello outros nós: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid esse problema, especifique um caminho de pasta que possa ser acessado por todos os nós como diretório de trabalho hello.
     > 
     > 
8. Clique em **Okey** e, em seguida, clique em **enviar** toorun esse trabalho.
   
   Por padrão, o HPC Pack envia trabalho hello como sua conta de logon do usuário atual. Uma caixa de diálogo pode solicitar que você tooenter Olá nome e uma senha depois de clicar em **enviar**.
   
   ![Credenciais de trabalho][creds]
   
   Sob algumas condições, o HPC Pack lembra informações de usuário de saudação antes de entrada e não mostrar esta caixa de diálogo. toomake HPC Pack mostrá-la novamente, insira Olá comando no Prompt de comando a seguir e, em seguida, enviar o trabalho de saudação.
   
   ```command
   hpccred delcreds
   ```
9. trabalho de saudação toma toofinish de vários minutos.
10. Localizar o log do trabalho de saudação em \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log e hello arquivos de saída \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Opcionalmente, inicie VMD tooview os resultados do trabalho. etapas Olá para visualizar os arquivos de saída NAMD hello (nesse caso, uma molécula de proteína ubiquitin em uma esfera de água) estão além do escopo deste artigo hello. Veja [Tutorial do NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) para obter mais detalhes.
    
    ![Resultados de trabalho][vmd_view]

## <a name="sample-files"></a>Arquivos de exemplo
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a>Exemplo de arquivo cred.xml
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a>Exemplo de script hpccharmrun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
