---
title: aaaMigrating VMs tooAzure armazenamento Premium | Microsoft Docs
description: "Migre seu tooAzure de VMs armazenamento Premium existente. O Armazenamento Premium dá suporte ao disco de alto desempenho e baixa latência para cargas de trabalho que usam muita E/S em execução em máquinas virtuais do Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migrando tooAzure Premium armazenamento (discos não gerenciado)

> [!NOTE]
> Este artigo aborda como não gerenciado toomigrate uma VM que usa discos padrão não gerenciado tooa VM que usa discos premium. É recomendável que você use discos gerenciado do Azure para novas VMs e que você converta os discos de toomanaged anterior discos não gerenciado. Contas de armazenamento subjacentes do discos identificador Olá gerenciado para que você não precisa. Para saber mais, confira [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md) (Visão geral do Managed Disks).
>

O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho intensivas para entradas e saídas. Você pode tirar proveito de velocidade de saudação e o desempenho desses discos migrando tooAzure de discos VM do seu aplicativo armazenamento Premium.

Olá finalidade deste guia é toohelp novos usuários do armazenamento do Azure Premium melhor preparar toomake uma transição suave das sua tooPremium atual do sistema armazenamento. Guia de saudação endereços três componentes principais do hello nesse processo:

* [Planejar a migração de saudação tooPremium armazenamento](#plan-the-migration-to-premium-storage)
* [Preparar e cópia discos de rígidos virtuais (VHDs) tooPremium armazenamento](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Criar uma Máquina Virtual do Azure usando o Armazenamento Premium](#create-azure-virtual-machine-using-premium-storage)

Você pode migrar máquinas virtuais de outra plataformas tooAzure armazenamento Premium ou migrar máquinas virtuais do Azure existentes de armazenamento padrão tooPremium armazenamento. Este guia aborda as etapas para os dois cenários. Siga as etapas de saudação especificadas na seção de relevantes Olá dependendo do cenário.

> [!NOTE]
> Você pode encontrar uma visão geral de recursos e os preços do Armazenamento Premium em [Armazenamento Premium: Armazenamento de Alto Desempenho para Cargas de Trabalho de Máquina Virtual do Azure](storage-premium-storage.md). É recomendável migrar qualquer disco de máquina virtual que requerem alta IOPS tooAzure armazenamento Premium para obter melhor desempenho para o seu aplicativo hello. Se o disco não requer IOPS alta, você pode limitar os custos mantendo-a no armazenamento padrão, que armazena dados de disco da máquina virtual em HDDs (unidades de disco rígido) em vez de SSDs.
>

Concluir o processo de migração de saudação em sua totalidade pode exigir ações adicionais antes e após Olá etapas fornecidas neste guia. Exemplos incluem a configuração de redes virtuais ou pontos de extremidade ou fazer alterações de código no hello próprio aplicativo que podem exigir algum tempo de inatividade em seu aplicativo. Essas ações são aplicativo tooeach exclusivo e deve ser concluída junto com hello etapas fornecidas neste guia toomake Olá transição completa tooPremium armazenamento de maneira mais uniforme possível.

## <a name="plan-the-migration-to-premium-storage"></a>Planejar a migração de saudação tooPremium armazenamento
Esta seção garante que são toofollow pronto etapas de migração Olá neste artigo e o ajuda a toomake Olá melhor decisão sobre tipos de VM e disco.

### <a name="prerequisites"></a>Pré-requisitos
* Você também precisará de uma assinatura do Azure. Se você ainda não tiver uma, você poderá criar uma assinatura de [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) de um mês ou visitar [Preços do Azure](https://azure.microsoft.com/pricing/) para obter mais opções.
* tooexecute cmdlets do PowerShell, você precisará módulo do Microsoft Azure PowerShell hello. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para Olá instalar ponto e instruções de instalação.
* Quando você planejar toouse Azure VMs em execução no armazenamento Premium, você precisa toouse Olá VMs com capacidade de armazenamento Premium. Você pode usar discos de Armazenamento Standard e Premium com VMs compatíveis com o Armazenamento Premium. Discos de armazenamento Premium estarão disponíveis com mais tipos de VM Olá futuras. Para obter informações sobre todos os tamanhos e tipos de discos de VM do Azure disponíveis, veja [Tamanhos para máquinas virtuais](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Tamanhos para Serviços de Nuvem](../../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Considerações
Uma VM do Azure oferece suporte ao anexar vários discos de armazenamento Premium para que seus aplicativos podem ter até too256 TB de armazenamento por VM. Com o Armazenamento Premium, seus aplicativos podem atingir 80.000 IOPS (operações de entrada/saída por segundo) por VM e taxa de transferência de disco de 2.000 MB por segundo por VM com latências extremamente baixas para operações de leitura. Você tem opções de várias VMs e Discos. Esta seção é toohelp toofind uma opção mais adequada para sua carga de trabalho.

#### <a name="vm-sizes"></a>Tamanhos de VM
especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho. Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.

#### <a name="disk-sizes"></a>Tamanhos do disco
Há cinco tipos de discos que podem ser usados com a VM e cada um tem IOPs específicos e limites de taxa de transferência. Leve em consideração esses limites quando escolhendo o tipo de disco Olá para sua VM com base em necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho, e o horário de pico é carregado.

| Tipo de discos premium  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Tamanho do disco           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| IOPS por disco       | 500   | 2.300  | 5.000           | 7500           | 7500           | 
| Taxa de transferência por disco | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo |

Dependendo da carga de trabalho, determine se discos de dados adicionais são necessários para sua VM. Você pode anexar várias tooyour de discos de dados persistentes VM. Se necessário, você pode distribuir em capacidade de Olá Olá discos tooincrease e o desempenho do volume de saudação. (Veja o que é a distribuição de disco [aqui](storage-premium-storage-performance.md#disk-striping).) Se você distribuir discos de dados do Armazenamento Premium usando [Espaços de Armazenamento][4], deverá configurá-lo com uma coluna para cada disco usado. Caso contrário, hello geral desempenho do volume de saudação distribuída pode ser menor do que o esperado devido toouneven distribuição do tráfego entre os discos de saudação. Para VMs do Linux, você pode usar o hello *mdadm* tooachieve utilitário Olá mesmo. Consulte o artigo [Configurar o Software RAID no Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes.

#### <a name="storage-account-scalability-targets"></a>Metas de escalabilidade da conta de armazenamento
Contas de armazenamento Premium têm Olá seguintes metas de escalabilidade em adição toohello [escalabilidade do armazenamento do Azure e metas de desempenho](storage-scalability-targets.md). Se seus requisitos de aplicativo excederem os destinos de escalabilidade de saudação de uma única conta de armazenamento, criar várias contas de armazenamento de seu aplicativo toouse e particionar seus dados entre as contas de armazenamento.

| Capacidade total da conta | Largura de banda total para uma conta de armazenamento com redundância local |
|:--- |:--- |
| Capacidade de disco: 35 TB<br />Capacidade do instantâneo: 10 TB |Backup too50 gigabits por segundo para entrada + saída |

Para obter mais informações sobre as especificações de armazenamento Premium Olá a, check-out [escalabilidade e metas de desempenho ao usar o armazenamento Premium](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Política de cache de disco
Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM. Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo. Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo. configurações de cache de saudação para discos de dados existentes podem ser atualizadas usando [Portal do Azure](https://portal.azure.com) ou hello *- HostCaching* parâmetro hello *Set-AzureDataDisk* cmdlet.

#### <a name="location"></a>Local
Escolha um local onde o Armazenamento do Azure Premium está disponível. Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis. Máquinas virtuais localizadas em Olá mesmo região como Olá conta de armazenamento que armazena Olá discos para Olá VM dará melhor desempenho que se eles estão em regiões separadas.

#### <a name="other-azure-vm-configuration-settings"></a>Outras definições de configuração da VM do Azure
Ao criar uma VM do Azure, você será solicitado tooconfigure algumas de suas configurações. Lembre-se de que algumas configurações são fixas para tempo de vida de saudação do hello VM, enquanto você pode modificar ou adicionar outros mais tarde. Examine essas definições de configuração de máquina virtual do Azure e certifique-se de que eles são configurados apropriadamente toomatch seus requisitos de carga de trabalho.

### <a name="optimization"></a>Otimização
[Armazenamento Premium do Azure: design de alto desempenho](storage-premium-storage-performance.md) fornece diretrizes para criação de aplicativos de alto desempenho usando o Armazenamento Premium do Azure. Você pode seguir as diretrizes de saudação combinadas com desempenho melhores práticas aplicável tootechnologies usados pelo seu aplicativo.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparar e copiar os discos rígidos virtuais (VHDs) tooPremium armazenamento
Olá seção a seguir fornece diretrizes para preparar VHDs de sua VM e copiar VHDs tooAzure armazenamento.

* [Cenário 1: "Estou migrando tooAzure de máquinas virtuais do Azure existente armazenamento Premium."](#scenario1)
* [Cenário 2: "eu estou migrando VMs de outra plataformas tooAzure armazenamento Premium."](#scenario2)

### <a name="prerequisites"></a>Pré-requisitos
Olá tooprepare VHDs para migração, você precisará:

* Uma assinatura do Azure, uma conta de armazenamento e um contêiner em que o armazenamento de conta toowhich, você pode copiar o VHD. Observe que a conta de armazenamento de destino Olá pode ser uma conta de Standard ou Premium armazenamento dependendo do requisito.
* Saudação de toogeneralize uma ferramenta VHD se você planejar toocreate várias instâncias VM dele. Por exemplo, o sysprep para Windows ou o virt-sysprep para Ubuntu.
* Uma ferramenta tooupload Olá VHD arquivo toohello conta de armazenamento. Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) ou use um [Gerenciador de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Este guia descreve como copiar seu VHD usando a ferramenta de AzCopy hello.

> [!NOTE]
> Se você escolher a opção de cópia síncrona com AzCopy, para um desempenho ideal, copie o VHD executando uma dessas ferramentas em uma VM do Azure que está em Olá mesma região da conta de armazenamento de destino hello. Se você estiver copiando um VHD de uma VM do Azure em uma região diferente, o desempenho pode ser mais lento.
>
> Para copiar uma grande quantidade de dados pela largura de banda limitada, considere [usando Olá importação/exportação do Azure serviço tootransfer dados tooBlob armazenamento](../storage-import-export-service.md); Isso permite tootransfer seus dados por disco rígido de envio de unidades tooan do Azure Datacenter. Você pode usar o hello importação/exportação do Azure serviço toocopy dados tooa conta de armazenamento padrão somente. Dados saudação em sua conta de armazenamento padrão, você pode usar o hello [API de cópia de Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou conta de armazenamento do AzCopy tootransfer Olá dados tooyour premium.
>
> Observe que o Microsoft Azure dá suporte apenas a arquivos VHD de tamanho fixo. Os arquivos VHDX ou VHDs dinâmicos não têm suporte. Se você tiver um VHD dinâmico, você pode convertê-la toofixed tamanho usando Olá [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.
>
>

### <a name="scenario1"></a>Cenário 1: "Estou migrando tooAzure de máquinas virtuais do Azure existente armazenamento Premium."
Se você estiver migrando existente VMs do Azure, Olá parar VM, preparar VHDs por tipo de saudação do VHD que você deseja e copie Olá VHD com AzCopy ou o PowerShell.

Olá VM precisa toobe completamente inoperante toomigrate um estado limpo. Haverá um tempo de inatividade até a conclusão da migração de saudação.

#### <a name="step-1-prepare-vhds-for-migration"></a>Etapa 1. Preparar VHDs para migração
Se você estiver migrando tooPremium de máquinas virtuais do Azure existente armazenamento, o VHD pode ser:

* Uma imagem de sistema operacional generalizado
* Um disco de sistema operacional exclusivo
* Um disco de dados

Abaixo, percorremos estes três cenários para preparar o VHD.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Usar um toocreate VHD do sistema operacional generalizado várias instâncias VM
Se você estiver carregando um VHD que será usado toocreate várias instâncias de VM do Azure genéricas, você deve primeiro generalizar VHD usando um utilitário de sysprep. Isso se aplica a tooa VHD que é local ou na nuvem hello. O Sysprep remove todas as informações específicas de computador Olá VHD.

> [!IMPORTANT]
> Tire um instantâneo ou realize backup de sua VM antes de generalizá-lo. Em execução de sysprep será parar e desalocar a instância VM hello. Siga as etapas abaixo toosysprep um VHD do sistema operacional Windows. Observe que executar comando de Sysprep Olá exigirá você tooshut máquina virtual do hello. Para saber mais sobre o Sysprep, consulte [Visão Geral do Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou [Referência Técnica do Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Abra uma janela de Prompt de comando como administrador.
2. Digite hello tooopen comando Sysprep a seguir:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. No Olá, ferramenta de preparação do sistema, selecione Enter System Out-of-Box Experience (OOBE), Olá selecione caixa de seleção de generalizar, selecione **desligamento**e, em seguida, clique em **Okey**, conforme mostrado na imagem de saudação abaixo. O Sysprep será generalizar o sistema operacional de saudação e desligar o sistema de saudação.

    ![][1]

Para uma VM Ubuntu, use sysprep virt tooachieve Olá mesmo. Consulte [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) para obter mais detalhes. Consulte também alguns do código-fonte aberto Olá [software de provisionamento do servidor Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) para outros sistemas operacionais Linux.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Usar um toocreate de VHD do sistema operacional exclusivo uma única instância VM
Se você tiver um aplicativo em execução no hello VM que exige que os dados específicos de máquina hello, não generalize Olá VHD. Um VHD não generalizado pode ser usado toocreate uma instância exclusiva da máquina virtual do Azure. Por exemplo, se você tiver um Controlador de Domínio em seu VHD, executar o sysprep irá torná-lo inútil como um Controlador de Domínio. Revisar aplicativos Olá em execução no seu impacto VM e hello da execução de sysprep-los antes de generalizar Olá VHD.

##### <a name="register-data-disk-vhd"></a>Registrar o VHD do disco de dados
Se você tiver discos de dados no Azure toobe migrados, você deve fazer se VMs Olá que usam esses dados discos serão desligados.

Execute as etapas de saudação descritas abaixo toocopy VHD tooAzure armazenamento Premium e registrá-lo como um disco de dados provisionado.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Etapa 2. Criar hello de destino para o VHD
Crie uma conta de armazenamento para manter seus VHDs. Considere Olá pontos a seguir ao planejar onde toostore seus VHDs:

* destino de saudação conta de armazenamento Premium.
* local de conta de armazenamento Olá deve ser igual ao armazenamento Premium compatível com máquinas virtuais do Azure você criará no estágio final de saudação. Você poderá copiar a nova conta de armazenamento tooa ou saudação do plano toouse mesma conta de armazenamento com base em suas necessidades.
* Copiar e salvar chave de conta de armazenamento Olá Olá destino da conta de armazenamento para o próximo estágio de saudação.

Para discos de dados, você pode escolher tookeep alguns discos de dados em uma conta de armazenamento padrão (por exemplo, discos que têm mais armazenamento), mas é altamente recomendável que você mover todos os dados para o armazenamento de premium de toouse de carga de trabalho de produção.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Etapa 3. Copiar o VHD com o AzCopy ou o PowerShell
Você precisará toofind seu caminho do contêiner e a conta chave tooprocess qualquer uma dessas duas opções de armazenamento. A chave de conta de armazenamento e o caminho do contêiner podem ser encontrados em **Portal do Azure** > **Armazenamento**. URL do contêiner Olá será como "https://myaccount.blob.core.windows.net/mycontainer/".

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Opção 1: copiar um VHD com o AzCopy (cópia assíncrona)
Usando AzCopy, você pode carregar facilmente Olá VHD sobre Olá da Internet. Dependendo do tamanho de saudação do hello VHDs, isso pode levar tempo. Lembre-se de entrada/saída limites da conta de armazenamento toocheck Olá ao usar essa opção. Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.

1. Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)
2. Abra o PowerShell do Azure e vá toohello pasta onde AzCopy é instalado.
3. Comando a seguir de saudação usar arquivo VHD Olá toocopy de "Origem" muito "Destino".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Exemplo:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Aqui estão as descrições dos parâmetros de saudação usados em Olá AzCopy comando:

   * **/ Origem:  *&lt;fonte&gt;:***  local da pasta de saudação ou URL do contêiner de armazenamento que contém a saudação VHD.
   * **/ SourceKey:  *&lt;chave da conta de origem&gt;:***  chave de conta de armazenamento da conta de armazenamento de origem hello.
   * **/ Dest:  *&lt;destino&gt;:***  toocopy de URL do contêiner de armazenamento Olá VHD para.
   * **/ DestKey:  *&lt;chave da conta de destino&gt;:***  chave de conta de armazenamento da conta de armazenamento de destino hello.
   * **/ Padrão:  *&lt;nome de arquivo&gt;:***  especificar nome do arquivo hello de saudação VHD toocopy.

Para obter detalhes sobre como usar AzCopy ferramenta, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Opção 2: copiar um VHD com o PowerShell (cópia sincronizada)
Você também pode copiar o arquivo VHD hello usando o cmdlet do PowerShell Olá AzureStorageBlobCopy de início. Use Olá comando a seguir no Azure PowerShell toocopy VHD. Substitua valores hello <> com valores correspondentes da sua conta de armazenamento de origem e de destino. toouse esse comando, você deve ter um contêiner chamado vhds em sua conta de armazenamento de destino. Se o contêiner Olá não existir, crie um antes de executar o comando hello.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Exemplo:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Cenário 2: "eu estou migrando VMs de outra plataformas tooAzure armazenamento Premium."
Se você estiver migrando o VHD do Azure nuvem armazenamento tooAzure, você deve primeiro exportar pasta local do tooa Olá VHD. Tem caminho de origem completa de saudação do diretório local hello, onde o VHD é armazenado útil e, em seguida, usando AzCopy tooupload-tooAzure armazenamento.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Etapa 1. Exportar o diretório local do VHD tooa
##### <a name="copy-a-vhd-from-aws"></a>Copiar um VHD do AWS
1. Se você estiver usando AWS, exporte Olá EC2 instância tooa VHD em um bucket S3 da Amazon. Siga etapas Olá descritas Olá documentação do Amazon para ferramenta de interface de linha de comando (CLI) exportando instâncias do Amazon EC2 tooinstall Olá EC2 Amazon e execute o arquivo VHD Olá comando Criar-instância-export-tarefa tooexport Olá EC2 instância tooa. Ser toouse se **VHD** para Olá disco &#95; imagem &#95; Variável de formato ao executar Olá **criar-instância-export-tarefa** comando. Olá VHD arquivo exportado é salvo no bucket de saudação Amazon S3 que designar durante esse processo.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Baixe o arquivo VHD de saudação do bucket de S3 hello. Arquivo VHD de Select hello, em seguida, **ações** > **baixar**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Copiar um VHD de outra nuvem que não é do Azure
Se você estiver migrando o VHD do Azure nuvem armazenamento tooAzure, você deve primeiro exportar pasta local do tooa Olá VHD. Copiar o caminho do código-fonte completo saudação do diretório local hello, onde o VHD é armazenado.

##### <a name="copy-a-vhd-from-on-premises"></a>Copiar um VHD do local
Se você estiver migrando o VHD de um ambiente local, você precisará de caminho de origem completa Olá onde o VHD é armazenado. caminho de origem Olá pode ser um compartilhamento de arquivo ou local do servidor.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Etapa 2. Criar hello de destino para o VHD
Crie uma conta de armazenamento para manter seus VHDs. Considere Olá pontos a seguir ao planejar onde toostore seus VHDs:

* conta de armazenamento de destino Olá pode ser armazenamento standard ou premium, dependendo do requisito de aplicativo.
* região da conta de armazenamento Olá deve ser igual ao armazenamento Premium compatível com máquinas virtuais do Azure você criará no estágio final de saudação. Você poderá copiar a nova conta de armazenamento tooa ou saudação do plano toouse mesma conta de armazenamento com base em suas necessidades.
* Copiar e salvar chave de conta de armazenamento Olá Olá destino da conta de armazenamento para o próximo estágio de saudação.

É altamente recomendável que você mover todos os dados para o armazenamento de premium de toouse de carga de trabalho de produção.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Etapa 3. Carregar Olá VHD tooAzure armazenamento
Agora que você tem o VHD no diretório local hello, você pode usar AzCopy ou AzurePowerShell tooupload hello. vhd arquivo tooAzure armazenamento. Ambas as opções são fornecidas aqui:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Opção 1: Usando o arquivo. vhd do Azure PowerShell Add-AzureVhd tooupload Olá

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Um exemplo <Uri> pode ser ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***. Um exemplo <FileInfo> pode ser ***"C:\path\to\upload.vhd"***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Opção 2: Usando o arquivo. vhd do AzCopy tooupload Olá
Usando AzCopy, você pode carregar facilmente Olá VHD sobre Olá da Internet. Dependendo do tamanho de saudação do hello VHDs, isso pode levar tempo. Lembre-se de entrada/saída limites da conta de armazenamento toocheck Olá ao usar essa opção. Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.

1. Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)
2. Abra o PowerShell do Azure e vá toohello pasta onde AzCopy é instalado.
3. Comando a seguir de saudação usar arquivo VHD Olá toocopy de "Origem" muito "Destino".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Exemplo:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Aqui estão as descrições dos parâmetros de saudação usados em Olá AzCopy comando:

   * **/ Origem:  *&lt;fonte&gt;:***  local da pasta de saudação ou URL do contêiner de armazenamento que contém a saudação VHD.
   * **/ SourceKey:  *&lt;chave da conta de origem&gt;:***  chave de conta de armazenamento da conta de armazenamento de origem hello.
   * **/ Dest:  *&lt;destino&gt;:***  toocopy de URL do contêiner de armazenamento Olá VHD para.
   * **/ DestKey:  *&lt;chave da conta de destino&gt;:***  chave de conta de armazenamento da conta de armazenamento de destino hello.
   * **/ BlobType: página:** especifica esse destino Olá é um blob de página.
   * **/ Padrão:  *&lt;nome de arquivo&gt;:***  especificar nome do arquivo hello de saudação VHD toocopy.

Para obter detalhes sobre como usar AzCopy ferramenta, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Outras opções para carregar um VHD
Você também pode carregar uma conta de armazenamento de tooyour VHD usando uma saudação significa a seguir:

* [API do Blob da Cópia de Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Carregamento de Blobs do Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/)
* [Referência de API REST do Serviço de Importação/Exportação do Armazenamento](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> É recomendável usar o Serviço de Importação/Exportação se o tempo de carregamento estimado é de mais de sete dias. Você pode usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tempo de saudação da unidade de tamanho e a transferência de dados.
>
> Importação/exportação pode ser usado a conta de armazenamento padrão de tooa toocopy. Você precisará toocopy da conta de armazenamento toopremium de armazenamento padrão usando uma ferramenta como AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Criar máquinas virtuais do Azure usando o Armazenamento Premium
Após Olá VHD carregado ou copiado toohello desejado conta de armazenamento, siga as instruções de saudação em Olá de tooregister essa seção VHD como uma imagem do sistema operacional ou o disco do sistema operacional dependendo do cenário e, em seguida, criar uma instância de VM a partir dele. disco de dados Olá VHD pode ser anexado toohello VM depois que ela é criada.
Um exemplo de script de migração é fornecido no final desta seção hello. Este script simples não corresponde a todos os cenários. Talvez seja necessário tooupdate Olá script toomatch com seu cenário específico. toosee se este script se aplica a tooyour cenário, consulte abaixo [um exemplo de Script de migração](#a-sample-migration-script).

### <a name="checklist"></a>Lista de verificação
1. Aguarde até que todos os discos VHD Olá cópia seja concluída.
2. Certifique-se de que armazenamento Premium está disponível na região Olá que você está migrando.
3. Decida Olá nova VM série que usará. Ele deve ser uma capacidade de armazenamento Premium, e o tamanho de Olá deve ser dependendo da disponibilidade de saudação na região de saudação e com base em suas necessidades.
4. Decida o tamanho VM exato Olá que você usará. Tamanho da VM precisa toobe toosupport grande o suficiente Olá quantos discos de dados que você tem. Por exemplo Se você tiver 4 discos de dados, Olá VM deve ter de 2 ou mais núcleos. Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.
5. Crie uma conta de armazenamento Premium na região de destino hello. Esta é a conta de saudação você usará para Olá nova VM.
6. Ter Olá detalhes atuais de VM úteis, inclusive Olá lista de discos e blobs VHD correspondentes.

Prepare seu aplicativo para o tempo de inatividade. toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema. Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma. Duração do tempo de inatividade dependerá da quantidade de saudação de dados em Olá discos toomigrate.

> [!NOTE]
> Se você estiver criando uma VM do Azure Resource Manager de um disco especializado do VHD, consulte muito[este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para implantar o Gerenciador de recursos de VM usando o disco existente.
>
>

### <a name="register-your-vhd"></a>Registrar seu VHD
toocreate uma VM do VHD do sistema operacional ou tooattach um tooa de disco de dados nova VM, você deve primeiro registrá-los. Siga as etapas abaixo, dependendo do cenário do VHD.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizado VHD do sistema operacional toocreate várias instâncias de VM do Azure
Após a imagem do sistema operacional generalizada VHD é carregado toohello conta de armazenamento, registrá-lo como um **a imagem da VM do Azure** para que você possa criar uma ou mais instâncias VM dele. Olá tooregister de cmdlets do PowerShell a seguir ao Use o VHD como uma imagem de sistema operacional da VM do Azure. Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Copie e salve o nome de saudação dessa nova imagem de VM do Azure. O exemplo hello acima, é *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate de VHD do sistema operacional exclusivo uma única instância de VM do Azure
Após Olá exclusivo VHD do sistema operacional é carregado toohello armazenamento de conta, registrá-lo como um **disco do sistema operacional Azure** para que você possa criar uma instância de VM dele. Use esses tooregister de cmdlets do PowerShell seu VHD como um disco do sistema operacional do Azure. Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Copiar e salvar Olá nome desse novo disco de sistema operacional do Azure. O exemplo hello acima, é *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Toobe VHD do disco de dados anexado toonew instâncias de VM do Azure
Depois de hello VHD do disco de dados carregado toostorage conta, registre-o como um disco de dados do Azure de para que ele possa ser anexado tooyour nova série DS, série DSv2 série ou instância de VM do Azure série GS.

Use esses tooregister de cmdlets do PowerShell seu VHD como um disco de dados do Azure. Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Copiar e salvar Olá nome desse novo disco de dados do Azure. O exemplo hello acima, é *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Criar uma VM com capacidade de Armazenamento Premium
Uma vez Olá imagem do sistema operacional ou o disco do sistema operacional são registrados, crie uma nova série DS, série dsv2 ou série GS VM. Você irá usar imagem do sistema operacional hello ou nome de disco do sistema operacional que você registrou. Selecione o tipo VM de saudação da camada de armazenamento Premium Olá. No exemplo a seguir, estamos usando Olá *Standard_DS2* tamanho da VM.

> [!NOTE]
> Atualize toomake de tamanho de disco de saudação se que ele corresponde a sua capacidade e requisitos de desempenho e tamanhos de disco do Azure disponíveis hello.
>
>

Cmdlets do PowerShell seguem Olá passo a passo abaixo toocreate Olá nova VM. Primeiro, defina os parâmetros comuns de saudação:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

Primeiro, crie um serviço de nuvem em que você hospedará suas novas VMs.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Em seguida, dependendo do cenário, crie instância de VM do Azure Olá Olá imagem do sistema operacional ou disco do sistema operacional que você registrou.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizado VHD do sistema operacional toocreate várias instâncias de VM do Azure
Criar hello uma ou mais instâncias nova VM do Azure série DS usando Olá **imagem do sistema operacional Azure** registrado. Especifica esse nome de imagem do sistema operacional na configuração da VM Olá ao criar a nova VM conforme mostrado abaixo.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate de VHD do sistema operacional exclusivo uma única instância de VM do Azure
Criar uma nova instância de máquina virtual do Azure de série DS usando Olá **disco do sistema operacional Azure** registrado. Especifica esse nome de disco do sistema operacional na configuração da VM hello quando criar hello nova VM, conforme mostrado abaixo.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Especifique outras informações da VM do Azure, como um serviço de nuvem, região, conta de armazenamento, conjunto de disponibilidade e política de cache. Observe que a instância VM Olá deve estar localizada com sistema operacional associado ou Olá de discos de dados, para a conta de serviço, região e armazenamento de nuvem Olá selecionada deve estar no mesmo local que Olá subjacente VHDs desses discos.

### <a name="attach-data-disk"></a>Anexar disco de dados
Por fim, se você tiver registrado dados disco VHDs, anexá-los toohello nova VM do Azure compatíveis com armazenamento Premium.

Usar as seguintes PowerShell cmdlet tooattach dados disco toohello nova VM e especifique Olá política de cache. No exemplo a seguir Olá política de cache está definida muito*ReadOnly*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Pode haver toosupport necessárias etapas adicionais seu aplicativo não será coberto por este guia.
>
>

### <a name="checking-and-plan-backup"></a>Verificação e planejamento de backup
Uma vez Olá nova máquina virtual está ativo e em execução, usando Olá mesmo id de logon e senha de acesso é como Olá VM original e verificar se tudo está funcionando conforme o esperado. Todas as configurações de hello, inclusive volumes de saudação distribuído, estaria presentes no hello nova VM.

Olá última etapa é tooplan agendamento de backup e manutenção para Olá que nova VM com base nas necessidades do aplicativo hello.

### <a name="a-sample-migration-script"></a>Um script de migração de exemplo
Se você tiver várias toomigrate de VMs, automação por scripts do PowerShell poderão ser úteis. A seguir está um exemplo de script que automatiza a migração de saudação de uma VM. Observe que o script abaixo é apenas um exemplo e há algumas suposições feitas sobre discos de VM Olá atuais. Talvez seja necessário tooupdate Olá script toomatch com seu cenário específico.

suposições Olá são:

* Você está criando VMs clássicas do Azure.
* Seus Discos de origem do Sistema Operacional e Discos de Dados de origem estão na mesma conta de armazenamento e no mesmo contêiner. Se os discos de sistema operacional e discos de dados não estão no hello mesmo colocar, você pode usar AzCopy ou o Azure PowerShell toocopy VHDs em contas de armazenamento e contêineres. Consulte a etapa anterior toohello: [cópia VHD com AzCopy ou o PowerShell](#copy-vhd-with-azcopy-or-powershell). Editar este script toomeet seu cenário é outra opção, mas é recomendável usar AzCopy ou o PowerShell, pois ela é mais rápido e fácil.

script de automação de saudação é fornecido abaixo. Substitua o texto com suas informações e atualize Olá script toomatch com seu cenário específico.

> [!NOTE]
> Usar o script existente de saudação não preserva a configuração de rede de saudação do seu VM de origem. Você precisará toore-config as configurações de rede de saudação em suas VMs migrados.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Otimização
A configuração da VM atual pode ser personalizada especificamente toowork bem com discos padrão. Por exemplo, tooincrease Olá desempenho usando muitos discos em um volume distribuído. Por exemplo, em vez de usar 4 discos separadamente no armazenamento Premium, você poderá toooptimize capaz de custo de saudação fazendo com que um único disco. Otimizações de como esse toobe necessidade tratado caso a caso e exigem etapas personalizadas após a migração de saudação. Além disso, observe que esse processo não pode funcionar bem para bancos de dados e aplicativos que dependem do layout de disco Olá definida na configuração de saudação.

##### <a name="preparation"></a>Preparação
1. Olá Concluir migração simples, conforme descrito em Olá anteriormente nesta seção. Otimizações serão executadas no hello nova VM após a migração de saudação.
2. Defina Olá novos tamanhos de disco necessários para configuração de saudação otimizada.
3. Determine o mapeamento de saudação atual volumes/discos toohello novo disco de especificações de.

##### <a name="execution-steps"></a>Etapas de execução
1. Crie hello novos discos com os tamanhos corretos de saudação em Olá VM de armazenamento Premium.
2. Logon toohello VM e cópia Olá dados de saudação atual toohello novo disco de volume que mapeia toothat volume. Faça isso para todos os volumes de saudação atual que precisem toomap tooa novo disco.
3. Em seguida, alterar Olá aplicativo configurações tooswitch toohello novos discos e desanexar volumes antigos hello.

Para ajustar o aplicativo hello para melhorar o desempenho de disco, consulte muito[otimizando o desempenho do aplicativo](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migrações de aplicativos
Bancos de dados e outros aplicativos complexos podem exigir etapas especiais, conforme definido pelo provedor de saudação do aplicativo para a migração de saudação. Consulte a documentação do aplicativo toorespective. Por exemplo , normalmente, bancos de dados podem ser migrados por meio de backup e restauração.

## <a name="next-steps"></a>Próximas etapas
Consulte Olá recursos para cenários específicos para migrar máquinas virtuais a seguir:

* [Migrar Máquinas Virtuais do Azure entre as Contas de Armazenamento](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Criar e carregar um VHD do Windows Server tooAzure.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migração de máquinas virtuais do Amazon AWS tooMicrosoft do Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Além disso, consulte Olá recursos toolearn mais sobre o armazenamento do Azure e máquinas virtuais do Azure a seguir:

* [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Máquinas Virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
