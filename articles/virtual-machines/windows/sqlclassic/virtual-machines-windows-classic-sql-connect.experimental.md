---
title: "aaaConnect tooa Máquina Virtual do SQL Server no Azure (clássica) | Microsoft Docs"
description: "Saiba como tooconnect tooSQL Server em execução em uma máquina Virtual no Azure. Este tópico usa o modelo de implantação clássico hello. cenários de saudação diferem dependendo da configuração de rede hello e local de saudação do cliente de saudação."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 9577e4bdad79435e34a64fc669ec4848649fc945
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Conecte-se tooa Máquina Virtual do SQL Server no Azure (implantação clássico)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](../sql/virtual-machines-windows-sql-connect.md)
> * [Clássico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Visão geral
Este tópico descreve como tooconnect tooyour do SQL Server da instância em execução em uma máquina virtual do Azure. Ele aborda alguns [cenários gerais de conectividade](#connection-scenarios) e descreve [etapas detalhadas para configurar a conectividade com o SQL Server em uma VM do Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Se você estiver usando máquinas virtuais do Gerenciador de recursos, consulte [tooa Máquina Virtual do SQL Server no Azure usando o Gerenciador de recursos de conexão](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Cenários de conexão
forma de saudação um cliente se conecta tooSQL Server em execução em uma máquina Virtual é diferente dependendo do local de saudação do cliente hello e configuração de rede de máquina/hello. Esses cenários incluem:

* [Conecte-se tooSQL Server no hello mesmo serviço de nuvem](#connect-to-sql-server-in-the-same-cloud-service)
* [Conectar tooSQL Server sobre Olá internet](#connect-to-sql-server-over-the-internet)
* [Conectar tooSQL Server no hello mesma rede virtual](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Antes de se conectar com qualquer um desses métodos, você deve seguir Olá [as etapas na conectividade de tooconfigure artigo](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Conecte-se tooSQL Server no hello mesmo serviço de nuvem
Várias máquinas virtuais podem ser criadas em Olá mesmo serviço de nuvem. máquinas de toounderstand virtual nesse cenário, consulte [como máquinas virtuais de tooconnect com um serviço de nuvem ou rede virtual](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Nesse cenário, um cliente em uma máquina virtual tenta tooconnect tooSQL Server em execução em outra máquina virtual no hello mesmo serviço de nuvem.

Nesse cenário, você pode se conectar usando Olá VM **nome** (também mostrado como **nome do computador** ou **hostname** no portal de saudação). Este é o nome de saudação fornecida para a VM de saudação durante a criação. Por exemplo, se você nomeou a VM do SQL **mysqlvm**, uma VM cliente em Olá mesmo serviço de nuvem pode usar Olá tooconnect de cadeia de caracteres de conexão a seguir:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Conecte-se tooSQL Server pela Internet da saudação
Se você quiser tooconnect tooyour mecanismo de banco de dados do SQL Server de saudação à Internet, você deve criar um ponto de extremidade de máquina virtual para comunicação TCP de entrada. Essa etapa de configuração do Azure, direciona a entrada TCP porta tráfego tooa pela porta TCP que é a máquina virtual de toohello acessível.

Olá de tooconnect pela internet, você deve usar DNS nome e hello VM ponto de extremidade número da porta da VM Olá (configurado neste artigo). Olá toofind nome DNS, navegue toohello Azure portal e selecione **máquinas virtuais (clássicas)**. Em seguida, selecione sua máquina virtual. Olá **nome DNS** é mostrado no hello **visão geral** seção.

Por exemplo, considere uma máquina virtual clássica chamada **mysqlvm** com o nome DNS **mysqlvm7777.cloudapp.net** e um ponto de extremidade da VM de **57500**. Supondo que a conectividade configurada adequadamente, Olá cadeia de caracteres de conexão a seguir pode ser máquina de virtual Olá tooaccess usado em qualquer lugar em Olá internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Embora essa cadeia de caracteres de conexão habilita a conectividade de clientes sobre Olá da internet, isso não significa que qualquer pessoa pode se conectar a tooyour do SQL Server. Clientes fora tem correto toohello de nome de usuário e senha. Para obter segurança adicional, não use porta bem conhecidos de saudação 1433 para ponto de extremidade de máquina virtual público hello. E, se possível, considere adicionar uma ACL no ponto de extremidade toorestrict tráfego toohello somente clientes que permite que você. Para obter instruções sobre como usar ACLs com pontos de extremidade, consulte [gerenciar Olá ACL em um ponto de extremidade](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Quando você usa essa técnica toocommunicate com o SQL Server, todos os dados de saída de hello datacenter do Azure é o assunto toonormal [de preço em transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Conectar tooSQL Server no hello mesma rede virtual
[Rede Virtual](../../../virtual-network/virtual-networks-overview.md) permite cenários adicionais. Você pode se conectar a máquinas virtuais na mesma rede virtual, mesmo se essas VMs existe nos serviços de nuvem diferente de saudação. E com um [VPN site a site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), você pode criar uma arquitetura híbrida que conecta as VMs a computadores e redes locais.

Redes virtuais também permitem que você toojoin seu domínio de tooa VMs do Azure. Unindo tooa domínio é toouse de maneira Olá somente autenticação do Windows com o SQL Server. Olá outros cenários de conexão requerem autenticação do SQL com nomes de usuário e senhas.

Se você planejar tooconfigure um ambiente de domínio e a autenticação do Windows, não é necessário o ponto de extremidade público tooconfigure hello ou hello autenticação do SQL e logons. Nesse cenário, você pode se conectar a instância do SQL Server tooyour, especificando o nome de VM do SQL Server de saudação na cadeia de caracteres de conexão de saudação. Olá exemplo a seguir pressupõe que a autenticação do Windows foi configurada e que o usuário Olá foi concedido a instância do SQL Server toohello acesso.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Etapas para configurar a conectividade com o SQL Server em uma VM do Azure
Olá, as etapas a seguir demonstram como tooconnect toohello a instância do SQL Server sobre Olá internet usando o SQL Server Management Studio (SSMS). No entanto, hello mesmas etapas se aplicam toomaking sua máquina de virtual do SQL Server acessível para seus aplicativos em execução no local e no Azure.

Antes de se conectar toohello instância do SQL Server de outra VM ou Olá da internet, você deve concluir Olá tarefas a seguir:

* [Criar um ponto de extremidade TCP para a máquina virtual de saudação](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Abra as portas TCP no firewall do Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configurar toolisten do SQL Server em Olá protocolo TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Configurar o SQL Server para autenticação do modo misto](#configure-sql-server-for-mixed-mode-authentication)
* [Criar logons de autenticação do SQL Server](#create-sql-server-authentication-logins)
* [Determinar nome DNS de saudação da máquina virtual de saudação](#determine-the-dns-name-of-the-virtual-machine)
* [Conectar toohello mecanismo de banco de dados de outro computador](#connect-to-the-database-engine-from-another-computer)

caminho de conexão de saudação é resumido por Olá diagrama a seguir:

![Conectando a máquina de virtual do SQL Server tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Próximas etapas
Se você também estiver planejando grupos de disponibilidade do AlwaysOn toouse para alta disponibilidade e recuperação de desastres, considere implementar um ouvinte. Clientes de banco de dados se conectar toohello ouvinte em vez de diretamente tooone Olá instâncias do SQL Server. Olá ouvinte rotas clientes toohello réplica primária do grupo de disponibilidade de saudação. Para obter mais informações, consulte [Configurar um ouvinte de ILB para Grupos de Disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).

É importante tooreview que todos hello práticas recomendadas de segurança para o SQL Server em execução em uma máquina virtual do Azure. Para obter mais informações, veja [Considerações sobre segurança para o SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-security.md).

[Explorar Olá aprendizado](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) para o SQL Server em máquinas virtuais do Azure. 

Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

