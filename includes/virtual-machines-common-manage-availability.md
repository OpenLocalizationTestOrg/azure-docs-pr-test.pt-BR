## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Entender as reinicializações de VM - manutenção vs. tempo de inatividade
Há três cenários que podem levar a máquina toovirtual no Azure que está sendo afetado: manutenção de hardware não planejado, o tempo de inatividade inesperado e, a manutenção planejada.

* **Evento de manutenção de Hardware não planejado** ocorre quando hello plataforma Windows Azure prevê hardware hello ou qualquer plataforma componente associado tooa máquina física, é sobre toofail. Quando a plataforma Olá prevê uma falha, ele emitirá um hardware não planejado manutenção evento tooreduce Olá impacto toohello máquinas virtuais hospedadas em hardware. O Azure usa Olá toomigrate tecnologia migração ao vivo máquinas virtuais de saudação falhando máquina física íntegra do tooa do hardware. Migração ao vivo é uma VM preservação de operação que só pausa Olá Máquina Virtual por um curto período. Memória, arquivos abertos e conexões de rede são mantidas, mas o desempenho pode ser reduzido antes e/ou após o evento de saudação. Em casos em que a migração ao vivo não pode ser usada, Olá VM enfrentam um tempo de inatividade inesperado, conforme descrito abaixo.


* **Um tempo de inatividade inesperado** raramente ocorre quando o hardware de saudação ou infraestrutura física hello, sua máquina virtual subjacente apresentou falha de alguma forma. Isso inclui falhas na rede local, falhas no disco local ou outras falhas no nível de rack. Quando uma falha é detectada, hello plataforma Windows Azure migra automaticamente (repara) seu tooa de máquina virtual Íntegro máquina física. Experiência de tempo de inatividade (reinicialização) durante a saudação procedimento de recuperação, máquinas virtuais e na perda de alguns casos de unidade temporária hello. Olá anexado SO e discos de dados são sempre preservados. 

