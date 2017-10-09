---
title: "aaaSAP HANA Azure Backup em nível de arquivo | Microsoft Docs"
description: "Há duas possibilidades principais de backup para SAP HANA em máquinas virtuais do Azure, e este artigo aborda o Backup do Azure do SAP HANA no nível do arquivo"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Backup do Azure do SAP HANA no nível do arquivo

## <a name="introduction"></a>Introdução

Este artigo faz parte de uma série dividida em três partes com artigos relacionados ao backup do SAP HANA. [Guia de backup para o SAP HANA em máquinas virtuais Azure](./sap-hana-backup-guide.md) fornece uma visão geral e informações sobre como começar, e [backup SAP HANA com base em instantâneos de armazenamento](./sap-hana-backup-storage-snapshots.md) abrange Olá opção backup de armazenamento baseados em instantâneo.

Verificando Olá tamanhos de VM do Azure, um pode ver um GS5 permite 64 discos de dados anexado. Para sistemas SAP HANA de grande porte, um número considerável de discos já pode estar ocupado por arquivos de log e de dados, possivelmente em combinação com RAID de software para obtenção da melhor taxa de transferência de E/S de disco. pergunta de Hello, em seguida, é onde toostore SAP HANA fazer backup de arquivos, que podem preencher dados saudação anexado discos ao longo do tempo? Consulte [tamanhos de máquinas virtuais Linux no Azure](../../linux/sizes.md) para tabelas de tamanho de VM do Azure hello.

No momento, não há integração de backup do SAP HANA disponível com o serviço de Backup do Azure. modo padrão de saudação toomanage backup/restauração no nível de arquivo hello é com um backup baseado em arquivo por meio do SAP HANA Studio ou instruções SQL do SAP HANA. Confira [SAP HANA SQL e referência de exibições do sistema](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) para saber mais.

![Esta figura mostra a caixa de diálogo Olá Olá backup do item de menu no SAP HANA Studio](media/sap-hana-backup-file-level/image022.png)

Esta figura mostra a caixa de diálogo Olá Olá backup do item de menu no SAP HANA Studio. Ao escolher o tipo &quot;arquivo,&quot; um tem um caminho toospecify no sistema de arquivos Olá onde SAP HANA grava arquivos de backup hello. A restauração funciona Olá mesma maneira.

Embora essa opção pareça simples e direta, há algumas considerações. Conforme mencionado anteriormente, uma VM do Azure tem uma limitação no número de discos de dados que podem ser anexados. Talvez não haja capacidade toostore SAP HANA arquivos de backup em sistemas de arquivos de saudação do hello VM, dependendo do tamanho de saudação do hello banco de dados e requisitos de produtividade, que pode envolver o software RAID usando distribuindo entre dados de vários discos. Posteriormente, este artigo fornece várias opções para mover esses arquivos de backup e gerenciar as restrições de tamanho de arquivo e desempenho ao lidar com terabytes de dados.

Outra opção, que oferece mais liberdade com relação à capacidade total, é o Armazenamento de Blobs do Azure. Enquanto um único blob também é restrito too1 TB, a capacidade total de saudação de um único contêiner de blob está atualmente 500 TB. Além disso, ele oferece aos clientes, chamados de tooselect choice Olá &quot;moderado&quot; armazenamento de blob, que tem um custo-benefício. Confira [Armazenamento de Blobs do Azure: camadas de armazenamento dinâmica e estática](../../../storage/blobs/storage-blob-storage-tiers.md) para obter detalhes sobre o armazenamento de blobs frio.

Para segurança adicional, use um armazenamento replicado geograficamente conta toostore Olá SAP HANA os backups. Confira [Replicação de Armazenamento do Azure](../../../storage/common/storage-redundancy.md) para obter mais detalhes sobre a replicação da conta de armazenamento.

É possível colocar VHDs dedicados para backups do SAP HANA em uma conta de armazenamento de backup dedicada com replicação geográfica. Caso contrário, um pode copiar VHDs Olá manter backups do SAP HANA Olá conta de armazenamento replicado geograficamente tooa ou tooa conta de armazenamento que está em uma região diferente.

