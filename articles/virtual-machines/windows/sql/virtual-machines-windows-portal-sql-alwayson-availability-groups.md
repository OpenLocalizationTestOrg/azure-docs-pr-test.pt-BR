---
title: "aaaSet a alta disponibilidade para máquinas virtuais do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Este tutorial mostra como toocreate uma disponibilidade de AlwaysOn agrupar com máquinas virtuais do Azure no modo do Gerenciador de recursos do Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Configurar um grupo de disponibilidade AlwaysOn nas máquinas virtuais do Azure automaticamente: Resource Manager

Este tutorial mostra como toocreate uma disponibilidade de SQL Server grupo que usa máquinas virtuais do Gerenciador de recursos do Azure. Olá tutorial usa o Azure folhas tooconfigure um modelo. Você pode examinar as configurações padrão de saudação, digite as configurações necessárias e atualizar folhas Olá no portal de saudação que você percorrer este tutorial.

tutorial completo Olá cria um grupo de disponibilidade do SQL Server em máquinas de virtuais do Azure que incluem hello elementos a seguir:

* Uma rede virtual que tem várias sub-redes, incluindo uma de front-end e uma de back-end
* Dois controladores de domínio que têm um domínio do Active Directory
* Duas máquinas virtuais que executam o SQL Server e são implantados toohello sub-rede de back-end e toohello ingressado no domínio de Active Directory
* Um cluster de failover de três nós com o modelo de quorum de maioria de nós Olá
* Um grupo de disponibilidade que tem duas réplicas de confirmação síncrona de um banco de dados de disponibilidade

Olá ilustração a seguir representa uma solução completa de saudação.

