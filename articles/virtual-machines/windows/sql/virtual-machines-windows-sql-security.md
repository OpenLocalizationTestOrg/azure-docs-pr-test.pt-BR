---
title: "aaaSecurity considerações para o SQL Server no Azure | Microsoft Docs"
description: "Este tópico fornece diretrizes gerais para proteger o SQL Server em execução em uma Máquina Virtual do Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Considerações sobre Segurança para SQL Server em Máquinas Virtuais do Azure

Este tópico inclui as diretrizes gerais de segurança que ajudam a estabelecer acesso seguro tooSQL Server instâncias em uma máquina virtual do Azure (VM).

Azure está em conformidade com vários regulamentos do setor e padrões que podem permitir que você toobuild uma solução compatível com o SQL Server em execução em uma máquina virtual. Para obter informações sobre conformidade regulamentar com o Azure, consulte a [Central de Confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Controlar acesso toohello VM do SQL

Quando você cria sua máquina de virtual do SQL Server, considere como toocarefully controlar quem tem toohello acessar o computador e tooSQL Server. Em geral, você deve fazer a seguir hello:

- Restringir acesso tooSQL Server tooonly Olá aplicativos e clientes que precisam dela.
- Siga as melhores práticas de gerenciamento de contas de usuário e senhas.

Olá seções a seguir fornece sugestões sobre pensando desses pontos.

## <a name="secure-connections"></a>Conexões seguras

Quando você cria uma máquina virtual SQL Server com uma imagem da galeria, Olá **conectividade do SQL Server** opção fornece Olá escolha de **Local (dentro da VM)**, **privada (dentro de uma rede Virtual)** , ou **pública (Internet)**.

![Conectividade do SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Para melhor segurança de hello, escolha a opção mais restritiva Olá para seu cenário. Por exemplo, se você estiver executando um aplicativo que acessa o SQL Server em Olá mesma VM, em seguida, **Local** é a opção mais segura de saudação. Se você estiver executando um aplicativo do Azure que requer acesso toohello SQL Server, em seguida, **privada** protege a comunicação tooSQL servidor apenas dentro de saudação especificada [rede Virtual do Azure](../../../virtual-network/virtual-networks-overview.md). Se você precisar **pública** toohello de acesso (internest) VM do SQL Server, em seguida, certifique-se de que toofollow outras práticas recomendadas em tooreduce este tópico a área de superfície de ataque.

Olá opções selecionadas no portal de saudação usam regras de segurança de entrada em Olá VMs [grupo de segurança de rede](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) ou negar máquina de virtual de tooyour de tráfego de rede. Você pode modificar ou criar novas regras NSG entradas porta do tooallow tráfego toohello do SQL Server (padrão 1433). Você também pode especificar endereços IP específicos que são permitidos toocommunicate por essa porta.

![Regras de grupo de segurança de rede](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Além disso, tooNSG regras toorestrict o tráfego de rede, você também pode usar o hello Firewall do Windows na máquina virtual de saudação.

Se você estiver usando pontos de extremidade com o modelo de implantação clássico hello, remova quaisquer pontos de extremidade na máquina virtual de saudação se você não usá-los. Para obter instruções sobre como usar ACLs com pontos de extremidade, consulte [gerenciar Olá ACL em um ponto de extremidade](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Isso não é necessário para VMs que usam Olá Gerenciador de recursos.

Finalmente, considere a possibilidade de habilitar conexões criptografadas para instância Olá Olá mecanismo de banco de dados do SQL Server na máquina virtual do Azure. Configure a instância do SQL Server com um certificado assinado. Para obter mais informações, consulte [toohello habilitar conexões criptografadas mecanismo de banco de dados](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) e [sintaxe de cadeia de caracteres de Conexão](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Usar uma porta não padrão

Por padrão, o SQL Server escuta uma porta conhecida, 1433. Para maior segurança, configure toolisten do SQL Server em uma porta não padrão, como 1401. Se você provisionar uma imagem da Galeria do SQL Server no hello portal do Azure, você pode especificar essa porta no hello **configurações do SQL Server** folha.

tooconfigure este após a configuração, você tem duas opções:

- Para máquinas virtuais do Gerenciador de recursos, você pode selecionar **configuração do SQL Server** da folha de visão geral VM hello. Isso fornece uma opção de porta de saudação toochange.

  ![Alteração da porta TCP no portal](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Para VMs clássico ou para VMs do SQL Server que não foram provisionados com o portal de saudação, você pode configurar manualmente o porta Olá conectando-se remotamente toohello VM. Para etapas de configuração hello, consulte [configurar tooListen um servidor em uma porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Se você usar essa técnica manual, você também precisa tooadd um tráfego de entrada de tooallow de regra de Firewall do Windows em que a porta TCP.

> [!IMPORTANT]
> Especificando uma porta não padrão é uma boa ideia se a porta do SQL Server é toopublic abrir conexões de internet.

Quando o SQL Server está escutando em uma porta não padrão, você deve especificar porta hello quando você se conectar. Por exemplo, considere um cenário em que o endereço IP do servidor de saudação é 13.55.255.255 e do SQL Server está escutando na porta 1401. tooconnect tooSQL Server, você especificaria `13.55.255.255,1401` na cadeia de caracteres de conexão de saudação.

## <a name="manage-accounts"></a>Gerenciar Contas

Você não deseja que os invasores tooeasily estimativa conta nomes ou senhas. Use Olá toohelp dicas a seguir:

- Crie uma conta de administrador local exclusiva que não esteja nomeada como **Administrador**.

- Use senhas fortes e complexas para todas as suas contas. Para obter mais informações sobre como toocreate uma senha forte, consulte [criar uma senha forte](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) artigo.

- Por padrão, o Azure seleciona a autenticação do Windows durante a instalação da máquina Virtual do SQL Server. Portanto, Olá **SA** logon está desabilitado e uma senha é atribuída pela instalação. É recomendável que Olá **SA** logon não deve ser usado ou habilitado. Se você deve ter um logon do SQL, use uma das Olá estratégias a seguir:

  - Crie uma conta do SQL com um nome exclusivo que tem a associação **sysadmin**. Você pode fazer isso no portal de saudação habilitando **autenticação SQL** durante o provisionamento.

    > [!TIP] 
    > Se você não habilitar a autenticação do SQL durante o provisionamento, você deve alterar manualmente o modo de autenticação Olá muito**do SQL Server e o modo de autenticação do Windows**. Para obter mais informações, consulte [Alterar Modo de Autenticação do Servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Se você precisar usar Olá **SA** logon, habilitar Olá logon depois de provisionamento e atribuir uma nova senha forte.

## <a name="follow-on-premises-best-practices"></a>Seguir as melhores práticas localmente

Além disso toohello práticas descritos neste tópico, é recomendável que você verifique e implemente práticas de segurança tradicionais locais Olá onde aplicável. Para obter mais informações, consulte [Considerações sobre segurança para uma instalação do SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Próximas etapas

Se você também estiver interessado em práticas recomendadas sobre desempenho, veja [Práticas recomendadas relacionadas ao desempenho para o SQL Server em máquinas virtuais do Azure](virtual-machines-windows-sql-performance.md).

Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais do Azure overview](virtual-machines-windows-sql-server-iaas-overview.md).

