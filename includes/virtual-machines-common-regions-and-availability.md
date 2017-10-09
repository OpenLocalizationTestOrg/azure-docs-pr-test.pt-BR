# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiões e disponibilidade para máquinas virtuais do Azure
Azure opera em vários data centers ao redor Olá, mundo. Esses datacenters estão agrupados em regiões toogeographic, dando a você a flexibilidade de escolher onde toobuild seus aplicativos. É importante toounderstand como e onde as máquinas virtuais (VMs) operar no Azure, juntamente com o desempenho de toomaximize opções, disponibilidade e redundância. Este artigo fornece uma visão geral da disponibilidade de saudação e recursos de redundância do Azure.

## <a name="what-are-azure-regions"></a>O que são as regiões do Azure?
Você cria recursos do Azure em regiões definidas, como “Oeste dos EUA”, “Europa Setentrional” ou “Sudeste Asiático”. Você pode examinar Olá [lista de regiões e seus locais](https://azure.microsoft.com/regions/). Dentro de cada região, vários datacenters existe tooprovide para redundância e disponibilidade. Essa abordagem oferece flexibilidade durante sua criação toomeet e usuários VMs tooyour mais próximos toocreate aplicativos qualquer conformidade legal, ou fins de imposto.

## <a name="special-azure-regions"></a>Regiões especiais do Azure
O Azure tem algumas regiões especiais que talvez seja conveniente toouse na criação de seus aplicativos para fins de conformidade e legais. Essas regiões especiais incluem:

* **Gov. EUA - Virgínia** e **Gov. EUA - Iowa**
  * Uma instância lógica e física do Azure isolada da rede, destinada a parceiros e órgãos do governo dos EUA, operada por cidadãos americanos selecionados. Inclui certificações de conformidade adicionais, como [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) e [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Leia mais sobre o [Azure Governamental](https://azure.microsoft.com/features/gov/).
* **Norte da China** e **Leste da China**
  * Essas regiões estão disponíveis por meio de uma parceria exclusiva entre a Microsoft e 21Vianet, no qual a Microsoft não diretamente mantém datacenters hello. Saiba mais sobre o [Microsoft Azure na China](http://www.windowsazure.cn/).
* **Centro da Alemanha** e **Nordeste Alemanha**
  * Essas regiões estão disponíveis por meio de um modelo de objeto de confiança de dados no qual os dados do cliente permanecem na Alemanha sob controle do T-Systems, uma empresa Deutsche Telekom, atuando como o objeto de confiança do hello dados alemão.

## <a name="region-pairs"></a>Pares de regiões
Cada região do Azure é emparelhado com outra região dentro de saudação mesmo geografia (por exemplo, EUA, Europa ou na Ásia). Essa abordagem permite para replicação de saudação de recursos, como armazenamento de máquina virtual em uma geografia que deve reduzir a probabilidade de saudação de desastres naturais, tumultos civis, quedas de energia ou interrupções de rede física que afetam as duas regiões de uma vez. Vantagens adicionais dos pares de regiões incluem:

* Em caso de saudação de uma interrupção do Azure mais amplo, uma região é priorizada fora de cada par toohelp reduzir Olá tempo toorestore para aplicativos. 
* Atualizações do Azure planejadas são distribuídas regiões toopaired um em um tempo de inatividade de toominimize de tempo e o risco de interrupção do aplicativo.
* Os dados continuam tooreside em hello mesmo geography como seu par (exceto o sul do Brasil) para fins de jurisdição de imposição de imposto e lei.

Exemplos de pares de regiões incluem:

| Primário | Secundário |
|:--- |:--- |
| Oeste dos EUA |Leste dos EUA |
| Norte da Europa |Europa Ocidental |
| Sudeste Asiático |Ásia Oriental |

Você pode ver Olá completo [lista de opções regionais pares aqui](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilidade de recursos
Alguns serviços ou recursos de VM estão disponíveis somente em determinadas regiões, como tamanhos específicos de VMs ou tipos de armazenamento. Também há alguns serviços globais do Azure que não exigem que você tooselect uma região específica, como [Active Directory do Azure](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), ou [DNS do Azure](../articles/dns/dns-overview.md). tooassist você na criação de seu ambiente de aplicativo, você pode verificar Olá [disponibilidade de serviços do Azure em cada região](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Disponibilidade de armazenamento
Noções básicas sobre regiões geográficas e regiões do Azure torna-se importante quando você considera Olá opções de replicação de armazenamento disponível. Dependendo do tipo de armazenamento hello, você tem opções de replicação diferentes.

**Azure Managed Disks**
* Armazenamento com redundância local (LRS)
  * Replica seus dados três vezes dentro de região de saudação em que você criou sua conta de armazenamento.

**Discos baseados em contas de armazenamento**
* Armazenamento com redundância local (LRS)
  * Replica seus dados três vezes dentro de região de saudação em que você criou sua conta de armazenamento.
* ZRS (Armazenamento com redundância de zona)
  * Replica seus dados três vezes em duas instalações toothree, dentro de uma única região ou em duas regiões.
* Armazenamento com redundância geográfica (GRS)
  * Replica seu dados tooa região secundária centenas de milhas de distância região primária hello.
* Armazenamento com redundância geográfica com acesso de leitura (RA-GRS)
  * Replica a região secundária do tooa de dados, assim como acontece com GRS, mas também fornece dados de toohello acesso somente leitura no local secundário hello.

Olá tabela a seguir fornece uma visão geral das diferenças de saudação entre tipos de replicação de armazenamento hello:

| Estratégia de replicação | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Os dados são replicados entre várias instalações. |Não |Sim |Sim |Sim |
| Dados podem ser lidos do local secundário hello e do local primário Olá. |Não |Não |Não |Sim |
| Número de cópias de dados mantidas em nós separados. |3 |3 |6 |6 |

Você pode ler mais sobre as [Opções de replicação de armazenamento do Azure aqui](../articles/storage/common/storage-redundancy.md). Para saber mais sobre discos gerenciados, veja [Visão geral dos Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Custos de armazenamento
Os preços variam dependendo do tipo de armazenamento de saudação e disponibilidade que você selecionar.

**Azure Managed Disks**
* Os Managed Disks Premium são compostos por unidades de estado sólido (SSDs) e os Managed Disks Standard são compostos por discos de rotação regular. Premium e Standard discos gerenciados são cobrados com base na capacidade de saudação provisionada para o disco de saudação.

**Discos não gerenciados**
* Armazenamento Premium é apoiado por Solid-State unidades (SSDs) e é cobrado com base na capacidade de saudação do disco de saudação.
* Padrão de armazenamento é apoiado por discos giratório regular e é cobrado com base na capacidade do hello em uso e desejado de disponibilidade de armazenamento.
  * Para RA-GRS, há uma taxa de transferência de dados de replicação geográfica adicional de largura de banda de saudação de replicação que tooanother dados região do Azure.

Consulte [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre opções de disponibilidade e Olá diferentes tipos de armazenamento de preço.

## <a name="availability-sets"></a>Conjuntos de disponibilidade
Um conjunto de disponibilidade é um agrupamento lógico de VMs que permite toounderstand do Azure como seu aplicativo é compilado tooprovide para redundância e disponibilidade. É recomendável que duas ou mais VMs são criadas dentro de um tooprovide de conjunto de disponibilidade para uma saudação altamente disponível do aplicativo e toomeet [99,95% do SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Quando uma única VM estiver usando [armazenamento Premium do Azure](../articles/storage/common/storage-premium-storage.md), Olá SLA do Azure se aplica a eventos de manutenção não planejada. 

Um conjunto de disponibilidade é composto de dois grupos adicionais que protegem contra falhas de hardware e permitem atualizações toosafely ser aplicado - (FDs) de domínios de falha e atualização (UDs) de domínios.

![Desenho conceitual da configuração de domínio Olá atualização falha e domínio](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Você pode ler mais sobre como toomanage Olá disponibilidade de [VMs do Linux](../articles/virtual-machines/linux/manage-availability.md) ou [VMs do Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domínios de falha
Um domínio de falha é um grupo lógico do hardware subjacente que compartilham uma fonte de alimentação comum e o comutador de rede, rack de tooa semelhante em um datacenter local. Como criar VMs em um conjunto de disponibilidade, Olá plataforma Windows Azure distribui automaticamente suas VMs entre esses domínios de falha. Essa abordagem limita o impacto de saudação de possíveis falhas de hardware físico, interrupções da rede ou interrupções de energia.

### <a name="update-domains"></a>Domínios de atualização
Um domínio de atualização é um grupo lógico do hardware subjacente que pode passar por manutenção ou ser reinicializado no hello simultaneamente. Como criar VMs em um conjunto de disponibilidade, hello plataforma Windows Azure distribui automaticamente suas VMs em esses domínios de atualização. Essa abordagem garante que pelo menos uma instância do seu aplicativo sempre permanece em execução como a plataforma Windows Azure hello sofre manutenção periódica. ordem de saudação de domínios de atualização está sendo reinicializado talvez não possa prosseguir sequencialmente durante a manutenção planejada, mas somente uma atualização de domínio é reinicializado por vez.

### <a name="managed-disk-fault-domains"></a>Domínios de falha de Disco Gerenciado
Para VMs que usam [Azure Managed Disks](../articles/virtual-machines/windows/faq-for-disks.md), as VMs são alinhadas aos domínios de falha de disco gerenciado quando usam um conjunto de disponibilidade gerenciada. Esse alinhamento garante que todos os Olá gerenciados discos anexado tooa VM estão dentro de saudação mesmo domínio de falha de disco gerenciado. Somente as VMs com discos gerenciados podem ser criadas em um conjunto de disponibilidade gerenciado. número de saudação de domínios de falha de disco gerenciado varia por região - duas ou três domínios de falha de disco gerenciado por região.

![FDs de disco gerenciado](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de saudação de domínios de falha para conjuntos de disponibilidade gerenciada varia por região - dois ou três por região. Olá tabela a seguir mostra o número de saudação por região

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Próximas etapas
Agora você pode iniciar toouse esses disponibilidade e redundância recursos toobuild seu ambiente do Azure. Para obter informações de práticas recomendadas, confira [Práticas recomendadas de disponibilidade do Azure](../articles/best-practices-availability-checklist.md).