* **Eventos de manutenção de planejado** atualizações periódicas feitas pela Microsoft toohello subjacente tooimprove da plataforma Windows Azure geral confiabilidade, desempenho e segurança da infraestrutura de plataforma Olá que suas máquinas virtuais executadas em. A maioria dessas atualizações é realizada sem nenhum impacto nas suas Máquinas Virtuais ou nos Serviços de Nuvem (veja [Manutenção de preservação da VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Embora Olá plataforma Windows Azure tentativas toouse manutenção preservando VM em todas as ocasiões possíveis, há casos raros quando essas atualizações exigem uma reinicialização da máquina virtual tooapply Olá atualizações necessárias toohello infra-estrutura subjacente. Nesse caso, você pode executar a manutenção planejada do Azure com a operação de reimplantação de manutenção iniciando manutenção Olá para suas VMs na janela de tempo adequado do hello. Para saber mais, veja [Manutenção planejada para máquinas virtuais](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


impacto de saudação tooreduce de tempo de inatividade devido tooone ou mais desses eventos, recomendamos Olá seguir as práticas recomendadas de alta disponibilidade para as máquinas virtuais:

* [Configurar diversas máquinas virtuais em um conjunto de disponibilidade para redundância]
* [Como usar discos gerenciados para VMs em um conjunto de disponibilidade]
* [Usar eventos agendados tooproactively resposta tooVM afetando eventos] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configurar cada camada de aplicativo em conjuntos de disponibilidade separados]
* [Combinar o balanceador de carga com os conjuntos de disponibilidade]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configurar diversas máquinas virtuais em um conjunto de disponibilidade para redundância
aplicativo de tooyour do tooprovide redundância, é recomendável agrupar duas ou mais máquinas virtuais em um conjunto de disponibilidade. Essa configuração garante que, durante a um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual está disponível e atende Olá 99,95% do SLA do Azure. Para obter mais informações, consulte Olá [SLA para máquinas virtuais](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Evite deixar uma única máquina virtual sozinha em um conjunto de disponibilidade. Máquinas virtuais nesta configuração não se qualificam para uma garantia de SLA e enfrentam tempo de inatividade durante eventos de manutenção planejada do Azure, exceto quando estiver usando uma única VM [armazenamento Premium do Azure](../articles/storage/common/storage-premium-storage.md). Para VMs individuais usando o armazenamento premium, Olá SLA do Azure se aplica.

Cada máquina virtual em seu conjunto de disponibilidade é atribuída um **domínio de atualização** e um **domínio de falha** por Olá subjacente a plataforma Windows Azure. Para um conjunto de disponibilidade específico, cinco domínios de atualização não-configuráveis pelo usuário são atribuídos por padrão (implantações do Gerenciador de recursos podem ser aumentada tooprovide too20 domínios de atualização) tooindicate grupos de máquinas virtuais e físicos subjacentes que pode ser reinicializado no hello simultaneamente. Quando mais de cinco máquinas virtuais são configuradas em um único conjunto de disponibilidade, Olá sexto máquina de virtual é colocada no hello mesmo atualização domínio como máquina virtual da primeira hello, hello sétima em Olá que mesmo domínio de atualização como Olá segunda máquina virtual e, portanto no. ordem de saudação de domínios de atualização está sendo reinicializado talvez não possa prosseguir sequencialmente durante a manutenção planejada, mas somente uma atualização de domínio é reinicializado por vez. Um domínio de atualização reinicializada recebe toorecover 30 minutos antes de manutenção é iniciada em um domínio de atualização diferentes.

Domínios de falha definem o grupo de saudação de máquinas virtuais que compartilham um comutador de origem e de rede de alimentação comum. Por padrão, as máquinas virtuais de saudação configuradas em seu conjunto de disponibilidade estiverem separadas em domínios de falha de toothree para implantações do Gerenciador de recursos (dois domínios de falha para clássico). Ao colocar as máquinas virtuais em um conjunto de disponibilidade não protege o aplicativo de sistema operacional ou falhas específicas do aplicativo, ele limitar o impacto de saudação de possíveis falhas de hardware físico, interrupções da rede ou interrupções de energia.

<!--Image reference-->
   ![Desenho conceitual da configuração de domínio Olá atualização falha e domínio](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Usar discos gerenciados para VMs no conjunto de disponibilidade
Se você estiver usando máquinas virtuais com discos não gerenciados, é altamente recomendável [converter VMs no conjunto de disponibilidade toouse gerenciados discos](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Discos gerenciado](../articles/virtual-machines/windows/managed-disks-overview.md) oferecem maior confiabilidade para conjuntos de disponibilidade, assegurando que os discos de saudação de VMs em um conjunto de disponibilidade são suficientemente isolados uns dos outros pontos de falha únicos tooavoid. Ele faz isso colocando automaticamente discos Olá em clusters de armazenamento diferente. Se um cluster de armazenamento falhar devido a falha de software ou toohardware, apenas as instâncias VM Olá com discos nesses carimbos falharem.

![FDs de disco gerenciado](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de saudação de domínios de falha para conjuntos de disponibilidade gerenciada varia por região - dois ou três por região. Olá tabela a seguir mostra o número de saudação por região

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Se você planejar toouse VMs com [não gerenciado discos](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), abaixo de práticas recomendadas para contas de armazenamento onde os discos rígidos virtuais (VHDs) de máquinas virtuais são armazenados como [blobs de página](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Manter todos os discos (sistema operacional e dados) associados a uma VM em Olá mesma conta de armazenamento**
2. **Saudação de revisão [limites](../articles/storage/common/storage-scalability-targets.md) no número de saudação de discos não gerenciados em uma conta de armazenamento** antes de adicionar mais contas de armazenamento de tooa VHDs
3. **Use uma conta de armazenamento distinta para cada VM em um conjunto de disponibilidade.** Não compartilhe contas de armazenamento com várias VMs em Olá mesmo conjunto de disponibilidade. É aceitável para máquinas virtuais em diferentes contas de armazenamento tooshare conjuntos de disponibilidade se forem seguidas acima práticas recomendadas

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configurar cada camada de aplicativo em conjuntos de disponibilidade separados
Se as máquinas virtuais são todos quase idênticas e servir Olá mesmo finalidade para seu aplicativo, é recomendável que você configure uma conjunto de disponibilidade para cada camada do aplicativo.  Se você colocar duas diferentes camadas em Olá mesmo conjunto de disponibilidade, todas as máquinas virtuais Olá mesma camada de aplicativo pode ser reinicializada ao mesmo tempo. Ao configurar ao menos duas máquinas virtuais no conjunto de disponibilidade de cada camada, você garante que ao menos uma máquina virtual de cada camada estará disponível.

Por exemplo, você pode colocar todas as máquinas virtuais de saudação no front-end do seu aplicativo executando o IIS, Apache, Nginx em um único conjunto de disponibilidade hello. Certifique-se de que somente as máquinas virtuais front-end são colocadas em Olá mesmo conjunto de disponibilidade. Da mesma forma, certifique-se de que apenas as máquinas virtuais de camadas de dados sejam colocadas no seu próprio conjunto de disponibilidade, como as máquinas virtuais do SQL Server ou suas máquinas virtuais do MySQL.

<!--Image reference-->
   ![Camadas de aplicativo](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combinar o balanceador de carga com os conjuntos de disponibilidade
Combinar Olá [balanceador de carga do Azure](../articles/load-balancer/load-balancer-overview.md) com uma disponibilidade definido tooget hello mais resiliência do aplicativo. Olá balanceador de carga do Azure distribui o tráfego entre várias máquinas virtuais. Para nosso máquinas virtuais de camada padrão, Olá balanceador de carga do Azure é incluído. Nem todos os níveis de máquina virtual incluem hello balanceador de carga do Azure. Para saber mais sobre o balanceamento de carga de suas máquinas virtuais, confira [Balanceamento de Carga em máquinas virtuais](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Se o balanceador de carga Olá não estiver configurado toobalance tráfego entre várias máquinas virtuais, qualquer evento de manutenção planejada afeta Olá somente servidores de tráfego máquina virtual, causando uma camada de aplicativo de tooyour de interrupção. Colocar várias máquinas virtuais de saudação mesmo nível em Olá mesmo balanceador de carga e disponibilidade conjunto permite tráfego toobe continuamente servidas pelo menos uma instância.


<!-- Link references -->
[Configurar diversas máquinas virtuais em um conjunto de disponibilidade para redundância]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configurar cada camada de aplicativo em conjuntos de disponibilidade separados]: #configure-each-application-tier-into-separate-availability-sets
[Combinar o balanceador de carga com os conjuntos de disponibilidade]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Como usar discos gerenciados para VMs em um conjunto de disponibilidade]: #use-managed-disks-for-vms-in-an-availability-set
