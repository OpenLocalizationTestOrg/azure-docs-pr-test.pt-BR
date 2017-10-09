---
title: "aaaHigh desempenho Premium armazenamento e o Azure gerenciados discos para máquinas virtuais | Microsoft Docs"
description: "Saiba mais sobre o Armazenamento Premium de alto desempenho e discos gerenciados para VMs do Azure. As VMs das séries DS, DSv2, GS e Fs do Azure são compatíveis com o Armazenamento Premium."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Armazenamento Premium de alto desempenho e discos gerenciados para VMs
O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais (VMs) com cargas de trabalho com uso intensivo de E/S (entrada/saída). Os discos de VM que usam Armazenamento Premium armazenam dados em SSDs (unidades de estado sólido). tootake vantagem de velocidade de saudação e o desempenho de discos de armazenamento premium, você pode migrar tooPremium de discos VM existente armazenamento.

No Azure, você pode anexar várias tooa de discos de armazenamento premium VM. O uso de vários discos oferece os aplicativos em too256 TB de armazenamento por VM. Com o armazenamento Premium, seus aplicativos podem obter 80.000 operações de e/s por segundo (IOPS) por VM e uma taxa de transferência de disco de backup too2, 000 megabytes por segundo (MB/s) por VM. As operações de leitura oferecem muito menos latências.

Com o armazenamento Premium, o Azure oferece a capacidade de saudação tootruly shift e comparação de precisão exigentes aplicativos empresariais, como nuvem toohello de farms Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite e do SharePoint. Você pode executar cargas de trabalho de banco de dados de alto desempenho em aplicativos como o SQL Server, Oracle, MongoDB, MySQL e Redis, que exigem alto desempenho consistente e baixa latência.

> [!NOTE]
> Para obter melhor desempenho para o seu aplicativo hello, é recomendável que você migre qualquer disco VM que requer alta IOPS tooPremium armazenamento. Se o disco não requer IOPS alta, você pode ajudar a limitar os custos mantendo o armazenamento padrão do Azure. No armazenamento padrão, dados de disco VM são armazenados em unidades de disco rígido (HDD) em vez de SSDs.
> 

O Azure oferece duas maneiras de discos de armazenamento premium toocreate para VMs:

* **Discos não gerenciados**

    método original de saudação é discos toouse não gerenciado. Em um disco não gerenciado, você gerenciar contas de armazenamento Olá que você usa arquivos de disco rígido virtual (VHD) de saudação toostore que correspondem a tooyour discos de VM. Os arquivos VHD são armazenados como blobs de páginas nas contas de armazenamento do Azure. 

* **Discos gerenciados**

    Quando você escolhe [discos gerenciado do Azure](storage-managed-disks-overview.md), o Azure gerencia contas de armazenamento Olá que você pode usar para os discos VM. Especifique o tipo de disco hello (Premium ou padrão) e o tamanho de saudação do disco de saudação que você precisa. Azure cria e gerencia disco Olá para você. Você não tem tooworry sobre onde colocar os discos de saudação em vários tooensure de contas de armazenamento que você está dentro de limites de escalabilidade para suas contas de armazenamento. O Azure trata disso para você.

É recomendável que você escolha discos gerenciados, tootake aproveitar seus muitos recursos.