![Arquitetura de laboratório de teste para grupos de disponibilidade no Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Todos os recursos nesta solução pertencem tooa único grupo de recursos.

Antes de iniciar este tutorial, confirme a seguir hello:

* Você já tem uma conta do Azure. Se não tiver uma, [inscreva-se para uma conta de avaliação](http://azure.microsoft.com/pricing/free-trial/).
* Você já sabe como toouse Olá GUI tooprovision uma máquina virtual de SQL Server da Galeria de máquinas virtuais de saudação. Para saber mais, veja [Provisionamento de uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Você já tem uma compreensão sólida dos grupos de disponibilidade. Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Se você estiver interessado em usar os grupos de disponibilidade com o SharePoint, confira também [Configure SQL Server 2012 Always On Availability Groups for SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx)(Configurar grupos de disponibilidade AlwaysOn do SQL Server 2012 para o SharePoint 2013).
>
>

Neste tutorial, use hello Azure portal para:

* Escolha Olá sempre no modelo do portal de saudação.
* Examine as configurações de modelo hello e atualizar alguns parâmetros de configuração para o seu ambiente.
* Monitor do Azure enquanto cria todo o ambiente de saudação.
* Conecte o controlador de domínio tooa e, em seguida, tooa servidor que executa o SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Cluster de saudação provisionar da Galeria de saudação
Azure fornece uma imagem da Galeria para toda a solução hello. modelo de saudação toolocate:

1. Entre no toohello portal do Azure usando sua conta.
2. No portal do Azure de Olá, clique em **+ novo** tooopen Olá **novo** folha.
3. Em Olá **novo** folha, procure **AlwaysOn**.
   ![Localizar o modelo AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Nos resultados da pesquisa hello, localize **Cluster do SQL Server AlwaysOn**.
   ![Modelo AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. Em **Selecionar um modelo de implantação**, escolha **Resource Manager**.

### <a name="basics"></a>Noções básicas
Clique em **Noções básicas de** e configurar Olá configurações a seguir:

* **Nome de usuário administrador** é uma conta de usuário que tenha permissões de administrador de domínio e é um membro da função de servidor fixa de sysadmin saudação do SQL Server em ambas as instâncias do SQL Server. Neste tutorial, use **DomainAdmin**.
* **Senha** é Olá senha de conta de administrador de domínio hello. Use uma senha complexa. Confirme senha hello.
* **Assinatura** assinatura hello Azure cobra implantado toorun todos os recursos para o grupo de disponibilidade hello. Se a conta tiver várias assinaturas, você poderá especificar outra assinatura.
* **Grupo de recursos** é nome Olá Olá grupo toowhich pertencem todos os recursos do Azure que são criados por este modelo. Neste tutorial, use **SQL-HA-RG**. Para saber mais, consulte [Visão geral do Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Local** é Olá região do Azure em que o tutorial Olá cria recursos hello. Escolha uma região do Azure.

Olá seguinte captura de tela é um concluído **Noções básicas sobre** folha:

![Noções básicas](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Clique em **OK**.

### <a name="domain-and-network-settings"></a>Configurações de rede e de domínio
Esse modelo da galeria do Azure cria um domínio e controladores de domínio. Ele também cria uma rede e duas sub-redes. modelo de saudação não é possível criar servidores em um domínio existente ou a rede virtual. próxima etapa do Hello define as configurações de rede e de domínio de saudação.

Em Olá **as configurações de rede e de domínio** folha, examine Olá predefinição valores para configurações de rede e de domínio hello:

* **Nome de domínio raiz de floresta** é o nome de domínio de saudação do domínio do Active Directory Olá cluster Olá hosts. Tutorial de hello, use **contoso.com**.
* **Nome de rede virtual** é o nome da rede Olá Olá rede virtual do Azure. Tutorial de hello, use **autohaVNET**.
* **Nome de sub-rede do controlador de domínio** é o nome de saudação de uma parte da rede virtual Olá esse controlador de domínio de saudação de hosts. Use **subnet-1**. Essa sub-rede usa o prefixo de endereço **10.0.0.0/24**.
* **Nome da sub-rede do SQL Server** é Olá nome de uma parte de servidores de saudação de hosts que executam o SQL Server e o arquivo hello testemunha de compartilhamento de rede virtual do hello. Use **subnet-2**. Essa sub-rede usa o prefixo de endereço **10.0.1.0/26**.

toolearn mais sobre redes virtuais no Azure, consulte [visão geral da rede Virtual](../../../virtual-network/virtual-networks-overview.md).  

Olá **as configurações de rede e de domínio** devem aparência Olá captura de tela a seguir:

![Configurações de rede e de domínio](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Se necessário, você pode alterar esses valores. Para este tutorial, use valores predefinidos de saudação.

Examine as configurações de saudação e, em seguida, clique em **Okey**.

### <a name="availability-group-settings"></a>Configurações de grupo de disponibilidade
Em **as configurações do grupo de disponibilidade**, examine Olá valores para o grupo de disponibilidade Olá predefinidos e Olá ouvinte.

* **Nome do grupo de disponibilidade** é o nome de recurso de cluster Olá Olá grupo de disponibilidade. Neste tutorial, use **Contoso-ag**.
* **Nome do ouvinte de grupo de disponibilidade** é usada pelo cluster hello e balanceador de carga interno hello. Clientes que se conectam tooSQL Server podem usar este nome tooconnect toohello apropriado réplica Olá banco de dados. Neste tutorial, use **Contoso-listener**.
* **Porta do ouvinte de grupo de disponibilidade** Especifica a porta TCP do ouvinte do SQL Server Olá Olá. Para este tutorial, use a porta de padrão de hello, **1433**.

Se necessário, você pode alterar esses valores. Para este tutorial, use valores predefinidos de saudação.  

![configurações de grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Clique em **OK**.

### <a name="virtual-machine-size-storage-settings"></a>Tamanho da máquina virtual, configurações de armazenamento
Em **tamanho da VM, as configurações de armazenamento**, escolha um tamanho de máquina virtual do SQL Server e examine Olá outras configurações.

* **Tamanho da máquina virtual do SQL Server** tamanho Olá para máquinas virtuais que executam o SQL Server. Escolha um tamanho de máquina virtual apropriado para sua carga de trabalho. Se você estiver criando esse ambiente tutorial hello, use **DS2**. Para cargas de trabalho de produção, escolha um tamanho de máquina virtual que pode dar suporte a cargas de trabalho de saudação. Várias cargas de trabalho de produção exigem **DS4** ou maior. modelo de saudação cria duas máquinas virtuais desse tamanho e instala o SQL Server em cada um deles. Para obter mais informações, confira [Tamanhos das máquinas virtuais](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Saudação de instalações do Azure Enterprise Edition do SQL Server. custo de saudação depende Olá edition e o tamanho da máquina virtual hello. Para obter informações detalhadas sobre os custos atuais, confira [Máquinas virtuais - preço](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **O tamanho de máquina virtual do controlador de domínio** é o tamanho da máquina virtual Olá para Olá controladores de domínio. Neste tutorial, use **D2**.
* **Tamanho da máquina virtual de testemunha de compartilhamento de arquivo** é o tamanho da máquina virtual Olá para testemunha de compartilhamento de arquivo hello. Neste tutorial, use **A1**.
* **Conta de armazenamento SQL** é nome Olá Olá da conta de armazenamento que contém os dados do SQL Server de saudação e discos do sistema operacional. Neste tutorial, use **alwaysonsql01**.
* **Conta de armazenamento do controlador de domínio** é o nome de Olá Olá da conta de armazenamento para Olá controladores de domínio. Neste tutorial, use **alwaysondc01**.
* **Tamanho de disco de dados do SQL Server** em TB é o tamanho de saudação do disco de dados do SQL Server Olá em TB. Especifique um número de 1 a 4. Neste tutorial, use **1**.
* **Otimização de armazenamento** define as configurações específicas de armazenamento para máquinas de virtuais do SQL Server Olá com base no tipo de carga de trabalho de saudação. Todas as máquinas virtuais de SQL Server neste cenário usar armazenamento premium com o cache de host do disco do Azure definido somente tooread. Além disso, você pode otimizar as configurações do SQL Server para cargas de trabalho hello, escolhendo uma dessas três configurações:

  * **Carga de trabalho geral** não define nenhuma configuração específica.
  * **Processamento transacional** define os sinalizadores de rastreamento 1117 e 1118.
  * **Data warehousing** define os sinalizadores de rastreamento 1117 e 610.

Neste tutorial, use a **Carga de trabalho geral**.

![Configurações de armazenamento de tamanho da VM](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Examine as configurações de saudação e, em seguida, clique em **Okey**.

#### <a name="a-note-about-storage"></a>Uma observação sobre armazenamento
Otimizações adicionais dependem do tamanho Olá Olá do SQL Server de discos de dados. Para cada terabyte de disco de dados, o Azure adiciona mais 1 TB de Armazenamento Premium. Quando um servidor requer de 2 TB ou mais, o modelo de saudação cria um pool de armazenamento nas máquinas virtuais do SQL Server. Um pool de armazenamento é uma forma de virtualização de armazenamento onde vários discos serão configurado tooprovide maior capacidade, desempenho e resiliência.  modelo de Hello, em seguida, cria um espaço de armazenamento no pool de armazenamento hello e apresenta um sistema operacional de toohello de disco de dados único. modelo de saudação designa esse disco como disco de dados Olá para o SQL Server. modelo Olá ajusta o pool de armazenamento de saudação do SQL Server usando Olá configurações a seguir:

* Tamanho de distribuição é hello intercalar a configuração de disco virtual hello. As cargas de trabalho transacionais usam 64 KB. As cargas de trabalho do data warehouse usam 256 KB.
* A resiliência é simples (sem resiliência).

> [!NOTE]
> Armazenamento premium do Azure é localmente redundante e mantém três cópias dos dados de saudação dentro de uma única região, resiliência adicional no pool de armazenamento Olá não é necessária.
>
>

* Contagem de colunas é igual a número Olá dos discos no pool de armazenamento hello.

Para saber mais sobre o espaço de armazenamento e os pools de armazenamento, veja:

* [Visão geral de Espaços de Armazenamento](http://technet.microsoft.com/library/hh831739.aspx)
* [Backup do Windows Server e pools de armazenamento](http://technet.microsoft.com/library/dn390929.aspx)

Para saber mais sobre as práticas recomendadas de configuração do SQL Server, confira [Práticas recomendadas relacionadas ao desempenho para o SQL Server em máquinas virtuais do Azure](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Configurações do SQL Server
Em **configurações do SQL Server**, revisar e modificar o prefixo do nome de máquina virtual saudação do SQL Server, a versão do SQL Server, a conta de serviço do SQL Server e a senha e Olá agenda de manutenção de aplicação de patch automática do SQL.

* **Prefixo do nome do SQL Server** é toocreate usado um nome para cada máquina virtual de SQL Server. Neste tutorial, use **sqlserver**. Olá modelo nomes Olá máquinas virtuais do SQL Server *0 sqlserver* e *1 do sqlserver*.
* **Versão do SQL Server** é a versão de saudação do SQL Server. Neste tutorial, use **SQL Server 2014**. Você também pode escolher **SQL Server 2012** ou **SQL Server 2016**.
* **Nome de usuário da conta de serviço do SQL Server** é o nome de conta de domínio Olá para Olá serviço do SQL Server. Neste tutorial, use **sqlservice**.
* **Senha** é senha Olá Olá conta de serviço do SQL Server.  Use uma senha complexa. Confirme senha hello.
* **Agenda de manutenção de aplicação de patch do SQL automática** identifica o dia de saudação da semana de saudação que o Azure corrige automaticamente Olá SQL Servers. Neste tutorial, digite **Domingo**.
* **Hora de início da manutenção de aplicação de patch do SQL automática** é tempo de saudação do dia para a região do Azure de saudação quando começa a aplicação de patch automática.

> [!NOTE]
> Olá janela para cada máquina virtual de aplicação de patch é gradativa em uma hora. Apenas uma máquina virtual é corrigida em uma interrupção de tooprevent tempo dos serviços.
>
>

![Configurações do SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Examine as configurações de saudação e, em seguida, clique em **Okey**.

### <a name="summary"></a>Resumo
Na página de resumo de hello Azure valida configurações de saudação. Você também pode baixar o modelo de saudação. Saudação de revisão resumida. Clique em **OK**.

### <a name="buy"></a>Comprar
Essa folha final contém os **Termos de uso** e a **Política de Privacidade**. Examine essas informações. Quando estiver pronto para máquinas virtuais do Azure toostart toocreate hello e todos Olá outros recursos necessários para o grupo de disponibilidade hello, clique em **criar**.

Olá portal do Azure cria o grupo de recursos de saudação e todos os recursos de saudação.

## <a name="monitor-deployment"></a>Monitorar implantação
Monitorar o progresso de implantação de saudação do hello portal do Azure. Um ícone que representa a implantação de saudação é fixado automaticamente toohello painel do portal do Azure.

![Painel do Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Conecte-se tooSQL Server
novas instâncias de saudação do SQL Server estão em execução em máquinas virtuais que têm endereços IP conectado à internet. Você pode remoto da área de trabalho (RDP) diretamente tooeach máquina virtual SQL Server.

tooRDP tooa SQL Server, siga estas etapas:

1. De Olá painel do portal do Azure, verifique se que a implantação de saudação teve êxito.
2. Clique em **Recursos**.
3. Em Olá **recursos** folha, clique em **0 sqlserver**, que é o nome do computador de saudação de uma das máquinas virtuais Olá que está executando o SQL Server.
4. Na folha de saudação para **0 sqlserver**, clique em **conectar**. Seu navegador perguntará se você deseja tooopen ou salva o objeto de conexão remota hello. Clique em **Abrir**.
5. **Conexão de área de trabalho remota** pode avisar que Olá Editor desta conexão remota não pode ser identificado. Clique em **Conectar**.
6. Segurança do Windows solicita que você tooenter seu endereço IP credenciais tooconnect toohello Olá primário do controlador de domínio. Clique em **Usar outra conta**. Em **Nome de usuário**, digite **contoso\DomainAdmin**. Você configurou essa conta quando você define o nome de usuário de administrador Olá no modelo de saudação. Use Olá complexa que você escolheu quando você configurou o modelo de saudação.
7. **Área de trabalho remota** pode avisá-lo esse computador Olá não pôde ser autenticado devido tooproblems com seu certificado de segurança. Ela mostra o nome do certificado de segurança de saudação. Se você seguiu o tutorial Olá, nome de saudação é **0.contoso.com sqlserver**. Clique em **Sim**.

Agora você está conectado com a máquina virtual do RDP toohello do SQL Server. Abra o SQL Server Management Studio, conecte-se a instância padrão de toohello do SQL Server e verifique se o que grupo de disponibilidade hello está configurado.
