# <a name="azure-managed-disks-overview"></a>Visão geral do Azure Managed Disks

Discos gerenciado do Azure simplifica o gerenciamento de disco para as VMs de IaaS do Azure Gerenciando Olá [contas de armazenamento](../articles/storage/common/storage-introduction.md) associadas Olá discos VM. Tiver apenas o tipo de saudação toospecify ([Premium](../articles/storage/common/storage-premium-storage.md) ou [padrão](../articles/storage/common/storage-standard-storage.md)) e o tamanho de saudação do disco é necessário e Azure cria e gerencia disco Olá para você.

## <a name="benefits-of-managed-disks"></a>Benefícios dos discos gerenciados

Vamos dar uma olhada em alguns dos benefícios de saudação obter usando discos gerenciados, começando com este vídeo do Channel 9, [melhor resiliência de VM do Azure com discos gerenciados](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Implantação simples e escalonável de VM

Gerenciado lida com armazenamento de discos para você em segundo plano da saudação. Anteriormente, você precisava discos toocreate armazenamento contas toohold hello (arquivos VHD) para as VMs do Azure. Quando o dimensionamento para cima, você precisava toomake-se de que você criou contas de armazenamento adicional para não exceder o limite de IOPS de saudação do armazenamento com qualquer um dos seus discos. Com discos gerenciados tratamento de armazenamento, você não está limitado pela Olá limites da conta de armazenamento (como 20.000 IOPS / conta). Você também não tem mais toocopy suas contas de armazenamento toomultiple imagens personalizadas (arquivos VHD). Você pode gerenciá-los em um local central – uma conta de armazenamento por região do Azure – e usá-los toocreate centenas de VMs em uma assinatura.

Discos gerenciados permitirá toocreate backup too10, VM 000 **discos** em uma assinatura, que permitirá que você toocreate milhares de **VMs** em uma única assinatura. Esse recurso também aumenta a escalabilidade de saudação do [conjuntos de escala de máquina Virtual (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) , permitindo que você toocreate backup tooa mil VMs em um VMSS usando uma imagem do Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Maior confiabilidade para Conjuntos de disponibilidade

Discos gerenciados fornece maior confiabilidade para conjuntos de disponibilidade, assegurando que Olá discos de [VMs em um conjunto de disponibilidade](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) são suficientemente isolados uns aos outros tooavoid pontos únicos de falha. Ele faz isso colocando automaticamente discos Olá em unidades de escala de armazenamento diferente (carimbos). Se um carimbo falhar devido a falha de software ou toohardware, apenas as instâncias VM Olá com discos nesses carimbos falharem. Por exemplo, digamos que você tenha um aplicativo em execução em cinco VMs e Olá VMs estão em um conjunto de disponibilidade. Olá discos para essas VMs não todas ser armazenados em Olá mesmo carimbo, então se um carimbo cair, hello outras instâncias do aplicativo hello continuam toorun.

### <a name="highly-durable-and-available"></a>Altamente durável e disponível

Os Discos do Azure foram projetados para oferecer uma disponibilidade de 99,999%. Fique tranquilo sabendo que você tem três réplicas dos seus dados, o que proporciona alta durabilidade. Se as réplicas de um ou dois ainda tiver problemas, réplicas restantes Olá garantir persistência de dados e alta tolerância contra falhas. Esta arquitetura ajudou o Azure a proporcionar durabilidade de nível empresarial de modo consistente para os discos de IaaS, com uma taxa de falha anualizada líder do setor de ZERO POR CENTO. 

### <a name="granular-access-control"></a>Controle de acesso granular

Você pode usar [o Access RBAC (controle)](../articles/active-directory/role-based-access-control-what-is.md) tooassign de permissões específicas para um disco gerenciado tooone ou mais usuários. Gerenciado discos expõe uma variedade de operações, inclusive de leitura, gravação (criar/atualizar), delete e recuperar um [assinatura de acesso compartilhado (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) para disco hello. Você pode conceder acesso tooonly Olá operações que precisa de uma pessoa tooperform seu trabalho. Por exemplo, se não quiser que uma pessoa toocopy uma conta de armazenamento do disco gerenciado tooa, você pode escolher não toogrant acesso toohello exportação ação para esse disco gerenciado. Da mesma forma, se não quiser que uma pessoa toouse toocopy um URI SAS um disco gerenciado, você pode escolher não toogrant toohello essa permissão disco gerenciado.

### <a name="azure-backup-service-support"></a>Suporte de serviço do Backup do Azure
Use o serviço de Backup do Azure com discos gerenciados toocreate um trabalho de backup com backups baseados em tempo, fácil restauração de VM e políticas de retenção de backup. Discos gerenciados só oferecem suporte a armazenamento localmente redundante (LRS) como a opção de replicação Olá; Isso significa que ele mantém três cópias dos dados de saudação dentro de uma única região. Para a recuperação de desastre regional, é necessário fazer backup dos discos da VM em outra região usando o [serviço de Backup do Azure](../articles/backup/backup-introduction-to-azure-backup.md) e uma conta de armazenamento GRS como o cofre de backup. No momento Backup do Azure oferece suporte a tamanhos de disco de dados para cima too1TB para backup. Leia mais sobre isso em [Usando o serviço de Backup do Azure para VMs com o Managed Disks](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Preços e cobrança

Ao usar discos gerenciados, Olá cobrança considerações a seguir se aplicam:
* Tipo de armazenamento

* Tamanho do disco

* Número de transações

* Transferências de dados de saída

* Instantâneos do disco gerenciado (cópia completa do disco)

Vamos examinar esses itens com mais detalhes.

**Tipo de armazenamento:** o Managed Disks oferece dois níveis de desempenho: [Premium](../articles/storage/common/storage-premium-storage.md) (baseado em SSD) e [Standard](../articles/storage/common/storage-standard-storage.md) (baseado em disco rígido). cobrança de saudação de um disco gerenciado depende de qual tipo de armazenamento que você selecionou para o disco de saudação.


**Tamanho do disco**: cobrança para discos gerenciados depende de tamanho de saudação provisionado de disco hello. Mapas do Azure Olá toohello tamanho provisionado (arredondado) mais próximo da opção de discos gerenciados como especificado nas tabelas de saudação abaixo. Cada tooone de mapas de disco gerenciado de saudação provisionados tamanhos suportados e cobrada de acordo. Por exemplo, se você cria um disco gerenciado padrão e especificar um tamanho provisionado de 200 GB, você será cobrado de acordo com hello preços de saudação tipo S20 disco.

Aqui estão os tamanhos de disco Olá disponíveis para um disco gerenciado premium:

| **Tipo de Premium Managed <br>Disk** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Tamanho do disco        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Aqui estão os tamanhos de disco Olá disponíveis para um disco gerenciado padrão:

| **Tipo de Standard Managed <br>Disk** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Tamanho do disco        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Número de transações**: você será cobrado por número de saudação de transações que podem ser executadas em um disco gerenciado padrão. Não há custo para transações de um disco gerenciado premium.

**Transferências de dados de saída**: as [transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados saindo dos datacenters do Azure) incorrem em cobrança por uso de largura de banda.

Para obter informações detalhadas sobre os preços para Managed Disks, confira [Preços do Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Instantâneos de disco gerenciado

Um Instantâneo Gerenciado é uma cópia completa somente leitura de um disco gerenciado que, por padrão, é armazenado como um disco gerenciado padrão. Com os instantâneos, você pode fazer backup de seus discos gerenciados a qualquer momento. Esses instantâneos existem independentemente do disco de origem hello e podem ser usado toocreate novos discos gerenciado. Eles são cobrados com base no tamanho de saudação usado. Por exemplo, se você criar um instantâneo de um disco gerenciado com capacidade provisionada de 64 GB e o tamanho real de dados usados de 10 GB, instantâneo será cobrado apenas pelo Olá usado o tamanho de dados de 10 GB.  

[Instantâneos incrementais](../articles/virtual-machines/windows/incremental-snapshots.md) atualmente não há suporte para discos gerenciados, mas terá suporte em Olá futuras.

toolearn mais sobre como instantâneos toocreate com discos gerenciados, faça check-out desses recursos:

* [Criar cópia de VHD armazenado como um Disco Gerenciado usando instantâneos no Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Criar cópia de VHD armazenado como um Disco Gerenciado usando instantâneos no Linux](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Imagens

O Managed Disks também oferece suporte à criação de uma imagem personalizada gerenciada. Crie uma imagem de seu VHD personalizado em uma conta de armazenamento ou diretamente de uma VM generalizada (por meio do Sysprep). Isso captura em uma única imagem todos gerenciados discos associados a uma VM, incluindo Olá SO e discos de dados. Este permite a criação de centenas de VMs usando sua imagem personalizada sem Olá precisa toocopy ou gerenciar contas de armazenamento.

Para obter informações sobre a criação de imagens, faça check-out Olá artigos a seguir:
* [Como toocapture uma imagem gerenciada de uma VM generalizada no Azure](../articles/virtual-machines/windows/capture-image-resource.md)
* [Como toogeneralize e capturar uma máquina virtual Linux usando Olá 2.0 do CLI do Azure](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Imagens versus instantâneos

Geralmente, você vê palavra hello "imagem" com as máquinas virtuais e agora consulte "instantâneos" também. É importante toounderstand diferença de saudação entre estas. Com o Managed Disks, você pode capturar uma imagem de uma VM generalizada que foi desalocada. Esta imagem incluirá todas Olá discos anexados toohello VM. Você pode usar essa imagem toocreate uma nova VM e incluirá todos os discos de saudação.

Um instantâneo é uma cópia de um disco no ponto de saudação tempo é necessário. Só se aplica a disco tooone. Se você tiver uma VM que tenha apenas um disco (Olá SO), você pode tirar um instantâneo ou uma imagem dele e criar uma VM do instantâneo hello ou imagem hello.

E se uma VM tiver cinco discos e eles estiverem distribuídos? Você pôde tirar um instantâneo de cada um dos discos de saudação, mas não há nenhum conhecimento sobre na Olá VM de estado de saudação de discos hello – instantâneos Olá conhecem apenas se um disco. Nesse caso, instantâneos de saudação precisaria toobe coordenado entre si e que não é suportada atualmente.

## <a name="managed-disks-and-encryption"></a>Managed Disks e criptografia

Há dois tipos de criptografia toodiscuss em discos de toomanaged de referência. Olá primeiro um é criptografia de serviço de armazenamento (SSE), que é executada pelo serviço de armazenamento de saudação. Olá, um segundo é criptografia de disco do Azure, que você pode habilitar em hello SO e discos de dados para suas VMs.

### <a name="storage-service-encryption-sse"></a>SSE (Criptografia do Serviço de Armazenamento)

[Criptografia do serviço de armazenamento do Azure](../articles/storage/common/storage-service-encryption.md) fornece criptografia em repouso e proteger seu dados toomeet seus compromissos de segurança e conformidade organizacionais. SSE está habilitado por padrão para todos os discos gerenciados, instantâneos e imagens em todas as regiões de saudação em discos gerenciados está disponível. Começando em 10 de junho de 2017, todos os novos gerenciados imagens/de instantâneos de discos e novos dados gravados discos tooexisting gerenciado são automaticamente criptografados em repouso com chaves gerenciadas pelo Microsoft.  Visite Olá [página de perguntas Frequentes de discos gerenciados](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) para obter mais detalhes.


### <a name="azure-disk-encryption-ade"></a>ADE (Azure Disk Encryption)

Criptografia de disco do Azure permite que você tooencrypt Olá SO e discos de dados usados por uma máquina Virtual IaaS. Isso inclui discos gerenciados. Para Windows, Olá unidades são criptografadas usando a tecnologia de criptografia do BitLocker padrão da indústria. Para o Linux, discos de saudação são criptografados usando a tecnologia de saudação DM Crypt. Isso é integrado com o Azure Key Vault tooallow você toocontrol e gerenciar chaves de criptografia de disco hello. Para obter mais informações, consulte [Azure Disk Encryption para VMs IaaS Windows e Linux](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre discos gerenciados, consulte toohello artigos a seguir.

### <a name="get-started-with-managed-disks"></a>Introdução aos Discos Gerenciados

* [Criar uma VM do Windows usando o Gerenciador de Recursos e o PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Criar uma VM do Linux usando Olá 2.0 do CLI do Azure](../articles/virtual-machines/linux/quick-create-cli.md)

* [Anexar um disco de dados gerenciado tooa VM do Windows usando o PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Adicionar um disco gerenciado de tooa VM do Linux](../articles/virtual-machines/linux/add-disk.md)

* [Scripts de exemplo do PowerShell de discos gerenciados](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Utilizar o Managed Disks nos modelos do Azure Resource Manager](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Comparar as opções de armazenamento de Managed Disks

* [Discos e armazenamento Premium](../articles/storage/common/storage-premium-storage.md)

* [Discos e armazenamento Standard](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>Diretrizes operacionais

* [Migrar de outras plataformas e AWS tooManaged discos no Azure](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Converta os discos de toomanaged de máquinas virtuais do Azure no Azure](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
