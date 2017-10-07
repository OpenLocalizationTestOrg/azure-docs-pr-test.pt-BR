---
title: aaaAzure Linux VMs e armazenamento do Azure | Microsoft Docs
description: "Descreve o Armazenamento Standard e Premium do Azure e Managed Disks e Unmanaged Disks com máquinas virtuais Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Armazenamento de VM do Linux e do Azure
Armazenamento do Azure é uma solução de armazenamento de nuvem Olá para aplicativos modernos que dependem de durabilidade, disponibilidade e escalabilidade toomeet Olá de seus clientes.  Em adição toomaking-possível para os desenvolvedores toobuild aplicativos em larga escala toosupport novos cenários, o armazenamento do Azure também fornece Olá armazenamento base para máquinas virtuais do Azure.

## <a name="managed-disks"></a>Managed Disks

Máquinas virtuais do Azure agora estão disponível com [discos gerenciado do Azure](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), que permite que você toocreate suas VMs sem criar ou gerenciar qualquer [contas de armazenamento do Azure](../../storage/common/storage-introduction.md) por conta própria. Você especifica se deseja Premium ou padrão de armazenamento e disco de saudação quão grande devem ser e Azure cria Olá discos de VM para você. As máquinas virtuais com Managed Disks têm vários recursos importantes, incluindo:

- Suporte de dimensionamento automático. Azure cria discos hello e gerencia Olá toosupport de armazenamento subjacente para cima too10, 000 discos por assinatura.
- Maior confiabilidade com Conjuntos de Disponibilidade. O Azure garante que os discos de VM sejam isolados automaticamente uns dos outros em Conjuntos de Disponibilidade.
- Maior controle de acesso. Os Managed Disks expõem uma variedade de operações controladas pelo [RBAC (Controle de Acesso Baseado em Função do Azure)](../../active-directory/role-based-access-control-what-is.md).

