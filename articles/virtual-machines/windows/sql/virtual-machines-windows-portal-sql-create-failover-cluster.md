---
title: "aaaSQL servidor FCI - máquinas virtuais do Azure | Microsoft Docs"
description: "Este artigo explica como toocreate instância de Cluster de Failover do SQL Server em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Configurar a instância de Cluster de Failover do SQL Server em máquinas virtuais do Azure

Este artigo explica como toocreate um SQL Server de Cluster de Failover (FCI) da instância em máquinas virtuais do Azure no modelo do Gerenciador de recursos. Esta solução usa [direta de espaços de armazenamento do Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como uma SAN virtual com base em software que sincroniza o armazenamento de saudação (discos de dados) entre nós de saudação (máquinas virtuais do Azure) em um Cluster do Windows. S2D é novo no Windows Server 2016.

Olá diagrama a seguir mostra solução completa de saudação em máquinas virtuais do Azure:

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Olá precede o diagrama mostra:

- Duas máquinas virtuais do Azure em um Cluster de Failover do Windows. Quando uma máquina virtual está em um cluster de failover, ela também é chamada de *nó de cluster* ou *nós*.
- Cada máquina virtual tem dois ou mais discos de dados.
- S2D sincroniza dados Olá no disco de dados hello e apresenta Olá sincronizado de armazenamento como um pool de armazenamento.
- pool de armazenamento Olá apresenta um cluster de failover do cluster (CSV) de volume compartilhado toohello.
- função de cluster do SQL Server FCI Olá usa Olá CSV Olá para unidades de dados.
- Um carga do Azure balanceador toohold Olá endereço IP hello FCI do SQL Server.
- Um conjunto de disponibilidade do Azure mantém todos os recursos de saudação.

   >[!NOTE]
   >Todos os recursos do Azure estão no diagrama Olá estão em Olá mesmo grupo de recursos.

Para obter detalhes sobre S2D, confira [Espaços de Armazenamento Direto do Windows Server 2016 Datacenter Edition \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

O S2D dá suporte a dois tipos de arquiteturas: convergida e hiperconvergida. arquitetura de saudação neste documento é hiperconvergida. Um armazenamento de saudação infraestrutura hiperconvergida locais no hello mesmos servidores de aplicativo hello cluster host. Nesta arquitetura, o armazenamento de saudação é em cada nó de FCI do SQL Server.

### <a name="example-azure-template"></a>Exemplo de modelo do Azure

Você pode criar a solução inteira Olá no Azure de um modelo. Um exemplo de um modelo está disponível no GitHub de saudação [modelos de início rápido do Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Este exemplo não é criado ou testado para qualquer carga de trabalho específica. Você pode executar Olá modelo toocreate um FCI do SQL Server com o domínio do S2D armazenamento tooyour conectado. Você pode avaliar modelo hello e modificá-lo para suas finalidades.

## <a name="before-you-begin"></a>Antes de começar

Há algumas coisas que você precisa tooknow e algumas coisas que você precisa em vigor antes de continuar.

### <a name="what-tooknow"></a>Quais tooknow
Você deve ter uma compreensão operacional de saudação tecnologias a seguir:

- [Tecnologias de cluster do Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Instâncias de Cluster de Failover do SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

Além disso, você deve ter uma compreensão geral dos Olá tecnologias a seguir:

- [Solução hiperconvergida usando Espaços de Armazenamento Direto no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Grupos de recursos do Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Quais toohave

Antes de seguir as instruções neste artigo hello, você já deve ter:

- Uma assinatura do Microsoft Azure.
- Um domínio do Windows em máquinas virtuais do Azure.
- Uma conta com objetos toocreate permissão Olá máquina virtual do Azure.
- Uma rede virtual do Azure e sub-rede com espaço de endereços IP suficiente para Olá componentes a seguir:
   - As duas máquinas virtuais.
   - endereço IP de cluster de failover de saudação.
   - Um endereço IP para cada FCI.
- DNS configurado no hello rede do Azure, apontando toohello controladores de domínio.

Com esses pré-requisitos em vigor, é possível continuar com a criação do cluster de failover. Olá primeira etapa é toocreate Olá VMs.

## <a name="step-1-create-virtual-machines"></a>Etapa 1: criar máquinas virtuais

1. Faça logon no toohello [portal do Azure](http://portal.azure.com) com sua assinatura.

1. [Criar um conjunto de disponibilidade do Azure](../tutorial-availability-sets.md).

   disponibilidade de saudação defina agrupa máquinas virtuais em domínios de falha e domínios de atualização. conjunto de disponibilidade Olá torna-se de que seu aplicativo não seja afetado por pontos únicos de falha, como o comutador de rede hello ou unidade de energia de saudação de um rack de servidores.

   Se você não tiver criado o grupo de recursos de saudação para as máquinas virtuais, fazê-lo quando você cria um conjunto de disponibilidade do Azure. Se você estiver usando o conjunto de disponibilidade de Olá Olá toocreate portal do Azure, Olá seguintes etapas:

   - No portal do Azure de Olá, clique em  **+**  tooopen hello Azure Marketplace. Procure **Conjunto de disponibilidade**.
   - Clique em **Conjunto de disponibilidade**.
   - Clique em **Criar**.
   - Em Olá **criar conjunto de disponibilidade** folha, Olá do conjunto de valores a seguir:
      - **Nome**: um nome para o conjunto de disponibilidade de saudação.
      - **Assinatura**: sua assinatura do Azure.
      - **Grupo de recursos**: toouse um grupo existente, clique em **usar existente** e grupo Olá selecione da lista suspensa de saudação. Caso contrário, escolha **criar novo** e digite um nome para o grupo de saudação.
      - **Local**: definir o local de saudação onde você planeja toocreate suas máquinas virtuais.
      - **Domínios de falha**: usar saudação padrão (3).
      - **Atualizar domínios**: usar saudação padrão (5).
   - Clique em **criar** toocreate conjunto de disponibilidade de saudação.

1. Crie máquinas virtuais de saudação no conjunto de disponibilidade de saudação.

   Provisione duas máquinas virtuais de SQL Server no conjunto de disponibilidade do Azure hello. Para obter instruções, consulte [provisionar uma máquina de virtual do SQL Server no portal do Azure de saudação](virtual-machines-windows-portal-sql-server-provision.md).

   Coloque as duas máquinas virtuais:

   - Olá mesmo grupo de recursos do Azure que sua disponibilidade definida está na.
   - Em Olá mesma rede como o controlador de domínio.
   - Em uma sub-rede com espaço suficiente de endereços IP para ambas as máquinas virtuais e todos ps FCIs que você pode vir a usar nesse cluster.
   - No conjunto de disponibilidade do Azure hello.   

      >[!IMPORTANT]
      >Você não pode definir nem alterar a disponibilidade definida depois que uma máquina virtual é criada.

   Escolha uma imagem de saudação do Azure Marketplace. Você pode usar um mercado imagem com o que inclui o Windows Server e SQL Server ou apenas saudação do Windows Server. Para obter detalhes, confira [Visão geral do SQL Server em máquinas virtuais do Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)

   Olá oficial do SQL Server imagens Olá Galeria do Azure incluem uma instância instalada do SQL Server, além de software de instalação do SQL Server hello e chave necessária hello.

   Escolha a imagem à direita de saudação de acordo com toohow que deseja toopay de licença do SQL Server hello:

   - **Pagar por uso de licenciamento**: Olá por minuto dessas imagens inclui licenciamento do hello do SQL Server:
      - **SQL Server 2016 Enterprise no Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard no Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer no Windows Server Datacenter 2016**

   - **BYOL (Traga sua própria licença)**

      - **{BYOL} SQL Server 2016 Enterprise no Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard no Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Depois de criar a máquina virtual de Olá, remova a instância do SQL Server autônomo pré-instalados Olá. Depois de configurar o cluster de failover hello e S2D, você usará Olá pré-instaladas do SQL Server mídia toocreate Olá FCI do SQL Server.

   Como alternativa, você pode usar imagens do Azure Marketplace com apenas o sistema de operacional hello. Escolha um **Datacenter do Windows Server 2016** da imagem e instalar Olá FCI do SQL Server depois de configurar o cluster de failover hello e S2D. Esta imagem não contém a mídia de instalação do SQL Server. Coloque a mídia de instalação de saudação em um local onde você pode executar a instalação do SQL Server Olá para cada servidor.

1. Depois que o Azure cria suas máquinas virtuais, conecte-se tooeach VM com o RDP.

   Quando você primeiro se conectar máquina virtual de tooa com o RDP, computador Olá perguntará se você deseja tooallow toobe este PC podem ser descobertos na rede de saudação. Clique em **Sim**.

1. Se você estiver usando uma das imagens de máquina virtual com o SQL Server hello, remova instância do SQL Server hello.

   - Em **Programas e Recursos**, clique com o botão direito do mouse em **Microsoft SQL Server 2016 (64 bits)** e clique em **Desinstalar/Alterar**.
   - Clique em **Remover**.
   - Selecione a instância padrão de saudação.
   - Remova todos os recursos em **Serviços de Mecanismo de Banco de Dados**. Não remova **Recursos Compartilhados**. Consulte Olá figura abaixo:

      ![Remover Recursos](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Clique em **Avançar** e em **Remover**.

1. <a name="ports"></a>Abra as portas de firewall hello.

   Em cada máquina virtual, abra Olá portas a seguir no hello Firewall do Windows.

   | Finalidade | Porta TCP | Observações
   | ------ | ------ | ------
   | SQL Server | 1433 | Porta normal para instâncias padrão do SQL Server. Se você usou uma imagem da Galeria hello, essa porta é aberta automaticamente.
   | Investigação de integridade | 59999 | Qualquer porta TCP aberta. Em uma etapa posterior, configure o balanceador de carga de saudação [investigação de integridade](#probe) e Olá cluster toouse essa porta.  

1. Adicione armazenamento toohello VM. Para obter informações detalhadas, confira [adicionar armazenamento](../../../storage/common/storage-premium-storage.md).

   As duas máquinas virtuais precisam de pelo menos dois discos de dados.

   Anexe discos brutos - não discos formatado com NTFS.
      >[!NOTE]
      >Se anexar discos formatados com NTFS, você só poderá habilitar S2D sem verificação de qualificação do disco.  

   Anexe um mínimo de dois tooeach de armazenamento Premium (discos SSD) VM. É recomendável ter pelo menos discos P30 (1 TB).

   Host de conjunto de cache muito**somente leitura**.

   capacidade de armazenamento Olá que usar em ambientes de produção depende de sua carga de trabalho. valores de saudação descritos neste artigo são para teste e demonstração.

1. [Adicionar máquinas virtuais de saudação tooyour domínio pré-existente](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Depois de máquinas virtuais de saudação sejam criadas e configuradas, você pode configurar o cluster de failover de saudação.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Etapa 2: Configurar Olá Cluster de Failover do Windows com S2D

Olá próxima etapa é o cluster de failover de saudação tooconfigure com S2D. Nesta etapa, você fará Olá subetapas a seguir:

1. Adicionar o recurso Clustering de Failover do Windows
1. Validar cluster Olá
1. Criar o cluster de failover Olá
1. Criar a testemunha de nuvem Olá
1. Adicionar armazenamento

### <a name="add-windows-failover-clustering-feature"></a>Adicionar o recurso Clustering de Failover do Windows

1. toobegin, conecte-se a máquina virtual da primeira toohello com RDP usando uma conta de domínio que é um membro do grupo local Administradores e objetos de toocreate permissões no Active Directory. Use essa conta para o restante da saudação da configuração de saudação.

1. [Adicionar o Clustering de Failover máquina de virtual do recurso tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   recurso de cluster de Failover de tooinstall de saudação da interface do usuário, Olá seguindo as etapas em ambas as máquinas virtuais.
   - Em **Gerenciador de Servidor**, clique em **Gerenciar** e clique em **Adicionar Funções e Recursos**.
   - Em **assistente Adicionar funções e recursos**, clique em **próximo** até chegar muito**selecionar recursos**.
   - Em **Selecionar Recursos**, clique em **Clustering de Failover**. Inclua todos os recursos necessários e ferramentas de gerenciamento de saudação. Clique em **Adicionar Recursos**.
   - Clique em **próximo** e, em seguida, clique em **concluir** tooinstall recursos de saudação.

   tooinstall Olá recurso cluster de Failover com o PowerShell, execute Olá script a partir de uma sessão do PowerShell de administrador a seguir em uma das máquinas virtuais de saudação.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Para referência, as próximas etapas Olá siga instruções de saudação na etapa 3 do [solução convergida Hyper usando espaços de armazenamento diretos no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Validar cluster Olá

Este guia se refere a tooinstructions em [validar cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Valide cluster Olá em Olá da interface do usuário ou com o PowerShell.

cluster de saudação toovalidate com hello da interface do usuário, Olá seguindo as etapas de uma das máquinas virtuais de saudação.

1. Em **Gerenciador do Servidor**, clique em **Ferramentas** e clique em **Gerenciador de Cluster de Failover**.
1. Em **Gerenciador de Cluster de Failover**, clique em **Ação** e clique em **Validar Configuração...**.
1. Clique em **Avançar**.
1. Em **selecionar servidores ou um Cluster**, nome de tipo de saudação de ambas as máquinas virtuais.
1. Em **Opções de teste**, escolha **Executar apenas os testes selecionados**. Clique em **Avançar**.
1. Em **Testar seleção**, inclua todos os testes, exceto **Armazenamento**. Consulte Olá figura abaixo:

   ![Validar Testes](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Clique em **Avançar**.
1. Em **Confirmação**, clique em **Avançar**.

Olá **validar um Assistente de configuração** Olá de execuções de testes de validação.

cluster de saudação toovalidate com o PowerShell, execute Olá script a partir de uma sessão do PowerShell de administrador a seguir em uma das máquinas virtuais de saudação.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Depois de validar cluster hello, crie o cluster de failover de saudação.

### <a name="create-hello-failover-cluster"></a>Criar o cluster de failover Olá

Este guia refere-se muito[criar cluster de failover Olá](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

cluster de failover do toocreate hello, você precisa:
- nomes de saudação de máquinas virtuais de saudação que se tornam Olá nós de cluster.
- Um nome de cluster de failover Olá
- Um endereço IP de cluster de failover de saudação. Você pode usar um endereço IP que não é usado em Olá mesma rede virtual do Azure e sub-redes Olá nós de cluster.

Olá PowerShell a seguir cria um cluster de failover. Atualizar o script hello com nomes de saudação de nós de saudação (nomes de máquina virtual de saudação) e um endereço IP disponível do hello VNET do Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Criar uma testemunha de nuvem

A Testemunha de Nuvem é um novo tipo de testemunha de quorum de cluster armazenado em um Azure Storage Blob. Isso elimina a necessidade de saudação de uma VM separada que hospeda uma testemunha de compartilhamento.

1. [Criar uma testemunha de nuvem para o cluster de failover Olá](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Criar um contêiner de blob.

1. Salve as chaves de acesso de saudação e URL do contêiner hello.

1. Configure testemunha de quorum de cluster do hello failover cluster. Consulte a [configurar testemunha de quorum de saudação na interface do usuário Olá]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) no hello da interface do usuário.

### <a name="add-storage"></a>Adicionar armazenamento

discos Olá S2D necessário toobe vazias e sem partições ou outros dados. Siga os discos tooclean [Olá as etapas neste guia](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Habilitar Espaços de Armazenamento Diretos \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Olá PowerShell a seguir permite que os espaços de armazenamento direct.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   Em **Gerenciador de Cluster de Failover**, agora você pode ver o pool de armazenamento hello.

1. [Criar um volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Um dos recursos de saudação do S2D é que ele cria automaticamente um pool de armazenamento quando você habilitá-la. Agora você está pronto toocreate um volume. Olá commandlet PowerShell `New-Volume` automatiza o processo de criação de volume hello, incluindo formatação, adicionar cluster toohello e criação de um volume compartilhado de cluster (CSV). saudação de exemplo a seguir cria um 800 GB (gigabyte) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Após a conclusão do comando, um volume de 800 GB é montado como um recurso de cluster. volume Hello está em `C:\ClusterStorage\Volume1\`.

   Olá diagrama a seguir mostra um volume compartilhado de cluster com S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Etapa 3: Testar o failover do cluster de failover

No Gerenciador de Cluster de Failover, verifique se que você pode mover Olá toohello de recursos de armazenamento a outro nó do cluster. Se você puder se conectar de cluster de failover toohello com **Gerenciador de Cluster de Failover** e mover o armazenamento de saudação de toohello um nó para outro, você estará pronto tooconfigure Olá FCI.

## <a name="step-4-create-sql-server-fci"></a>Etapa 4: criar FCI do SQL Server

Depois que você configurou o cluster de failover hello e todos os componentes do cluster, incluindo o armazenamento, você pode criar hello FCI do SQL Server.

1. Conecte a máquina virtual da primeira toohello com RDP.

1. Em **Gerenciador de Cluster de Failover**, verifique se todos os recursos principais de cluster estão na primeira máquina virtual do hello. Se necessário, mova todos os recursos toothis VM.

1. Localize a mídia de instalação de saudação. Se a máquina virtual de saudação usa uma das imagens do Azure Marketplace hello, mídia hello está localizada em `C:\SQLServer_<version number>_Full`. Clique em **Instalação**.

1. Em Olá **Central de instalação do SQL Server**, clique em **instalação**.

1. Clique em **Nova instalação de cluster de failover do SQL Server**. Siga as instruções de Olá Olá tooinstall de assistente Olá FCI do SQL Server.

   diretórios de dados do Hello FCI necessário toobe no armazenamento de cluster. Com S2D, não é um disco compartilhado, mas um volume de tooa de ponto de montagem em cada servidor. S2D sincroniza volume Olá entre os dois nós. volume de saudação é apresentado toohello cluster como um volume compartilhado de cluster. Use o ponto de montagem CSV de saudação para diretórios de dados hello.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Depois de concluir o Assistente de saudação, a instalação instalará um FCI do SQL Server no primeiro nó de saudação.

1. Após a instalação com êxito Olá FCI no primeiro nó de hello, conecte-se toohello segundo nó ao RDP.

1. Olá abrir **Central de instalação do SQL Server**. Clique em **Instalação**.

1. Clique em **cluster de failover do SQL Server do adicionar nó tooa**. Siga as instruções de Olá Olá Assistente tooinstall SQL servidor e adicione toohello esse servidor FCI.

   >[!NOTE]
   >Se você usou uma imagem da Galeria do Azure Marketplace com o SQL Server, ferramentas do SQL Server foram incluídas com a imagem de saudação. Se você não usou essa imagem, instale ferramentas do SQL Server Olá separadamente. Confira [Baixar o SSMS (SQL Server Management Studio)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Etapa 5: criar o balanceador de carga do Azure

Em máquinas virtuais do Azure, os clusters usam um balanceador de carga toohold um endereço IP que precisa toobe em um nó de cluster por vez. Nesta solução, o balanceador de carga Olá contém endereço IP Olá Olá FCI do SQL Server.

[Criar e configurar um balanceador de carga do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Criar balanceador de carga Olá Olá portal do Azure

Balanceador de carga de saudação toocreate:

1. No hello portal do Azure, vá toohello grupo de recursos com máquinas virtuais de saudação.

1. Clique em **+ Adicionar**. Saudação de pesquisa Marketplace para **balanceador de carga**. Clique em **Balanceador de Carga**.

1. Clique em **Criar**.

1. Configure o balanceador de carga de saudação com:

   - **Nome**: um nome que identifica o balanceador de carga de saudação.
   - **Tipo**: balanceador de carga Olá pode ser público ou privado. Um balanceador de carga privadas pode ser acessado de dentro Olá mesma rede virtual. A maioria dos aplicativos do Azure pode usar um balanceador de carga privado. Se seu aplicativo precisa de acesso tooSQL Server diretamente pela Internet de hello, use um balanceador de carga público.
   - **Rede virtual**: Olá mesma rede como máquinas virtuais de saudação.
   - **Subrede**: Olá mesma sub-rede que máquinas virtuais de saudação.
   - **Endereço IP privado**: Olá mesmo endereço IP que você atribuiu o recurso de rede de cluster toohello FCI do SQL Server.
   - **assinatura**: sua assinatura do Azure.
   - **Grupo de recursos**: Use Olá mesmo grupo de recursos que as máquinas virtuais.
   - **Local**: Use Olá mesmo local do Azure que suas máquinas virtuais.
   Consulte Olá figura abaixo:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Configurar o pool de back-end do balanceador de carga Olá

1. Retornar toohello grupo de recursos do Azure com máquinas virtuais de saudação e localize o balanceador de carga novo hello. Você pode ter o modo de exibição de saudação toorefresh em Olá grupo de recursos. Clique o balanceador de carga de saudação.

1. Na folha de Balanceador de carga hello, clique em **pools de back-end**.

1. Clique em **+ adicionar** tooadd um pool de back-end.

1. Digite um nome para o pool de back-end de saudação.

1. Clique em **Adicionar uma máquina virtual**.

1. Em Olá **escolha máquinas virtuais** folha, clique em **escolher um conjunto de disponibilidade**.

1. Escolha o conjunto de disponibilidade de saudação que você colocou Olá máquinas de virtuais do SQL Server em.

1. Em Olá **escolha máquinas virtuais** folha, clique em **escolha máquinas virtuais de saudação**.

   Seu portal do Azure deve ter aparência Olá figura abaixo:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Clique em **selecione** em Olá **escolha máquinas virtuais** folha.

1. Clique em **OK** duas vezes.

### <a name="configure-a-load-balancer-health-probe"></a>Configurar um teste de integridade do balanceador de carga

1. Na folha de Balanceador de carga hello, clique em **sondas de integridade**.

1. Clique em **+ Adicionar**.

1. Em Olá **investigação de integridade de adicionar** folha, <a name="probe"> </a>definir parâmetros de teste de integridade hello:

   - **Nome**: um nome para a investigação de integridade de saudação.
   - **Protocolo**: TCP.
   - **Porta**: definir tooan porta TCP disponível. Essa porta exige uma porta de firewall aberta. Saudação de uso [mesma porta](#ports) definido para a investigação de integridade Olá no firewall hello.
   - **Intervalo**: 5 segundos.
   - **Limite não íntegro**: duas falhas consecutivas.

1. Clique em OK.

### <a name="set-load-balancing-rules"></a>Definir regras de balanceamento de carga

1. Na folha de Balanceador de carga hello, clique em **regras de balanceamento de carga**.

1. Clique em **+ Adicionar**.

1. Definir parâmetros de regras de balanceamento da carga de saudação:

   - **Nome**: um nome para as regras de balanceamento de carga de saudação.
   - **Endereço IP de Frontend**: Use o endereço IP Olá Olá recursos de rede de cluster FCI do SQL Server.
   - **Porta**: definido para Olá porta TCP do SQL Server FCI. porta de instância saudação padrão é 1433.
   - **Porta de back-end**: este valor usa Olá mesma porta como Olá **porta** valor quando você habilitar **IP flutuante (retorno de servidor direto)**.
   - **Pool de back-end**: Use Olá back-end nome do pool que você configurou anteriormente.
   - **Investigação de integridade**: investigação de integridade de saudação de uso que você configurou anteriormente.
   - **Persistência de sessão**: nenhuma.
   - **Tempo limite de ociosidade (minutos)**: 4.
   - **IP flutuante (retorno de servidor direto)**: habilitado

1. Clique em **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Etapa 6: configurar o cluster para investigação

Defina o parâmetro de porta de investigação de cluster hello no PowerShell.

tooset Olá parâmetro de porta de investigação de cluster, atualize as variáveis no hello script a seguir do seu ambiente.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Etapa 7: testar o failover de FCI

Failover de teste de saudação funcionalidade do cluster toovalidate FCI. Olá seguintes etapas:

1. Conecte-se tooone Olá FCI do SQL Server de nós de cluster com o RDP.

1. Abra o **Gerenciador de Cluster de Failover**. Clique em **Funções**. Aviso de nó que possui a função de FCI do SQL Server de saudação.

1. Clique a função do hello FCI do SQL Server.

1. Clique em **Mover** e em **Melhor Nó Possível**.

**Gerenciador de Cluster de failover** mostra Olá função e seus recursos offline. Olá recursos, em seguida, mover e ficar online Olá no outro nó.

### <a name="test-connectivity"></a>Testar a conectividade

conectividade de tootest log na máquina virtual tooanother Olá mesma rede virtual. Abra **SQL Server Management Studio** e conecte-se o nome do toohello FCI do SQL Server.

>[!NOTE]
>Se necessário, você pode [baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Limitações
Em máquinas virtuais do Azure, o coordenador de transações distribuídas (DTC) da Microsoft não é suportado em FCIs porque Olá porta RPC não é suportado pelo Balanceador de carga de saudação.

## <a name="see-also"></a>Consulte também

[Instalação S2D com área de trabalho remota (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Solução hiperconvergida com espaços de armazenamento diretos](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Visão geral direta de espaço de armazenamento](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Suporte do SQL Server para S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
