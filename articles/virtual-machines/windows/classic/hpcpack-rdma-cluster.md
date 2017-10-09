---
title: aaaSet um aplicativos do Windows RDMA cluster toorun MPI | Microsoft Docs
description: "Saiba como um cluster do Windows HPC Pack com toouse H16r, H16mr, A8 ou A9 VMs de tamanho de toocreate Olá aplicativos MPI de toorun de rede RDMA do Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Configurar um cluster do Windows RDMA com aplicativos de MPI toorun HPC Pack
Configurar um cluster do Windows RDMA no Azure com [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) e [tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun aplicativos de Interface MPI (Message Passing) paralelos. Quando você configura nós compatíveis com RDMA baseados no Windows Server em um cluster de Pacote HPC, os aplicativos MPI se comunicam de modo eficiente por uma rede de baixa latência e alta taxa de transferência baseada na tecnologia RDMA (acesso remoto direto à memória).

Se você quiser toorun cargas de trabalho MPI em VMs do Linux rede acesso Olá RDMA do Azure, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Opções de implantação do cluster do Pacote HPC
Microsoft HPC Pack é uma ferramenta fornecida em nenhum custo adicional toocreate HPC clusters local ou no Azure toorun Windows ou os aplicativos de HPC do Linux. HPC Pack inclui um ambiente de tempo de execução para a implementação da Microsoft de saudação do hello mensagem passando Interface para Windows (MS-MPI). Quando usado com compatíveis com RDMA instâncias executando um sistema de operacional com suporte do Windows Server, o HPC Pack fornece um aplicativo de Windows MPI toorun opção eficiente rede acesso Olá RDMA do Azure. 

Este artigo apresenta dois cenários e links toodetailed orientação tooset um cluster do Windows RDMA com Microsoft HPC Pack. 

* Cenário 1. Implantar instâncias de função de trabalho de computação intensiva (PaaS)
* Cenário 2: Implantar nós de computação em VMs de computação intensiva (IaaS)

Para instâncias de computação intensiva toouse de pré-requisitos gerais com o Windows, consulte [tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Cenário 1: Implantar instâncias de função de trabalho de computação intensiva (PaaS)
Em um cluster existente do HPC Pack, adicione recursos de computação extras nas instâncias de função de trabalho do Azure (nós do Azure) em execução em um serviço de nuvem (PaaS). Esse recurso, também chamado de "intermitência tooAzure" do HPC Pack suporta uma variedade de tamanhos para instâncias de função de trabalho hello. Ao adicionar hello nós do Azure, especifique um dos tamanhos de saudação compatíveis com RDMA.

A seguir está considerações e etapas tooburst tooRDMA compatíveis com instâncias do Azure de uma já existente (normalmente no local) cluster. Use semelhante procedimentos tooadd trabalho função instâncias tooan HPC Pack nó principal que é implantado em uma VM do Azure.

> [!NOTE]
> Para um tooAzure tooburst tutorial com o HPC Pack, consulte [configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Observe as considerações Olá Olá seguindo as etapas que se aplicam especificamente nós do Azure compatíveis com tooRDMA.
> 
> 

![Intermitência tooAzure][burst]

### <a name="steps"></a>Etapas
1. **Implantar e configurar um nó de cabeçalho do HPC Pack 2012 R2**
   
    Baixar pacote de instalação HPC Pack mais recente de saudação do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Para requisitos e instruções tooprepare para uma implantação de disparo do Azure, consulte [disparar tooAzure instâncias de trabalho com o Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).
2. **Configurar um certificado de gerenciamento no hello assinatura do Azure**
   
    Configure uma conexão de saudação do certificado toosecure entre o nó principal hello e o Azure. Para opções e procedimentos, consulte [Olá tooConfigure de cenários certificado de gerenciamento do Azure para o HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). Para implantações de teste, o HPC Pack instala um certificado padrão de Microsoft HPC Azure gerenciamento rapidamente, você pode carregar tooyour assinatura do Azure.
3. **Criar um novo serviço de nuvem e uma conta de armazenamento**
   
    Use Olá toocreate portal do Azure de um serviço de nuvem e uma conta de armazenamento para implantação de saudação em uma região onde as instâncias de saudação compatíveis com RDMA estejam disponíveis.
4. **Criar um modelo de nó do Azure**
   
    Use Olá criar Assistente de modelo de nó no Gerenciador de Cluster de HPC. Para obter as etapas, consulte [criar um modelo de nó do Azure](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) em "Etapas tooDeploy nós do Azure com Microsoft HPC Pack".
   
    Para testes iniciais, sugerimos configurar uma política de disponibilidade manual no modelo de saudação.
5. **Adicionar nós toohello cluster**
   
    Use o Assistente para adicionar nó de saudação no Gerenciador de Cluster de HPC. Para obter mais informações, consulte [toohello adicionar nós do Azure Windows HPC Cluster](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Ao especificar o tamanho de saudação de nós Olá, selecione um dos tamanhos de instância compatível com RDMA hello.
   
   > [!NOTE]
   > Em cada implantação de tooAzure intermitente com instâncias de computação intensiva hello, HPC Pack implanta automaticamente um mínimo de duas instâncias compatíveis com RDMA (como A8) como nós de proxy, além de toohello instâncias de função de trabalho do Azure que você especificar. nós de proxy de saudação usam núcleos que estão alocados toohello assinatura e incorrer em encargos juntamente com instâncias de função de trabalho do Azure hello.
   > 
   > 
6. **Iniciar (provisionar) Olá nós e colocá-los online toorun trabalhos**
   
    Selecionar nós hello e usar Olá **iniciar** ação no Gerenciador de Cluster de HPC. Quando o provisionamento for concluído, selecione nós hello e use Olá **colocar Online** ação no Gerenciador de Cluster de HPC. nós de saudação são trabalhos toorun pronto.
7. **Cluster de toohello trabalhos de envio**
   
   Use ferramentas de envio do HPC Pack trabalho toorun cluster trabalhos. Consulte [Microsoft HPC Pack: gerenciamento de trabalhos](http://technet.microsoft.com/library/jj899585.aspx).
8. **Pare (desprovisione) Olá nós**
   
   Quando você terminar de executar trabalhos, coloque nós de saudação offline e usar Olá **parar** ação no Gerenciador de Cluster de HPC.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Cenário 2: Implantar nós de computação em VMs de computação intensiva (IaaS)
Nesse cenário, você implantar o nó principal do HPC Pack hello e nós de computação de cluster em máquinas virtuais em uma rede virtual do Azure. O HPC Pack fornece várias [opções de implantação em VMs do Azure](../../linux/hpcpack-cluster-options.md), incluindo scripts de implantação automatizada e modelos de início rápido do Azure. Por exemplo, Olá seguintes considerações e etapas guiá-lo Olá toouse [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) para automatizar a implantação de saudação de um cluster de HPC Pack 2012 R2 no Azure.

![Cluster em VMs do Azure][iaas]

### <a name="steps"></a>Etapas
1. **Criar um nó principal do cluster e VMs do nó de computação, executando o script de implantação de IaaS do HPC Pack Olá em um computador cliente**
   
    Baixar o pacote de Script de implantação de IaaS do HPC Pack de saudação do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    computador de cliente Olá tooprepare, criar o arquivo de configuração do script hello e script de execução hello, consulte [criar um Cluster de HPC com hello script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md). 
   
    nós de computação toodeploy compatíveis com RDMA, Olá Observação considerações adicionais a seguir:
   
   * **Rede virtual**: Especifique uma nova rede virtual em uma região na qual Olá compatíveis com RDMA tamanho da instância que você deseja toouse está disponível.
   * **Sistema operacional Windows Server**: toosupport conectividade RDMA, especifique um sistema operacional Windows Server 2012 R2 ou Windows Server 2012 para VMs do nó de computação hello.
   * **Serviços de nuvem**: é recomendável implantar o nó de cabeçalho em um serviço de nuvem e seus nós de computação em outro serviço de nuvem.
   * **Tamanho de nó de cabeçalho**: para este cenário, considere um tamanho de pelo menos A4 (Extra grande) para o nó principal hello.
   * **Extensão HpcVmDrivers**: Olá script de implantação instala hello Azure VM Agent e Olá extensão HpcVmDrivers automaticamente quando você implanta nós de computação A8 ou A9 de tamanho com um sistema operacional Windows Server. HpcVmDrivers instala drivers em VMs do nó de computação Olá para que eles possam se conectar a rede RDMA toohello. Nas VMs da série H compatíveis com RDMA, você deve instalar manualmente a extensão HpcVmDrivers de saudação. Consulte [Tamanhos de VM de computação de alto desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Configuração de rede de cluster**: o script de implantação Olá define automaticamente o cluster de HPC Pack Olá na topologia 5 (todos os nós na rede da empresa de saudação). Essa topologia é necessária para todas as implantações de cluster de HPC Pack em VMs. Não altere topologia de rede de cluster hello mais tarde.
2. **Coloque os nós de computação de Olá trabalhos toorun online**
   
    Selecionar nós hello e usar Olá **colocar Online** ação no Gerenciador de Cluster de HPC. nós de saudação são trabalhos toorun pronto.
3. **Cluster de toohello trabalhos de envio**
   
    Conectar-se toohello trabalhos de toosubmit de nó principal ou configurar um toodo do computador local, isso. Para obter informações, consulte [tooan enviar trabalhos HPC cluster no Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Take Olá nós off-line e pare (desaloque)-los**
   
    Quando você terminar de executar trabalhos, coloque a nós de saudação offline no Gerenciador de Cluster de HPC. Em seguida, use tooshut de ferramentas de gerenciamento do Azure-las para baixo.

## <a name="run-mpi-applications-on-hello-cluster"></a>Executar aplicativos MPI no cluster Olá
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Exemplo: executar mpipingpong em um cluster do HPC Pack
tooverify uma implantação do HPC Pack de instâncias de saudação compatíveis com RDMA, execute Olá HPC Pack **mpipingpong** comando cluster hello. **MPIPingPong** envia pacotes de dados entre nós emparelhados repetidamente toocalculate medições de latência e taxa de transferência e estatísticas de rede de saudação de aplicativos habilitados para RDMA. Este exemplo mostra um padrão comum para a execução de um trabalho MPI (nesse caso, **mpipingpong**) usando o cluster Olá **mpiexec** comando.

Este exemplo presume que você adicionou nós do Azure em uma configuração "disparar tooAzure" ([cenário 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Se você implantou o HPC Pack em um cluster de máquinas virtuais do Azure, será necessário toomodify Olá comando sintaxe toospecify um grupo de nó diferente e definir a rede RDMA toohello de tráfego rede de toodirect variáveis de ambiente adicionais.

toorun mpipingpong no cluster hello:

1. No nó de cabeçalho hello, ou em um computador cliente configurado corretamente, abra um Prompt de comando.
2. tooestimate latência entre pares de nós em uma implantação de disparo do Azure de quatro nós, Olá tipo comando toosubmit mpipingpong de toorun um trabalho com um tamanho de pacote pequeno e muitas iterações a seguir:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    comando Olá retorna a ID de saudação do trabalho de saudação que é enviado.
   
    Se você implantou o cluster de HPC Pack Olá implantado em VMs do Azure, especifique um grupo de nó que contém implantadas em um único serviço de nuvem de VMs do nó de computação e modificar Olá **mpiexec** comando da seguinte maneira:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Quando o trabalho de saudação for concluído, tooview Olá saída (nesse caso, saída de saudação da tarefa 1 do trabalho de saudação), Olá tipo a seguir
   
    ```Command
    task view <JobID>.1
    ```
   
    onde &lt; *JobID* &gt; é Olá ID do trabalho de saudação que foi enviado.
   
    saída de Hello inclui procedimentos de toohello latência resultados semelhantes.
   
    ![Latência ping pong][pingpong1]
4. nós de disparo tooestimate a taxa de transferência entre pares do Azure, digite o seguinte Olá comando toosubmit toorun um trabalho **mpipingpong** com um tamanho de pacote grande e algumas iterações:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    comando Olá retorna a ID de saudação do trabalho de saudação que é enviado.
   
    Em um cluster de HPC Pack implantado em VMs do Azure, modifique o comando Olá conforme observado na etapa 2.
5. Quando o trabalho de saudação for concluído, tooview Olá saída (nesse caso, saída de saudação da tarefa 1 do trabalho de saudação), Olá tipo a seguir:
   
    ```Command
    task view <JobID>.1
    ```
   
   saída de Hello inclui procedimentos de toohello taxa de transferência resultados semelhantes.
   
   ![Taxa de transferência de ping pong][pingpong2]

### <a name="mpi-application-considerations"></a>Considerações de aplicativos MPI
A seguir, as considerações para execução de aplicativos MPI com HPC Pack no Azure. Alguns se aplicam apenas toodeployments de nós do Azure (instâncias de função trabalho adicionadas em uma configuração de "intermitência tooAzure").

* As instâncias de função de trabalho em um serviço de nuvem são reprovisionadas periodicamente sem aviso pelo Azure (por exemplo, para manutenção do sistema ou no caso de uma instância falhar). Se uma instância for reprovisionada enquanto ele está em execução em um trabalho MPI, Olá perder seus dados e retorna o estado de toohello quando ela foi implantada pela primeira vez, que pode causar toofail de trabalho MPI hello. Hello mais nós que você usa para um único trabalho MPI e hello mais hello trabalho é executado, hello mais provável que uma das instâncias de saudação for reprovisionada enquanto um trabalho está em execução. Considere também o seguinte se você designar um único nó na implantação hello como um servidor de arquivos.
* toorun trabalhos MPI no Azure, você não tem instâncias do toouse Olá compatíveis com RDMA. Você pode usar qualquer tamanho de instância que tenha o suporte do HPC Pack. No entanto, instâncias compatíveis com RDMA Olá são recomendadas para executar trabalhos MPI relativamente de grande escala que são confidenciais toohello latência e largura de banda de saudação da rede Olá que conecta nós de saudação. Se você usar outros trabalhos MPI tamanhos toorun sensíveis à latência e largura de banda, recomendamos executar trabalhos pequenos, nos quais uma única tarefa é executada em apenas alguns nós.
* Aplicativos implantados tooAzure instâncias são toohello da entidade associados ao aplicativo hello de termos de licenciamento. Verifique com o fornecedor de saudação de qualquer aplicativo comercial para licenciamento ou outras restrições de execução na nuvem hello. Nem todos os fornecedores oferecem licenciamento pré-pago.
* Instâncias do Azure precisam configurar ainda mais nós do tooaccess locais, compartilhamentos e servidores de licença. Por exemplo, Olá tooenable nós do Azure tooaccess um servidor de licença local, você pode configurar uma rede virtual do Azure de site a site.
* toorun aplicativos de MPI em instâncias do Azure, registrar cada aplicativo MPI com o Firewall do Windows em instâncias de saudação executando Olá **hpcfwutil** comando. Isso permite que o local de tootake comunicações MPI em uma porta atribuída dinamicamente pelo firewall hello.
  
  > [!NOTE]
  > Para implantações de tooAzure intermitente, você também pode configurar um toorun de comando de exceção de firewall automaticamente em todos os nós do Azure que são adicionados tooyour cluster. Depois de executar Olá **hpcfwutil** de comando e verifique se que o aplicativo funciona, adicione o script de inicialização do hello comando tooa para seus nós do Azure. Para obter mais informações, consulte [Usar um script de inicialização para nós do Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack usa toospecify de variável ambiente um intervalo de endereços aceitáveis de cluster CCP_MPI_NETMASK Olá para comunicação MPI. A partir do HPC Pack 2012 R2, variável de ambiente em cluster Olá CCP_MPI_NETMASK afeta apenas a comunicação MPI entre nós de computação de cluster ingressaram no domínio (no local ou em VMs do Azure). Olá variável será ignorada por nós adicionados em uma configuração de tooAzure de disparo.
* Não é possível executar trabalhos MPI em instâncias do Azure que são implantadas em diferentes serviços de nuvem (por exemplo, em implantações de tooAzure intermitente com modelos de nó diferentes ou nós de computação de máquina virtual do Azure implantados em vários serviços de nuvem). Se você tiver várias implantações do nó do Azure que são iniciadas com modelos de nó diferentes, Olá MPI trabalho deve ser executado em apenas um conjunto de nós do Azure.
* Quando você adicionar nós do Azure tooyour cluster e colocá-los Olá online, o serviço de Agendador de trabalho do HPC imediatamente tenta toostart trabalhos em nós de saudação. Se apenas uma parte da carga de trabalho pode executar no Azure, certifique-se de que você atualizar ou cria trabalho modelos toodefine qual trabalho tipos podem ser executados no Azure. Por exemplo, tooensure que trabalhos enviados com um modelo de trabalho executado somente em nós do Azure, adicione o modelo de trabalho do hello nó grupos propriedade toohello e selecione AzureNodes como Olá valor obrigatório. grupos personalizados de toocreate para seus nós do Azure, use saudação do cmdlet Add-HpcGroup HPC PowerShell.

## <a name="next-steps"></a>Próximas etapas
* Como uma alternativa toousing HPC Pack, desenvolva aplicativos MPI nos pools gerenciados de nós de computação no Azure com hello toorun de serviço de lote do Azure. Consulte [Use a instância várias tarefas toorun passando Interface aplicativos MPI (Message) em lote do Azure](../../../batch/batch-mpi.md).
* Se você quiser toorun Linux MPI aplicativos que acessam a rede de RDMA do Azure hello, consulte [configurar aplicativos de MPI um Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
