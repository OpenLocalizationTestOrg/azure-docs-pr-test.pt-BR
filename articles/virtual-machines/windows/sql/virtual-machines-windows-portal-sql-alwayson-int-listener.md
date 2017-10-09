---
title: "aaaCreate um ouvinte de grupo de disponibilidade do SQL Server em máquinas virtuais do Azure | Microsoft Docs"
description: "Instruções passo a passo de como criar um ouvinte para um grupo de disponibilidade Always On para SQL Server em máquinas virtuais do Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Configurar um balanceador de carga para um grupo de disponibilidade Always On no Azure
Este artigo explica como toocreate um balanceador de carga para um grupo de disponibilidade do SQL Server Always On no Azure virtual máquinas que estão em execução no Gerenciador de recursos do Azure. Um grupo de disponibilidade exige um balanceador de carga quando instâncias do SQL Server de saudação em máquinas virtuais do Azure. Balanceador de carga Olá armazena o endereço IP Olá para o ouvinte do grupo de disponibilidade de saudação. Se um grupo de disponibilidade abranger várias regiões, cada região precisará de um balanceador de carga.

toocomplete nesta tarefa, você precisa toohave implantado de um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure que está executando o com o Gerenciador de recursos. Máquinas virtuais do SQL Server deve pertencer toohello mesmo conjunto de disponibilidade. Você pode usar o hello [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically criar grupo de disponibilidade de saudação no Gerenciador de recursos. Este modelo cria automaticamente um balanceador de carga interno para você. 

Se preferir, você poderá [configurar manualmente um grupo de disponibilidade](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Este artigo exige que os grupos de disponibilidade já estejam configurados.  

Os tópicos relacionados incluem:

* [Configurar os grupos de disponibilidade Always On na VM do Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurar uma conexão de rede virtual com rede virtual usando o PowerShell e o Azure Resource Manager](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Examinando neste artigo, você cria e configurar um balanceador de carga no hello portal do Azure. Após a conclusão do processo de saudação, você configura Olá toouse Olá endereço IP do balanceador de carga Olá para o ouvinte do grupo de disponibilidade de saudação.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Criar e configurar o balanceador de carga Olá Olá portal do Azure
Nesta parte da tarefa hello, Olá a seguir:

1. No hello portal do Azure, crie balanceador de carga hello e configurar o endereço IP de saudação.
2. Configure o pool de back-end de saudação.
3. Crie a investigação de saudação. 
4. Definir regras de balanceamento de carga de saudação.

> [!NOTE]
> Se houver instâncias do SQL Server de saudação em vários grupos de recursos e as regiões, execute cada etapa duas vezes, uma vez em cada grupo de recursos.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Etapa 1: Criar balanceador de carga hello e configurar o endereço IP de saudação
Primeiro, crie o balanceador de carga de saudação. 

1. No portal do Azure de Olá, abra o grupo de recursos de saudação que contém máquinas virtuais a saudação do SQL Server. 

2. No grupo de recursos de saudação, clique em **adicionar**.

3. Procurar **balanceador de carga** e, em seguida, nos resultados da pesquisa hello, selecione **balanceador de carga**, que é publicado pelo **Microsoft**.

4. Em Olá **balanceador de carga** folha, clique em **criar**.

5. Em Olá **criar balanceador de carga** caixa de diálogo caixa, configure o balanceador de carga de saudação da seguinte maneira:

   | Configuração | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa o balanceador de carga de saudação. Por exemplo, **sqlLB**. |
   | **Tipo** |**Interno**: a maioria das implementações usar um balanceador de carga interno, que permite que aplicativos em Olá mesmo grupo de disponibilidade do toohello tooconnect de rede virtual.  </br> **Externa**: permite que aplicativos tooconnect toohello o grupo de disponibilidade por meio de uma conexão de Internet pública. |
   | **Rede virtual** |Selecione a rede virtual Olá Olá instâncias do SQL Server estão em. |
   | **Sub-rede** |Selecione a sub-rede Olá Olá instâncias do SQL Server estiverem em. |
   | **Atribuição de endereço IP** |**Estático** |
   | **Endereço IP privado** |Especifique um endereço IP disponível na sub-rede hello. Quando você cria um ouvinte no cluster hello, use esse endereço IP. Em um script do PowerShell, neste artigo, use esse endereço de saudação `$ILBIP` variável. |
   | **Assinatura** |Se você tiver várias assinaturas, este campo poderá aparecer. Selecione Olá assinatura que você deseja tooassociate com esse recurso. Ele é normalmente Olá mesma assinatura como todos os recursos de Olá Olá grupo de disponibilidade. |
   | **Grupo de recursos** |Selecione o grupo de recursos de saudação que são instâncias do SQL Server Olá no. |
   | **Localidade** |Selecione Olá local do Azure que são instâncias do SQL Server Olá no. |

6. Clique em **Criar**. 

O Azure cria o balanceador de carga hello. o balanceador de carga Olá pertence tooa rede específica, sub-rede, grupo de recursos e local. Após o Azure concluir tarefas hello, verifique se configurações de Balanceador de carga Olá no Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Etapa 2: Configurar o pool de back-end Olá
Chamadas do Azure Olá pool de endereços de back-end *pool de back-end*. Nesse caso, o pool de back-end de saudação é endereços Olá Olá duas instâncias do SQL Server em seu grupo de disponibilidade. 

1. No seu grupo de recursos, clique em balanceador de carga de saudação que você criou. 

2. Em **Configurações**, clique em **Pools de back-end**.

3. Em **pools de back-end**, clique em **adicionar** toocreate um pool de endereços de back-end. 

4. Em **Adicionar pool de back-end**, em **nome**, digite um nome para o pool de back-end de saudação.

5. Em **Máquinas virtuais**, clique em **Adicionar uma máquina virtual**. 

6. Em **escolha máquinas virtuais**, clique em **escolher um conjunto de disponibilidade**e em seguida, especifique o conjunto de disponibilidade de saudação que Olá máquinas de virtuais de SQL Server pertence ao.

7. Depois de ter escolhido o conjunto de disponibilidade de saudação, clique em **escolha máquinas virtuais de saudação**, selecione Olá duas máquinas virtuais que hospedam instâncias do SQL Server Olá no grupo de disponibilidade hello e, em seguida, clique em **selecione**. 

8. Clique em **Okey** tooclose folhas de saudação para **escolha máquinas virtuais**, e **Adicionar pool de back-end**. 

Azure atualiza as configurações de saudação para o pool de endereços de back-end de saudação. Agora seu conjunto de disponibilidade tem um pool de duas instâncias do SQL Server.

### <a name="step-3-create-a-probe"></a>Etapa 3: Criar uma investigação
investigação de saudação define como o Azure verifica que Olá instâncias do SQL Server no momento possui o ouvinte do grupo de disponibilidade de saudação. Azure sondas de serviço de saudação com base no endereço IP de saudação em uma porta que definem quando você cria a investigação de saudação.

1. Balanceador de carga Olá **configurações** folha, clique em **sondas de integridade**. 

2. Em Olá **sondas de integridade** folha, clique em **adicionar**.

3. Configurar a investigação de saudação em Olá **adicionar teste** folha. Olá Use valores tooconfigure Olá investigação a seguir:

   | Configuração | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa a investigação de saudação. Por exemplo, **SQLAlwaysOnEndPointProbe**. |
   | **Protocolo** |**TCP** |
   | **Porta** |Você pode usar qualquer porta disponível. Por exemplo, *59999*. |
   | **Intervalo** |*5* |
   | **Limite não íntegro** |*2* |

4.  Clique em **OK**. 

> [!NOTE]
> Certifique-se de que a porta de saudação especificado é aberta no firewall Olá ambas as instâncias do SQL Server. Ambas as instâncias exigem uma regra de entrada para Olá a porta TCP que você usa. Para saber mais, confira [Adicionar ou Editar Regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure cria investigação hello e, em seguida, usa-tootest qual instância do SQL Server tem ouvinte Olá Olá grupo de disponibilidade.

### <a name="step-4-set-hello-load-balancing-rules"></a>Etapa 4: Definir as regras de balanceamento de carga de saudação
regras de balanceamento de carga Olá configurar como o balanceador de carga de saudação roteia instâncias do tráfego toohello do SQL Server. Para este balanceador de carga, você deve habilitar um retorno de servidor direto porque somente um Olá duas instâncias do SQL Server possui o recurso de ouvinte de grupo de disponibilidade Olá por vez.

1. Balanceador de carga Olá **configurações** folha, clique em **regras de balanceamento de carga**. 

2. Em Olá **regras de balanceamento de carga** folha, clique em **adicionar**.

3. Em Olá **regras de balanceamento de carga de adicionar** folha, configurar a regra de balanceamento de carga de saudação. Saudação de usar as configurações a seguir: 

   | Configuração | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa as regras de balanceamento de carga de saudação. Por exemplo, **SQLAlwaysOnEndPointListener**. |
   | **Protocolo** |**TCP** |
   | **Porta** |*1433* |
   | **Porta de back-end** |*1433*. Esse valor é ignorado porque essa regra usa **IP flutuante (retorno de servidor direto)**. |
   | **Investigação** |Use o nome de saudação do teste de saudação que você criou para este balanceador de carga. |
   | **Persistência de sessão** |**Nenhum** |
   | **Tempo limite de ociosidade (minutos)** |*4* |
   | **IP flutuante (retorno de servidor direto)** |**Habilitado** |

   > [!NOTE]
   > Você pode ter tooscroll para baixo Olá folha tooview todas as configurações de saudação.
   > 

4. Clique em **OK**. 
5. Regra de balanceamento de carga de saudação o Azure configura. Agora o balanceador de carga de saudação está configurado tooroute tráfego toohello SQL instância de servidor que hospeda o ouvinte Olá Olá grupo de disponibilidade. 

Neste ponto, o grupo de recursos de saudação tem um balanceador de carga que se conecta tooboth máquinas do SQL Server. Balanceador de carga Olá também contém um endereço IP para Olá SQL Server Always On disponibilidade ouvinte de grupo, para que a máquina pode responder toorequests Olá para grupos de disponibilidade.

> [!NOTE]
> Se suas instâncias do SQL Server estão em duas regiões separadas, repita as etapas de saudação em Olá outra região. Cada região exige um balanceador de carga. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Configurar Olá cluster toouse Olá IP balanceador de carga
Olá próxima etapa tooconfigure Olá ouvinte no cluster Olá e coloque o ouvinte Olá online. Olá a seguir: 

1. Crie o ouvinte do grupo de disponibilidade Olá no cluster de failover de saudação. 

2. Coloque o ouvinte Olá online.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Etapa 5: Criar o ouvinte do grupo de disponibilidade de saudação no cluster de failover de saudação
Nesta etapa, você criar manualmente o ouvinte do grupo de disponibilidade Olá no Gerenciador de Cluster de Failover e o SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Verificar a configuração de saudação do ouvinte Olá

Se as dependências e os recursos de cluster Olá são configuradas corretamente, você deve estar tooview capaz de ouvinte de saudação no SQL Server Management Studio. tooset Olá porta do ouvinte, Olá a seguir:

1. Inicie o SQL Server Management Studio e conecte a réplica primária toohello.

2. Vá muito**alta disponibilidade AlwaysOn** > **grupos de disponibilidade** > **ouvintes do grupo de disponibilidade**.  
    Agora você deve ver o nome do ouvinte Olá que você criou no Gerenciador de Cluster de Failover. 

3. Clique no nome do ouvinte Olá e clique **propriedades**.

4. Em Olá **porta** , especifique o número da porta saudação do ouvinte do grupo de disponibilidade Olá usando Olá $EndpointPort utilizado antes (1433 foi padrão Olá) e, em seguida, clique em **Okey**.

Agora você tem um grupo de disponibilidade nas máquinas virtuais do Azure em execução no modo Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>Ouvinte de toohello de conexão de saudação do teste
Testar conexão Olá Olá seguinte:

1. Instância do SQL Server do RDP tooa que está em Olá mesmo virtual de rede, mas não não réplica Olá próprio. Esse servidor pode ser outra instância do SQL Server no cluster Olá Olá.

2. Use **sqlcmd** conexão de saudação do utilitário tootest. Por exemplo, a saudação script a seguir estabelece uma **sqlcmd** réplica primária de toohello de conexão por meio do ouvinte Olá com autenticação do Windows:
   
        sqlcmd -S <listenerName> -E

Olá conexão SQLCMD conecta-se automaticamente toohello instância de SQL Server que hospeda a réplica primária hello. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Criar um endereço IP para um grupo de disponibilidade adicional

Cada grupo de disponibilidade usa um ouvinte separado. Cada ouvinte tem seu próprio endereço IP. Use Olá mesmo toohold Olá IP do balanceador de carga para ouvintes adicionais. Depois de criar um grupo de disponibilidade, adicionar balanceador de carga toohello do endereço IP hello e, em seguida, configurar o ouvinte de saudação.

tooadd um balanceador de carga tooa de endereço IP com hello portal do Azure, Olá a seguir:

1. No portal do Azure de Olá, abra Olá grupo de recursos que contém o balanceador de carga hello e clique em balanceador de carga de saudação. 

2. Em **CONFIGURAÇÕES**, clique em **Pool IP de front-ends** e clique em **Adicionar**. 

3. Em **adicionar endereço IP de front-end**, atribua um nome para o front-end hello. 

4. Verifique se esse Olá **rede Virtual** e hello **sub-rede** são Olá mesmo Olá instâncias do SQL Server.

5. Definir o endereço IP de saudação para ouvinte hello. 
   
   >[!TIP]
   >Você pode definir Olá toostatic de endereço IP e digite um endereço que não está sendo usado na sub-rede hello. Como alternativa, você pode definir Olá toodynamic de endereço IP e salvar o novo pool IP front-end hello. Quando você fizer isso, Olá portal do Azure atribui automaticamente um pool de toohello de endereços IP disponível. Você pode, em seguida, reabra o pool de IP de front-end de saudação e alterar Olá atribuição toostatic. 

6. Salve endereço IP hello ouvinte hello. 

7. Adicione um teste de integridade usando Olá configurações a seguir:

   |Configuração |Valor
   |:-----|:----
   |**Nome** |Investigação de saudação do tooidentify um nome.
   |**Protocolo** |TCP
   |**Porta** |Uma porta TCP não usada, que deve estar disponível em todas as máquinas virtuais. Não pode ser usada para qualquer outra finalidade. Não há dois ouvintes podem usar o hello mesma porta de investigação. 
   |**Intervalo** |tentativas de quantidade de saudação de tempo entre a investigação. Use o padrão de saudação (5).
   |**Limite não íntegro** |número de saudação de limites consecutivos que deve falhar antes que uma máquina virtual é considerada não íntegra.

8. Clique em **Okey** toosave investigação de saudação. 

9. Criar uma regra de balanceamento de carga. Clique em **Regras de balanceamento de carga** e clique em **Adicionar**.

10. Configure Olá novo balanceamento de carga regra usando Olá configurações a seguir:

   |Configuração |Valor
   |:-----|:----
   |**Nome** |Regra de balanceamento de carga de saudação de tooidentify um nome. 
   |**Endereço IP de front-end** |Selecione o endereço IP de saudação criado por você. 
   |**Protocolo** |TCP
   |**Porta** |Use a porta Olá que instâncias do SQL Server hello estão usando. Uma instância padrão usa a porta 1433, a menos que você tenha alterado. 
   |**Porta de back-end** |Olá Use mesmo valor **porta**.
   |**Pool de back-end** |pool de saudação que contém máquinas virtuais de saudação com instâncias do SQL Server hello. 
   |**Investigação de integridade** |Escolha investigação Olá criado por você.
   |**Persistência de sessão** |Nenhum
   |**Tempo limite de ociosidade (minutos)** |(4) padrão
   |**IP flutuante (retorno de servidor direto)** | habilitado

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Configurar Olá disponibilidade toouse Olá novo endereço IP do grupo

toofinish Configurando cluster hello, etapas de repetição Olá que você seguiu quando você fez o primeiro grupo de disponibilidade hello. Ou seja, configurar Olá [toouse Olá novo endereço IP de cluster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Depois que você adicionou um endereço IP de ouvinte hello, configure o grupo de disponibilidade adicional de Olá Olá seguinte: 

1. Verifique se a porta de investigação Olá para o novo endereço IP hello está aberta em máquinas virtuais do SQL Server. 

2. [No Gerenciador de Cluster, adicione o ponto de acesso de cliente de Olá](#addcap).

3. [Configurar o recurso IP Olá para o grupo de disponibilidade Olá](#congroup).

   >[!IMPORTANT]
   >Quando você cria um endereço IP Olá, use o endereço IP de saudação que você adicionou toohello balanceador de carga.  

4. [Tornar o recurso de grupo de disponibilidade do SQL Server Olá dependente no ponto de acesso de cliente Olá](#dependencyGroup).

5. [Verifique o acesso para cliente Olá ponto recursos dependentes no endereço IP hello](#listname).
 
6. [Definir parâmetros de cluster de saudação do PowerShell](#setparam).

Depois de configurar Olá disponibilidade grupo toouse Olá novo endereço IP, configure o ouvinte de toohello de conexão de saudação. 

## <a name="next-steps"></a>Próximas etapas

- [Configurar um Grupo de Disponibilidade Always On do SQL Server em Máquinas Virtuais do Azure em diferentes regiões](virtual-machines-windows-portal-sql-availability-group-dr.md)