tooget de Introdução ao armazenamento Premium, [criar sua conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 

Para obter informações sobre como migrar seu tooPremium de VMs armazenamento existente, consulte [converter uma VM do Windows de discos de toomanaged de discos não gerenciado](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) ou [converter uma VM do Linux de discos de toomanaged de discos não gerenciado](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> O Armazenamento Premium está disponível na maioria das regiões. Para obter lista de saudação das regiões disponíveis, em [os serviços do Azure por região](https://azure.microsoft.com/regions/#services), examinar regiões Olá no qual suporte para VMs de tamanho da série de suporte Premium (série DS, série DSV2-series, série GS e as VMs da série Fs) têm suporte.
> 

## <a name="features"></a>Recursos

Aqui estão alguns dos recursos de saudação do armazenamento Premium:

* **Discos de Armazenamento Premium**

    Premium armazenamento dá suporte a discos de VM que podem ser anexado a série toospecific tamanho VMs. O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS, Ls e Fs. Você tem sete opções de tamanho de disco: P4 (32 GB), P6 (64 GB), P10 (128 GB), P20 (512 GB), P30 (1024 GB), P40 (2048 GB), P50 (4095 GB). Tamanhos de disco P4 e P6 no momento têm suporte somente para o Managed Disks. Cada tamanho de disco tem suas próprias especificações de desempenho. Dependendo dos requisitos de aplicativo, você pode anexar um ou mais discos tooyour VM. Descrevemos especificações hello mais detalhadamente em [destinos de escalabilidade e desempenho de armazenamento Premium](#scalability-and-performance-targets).

* **Blobs de página Premium**

    O Armazenamento Premium dá suporte a blobs de página. Os blobs de página usar discos persistentes e não gerenciado de toostore para VMs no armazenamento Premium. Ao contrário do Armazenamento do Azure padrão, o Armazenamento Premium não oferece suporte a blobs de bloco, blobs de acréscimo, arquivos, tabelas ou filas. Blobs de página Premium oferece suporte a seis tamanhos de P10 tooP50 e P60 (8191GiB). Blob de páginas P60 Premium não é suportada toobe anexado como discos VM. 

    Qualquer objeto colocado em uma conta de armazenamento premium será um blob de páginas. blob de página Olá ajusta tooone de saudação com suporte a tamanhos de provisionamento. Isso é por uma conta de armazenamento premium não se destina toobe usado blobs pequenos toostore.

* **Conta de Armazenamento Premium**

    toostart usando o armazenamento Premium, crie uma conta de armazenamento premium para discos não gerenciados. Em Olá [portal do Azure](https://portal.azure.com), escolha de toocreate uma conta de armazenamento premium Olá **Premium** nível de desempenho. Selecione Olá **armazenamento localmente redundante (LRS)** opção de replicação. Você também pode criar uma conta de armazenamento premium, configurando o tipo de saudação muito**Premium_LRS** em uma saudação locais a seguir:
    * [API REST de armazenamento](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (versão 2014-02-14 ou posterior)
    * [API REST do Gerenciamento de Serviço](http://msdn.microsoft.com/library/azure/ee460799.aspx) (versão 2014-10-01 ou posterior; para implantações de clássicas do Azure)
    * [API REST do Azure do provedor de recursos de armazenamento](https://docs.microsoft.com/rest/api/storagerp) (para implantações do Azure Resource Manager)
    * [Azure PowerShell](../powershell-install-configure.md) (versão 0.8.10 ou posterior)

    toolearn sobre limites de conta de armazenamento premium, consulte [destinos de escalabilidade e desempenho de armazenamento Premium](#premium-storage-scalability-and-performance-targets).

* **Armazenamento com redundância local Premium**

    Uma conta de armazenamento premium dá suporte ao armazenamento de redundância apenas local como a opção de replicação hello. Armazenamento com redundância local mantém três cópias de dados hello dentro de uma única região. Para recuperação de desastres regionais, você deve fazer backup os discos VM em uma região diferente usando o [Backup do Azure](../backup/backup-introduction-to-azure-backup.md). Você também deve usar uma conta de armazenamento com redundância geográfica (GRS) como o Cofre de backup hello. 

    O Azure usa a conta de armazenamento como contêiner para seus discos não gerenciados. Quando você cria uma VM do Azure da série DS, série DSv2, série GS, ou série Fs com discos não gerenciados e seleciona uma conta de armazenamento premium, o sistema operacional e discos de dados são armazenados na conta de armazenamento.

## <a name="supported-vms"></a>VMs com suporte
O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS, Ls e Fs. Você pode usar os discos do Armazenamento Standard e Premium com esses tipos de VM. Não é possível usar discos de Armazenamento Premium com séries de VM que não são compatíveis com o Armazenamento Premium.

Para obter informações sobre tipos de VM e tamanhos no Azure para Windows, confira [Tamanhos de VM do Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para obter informações sobre tipos de VM e tamanhos no Azure para Linux, confira [Tamanhos de VM Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Estes são alguns dos recursos de saudação do hello série DS, série DSv2-series, série GS, Ls-series e as VMs da série Fs:

* **Serviço de nuvem**

    Você pode adicionar as VMs da série DS tooa serviço de nuvem tem apenas as VMs da série DS. Não adicione VMs da série DS tooan serviço de nuvem existente que tenha qualquer tipo diferente de VMs da série DS. Você pode migrar seu VHDs tooa novo serviço de nuvem existente que executa apenas as VMs da série DS. Se você quiser toouse Olá mesmo endereço IP virtual para Olá novo serviço de nuvem que hospeda suas VMs da série DS, use [endereços IP reservados](../virtual-network/virtual-networks-instance-level-public-ip.md). As VMs da série GS podem ser adicionadas tooan serviço de nuvem existente que tenha somente as VMs da série GS.

* **Disco do sistema operacional**

    Você pode configurar sua VM de armazenamento Premium toouse um premium ou um disco de sistema operacional padrão. Para melhor experiência de Olá, é recomendável usar um disco de sistema operacional baseado em armazenamento Premium.

* **Discos de dados**

    Você pode usar o premium e Olá de discos padrão na mesma VM de armazenamento Premium. Com o armazenamento Premium, você pode provisionar uma máquina virtual e conectar várias toohello de discos de dados persistentes VM. Se necessário, a capacidade de saudação do tooincrease e o desempenho do volume hello, você pode distribuir em seus discos.

    > [!NOTE]
    > Se você distribuir discos de dados de armazenamento premium usando [Espaços de Armazenamento](http://technet.microsoft.com/library/hh831739.aspx), configure espaços de armazenamento com uma coluna para cada disco que será usado. Caso contrário, geral desempenho do volume de saudação distribuída pode ser menor do que o esperado devido a distribuição irregular de tráfego entre os discos de saudação. Por padrão, no Gerenciador do servidor, você pode definir as colunas para os discos too8. Se você tiver mais de 8 discos, use o volume de saudação do PowerShell toocreate. Especifica manualmente o número de saudação de colunas. Caso contrário, Olá Gerenciador do servidor UI continua toouse 8 colunas, mesmo se você tiver mais discos. Por exemplo, se você tiver 32 discos em um conjunto único de distribuição, especifique 32 colunas. número de saudação toospecify de colunas Olá uso de disco virtual, em Olá [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) cmdlet do PowerShell, use Olá *NumberOfColumns* parâmetro. Para obter mais informações, confira [Visão geral dos espaços de armazenamento](http://technet.microsoft.com/library/hh831739.aspx) e [Perguntas frequentes de espaços de armazenamento](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Cache**

    As VMs na série de tamanho de saudação que dão suporte ao armazenamento Premium têm um recurso de cache exclusivo de altos níveis de taxa de transferência e latência. Olá capacidade de cache excede o desempenho do disco de armazenamento premium subjacente. Você pode definir a política nos discos de armazenamento premium do cache muito no disco Olá**ReadOnly**, **ReadWrite**, ou **nenhum**. saudação padrão disco política de cache é **ReadOnly** para todos os discos de dados premium, e **ReadWrite** para discos do sistema operacional. Para obter desempenho ideal para seu aplicativo, use Olá corrija a configuração de cache. Por exemplo, alta taxa de leitura ou somente leitura para discos de dados, como arquivos de dados do SQL Server, definir disco Olá política de cache muito**ReadOnly**. Pesada de gravação ou somente gravação para discos de dados, como arquivos de log do SQL Server, defina o disco Olá política de cache muito**nenhum**. toolearn mais sobre como otimizar o seu design de armazenamento Premium, consulte [Design de desempenho com o armazenamento Premium](storage-premium-storage-performance.md).

* **Analytics**

    desempenho de VM tooanalyze usando discos no armazenamento Premium, ativar o diagnóstico VM no hello [portal do Azure](https://portal.azure.com). Para obter mais informações, confira [Monitoramento de VM do Azure com extensão de diagnóstico do Azure](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    usar ferramentas baseadas no sistema operacional, toosee o desempenho do disco, como [o Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) para máquinas virtuais do Windows e hello [iostat](http://linux.die.net/man/1/iostat) comando para VMs do Linux.

* **Desempenho e limites de escala VM**

    Cada tamanho VM com suporte para armazenamento Premium tem limites de escala e especificações de desempenho de IOPS, largura de banda e número de saudação de discos que podem ser anexados por VM. Quando você usar discos de armazenamento premium com máquinas virtuais, certifique-se de que haja suficiente IOPS e largura de banda em seu tráfego de disco toodrive VM.

    Por exemplo, uma VM STANDARD_DS1 tem uma largura de banda dedicada de 32 MB/s para o tráfego de discos do Armazenamento Premium. Um disco de Armazenamento Premium P10 pode fornecer uma largura de banda de 100 MB/s. Se um disco de armazenamento premium P10 toothis anexado VMs, pode fazer backup too32 MB/s. Não será possível usar Olá que máximo 100 MB/s disco P10 Olá pode fornecer.

    Atualmente, hello VM maior no hello série DS é hello Standard_DS15_v2. Olá Standard_DS15_v2 pode fornecer o too960 MB/s em todos os discos. Olá VM maior no hello série GS é hello Standard_GS5. Olá Standard_GS5 pode fornecer até too2, 000 MB/s em todos os discos.

    Observe que esses limites são apenas para o tráfego de disco. Esses limites não incluem acertos de cache e tráfego de rede. Uma largura de banda separada está disponível para o tráfego de rede de VM. Largura de banda para o tráfego de rede é diferente da largura de banda Olá dedicado usada pelos discos de armazenamento premium.

    Para Olá informações mais atualizadas sobre a taxa de transferência (largura de banda) e IOPS máximo para VMs com suporte para armazenamento Premium, consulte [tamanhos de VM do Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Para obter mais informações sobre discos de armazenamento premium e seus limites IOPS e taxa de transferência, consulte a tabela de saudação na próxima seção, Olá.

## <a name="scalability-and-performance-targets"></a>Escalabilidade e metas de desempenho
Nesta seção, descrevemos Olá tooconsider de destinos de escalabilidade e desempenho quando você usa o armazenamento Premium.

Contas de armazenamento Premium têm Olá destinos de escalabilidade a seguir:

| Capacidade total da conta | Largura de banda total para uma conta de armazenamento com redundância local |
| --- | --- | 
| Capacidade do disco: 35 TB <br>Capacidade do instantâneo: 10 TB | Backup too50 gigabits por segundo para entrada<sup>1</sup> + saída<sup>2</sup> |

<sup>1</sup> todos os dados (solicitações) que são enviados a conta de armazenamento tooa

<sup>2</sup> Todos os dados (respostas) que são recebidos de uma conta de armazenamento

Para saber mais, confira [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).

Se você estiver usando contas de armazenamento premium para discos não gerenciados e seu aplicativo exceder os destinos de escalabilidade de saudação de uma única conta de armazenamento, você poderá toomigrate toomanaged discos. Se você não quiser toomigrate toomanaged discos, crie seu aplicativo toouse várias contas de armazenamento. Em seguida, particione os dados nessas contas de armazenamento. Por exemplo, se você quiser tooattach discos de 51 TB em várias VMs, espalhá-los por duas contas de armazenamento. 35 TB é o limite de saudação para uma conta de armazenamento premium único. Certifique-se de que uma única conta de Armazenamento Premium nunca tenha mais do que 35 TB de discos provisionados.

### <a name="premium-storage-disk-limits"></a>Limites do disco de Armazenamento Premium
Quando você provisionar um disco de armazenamento premium, o tamanho de saudação do disco de saudação determina Olá máximo de IOPS e taxa de transferência (largura de banda). O Azure oferece sete tipos de disco de armazenamento Premium: P4 (somente Managed Disks), P6 (somente Managed Disks), P10, P20, P30, P40 e P50. Cada tipo de disco de armazenamento premium tem limites específicos de IOPS e taxa de transferência. Limites para tipos de disco Olá descritos Olá a tabela a seguir:

| Tipo de discos premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2.300              | 5.000              | 7500              | 7500              | 
| Taxa de transferência por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

> [!NOTE]
> Certifique-se de largura de banda suficiente está disponível no tráfego de disco de toodrive sua VM, conforme descrito em [suporte para armazenamento Premium VMs](#premium-storage-supported-vms). Caso contrário, a taxa de transferência do disco e o IOPS é restrita toolower valores. Taxa de transferência máxima e IOPS com base nos limites VM hello, não em limites de disco Olá descritos Olá anterior da tabela.  
> 
> 

Aqui estão alguns tooknow coisas importantes sobre os destinos de escalabilidade e desempenho de armazenamento Premium:

* **Desempenho e capacidade provisionada**

    Quando você provisiona um disco de armazenamento premium, ao contrário do armazenamento padrão, você terá garantia de capacidade hello, IOPS e taxa de transferência de disco. Por exemplo, se você criar um disco P50, o Azure provisionará uma capacidade de armazenamento de 4.095 GB, 7.500 IOPS e uma taxa de transferência de 250 MB/s para o disco. Seu aplicativo pode usar toda ou parte da saudação capacidade e desempenho.

* **Tamanho do disco**

    Mapas do Azure Olá toohello de tamanho (arredondado para cima) de disco mais próximo da opção de disco de armazenamento premium, conforme especificado na tabela Olá Olá anterior a seção. Por exemplo, um tamanho de disco de 100 GB é classificado como uma opção P10. Ele pode realizar backup too500 IOPS, com a taxa de transferência too100 MB/s. Da mesma forma, um disco de tamanho de 400 GB é classificado como P20. Ele pode realizar backup too2, 300 IOPS com produtividade de 150 MB/s.
    
    > [!NOTE]
    > Você facilmente pode aumentar o tamanho de saudação de discos existentes. Por exemplo, convém tooincrease tamanho de saudação de 30 GB de disco too128 GB ou TB too1 mesmo. Ou, você poderá tooconvert tooa P30 de disco seu P20 porque você precisa de mais capacidade ou mais IOPS e taxa de transferência. 
    > 
 
* **Tamanho de E/S**

    tamanho de saudação de uma e/s é 256 KB. Se dados Olá transferidos forem menor que 256 KB, ele será considerado 1 unidade de e/s. Tamanhos maiores de e/s são contados como várias entradas e saídas de tamanho de 256 KB. Por exemplo, 1.100 KB E/S é contado como cinco unidades de E/S.

* **Taxa de transferência**

    limite de taxa de transferência de saudação inclui toohello de gravações de disco e inclui operações de leitura de disco que não são atendidas do cache de saudação. Por exemplo, um disco P10 tem taxa de transferência de 100 MB/s por disco. Alguns exemplos de taxa de transferência válido para um disco P10 são mostrados em Olá a tabela a seguir:

    | Taxa de transferência máxima por disco P10 | Leituras não armazenadas em cache do disco | Gravações em cache não toodisk |
    | --- | --- | --- |
    | 100 MB/s | 100 MB/s | 0 |
    | 100 MB/s | 0 | 100 MB/s |
    | 100 MB/s | 60 MB/s | 40 MB/s |

* **Acertos do cache**

    Acertos de cache não são limitados por Olá alocado IOPS ou a taxa de transferência de disco hello. Por exemplo, quando você usa um disco de dados com um **ReadOnly** configuração de cache em uma VM que é suportada pelo armazenamento Premium, leituras são atendidas do cache de saudação não é assunto toohello IOPS e limites de taxa de transferência do disco hello. Se a carga de trabalho de saudação de um disco é predominantemente lê, você pode obter muito alta taxa de transferência. cache de saudação é assunto tooseparate IOPS e limites de taxa de transferência a saudação nível da VM, com base no tamanho da VM de saudação. VMs da série DS têm aproximadamente 4.000 IOPS e taxa de transferência de 33 MB/s por núcleo para cache e E/S de SSD local. As VMs da série GS têm um limite de 5.000 IOPS e taxa de transferência de 50 MB/s por núcleo para cache e E/S de SSD local. 

## <a name="throttling"></a>Limitação
A limitação pode ocorrer se o seu aplicativo IOPS ou a taxa de transferência excede os limites de saudação alocada para um disco de armazenamento premium. Também limitação pode ocorrer se o tráfego total em disco em todos os discos em Olá VM exceder o limite de largura de banda de disco de saudação disponível para Olá VM. tooavoid limitação, é recomendável limitar o número de saudação de pendentes solicitações de e/s de disco de saudação. Use um limite com base em destinos de escalabilidade e desempenho do disco Olá que ter provisionado e Olá disco largura de banda disponível toohello VM.  

Seu aplicativo pode obter a menor latência de saudação quando ele é projetado tooavoid limitação. No entanto, se hello a número de solicitações de e/s de disco Olá pendentes é muito pequeno, seu aplicativo não pode tirar proveito da saudação níveis máximos de IOPS e taxa de transferência que estão disponíveis toohello disco.

Olá exemplos a seguir demonstram como limitação toocalculate níveis. Todos os cálculos baseiam-se no tamanho da unidade de E/S de 256 KB.

### <a name="example-1"></a>Exemplo 1
O aplicativo processou 495 unidades de E/S de tamanho de 16 KB em um segundo em um disco P10. unidades de e/s de saudação são contadas como 495 IOPS. Se você tentar uma e/s de 2 MB no Olá mesmo segundo, total de saudação de unidades de e/s é igual too495 + 8 IOPS. Isso ocorre porque 2 MB e/s = unidades de 256 KB/2.048 KB = 8 e/s ao Olá tamanho de unidade de e/s é 256 KB. Como soma de Olá de 495 + 8 excede limite de IOPS 500 Olá para disco Olá, a limitação ocorre.

### <a name="example-2"></a>Exemplo 2
Seu aplicativo processou 400 unidades de E/S de tamanho de 256 KB em um disco P10. Olá largura de banda total consumida (400 &#215; 256) / 1.024 KB = 100 MB/s. Um disco P10 tem um limite de taxa de transferência de 100 MB/s. Se seu aplicativo tenta tooperform mais operações de e/s em que o segundo, ele é limitado porque ele excede o limite de saudação alocada.

### <a name="example-3"></a>Exemplo 3
Você tem uma VM DS4 com dois discos P30 conectados. Cada disco P30 é capaz de ter uma taxa de transferência de 200 MB/s. No entanto, uma VM DS4 tem uma capacidade de largura de banda total do disco de 256 MB/s. Não é a unidade de produtividade máxima de toohello ambos os discos anexados nessa VM DS4 em Olá simultaneamente. tooresolve isso, pode permitir tráfego de 200 MB/s em um disco e 56 MB/s em Olá outro disco. Se a soma de saudação do tráfego em disco será 256 MB/s, tráfego de disco é limitado.

> [!NOTE]
> Se o tráfego de disco principalmente consiste em tamanhos pequenos de e/s, seu aplicativo provavelmente será atingiu o limite IOPS de saudação antes de limite de taxa de transferência de saudação. No entanto, se o tráfego de disco Olá principalmente consiste em grandes tamanhos de e/s, seu aplicativo provavelmente será atingido limite de taxa de transferência de saudação primeiro, em vez de limite de IOPS de saudação. Você pode maximizar o IOPS do aplicativo e a capacidade de taxa de transferência usando tamanhos de E/S ideais. Além disso, você pode limitar o número de saudação de solicitações de e/s para um disco pendentes.
> 

toolearn mais sobre a criação de alto desempenho usando o armazenamento Premium, consulte [Design de desempenho com o armazenamento Premium](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Instantâneos e cópia de Blob

toohello serviço de armazenamento do arquivo VHD Olá é um blob de página. Você pode tirar instantâneos de blobs de página e copiá-los tooanother local, como tooa outra conta de armazenamento.

### <a name="unmanaged-disks"></a>Discos não gerenciados

Criar [instantâneos incrementais](storage-incremental-snapshots.md) para discos não gerenciado premium Olá mesma forma como você usa instantâneos com o armazenamento padrão. Armazenamento Premium dá suporte ao armazenamento de redundância apenas local como a opção de replicação hello. É recomendável que você crie instantâneos e, em seguida, copie a conta de armazenamento com redundância geográfica de padrão de tooa Olá instantâneos. Para saber mais, confira [Opções de redundância do Armazenamento do Azure](storage-redundancy.md).

Se um disco estiver anexado tooa VM, algumas operações de API no disco Olá não são permitidas. Por exemplo, você não pode executar uma [cópia Blob](/rest/api/storageservices/Copy-Blob) operação nesse blob se Olá disco estiver anexado tooa VM. Em vez disso, primeiro crie um instantâneo do blob usando Olá [Blob de instantâneo](/rest/api/storageservices/Snapshot-Blob) API REST. Em seguida, execute Olá [cópia Blob](/rest/api/storageservices/Copy-Blob) de saudação do hello instantâneo toocopy disco anexado. Como alternativa, você pode desanexar o disco hello e, em seguida, executar todas as operações necessárias.

Olá limites a seguir se aplicam a toopremium instantâneos de blob de armazenamento:

| Limite de armazenamento Premium | Valor |
| --- | --- |
| Número máximo de instantâneos por blob | 100 |
| Capacidade de conta de armazenamento de instantâneos<br>(Inclui dados em apenas instantâneos. Não inclui dados no blob de base.) | 10 TB |
| Tempo mínimo entre instantâneos consecutivos | 10 minutos |

toomaintain cópias com redundância geográfica de seus instantâneos, você pode copiar os instantâneos de uma conta de armazenamento padrão com redundância geográfica premium armazenamento conta tooa usando AzCopy ou cópia de Blob. Para obter mais informações, consulte [transferir dados com o utilitário de linha de comando do hello AzCopy](storage-use-azcopy.md) e [cópia Blob](/rest/api/storageservices/Copy-Blob).

Para obter informações detalhadas sobre como executar operações REST em blobs de página nas contas de Armazenamento Premium, confira [Operações do serviço Blob com o Armazenamento Premium do Azure](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Discos gerenciados

Um instantâneo de um disco gerenciado é uma cópia somente leitura de disco gerenciado hello. Olá instantâneo é armazenado como um disco gerenciado padrão. Atualmente, [instantâneos incrementais](storage-incremental-snapshots.md) não têm suporte para discos gerenciados. toolearn como tootake um instantâneo para um disco gerenciado, consulte [criar uma cópia de um VHD armazenado como um Azure gerenciado disco usando instantâneos gerenciados no Windows](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) ou [criar uma cópia de um VHD armazenado como um Azure gerenciado disco usando gerenciados instantâneos no Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Se um disco gerenciado é anexado tooa VM, algumas operações de API no disco Olá não são permitidas. Por exemplo, você não pode gerar uma SAS (assinatura) de acesso compartilhado tooperform uma operação de cópia enquanto o disco de saudação está anexado tooa VM. Em vez disso, primeiro criar um instantâneo do disco hello e, em seguida, executar a cópia de saudação do instantâneo de saudação. Como alternativa, você pode desanexar o disco hello e, em seguida, gerar uma operação de cópia do SAS tooperform hello.


## <a name="premium-storage-for-linux-vms"></a>Armazenamento Premium para VMs do Linux
Você pode usar o hello toohelp informações que você configurar suas VMs do Linux no armazenamento Premium a seguir:

destinos de escalabilidade tooachieve no armazenamento Premium, para todos os discos de armazenamento premium com o conjunto de cache muito**ReadOnly** ou **nenhum**, você deve desabilitar a "barreiras" ao montar o sistema de arquivo hello. Você não precisa barreiras nesse cenário porque Olá grava toopremium discos de armazenamento são duráveis para essas configurações de cache. Quando a solicitação de gravação da saudação foi concluída com êxito, dados foram gravados repositório persistente toohello. toodisable "barreiras", use um dos métodos a seguir de saudação. Escolha a saudação para seu sistema de arquivos:
  
* Para **reiserFS**, toodisable barreiras, use Olá `barrier=none` opção de montagem. (as barreiras tooenable, use `barrier=flush`.)
* Para **ext3/ext4**, toodisable barreiras, use Olá `barrier=0` opção de montagem. (as barreiras tooenable, use `barrier=1`.)
* Para **XFS**, toodisable barreiras, use Olá `nobarrier` opção de montagem. (as barreiras tooenable, use `barrier`.)
* Para discos de armazenamento premium com o cache configurado muito**ReadWrite**, habilite as barreiras de durabilidade de gravação.
* Para toopersist de rótulos de volume após a reinicialização Olá VM, você deve atualizar /etc/fstab com hello identificador universalmente exclusivo (UUID) referências toohello discos. Para obter mais informações, consulte [adicionar tooa um disco gerenciado VM Linux](../virtual-machines/linux/add-disk.md).

Olá distribuições do Linux a seguir foram validado para o armazenamento Premium do Azure. Para obter melhor desempenho e estabilidade com o armazenamento Premium, é recomendável que você atualize seu tooone VMs dessas versões, no mínimo (ou tooa versão posterior). Alguns dos Olá versões exigem hello mais recente Integration Services LIS (Linux), v 4.0, para o Azure. toodownload e instale uma distribuição, siga o link de saudação listado no Olá a tabela a seguir. Adicionamos a lista de toohello imagens como podemos concluir a validação. Observe que nossas validações mostram que o desempenho varia para cada imagem. O desempenho depende da carga de trabalho e das configurações de imagem. Imagens diferentes são ajustadas para tipos diferentes de carga de trabalho.

| Distribuição | Versão | Kernel com suporte | Detalhes |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 obrigatório](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consulte a observação na próxima seção, Olá* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 recomendado](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consulte a observação na próxima seção, Olá* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 ou RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 ou RHCK c/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 ou RHCK c/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Drivers LIS para Openlogic CentOS

Se você estiver executando OpenLogic CentOS VMs, execute Olá drivers mais recentes do comando tooinstall Olá a seguir:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

Olá tooactivate novos drivers, reinicie o computador de saudação.

## <a name="pricing-and-billing"></a>Preços e cobrança

Quando você usa o armazenamento Premium Olá cobrança considerações a seguir se aplicam:

* **Tamanho de disco e blob de Armazenamento Premium**

    Cobrança por um disco de armazenamento premium ou blob depende do tamanho Olá provisionado de disco de saudação ou blob. Mapas do Azure Olá toohello tamanho provisionado (arredondado) mais próximo da opção de disco de armazenamento premium. Para obter detalhes, consulte a tabela Olá [destinos de escalabilidade e desempenho de armazenamento Premium](#premium-storage-scalability-and-performance-targets). Cada tooa de mapas de disco com suporte provisionado o tamanho do disco e é cobrado de acordo. A cobrança por qualquer disco provisionado é proporcional por hora, usando o preço mensal Olá de oferta de armazenamento Premium Olá. Por exemplo, se você provisionado um disco P10 e excluído após 20 horas, você será cobrado Olá P10 oferta rateados too20 horas. Isso ocorre independentemente da quantidade de saudação de dados reais gravados toohello disco ou hello IOPS e taxa de transferência usada.

* **Instantâneos de discos não gerenciados Premium**

    Instantâneos de discos premium não gerenciado são cobrados para capacidade adicional de saudação usada por instantâneos do hello. Para obter mais informações sobre instantâneos, confira [Criar um instantâneo de um blob](/rest/api/storageservices/Snapshot-Blob).

* **Instantâneos de discos gerenciados Premium**

    Um instantâneo de um disco gerenciado é uma cópia somente leitura de disco de saudação. Olá disco é armazenado como um disco gerenciado padrão. Os custos de um instantâneo Olá mesmo como um padrão gerenciado em disco. Por exemplo, se você capturar um instantâneo de um disco de 128 GB premium gerenciado, o custo de saudação do instantâneo de saudação é equivalente tooa 128 GB disco gerenciado padrão.  

* **Transferências de dados de saída**

    [Transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados saindo dos data centers do Azure) acarretam a cobrança por uso de largura de banda.

Para obter informações detalhadas sobre os preços para Armazenamento Premium, o suporte para Armazenamento Premium VMs e discos gerenciados, confira estes artigos:

* [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Preços de Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Preços de discos gerenciados](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Suporte de Backup do Azure 

Para a recuperação de desastre regional, é necessário fazer backup dos discos da VM em outra região usando o [Backup do Azure](../backup/backup-introduction-to-azure-backup.md) e uma conta de armazenamento GRS como o cofre de backup.

toocreate um trabalho de backup com backups baseados em tempo, fácil restauração de VM e políticas de retenção de backup, use o Backup do Azure. Você pode usar os Backup com discos gerenciados e não gerenciados. Para obter mais informações, confira [Backup do Azure para máquinas virtuais com discos não gerenciados](../backup/backup-azure-vms-first-look-arm.md) e [Backup do Azure para máquinas virtuais com discos gerenciados](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o armazenamento Premium, consulte Olá artigos a seguir.

### <a name="design-and-implement-with-premium-storage"></a>Criar e implementar com o Armazenamento Premium
* [Design para desempenho com o Armazenamento Premium](storage-premium-storage-performance.md)
* [Operações de armazenamento de blobs com o Armazenamento Premium](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Diretrizes operacionais
* [Migrar tooAzure armazenamento Premium](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Postagens no blog
* [Armazenamento Premium do Azure com disponibilidade geral](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Anunciando Olá série GS: adicionando toohello de suporte de armazenamento Premium maior Olá de VMs na nuvem pública](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
