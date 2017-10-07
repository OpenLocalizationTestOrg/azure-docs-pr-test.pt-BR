---
title: "aaaMigrate um tooSQL de banco de dados de servidor SQL Server em uma máquina virtual | Microsoft Docs"
description: "Saiba mais sobre como toomigrate um usuário local do banco de dados tooSQL Server em uma máquina virtual do Azure."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Migrar um banco de dados de SQL Server tooSQL Server em uma VM do Azure

Há um número de métodos toomigrate um tooSQL de banco de dados de usuário local do SQL Server Server em uma VM do Azure. Este artigo brevemente discutem vários métodos e recomenda o melhor método para vários cenários de saudação.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Quais são os métodos de migração primário Olá?
Olá migração principais métodos são:

* Executar backup local usando a compactação e manualmente copiar arquivo de backup de saudação em Olá máquina virtual do Azure
* Executar um tooURL backup e restaurar para Olá máquina virtual do Azure da URL de saudação
* Desanexar e copie Olá dados e log arquivos tooAzure armazenamento de blob e, em seguida, anexar tooSQL Server na VM do Azure de URL
* Converter em locais físicos tooHyper V VHD da máquina, carregue o armazenamento de Blob tooAzure e, em seguida, implantar como nova VM usando carregar o VHD
* Remeter o disco rígido usando o Serviço de Importação/Exportação do Windows
* Se você tiver uma implantação de AlwaysOn no local, use Olá [assistente Adicionar réplica do Azure](../classic/sql-onprem-availability.md) toocreate uma réplica no Azure e, em seguida, o failover, apontando a instância de banco de dados do Azure toohello usuários
* Use o SQL Server [replicação transacional](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server como um assinante da instância e, em seguida, desabilite a replicação, apontando a instância de banco de dados do Azure toohello usuários

> [!TIP]
> Você também pode usar esses mesmos técnicas toomove bancos de dados entre VMs do SQL Server no Azure. Por exemplo, não há nenhum tooupgrade de maneira com suporte uma VM da imagem da Galeria do SQL Server de um tooanother de versão/edição. Nesse caso, você deve criar uma nova VM do SQL Server com a nova versão/edição hello e usar um das técnicas de migração de saudação em toomove este artigo seus bancos de dados. 

## <a name="choosing-your-migration-method"></a>Escolhendo o método de migração
Para desempenho de transferência de dados ideal, migre arquivos de banco de dados de saudação em Olá VM do Azure usando um arquivo de backup compactado.

toominimize de tempo de inatividade durante o processo de migração do banco de dados hello, use opção Olá AlwaysOn ou opção de replicação transacional hello.

Se não for possível toouse Olá acima métodos, migre seu banco de dados manualmente. Usando esse método, você normalmente inicia com um backup de banco de dados seguido por uma cópia de backup de banco de dados de saudação no Azure e, em seguida, executar uma restauração de banco de dados. Você pode também copiar os próprios arquivos de banco de dados Olá no Azure e, em seguida, anexá-los. Existem vários métodos pelos quais você pode realizar esse processo manual de migrar um banco de dados para uma VM do Azure.

> [!NOTE]
> Quando você atualiza tooSQL Server 2014 ou SQL Server 2016 de versões anteriores do SQL Server, você deve considerar se as alterações são necessárias. É recomendável que você aborde todas as dependências nos recursos sem suporte pela nova versão de saudação do SQL Server como parte de seu projeto de migração. Para obter mais informações sobre edições Olá com suporte e cenários, consulte [atualização tooSQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

Olá a tabela a seguir lista cada um dos métodos de migração primário hello e descreve quando usar saudação de cada método é mais apropriado.

| Método | Versão do banco de dados de origem | Versão do banco de dados de destino | Restrição de tamanho do backup do banco de dados de origem | Observações |
| --- | --- | --- | --- | --- |
| [Executar backup local usando a compactação e manualmente copiar arquivo de backup de saudação em Olá máquina virtual do Azure](#backup-and-restore) |SQL Server 2005 ou posterior |SQL Server 2005 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Essa é uma técnica muito simples e bem testada para mover bancos de dados entre máquinas. |
| [Executar um tooURL backup e restaurar para Olá máquina virtual do Azure da URL de saudação](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 ou posterior |SQL Server 2012 SP1 CU2 ou posterior |< 12,8 TB para SQL Server 2016, caso contrário, < 1 TB | Esse método é apenas outra maneira toomove Olá arquivo de backup toohello VM usando o armazenamento do Azure. |
| [Desanexar e copie Olá dados e log arquivos tooAzure armazenamento de blob e, em seguida, anexar tooSQL Server na máquina virtual do Azure de URL](#detach-and-attach-from-url) |SQL Server 2005 ou posterior |SQL Server 2014 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Use este método quando desejar muito[armazene esses arquivos usando o serviço de armazenamento de BLOBs do Azure Olá](https://msdn.microsoft.com/library/dn385720.aspx) e anexá-los tooSQL Server em execução em uma VM do Azure, particularmente com bancos de dados muito grandes |
| [Converter local tooHyper V VHDs de máquina, carregue o armazenamento de Blob tooAzure e, em seguida, implantar uma nova máquina virtual usando o VHD carregado](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 ou posterior |SQL Server 2005 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Use quando [colocar sua própria licença do SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), ao migrar um banco de dados que você executará em uma versão anterior do SQL Server, ou quando a migração de sistema e de bancos de dados de usuário como parte de Olá migração do banco de dados depende dos outros bancos de dados de usuário e/ou bancos de dados do sistema. |
| [Remeter o disco rígido usando o Serviço de Importação/Exportação do Windows](#ship-hard-drive) |SQL Server 2005 ou posterior |SQL Server 2005 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Saudação de uso [serviço de importação/exportação do Windows](../../../storage/common/storage-import-export-service.md) quando o método de cópia manual está muito lento, como bancos de dados muito grandes |
| [Use Olá assistente Adicionar réplica do Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 ou posterior |SQL Server 2012 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Minimiza o tempo de inatividade, use quando tiver uma implantação local do AlwaysOn |
| [Usar a replicação transacional do SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 ou posterior |SQL Server 2005 ou posterior |[Limite de armazenamento da VM do Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Use quando você precisa de tempo de inatividade toominimize e não tiver uma implantação de local do AlwaysOn |

## <a name="backup-and-restore"></a>Backup e restauração
Fazer backup de banco de dados com a compactação, copie Olá backup toohello VM e, em seguida, restaure o banco de dados de saudação. Se o arquivo de backup for maior que 1 TB, você deve distribui-lo porque o tamanho máximo de saudação de um disco VM é 1 TB. Use Olá um banco de dados de usuário usando esse método manual toomigrate etapas gerais a seguir:

1. Execute um instalação local do banco de dados completo tooan backup.
2. Crie ou carregue uma máquina virtual com a versão de saudação do SQL Server desejado.
3. Configure a conectividade com base em seus requisitos de instalação. Consulte [conectar tooa Máquina Virtual do SQL Server no Azure (Gerenciador de recursos)](virtual-machines-windows-sql-connect.md).
4. Copie seu arquivos de backup de tooyour VM usando o comando remoto de cópia de área de trabalho, o Windows Explorer ou Olá em um prompt de comando.

## <a name="backup-toourl-and-restore"></a>TooURL backup e restauração
Em vez de fazer backup de arquivo local tooa, você pode usar o hello [tooURL backup](https://msdn.microsoft.com/library/dn435916.aspx) e, em seguida, restaure a partir de URL toohello VM. Com o SQL Server 2016, conjuntos de backup distribuídos têm suporte, são recomendados para desempenho e necessário limites de tamanho de saudação tooexceed por blob. Para bancos de dados muito grandes, Olá uso de saudação [serviço de importação/exportação do Windows](../../../storage/common/storage-import-export-service.md) é recomendado.

## <a name="detach-and-attach-from-url"></a>Desanexar e anexar da URL
Desanexar os banco de dados e arquivos de log e transferi-los muito[armazenamento de BLOBs do Azure](https://msdn.microsoft.com/library/dn385720.aspx). Em seguida, anexe o banco de dados de saudação da URL de saudação em sua VM do Azure. Use-o se desejar Olá tooreside de arquivos de banco de dados físico no armazenamento de Blob. Isso pode ser útil para bancos de dados muito grandes. Use Olá um banco de dados de usuário usando esse método manual toomigrate etapas gerais a seguir:

1. Desanexe os arquivos de banco de dados de saudação da instância de banco de dados do local de saudação.
2. Copiar arquivos de banco de dados desanexado de saudação no armazenamento de BLOBs do Azure usando Olá [utilitário de linha de comando AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Anexe arquivos de banco de dados de saudação da instância do SQL Server toohello hello Azure URL no hello VM do Azure.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Converter tooVM e carregue tooURL e implantar como uma nova VM
Use este método toomigrate todos os bancos de dados de sistema e usuário em uma máquina virtual do local do SQL Server instância tooAzure. Use Olá uma instância inteira do SQL Server usando esse método manual toomigrate etapas gerais a seguir:

1. Converter físico ou virtual máquinas VHDs tooHyper-V usando [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Carregar arquivos VHD tooAzure armazenamento usando Olá [cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Implantar uma nova máquina virtual usando Olá carregar o VHD.

> [!NOTE]
> toomigrate um aplicativo inteiro, considere o uso de [do Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Remeter a unidade de disco rígido
Saudação de uso [método do serviço de importação/exportação do Windows](../../../storage/common/storage-import-export-service.md) tootransfer grandes quantidades de dados de arquivo tooAzure armazenamento de Blob em situações onde carregar pela rede Olá é extremamente dispendioso ou inviável. Com esse serviço, você enviar uma ou mais unidades de disco rígido que contém dados tooan do Azure data center, onde os dados serão carregados tooyour conta de armazenamento.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como executar o SQL Server em Máquinas Virtuais do Azure, veja [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Para obter instruções sobre como criar uma máquina Virtual do Azure SQL Server de uma imagem capturada, consulte [dicas e truques 'clonagem' máquinas virtuais de SQL do Azure de imagens capturadas](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) no blog do hello engenheiros do CSS SQL Server.