Os preços dos Managed Disks são diferentes dos discos não gerenciados. Para obter essas informações, veja [Preços e cobrança para Managed Disks](../windows/managed-disks-overview.md#pricing-and-billing).

Você pode converter VMs existentes que usam discos não gerenciado toouse gerenciado discos com [az vm converter](/cli/azure/vm#convert). Para obter mais informações, consulte [como tooconvert uma VM do Linux de não discos tooAzure gerenciados discos](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Não é possível converter um disco não gerenciado em um disco gerenciado, se o disco não gerenciado hello está em uma conta de armazenamento, ou a qualquer momento foram, criptografada usando [criptografia de serviço de armazenamento do Azure (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). as etapas a seguir de saudação detalhes como tootooconvert não gerenciado em discos que estão, ou tem sido em uma conta de armazenamento criptografado:

- Copiar Olá virtual VHD (disco rígido) com [inicial de cópia de blob de armazenamento az](/cli/azure/storage/blob/copy#start) tooa conta de armazenamento que nunca tenha sido habilitada para criptografia de serviço de armazenamento do Azure.
- Crie uma VM que usa discos gerenciados e especifique este arquivo VHD durante a criação com [az vm create](/cli/azure/vm#create), ou
- Anexar Olá copiados VHD com [anexar disco de vm az](/cli/azure/vm/disk#attach) tooa executando VM com discos de gerenciado.


## <a name="azure-storage-standard-and-premium"></a>Armazenamento do Azure: Standard e Premium
As VMs do Azure - usando Managed Disks ou discos não gerenciados — podem ser criadas em discos de armazenamento standard ou em discos de armazenamento premium. Ao usar toochoose portal Olá sua VM, você deve alternar uma lista suspensa em Olá **Noções básicas de** tela tooview discos standard e premium. Quando alternado tooSSD, apenas armazenamento premium VMs habilitadas serão mostradas, todas com o apoio de SSD unidades.  Quando alternado tooHDD, VMs habilitadas para armazenamento padrão com o apoio de unidades de disco de rotação são mostrados, juntamente com o armazenamento premium VMs com o apoio de SSD.

Ao criar uma VM do hello `azure-cli` você pode escolher entre standard e premium, ao escolher o tamanho da VM Olá via Olá `-z` ou `--vm-size` sinalizador cli.

## <a name="creating-a-vm-with-a-managed-disk"></a>Criação de uma máquina virtual com um Managed Disk

exemplo a seguir Hello requer Olá 2.0 de CLI do Azure, que você pode [instalar aqui](/cli/azure/install-azure-cli).

Primeiro, crie uma saudação de toomanage do grupo de recursos de recursos com [criar grupo az](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Agora crie Olá VM com [criar vm az](/cli/azure/vm#create). Especifique um argumento `--public-ip-address-dns-name` exclusivo, pois `mypublicdns` provavelmente já está sendo usado.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

exemplo de Hello anterior cria uma VM com um disco gerenciado em uma conta de armazenamento padrão. Adicionar de toouse uma conta de armazenamento Premium Olá `--storage-sku Premium_LRS` argumento, como Olá exemplo a seguir:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Armazenamento Standard
Padrão de armazenamento do Azure é o tipo de padrão de saudação do armazenamento.  O Armazenamento Standard é econômico e, ainda assim, eficaz.  

## <a name="premium-storage"></a>Armazenamento Premium
O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho intensivas para entradas e saídas. Discos de VM (máquina virtual) que usam o armazenamento Premium armazenam dados em SSDs (unidades de estado sólido). Você pode migrar tooAzure de discos VM do seu aplicativo aproveita de tootake velocidade de saudação do armazenamento Premium e o desempenho desses discos.

Recursos de Armazenamento Premium:

* Discos de armazenamento Premium: Armazenamento Premium do Azure oferece suporte a discos VM que podem ser anexados tooDS, série DSv2 ou máquinas virtuais do Azure de série GS.
* Blob de página Premium: Armazenamento Premium oferece suporte a Blobs de página do Azure, que são usados toohold persistente discos para máquinas virtuais do Azure (VMs).
* O armazenamento redundante localmente Premium: Uma conta de armazenamento Premium oferece suporte apenas localmente redundante Storage (LRS) como a opção de replicação hello e mantém três cópias dos dados de saudação dentro de uma única região.
* [Armazenamento Premium](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>VMs com suporte do Armazenamento Premium
O Armazenamento Premium oferece suporte às VMs (Máquinas Virtuais) do Azure das séries DS, DSv2, GS e Fs. Você pode usar discos de armazenamento Standard e Premium com VMs que têm suporte do Armazenamento Premium. Mas não é possível usar discos de Armazenamento Premium com séries de VM que não são compatíveis com o Armazenamento Premium.

A seguir estão Olá distribuições do Linux que são validados com o armazenamento Premium.

| Distribuição | Versão | Kernel com suporte |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Armazenamento de arquivos do Azure
Armazenamento de arquivo do Azure oferece compartilhamentos de arquivos na nuvem hello usando o protocolo SMB padrão de saudação. Com os arquivos do Azure, você pode migrar aplicativos empresariais que se baseiam na tooAzure de servidores de arquivo. Os aplicativos em execução no Azure podem facilmente montar compartilhamentos de arquivos a partir das máquinas virtuais do Azure executando o Linux. E com a versão mais recente de saudação do armazenamento de arquivos, você também pode montar um compartilhamento de arquivos de um aplicativo local que dá suporte a SMB 3.0.  Como os compartilhamentos de arquivos são compartilhamentos do SMB, você pode acessá-los por meio de APIs standard do sistema de arquivos.

Armazenamento de arquivo é criado em Olá a mesma tecnologia que o armazenamento de Blob, tabela e fila, para que armazenamento de arquivos oferece disponibilidade hello, durabilidade, escalabilidade e redundância geográfica que baseia-se na plataforma de armazenamento do Azure hello. Para obter detalhes os destinos e os limites do desempenho do Armazenamento de arquivos, veja Escalabilidade e metas de desempenho do Armazenamento do Azure.

* [Como toouse armazenamento de arquivo do Azure com Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Armazenamento Dinâmico
camada de armazenamento ativa do Azure Olá é otimizada para armazenar dados acessados com frequência.  Armazenamento ativo é o tipo de armazenamento de padrão de saudação para repositórios de blob.

## <a name="cool-storage"></a>Armazenamento Estático
camada de armazenamento moderados do Azure Olá é otimizada para armazenar dados pouco acessados e vida longa. Alguns casos de uso de exemplo para armazenamento estático incluem backups, conteúdo de mídia, dados científicos, dados de conformidade e dados de arquivamento. Em geral, todos os dados raramente acessados serão candidatos perfeitos para o armazenamento estático.

|  | camada de armazenamento dinâmica | camada de armazenamento estática |
|:--- |:---:|:---:|
| Disponibilidade |99,9% |99% |
| Disponibilidade (leituras de RA-GRS) |99,99% |99,9% |
| Encargos de uso |Custos de armazenamento maiores |Custos de armazenamento menores |
| Menores custos |Maiores custos | |
| de acesso e de transação |de acesso e de transação | |

## <a name="redundancy"></a>Redundância
dados de saudação em sua conta de armazenamento é sempre do Microsoft Azure replicados tooensure durabilidade e alta disponibilidade, Olá SLA de armazenamento do Azure, mesmo em face de saudação de falhas de hardware transitória de reunião.

Quando você cria uma conta de armazenamento, você deve selecionar uma saudação as opções de replicação a seguir:

* Armazenamento com redundância local (LRS)
* Armazenamento com redundância de zona (ZRS)
* Armazenamento com redundância geográfica (GRS)
* Armazenamento com redundância geográfica com acesso de leitura (RA-GRS)

### <a name="locally-redundant-storage"></a>Armazenamento com redundância local
Armazenamento localmente redundante (LRS) replica seus dados na região de saudação em que você criou sua conta de armazenamento. toomaximize durabilidade, todas as solicitações feitas em relação aos dados na conta de armazenamento é replicada três vezes. Essas três réplicas residem em domínios de falha e domínios de atualização separados.  Uma solicitação retorna com êxito depois que ele foi escrito tooall três réplicas.

### <a name="zone-redundant-storage"></a>Armazenamento com redundância de zona
Armazenamento com redundância de zona (ZRS) replica seus dados em dois toothree instalações, em uma única região ou em duas regiões, fornecendo maior durabilidade do que o LRS. Se sua conta de armazenamento tiver o ZRS habilitado, então seus dados serão duráveis mesmo no caso de saudação de falha em uma das instalações de saudação.

### <a name="geo-redundant-storage"></a>Armazenamento com redundância geográfica
Armazenamento com redundância geográfica (GRS) replica seu dados tooa região secundária centenas de milhas de distância região primária hello. Se sua conta de armazenamento permitiu GRS, então seus dados serão duráveis mesmo no caso de saudação de uma interrupção regional completa ou um desastre no qual Olá região primária não é recuperável.

### <a name="read-access-geo-redundant-storage"></a>Armazenamento com redundância geográfica com acesso de leitura
Armazenamento com redundância geográfica com acesso de leitura (RA-GRS) maximiza a disponibilidade da sua conta de armazenamento, fornecendo dados de toohello acesso somente leitura no local secundário do hello, além de replicação toohello em duas regiões fornecidas por GRS. No caso de Olá dados ficarem indisponíveis na região primária hello, seu aplicativo pode ler dados de região secundária hello.

Para se aprofundar em redundância de armazenamento do Azure, consulte:

* [Replicação de Armazenamento do Azure](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Escalabilidade
Armazenamento do Azure é altamente escalonável, portanto você pode armazenar e processar centenas de terabytes de cenários de dados grandes de dados toosupport Olá exigidos pela análise científica financeiro e aplicativos de mídia. Ou você pode armazenar Olá pequenas quantidades de dados necessários para um site de pequenas empresas. Sempre que se enquadram às suas necessidades, você paga somente para dados Olá que estiver armazenando. O Armazenamento do Azure atualmente armazena dezenas de trilhões de objetos exclusivos de clientes e manipula milhões de solicitações por segundo em média.

Para contas de armazenamento standard: uma conta de armazenamento standard tem uma taxa de solicitação total máxima de 20.000 IOPS. Olá IOPS total em todos os discos da máquina virtual em uma conta de armazenamento padrão não deve exceder esse limite.

Para contas de armazenamento premium: uma conta de armazenamento premium tem uma taxa de transferência total máxima de 50 Gbps. taxa de transferência total em todos os discos VM saudação não deve exceder esse limite.

## <a name="availability"></a>Disponibilidade
Podemos garantir que pelo menos 99,99% (99,9% para a camada de acesso fria) de tempo de saudação, podemos com êxito será processar solicitações tooread dados de contas de armazenamento de redundância geográfica de acesso de leitura (RA-GRS), desde que a falha de tentativas tooread dados da região primária Olá são nova tentativa na região secundária hello.

Podemos garantir que pelo menos 99,9% (99% para a camada de acesso fria) de tempo de saudação, vamos com êxito processo solicita dados tooread de armazenamento localmente redundante (LRS), o armazenamento da redundância de zona (ZRS) e contas de armazenamento redundante da replicação geográfica (GRS).

Podemos garantir que pelo menos 99,9% (99% para a camada de acesso fria) de tempo de saudação, vamos com êxito processa solicitações toowrite dados tooLocally armazenamento redundante (LRS), zona redundante armazenamento (ZRS) e contas GRS (armazenamento) da redundância geográfica e redundância geográfica de acesso de leitura Contas de armazenamento (RA-GRS).

* [SLA do Azure para Armazenamento](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Regiões
Azure está disponível em 30 regiões mundo hello e anunciou planos para 4 regiões adicionais. Expansão geográfica é uma prioridade para o Azure porque ele permite nossos clientes tooachieve maior desempenho e suporte a seus requisitos e preferências de dados local.  Azures toolaunch mais recente de região está localizado na Alemanha.

Olá Microsoft Cloud Alemanha fornece uma opção diferenciados toohello Microsoft Cloud serviços já disponíveis na Europa, criando maiores oportunidades de inovação e crescimento econômico para altamente regulamentados parceiros e clientes na Alemanha, saudação (união) e hello da (EFTA-associação de livre comércio Europa).

Dados de cliente em datacenters esses novos, Magdeburg e Frankfurt, são gerenciados sob o controle de saudação de um objeto de confiança de dados, T sistemas internacionais, uma empresa alemão independente e subsidiária da Deutsche Telekom. Serviços de nuvem comercial da Microsoft nesses datacenters aderem regulamentações de manipulação de dados de tooGerman e oferecem aos clientes opções adicionais de como e onde os dados são processados.

* [Mapa de Regiões do Azure](https://azure.microsoft.com/regions/)

## <a name="security"></a>Segurança
Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança que juntos permitem que os desenvolvedores de aplicativos seguros toobuild. conta de armazenamento Olá em si pode ser protegida usando o controle de acesso baseado em função e o Active Directory do Azure. Os dados podem ser protegidos em trânsito, entre um aplicativo e o Azure usando a Criptografia do cliente, HTTPs ou SMB 3.0. Dados podem ser definidos toobe criptografado automaticamente quando gravados tooAzure armazenamento usando a criptografia de serviço de armazenamento (SSE). Sistema operacional e discos de dados usados por máquinas virtuais podem ser definidos toobe criptografado usando a criptografia de disco do Azure. Acesso delegado toohello objetos de dados no armazenamento do Azure podem ser concedidos usando assinaturas de acesso compartilhado.

### <a name="management-plane-security"></a>Segurança do plano de gerenciamento
plano de gerenciamento de saudação consiste Olá recursos usados toomanage sua conta de armazenamento. Nesta seção, falaremos sobre o modelo de implantação do Azure Resource Manager hello e como toocontrol de controle de acesso baseado em função (RBAC) toouse acessar tooyour contas de armazenamento. Também falaremos sobre como gerenciar as chaves de conta de armazenamento e como tooregenerate-los.

### <a name="data-plane-security"></a>Segurança do plano de dados
Nesta seção, vamos examinar permitir acesso a objetos de dados reais de toohello na sua conta de armazenamento, como arquivos, blobs, filas e tabelas, usando assinaturas de acesso compartilhado e políticas de acesso armazenado. Vamos abordar a SAS de nível de serviço e de nível de conta. Também veremos como toolimit acessar tooa endereço IP específico (ou intervalo de endereços IP), como o protocolo de saudação toolimit usado tooHTTPS e toorevoke uma assinatura de acesso compartilhado, sem esperar que ele tooexpire.

## <a name="encryption-in-transit"></a>Criptografia em trânsito
Esta seção discute como toosecure dados ao transferir para dentro ou fora do armazenamento do Azure. Falaremos sobre Olá recomendado o uso de criptografia de HTTPS e hello usado pelo SMB 3.0 para compartilhamentos de arquivos do Azure. Também, obtemos uma olhada na criptografia do lado do cliente, o que permite que você tooencrypt Olá dados antes que sejam transferidos para o armazenamento em um aplicativo cliente e dados de saudação toodecrypt depois que ela é transferida do armazenamento.

## <a name="encryption-at-rest"></a>Criptografia em repouso
Falaremos sobre criptografia de serviço de armazenamento (SSE), e como você pode habilitá-la para uma conta de armazenamento, resultando em seus blobs de bloco, blobs de página e acrescentar blobs sejam criptografados automaticamente quando gravados tooAzure armazenamento. Podemos também examinar como você pode usar a criptografia de disco do Azure e explorar diferenças básicas hello e casos de criptografia de disco versus SSE versus criptografia do lado do cliente. Examinaremos rapidamente a compatibilidade de FIPS com os computadores do governo norte-americano.

* [Guia de segurança do Armazenamento do Azure](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. disco temporário Olá fornece armazenamento de curto prazo para aplicativos e processos e dados de repositório tooonly desejado, como arquivos de paginação ou de permuta. Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando você [reimplantar uma VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante uma reinicialização padrão do hello VM, devem persistir os dados de saudação na unidade temporária hello.

Em máquinas virtuais Linux, o disco Olá normalmente é **/desenvolvimento/sdb** e é formatado e montado muito**/mnt** por Olá agente Linux do Azure. tamanho de saudação do disco temporário Olá varia de acordo com base no tamanho de saudação da máquina virtual de saudação. Para saber mais, confira [Tamanhos de máquinas virtuais do Linux](sizes.md).

Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Economia de custos
* [Custo de armazenamento](https://azure.microsoft.com/pricing/details/storage/)
* [Calculadora de custos de armazenamento](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Limites de armazenamento
* [Limites de Serviço de Armazenamento](../../azure-subscription-service-limits.md#storage-limits)