## <a name="azure-backup-agent"></a>Agente de backup do Azure

Ofertas de backup do Azure Olá opção toonot backup somente completo VMs, mas também arquivos e diretórios por meio do agente de backup hello, que tem toobe instalado no sistema operacional convidado de saudação. Mas a partir de dezembro de 2016, o agente só tem suporte no Windows (consulte [fazer backup de um tooAzure de cliente ou servidor do Windows usando o modelo de implantação do Gerenciador de recursos de saudação](../../../backup/backup-configure-vault.md)).

Uma solução alternativa é copiar toofirst tooa de arquivos de backup do SAP HANA VM do Windows no Azure (por exemplo, por meio do compartilhamento SAMBA) e use Olá agente de backup do Azure a partir daí. Embora seja tecnicamente possível, ele seria adicionar complexidade e reduzir a velocidade do backup hello ou restaurar processo bastante devido a cópia toohello entre Olá Linux e hello VM do Windows. Não é recomendável toofollow essa abordagem.

## <a name="azure-blobxfer-utility-details"></a>Detalhes do utilitário blobxfer do Azure

toostore diretórios e arquivos no armazenamento do Azure, você pode usar CLI ou o PowerShell, ou desenvolva uma ferramenta usando um Olá [SDKs do Azure](https://azure.microsoft.com/downloads/). Também há um utilitário prontos para uso, AzCopy, para copiar o armazenamento de tooAzure de dados, mas é só Windows (consulte [transferir dados com hello utilitário de linha de comando AzCopy](../../../storage/common/storage-use-azcopy.md)).

Portanto, o blobxfer foi usado para copiar arquivos de backup do SAP HANA. Ele é um software livre, usado por muitos clientes em ambientes de produção e disponível no [GitHub](https://github.com/Azure/blobxfer). Essa ferramenta permite que os dados toocopy diretamente tooeither Azure blob storage ou compartilhamento de arquivos do Azure. Ele também oferece vários recursos úteis, como o hash md5 ou o paralelismo automático ao copiar um diretório com vários arquivos.

## <a name="sap-hana-backup-performance"></a>Desempenho de backup do SAP HANA

![Esta captura de tela é Olá SAP HANA backup console SAP HANA Studio](media/sap-hana-backup-file-level/image023.png)

Esta captura de tela é Olá SAP HANA backup console SAP HANA Studio. Que levou o backup do aproximadamente 42 minutos toodo Olá Olá 230 GB em um disco único armazenamento padrão do Azure anexados toohello HANA VM usando o sistema de arquivos XFS.

![Esta captura de tela é do YaST na VM de teste do hello SAP HANA](media/sap-hana-backup-file-level/image024.png)

Esta captura de tela é de YaST na VM de teste do hello SAP HANA. Um pode ver Olá 1 TB único disco de backup do SAP HANA conforme mencionado anteriormente. Levou aproximadamente 42 minutos toobackup 230 GB. Além disso, cinco discos de 200 GB foram anexados e o RAID de software md0 foi criado, com distribuição nesses cinco discos de dados do Azure.

![Repetir Olá mesmo backup de RAID de software com a distribuição em cinco anexado discos de dados de armazenamento do Azure standard](media/sap-hana-backup-file-level/image025.png)

Olá repetição mesmo backup de RAID de software com a distribuição em cinco anexados tempo de backup do armazenamento do Azure standard dados discos colocados Olá de 42 minutos para baixo too10 minutos. Olá discos foram anexados sem cache toohello VM. Portanto, é óbvio throughput de gravação de disco como importante é para o tempo de backup de saudação. Um poderia então comutador tooAzure premium armazenamento toofurther acelerar o processo de saudação para otimizar o desempenho. Em geral, o Armazenamento premium do Azure deve ser usado para sistemas de produção.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Copiar o armazenamento de BLOBs do SAP HANA arquivos de backup tooAzure

Como de dezembro de 2016, Olá melhor opção tooquickly repositório SAP HANA backup de arquivos é o armazenamento de BLOBs do Azure. Um único contêiner de blob tem um limite de 500 TB, suficiente para a maioria dos sistemas SAP HANA, em execução em uma VM GS5 no Azure, tookeep suficientes backups de SAP HANA. Os clientes têm a opção Olá entre &quot;hot&quot; e &quot;frios&quot; armazenamento de blob (consulte [armazenamento de BLOBs do Azure: Hot e interessantes camadas de armazenamento](../../../storage/blobs/storage-blob-storage-tiers.md)).

Com a ferramenta de blobxfer Olá, é fácil toocopy arquivos de backup do SAP HANA de saudação diretamente tooAzure armazenamento de blob.

![Aqui um pode ver os arquivos de saudação de um backup de arquivo completo do SAP HANA](media/sap-hana-backup-file-level/image026.png)

Aqui um verá Olá arquivos de um backup de arquivo completo do SAP HANA. Há quatro arquivos e uma maior hello tem aproximadamente 230 GB.

![Levou aproximadamente 3000 segundos contêiner de blob toocopy Olá GB 230 tooan padrão de armazenamento do Azure conta](media/sap-hana-backup-file-level/image027.png)

Não usando o hash md5 no teste inicial hello, levou aproximadamente 3000 segundos toocopy Olá GB 230 tooan padrão conta blob contêiner de armazenamento Azure.

![Esta captura de tela, um pode ver sua aparência no hello portal do Azure](media/sap-hana-backup-file-level/image028.png)

Nesta captura de tela, um pode ver sua aparência no hello portal do Azure. Um contêiner de blob denominado &quot;backups do sap hana&quot; foi criado e inclui blobs Olá quatro, que representam os arquivos de backup Olá SAP HANA. Um deles tem um tamanho de aproximadamente 230 GB.

console backup do HANA Studio Olá permite que um tamanho de arquivo máximo Olá toorestrict HANA dos arquivos de backup. No ambiente do exemplo hello, ele melhor desempenho, tornando possível toohave backup menor de vários arquivos, em vez de um arquivo grande de 230-GB.

![Definir o limite de tamanho do arquivo de backup Olá Olá HANA lado &#39; t melhorar o tempo de backup de saudação](media/sap-hana-backup-file-level/image029.png)

Definir o limite de tamanho do arquivo de backup Olá Olá HANA lado &#39; t melhorar o tempo de backup hello, porque os arquivos de saudação são gravados em sequência, conforme mostrado na figura. limite de tamanho de arquivo Hello foi definido too60 GB, para que backup Olá criou quatro arquivos de dados grandes, em vez da saudação 230-GB arquivo único.

![paralelismo de tootest da ferramenta de blobxfer hello, tamanho de arquivo máximo Olá para backups do HANA foi definido, em seguida, too15 GB](media/sap-hana-backup-file-level/image030.png)

paralelismo de tootest da ferramenta de blobxfer hello, tamanho de arquivo máximo Olá para backups do HANA foi definido, em seguida, too15 GB, o que resultou em 19 de arquivos de backup. Essa configuração trazidas de tempo de saudação blobxfer toocopy Olá GB 230 tooAzure armazenamento de blob de 3000 segundos para baixo too875 segundos.

Esse resultado é devido toohello limite de 60 MB/s para escrever um blob do Azure. Paralelismo por meio de vários blobs resolve afunilamento hello, mas há uma desvantagem: armazenamento de blob aumentando o desempenho de saudação blobxfer ferramenta toocopy todos esses tooAzure de arquivos de backup do HANA coloca carga Olá HANA VM e rede hello. Operação do sistema HANA fica afetada.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Cópia de blob de discos de dados do Azure dedicados no RAID do software de backup

Diferentemente Olá manual VM dados backup em disco, essa abordagem um não fazer backup de todos os discos de dados de saudação em uma VM toosave Olá SAP instalação completa, inclusive dados do HANA, HANA arquivos de log e arquivos de configuração. Em vez disso, ideia Olá é RAID de software toohave dedicado com distribuição entre vários VHDs de dados do Azure para armazenar um backup de arquivo completo do SAP HANA. Uma copia somente esses discos, que têm o backup do SAP HANA hello. Eles facilmente pode ser mantidos em uma conta de armazenamento de backup do HANA dedicada ou anexado tooa dedicado &quot;backup gerenciamento VM&quot; para processamento adicional.

![Todos os VHDs envolvidos foram copiados usando hello * * iniciar-azurestorageblobcopy * * comando do PowerShell](media/sap-hana-backup-file-level/image031.png)

Após Olá toohello backup local RAID de software foi concluída, todos os VHDs envolvidos foram copiados usando Olá **início azurestorageblobcopy** comando do PowerShell (consulte [AzureStorageBlobCopy início](/powershell/module/azure.storage/start-azurestorageblobcopy)). Como ela afeta apenas o sistema de arquivos dedicado de saudação para manter os arquivos de backup Olá, não há nenhum preocupações sobre a consistência do arquivo de dados ou de log do SAP HANA no disco hello. Uma vantagem desse comando é que ele funciona enquanto Olá VM permanece online. toobe certos de que nenhum processo grava o conjunto de backup distribuído de toohello, ser toounmount-se de que ele antes de saudação cópia de blob e montá-lo novamente mais tarde. Ou poderia ser usada uma apropriado muito&quot;congelar&quot; Olá sistema de arquivos. Por exemplo, via xfs\_congelar Olá XFS sistema de arquivos.

![Esta captura de tela mostra a lista de saudação de blobs no contêiner de vhds Olá em Olá portal do Azure](media/sap-hana-backup-file-level/image032.png)

Esta captura de tela mostra a lista de saudação de blobs em Olá &quot;vhds&quot; contêiner em Olá portal do Azure. captura de tela de saudação mostra Olá cinco VHDs, que foram anexados toohello SAP HANA server VM tooserve como Olá software RAID tookeep SAP HANA arquivos de backup. Ele também mostra Olá cinco cópias, que foram feitas por meio do comando de cópia de blob hello.

![Para fins de teste, cópias de saudação de discos RAID de software de backup de SAP HANA Olá foram anexados toohello VM do servidor de aplicativo](media/sap-hana-backup-file-level/image033.png)

Para fins de teste, cópias de saudação de discos RAID de software de backup de SAP HANA Olá foram anexados toohello VM do servidor de aplicativo.

![VM do servidor de aplicativo Hello foi desligado tooattach Olá disco cópias](media/sap-hana-backup-file-level/image034.png)

VM do servidor de aplicativo Hello foi desligado tooattach Olá disco cópias. Depois de iniciar Olá VM, discos hello e hello RAID detectados corretamente (montados por meio de UUID). Somente o ponto de montagem Olá estava ausente, que foi criado por meio de particionador de YaST hello. Depois cópias de backup de arquivo do SAP HANA Olá tornou-se visível no nível do sistema operacional.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Copiar arquivos de backup do SAP HANA tooNFS compartilhar

toolessen Olá impacto em Olá sistema SAP HANA de uma perspectiva de espaço em disco ou de desempenho, um pode considerar a armazenar os arquivos de backup Olá SAP HANA em um compartilhamento NFS. Tecnicamente, isso funciona, mas significa usando uma segunda VM do Azure como host de saudação da saudação de compartilhamento NFS. Não deve ser um pequeno tamanho da VM, devido a largura de banda de rede VM toohello. Faria sentido e tooshut para baixo isso &quot;backup VM&quot; e apenas exibi-la para executar o backup do SAP HANA hello. Gravar em um NFS compartilhamento coloca a carga na rede hello e impactos Olá sistema SAP HANA, mas simplesmente gerenciar Olá arquivos de backup posteriormente em Olá &quot;backup VM&quot; seria influencia sistema do SAP HANA hello.

![Um compartilhamento NFS de outra VM do Azure foi montado toohello VM do servidor de SAP HANA](media/sap-hana-backup-file-level/image035.png)

caso de uso tooverify Olá NFS, um compartilhamento NFS de outra VM do Azure VM do servidor SAP HANA toohello montado. Não havia um ajuste de NFS especial aplicado.

![Backup de saudação toodo 1 hora e 46 minutos levou diretamente](media/sap-hana-backup-file-level/image036.png)

compartilhamento NFS Olá era um conjunto de distribuição rápida, como Olá no servidor do SAP HANA hello. No entanto, ela levou 1 hora e saudação de toodo 46 minutos backup diretamente no compartilhamento NFS Olá em vez de 10 minutos, ao gravar o conjunto de distribuição local de tooa.

![alternativa de saudação não era muito mais rápida em 1 hora e 43 minutos](media/sap-hana-backup-file-level/image037.png)

alternativa de saudação de fazer um conjunto de distribuição local de backup tooa e copiando toohello de compartilhamento NFS no nível do sistema operacional (um simples **cp - avr** comando) não era muito mais rápida. Demorou 1 hora e 43 minutos.

Para que ele funciona, mas desempenho não era bom para teste de backup Olá 230 GB. Ficaria ainda pior para vários terabytes.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Copie o serviço de arquivo do SAP HANA arquivos de backup tooAzure

É possível toomount compartilhar um arquivo do Azure dentro de uma VM do Linux do Azure. artigo Olá [como toouse armazenamento de arquivo do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md) fornece detalhes sobre como toodo-lo. Tenha em mente de que há um limite de cota de 5 TB de um compartilhamento de arquivos do Azure e um limite de tamanho de arquivo de 1 TB por arquivo. Confira [Metas de desempenho e de escalabilidade do Armazenamento do Azure](../../../storage/common/storage-scalability-targets.md) para saber mais sobre os limites de armazenamento.

Os testes mostraram, no entanto, que o backup do SAP HANA não funciona diretamente no momento com esse tipo de montagem de CIFS. Também está declarado na [Nota SAP 1820529](https://launchpad.support.sap.com/#/notes/1820529) que o CIFS não é recomendado.

![Esta figura mostra um erro na caixa de diálogo backup no SAP HANA Studio Olá](media/sap-hana-backup-file-level/image038.png)

Esta figura mostra um erro na caixa de diálogo backup no Studio do HANA SAP, Olá durante a tentativa de tooback backup do compartilhamento de arquivos do Azure montado CIFS tooa diretamente. Para um tem toodo um backup SAP HANA padrão em um sistema de arquivos de máquina virtual pela primeira vez e, em seguida, os arquivos de backup de cópia de saudação de lá tooAzure serviço de arquivo.

![Esta figura mostra que levou sobre 929 segundos toocopy 19 SAP HANA arquivos de backup](media/sap-hana-backup-file-level/image039.png)

Esta figura mostra que levou sobre toocopy 929 segundos 19 arquivos de backup SAP HANA, com um tamanho total de aproximadamente 230 GB toohello do Azure do compartilhamento de arquivos.

![estrutura de diretórios de origem Olá na Olá SAP HANA VM foi copiado toohello compartilhamento de arquivos do Azure](media/sap-hana-backup-file-level/image040.png)

Nesta captura de tela, um pode ver a estrutura de diretórios de origem Olá na Olá SAP HANA VM foi copiado toohello compartilhamento de arquivos do Azure: um diretório (hana\_backup\_fsl\_15 gb) e arquivos de backup individuais 19.

Armazenar arquivos de backup do SAP HANA em arquivos do Azure pode ser uma opção interessante no futuro de saudação quando backups de arquivo do SAP HANA suportam diretamente. Ou, quando ele se torna possível toomount Azure arquivos por meio de NFS e o limite de cota máximo Olá é consideravelmente maior do que 5 TB.

## <a name="next-steps"></a>Próximas etapas
* [Guia de backup do SAP HANA nas Máquinas Virtuais do Azure](sap-hana-backup-guide.md) fornece uma visão geral e informações sobre como começar.
* [Backup do HANA SAP com base em instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descreve Olá armazenamento baseado em instantâneo opção de backup.
* toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md).
