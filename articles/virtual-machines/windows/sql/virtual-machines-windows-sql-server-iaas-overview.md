---
title: "aaaOverview do SQL Server em máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba mais sobre como toorun completo edições do SQL Server em máquinas virtuais do Azure. Obter imagens de VM do SQL Server tooall links diretos e conteúdo relacionado."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Visão geral do SQL Server nas Máquinas Virtuais do Azure
Este tópico descreve as opções para executar o SQL Server em máquinas virtuais do Azure (VMs), juntamente com [links imagens tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) e uma visão geral de [tarefas comuns de](#manage-your-sql-vm).

> [!NOTE]
> Se você já estiver familiarizado com o SQL Server e deseja apenas toosee como toodeploy uma VM do SQL Server, consulte [provisionar uma máquina de virtual do SQL Server no portal do Azure de saudação](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Visão geral
Se você for um administrador de banco de dados ou um desenvolvedor, máquinas virtuais do Azure fornecem uma maneira toomove seu local do SQL Server cargas de trabalho e aplicativos toohello nuvem. Olá vídeo a seguir fornece uma visão geral técnica do Azure VMs do SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Olá vídeo aborda Olá áreas a seguir:

| Hora | Área |
| --- | --- |
| 00:21 |O que são VMs do Azure? |
| 01:45 |Segurança |
| 02:50 |Conectividade |
| 03:30 |Desempenho e confiabilidade do armazenamento |
| 05:20 |Tamanhos de VM |
| 05:54 |Alta disponibilidade e SLA |
| 07:30 |Suporte de configuração |
| 08:00 |Monitoramento |
| 08:32 |Demonstração: Criar uma VM do SQL Server 2016 |

> [!NOTE]
> Olá vídeo se concentra no SQL Server 2016, mas o Azure fornece imagens da VM para várias versões do SQL Server, incluindo o 2012, 2014 e 2016. 
> 
> 

## <a name="scenarios"></a>Cenários
Há muitas razões que você pode escolher toohost seus dados no Azure. Se seu aplicativo é mover tooAzure, melhora o desempenho tooalso mover Olá dados. Mas há outros benefícios. Você automaticamente tem acesso toomultiple data centers para uma recuperação de desastres e presença global. Olá dados também é altamente seguro e durável.

A execução do SQL Server em VMs do Azure é uma opção para armazenar dados relacionais no Azure. É uma boa escolha para vários cenários. Por exemplo, convém tooconfigure Olá VM do Azure como da mesma forma como computador de SQL Server local tooan possíveis. Ou talvez você queira toorun outros aplicativos e serviços em Olá mesmo servidor de banco de dados. Há dois recursos principais que podem ajudar você a pensar em mais cenários e considerações:

* [SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) fornece uma visão geral dos cenários de melhor Olá para usar o SQL Server em VMs do Azure. 
* [Escolher uma opção do SQL Server de nuvem: Banco de Dados do SQL Azure (PaaS) ou SQL Server em VMs do Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)fornece uma comparação detalhada entre o Banco de Dados SQL e o SQL Server em execução em uma VM.

## <a name="create-a-new-sql-vm"></a>Criar uma nova VM de SQL
Olá seções a seguir fornecem links diretos toohello portal do Azure para imagens de galeria de máquina virtual saudação do SQL Server. Dependendo de você selecionar a imagem hello, você pode o pagamento para os custos de licenciamento do SQL Server em uma base por minuto, ou você pode colocar sua própria licença (BYOL).

Localizar instruções passo a passo para criar uma nova VM do SQL no tutorial hello, [provisionar uma máquina de virtual do SQL Server no portal do Azure de saudação](virtual-machines-windows-portal-sql-server-provision.md). Além disso, examine Olá [práticas recomendadas para VMs do SQL Server](virtual-machines-windows-sql-performance.md), que explica como computador apropriados com hello tooselect tamanho e outros recursos disponível durante o provisionamento.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Opção 1: Criar uma VM do SQL com licenciamento por minuto
Olá tabela a seguir fornece uma matriz de imagens na Galeria de máquinas virtuais de saudação do hello mais recentes do SQL Server. Clique em qualquer toobegin link criando uma nova VM do SQL com a versão especificada, a edição e o sistema operacional. 

> [!TIP]
> Olá toounderstand VM e preços do SQL para essas imagens, consulte [preços orientação para VMs do Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Versão | Sistema operacional | Edição |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Além disso toothis lista, outras combinações de sistemas operacionais e versões do SQL Server estão disponíveis. Localize outras imagens por meio de uma pesquisa de mercado em Olá portal do Azure. 

## <a id="BYOL"></a>Opção 2: Criar uma VM do SQL com uma licença existente
Também é possível usar sua própria licença (BYOL). Nesse cenário, você só paga pelo Olá VM sem encargos adicionais para licenciamento do SQL Server. toouse sua própria licença, use Olá matriz de versões do SQL Server, edições e sistemas operacionais abaixo. No portal de hello, esses nomes de imagem são prefixados com **{BYOL}**.

> [!TIP]
> Colocar sua própria licença pode economizar dinheiro ao longo do tempo para cargas de trabalho de produção contínua. Para obter mais informações, consulte [Diretrizes para os preço das VMs do Azure do SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Versão | Sistema operacional | Edição |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard  BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Além disso toothis lista, outras combinações de sistemas operacionais e versões do SQL Server estão disponíveis. Localize outras imagens por meio de uma pesquisa de mercado em Olá portal do Azure (procure "{BYOL} SQL Server").

> [!IMPORTANT]
> as imagens de VM BYOL toouse, você deve ter um contrato corporativo com [License Mobility por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/). Você também precisa de uma licença válida Olá/edição da versão do SQL Server que você deseja toouse. Você deve [fornecer Olá necessário BYOL informações tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) em **10** dias após o provisionamento de VM. 

> [!NOTE]
> Não é possível toochange Olá licenciamento sua própria licença do modelo de um toouse de VM do SQL Server de pagamento por minuto. Nesse caso, você deve criar uma nova VM BYOL e migrar seu bancos de dados toohello nova VM. 

## <a name="manage-your-sql-vm"></a>Gerenciar sua VM do SQL
Após o provisionamento da VM do SQL Server, várias tarefas de gerenciamento opcionais estarão disponíveis. Em muitos aspectos, você configura e gerencia o SQL Server exatamente como configuraria uma instância local do SQL Server. No entanto, algumas tarefas são tooAzure específico. Olá seções a seguir destacam algumas dessas áreas com as informações de toomore links.

### <a name="connect-toohello-vm"></a>Conecte-se toohello VM
Uma das etapas de gerenciamento mais básicas de saudação é tooconnect tooyour VM do SQL Server por meio de ferramentas, como o SQL Server Management Studio (SSMS). Para obter instruções sobre como tooconnect tooyour nova VM do SQL Server, consulte [conectar tooa Máquina Virtual do SQL Server no Azure](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Migrar seus dados
Se você tiver um banco de dados existente, você desejará toomove que toohello recentemente provisionados VM do SQL. Para obter uma lista de opções de migração e orientações, consulte [migrando um banco de dados tooSQL Server em uma VM do Azure](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Configurar alta disponibilidade
Se você precisar de alta disponibilidade, considere configurar grupos de disponibilidade do SQL Server. Isso envolve várias VMs do Azure em uma rede virtual. Olá portal do Azure tem um modelo que define esta configuração para você. Para obter mais informações, consulte [Configurar um grupo de disponibilidade AlwaysOn nas máquinas virtuais do Azure Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Se você quiser toomanually configurar seu grupo de disponibilidade e de escuta associada, consulte [configurar grupos de disponibilidade AlwaysOn em VM do Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Para outras considerações sobre alta disponibilidade, consulte [alta disponibilidade e recuperação de desastres para SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Fazer backup dos dados
Máquinas virtuais do Azure podem tirar proveito do [Backup automatizado](virtual-machines-windows-sql-automated-backup.md), que cria regularmente o backup de seu armazenamento de tooblob do banco de dados. Essa técnica também pode ser usada manualmente. Para obter mais informações, consulte [Usar o Armazenamento do Azure para o Backup e a Restauração do SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Para obter uma visão geral das opções de backup e restauração, consulte [Backup e Restauração do SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Automatizar as atualizações
Máquinas virtuais do Azure podem usar [aplicação de patch automatizada](virtual-machines-windows-sql-automated-patching.md) tooschedule atualiza automaticamente a uma janela de manutenção para a instalação do windows importantes e o SQL Server.

### <a name="customer-experience-improvement-program-ceip"></a>Programa de aperfeiçoamento da experiência do usuário (CEIP)
saudação do programa de Aperfeiçoamento da experiência (CEIP) está habilitada por padrão. Nesse periodicamente envia relatórios tooMicrosoft toohelp aprimorar o SQL Server. Não há nenhuma tarefa de gerenciamento necessária com o CEIP, a menos que você deseja toodisable-lo após a configuração. Você pode personalizar ou desabilitar Olá CEIP conectando toohello VM com área de trabalho remota. Em seguida, execute Olá **erro do SQL Server e o relatório de uso** utilitário. Siga Olá instruções toodisable reporting. 

Para obter mais informações, consulte Olá seção CEIP Olá [aceitar termos de licença](https://msdn.microsoft.com/library/ms143343.aspx) tópico. 

## <a name="next-steps"></a>Próximas etapas

Para perguntas sobre preços, consulte [preços orientação para VMs do Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md) e hello [do Azure de página de preços](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Selecione a edição de destino do SQL Server no hello **SO/Software** lista. Exiba os preços de saudação para máquinas virtuais de tamanho diferente.

Mais perguntas? Primeiro, consulte Olá [SQL Server nas perguntas frequentes sobre máquinas virtuais do Azure](virtual-machines-windows-sql-server-iaas-faq.md). Mas também adicionar a parte inferior toohello perguntas ou comentários de qualquer toointeract de tópicos de VM do SQL com a comunidade Microsoft e hello.
