---
title: aaaRun OpenFOAM com HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e execute um trabalho OpenFOAM em vários nós de computação do Linux em uma rede RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Executar o OpenFoam com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure
Este artigo mostra uma maneira toorun OpenFoam em máquinas virtuais do Azure. Aqui, você implanta um cluster do Microsoft HPC Pack com nós de computação do Linux no Azure e executa um trabalho [OpenFoam](http://openfoam.com/) com Intel MPI. Você pode usar VMs do Azure compatíveis com RDMA para nós de computação hello, para que nós de computação Olá se comunicar pela rede de RDMA do Azure hello. Outros toorun opções OpenFoam no Azure incluem totalmente configurado comerciais imagens disponíveis na Olá Marketplace, como do UberCloud [OpenFoam 2.3 em CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)e executando em [do Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (Operação e Manipulação de Campo Aberto) é um pacote de software com CFD (dinâmica de fluido computacional) aberto, amplamente utilizado na Engenharia e nas Ciências em organizações comerciais e acadêmicas. Ele inclui ferramentas para criar malhas, especialmente o snappyHexMesh, um mesher em paralelo para geometrias CAD complexas e de pré e pós-processamento. Quase todos os processos executados em paralelo, permitindo que os usuários tootake proveito do hardware do computador à sua disposição.  

Microsoft HPC Pack fornece recursos toorun HPC em larga escala e aplicativos em paralelo, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure. O HPC Pack também dá suporte a aplicativos de HPC no Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack. Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para uma introdução toousing nós com o HPC Pack de computação do Linux.

> [!NOTE]
> Este artigo ilustra como toorun uma carga de trabalho do Linux MPI com HPC Pack. Ele pressupõe que você tem alguma familiaridade com a administração do sistema Linux e com a execução das cargas de trabalho MPI nos clusters do Linux. Se você usar versões de MPI e OpenFOAM diferente da saudação aqueles mostrados neste artigo, você pode ter toomodify algumas etapas de instalação e configuração. 
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* **Cluster HPC Pack com nós de computação do Linux compatíveis com RDMA** – Implante um cluster HPC Pack com nós de computação do Linux do tamanho A8, A9, H16r ou H16rm usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md). Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para pré-requisitos hello e as etapas para qualquer uma das opções. Se você escolher Olá opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo hello nos arquivos de exemplo hello final Olá deste artigo. Use este cluster de HPC Pack configuração toodeploy um baseado no Azure consiste em um nó de cabeçalho de tamanho A8 Windows Server 2012 R2 e nós de computação de tamanho de 2 A8 SUSE Linux Enterprise Server 12. Substitua os valores apropriados por sua assinatura e nomes de serviço. 
  
  **Outras coisas que você tooknow**
  
  * Para pré-requisitos de rede RDMA Linux no Azure, consulte [Tamanhos de VM de computação de alto desempenho](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Se você usar Olá opção de implantação de script do Powershell, implante todos os nós de computação Linux hello dentro de conexão de rede RDMA uma nuvem serviço toouse hello.
  * Depois de implantar nós do Linux hello, conecte-se SSH tooperform outras tarefas administrativas. Localize detalhes de conexão SSH Olá para cada VM do Linux no hello portal do Azure.  
* **Intel MPI** -toorun OpenFOAM em SLES 12 HPC nós de computação no Azure, é necessário em tempo de execução do tooinstall Olá Intel MPI biblioteca 5 da saudação [site Intel.com](https://software.intel.com/en-us/intel-mpi-library/). (O Intel MPI 5 está pré-instalado em imagens do HPC baseado em CentOS.)  Em uma etapa posterior, se necessário, instale o Intel MPI em seus nós de computação do Linux. tooprepare para esta etapa, depois de registrar com a Intel, siga o link de saudação na Olá email toohello relacionados web página de confirmação. Em seguida, Olá cópia baixar link para arquivo hello. tgz versão apropriada de saudação do Intel MPI. Este artigo se baseia no Intel MPI versão 5.0.3.048.
* **Pacote de origem OpenFOAM** -baixar o software de pacote de origem OpenFOAM Olá para Linux de saudação [site OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/). Este artigo baseia-se no Source Pack versão 2.3.1, disponível para download como OpenFOAM-2.3.1.tgz. Siga instruções Olá posteriormente neste artigo toounpack e compilar OpenFOAM em nós de computação Linux hello.
* **EnSight** (opcional) - resultados de saudação toosee de simulação OpenFOAM, baixe e instale Olá [EnSight](https://www.ceisoftware.com/download/) programa de visualização e análise. São informações de licença e o download no site de EnSight hello.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configurar a relação de confiança mútua entre os nós de computação
Executar um trabalho de nó cruzado em vários nós do Linux requer Olá nós tootrust entre si (por **rsh** ou **ssh**). Quando você cria o cluster de HPC Pack Olá com hello script de implantação do Microsoft HPC Pack IaaS, o script hello configura automaticamente confiança mútua permanente da conta de administrador Olá que você especificar. Para usuários não-administrador que criar no domínio do cluster hello, você tem tooset a relação de confiança mútua temporária entre nós hello quando um trabalho é alocada toothem e destruir relação Olá após a conclusão do trabalho de saudação. confiança tooestablish para cada usuário, forneça um cluster de toohello de par de chaves RSA HPC Pack usa Olá relação de confiança.

### <a name="generate-an-rsa-key-pair"></a>Gerar um par de chaves RSA
É fácil toogenerate um par de chaves RSA, que contém uma chave pública e uma chave privada, executando Olá Linux **ssh-keygen** comando.

1. Faça logon no tooa computador Linux.
2. Execute Olá comando a seguir:
   
   ```
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
1. Fazer um nó de cabeçalho de tooyour de conexão de área de trabalho remota com sua conta de administrador do HPC Pack (conta de administrador Olá configurada durante a execução do script de implantação de saudação).
2. Use toocreate de procedimentos padrão do Windows Server uma conta de usuário de domínio no domínio do Active Directory do cluster hello. Por exemplo, use o hello usuário do Active Directory e a ferramenta de computadores no nó de cabeçalho hello. exemplos de saudação neste artigo presumem que você criar um usuário de domínio chamado hpclab\hpcuser.
3. Crie um arquivo chamado C:\cred.xml e copiar Olá RSA chave dados nele. É um arquivo de exemplo cred.xml final Olá deste artigo.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Abra um Prompt de comando e digite Olá Olá tooset credenciais dados da conta de hpclab\hpcuser de saudação do comando a seguir. Use Olá **extendeddata** toopass parâmetro hello nome de arquivo C:\cred.xml criado para dados de chave hello.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Esse comando é concluído com êxito sem resultados. Depois de definir credenciais Olá Olá para contas de usuário que é necessário toorun trabalhos, armazenar o arquivo de cred.xml Olá em um local seguro ou exclua-o.
5. Se você gerou Olá par de chaves RSA em um de seus nós do Linux, lembre-se as chaves de saudação toodelete depois de terminar de usá-los. Se o HPC Pack encontrar um arquivo id_rsa ou id_rsa.pub existente, ele não definirá uma relação de confiança mútua.

> [!IMPORTANT]
> Não é recomendável executar um trabalho de Linux como um administrador de cluster em um cluster compartilhado, porque um trabalho enviada por um administrador é executado na conta de raiz de saudação em nós do Linux hello. No entanto, um trabalho enviada por um usuário não administrador é executado sob uma conta de usuário local do Linux com hello mesmo nome como usuário do trabalho de saudação. Nesse caso, HPC Pack define a relação de confiança mútua para esse usuário do Linux em nós Olá alocadas toohello trabalho. Você pode configurar o usuário do Linux Olá manualmente em nós do Linux Olá antes de executar o trabalho de saudação ou HPC Pack cria usuário Olá automaticamente quando o trabalho de saudação é enviado. Se o HPC Pack cria usuário hello, HPC Pack excluirá Olá trabalho concluído. ameaças de segurança tooreduce, HPC Pack remove chaves Olá após a conclusão do trabalho.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configurar um compartilhamento de arquivos para nós do Linux
Agora, configure um compartilhamento SMB padrão em uma pasta no nó principal hello. tooallow Olá Linux nós tooaccess arquivos de aplicativo com um caminho comum montagem Olá compartilhados pasta em nós do Linux hello. Se desejar, você pode usar outra opção de compartilhamento de arquivos, como o compartilhamento de Arquivos do Azure - recomendado para muitos cenários - ou um compartilhamento NFS. Consulte informações e etapas detalhadas de compartilhamento de arquivo hello [começar conosco de computação do Linux em um Cluster do HPC Pack no Azure](hpcpack-cluster.md).

1. Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone Configurando os privilégios de leitura/gravação. Por exemplo, compartilhar C:\OpenFOAM no nó principal do hello como \\ \\SUSE12RDMA HN\OpenFOAM. Aqui, *SUSE12RDMA HN* é nome do host de saudação do nó principal hello.
2. Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Olá primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo de LinuxNodes hello. comando segundo Olá monta Olá compartilhado pasta //SUSE12RDMA-HN/OpenFOAM em nós do Linux Olá com dir_mode e file_mode too777 de conjunto de bits. Olá *username* e *senha* Olá comando deve ser credenciais de saudação de um usuário no nó de cabeçalho hello.

> [!NOTE]
> Olá "\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell. "\`,"significa hello"," (vírgula) é uma parte do comando hello.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Instalar o MPI e o OpenFOAM
toorun OpenFOAM como um trabalho MPI na rede RDMA Olá, é necessário toocompile OpenFOAM com bibliotecas de MPI Intel hello. 

Primeiro, execute várias **clusrun** comandos tooinstall bibliotecas de MPI Intel (se ainda não estiver instalado) e OpenFOAM em seus nós do Linux. Compartilhamento de nó principal do uso Olá configurado anteriormente arquivos de instalação de saudação tooshare entre nós do Linux hello.

> [!IMPORTANT]
> Essas etapas de instalação e compilação são exemplos. É necessário algum conhecimento dos tooensure de administração do sistema Linux bibliotecas e compiladores dependentes estão instaladas corretamente. Talvez seja necessário toomodify determinadas variáveis de ambiente ou outras configurações para suas versões do Intel MPI e OpenFOAM. Para obter detalhes, consulte [Guia de instalação do Intel MPI Library para Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) e [Instalação do OpenFOAM Source Pack](http://openfoam.org/download/2-3-1-source/) para seu ambiente.
> 
> 

### <a name="install-intel-mpi"></a>Instalar o Intel MPI
Salve pacote de instalação baixado de saudação para Intel MPI (l_mpi_p_5.0.3.048.tgz neste exemplo) em C:\OpenFoam no nó de cabeçalho Olá para que nós do Linux Olá podem acessar esse arquivo de /openfoam. Em seguida, execute **clusrun** biblioteca de MPI Intel tooinstall em todos os nós do Linux hello.

1. a seguir Olá comandos do pacote de instalação de saudação de cópia e extraia-muito/opt/intel em cada nó.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI biblioteca silenciosamente, use um arquivo silent.cfg. Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello. Coloque esse arquivo no hello compartilhados /openfoam de pasta. Para obter detalhes sobre o arquivo de silent.cfg hello, consulte [Intel MPI biblioteca para o guia de instalação do Linux - instalação silenciosa](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Salve o arquivo silent.cfg como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF). Essa etapa garante que ele seja executado corretamente em nós do Linux hello.
   > 
   > 
3. Instale a Intel MPI Library no modo silencioso.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Configurar o MPI
Para testar, você deve adicionar Olá linhas toohello /etc/security/limits.conf a seguir em cada um de nós do Linux hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Reinicie nós do Linux Olá depois de atualizar o arquivo de limits.conf hello. Por exemplo, use o seguinte Olá **clusrun** comando:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Depois de reiniciar, verifique a que pasta compartilhada hello está montada como /openfoam.

### <a name="compile-and-install-openfoam"></a>Compilar e instalar o OpenFOAM
Salve o pacote de instalação baixado de saudação para Olá tooC:\OpenFoam OpenFOAM fonte Pack (OpenFOAM 2.3.1.tgz neste exemplo) no nó de cabeçalho Olá para que nós do Linux Olá podem acessar esse arquivo de /openfoam. Em seguida, execute **clusrun** comandos Olá de toocompile OpenFOAM em todos os nós do Linux.

1. Criar uma pasta /opt/OpenFOAM em cada nó do Linux, pasta de toothis do pacote de origem de saudação cópia e extraia-o lá.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM com hello Intel MPI biblioteca, primeiro configure algumas variáveis de ambiente para Intel MPI e OpenFOAM. Use um script de bash chamado settings.sh tooset Olá variáveis. Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello. O local deste arquivo (salvo com terminações de linha do Linux) em Olá compartilhados /openfoam de pasta. Esse arquivo também contém configurações para Olá MPI OpenFOAM tempos de execução e que você use toorun posteriormente um trabalho OpenFOAM.
3. Instale pacotes dependentes necessário toocompile OpenFOAM. Dependendo da distribuição do Linux, talvez seja necessário primeiro tooadd um repositório. Executar **clusrun** comandos a seguir toohello semelhante:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Se necessário, a saudação do SSH tooeach Linux nó toorun comandos tooconfirm que são executadas corretamente.
4. Execute Olá comando toocompile OpenFOAM a seguir. o processo de compilação Olá leva algum tempo toocomplete e gera uma grande quantidade de saída de toostandard de informações de log, use Olá **/ intercaladas** opção de saída de hello toodisplay intercalada.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Olá "\`" símbolo no comando Olá é um símbolo de escape para o PowerShell. "\`&" significa Olá "&" é uma parte do comando hello.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Preparar um trabalho de OpenFOAM de toorun
Agora Obtenha pronto toorun um trabalho MPI chamado sloshingTank3D, que é um dos exemplos de OpenFoam hello, em dois nós do Linux. 

### <a name="set-up-hello-runtime-environment"></a>Configurar o ambiente de tempo de execução de saudação
tooset ambientes de tempo de execução Olá para MPI e OpenFOAM em nós do Linux hello, executados Olá comando em uma janela do Windows PowerShell a seguir no nó de cabeçalho hello. (Este comando é válido apenas para o Linux SUSE)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Preparar os dados de exemplo
Compartilhamento de nó principal do uso Olá foi configurado anteriormente tooshare arquivos entre os nós do Linux hello (montados como /openfoam).

1. Nós de computação tooone SSH do seu Linux.
2. Execute Olá após o comando tooset o ambiente de tempo de execução de OpenFOAM hello, se você ainda não tiver feito isso.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Copie a pasta compartilhada do hello sloshingTank3D exemplo toohello e navegue tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Quando você usa os parâmetros padrão Olá deste exemplo, pode levar dezenas de toorun minutos, portanto, talvez você queira toomodify toomake alguns parâmetros que ele executado mais rapidamente. Uma opção simple é toomodify Olá tempo Etapa variáveis deltaT e writeInterval no arquivo de sistema/controlDict hello. Esse arquivo armazena todos os dados de entrada relacionados toohello controle de tempo e leitura e gravação de dados da solução. Por exemplo, você pode alterar o valor de Olá de deltaT de 0,05 too0.5 e valor de saudação do writeInterval de too0.5 0,05.
   
   ![Modificar as variáveis da etapa][step_variables]
5. Especifique os valores desejados para variáveis de saudação no arquivo de sistema/decomposeParDict hello. Este exemplo usa dois nós Linux cada com 8 núcleos, portanto, definir numberOfSubdomains too16 e n hierarchicalCoeffs too(1 1 16), que significa OpenFOAM ser executados em paralelo com 16 processos. Para obter mais informações, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guia do usuário OpenFOAM: 3.4 Execução de aplicativos em paralelo).
   
   ![Decompor processos][decompose]
6. Execute Olá comandos a seguir de dados de exemplo hello sloshingTank3D directory tooprepare hello.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. No nó de cabeçalho Olá, você deve ver os arquivos de dados de exemplo hello são copiados para C:\OpenFoam\sloshingTank3D. (C:\OpenFoam é a pasta compartilhada Olá no nó de cabeçalho hello.)
   
   ![Arquivos de dados no nó principal Olá][data_files]

### <a name="host-file-for-mpirun"></a>Arquivo de host para mpirun
Nesta etapa, você criar um arquivo de host (uma lista de nós de computação) que Olá **mpirun** comando usa.

1. Em um de nós do Linux hello, crie um arquivo chamado arquivo de host em /openfoam, para que esse arquivo pode ser contatado pelo /openfoam/hostfile em todos os nós do Linux.
2. Grave os nomes dos nós do Linux nesse arquivo. Neste exemplo, o arquivo hello contém Olá nomes a seguir:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > Você também pode criar esse arquivo no C:\OpenFoam\hostfile no nó de cabeçalho hello. Se você escolher esta opção, salve-o como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF). Isso garante que ele seja executado corretamente em nós do Linux hello.
   > 
   > 
   
   **Wrapper de script bash**
   
   Se você tiver muitos nós do Linux, e você desejar toorun seu trabalho em apenas alguns deles, não é um toouse recomendável um host fixo de arquivos, porque você não sabe quais nós serão alocados tooyour trabalho. Nesse caso, grave um wrapper de script bash para **mpirun** toocreate Olá arquivo host automaticamente. Você pode encontrar um wrapper de script do exemplo bash chamado hpcimpirun.sh no final deste artigo hello e salve-o como /openfoam/hpcimpirun.sh. Esse script de exemplo hello a seguir:
   
   1. Define as variáveis de ambiente Olá para **mpirun**e alguns adição comando parâmetros toorun Olá MPI trabalho por meio da rede RDMA hello. Nesse caso, ele define Olá variáveis a seguir:
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Cria um arquivo de host de acordo com toohello variável de ambiente $CCP_NODES_CORES, que é definido por nó principal do HPC hello quando o trabalho de saudação é ativado.
      
      formato de saudação do $CCP_NODES_CORES segue este padrão:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      onde
      
      * `<Number of nodes>`-número de saudação de nós alocado toothis trabalho.  
      * `<Name of node_n_...>`-nome de saudação de cada nó alocada toothis trabalho.
      * `<Cores of node_n_...>`-Olá número de núcleos no trabalho do hello nó toothis alocado.
      
      Por exemplo, se o trabalho de saudação precisa toorun de dois nós, $CCP_NODES_CORES é semelhante a
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Saudação de chamadas **mpirun** de comando e acrescenta dois parâmetros toohello comando linha.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-Olá caminho do script de saudação do arquivo de host Olá cria
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-uma variável de ambiente definida pelo Olá HPC Pack nó principal, que armazena o número de saudação de núcleos total alocada toothis trabalho. Nesse caso, ele especifica o número de saudação de processos para **mpirun**.

## <a name="submit-an-openfoam-job"></a>Enviar um trabalho do OpenFOAM
Agora, você pode enviar um trabalho no Gerenciador de Cluster de HPC. É necessário toopass Olá script hpcimpirun.sh nas linhas de comando Olá para algumas das tarefas de trabalho hello.

1. Conecte-se o nó principal do cluster tooyour e iniciar o Gerenciador de Cluster de HPC.
2. **No gerenciamento de recursos**, verifique se nós de computação Olá Linux estão em Olá **Online** estado. Se não estiverem, selecione-os e clique em **Colocar Online**.
3. Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.
4. Insira um nome para o trabalho, como *sloshingTank3D*.
   
   ![Detalhes do trabalho][job_details]
5. Em **recursos de trabalho**, escolha o tipo de saudação do recurso como "Nó" e defina Olá mínimo too2. Essa configuração executa o trabalho de saudação em dois nós do Linux, cada um deles tem oito núcleos neste exemplo.
   
   ![Recursos de trabalho][job_resources]
6. Clique em **editar tarefas** Olá navegação esquerdo e, em seguida, clique em **adicionar** tooadd um trabalho de toohello de tarefa. Adicionar quatro tarefas toohello trabalho Olá linhas de comando e as configurações a seguir.
   
   > [!NOTE]
   > Executando `source /openfoam/settings.sh` configura ambientes de tempo de execução de OpenFOAM e MPI da saudação, para cada uma das seguintes tarefas de saudação chamá-lo antes de saudação OpenFOAM comando.
   > 
   > 
   
   * **Tarefa 1**. Executar **decomposePar** toogenerate arquivos de dados para a execução **interDyMFoam** em paralelo.
     
     * Atribuir uma tarefa de toohello de nó
     * **Linha de comando** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Diretório de trabalho** - /openfoam/sloshingTank3D
     
     Consulte Olá figura a seguir. Você pode configurar as tarefas restantes Olá da mesma forma.
     
     ![Detalhes da tarefa 1][task_details1]
   * **Tarefa 2**. Executar **interDyMFoam** no exemplo de hello toocompute paralela.
     
     * Atribuir tarefas de toohello dois nós
     * **Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Diretório de trabalho** - /openfoam/sloshingTank3D
   * **Tarefa 3**. Executar **reconstructPar** toomerge Olá conjuntos dos diretórios de tempo de cada diretório processor_N_ em um único conjunto.
     
     * Atribuir uma tarefa de toohello de nó
     * **Linha de comando** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Diretório de trabalho** - /openfoam/sloshingTank3D
   * **Tarefa 4**. Executar **foamToEnsight** em paralelo tooconvert arquivos de resultado Olá OpenFOAM em EnSight formatar em colocar arquivos de EnSight de saudação em um diretório chamado Ensight no diretório caso hello.
     
     * Atribuir tarefas de toohello dois nós
     * **Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Diretório de trabalho** - /openfoam/sloshingTank3D
7. Adicione tarefas de toothese dependências na tarefa ordem crescente.
   
   ![Dependências da tarefa][task_dependencies]
8. Clique em **enviar** toorun esse trabalho.
   
   Por padrão, o HPC Pack envia trabalho hello como sua conta de logon do usuário atual. Depois de clicar em **enviar**, você verá uma caixa de diálogo solicitando que você tooenter Olá nome e uma senha.
   
   ![Credenciais de trabalho][creds]
   
   Sob algumas condições, o HPC Pack lembra informações de usuário de saudação antes de entrada e não mostrar esta caixa de diálogo. toomake HPC Pack mostrá-la novamente, insira Olá comando no prompt de comando a seguir e, em seguida, enviar o trabalho de saudação.
   
   ```
   hpccred delcreds
   ```
9. trabalho de saudação leva de dezenas de minutos tooseveral horas de acordo com os parâmetros de toohello que você definiu para o exemplo hello. Mapa de calor hello, você verá trabalho Olá em execução em nós do Linux hello. 
   
   ![Mapa de calor][heat_map]
   
   Em cada nó, oito processos são iniciados.
   
   ![Processos do Linux][linux_processes]
10. Quando termina de trabalho hello, localize resultados do trabalho Olá nas pastas C:\OpenFoam\sloshingTank3D e os arquivos de log de saudação em C:\OpenFoam.

## <a name="view-results-in-ensight"></a>Exibir resultados no EnSight
Opcionalmente, use [EnSight](https://www.ceisoftware.com/) toovisualize e analisar os resultados de saudação do trabalho de OpenFOAM hello. Para obter mais informações sobre a visualização e a animação no EnSight, consulte o [guia em vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Depois de instalar EnSight no nó principal do hello, inicie-o.
2. Abra o C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Você verá um tanque no Visualizador de saudação.
   
   ![Tanque no EnSight][tank]
3. Criar um **Isosurface** de **internalMesh**e, em seguida, escolha variável Olá **alpha_water**.
   
   ![Criar um isosurface][isosurface]
4. Definir cor Olá para **Isosurface_part** criado na etapa anterior hello. Por exemplo, defina-toowater azul.
   
   ![Editar cor do isosurface][isosurface_color]
5. Criar um **volume Iso** de **paredes** selecionando **paredes** em Olá **partes** painel e clique em Olá **Isosurfaces**  botão na barra de ferramentas de saudação.
6. Na caixa de diálogo hello, selecione **tipo** como **Isovolume** e defina Olá Min de **Isovolume intervalo** too0.5. toocreate Olá isovolume, clique em **criar com partes selecionadas**.
7. Definir cor Olá para **Iso_volume_part** criado na etapa anterior hello. Por exemplo, defina-água toodeep azul.
8. Definir cor Olá para **paredes**. Por exemplo, defina-tootransparent branco.
9. Agora clique **reproduzir** toosee resultados de saudação de simulação de saudação.
   
    ![Resultado do tanque][tank_result]

## <a name="sample-files"></a>Arquivos de exemplo
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Exemplo silent.cfg arquivo tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Script settings.sh de exemplo
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Script hpcimpirun.sh de exemplo
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
