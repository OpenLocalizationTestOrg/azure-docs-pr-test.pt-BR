---
title: "aaaPerformance práticas recomendadas para o SQL Server no Azure | Microsoft Docs"
description: "Fornece as práticas recomendadas para aprimoramento do desempenho do SQL Server em VMs do Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Práticas recomendadas relacionadas ao desempenho para o SQL Server em máquinas virtuais do Azure

## <a name="overview"></a>Visão geral

Este tópico fornece as práticas recomendadas para otimização do desempenho do SQL Server na Máquina Virtual do Microsoft Azure. Durante a execução do SQL Server em máquinas virtuais do Azure, recomendamos que você continue usando Olá as mesmas opções que são aplicável tooSQL Server no ambiente de servidor de local de ajuste de desempenho do banco de dados. No entanto, desempenho de saudação do banco de dados relacional em uma nuvem pública depende de muitos fatores, como tamanho de saudação de uma máquina virtual e a configuração de Olá Olá de discos de dados.

Ao criar imagens do SQL Server, [considere provisionamento suas VMs no portal do Azure de saudação](virtual-machines-windows-portal-sql-server-provision.md). Provisionado no hello Portal com o Gerenciador de recursos de VMs do SQL Server implementa todas essas práticas recomendadas, incluindo a configuração de armazenamento de saudação.

Este artigo destina-se em obter Olá *melhor* desempenho para o SQL Server em VMs do Azure. Se sua carga de trabalho for menos exigente, talvez você não precise de todos os aprimoramentos relacionados abaixo. Considere suas necessidades de desempenho e padrões de carga de trabalho ao avaliar essas recomendações.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Lista de verificação rápida

a seguir Olá é uma lista de verificação rápida para otimizar o desempenho do SQL Server em máquinas virtuais do Azure:

| Área | Otimizações |
| --- | --- |
| [Tamanho da VM](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) ou superior para o SQL Enterprise Edition.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) ou superior para os SQL Standard e Web Editions. |
| [Armazenamento](#storage-guidance) |Use o [Armazenamento Premium](../../../storage/common/storage-premium-storage.md). O armazenamento padrão é recomendado somente para desenvolvimento/teste.<br/><br/>Lembre-Olá [conta de armazenamento](../../../storage/common/storage-create-storage-account.md) e VM do SQL Server no hello mesma região.<br/><br/>Desabilitar o Azure [armazenamento com redundância geográfica](../../../storage/common/storage-redundancy.md) (replicação geográfica) na conta de armazenamento hello. |
| [Discos](#disks-guidance) |Usar no mínimo dois [discos P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (um para arquivos de log; um para arquivos de dados e o TempDB).<br/><br/>Evite usar o sistema operacional ou discos temporários para armazenamento de banco de dados ou registro em log.<br/><br/>Habilite o cache de leitura em discos Olá hospeda os arquivos de dados hello e TempDB.<br/><br/>Não habilite o cache em discos que hospeda o arquivo de log de saudação.<br/><br/>Importante: Parar serviço de SQL Server Olá ao alterar as configurações de cache de saudação de um disco de VM do Azure.<br/><br/>Distribua vários rendimento de IO do tooget aumentado discos de dados do Azure.<br/><br/>Formate com os tamanhos de alocação documentados. |
| [E/S](#io-guidance) |Habilite a compactação de página do banco de dados.<br/><br/>Habilite a inicialização instantânea de arquivos para arquivos de dados.<br/><br/>Limitar ou desabilitar o crescimento automático no banco de dados de saudação.<br/><br/>Desabilite a redução automática no banco de dados de saudação.<br/><br/>Mova todos os discos de toodata de bancos de dados, incluindo bancos de dados do sistema.<br/><br/>Mova do SQL Server erro log e rastreamento diretórios toodata discos de arquivo.<br/><br/>Configure os locais do arquivo de banco de dados e backup padrão.<br/><br/>Habilite as páginas bloqueadas.<br/><br/>Aplique correções de desempenho do SQL Server. |
| [Específico do recurso](#feature-specific-guidance) |Fazer backup diretamente tooblob armazenamento. |

Para obter mais informações sobre *como* e *por* toomake dessas otimizações, examine os detalhes de saudação e orientações fornecidas nas seções a seguir.

## <a name="vm-size-guidance"></a>Diretrizes de tamanho de VM

Para aplicativos sensíveis ao desempenho, é recomendável que você use o seguinte Olá [tamanhos de máquinas virtuais](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 ou superior
* **SQL Server Standard e Web Editions**: DS2 ou superior

## <a name="storage-guidance"></a>Orientação de armazenamento

As VMs da série DS (com as séries DSv2 e GS) dão suporte ao [Armazenamento Premium](../../../storage/common/storage-premium-storage.md). O Armazenamento Premium é recomendado para todas as cargas de trabalho de produção.

> [!WARNING]
> O Armazenamento Standard tem largura de banda e latências variáveis e só é recomendado para cargas de trabalho de desenvolvimento e teste. As cargas de trabalho de produção devem usar o Armazenamento Premium.

Além disso, é recomendável que você crie sua conta de armazenamento do Azure no hello mesmo data center que seu atrasos de transferência de tooreduce de máquinas virtuais do SQL Server. Ao criar uma conta de armazenamento, desabilite a replicação geográfica, pois não há garantia para uma ordem de gravação consistente em vários discos. Em vez disso, considere a configuração de uma tecnologia de recuperação de desastres do SQL Server entre dois data centers do Azure. Para saber mais, confira [Alta disponibilidade e recuperação de desastre para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Diretrizes de discos

Há três tipos principais de discos em uma VM do Azure:

* **Disco do sistema operacional**: quando você cria uma máquina Virtual do Azure, plataforma Olá anexará pelo menos um disco (rotulado como Olá **C** unidade) toohello VM para o disco do sistema operacional. Cada disco é um VHD armazenado como um blob de páginas no armazenamento.
* **Disco temporário**: máquinas virtuais do Azure contêm outro disco chamado disco temporário hello (rotulado como Olá **D**: unidade). Este é um disco no nó de saudação que pode ser usado para o espaço transitório.
* **Discos de dados**: você também pode anexar discos adicionais tooyour VM como discos de dados e eles serão armazenados no armazenamento como blobs de página.

Olá seções a seguir descrevem as recomendações para usar esses discos diferentes.

### <a name="operating-system-disk"></a>Disco do sistema operacional

Um disco do sistema operacional é um VHD que pode ser inicializado e montado como uma versão em execução de um sistema operacional e é rotulado como a unidade **C** .

Cache de política no disco do sistema operacional de saudação padrão é **leitura/gravação**. Para aplicativos sensíveis ao desempenho, recomendamos que você use discos de dados em vez de disco do sistema operacional hello. Consulte a seção de saudação em discos de dados abaixo.

### <a name="temporary-disk"></a>Disco temporário

Olá unidade de armazenamento temporário, rotulada como Olá **D**: disco, não é persistente tooAzure armazenamento de blob. Não armazenar arquivos de banco de dados de usuário ou arquivos de log de transações do usuário no hello **D**: unidade.

Para D-series, série Dv2 e VMs da série G, a unidade temporária Olá nessas máquinas virtuais é baseada em SSD. Se sua carga de trabalho faz uso intenso de TempDB (por exemplo, para objetos temporários ou junções complexas), armazenando o TempDB em Olá **D** unidade pode resultar em maior taxa de transferência de TempDB e reduzir a latência de TempDB.

Para VMs que têm suporte para Armazenamento Premium (séries DS, DSv2 e GS), é recomendável armazenar o TempDB em um disco que dê suporte ao Armazenamento Premium com o cache de leitura habilitado. Há uma recomendação de toothis exceção; Se o uso de TempDB for intensivo de gravação, você poderá obter maior desempenho armazenando TempDB no local de saudação **D** unidade, que também é baseada em SSD sobre esses tamanhos de máquina.

### <a name="data-disks"></a>Discos de dados

* **Usar discos de dados para dados e arquivos de log**: no mínimo, usar o armazenamento de Premium 2 [P30 discos](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) onde um disco contém os arquivos de log hello e Olá outros contém dados saudação e arquivos de TempDB. Cada disco de armazenamento Premium fornece um número de IOPs e largura de banda (MB/s) dependendo de seu tamanho, conforme descrito em Olá artigo a seguir: [usando o armazenamento Premium para discos](../../../storage/common/storage-premium-storage.md).

* **Distribuição de Discos**: para produtividade mais alta, você pode adicionar outros discos de dados e usar a Distribuição de Discos. número de saudação toodetermine de discos de dados, é necessário tooanalyze Olá inúmeros IOPS e largura de banda necessária para os arquivos de log e para seus dados e arquivos de TempDB. Observe que diferentes tamanhos de VM tem limites diferentes no número de saudação de IOPs e largura de banda com suporte, consulte as tabelas de saudação em IOPS por [tamanho da VM](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Olá Use as diretrizes a seguir:

  * Para Windows 8/Windows Server 2012 ou posterior, use [espaços de armazenamento](https://technet.microsoft.com/library/hh831739.aspx) com hello diretrizes a seguir:

      1. Saudação de conjunto de intercalação (tamanho de distribuição) too64 KB (65536 bytes) para cargas de trabalho OLTP e 256 KB (262144 bytes) para cargas de trabalho tooavoid impacto sobre o desempenho devido toopartition desalinhamento de armazenagem de dados. Isso deve ser definido com o PowerShell.
      1. Defina a contagem de colunas = número de discos físicos. Use o PowerShell ao configurar mais de 8 discos (não interface do usuário do Gerenciador do Servidor). 

    Por exemplo, a saudação do PowerShell a seguir cria um novo pool de armazenamento com hello intercalar too64 KB e hello número de colunas too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Para o Windows 2008 R2 ou anterior, você pode usar discos dinâmicos (volumes com marcação) e o tamanho do stripe Olá é sempre 64 KB. Observe que essa opção tornou-se obsoleta no Windows 8/Windows Server 2012. Para obter informações, consulte a declaração de suporte de saudação em [serviço de disco Virtual está em transição tooWindows API de gerenciamento de armazenamento](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Se sua carga de trabalho não utilizar muito o log e não precisar de um IPS dedicado, você poderá configurar apenas um pool de armazenamento. Caso contrário, crie dois pools de armazenamento, um para os arquivos de log hello e outro pool de armazenamento para arquivos de dados hello e TempDB. Determine o número de saudação de discos associados a cada pool de armazenamento com base em suas expectativas de carga. Tenha em mente que tamanhos de VM diferentes permitem quantidades diferentes de discos de dados anexados. Para obter mais informações, confira [Tamanhos das Máquinas Virtuais](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Se você não estiver usando o armazenamento Premium (cenários de desenvolvimento/teste), recomendação Olá é o número de máximo de saudação do tooadd de discos de dados suportado pelo seu [tamanho da VM](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e usar a distribuição de disco.

* **Política de cache**: os discos de dados para o armazenamento Premium, habilitar o cache de leitura em discos de dados Olá hospeda os arquivos de dados e TempDB somente. Se você não estiver usando o Armazenamento Premium, não habilite o caching em discos de dados. Para obter instruções sobre como configurar o cache de disco, consulte Olá tópicos a seguir: [Set-AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) e [Set-AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Pare serviço do SQL Server Olá ao alterar a configuração de cache de saudação da possibilidade de saudação de tooavoid de discos de VM do Azure de qualquer corrupção de banco de dados.

* **Tamanho da unidade de alocação NTFS**: ao formatar o disco de dados Olá, é recomendável que você use um tamanho de unidade de alocação de 64 KB para dados e arquivos de log, bem como TempDB.

* **Práticas recomendadas de gerenciamento de disco**: quando o tipo de remoção de um disco de dados ou alterar seu cache, interromper o serviço de SQL Server de Olá durante a alteração da saudação. Quando as configurações de caching Olá alterado no disco de SO de saudação Azure interrompe Olá VM, altera o tipo de cache hello e reinicia Olá VM. Quando as configurações de cache de saudação de um disco de dados são alteradas, Olá VM não for interrompido, mas o disco de dados Olá é separado da saudação VM durante a saudação alterar e, em seguida, reanexados.

  > [!WARNING]
  > Saudação de toostop falha durante essas operações de serviço do SQL Server pode causar corrupção do banco de dados.

## <a name="io-guidance"></a>Diretrizes de E/S

* obter os melhores resultados Olá com o armazenamento Premium são obtidos quando paralelizar seu aplicativo e as solicitações. Armazenamento Premium foi projetado para cenários em que a profundidade da fila de e/s Olá é maior que 1, para que você veja pouca ou nenhuma ganhos de desempenho para solicitações seriais single-threaded (mesmo que sejam intensivas de armazenamento). Por exemplo, isso poderá afetar os resultados de teste de thread único Olá das ferramentas de análise de desempenho, como SQLIO.

* Considere o uso da [compactação de página do banco de dados](https://msdn.microsoft.com/library/cc280449.aspx) , pois isso pode ajudar a melhorar o desempenho de cargas de trabalho com uso intenso de E/S. No entanto, a compactação de dados Olá pode aumentar o consumo de CPU Olá no servidor de banco de dados de saudação.

* Considere habilitar instantânea de arquivo inicialização tooreduce Olá tempo necessário para alocação de arquivo inicial. tootake vantagem de inicialização instantânea de arquivo, você pode conceder a conta de serviço do SQL Server (MSSQLSERVER) Olá SE_MANAGE_VOLUME_NAME e adicioná-lo toohello **executar tarefas de manutenção de Volume** política de segurança. Se você estiver usando uma imagem de plataforma do SQL Server para o Azure, a conta de serviço saudação padrão (NT Service\MSSQLSERVER) não é adicionada toohello **executar tarefas de manutenção de Volume** política de segurança. Em outras palavras, a inicialização instantânea de arquivo não está habilitada em uma imagem de plataforma do SQL Server do Azure. Depois da adição de saudação do SQL Server service conta toohello **executar tarefas de manutenção de Volume** política de segurança, reinicialização saudação do SQL Server service. Talvez existam considerações de segurança sobre a utilização desse recurso. Para obter mais informações, consulte [Inicialização de Arquivo de Banco de Dados](https://msdn.microsoft.com/library/ms175935.aspx).

* **crescimento automático** é considerado toobe meramente uma contingência de crescimento inesperado. Não gerencie diariamente o crescimento de seus dados e do log com o crescimento automático. Se o crescimento automático for usado, crescer previamente arquivo hello usando a opção de tamanho de saudação.

* Certifique-se de **autoshrink** tooavoid desabilitado sobrecarga desnecessária que pode afetar negativamente o desempenho.

* Mova todos os discos de toodata de bancos de dados, incluindo bancos de dados do sistema. Para saber mais, confira [Mover bancos de dados do sistema](https://msdn.microsoft.com/library/ms345408.aspx).

* Mova do SQL Server erro log e rastreamento diretórios toodata discos de arquivo. Isso pode ser feito no SQL Server Configuration Manager clicando duas vezes na Instância do SQL Server e selecionando Propriedades. Olá configurações de arquivo de log e rastreamento de erro podem ser alteradas no hello **parâmetros de inicialização** Olá na guia diretório de despejo especificado no hello **avançado** Olá guia captura de tela a seguir mostra onde toolook para parâmetro de inicialização do log do erro Hello.

    ![Captura de Tela de Log de Erros do SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Configure os locais do arquivo de banco de dados e backup padrão. Use as recomendações de saudação neste tópico e fazer alterações de saudação na janela de propriedades do servidor de saudação. Para obter instruções, consulte [Olá exibir ou alterar locais padrão para dados e arquivos de Log (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Olá, seguinte captura de tela demonstra onde toomake essas alterações.

    ![Log de Dados de SQL e Arquivos de Backup](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Habilitar bloqueada tooreduce páginas e/s e qualquer atividade de paginação. Para obter mais informações, consulte [habilitar Olá opção Bloquear páginas na memória (Windows)](https://msdn.microsoft.com/library/ms190730.aspx).

* Se você estiver executando o SQL Server 2012, instale a Atualização Cumulativa 10 do Service Pack 1. Esta atualização contém a correção de saudação do desempenho insatisfatório em e/s ao executar a seleção para a instrução de tabela temporária no SQL Server 2012. Para obter informações, consulte este [artigo da base de dados de conhecimento](http://support.microsoft.com/kb/2958012).

* Considere a compactação de qualquer arquivo de dados durante a transferência de entrada/saída do Azure.

## <a name="feature-specific-guidance"></a>Diretrizes específicas do recurso

Algumas implantações podem obter outros benefícios de desempenho usando técnicas mais avançadas de configuração. Olá lista a seguir destaca alguns recursos do SQL Server que podem ajudar a melhorar o desempenho tooachieve:

* **Fazer backup de armazenamento de tooAzure**: ao realizar backups para o SQL Server em execução em máquinas virtuais do Azure, você pode usar [tooURL de Backup do SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Este recurso está disponível a partir do SQL Server 2012 SP1 CU2 e recomendado para fazer backup de discos de dados toohello anexado. Quando você backup/restauração para/do armazenamento do Azure, siga as recomendações de saudação fornecidas no [Backup do SQL Server tooURL práticas recomendadas e solução de problemas e restauração de Backups armazenados no armazenamento do Azure](https://msdn.microsoft.com/library/jj919149.aspx). Você também pode automatizar esses backups usando o [Backup Automatizado para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-automated-backup.md).

    TooSQL anterior Server 2012, você pode usar [tooAzure de Backup do SQL Server ferramenta](https://www.microsoft.com/download/details.aspx?id=40740). Essa ferramenta pode ajudar o rendimento do backup tooincrease utilizando vários alvos de marcação de backup.

* **Arquivos de dados do SQL Server no Azure**: este recurso novo, [Arquivos de dados do SQL Server no Azure](https://msdn.microsoft.com/library/dn385720.aspx), está disponível desde o SQL Server 2014. A execução do SQL Server com os arquivos de dados no Azure demonstra características de desempenho comparáveis as dos discos de dados do Azure.

## <a name="next-steps"></a>Próximas etapas

Para conferir as práticas recomendadas de segurança, consulte [Considerações sobre segurança para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-security.md).

Examine outros tópicos sobre Máquinas Virtuais do SQL Server em [Visão geral do SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).
