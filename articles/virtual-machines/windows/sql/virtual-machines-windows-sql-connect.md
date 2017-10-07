---
title: "aaaConnect tooa Máquina Virtual do SQL Server (Gerenciador de recursos) | Microsoft Docs"
description: "Saiba como tooconnect tooSQL Server em execução em uma máquina Virtual no Azure. Este tópico usa o modelo de implantação clássico hello. cenários de saudação diferem dependendo da configuração de rede hello e local de saudação do cliente de saudação."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Conecte-se tooa Máquina Virtual do SQL Server no Azure (Gerenciador de recursos)
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](virtual-machines-windows-sql-connect.md)
> * [Clássico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Visão geral

Este tópico descreve como tooconnect tooyour do SQL Server da instância em execução em uma máquina virtual do Azure. Ele aborda alguns [cenários gerais de conectividade](#connection-scenarios) e descreve [etapas detalhadas para configurar a conectividade com o SQL Server em uma VM do Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Para ver uma apresentação completa sobre provisionamento e conectividade, veja [Provisionando uma Máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Cenários de conexão

forma de saudação um cliente se conecta tooSQL Server em execução em uma máquina Virtual é diferente dependendo do local de saudação do cliente hello e configuração de rede de saudação.

Se você provisionar uma VM no portal do Azure de saudação do SQL Server, você tem a opção de saudação da especificação de tipo de saudação do **conectividade SQL**.

![Opção de conectividade SQL pública durante o provisionamento](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

As opções de conectividade incluem:

| Opção | Descrição |
|---|---|
| **Pública** | Conectar tooSQL Server sobre Olá internet |
| **Privada** | Conectar tooSQL Server no hello mesma rede virtual |
| **Local** | Conecte-se tooSQL Server localmente no hello mesma máquina virtual | 

Olá, seções a seguir explicam Olá **pública** e **privada** opções em mais detalhes.

## <a name="connect-toosql-server-over-hello-internet"></a>Conecte-se tooSQL Server pela Internet da saudação

Se você desejar tooconnect tooyour mecanismo de banco de dados do SQL Server de saudação da Internet, selecione **pública** para Olá **conectividade SQL** tipo no portal de saudação durante o provisionamento. portal Olá Olá automaticamente as etapas a seguir:

* Habilita o protocolo TCP/IP de saudação do SQL Server.
* Configura uma saudação de tooopen de regra de firewall porta TCP do SQL Server (padrão: 1433).
* Habilita a Autenticação do SQL Server, necessária para acesso público.
* Configura o grupo de segurança de rede Olá no Olá VM tooall TCP no tráfego da saudação porta do SQL Server.

> [!IMPORTANT]
> imagens de máquina virtual de saudação para Olá SQL Server Developer e edições Express automaticamente não habilite o protocolo de saudação TCP/IP. Para edições Express e de desenvolvedor, você deve usar SQL Server Configuration Manager muito[habilitar manualmente o protocolo TCP/IP de saudação](#manualtcp) depois de criar hello VM.

Qualquer cliente com acesso à internet pode se conectar a instância do SQL Server toohello especificando o endereço IP público de saudação da máquina virtual de saudação ou qualquer rótulo DNS atribuído toothat endereço IP. Se Olá porta do SQL Server é 1433, não é necessário toospecify na cadeia de caracteres de conexão de saudação. saudação de cadeia de caracteres de conexão a seguir conecta tooa VM do SQL com um rótulo DNS de `sqlvmlabel.eastus.cloudapp.azure.com` usando a autenticação do SQL (você também pode usar endereço IP público de saudação).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Embora isso habilita a conectividade de clientes sobre Olá da internet, isso não significa que qualquer pessoa pode se conectar a tooyour do SQL Server. Clientes fora tem correto toohello de nome de usuário e senha. No entanto, para segurança adicional, você pode evitar a porta conhecida Olá 1433. Por exemplo, se você configurou toolisten do SQL Server na porta 1500 e estabelecida apropriadas do firewall e regras de grupo de segurança de rede, você pôde se conectar por meio do acréscimo Olá porta número toohello nome do servidor. Olá exemplo a seguir altera a saudação anterior, adicionando um número de porta personalizada, **1500**, toohello o nome do servidor:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Quando você consulta do SQL Server em uma VM em Olá internet, todos os dados de saída de hello Azure datacenter é o assunto toonormal [de preço em transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Conecte-se tooSQL Server em uma rede virtual

Quando você escolhe **privada** para Olá **conectividade SQL** tipo no portal hello, o Azure configura a maioria das configurações de saudação idênticas muito**público**. Olá uma diferença é que não há nenhuma regra tooallow do rede segurança grupo fora do tráfego na porta do SQL Server de saudação (padrão 1433).

> [!IMPORTANT]
> imagens de máquina virtual de saudação para Olá SQL Server Developer e edições Express automaticamente não habilite o protocolo de saudação TCP/IP. Para edições Express e de desenvolvedor, você deve usar SQL Server Configuration Manager muito[habilitar manualmente o protocolo TCP/IP de saudação](#manualtcp) depois de criar hello VM.

Normalmente, a conectividade privada é usada em conjunto com [Rede Virtual](../../../virtual-network/virtual-networks-overview.md), o que permite vários cenários. Você pode se conectar a máquinas virtuais na mesma rede virtual, mesmo se essas VMs existe em grupos de recursos diferentes de saudação. E com um [VPN site a site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), você pode criar uma arquitetura híbrida que conecta as VMs a computadores e redes locais.

Redes virtuais também permitem que você toojoin seu domínio de tooa VMs do Azure. Isso é Olá somente o modo toouse a autenticação do Windows tooSQL Server. Olá outros cenários de conexão requerem autenticação do SQL com nomes de usuário e senhas.

Supondo que você configurou o DNS em sua rede virtual, você pode se conectar a instância do SQL Server tooyour especificando o nome do computador Olá VM do SQL Server na cadeia de caracteres de conexão de saudação. saudação de exemplo a seguir também pressupõe que a autenticação do Windows também foi configurada e usuário Olá foi concedido a instância do SQL Server toohello acesso.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a> Alterar as configurações de conectividade do SQL

Você pode alterar as configurações de conectividade Olá para sua máquina de virtual do SQL Server no hello portal do Azure.

1. No portal do Azure de Olá, selecione **máquinas virtuais**.

2. Selecione sua VM do SQL Server.

3. Em **Configurações**, clique em **Configuração do SQL Server**.

4. Saudação de alteração **o nível de conectividade do SQL** tooyour configuração necessária. Opcionalmente, você pode usar este Olá toochange de área porta do SQL Server ou as configurações de autenticação do SQL hello.

   ![Alterar a conectividade do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Aguarde alguns minutos para Olá toocomplete de atualização.

   ![Notificação de atualização da VM do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> Habilitar TCP/IP para as edições Developer e Express

Ao alterar as configurações de conectividade do SQL Server, o Azure não habilita automaticamente protocolo hello TCP/IP para edições Express e o SQL Server Developer. Olá estas etapas explicam como toomanually habilitar TCP/IP para que você pode se conectar remotamente pelo endereço IP.

Primeiro, conecte-se a máquina do SQL Server toohello com área de trabalho remota.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Em seguida, habilite o protocolo TCP/IP de saudação com **SQL Server Configuration Manager**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Conectar com SSMS

Olá etapas a seguir mostram como toocreate um opcional DNS de rótulo para VMs do Azure e, em seguida, conecte-se com o SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Próximas etapas

instruções de provisionamento toosee junto com essas etapas de conectividade, consulte [provisionar uma máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).

Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-server-iaas-overview.md).
