---
title: "aaaConfigure sempre no grupo de disponibilidade em máquinas virtuais do Azure (clássica) | Microsoft Docs"
description: "Crie um grupo de disponibilidade AlwaysOn em Máquinas Virtuais do Azure. Este tutorial usa principalmente a interface do usuário hello e ferramentas em vez de script."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Configurar grupo de disponibilidade AlwaysOn em Máquinas Virtuais do Azure (clássico)
> [!div class="op_single_selector"]
> * [Clássico: Interface de usuário](../classic/portal-sql-alwayson-availability-groups.md)
> * [Clássico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Antes de começar, considere que agora você pode concluir esta tarefa no modelo do Azure Resource Manager. O modelo do Azure Resource Manager é recomendável para novas implantações. Confira, [Introdução aos grupos de disponibilidade Always On do SQL Server em máquinas virtuais do Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. O Azure tem dois toocreate de modelos de implantação diferentes e trabalhar com recursos: [Gerenciador de recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo explica como toouse Olá modelo de implantação clássico. 

toocomplete essa tarefa com o modelo do Azure Resource Manager hello, consulte [SQL Server Always On grupos de disponibilidade em máquinas virtuais do Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

Este tutorial de ponta a ponta mostra como os grupos de disponibilidade tooimplement usando SQL Server Always On em execução em máquinas virtuais do Azure.

No final de saudação do tutorial hello, sua solução SQL Server Always On no Azure consistirá Olá elementos a seguir:

* Uma rede virtual que contém várias sub-redes, incluindo uma sub-rede de front-end e uma de back-end
* Um controlador de domínio com um domínio do Active Directory (Azure AD)
* Duas máquinas virtuais que executam o SQL Server e são implantados toohello back-end subrede e domínio toohello ingressado no AD do Azure
* Um cluster de failover de três nós com o modelo de quorum de maioria de nós Olá
* Um grupo de disponibilidade que tem duas réplicas de confirmação síncrona de um banco de dados de disponibilidade

Olá ilustração a seguir é uma representação gráfica da solução hello.

![Arquitetura de laboratório de teste para grupos de disponibilidade no Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Observe que se trata de uma das configurações possíveis. Por exemplo, você pode minimizar o número de saudação de máquinas virtuais para um grupo de disponibilidade de duas réplicas. Essa configuração é salva em horas de computação no Azure usando o controlador de domínio hello como testemunha de compartilhamento de arquivo hello quorum em um cluster de dois nós. Esse método reduz Olá contagem de máquina virtual por uma configuração Olá ilustrado.

Este tutorial pressupõe o seguinte hello:

* Você já tem uma conta do Azure.
* Você já sabe como toouse Olá GUI no hello máquina virtual Galeria tooprovision uma máquina virtual clássica que executa o SQL Server.
* Você já tem uma compreensão sólida dos grupos de disponibilidade AlwaysOn. Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Se você estiver interessado em usar os grupos de disponibilidade Always On com o SharePoint, consulte também [Configure SQL Server 2012 Always On Availability Groups for SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx)(Configurar grupos de disponibilidade AlwaysOn do SQL Server 2012 para o SharePoint 2013).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Criar rede virtual hello e o servidor do controlador de domínio
Comece com uma nova conta de avaliação do Azure. Depois de configurar sua conta, você deve estar na tela inicial de saudação do hello portal clássico do Azure.

1. Clique em Olá **novo** botão no canto esquerdo de saudação do inferior Olá da página hello, conforme mostrado no hello captura de tela a seguir.
   
    ![Clique em novo no portal de saudação](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Clique em **serviços de rede** > **rede Virtual** > **criação personalizada**, conforme mostrado no hello captura de tela a seguir.
   
    ![Criar rede virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. Em Olá **criar uma rede VIRTUAL** caixa de diálogo caixa, crie uma nova rede virtual percorrendo páginas hello e usando configurações de Olá Olá a tabela a seguir. 
   
   | Página | Configurações |
   | --- | --- |
   | Detalhes de rede virtual |**NAME = ContosoNET**<br/>**REGION = Oeste dos EUA** |
   | Conectividade de VPN e servidores DNS |Nenhum |
   | Espaços de Endereço da Rede Virtual |As configurações são mostradas na Olá captura de tela a seguir: ![Criar rede virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Crie máquina virtual Olá que você usará como controlador de domínio da saudação (DC). Clique em **novo** > **de computação** > **Máquina Virtual** > **da galeria**, conforme mostrado na Olá captura de tela a seguir.
   
    ![Criar uma máquina virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. Em Olá **criar uma máquina VIRTUAL** caixa de diálogo caixa, configure uma nova máquina virtual percorrendo páginas hello e usando configurações de Olá Olá a tabela a seguir. 
   
   | Página | Configurações |
   | --- | --- |
   | Selecionar Olá sistema operacional da máquina virtual |Windows Server 2012 R2 Datacenter |
   | Configuração de máquina virtual |**VERSION RELEASE DATE** = (latest)<br/>**VIRTUAL MACHINE NAME** = ContosoDC<br/>**TIER** = STANDARD<br/>**TAMANHO** = A2 (2 núcleos)<br/>**NEW USER NAME** = AzureAdmin<br/>**NEW PASSWORD** = Contoso!000<br/>**CONFIRM** = Contoso!000 |
   | Configuração de máquina virtual |**CLOUD SERVICE** = Criar um novo serviço de nuvem<br/>**CLOUD SERVICE DNS NAME** = um nome de serviço de nuvem exclusivo<br/>**DNS NAME** = um nome exclusivo (ex: ContosoDC123)<br/>**REGION/AFFINITY GROUP/VIRTUAL NETWORK** = ContosoNET<br/>**VIRTUAL NETWORK SUBNETS** = Back(10.10.2.0/24)<br/>**CONTA DE ARMAZENAMENTO** = Use uma conta de armazenamento gerada automaticamente<br/>**AVAILABILITY SET** = (Nenhum) |
   | Opções de máquina virtual |Usar padrões |

Depois de configurar a nova máquina de virtual hello, aguarde Olá máquina virtual toobe provisionada. Esse processo leva alguns toofinish de tempo. Se você clicar em Olá **Máquina Virtual** guia Olá clássico do Azure portal, consulte estados de ciclo de ContosoDC de **iniciando (Provisionando)** muito**parado**, **Iniciando**, **executando (Provisionando)**e, finalmente, **executando**.

Agora o servidor de controlador de domínio de saudação está provisionado com êxito. Em seguida, você configurará o domínio do Active Directory Olá neste servidor de controlador de domínio.

## <a name="configure-hello-domain-controller"></a>Configurar o controlador de domínio Olá
Olá etapas a seguir, você configura a máquina ContosoDC de saudação como um controlador de domínio para corp.contoso.com.

1. No portal de saudação, selecione Olá **ContosoDC** máquina. Em Olá **painel** , clique em **conectar** tooopen uma área de trabalho remota (RDP) de arquivo para acesso de área de trabalho remoto.
   
    ![Conecte-se tooVritual máquina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Entre com sua conta de administrador configurada (**\AzureAdmin**) e senha (**Contoso!000**).
3. Por padrão, Olá **Gerenciador do servidor** painel deve ser exibido.
4. Clique em Olá **adicionar funções e recursos** link no painel de saudação.
   
    ![Adicionar Funções ao Gerenciador de Servidores](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Clique em **próximo** até chegar toohello **funções de servidor** seção.
6. Selecione Olá **serviços de domínio do Active Directory** e **servidor DNS** funções. Quando solicitado, adicione mais recursos que exigem essas funções.
   
   > [!NOTE]
   > Você receberá um aviso de validação de que não há nenhum endereço IP estático. Se você estiver testando configuração hello, clique em **continuar**. Para cenários de produção [PowerShell tooset Olá endereço IP estático do computador do controlador de domínio Olá](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Adicionar Caixa de Diálogo de Funções](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Clique em **próximo** até que você alcance Olá **confirmação** seção. Selecione Olá **reinicialização do servidor de destino Olá automaticamente, se necessário** caixa de seleção.
8. Clique em **Instalar**.
9. Depois de saudação recursos estão instalados, retorne toohello **Gerenciador do servidor** painel.
10. Selecione Olá novo **AD DS** opção no painel esquerdo da saudação.
11. Clique em Olá **mais** link na barra de aviso Olá amarelo.
    
     ![Caixa de diálogo do AD DS na máquina virtual do servidor DNS](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. Em Olá **ação** coluna da saudação **todos os detalhes de tarefas do servidor** caixa de diálogo, clique em **promover este controlador de domínio do servidor tooa**.
13. Em Olá **Assistente de configuração de serviços do Active Directory domínio**, use Olá valores a seguir:
    
    | Página | Configuração |
    | --- | --- |
    | Configuração de Implantação |**Adicionar uma nova floresta** = selecionado<br/>**Nome do domínio raiz** = corp.contoso.com |
    | Opções de Controlador de Domínio |**Senha** = Contoso!000<br/>**Confirmar Senha** = Contoso!000 |
14. Clique em **próximo** toogo por meio de Olá outras páginas no Assistente de saudação. Em Olá **verificação de pré-requisitos** , verifique se que você vê a seguinte mensagem de saudação: **todas as verificações de pré-requisitos passaram com êxito**. Observe que você deve examinar todas as mensagens de aviso aplicáveis, mas é possível toocontinue com instalação hello.
15. Clique em **Instalar**. Olá **ContosoDC** máquina virtual reiniciará automaticamente.

## <a name="configure-domain-accounts"></a>Configurar contas de domínio
Olá próximas etapas configuram contas do Active Directory Olá para uso posterior.

1. Entrar novamente toohello **ContosoDC** máquina.
2. No **Gerenciador de Servidores**, clique em **Ferramenta** > **Centro Administrativo do Active Directory**.
   
    ![Centro Administrativo do Active Directory](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. Em Olá **Centro Administrativo do Active Directory**, selecione **corp (local)** no painel esquerdo da saudação.
4. Em Olá direito **tarefas** painel, clique em **novo** > **usuário**. Saudação de usar as configurações a seguir:
   
   | Configuração | Valor |
   | --- | --- |
   | **Nome** |Instalar |
   | **SamAccountName do usuário** |Instalar |
   | **Senha** |Contoso!000 |
   | **Confirmar senha** |Contoso!000 |
   | **Outras opções de senha** |Selecionado |
   | **A senha nunca expira** |Verificado |
5. Clique em **Okey** toocreate Olá **instalar** usuário. Esta conta será usada tooconfigure Olá failover cluster e hello grupo de disponibilidade.
6. Crie dois usuários adicionais, **CORP\SQLSvc1** e **CORP\SQLSvc2**, com hello mesmas etapas. Essas contas serão usadas para instâncias do SQL Server hello. Em seguida, você precisa toogive **CORP\Install** Olá clustering de failover do Windows tooconfigure permissões necessárias.
7. Em Olá **Centro Administrativo do Active Directory**, clique em **corp (local)** no painel esquerdo da saudação. Em Olá **tarefas** painel, clique em **propriedades**.
   
    ![Propriedades do usuário CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Selecione **extensões**e, em seguida, clique em Olá **avançado** botão Olá **segurança** guia.
9. Em Olá **configurações de segurança avançadas para corp** caixa de diálogo, clique em **adicionar**.
10. Clique em **Selecionar uma entidade**, procure **CORP\Install**e, em seguida, clique em **OK**.
11. Selecione Olá **ler todas as propriedades** e **criar objetos de computador** permissões.
    
     ![Permissões de usuário corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Clique em **OK** e em **OK** novamente. Janela de propriedades corp Olá fechar.

Agora que você configurou o Active Directory e objetos de saudação do usuário, você criará três máquinas virtuais de SQL Server e associá-las toothis domínio.

## <a name="create-hello-sql-server-virtual-machines"></a>Criar hello máquinas virtuais do SQL Server
Criar três máquinas virtuais do SQL Server. Uma é para um nó de cluster e duas são para o SQL Server. toocreate de máquinas virtuais de hello, vá fazer toohello portal clássico do Azure, clique em **novo** > **de computação** > **Máquina Virtual**  >  **Da galeria**. Em seguida, use modelos de Olá Olá toohelp tabela criar máquinas virtuais de saudação a seguir.

| Página | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Selecionar Olá sistema operacional da máquina virtual |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Configuração de máquina virtual |**VERSION RELEASE DATE** = (latest)<br/>**VIRTUAL MACHINE NAME** = ContosoWSFCNode<br/>**TIER** = STANDARD<br/>**TAMANHO** = A2 (2 núcleos)<br/>**NEW USER NAME** = AzureAdmin<br/>**NEW PASSWORD** = Contoso!000<br/>**CONFIRM** = Contoso!000 |**VERSION RELEASE DATE** = (latest)<br/>**VIRTUAL MACHINE NAME** = ContosoSQL1<br/>**TIER** = STANDARD<br/>**TAMANHO** = A3 (4 núcleos)<br/>**NEW USER NAME** = AzureAdmin<br/>**NEW PASSWORD** = Contoso!000<br/>**CONFIRM** = Contoso!000 |**VERSION RELEASE DATE** = (latest)<br/>**VIRTUAL MACHINE NAME** = ContosoSQL2<br/>**TIER** = STANDARD<br/>**TAMANHO** = A3 (4 núcleos)<br/>**NEW USER NAME** = AzureAdmin<br/>**NEW PASSWORD** = Contoso!000<br/>**CONFIRM** = Contoso!000 |
| Configuração de máquina virtual |**CLOUD SERVICE** = nome DNS do serviço de nuvem exclusivo criado anteriormente (ex: ContosoDC123)<br/>**REGION/AFFINITY GROUP/VIRTUAL NETWORK** = ContosoNET<br/>**VIRTUAL NETWORK SUBNETS** = Back(10.10.2.0/24)<br/>**CONTA DE ARMAZENAMENTO** = Use uma conta de armazenamento gerada automaticamente<br/>**AVAILABILITY SET** = Criar um conjunto de disponibilidade<br/>**AVAILABILITY SET NAME** = SQLHADR |**CLOUD SERVICE** = nome DNS do serviço de nuvem exclusivo criado anteriormente (ex: ContosoDC123)<br/>**REGION/AFFINITY GROUP/VIRTUAL NETWORK** = ContosoNET<br/>**VIRTUAL NETWORK SUBNETS** = Back(10.10.2.0/24)<br/>**CONTA DE ARMAZENAMENTO** = Use uma conta de armazenamento gerada automaticamente<br/>**CONJUNTO de disponibilidade** = SQLHADR (você também pode configurar disponibilidade Olá definida depois Olá máquina foi criada. Todas as três máquinas devem ser atribuídas conjunto de disponibilidade SQLHADR toohello.) |**CLOUD SERVICE** = nome DNS do serviço de nuvem exclusivo criado anteriormente (ex: ContosoDC123)<br/>**REGION/AFFINITY GROUP/VIRTUAL NETWORK** = ContosoNET<br/>**VIRTUAL NETWORK SUBNETS** = Back(10.10.2.0/24)<br/>**CONTA DE ARMAZENAMENTO** = Use uma conta de armazenamento gerada automaticamente<br/>**CONJUNTO de disponibilidade** = SQLHADR (você também pode configurar disponibilidade Olá definida depois Olá máquina foi criada. Todas as três máquinas devem ser atribuídas conjunto de disponibilidade SQLHADR toohello.) |
| Opções de máquina virtual |Usar padrões |Usar padrões |Usar padrões |

<br/>

> [!NOTE]
> configuração de saudação anterior sugere máquinas virtuais de camada padrão, porque máquinas da camada BASIC não oferecem suporte a pontos de extremidade com balanceamento de carga. Você precisa de pontos de extremidade com balanceamento de carga toocreate posteriormente um ouvinte de grupo de disponibilidade. Além disso, os tamanhos de máquina Olá sugeridas aqui destinam-se para grupos de disponibilidade de teste em máquinas virtuais do Azure. Para melhor desempenho em cargas de trabalho de produção Olá, consulte recomendações Olá para tamanhos de máquina do SQL Server e configuração em [práticas recomendadas de desempenho para o SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Depois de máquinas virtuais de saudação três totalmente provisionadas, você precisa toojoin-los toohello **corp.contoso.com** máquinas de toohello do domínio e grant CORP\Install direitos administrativos. toodo, Olá use as etapas a seguir para cada uma das máquinas virtuais de saudação três.

1. Primeiro, altere o endereço do servidor DNS preferido de saudação. Baixar o diretório local de tooyour cada máquina virtual de arquivo RDP selecionando Olá VM na lista de saudação e clicando em hello **conectar** botão. tooselect uma máquina virtual, clique em qualquer lugar mas a primeira célula Olá na linha de saudação, conforme mostrado no hello captura de tela a seguir.
   
    ![Baixar o arquivo RDP de saudação](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Abra Olá RDP do arquivo que você baixou e entrar na máquina virtual de toohello usando sua conta de administrador configurada (**BUILTIN\AzureAdmin**) e a senha (**Contoso! 000**).
3. Depois de entrar, você deve ver Olá **Gerenciador do servidor** painel. Clique em **servidor Local** no painel esquerdo da saudação.
4. Clique em Olá **endereço IPv4 atribuído pelo DHCP, IPv6 habilitado** link.
5. Em Olá **conexões de rede** caixa de diálogo, clique o ícone de rede hello.
   
    ![Alterar servidor de DNS de máquina virtual preferido Olá](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Na barra de comandos de saudação, clique em **alterar as configurações de saudação dessa conexão**. (Dependendo do tamanho de saudação da janela, talvez seja necessário tooclick Olá seta dupla à direita toosee esse comando).
7. Selecione **Internet Protocol Version 4 (TCP/IPv4)** e, em seguida, clique em **Propriedades**.
8. Selecione **Olá usar endereços de servidor DNS a seguir** e, em seguida, especifique **10.10.2.4** na **servidor DNS preferencial**.
9. Olá **10.10.2.4** endereço é Olá que é atribuído tooa VM na sub-rede de 10.10.2.0/24 de saudação em uma rede virtual do Azure. Essa máquina virtual é **ContosoDC**. tooverify **ContosoDC**do endereço IP, use **nslookup contosodc** na janela de prompt de comando do hello, conforme mostrado no hello captura de tela a seguir.
   
    ![Use o endereço IP toofind NSLOOKUP para o controlador de domínio](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Clique em **Okey** > **fechar** toocommit alterações de saudação. Você agora pode unir a máquina virtual de saudação muito**corp.contoso.com**.
11. Em Olá **servidor Local** janela, clique em Olá **WORKGROUP** link.
12. Em Olá **nome do computador** seção, clique em **alteração**.
13. Selecione Olá **domínio** caixa de seleção, digite **corp.contoso.com** Olá caixa de texto e, em seguida, clique em **Okey**.
14. Em Olá **a segurança do Windows** caixa de diálogo, especifique as credenciais de saudação para conta de administrador de domínio saudação padrão (**CORP\AzureAdmin**) e a senha da saudação (**Contoso! 000**).
15. Quando você vir a mensagem "Bem-vindo toohello corp.contoso.com domínio", clique em **Okey**.
16. Clique em **fechar** > **reiniciar agora** na caixa de diálogo de saudação.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Adicionar usuário do hello Corp\Install como um administrador em cada máquina virtual
1. Aguarde até que a máquina virtual de saudação for reiniciada e, em seguida, abra hello RDP de arquivos novamente toosign na máquina virtual de toohello usando Olá **BUILTIN\AzureAdmin** conta.
2. Em **Gerenciador de Servidores** clique **Ferramentas** > **Gerenciamento do Computador**.
   
    ![Gerenciamento do Computador](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. Em Olá **gerenciamento do computador** caixa de diálogo caixa, expanda **usuários e grupos locais**e, em seguida, clique em **grupos**.
4. Clique duas vezes em Olá **administradores** grupo.
5. Em Olá **propriedades de administradores** caixa de diálogo, clique em Olá **adicionar** botão.
6. Insira o usuário Olá **CORP\Install**e, em seguida, clique em **Okey**. Quando solicitado a fornecer credenciais, use Olá **AzureAdmin** conta com hello **Contoso! 000** senha.
7. Clique em **Okey** tooclose Olá **propriedades do administrador** caixa de diálogo.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Adicionar Olá Clustering de Failover do recurso tooeach virtual machine
1. Em Olá **Gerenciador do servidor** painel, clique em **adicionar funções e recursos**.
2. Em Olá **assistente Adicionar funções e recursos**, clique em **próximo** até chegar toohello **recursos** página.
3. Selecione **Clustering de Failover**. Quando solicitado, adicione outros recursos dependentes.
   
    ![Adicionar o recurso de Clustering de Failover toovirtual máquina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Clique em **próximo**e, em seguida, clique em **instalar** em Olá **confirmação** página.
5. Olá quando **Clustering de Failover** recurso instalação for concluída, clique em **fechar**.
6. Sair de máquina virtual de saudação.
7. Repita as etapas nesta seção para todos os três servidores Olá: **ContosoWSFCNode**, **ContosoSQL1**, e **ContosoSQL2**.

Olá SQL Server agora as máquinas virtuais são provisionadas e em execução, mas cada um tem opções padrão de saudação do SQL Server.

## <a name="create-hello-failover-cluster"></a>Criar o cluster de failover Olá
Nesta seção, você cria o cluster de failover de Olá que irá hospedar o grupo de disponibilidade de saudação que você criará mais tarde. Agora, você deve ter feito Olá tooeach de máquinas virtuais Olá três que você usará no cluster de failover Olá a seguir:

* Máquina virtual de saudação totalmente provisionado no Azure
* Ingressado Olá máquina virtual toohello domínio
* Adicionado **CORP\Install** toohello grupo de administradores local
* Recurso de cluster de failover Olá adicionado

Todos esses são os pré-requisitos em cada máquina virtual antes de associá-lo toohello cluster de failover.

Além disso, observe que Olá rede virtual do Azure não se comporta Olá mesma forma que uma rede local. É necessário toocreate cluster Olá Olá ordem a seguir:

1. Crie um cluster de nó único em um nó (**ContosoSQL1**).
2. Modificar tooan de endereço IP de cluster Olá endereço IP não usado (**10.10.2.101**).
3. Colocar Olá, nome de cluster online.
4. Adicionar Olá outros nós (**ContosoSQL2** e **ContosoWSFCNode**).

Use Olá seguintes etapas toocomplete Olá tarefas que configurar totalmente o cluster de saudação.

1. Arquivo RDP Olá aberto para **ContosoSQL1**e entre usando a conta de domínio Olá **CORP\Install**.
2. Em Olá **Gerenciador do servidor** painel, clique em **ferramentas** > **Gerenciador de Cluster de Failover**.
3. No painel esquerdo do hello, clique com botão direito **Gerenciador de Cluster de Failover**e, em seguida, clique em **criar um Cluster**, conforme mostrado no hello captura de tela a seguir.
   
    ![Criar cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. No Assistente para criação de Cluster de hello, criar um cluster de um nó percorrendo as páginas de saudação e usando configurações de Olá Olá a tabela a seguir:
   
   | Página | Configurações |
   | --- | --- |
   | Antes de começar |Usar padrões |
   | Selecionar Servidores |Digite **ContosoSQL1** em **Inserir nome do servidor** e clique em **Adicionar** |
   | Aviso de Validação |Selecione **n º eu não precisar do suporte da Microsoft para este cluster e, portanto, não quiser que a validação de saudação toorun testes. Quando clico em Avançar, continuo a criar o cluster Olá**. |
   | Ponto de acesso para administrar Olá Cluster |Digite **Cluster1** em **Nome do Cluster** |
   | Confirmação |Use os padrões, a menos que você esteja usando Espaços de Armazenamento. Consulte o aviso Olá após esta tabela. |
   
   > [!WARNING]
   > Se você estiver usando [espaços de armazenamento](https://technet.microsoft.com/library/hh831739), que agrupam vários discos em pools de armazenamento, você deve limpar Olá **adicionar todos os armazenamento qualificado ao cluster toohello** caixa de seleção Olá **confirmação** página. Se você não desmarcar essa opção, discos virtuais hello serão desanexados durante a saudação clustering processo. Como resultado, eles também não aparecerão no Gerenciador de discos até que espaços de armazenamento de saudação são removidos do cluster hello e reanexados usando o PowerShell.
   > 
   > 
5. No painel esquerdo do hello, expanda **Gerenciador de Cluster de Failover**e, em seguida, clique em **Cluster1.corp.contoso.com**.
6. No painel central do hello, role para baixo toohello **recursos principais de Cluster** seção e, em seguida, expanda Olá **nome: Clutser1** detalhes. Você deverá ver dois Olá **nome** e hello **endereço IP** recursos Olá **falha** estado. Olá recurso de endereço IP não pode ser colocado online porque Olá cluster recebeu Olá o mesmo endereço IP hello própria máquina, que é um endereço duplicado.
7. Com o botão direito Olá falhado **endereço IP** recursos e depois clique em **propriedades**.
   
    ![Propriedades do cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Selecione **endereço IP estático**, especifique **10.10.2.101** em Olá **endereço** caixa de texto e clique **Okey**.
9. Em Olá **recursos principais de Cluster** seção, clique no **nome: Cluster1**e, em seguida, clique em **colocar Online**. Aguarde até que ambos os recursos estejam online. Quando o recurso de nome de cluster Olá fica online, o servidor de controlador de domínio de hello está atualizado com uma nova conta de computador do Active Directory. Esta conta do Active Directory será usada toorun saudação do grupo de disponibilidade serviço clusterizado mais tarde.
10. Adicione Olá restantes do cluster de toohello de nós. Na árvore do navegador de saudação, clique com botão direito **Cluster1.corp.contoso.com**e, em seguida, clique em **adicionar nó**, conforme mostrado no hello captura de tela a seguir.
    
     ![Adicionar nó toohello cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. Em Olá **Assistente para adicionar nó**, clique em **próximo** em Olá **selecionar servidores** página, adicione **ContosoSQL2** e **ContosoWSFCNode**  toohello lista, digitando o nome do servidor de saudação em **digite o nome do servidor** e, em seguida, clicando em **adicionar**. Quando terminar, clique em **Avançar**.
12. Em Olá **aviso de validação** , clique em **não**, embora em um cenário de produção, você deve executar testes de validação de saudação. Em seguida, clique em **Avançar**.
13. Em Olá **confirmação** , clique em **próximo** tooadd nós de saudação.
    
    > [!WARNING]
    > Se você estiver usando [espaços de armazenamento](https://technet.microsoft.com/library/hh831739), que agrupam vários discos em pools de armazenamento, você deve limpar Olá **adicionar todos os armazenamento qualificado ao cluster toohello** caixa de seleção. Se você não desmarcar essa opção, discos virtuais hello serão desanexados durante a saudação clustering processo. Como resultado, eles também não aparecerão no Gerenciador de discos até que os espaços de armazenamento Olá são removidos do cluster e reanexados usando o PowerShell.
    > 
    > 
14. Depois que nós de saudação são adicionados toohello cluster, clique em **concluir**. Gerenciador de Cluster de failover agora deve mostrar que o cluster tem três nós e listá-los na saudação **nós** contêiner.
15. Sair de sessão de área de trabalho remota hello.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Preparar instâncias do SQL Server Olá para grupos de disponibilidade
Nesta seção, você fará Olá a seguir em ambos os **ContosoSQL1** e **contosoSQL2**:

* Adicionar um logon para **NT AUTHORITY\System** com as permissões necessárias definido na instância do SQL Server padrão toohello.
* Adicionar **CORP\Install** como uma instância do SQL Server do padrão de toohello da função de sysadmin.
* Abra o firewall Olá para acesso remoto do SQL Server.
* Habilite Olá sempre no recurso de grupos de disponibilidade.
* Alterar a conta de serviço do SQL Server Olá muito**CORP\SQLSvc1** e **CORP\SQLSvc2**, respectivamente.

Essas ações podem ser executadas em qualquer ordem. No entanto, Olá etapas guiará-los na ordem. Siga as etapas de saudação para ambos **ContosoSQL1** e **ContosoSQL2**:

1. Se você não tiver entrado logoff da sessão de área de trabalho remota Olá para a máquina virtual de hello, faça isso agora.
2. Arquivos aberto Olá RDP para **ContosoSQL1** e **ContosoSQL2**e entre como **BUILTIN\AzureAdmin**.
3. Adicionar **NT AUTHORITY\System** toohello logins do SQL Server com as permissões necessárias. Abra o **SQL Server Management Studio**.
4. Clique em **conectar** instância do SQL Server tooconnect toohello padrão.
5. No **Pesquisador de Objetos**, expanda **Segurança** e depois **Logons**.
6. Saudação de atalho **NT AUTHORITY\System** logon e clique **propriedades**.
7. Em Olá **protegíveis** página servidor local hello, selecione **Grant** para Olá as seguintes permissões e, em seguida, clique em **Okey**.
   
   * Alterar qualquer grupo de disponibilidade
   * Conectar o SQL
   * Exibir o estado do servidor
8. Adicionar **CORP\Install** como um **sysadmin** instância da função toohello padrão do SQL Server. Em **Pesquisador de Objetos**, clique com o botão direito do mouse em **Logons** e, em seguida, clique em **Novo Logon**.
9. Digite **CORP\Install** em **Nome de logon**.
10. Em Olá **funções de servidor** página, selecione **sysadmin**e, em seguida, clique em **Okey**. Depois de criar logon hello, você pode vê-lo expandindo **logons** na **Pesquisador de objetos**.
11. toocreate uma regra de firewall para SQL Server, Olá **iniciar** tela, abra **Firewall do Windows com segurança avançada**.
12. No painel esquerdo do hello, selecione **regras de entrada**. No painel direito da saudação, clique em **nova regra**.
13. Em Olá **tipo de regra** , clique em **programa** > **próximo**.
14. Em Olá **programa** página, selecione **este caminho de programa**, tipo **%ProgramFiles%\Microsoft SQL Server \ mssql12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** Olá caixa de texto e, em seguida, clique em **próximo**. Se você estiver seguindo estas instruções, mas usando o SQL Server 2012, o diretório do SQL Server Olá é **MSSQL11. MSSQLSERVER**.
15. Em Olá **ação** página, mantenha **Permitir conexão Olá** selecionado e, em seguida, clique em **próximo**.
16. Em Olá **perfil** página, aceite as configurações padrão de saudação e, em seguida, clique em **próximo**.
17. Em Olá **nome** página, especifique um nome de regra, como **do SQL Server (regra de programa)**, em Olá **nome** texto caixa e, em seguida, clique em **concluir**.
18. Olá tooenable **grupos de disponibilidade AlwaysOn** recurso em Olá **iniciar** tela, abra **SQL Server Configuration Manager**.
19. Na árvore do navegador de saudação, clique em **SQL Server Services**, Olá com o botão direito **SQL Server (MSSQLSERVER)** de serviço e, em seguida, clique em **propriedades**.
20. Clique em Olá **alta disponibilidade AlwaysOn** guia, selecione **habilitar grupos de disponibilidade AlwaysOn**, conforme mostrado no hello captura de tela a seguir e, em seguida, clique em **aplicar**. Clique em **Okey** em Olá a caixa de diálogo e não feche Olá **propriedades** ainda a caixa de diálogo. Você reiniciará o serviço de SQL Server de saudação depois que você alterar a conta de serviço de saudação.
    
     ![Habilitar grupos de disponibilidade AlwaysOn](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. Olá toochange conta de serviço do SQL Server, clique em Olá **logon** guia, digite **CORP\SQLSvc1** (para **ContosoSQL1**) ou **CORP\SQLSvc2** ( para **ContosoSQL2**) em **nome da conta**, preencha e confirme a senha hello e, em seguida, clique em **Okey**.
22. Na caixa de diálogo de saudação que é aberta, clique em **Sim** toorestart Olá serviço do SQL Server. Depois Olá serviço do SQL Server for reiniciado, alterações feitas no hello **propriedades** caixa de diálogo entrarão em vigor.
23. Sair de máquinas virtuais de saudação.

## <a name="create-hello-availability-group"></a>Criar grupo de disponibilidade Olá
Agora você está pronto tooconfigure um grupo de disponibilidade. Abaixo está uma descrição do que você deve fazer:

* Crie um novo banco de dados (**MyDB1**) em **ContosoSQL1**.
* Faça um backup completo e um backup de log de transações do banco de dados de saudação.
* Restaurar Olá completo e backups de log muito**ContosoSQL2** com hello **NORECOVERY** opção.
* Criar grupo de disponibilidade da saudação (**AG1**) com confirmação síncrona, failover automático e réplicas secundárias legíveis.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Crie o banco de dados do hello MyDB1 ContosoSQL1
1. Se você não já saiu sessões de área de trabalho remota Olá para **ContosoSQL1** e **ContosoSQL2**, faça isso agora.
2. Arquivo RDP Olá aberto para **ContosoSQL1**e entre como **CORP\Install**.
3. No **Explorador de Arquivos**, em **C:\\**, crie um diretório chamado **backup**. Você usará esse diretório tooback e restaurar seu banco de dados.
4. Clique o novo diretório de hello, aponte muito**compartilhar com**e, em seguida, clique em **pessoas específicas**, conforme mostrado no hello captura de tela a seguir.
   
    ![Criar uma pasta de backup](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Adicionar **CORP\SQLSvc1**e, em seguida, atribua a ele Olá **leitura/gravação** permissão. Adicionar **CORP\SQLSvc2**e, em seguida, atribua a ele Olá **leitura** permissão, conforme mostrado no hello captura de tela a seguir e, em seguida, clique em **compartilhamento**. Após a conclusão do processo de compartilhamento de arquivo hello, clique em **feito**.
   
    ![Conceder permissões para a pasta de Backup](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. toocreate Olá banco de dados, da saudação **iniciar** menu, abrir **SQL Server Management Studio**e, em seguida, clique em **conectar** instância do SQL Server tooconnect toohello padrão.
7. No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Banco de Dados** e, em seguida, clique em **Novo Banco de Dados**.
8. Em **Nome do banco de dados**, digite **MyDB1** e, em seguida, clique em **OK**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Faça um backup completo de MyDB1 e restaure-o no ContosoSQL2
1. um backup completo de saudação do banco de dados, além de toomake **Pesquisador de objetos**, expanda **bancos de dados**, com o botão direito **MyDB1**, ponto muito**tarefas**, e em seguida, clique em **backup**.
2. Em Olá **fonte** seção, mantenha **o tipo de Backup** definido muito**completo**. Em Olá **destino** seção, clique em **remover** caminho do arquivo padrão tooremove Olá Olá arquivo de backup.
3. Em Olá **destino** seção, clique em **adicionar**.
4. Em Olá **nome de arquivo** caixa de texto, digite  **\\ContosoSQL1\backup\MyDB1.bak**, clique em **Okey**e, em seguida, clique em **Okey** novamente tooback o banco de dados de saudação. Quando termina de operação de backup hello, clique em **Okey** novamente tooclose caixa de diálogo de saudação.
5. toomake uma transação efetuar backup de banco de dados de saudação **Pesquisador de objetos**, expanda **bancos de dados**, clique com botão direito **MyDB1**, ponto muito**tarefas**e, em seguida, clique em **backup**.
6. No tipo **Backup**, selecione **Log de Transações**. Lembre-Olá **destino** toohello de conjunto de caminho um especificado anteriormente do arquivo e, em seguida, clique em **Okey**. Após a conclusão da operação de backup hello, clique em **Okey** novamente.
7. toorestore Olá completo e a transação de backups de log **ContosoSQL2**, abra arquivo hello RDP para **ContosoSQL2**e entre como **CORP\Install**. Sair da sessão de área de trabalho remota Olá para **ContosoSQL1** abrir.
8. De saudação **iniciar** menu, abrir **SQL Server Management Studio**e, em seguida, clique em **conectar** instância do SQL Server tooconnect toohello padrão.
9. No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Bancos de Dados** e, em seguida, em **Restaurar Banco de Dados**.
10. Em Olá **fonte** seção, selecione **dispositivo**e clique botão de reticências Olá **...** .
11. Em **Selecionar dispositivos de backup**, clique em **Adicionar**.
12. Em **Local do Arquivo de Backup**, digite **\\ContosoSQL1\backup**, clique em **Atualizar**, selecione **MyDB1.bak**, clique em **OK**e, em seguida, clique em **OK** novamente. Agora você deve ver hello backup completo e backup de log Olá Olá **toorestore de conjuntos de Backup** painel.
13. Vá toohello **opções** página, selecione **RESTORE WITH NORECOVERY** na **estado de recuperação**e, em seguida, clique em **Okey** o banco de dados do toorestore hello. Depois de Olá conclusão da operação de restauração, clique em **Okey**.

### <a name="create-hello-availability-group"></a>Criar grupo de disponibilidade Olá
1. Vá fazer toohello sessão de área de trabalho remota para **ContosoSQL1**. Em **Pesquisador de objetos** no SQL Server Management Studio, clique com botão direito **alta disponibilidade AlwaysOn**e, em seguida, clique em **Assistente de novo grupo de disponibilidade**, conforme mostrado no Olá captura de tela abaixo.
   
    ![Inicie o Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Em Olá **Introdução** , clique em **próximo**. Em Olá **especificar nome do grupo de disponibilidade** página, digite **AG1** na **nome do grupo de disponibilidade**, em seguida, clique em **próximo** novamente.
   
    ![Assistente para Novo Grupo de Disponibilidade, Especificar o nome do grupo de disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Em Olá **Selecionar bancos de dados** , selecione **MyDB1**e, em seguida, clique em **próximo**. banco de dados de saudação atende aos pré-requisitos de saudação para um grupo de disponibilidade porque você ter obtido pelo menos um backup completo na réplica primária pretendida de saudação.
   
    ![Assistente de Novo Grupo de Disponibilidade, Selecionar bancos de dados](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. em Olá **especificar réplicas** , clique em **adicionar réplica**.
   
    ![Assistente de Novo Grupo de Disponibilidade, Selecionar réplicas](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. Em Olá **conectar tooServer** caixa de diálogo, digite **ContosoSQL2** na **nome do servidor**e, em seguida, clique em **conectar**.
   
    ![Assistente de novo grupo de disponibilidade, conectar tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Em Olá **especificar réplicas** página, você verá agora **ContosoSQL2** listadas na **réplicas disponíveis**. Configure réplicas de saudação conforme Olá captura de tela a seguir. Quando tiver terminado, clique em **Avançar**.
   
    ![Assistente de Novo Grupo de Disponibilidade, Selecionar réplicas (Concluído)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Em Olá **selecionar sincronização de dados inicial** , selecione **somente junção**e, em seguida, clique em **próximo**. Você já executou a sincronização de dados manualmente quando você fez backups completos e transações de saudação em **ContosoSQL1** e restaurado-los em **ContosoSQL2**. Você pode escolher não tooperform Olá operações de backup e restauração do banco de dados e selecione **completo** toolet Olá Assistente de novo grupo de disponibilidade execute a sincronização de dados para você. No entanto, isso não é recomendado para grandes bancos de dados que se encontram em algumas empresas.
   
    ![Assistente de Novo Grupo de Disponibilidade, Selecionar sincronização inicial de dados](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Em Olá **validação** , clique em **próximo**. Esta página deve ter aparência semelhante toohello captura de tela a seguir. Há um aviso para configuração de ouvinte Olá porque você não configurou um ouvinte de grupo de disponibilidade. Você pode ignorar esse aviso, pois este tutorial não configura um ouvinte. ouvinte de saudação tooconfigure depois de concluir este tutorial, consulte [configurar um ouvinte ILB para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).
   
    ![Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Em Olá **resumo** , clique em **concluir**e aguarde enquanto o Assistente de saudação configura o novo grupo de disponibilidade hello. Em Olá **andamento** página, você pode clicar em **mais detalhes** tooview Olá detalhadas progresso. Após a conclusão do assistente Olá, inspecionar Olá **resultados** tooverify página grupo de disponibilidade Olá é criado com êxito, conforme mostrado no hello captura de tela a seguir e, em seguida, clique em **fechar** tooexit Olá Assistente.
   
    ![Assistente de Novo Grupo de Disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. No **Pesquisador de Objetos**, expanda **Alta Disponibilidade AlwaysOn** e, em seguida, expanda **Grupos de Disponibilidade**. Agora você deve ver o novo grupo de disponibilidade Olá neste contêiner. Clique com o botão direito do mouse em **AG1 (Primário)** e, em seguida, clique em **Mostrar Painel**.
    
     ![Mostrar Painel do Grupo de Disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. O **painel AlwaysOn** devem aparência semelhante toohello um no hello captura de tela a seguir. Você pode ver réplicas hello, modo de failover de saudação de cada réplica e o estado de sincronização de saudação.
    
     ![Painel do Grupo de Disponibilidade](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Retornar muito**Gerenciador do servidor**, clique em **ferramentas**e, em seguida, abra **Gerenciador de Cluster de Failover**.
13. Expanda **Cluster1.corp.contoso.com** e depois expanda **Serviços e Aplicativos**. Selecione **funções** e observe que Olá **AG1** função do grupo de disponibilidade foi criada. Observe que o AG1 não tem um endereço IP pelo banco de dados que os clientes podem se conectar a toohello o grupo de disponibilidade, porque você não configurou um ouvinte. Você pode se conectar diretamente toohello o nó principal para operações de leitura / gravação e o nó secundário do Olá para consultas somente leitura.
    
     ![AG no Gerenciador de Cluster de Failover](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> Não tente toofail sobre o grupo de disponibilidade de saudação do hello Gerenciador de Cluster de Failover. Todas as operações de failover devem ser executadas no **Painel do AlwaysOn** no SQL Server Management Studio. Para obter mais informações, consulte [restrições usando Olá Gerenciador de Cluster de Failover com grupos de disponibilidade](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora você implementou com êxito o SQL Server AlwaysOn criando um grupo de disponibilidade no Azure. tooconfigure um ouvinte para esse grupo de disponibilidade, consulte [configurar um ouvinte de ILB para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).

Para obter outras informações sobre como usar o SQL Server no Azure, veja [SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

