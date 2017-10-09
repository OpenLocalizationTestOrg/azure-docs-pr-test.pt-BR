---
title: "aaaLinux de computação VMs em um cluster de HPC Pack | Microsoft Docs"
description: "Saiba como toocreate e usar um pacote de HPC cluster no Azure para cargas de trabalho (HPC) de computação de alto e desempenho do Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Introdução a nós de computação Linux em um cluster de HPC Pack no Azure
Configure um cluster do [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) no Azure que contenha um nó de cabeçalho que executa o Windows Server e vários nós de computação que executam uma distribuição do Linux com suporte. Explore opções toomove dados entre nós do Linux hello e o nó principal do Windows de saudação do cluster de saudação. Saiba como toosubmit Linux HPC trabalhos toohello cluster.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Em um nível alto, hello diagrama a seguir mostra o cluster de HPC Pack Olá criar e trabalhar com.

![Cluster HPC Pack com nós Linux][scenario]

Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para o lote e computação de alto desempenho](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Implantar um cluster de HPC Pack com nós de computação Linux
Este artigo mostra duas opções toodeploy um cluster de HPC Pack no Azure conosco de computação do Linux. Ambos os métodos usam uma imagem do Marketplace do Windows Server com o nó principal do HPC Pack toocreate hello. 

* **Modelo do Gerenciador de recursos do Azure** -usar um modelo de saudação do Azure Marketplace ou um modelo de início rápido da comunidade hello, tooautomate criação de cluster de saudação no modelo de implantação do Gerenciador de recursos de saudação. Por exemplo, Olá [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no hello Azure Marketplace cria uma infraestrutura completa de cluster de HPC Pack para Linux HPC cargas de trabalho.
* **Script do PowerShell** -Olá Use [script de implantação do Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate uma implantação completa de cluster no modelo de implantação clássico hello. Este script do PowerShell do Azure usa uma imagem de VM do HPC Pack em hello Azure Marketplace para implantação rápida e fornece um conjunto abrangente de toodeploy de parâmetros de configuração de nós de computação do Linux.

Para obter mais informações sobre as opções de implantação de cluster de HPC Pack no Azure, consulte [opções toocreate e gerenciar um cluster de computação de alto desempenho (HPC) no Azure com Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Pré-requisitos
* **Assinatura do Azure** -você pode usar uma assinatura em qualquer serviço Global Azure ou Azure China hello. Se você não tem uma conta, pode criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* **Cota de núcleos** -você pode precisar de uma cota de Olá tooincrease de núcleos, especialmente se você escolher toodeploy vários nós de cluster com tamanhos VM com vários núcleos. tooincrease uma cota, abra uma solicitação de suporte do cliente online sem custo adicional.
* **Distribuições do Linux** -atualmente HPC Pack suporta Olá distribuições do Linux para nós de computação a seguir. Você pode usar as versões do Marketplace dessas distribuições quando disponíveis ou fornecer as suas próprias.
  
  * **Com base em centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, HPC 6.5, HPC 7.1
  * **Red Hat Enterprise Linux**: 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC, SLES 12 para HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > rede de RDMA do Azure Olá toouse com um dos tamanhos de VM Olá compatíveis com RDMA, especifique uma imagem do SUSE Linux Enterprise Server 12 HPC ou com base em CentOS HPC de saudação do Azure Marketplace. Para obter mais informações, consulte [Tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Cluster de saudação pré-requisitos adicionais toodeploy usando o script de implantação de IaaS do HPC Pack hello:

* **Computador cliente** -você precisa de um script de implantação do cliente com base em Windows computador toorun Olá cluster.
* **Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Você pode verificar a versão de saudação do script hello executando `.\New-HPCIaaSCluster.ps1 –Version`. Este artigo se baseia na versão 4.4.1 ou posterior do script hello.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Opção de implantação 1. Use um modelo do Resource Manager
1. Vá toohello [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no hello Azure Marketplace e clique em **implantar**.
2. Olá portal do Azure, examinar as informações de saudação e, em seguida, clique em **criar**.
   
    ![Criação de portal][portal]
3. Em Olá **Noções básicas sobre** folha, insira um nome para o cluster de saudação, que também nomeia a VM do nó principal hello. Você pode escolher um grupo de recursos existente ou crie um grupo para a implantação de saudação em um local que é tooyou disponível. Hello local afeta a disponibilidade de saudação de determinados tamanhos de VM e outros serviços do Azure (consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/)).
4. Em Olá **configurações do nó de cabeçalho** folha, para uma implantação primeiro, você pode aceitar as configurações padrão de saudação. 
   
   > [!NOTE]
   > Olá **script pós-configuração URL** é uma configuração opcional toospecify um script do Windows PowerShell publicamente disponível que você deseja toorun na VM do nó principal Olá depois que ele está em execução. 
   > 
   > 
5. Em Olá **configurações de nós de computação** folha, selecione um padrão de nomeação de nós hello, o número de saudação e o tamanho de nós de saudação e Olá toodeploy de distribuição do Linux.
6. Em Olá **definições de infraestrutura** folha, insira os nomes de rede virtual hello e Active Directory domínio, domínio e as credenciais de administrador VM e um padrão de nomeação para as contas de armazenamento de saudação.
   
   > [!NOTE]
   > HPC Pack usa os usuários de cluster tooauthenticate de domínio do Active Directory hello. 
   > 
   > 
7. Depois de executar testes de validação de saudação e revise os termos de uso do hello, clique em **compra**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Opção de implantação 2. Usar script de implantação IaaS Olá
Estes são os cluster de saudação toodeploy pré-requisitos adicionais usando o script de implantação de IaaS do HPC Pack Olá:

* **Computador cliente** -você precisa de um script de implantação do cliente com base em Windows computador toorun Olá cluster.
* **Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Você pode verificar a versão de saudação do script hello executando `.\New-HPCIaaSCluster.ps1 –Version`. Este artigo se baseia na versão 4.4.1 ou posterior do script hello.

**Arquivo de configuração XML**

Olá script de implantação IaaS do HPC Pack usa um arquivo de configuração XML como cluster HPC Olá toodescribe de entrada. Olá seguinte arquivo de configuração de exemplo especifica um pequeno cluster consiste em um nó principal do HPC Pack e dois nós de computação do tamanho A7 CentOS 7.0 Linux. 

Modificar arquivo hello conforme necessário para seu ambiente e a configuração de cluster desejado e salve-o com um nome como HPCDemoConfig.xml. Por exemplo, você precisa toosupply nome da sua assinatura e um nome de conta de armazenamento exclusivo e o nome do serviço de nuvem. Além disso, talvez você queira toochoose outro suporte para a imagem do Linux para nós de computação hello. Para obter mais informações sobre elementos Olá no arquivo de configuração hello, consulte o arquivo de Manual.rtf Olá na pasta de script hello e [criar um cluster HPC com hello script de implantação IaaS do HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**Olá toorun script de implantação IaaS do HPC Pack**

1. Abra o Windows PowerShell como administrador no computador do cliente de saudação.
2. Alterar pasta de toohello de diretório em que o script hello está instalado (E:\IaaSClusterScript neste exemplo).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Execute Olá cluster de HPC Pack de saudação do comando toodeploy a seguir. Este exemplo supõe que esse arquivo de configuração hello está localizado em E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Porque Olá **AdminPassword** não for especificado Olá antes do comando, você é tooenter solicitadas senha de saudação do usuário *MyAdminName*.
   
    b. script Hello, em seguida, inicia o arquivo de configuração toovalidate hello. Pode demorar até tooseveral minutos dependendo da conexão de rede de saudação.
   
    ![Validação][validate]
   
    c. Depois de passarem validações, script hello lista Olá toocreate de recursos de cluster. Digite *Y* toocontinue.
   
    ![Recursos][resources]
   
    d. script Hello inicia o cluster de HPC Pack toodeploy hello e conclui a configuração de saudação sem mais etapas manuais. Olá script pode ser executado por vários minutos.
   
    ![Implantar][deploy]
   
   > [!NOTE]
   > Neste exemplo, script hello gera um arquivo de log automaticamente desde Olá **- arquivo de log** parâmetro não for especificado. Olá logs não são gravados em tempo real, mas são coletados no final de saudação de validação de saudação e implantação de saudação. Se Olá PowerShell processo for interrompido enquanto o script hello está sendo executado, alguns logs serão perdidos.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Conecte-se o nó principal toohello
Depois de implantar o cluster de HPC Pack Olá no Azure, [conectar por área de trabalho remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nó principal VM usando Olá credenciais de domínio fornecido quando você implantou o cluster hello (por exemplo, *hpc\\ clusteradmin*). Você gerencia o cluster de saudação do nó principal hello.

No nó de cabeçalho hello, inicie toocheck do Gerenciador de Cluster de HPC status de saudação do cluster de HPC Pack hello. Você pode gerenciar e monitorar nós de computação Linux hello mesma maneira que trabalha com o Windows nós de computação. Por exemplo, você verá que nós do Linux Olá listados no **gerenciamento de recursos** (esses nós são implantados com hello **LinuxNode** modelo).

![Gerenciamento de nós][management]

Você também ver nós Linux Olá Olá **mapa de calor** exibição.

![Mapa de calor][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Como toomove dados em um cluster conosco do Linux
Você tem vários dados de toomove opções entre nós do Linux e o nó principal do Windows de saudação do cluster de saudação. Aqui estão os três métodos comuns, descritos mais detalhadamente Olá seções a seguir:

* **Arquivo do Azure** -expõe um toostore dados gerenciados do SMB arquivo compartilhamento de arquivos no armazenamento do Azure. Nós do Windows e Linux pode montar um compartilhamento de arquivos do Azure como uma unidade ou pasta em Olá a mesma hora, mesmo se eles são implantados em redes virtuais diferentes.
* **Nó de cabeçalho SMB compartilhar** -monta uma pasta compartilhada do Windows padrão do nó principal Olá em nós do Linux.
* **Servidor NFS do nó de cabeçalho** – fornece uma solução de compartilhamento de arquivos para um ambiente misto do Windows e do Linux.

### <a name="azure-file-storage"></a>Armazenamento de arquivos do Azure
Olá [arquivo Azure](https://azure.microsoft.com/services/storage/files/) serviço expõe os compartilhamentos de arquivos usando o protocolo SMB 2.1 padrão de saudação. Serviços de nuvem e VMs do Azure podem compartilhar dados de arquivo entre componentes de aplicativos por meio de compartilhamentos montados e aplicativos locais podem acessar dados de arquivo em um compartilhamento de por meio de saudação API de armazenamento de arquivo. 

Para etapas detalhadas toocreate um arquivo do Azure compartilham e recriá-lo no nó de cabeçalho hello, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../../../storage/files/storage-how-to-use-files-windows.md). compartilhamento de arquivo do Azure Olá toomount em nós do Linux hello, consulte [como toouse armazenamento de arquivo do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md). tooset as conexões persistentes, consulte [Persisting conexões tooMicrosoft arquivos do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

Em Olá exemplo a seguir, crie um compartilhamento de arquivos do Azure em uma conta de armazenamento. Olá toomount compartilhamento no nó principal hello, abra um Prompt de comando e digite Olá comandos a seguir:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

Neste exemplo, allvhdsje é o nome da sua conta de armazenamento, storageaccountkey é a chave da conta de armazenamento e o rdma é o nome de compartilhamento de arquivo do Azure hello. compartilhamento de arquivo do Azure Olá está montado como z no nó de cabeçalho hello.

compartilhamento de arquivo do Azure Olá toomount em nós do Linux, execute um **clusrun** comando no nó de cabeçalho hello. **[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  é um toocarry de ferramenta do HPC Pack útil tarefas administrativas em vários nós. (Consulte também [Clusrun para nós Linux](#Clusrun-for-Linux-nodes) neste artigo.)

Abra uma janela do Windows PowerShell e digite Olá comandos a seguir:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Olá primeiro comando cria uma pasta chamada /rdma em todos os nós no grupo de LinuxNodes hello. comando segundo Olá monta hello Azure arquivo compartilhamento allvhdsjw.file.core.windows.net/rdma para pasta de /rdma Olá com too777 de conjunto de bits modo dir e arquivo. No segundo comando de hello, allvhdsje é o nome da sua conta de armazenamento e storageaccountkey é a chave da conta de armazenamento.

> [!NOTE]
> Olá "\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell. "\`,"significa que hello"," (vírgula) é uma parte do comando hello.
> 
> 

### <a name="head-node-share"></a>Compartilhamento do nó principal
Como alternativa, monte uma pasta compartilhada de nó principal Olá em nós do Linux. Um compartilhamento fornece arquivos de tooshare de maneira mais simples do hello, mas nó principal hello e todos os nós do Linux devem ser implantados em Olá mesma rede virtual. Aqui estão as etapas de saudação.

1. Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone com permissões de leitura/gravação. Por exemplo, compartilhar D:\OpenFOAM no nó principal do hello como \\CentOS7RDMA HN\OpenFOAM. Aqui HN CentOS7RDMA é o nome de host de saudação do nó principal hello.
   
    ![Permissões de compartilhamento de arquivo][fileshareperms]
   
    ![Compartilhamento de arquivos][filesharing]
2. Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Olá primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo de LinuxNodes hello. comando segundo Olá monta Olá compartilhado pasta //CentOS7RDMA-HN/OpenFOAM na pasta Olá com dir e arquivo too777 de conjunto de bits de modo. Olá username e password no comando Olá devem ser Olá nome de usuário e senha de um usuário de cluster no nó principal hello. (Confira [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx)).

> [!NOTE]
> Olá "\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell. "\`,"significa que hello"," (vírgula) é uma parte do comando hello.
> 
> 

### <a name="nfs-server"></a>Servidor NFS
Olá serviço NFS permite tooshare e migra arquivos entre computadores que executam o sistema operacional de saudação do Windows Server 2012 usando o protocolo SMB de saudação e computadores baseados em Linux usando o protocolo NFS de saudação. Olá servidor NFS e todos os outros nós têm toobe implantado em Olá mesma rede virtual. Ele fornece a melhor compatibilidade com nós do Linux em comparação com um compartilhamento SMB. Por exemplo, ele dá suporte a links de arquivo.

1. tooinstall e configurar um servidor NFS, siga as etapas de saudação em [servidor para compartilhamento primeiro do sistema de arquivos de rede ponta a ponta](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Por exemplo, crie um compartilhamento NFS chamado nfs com hello propriedades a seguir:
   
    ![Autorização de NFS][nfsauth]
   
    ![Permissões de compartilhamento NFS][nfsshare]
   
    ![Permissões de compartilhamento NFS NTFS][nfsperm]
   
    ![Propriedades de gerenciamento de NFS][nfsmanage]
2. Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Olá primeiro comando cria uma pasta chamada /nfsshared em todos os nós no grupo de LinuxNodes hello. saudação de montagens segundo comando NFS Hello compartilhar HN CentOS7RDMA: / nfs em Olá pasta. Aqui CentOS7RDMA HN: nfs é o caminho remoto de saudação do seu compartilhamento NFS.

## <a name="how-toosubmit-jobs"></a>Como toosubmit trabalhos
Há um cluster de HPC Pack do várias maneiras toosubmit trabalhos toohello:

* Gerenciador de Cluster HPC ou GUI do Gerenciador de Trabalhos HPC
* Portal da Web do HPC
* API REST

Envio de trabalho cluster toohello no Azure por meio de ferramentas de GUI do HPC Pack e o portal da web hello HPC estão Olá mesmo para nós de computação do Windows. Consulte [Gerenciador de trabalhos do HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [como toosubmit trabalhos de um computador de cliente local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

trabalhos toosubmit via Olá API REST, consulte muito[criando e enviando trabalhos usando Olá API REST do Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). toosubmit trabalhos de um cliente do Linux, consulte exemplo de Python toohello Olá também [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun para nós Linux
Olá HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) ferramenta pode ser usada tooexecute comandos em nós do Linux por meio de um Prompt de comando ou o Gerenciador de Cluster de HPC. Veja alguns exemplos básicos.

* Mostre nomes de usuário atuais em todos os nós no cluster de saudação.
  
    ```command
    clusrun whoami
    ```
* Instalar Olá **gdb** ferramenta de depuração com **yum** em todos os nós Olá linuxnodes grupo e, em seguida, reinicie nós de saudação após 10 minutos.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Criar um script de shell exibindo cada número de 1 a 10 para um segundo em cada nó do Linux no cluster hello, executá-lo e Mostrar saída de nós Olá imediatamente.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Talvez seja necessário toouse certos caracteres de escape **clusrun** comandos. Conforme mostrado neste exemplo, usar ^ em uma saudação do Prompt de comando tooescape ">" símbolo.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Tente expansão Olá cluster tooa maior número de nós, ou executando uma carga de trabalho do Linux no cluster hello. Para ver um exemplo, confira [Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md).
* Tente um cluster com [compatíveis com RDMA, com uso intensivo de computação VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun cargas de trabalho MPI. Para ver um exemplo, confira [Executar o OpenFOAM com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure](hpcpack-cluster-openfoam.md).
* Se você estiver interessado em trabalhar com nós do Linux em um cluster de HPC Pack no local, consulte Olá [orientação da TechNet](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
