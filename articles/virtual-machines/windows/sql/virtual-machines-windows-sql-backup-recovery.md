---
title: "aaaBackup e restauração do SQL Server | Microsoft Docs"
description: "Descreve as considerações de backup e restauração para bancos de dados do SQL Server em execução em Máquinas Virtuais do Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Backup e restauração para o SQL Server em Máquinas Virtuais do Azure
## <a name="overview"></a>Visão geral
Armazenamento do Azure mantém 3 cópias de cada tooguarantee proteção de disco de VM do Azure contra perda de dados ou corrupção de dados físicos. Assim, diferentemente no local, não é preciso tooworry sobre eles. No entanto, você ainda deve fazer backup de seu tooprotect de bancos de dados do SQL Server contra erros de aplicativo ou usuário (por exemplo, a inserção de dados errado ou excluir uma tabela) e ser capaz de toorestore tooa ponto no tempo.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Para o SQL Server em execução em VMs do Azure, você pode usar o backup nativo e restaurar técnicas usando discos anexados para destino Olá Olá dos arquivos de backup. No entanto, há um número de toohello limite de discos que você pode anexar tooan máquina virtual do Azure, com base em Olá [tamanho da máquina virtual de saudação](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Também há sobrecarga de saudação do tooconsider de gerenciamento de disco.

Começando com o SQL Server 2014, você pode fazer backup e restaurar tooMicrosoft armazenamento de BLOBs do Azure. O SQL Server 2016 também fornece aprimoramentos para essa opção. Além disso, para os arquivos de banco de dados armazenados no armazenamento de Blobs do Microsoft Azure, o SQL Server 2016 fornece uma opção de backups quase imediatos e restaurações rápidas usando instantâneos do Azure. Este artigo fornece uma visão geral dessas opções. Encontre mais informações em [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Para obter uma discussão das opções de saudação para fazer backup de bancos de dados muito grandes, consulte [estratégias de Backup do banco de dados do servidor em SQL vários terabytes para máquinas virtuais do Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Olá seções a seguir incluem informações específicas toohello diferentes versões do SQL Server com suporte em uma máquina virtual do Azure.

## <a name="sql-server-virtual-machines"></a>Máquinas virtuais do SQL Server
Quando a instância do SQL Server está em execução em uma máquina virtual do Azure, os arquivos de banco de dados já residem em discos de dados no Azure. Esses discos residem no armazenamento de blobs do Azure. Portanto Olá razões para fazer backup de seu banco de dados e hello abordagens que alteração você demorar um pouco. Considere o seguinte hello. 

* Você não precisar mais proteção de tooprovide de backups de banco de dados de tooperform contra falha de hardware ou mídia porque o Microsoft Azure fornece essa proteção como parte da saudação serviço Microsoft Azure.
* Você ainda precisa tooperform banco de dados backups tooprovide proteção contra erros de usuário ou para fins de arquivamento, razões regulamentares ou fins administrativos.
* Você pode armazenar o arquivo de backup Olá diretamente no Azure. Para obter mais informações, consulte Olá seguintes seções que fornecem orientação para Olá diferentes versões do SQL Server.

## <a name="sql-server-2016"></a>SQL Server 2016
O Microsoft SQL Server 2016 dá suporte às funcionalidades de [backup e restauração com blobs do Azure](https://msdn.microsoft.com/library/jj919148.aspx) encontradas no SQL Server 2014. Mas ele também inclui Olá aprimoramentos a seguir:

| Aprimoramento do 2016 | Detalhes |
| --- | --- |
| **Distribuição** |Ao fazer backup tooMicrosoft armazenamento de BLOBs do Azure, SQL Server 2016 dá suporte a backup toomultiple blobs tooenable fazendo backup de bancos de dados grandes, o máximo de tooa de 12,8 TB. |
| **Backup de instantâneo** |Por meio do uso de saudação de instantâneos do Azure, o Backup de instantâneo de arquivo do SQL Server fornece backups quase imediatos e restaurações rápidas para os arquivos de banco de dados armazenados usando o serviço de armazenamento de BLOBs do Azure hello. Esse recurso permite que você toosimplify suas políticas de backup e restauração. O backup de instantâneo de arquivo também dá suporte à recuperação pontual. Para obter mais informações, veja [Backups de instantâneo para arquivos de banco de dados no Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Agendamento de backup gerenciado** |TooAzure de Backup gerenciado do SQL Server agora dá suporte a agendas personalizadas. Para obter mais informações, consulte [tooMicrosoft de Backup gerenciado do SQL Server do Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Para obter um tutorial de recursos de saudação do SQL Server 2016 ao usar o armazenamento de BLOBs do Azure, consulte [Tutorial: usando o serviço de armazenamento de BLOBs do Microsoft Azure Olá com bancos de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 inclui Olá aprimoramentos a seguir:

1. **Backup e restauração tooAzure**:
   
   * *Backup do SQL Server tooURL* agora tem suporte no SQL Server Management Studio. Olá opção tooback backup tooAzure agora está disponível ao usar a tarefa de Backup ou restauração ou Assistente de plano de manutenção no SQL Server Management Studio. Para obter mais informações, consulte [tooURL de Backup do SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *Backup gerenciado do SQL tooAzure* tem uma nova funcionalidade que permite o gerenciamento de backup automatizado. Isso é especialmente útil para automatizar o gerenciamento de backups para instâncias do SQL Server 2014 em execução em um computador do Azure. Para obter mais informações, consulte [tooMicrosoft de Backup gerenciado do SQL Server do Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Backup automatizado* fornece automação adicionais tooautomatically habilitar *tooAzure de Backup gerenciado do SQL Server* em todos os existentes e novos bancos de dados para uma VM do SQL Server no Azure. Para obter mais informações, veja [Backup Automatizado para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-automated-backup.md).
   * Para obter uma visão geral de todas as opções de saudação para tooAzure de Backup do SQL Server 2014, consulte [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Criptografia**: o SQL Server 2014 dá suporte à criptografia de dados durante a criação de um backup. Ele oferece suporte a vários algoritmos de criptografia e Olá use osf um certificado ou chave assimétrica. Para obter mais informações, veja [Criptografia de backup](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Para obter informações detalhadas sobre o Backup e restauração do SQL Server no SQL Server 2012, veja [Backup e restauração de Bancos de Dados do SQL Server (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

A partir do SQL Server 2012 SP1 atualização cumulativa 2, você pode fazer backup tooand restauração da saudação serviço de armazenamento de Blob do Azure. Esse aprimoramento pode ser usado tooback dos bancos de dados do SQL Server em um SQL Server em execução em uma máquina Virtual do Azure ou em uma instância local. Para obter mais informações, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blob do Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Alguns dos benefícios de saudação do usando o serviço de armazenamento de BLOBs do Azure Olá incluem hello capacidade toobypass Olá 16 limite de disco para discos anexados, facilidade de gerenciamento, disponibilidade direta de saudação da instância de tooanother Olá arquivo de backup da instância do SQL Server em execução em um Azure máquina virtual, ou uma instância local para fins de recuperação de desastres ou de migração. Para obter uma lista completa dos benefícios toousing um serviço de armazenamento de BLOBs do Azure para backups do SQL Server, consulte Olá *benefícios* seção [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Para ver as práticas recomendadas e informações de solução de problemas, veja [Práticas recomendadas de Backup e restauração (Serviço de Armazenamento de Blob do Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Para Backup e restauração do SQL Server no SQL Server 2008 R2, veja [Fazer backup e restauração de bancos de dados no SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Para Backup e restauração do SQL Server no SQL Server 2008, veja [Fazer backup e restauração de bancos de dados no SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Próximas etapas
Se você estiver planejando sua implantação do SQL Server em uma VM do Azure, você encontrará orientações provisionamento Olá tutorial a seguir: [provisionar uma máquina Virtual do SQL Server no Azure com o Azure Resource Manager](virtual-machines-windows-portal-sql-server-provision.md).

Embora o backup e restauração pode ser usado toomigrate seus dados, há tooSQL de caminhos de migração de dados potencialmente mais fácil Server em uma VM do Azure. Para obter uma discussão completa sobre opções de migração e recomendações, consulte [migrando um banco de dados tooSQL Server em uma VM do Azure](virtual-machines-windows-migrate-sql.md).

Examine outros [recursos para executar o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

