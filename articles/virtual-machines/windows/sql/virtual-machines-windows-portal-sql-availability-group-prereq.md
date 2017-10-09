---
title: "grupos de disponibilidade do servidor de aaaSQL - máquinas virtuais do Azure - pré-requisitos | Microsoft Docs"
description: "Este tutorial mostra como pré-requisitos de saudação do tooconfigure para criar uma disponibilidade de SQL Server Always On agrupar em VMs do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Pré-requisitos Olá completa para a criação de grupos de disponibilidade AlwaysOn em máquinas virtuais do Azure

Este tutorial mostra como toocomplete Olá pré-requisitos para a criação de um [SQL Server Always On o grupo de disponibilidade em máquinas virtuais (VMs) do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Quando você terminar de pré-requisitos Olá, você tem um servidor testemunha, um controlador de domínio e duas VMs do SQL Server em um único grupo de recursos.

**Tempo estimado**: pode levar algumas horas pré-requisitos do toocomplete hello. Grande parte desse tempo é gasto na criação de máquinas virtuais.

Olá diagrama a seguir ilustra o que você cria no tutorial de saudação.

![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Leia a documentação do grupo de disponibilidade

Este tutorial supõe que você tem uma compreensão básica dos grupos de disponibilidade Always On do SQL Server. Se você não estiver familiarizado com essa tecnologia, veja [Visão geral dos Grupos de Disponibilidade AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Criar uma conta do Azure
Você precisa de uma conta do Azure. Você pode [abrir uma conta gratuita do Azure](/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar os benefícios de assinante do Visual Studio](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
1. Entrar toohello [portal do Azure](http://portal.azure.com).
2. Clique em  **+**  toocreate um novo objeto no portal de saudação.

   ![Novo objeto](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Tipo **grupo de recursos** em Olá **Marketplace** janela Pesquisar.

   ![Grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Clique em **Grupo de recursos**.
5. Clique em **Criar**.
6. Em Olá **grupo de recursos** folha, em **nome do grupo de recursos**, digite um nome para o grupo de recursos de saudação. Por exemplo, digite **sql-ha-rg**.
7. Se você tiver várias assinaturas do Azure, verifique se assinatura Olá Olá assinatura do Azure que deseja toocreate grupo de disponibilidade de saudação.
8. Selecione um local. local de saudação é Olá região do Azure onde deseja que o grupo de disponibilidade toocreate hello. Para este tutorial, vamos toobuild todos os recursos em um local do Azure.
9. Verifique **toodashboard Pin** é verificada. Essa configuração opcional coloca um atalho para o grupo de recursos de saudação em Olá painel do portal do Azure.

   ![Grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Clique em **criar** toocreate grupo de recursos de saudação.

Azure cria o grupo de recursos hello e pins um grupo de recursos do atalho toohello no portal de saudação.

## <a name="create-hello-network-and-subnets"></a>Criar sub-redes e rede Olá
Olá próxima etapa é redes de saudação toocreate e sub-redes no grupo de recursos do Azure hello.

solução de saudação usa uma rede virtual com duas sub-redes. Olá [visão geral da rede Virtual](../../../virtual-network/virtual-networks-overview.md) fornece mais informações sobre redes no Azure.

rede virtual do toocreate hello:

1. No hello portal do Azure, no grupo de recursos, clique em **+ adicionar**. Olá abre Azure **tudo** folha.

   ![Novo item](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Pesquise pela **rede virtual**.

     ![Pesquisar pela rede virtual](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Clique em **Rede virtual**.
4. Em Olá **rede Virtual** folha, clique em Olá **Gerenciador de recursos de** modelo de implantação e clique **criar**.

    Olá tabela a seguir mostra as configurações de saudação para rede virtual hello:

   | **Campo** | Valor |
   | --- | --- |
   | **Nome** |autoHAVNET |
   | **Espaço de endereço** |10.33.0.0/24 |
   | **Nome da sub-rede** |Administrador |
   | **Intervalo de endereços da sub-rede** |10.33.0.0/29 |
   | **Assinatura** |Especifique que você pretende toouse de assinatura de saudação. **Assinatura** estará em branco se você tiver apenas uma assinatura. |
   | **Grupo de recursos** |Escolha **usar existente** e selecione o nome de Olá Olá do grupo de recursos. |
   | **Localidade** |Especifique Olá local do Azure. |

   O intervalo de endereços de espaço e a sub-rede do endereço pode ser diferente da tabela de saudação. Dependendo de sua assinatura, o portal de saudação sugere um espaço de endereço disponível e o intervalo de endereços de sub-rede correspondente. Se não houver espaço de endereço disponível suficiente, use uma assinatura diferente.

   exemplo Hello usa Olá nome da sub-rede **Admin**. Essa sub-rede é Olá para controladores de domínio.

5. Clique em **Criar**.

   ![Configurar rede virtual Olá](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

O Azure retorna toohello painel do portal e notifica quando a nova rede de saudação é criado.

### <a name="create-a-second-subnet"></a>Criar uma segunda sub-rede
Olá, nova rede virtual tem uma sub-rede, denominada **Admin**. controladores de domínio Olá usam essa sub-rede. Olá VMs do SQL Server usa uma segunda sub-rede denominada **SQL**. tooconfigure essa sub-rede:

1. No painel, clique em grupo de recursos de saudação que você criou, **SQL-HA-RG**. Localizar rede Olá no grupo de recursos de saudação em **recursos**.

    Se **SQL-HA-RG** não estiver visível, encontrá-lo clicando **grupos de recursos** e filtrando pelo nome do grupo de recursos de saudação.
2. Clique em **autoHAVNET** na lista de saudação de recursos. Azure abre a folha de configuração de rede hello.
3. Em Olá **autoHAVNET** folha de rede virtual, em **configurações** , clique em **sub-redes**.

    Observe a sub-rede de saudação que você já tenha criado.

   ![Configurar rede virtual Olá](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Crie uma segunda sub-rede. Clique em **+ Subnet (+ Sub-rede)**.
6. Em Olá **Adicionar sub-rede** folha, configurar a sub-rede Olá digitando **sqlsubnet** em **nome**. O Azure especifica automaticamente um **Intervalo de endereços**válido. Verifique se este intervalo de endereços tem pelo menos 10 endereços nele. Em um ambiente de produção, você poderá exigir mais endereços.
7. Clique em **OK**.

    ![Configurar rede virtual Olá](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Olá a tabela a seguir resume os parâmetros de configuração de rede de saudação:

| **Campo** | Valor |
| --- | --- |
| **Nome** |**autoHAVNET** |
| **Espaço de endereço** |Esse valor depende de espaços de endereço disponível Olá em sua assinatura. Um valor típico é 10.0.0.0/16. |
| **Nome da sub-rede** |**admin** |
| **Intervalo de endereços da sub-rede** |Esse valor depende de intervalos de endereço disponível Olá em sua assinatura. Um valor típico é 10.0.0.0/24. |
| **Nome da sub-rede** |**sqlsubnet** |
| **Intervalo de endereços da sub-rede** |Esse valor depende de intervalos de endereço disponível Olá em sua assinatura. Um valor típico é 10.0.1.0/24. |
| **Assinatura** |Especifique que você pretende toouse de assinatura de saudação. |
| **Grupo de recursos** |**SQL-HA-RG** |
| **Localidade** |Especificar Olá mesmo local que você escolheu para o grupo de recursos de saudação. |

## <a name="create-availability-sets"></a>Criar conjuntos de disponibilidade

Antes de criar máquinas virtuais, você precisa toocreate conjuntos de disponibilidade. Conjuntos de disponibilidade reduzem tempo de inatividade Olá para eventos de manutenção planejada ou não. Um conjunto de disponibilidade do Azure é um grupo lógico de recursos que o Azure coloca em domínios de falha física e em domínios de atualização. Um domínio de falha garante que os membros de saudação do conjunto de disponibilidade Olá têm recursos de energia e rede separados. Um domínio de atualização assegura que membros do conjunto de disponibilidade de saudação não desativados para manutenção em Olá mesmo tempo. Para obter mais informações, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Você precisará de dois conjuntos de disponibilidade. Um é Olá para controladores de domínio. Olá segundo é para Olá VMs do SQL Server.

toocreate uma disponibilidade definida, vá toohello grupo de recursos e clique em **adicionar**. Filtrar resultados de saudação digitando **conjunto de disponibilidade**. Clique em **conjunto de disponibilidade** Olá resultados e, em seguida, clique em **criar**.

Configure dois conjuntos de disponibilidade, de acordo com os parâmetros de toohello em Olá a tabela a seguir:

| **Campo** | Conjunto de disponibilidade do controlador de domínio | Conjunto de disponibilidade do SQL Server |
| --- | --- | --- |
| **Nome** |adavailabilityset |sqlavailabilityset |
| **Grupo de recursos** |SQL-HA-RG |SQL-HA-RG |
| **Domínios de falha** |3 |3 |
| **Domínios de atualização** |5 |3 |

Depois de criar conjuntos de disponibilidade hello, retorne o grupo de recursos toohello em Olá portal do Azure.

## <a name="create-domain-controllers"></a>Criar controladores de domínio
Depois que você criou a rede hello, sub-redes, conjuntos de disponibilidade e um balanceador de carga para a Internet, você está pronto toocreate máquinas de virtuais Olá Olá para controladores de domínio.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Criar máquinas virtuais para Olá controladores de domínio
toocreate e configurar controladores de domínio hello, retornar toohello **SQL-HA-RG** grupo de recursos.

1. Clique em **Adicionar**. Olá **tudo** folha é aberta.
2. Digite **Windows Server 2016 Datacenter**.
3. Clique em **Windows Server 2016 Datacenter**. Em Olá **Datacenter do Windows Server 2016** folha, verifique se esse modelo de implantação de saudação é **Gerenciador de recursos de**e, em seguida, clique em **criar**. Olá abre Azure **criar a máquina virtual** folha.

Repita Olá anterior etapas toocreate duas máquinas virtuais. Nome hello duas máquinas de virtuais:

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > Olá **CD do ad-secundário** máquina virtual é opcional, tooprovide alta disponibilidade para serviços de domínio do Active Directory.
  >
  >

Olá tabela a seguir mostra as configurações de saudação para essas duas máquinas:

| **Campo** | Valor |
| --- | --- |
| **Nome** |Primeiro controlador de domínio: *ad-primary-dc*.</br>Segundo controlador de domínio *ad-secondary-dc*. |
| **Tipo de disco da VM** |SSD |
| **Nome de usuário** |DomainAdmin |
| **Senha** |Contoso!0000 |
| **Assinatura** |*Sua assinatura* |
| **Grupo de recursos** |SQL-HA-RG |
| **Localidade** |*Seu local* |
| **Tamanho** |DS1_V2 |
| **Armazenamento** | **Usar discos gerenciados** - **Sim** |
| **Rede virtual** |autoHAVNET |
| **Sub-rede** |admin |
| **Endereço IP público** |*Mesmo nome hello VM* |
| **Grupo de segurança de rede** |*Mesmo nome hello VM* |
| **Conjunto de disponibilidade** |adavailabilityset </br>**Domínios de falha**: 2</br>**Domínio de atualização**: 2|
| **Diagnostics** |Habilitado |
| **Conta de armazenamento de diagnóstico** |*Criada automaticamente* |

   >[!IMPORTANT]
   >Você só pode colocar uma VM em um conjunto de disponibilidade ao criá-la. Você não pode alterar a disponibilidade de Olá definida depois que uma VM é criada. Consulte [gerenciar Olá disponibilidade das máquinas virtuais](../manage-availability.md).

O Azure cria máquinas virtuais de saudação.

Depois de máquinas virtuais de saudação são criadas, configure o controlador de domínio de saudação.

### <a name="configure-hello-domain-controller"></a>Configurar o controlador de domínio Olá
Olá etapas a seguir, configurar Olá **CD do ad-primário** máquina como um controlador de domínio para corp.contoso.com.

1. No portal de hello, abra Olá **SQL-HA-RG** grupo de recursos e selecione Olá **CD do ad-primário** máquina. Em Olá **CD do ad-primário** folha, clique em **conectar** tooopen uma RDP de arquivo para acesso de área de trabalho remoto.

    ![Conecte-se a máquina virtual de tooa](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Entre com sua conta de administrador (**\DomainAdmin**) e senha (**Contoso!0000**) configuradas.
3. Por padrão, Olá **Gerenciador do servidor** painel deve ser exibido.
4. Clique em Olá **adicionar funções e recursos** link no painel de saudação.

    ![Gerenciador de servidores - adicionar funções](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Selecione **próximo** até chegar toohello **funções de servidor** seção.
6. Selecione Olá **serviços de domínio do Active Directory** e **servidor DNS** funções. Quando for solicitado, acrescente os recursos adicionais que são necessários para essas funções.

   > [!NOTE]
   > Windows avisa que não há nenhum endereço IP estático. Se você estiver testando configuração hello, clique em **continuar**. Para cenários de produção, definir Olá toostatic de endereço IP no hello portal do Azure, ou [PowerShell tooset Olá endereço IP estático do computador do controlador de domínio Olá](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Caixa de diálogo Adicionar Funções](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Clique em **próximo** até que você alcance Olá **confirmação** seção. Selecione Olá **reinicialização do servidor de destino Olá automaticamente, se necessário** caixa de seleção.
8. Clique em **Instalar**.
9. Encerradas recursos Olá instalar, retorne toohello **Gerenciador do servidor** painel.
10. Selecione Olá novo **AD DS** opção no painel esquerdo da saudação.
11. Clique em Olá **mais** link na barra de aviso Olá amarelo.

    ![Caixa de diálogo do AD DS no hello VM do servidor DNS](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. Em Olá **ação** coluna da saudação **todos os detalhes de tarefas do servidor** caixa de diálogo, clique em **promover este controlador de domínio do servidor tooa**.
13. Em Olá **Assistente de configuração de serviços do Active Directory domínio**, use Olá valores a seguir:

    | **Página** | Configuração |
    | --- | --- |
    | **Configuração de Implantação** |**Adicionar uma nova floresta**<br/> **Nome do domínio raiz** = corp.contoso.com |
    | **Opções de Controlador de Domínio** |**Senha DSRM** = Contoso!0000<br/>**Confirmar Senha** = Contoso!0000 |
14. Clique em **próximo** toogo por meio de Olá outras páginas no Assistente de saudação. Em Olá **verificação de pré-requisitos** , verifique se que você vê a seguinte mensagem de saudação: **todas as verificações de pré-requisitos passaram com êxito**. Você pode examinar as mensagens de aviso aplicáveis, mas é possível toocontinue com instalação hello.
15. Clique em **Instalar**. Olá **CD do ad-primário** máquina virtual reinicializa automaticamente.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Observe o endereço IP Olá Olá primário do controlador de domínio

Use o controlador de domínio primário Olá para o DNS. Observe o endereço IP do controlador de domínio primário hello.

Endereço IP do controlador de domínio primário de saudação tooget unidirecional é por meio de saudação portal do Azure.

1. No hello portal do Azure, abra o grupo de recursos de saudação.

2. Clique em controlador de domínio primário hello.

3. Na folha de controlador de domínio primário hello, clique em **interfaces de rede**.

![Interfaces de rede](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Observe o endereço IP privado de saudação para este servidor.

### <a name="configure-hello-virtual-network-dns"></a>Configurar rede virtual de saudação DNS
Depois de criar o primeiro controlador de domínio hello e ativar o DNS no primeiro servidor de saudação, configure Olá rede virtual toouse esse servidor DNS.

1. No hello portal do Azure, clique na rede virtual hello.

2. Em **Configurações**, clique em **Servidor DNS**.

3. Clique em **personalizado**e digite o endereço IP privado de Olá Olá primário do controlador de domínio.

4. Clique em **Salvar**.

### <a name="configure-hello-second-domain-controller"></a>Configurar o segundo controlador de domínio Olá
Após a reinicialização do controlador de domínio primário hello, você pode configurar o segundo controlador de domínio hello. Esta etapa opcional é para alta disponibilidade. Siga estas etapas tooconfigure Olá segundo controlador de domínio:

1. No portal de hello, abra Olá **SQL-HA-RG** grupo de recursos e selecione Olá **CD do ad-secundário** máquina. Em Olá **CD do ad-secundário** folha, clique em **conectar** tooopen uma RDP de arquivo para acesso de área de trabalho remoto.
2. Entrar toohello VM usando sua conta de administrador configurada (**BUILTIN\DomainAdmin**) e a senha (**Contoso! 0000**).
3. Alteração Olá preferido endereço toohello endereço do servidor DNS saudação do controlador de domínio.
4. Em **Central de rede e compartilhamento**, clique em Olá interface de rede.
   ![Interface de rede](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Clique em **Propriedades**.
6. Clique em **Protocolo IP versão 4 (TCP/IPv4)** e clique em **Propriedades**.
7. Selecione **Olá usar endereços de servidor DNS a seguir** e especifique o endereço Olá Olá controlador de domínio primário no **servidor DNS preferencial**.
8. Clique em **Okey**e, em seguida, **fechar** toocommit alterações de saudação. Agora você está Olá toojoin capaz de VM muito**corp.contoso.com**.

   >[!IMPORTANT]
   >Se você perder Olá conexão tooyour área de trabalho remota depois de alterar a configuração de DNS de saudação, vá toohello Azure portal e reinicialização Olá máquinas virtuais.

9. No controlador de domínio secundário do hello toohello de área de trabalho remota, abra **painel do Gerenciador do servidor**.
10. Clique em Olá **adicionar funções e recursos** link no painel de saudação.

    ![Gerenciador de servidores - adicionar funções](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Selecione **próximo** até chegar toohello **funções de servidor** seção.
12. Selecione Olá **serviços de domínio do Active Directory** e **servidor DNS** funções. Quando for solicitado, acrescente os recursos adicionais que são necessários para essas funções.
13. Encerradas recursos Olá instalar, retorne toohello **Gerenciador do servidor** painel.
14. Selecione Olá novo **AD DS** opção no painel esquerdo da saudação.
15. Clique em Olá **mais** link na barra de aviso Olá amarelo.
16. Em Olá **ação** coluna da saudação **todos os detalhes de tarefas do servidor** caixa de diálogo, clique em **promover este controlador de domínio do servidor tooa**.
17. Em **configuração de implantação**, selecione **adicionar um domínio existente do tooan de controlador de domínio**.
   ![Configuração de Implantação](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Clique em **Selecionar**.
19. Conecte-se usando a conta de administrador de saudação (**CORP. Contoso.COM\domainadmin**) e a senha (**Contoso! 0000**).
20. Em **selecione um domínio na floresta Olá**, clique em seu domínio e, em seguida, clique em **Okey**.
21. Em **opções do controlador de domínio**, use os valores padrão de saudação e definir uma senha do DSRM.

   >[!NOTE]
   >Olá **opções de DNS** página pode avisá-lo que uma delegação para esse servidor DNS não pode ser criada. Você pode ignorar esse aviso em ambientes que não são de produção.
22. Clique em **próximo** até que alcance de diálogo Olá Olá **pré-requisitos** verificar. Em seguida, clique em **Instalar**.

Depois que o servidor de saudação terminar as alterações de configuração hello, reinicie o servidor de saudação.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Adicionar Olá toohello de controlador de domínio segundo endereço IP privado toohello servidor DNS de VPN

No portal do Azure, na rede virtual, de saudação altere Olá DNS tooinclude Olá endereço IP de servidor controlador de domínio secundário Olá. Isso permite que a redundância de serviço DNS hello.

### <a name=DomainAccounts></a>Configurar contas de domínio Olá

Próximas etapas de hello, configure contas do Active Directory de saudação. Olá tabela a seguir mostra as contas de saudação:

| |Conta de instalação<br/> |sqlserver-0 <br/>Conta do SQL Server e do serviço SQL Agent |sqlserver-1<br/>Conta do SQL Server e do serviço SQL Agent
| --- | --- | --- | ---
|**Nome** |Instalar |SQLSvc1 | SQLSvc2
|**SamAccountName do usuário** |Instalar |SQLSvc1 | SQLSvc2

As etapas a seguir do uso Olá toocreate cada conta.

1. Entrar toohello **CD do ad-primário** máquina.
2. No **Gerenciador do Servidor**, selecione **Ferramentas** e clique em **Centro Administrativo do Active Directory**.   
3. Selecione **corp (local)** no painel esquerdo do hello.
4. Em Olá direito **tarefas** painel, selecione **novo**e, em seguida, clique em **usuário**.
   ![Centro Administrativo do Active Directory](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Defina uma senha complexa para cada conta.<br/> Para ambientes de produção não toonever de conta de usuário do conjunto Olá expirar.

5. Clique em **Okey** toocreate usuário de saudação.
6. Repita etapas anteriores para cada uma das três contas de saudação do hello.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Conceder permissões de saudação necessária toohello conta de instalação
1. Em Olá **Centro Administrativo do Active Directory**, selecione **corp (local)** no painel esquerdo da saudação. Em seguida, no lado direito da saudação **tarefas** painel, clique em **propriedades**.

    ![Propriedades do usuário CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Selecione **extensões**e, em seguida, clique em Olá **avançado** botão Olá **segurança** guia.
3. Em Olá **configurações de segurança avançadas para corp** caixa de diálogo, clique em **adicionar**.
4. Clique em **Selecionar uma entidade**, procure **CORP\Install**e, em seguida, clique em **OK**.
5. Selecione Olá **ler todas as propriedades** caixa de seleção.

6. Selecione Olá **criar objetos de computador** caixa de seleção.

     ![Permissões de usuário corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Clique em **OK** e em **OK** novamente. Olá fechar **corp** janela Propriedades.

Agora que você terminou a configuração do Active Directory e objetos de saudação do usuário, crie duas VMs do SQL Server e uma VM de servidor testemunha. Em seguida, ingresse em todos os três domínio de toohello.

## <a name="create-sql-server-vms"></a>Criar VMs do SQL Server

Crie três máquinas virtuais adicionais. solução de saudação requer duas máquinas virtuais com instâncias do SQL Server. Uma terceira máquina virtual funcionará como uma testemunha. O Windows Server 2016 pode usar uma [testemunha em nuvem](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness), no entanto, para manter a consistência com sistemas operacionais anteriores, este documento usa uma máquina virtual para uma testemunha.  

Antes de prosseguir, considere Olá deisign decisões a seguir.

* **Armazenamento – Azure Managed Disks**

   Para o armazenamento de máquina virtual hello, use discos gerenciado do Azure. A Microsoft recomenda Managed Disks para máquinas virtuais do SQL Server. Gerenciado lida com armazenamento de discos em segundo plano da saudação. Além disso, quando as máquinas virtuais com discos gerenciados estão em Olá mesmo conjunto de disponibilidade, o Azure distribui Olá recursos tooprovide apropriado a redundância de armazenamento. Para obter informações adicionais, consulte [Visão geral do Azure Managed Disks](../managed-disks-overview.md). Para obter informações específicas sobre discos gerenciados em um conjunto de disponibilidade, consulte [Usar discos gerenciados para VMs no conjunto de disponibilidade](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Rede – Endereços IP privados em produção**

   Para máquinas virtuais de hello, este tutorial usa endereços IP públicos. Isso permite que a conexão remota diretamente a máquina virtual de toohello via Olá internet - facilita as etapas de configuração. Em ambientes de produção, a Microsoft recomenda somente endereços IP privados da margem de vulnerabilidade de saudação ordem tooreduce da instância do SQL Server Olá recursos da VM.

### <a name="create-and-configure-hello-sql-server-vms"></a>Criar e configurar Olá VMs do SQL Server
Em seguida, crie três VMs: duas VMs do SQL Server e uma VM para um nó de cluster adicional. toocreate Olá VMs, volte toohello **SQL-HA-RG** grupo de recursos, clique em **adicionar**, pesquisa Olá apropriado item da galeria, clique em **Máquina Virtual**e, em seguida, Clique em **da galeria**. Use as informações de Olá Olá toohelp tabela criar VMs Olá a seguir:


| Página | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Selecionar item de galeria apropriado Olá |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise no Windows Server 2016** |**SQL Server 2016 SP1 Enterprise no Windows Server 2016** |
| **Noções básicas** |**Nome** = cluster-fsw<br/>**Nome de usuário** = DomainAdmin<br/>**Senha** = Contoso!0000<br/>**Assinatura** = Sua assinatura<br/>**Grupo de recursos** = SQL-HA-RG<br/>**Local** = Seu local do Azure |**Nome** = sqlserver-0<br/>**Nome de usuário** = DomainAdmin<br/>**Senha** = Contoso!0000<br/>**Assinatura** = Sua assinatura<br/>**Grupo de recursos** = SQL-HA-RG<br/>**Local** = Seu local do Azure |**Nome** = sqlserver-1<br/>**Nome de usuário** = DomainAdmin<br/>**Senha** = Contoso!0000<br/>**Assinatura** = Sua assinatura<br/>**Grupo de recursos** = SQL-HA-RG<br/>**Local** = Seu local do Azure |
| **Tamanho** |**SIZE** = DS1\_V2 (1 core, 3,5 GB) |**SIZE** = DS2\_V2 (2 núcleos, 7 GB)</br>tamanho de saudação deve dar suporte ao armazenamento SSD (suporte a discos Premium. )) |**SIZE** = DS2\_V2 (2 núcleos, 7 GB) |
| **Configurações** |**Armazenamento**: use discos gerenciados.<br/>**Rede virtual** = autoHAVNET<br/>**Sub-rede** = sqlsubnet(10.1.1.0/24)<br/>**Endereço IP público** gerado automaticamente.<br/>**Grupo de segurança de rede** = Nenhum<br/>**Monitorando Diagnóstico** = Habilitado<br/>**Conta de armazenamento de diagnóstico** = Use uma conta de armazenamento gerada automaticamente<br/>**Conjunto de disponibilidade** = sqlAvailabilitySet<br/> |**Armazenamento**: use discos gerenciados.<br/>**Rede virtual** = autoHAVNET<br/>**Sub-rede** = sqlsubnet(10.1.1.0/24)<br/>**Endereço IP público** gerado automaticamente.<br/>**Grupo de segurança de rede** = Nenhum<br/>**Monitorando Diagnóstico** = Habilitado<br/>**Conta de armazenamento de diagnóstico** = Use uma conta de armazenamento gerada automaticamente<br/>**Conjunto de disponibilidade** = sqlAvailabilitySet<br/> |**Armazenamento**: use discos gerenciados.<br/>**Rede virtual** = autoHAVNET<br/>**Sub-rede** = sqlsubnet(10.1.1.0/24)<br/>**Endereço IP público** gerado automaticamente.<br/>**Grupo de segurança de rede** = Nenhum<br/>**Monitorando Diagnóstico** = Habilitado<br/>**Conta de armazenamento de diagnóstico** = Use uma conta de armazenamento gerada automaticamente<br/>**Conjunto de disponibilidade** = sqlAvailabilitySet<br/> |
| **Definições do SQL Server** |Não aplicável |**Conectividade SQL** = Particular (em rede virtual)<br/>**Porta** = 1433<br/>**Autenticação SQL** = Desabilitar<br/>**Configuração de armazenamento** = Geral<br/>**Aplicação de patch automatizada** = Domingo às 2:00<br/>**Backup automatizado** = Desabilitado</br>**Integração do Cofre de Chaves do Azure** = Desabilitado |**Conectividade SQL** = Particular (em rede virtual)<br/>**Porta** = 1433<br/>**Autenticação SQL** = Desabilitar<br/>**Configuração de armazenamento** = Geral<br/>**Aplicação de patch automatizada** = Domingo às 2:00<br/>**Backup automatizado** = Desabilitado</br>**Integração do Cofre de Chaves do Azure** = Desabilitado |

<br/>

> [!NOTE]
> tamanhos de máquina Olá sugeridos aqui destinam-se para grupos de disponibilidade de teste em VMs do Azure. Para melhor desempenho em cargas de trabalho de produção Olá, consulte recomendações Olá para tamanhos de máquina do SQL Server e configuração em [práticas recomendadas de desempenho para o SQL Server em máquinas virtuais do Azure](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Depois de provisionamento Olá três VMs, você precisa toojoin-los toohello **corp.contoso.com** máquinas de toohello do domínio e grant CORP\Install direitos administrativos.

### <a name="joinDomain"></a>Ingressar em domínio do hello servidores toohello

Você está agora capaz de toojoin Olá VMs muito**corp.contoso.com**. Você deve seguir Olá Olá VMs do SQL Server e o arquivo hello compartilhar servidor testemunha:

1. Se conectar remotamente a máquina virtual toohello **BUILTIN\DomainAdmin**.
2. Em **Gerenciador do Servidor**, clique em **Servidor Local**.
3. Clique em Olá **WORKGROUP** link.
4. Em Olá **nome do computador** seção, clique em **alteração**.
5. Selecione Olá **domínio** caixa de seleção e digite **corp.contoso.com** na caixa de texto de saudação. Clique em **OK**.
6. Em hello **a segurança do Windows** caixa de diálogo pop-up, especifique as credenciais de saudação para conta de administrador de domínio saudação padrão (**CORP\DomainAdmin**) e a senha de saudação (**Contoso! 0000**).
7. Quando você vir a mensagem "Bem-vindo toohello corp.contoso.com domínio", clique em **Okey**.
8. Clique em **fechar**e, em seguida, clique em **reiniciar agora** na caixa de diálogo de pop-up de saudação.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Adicionar usuário de Corp\Install de saudação como um administrador em cada cluster de VM

Depois de reiniciar cada máquina virtual como um membro do domínio hello, adicionar **CORP\Install** como um membro do grupo de administradores locais hello.

1. Aguarde até que a saudação VM for reiniciada, em seguida, inicie o arquivo RDP de saudação novamente do hello toosign de controlador de domínio primário no muito**0 sqlserver** usando Olá **CORP\DomainAdmin** conta.
   >[!TIP]
   >Certifique-se de que você entrar com a conta de administrador de domínio hello. Nas etapas anteriores do hello, você estava usando a conta de administrador interno em hello. Agora que hello servidor estiver no domínio hello, use a conta de domínio de saudação. Na sua sessão de RDP, especifique *DOMÍNIO*\\*nome de usuário*.

2. Em **Gerenciador do Servidor**, selecione **Ferramentas** e clique em **Gerenciamento do Computador**.
3. Em Olá **gerenciamento do computador** janela, expanda **usuários e grupos locais**e, em seguida, selecione **grupos**.
4. Clique duas vezes em Olá **administradores** grupo.
5. Em Olá **propriedades de administradores** caixa de diálogo, clique em Olá **adicionar** botão.
6. Insira o usuário Olá **CORP\Install**e, em seguida, clique em **Okey**.
7. Clique em **Okey** tooclose Olá **propriedades do administrador** caixa de diálogo.
8. Repita as etapas anteriores de saudação em **sqlserver 1** e **fsw cluster**.

### <a name="setServiceAccount"></a>Configurar as contas de serviço do SQL Server Olá

Em cada VM do SQL Server, defina a conta de serviço do SQL Server Olá. Use contas Olá criado quando você [configurou contas de domínio Olá](#DomainAccounts).

1. Abra o **SQL Server Configuration Manager**.
2. Clique no serviço do SQL Server Olá e clique **propriedades**.
3. Definir Olá conta e senha.
4. Repita essas etapas em Olá outra VM do SQL Server.  

Para grupos de disponibilidade do SQL Server, cada VM do SQL Server precisa toorun como uma conta de domínio.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Criar uma entrada em cada VM do SQL Server para a conta de instalação Olá

Use o grupo de disponibilidade do hello instalação conta (CORP\install) tooconfigure hello. Essa conta precisa toobe um membro da saudação **sysadmin** a função de servidor fixa em cada VM do SQL Server. Olá etapas a seguir criam uma entrada para a conta de instalação hello:

1. Conectar o servidor de toohello por meio de saudação protocolo de área de trabalho remota (RDP) usando Olá  *\<MachineName\>\DomainAdmin* conta.

1. Abra o SQL Server Management Studio e conecte-se toohello a instância local do SQL Server.

1. Em **Pesquisador de Objetos**, clique em **Segurança**.

1. Clique com botão direito do mouse em **Logons**. Clique em **Novo Logon**.

1. Em **Logon – Novo**, clique em **Pesquisar**.

1. Clique em **Locais**.

1. Insira as credenciais de rede do administrador de domínio de saudação.

1. Use conta de instalação de saudação.

1. Um membro de saudação do conjunto de saudação entrar toobe **sysadmin** função de servidor fixa.

1. Clique em **OK**.

Repita Olá anterior etapas em Olá outra VM do SQL Server.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Adicionar tooboth de recursos de cluster de Failover VMs do SQL Server

recursos de cluster de Failover tooadd, Olá em ambas as VMs do SQL Server a seguir:

1. Conectar máquina de virtual do SQL Server toohello por meio de saudação protocolo de área de trabalho remota (RDP) usando o hello *CORP\install* conta. Abra o **Painel do Gerenciador do Servidor**.
2. Clique em Olá **adicionar funções e recursos** link no painel de saudação.

    ![Gerenciador de servidores - adicionar funções](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Selecione **próximo** até chegar toohello **recursos de servidor** seção.
4. Em **Recursos**, selecione **Clustering de Failover**.
5. Adicione os recursos adicionais necessários.
6. Clique em **instalar** tooadd recursos de saudação.

Repita as etapas de saudação em Olá outra VM do SQL Server.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Configurar o firewall de saudação em cada VM do SQL Server

solução de saudação requer Olá portas TCP toobe abrir no firewall Olá a seguir:

- **VM do SQL Server**:<br/>
   Porta 1433 para uma instância padrão do SQL Server.
- **Investigação do Azure Load Balancer:**<br/>
   Qualquer porta disponível. Os exemplos geralmente usam 59999.
- **Ponto de extremidade de espelhamento de banco de dados:** <br/>
   Qualquer porta disponível. Os exemplos geralmente usam 5022.

Olá firewall portas necessidade toobe abertos em ambas as VMs do SQL Server.

método Hello de abertura de portas Olá depende da solução de firewall de saudação que você usar. Olá próxima seção explica como Olá tooopen portas no Firewall do Windows. Abra as portas Olá necessários em cada uma das VMs do SQL Server.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Abrir uma porta TCP no firewall Olá

1. Em Olá primeiro servidor do SQL **iniciar** tela, inicie **Firewall do Windows com segurança avançada**.
2. No painel esquerdo do hello, selecione **regras de entrada**. No painel direito da saudação, clique em **nova regra**.
3. Para **Tipo de Regra**, escolha **Porta**.
4. Para a porta hello, especifique **TCP** e hello tipo apropriado de números de porta. Consulte Olá exemplo a seguir:

   ![Firewall do SQL](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Clique em **Avançar**.
6. Em Olá **ação** página, mantenha **Permitir conexão Olá** selecionado e, em seguida, clique em **próximo**.
7. Em Olá **perfil** página, aceite as configurações padrão de saudação e, em seguida, clique em **próximo**.
8. Em Olá **nome** página, especifique um nome de regra (como **investigação de balanceamento de carga do Azure**) no hello **nome** caixa de texto e clique **concluir**.

Repita essas etapas em Olá segundo VM do SQL Server.

## <a name="next-steps"></a>Próximas etapas

* [Criar um grupo de disponibilidade AlwaysOn do SQL Server em máquinas virtuais do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
