---
title: "aaaSQL servidor nas perguntas frequentes sobre máquinas virtuais do Azure | Microsoft Docs"
description: "Este artigo fornece respostas toofrequently perguntas frequentes sobre a execução do SQL Server em máquinas virtuais do Azure."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Perguntas frequentes sobre o SQL Server nas Máquinas Virtuais do Azure
Este tópico fornece respostas toosome de saudação perguntas mais comuns sobre a execução [do SQL Server em máquinas virtuais Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Perguntas frequentes

1. **Como criar uma máquina virtual do Azure com o SQL Server?**

    a solução mais fácil Olá é toocreate uma máquina Virtual que inclui o SQL Server. Para obter um tutorial sobre como inscrever-se no Azure e criar uma VM do SQL do portal de saudação, consulte [provisionar uma máquina de virtual do SQL Server no hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md). Você pode selecionar uma imagem de máquina virtual que usa o licenciamento do pagamento por minuto SQL Server, ou você pode usar uma imagem que permite que você toobring sua própria licença do SQL Server. Você também tem a opção de saudação de instalação do SQL Server em uma máquina virtual manualmente e reutilizar uma licença de local. Se você trouxer sua própria licença, será necessário ter o [License Mobility por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/). Para obter mais informações, consulte [Diretrizes de preço para VMs do Azure do SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Qual é a diferença de saudação entre VMs do SQL e hello serviço de banco de dados SQL?**

    Conceitualmente, a execução do SQL Server em uma máquina virtual do Azure não é diferente da execução do SQL Server em um datacenter remoto. Por outro lado, o [Banco de Dados SQL](../../../sql-database/sql-database-technical-overview.md) oferece o banco de dados como serviço. Com o banco de dados SQL, você não tem máquinas de toohello de acesso que hospedam seus bancos de dados. Para obter uma comparação completa, confira [Escolher uma opção do SQL Server de nuvem: Banco de Dados SQL do Azure (PaaS) ou SQL Server em VMs do Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Como posso migrar meu toohello de banco de dados do SQL Server local nuvem?**

    Primeiro, crie uma máquina virtual do Azure com uma instância do SQL Server. Em seguida, migre sua instância de toothat de bancos de dados local. Para estratégias de migração de dados, consulte [migrar um banco de dados de SQL Server tooSQL Server em uma VM do Azure](virtual-machines-windows-migrate-sql.md).

1. **Posso instalar uma segunda instância do SQL Server em Olá mesma VM? Alterar os recursos instalados de instância padrão de saudação?**

    Sim. Olá mídia de instalação do SQL Server está localizado em uma pasta no hello **C** unidade. Executar **Setup.exe** entre instâncias do SQL Server local tooadd novo ou recursos toochange outros instalado do SQL Server na máquina de saudação. Observe que alguns recursos, como Backup automatizado, aplicação de patch automatizada e integração do cofre da chave do Azure, só funcionam em relação a instância padrão de saudação.

1. **Instância padrão de saudação do SQL Server pode desinstalar?**

    Sim. Mas há algumas considerações. Conforme indicado na resposta anterior hello, recursos que dependem de saudação [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md) operar somente na instância padrão de saudação. Se você desinstalar a instância padrão de saudação, extensão Olá continua toolook para ele e pode gerar erros de log de eventos. Esses erros são de saudação duas origens a seguir: **gerenciamento de credenciais do Microsoft SQL Server** e **Microsoft SQL Server IaaS Agent**. Um dos erros de saudação pode ser a seguir toohello semelhante:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Se você decidir instância padrão do toouninstall Olá, desinstalá-Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md) também.

1. **Como atualizar o tooa nova versão/edição de saudação do SQL Server em uma VM do Azure?**

    Atualmente, não existe uma atualização in-loco para o SQL Server em execução em uma VM do Azure. Criar uma nova máquina virtual do Azure com edição Olá desejado da versão do SQL Server e, em seguida, migrar seu servidor de novo toohello em bancos de dados usando o padrão [técnicas de migração de dados](virtual-machines-windows-migrate-sql.md).

1. **Como instalar minha cópia licenciada do SQL Server em uma VM do Azure?**

    Há dois toodo de maneiras isso. Você pode provisionar uma saudação [imagens da máquina virtual que oferece suporte a licenças](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Outra opção é tooa do mídia de instalação do SQL Server toocopy Olá VM do Windows Server e, em seguida, instalar o SQL Server na VM de saudação. Por motivos de licenciamento, você deve ter o [License Mobility por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/). Para obter mais informações, consulte [Diretrizes de preço para VMs do Azure do SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Alterar uma VM toouse minha própria licença do SQL Server se ele foi criado de uma saudação pré-pago imagens da Galeria?**

    Não. Você não pode alternar de toousing de licenciamento de pagamento por minuto sua própria licença. Criar uma nova máquina virtual do Azure usando uma saudação [imagens BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), e, em seguida, migrar seu servidor de novo toohello em bancos de dados usando o padrão [técnicas de migração de dados](virtual-machines-windows-migrate-sql.md).

1. **Há suporte para FCIs (Instâncias de Cluster de Failover) do SQL Server nas VMs do Azure?**

   Sim. Você pode [criar um Cluster de Failover do Windows no Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) e usar espaços de armazenamento diretos (S2D) Olá para armazenamento de cluster. Como alternativa, você pode usar soluções de clustering ou armazenamento de terceiros, conforme descrito em [Alta disponibilidade e recuperação de desastre para SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **É necessário o toopay toolicense do SQL Server em uma VM do Azure se ele está sendo usado apenas para modo de espera para o failover?**

    Você não tem toopay toolicense um SQL Server participa como uma réplica secundária passiva em uma implantação de alta disponibilidade, se você tiver Software Assurance e usa mobilidade de licença, conforme descrito em [perguntas frequentes sobre licenciamento de máquina Virtual](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Como as atualizações e os service packs são aplicados a uma VM do SQL Server?**

    Máquinas virtuais dão a você controle sobre o computador de host hello, incluindo quando e como aplicar as atualizações. Para o sistema operacional de saudação, você poderá aplicar manualmente as atualizações do windows, ou você pode habilitar um serviço de agendamento chamado [aplicação de patch automatizada](virtual-machines-windows-sql-automated-patching.md). A Aplicação de Patch Automatizada instala todas as atualizações marcadas como importantes, inclusive atualizações do SQL Server nessa categoria. Outros tooSQL atualizações opcionais que servidor deve ser instalado manualmente.

1. **É possível tooset as configurações não são mostrados na Galeria de máquinas virtuais de saudação (por exemplo, Windows 2008 R2 + SQL Server 2012)?**

    Não. Para imagens de galeria de máquinas virtuais que incluem o SQL Server, você deve selecionar uma saudação fornecida imagens.

1. **Como instalar as ferramentas de Dados do SQL em minha VM do Azure?**

     Baixar e instalar as ferramentas de dados do SQL de saudação do [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Recursos

Para obter uma visão geral do SQL Server em máquinas virtuais do Azure, assista o vídeo de saudação [VM do Azure é a melhor plataforma Olá para o SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). Você também pode obter uma boa introdução tópico hello, [do SQL Server em máquinas virtuais do Azure overview](virtual-machines-windows-sql-server-iaas-overview.md).

Outros recursos incluem:

* [Provisionar uma máquina de virtual do SQL Server no hello Portal do Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrando um banco de dados tooSQL Server em uma VM do Azure](virtual-machines-windows-migrate-sql.md)
* [Alta disponibilidade e recuperação de desastres para SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Práticas recomendadas para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-performance.md)
* [Estratégias de Desenvolvimento e Padrões de Aplicativo para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 