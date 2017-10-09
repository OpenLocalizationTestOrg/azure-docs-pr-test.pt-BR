Azure executa periodicamente atualizações tooimprove Olá confiabilidade, desempenho e segurança da infraestrutura de host Olá para máquinas virtuais. Essas atualizações variam de componentes de software em Olá hospedagem ambiente (como o sistema operacional, hipervisor e vários agentes implantados no host de saudação), a aplicação de patch atualizar componentes de rede, toohardware encerramento. maioria de saudação essas atualizações são executadas sem todas as máquinas virtuais impacto toohello hospedado. No entanto, há casos em que as atualizações possuem um impacto:

- Se a manutenção de saudação não exigir uma reinicialização, o Azure usa Olá toopause de migração in-loco VM enquanto Olá host é atualizado.

- Se manutenção requer uma reinicialização, você receberá um aviso de quando Olá manutenção está planejada. Nesses casos, você também terá uma janela de tempo, onde você pode iniciar manutenção Olá por conta própria, cada vez que funciona para você.

Esta página descreve como o Microsoft Azure executa os dois tipos de manutenção. Para obter mais informações sobre eventos não planejados (interrupções), consulte gerenciar disponibilidade de saudação de máquinas virtuais para [Windows] (... / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).

Aplicativos em execução em uma máquina virtual podem reunir informações sobre as atualizações futuras usando hello Azure serviço de metadados para [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) ou [Linux] (... / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migração de VM local

Quando as atualizações não exigem uma reinicialização completa, uma migração ao vivo local é usada. Durante a atualização de saudação Olá VM está em pausa por aproximadamente 30 segundos, preservando memória RAM, Olá enquanto Olá ambiente de hospedagem aplica patches e atualizações necessárias hello. máquina virtual de saudação é retomada e relógio Olá da máquina virtual de saudação é sincronizado automaticamente.

Para VMs em conjuntos de disponibilidade, os domínios de atualização são atualizados um de cada vez. Todas as VMs em um domínio de atualização (UD) está em pausa, atualizadas e retomadas antes da manutenção planejada prossegue toohello UD Avançar.

Alguns aplicativos podem ser afetados por esses tipos de atualizações. Aplicativos que executam em tempo real de processamento de eventos, como o streaming de mídia ou transcodificação ou alta taxa de transferência de rede cenários, não podem ser projetado tootolerate 30 segundo intervalo. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Manutenção que exige uma reinicialização

Quando precisarem de VMs toobe reinicializado para manutenção planejada, você será notificado com antecedência. Manutenção planejada tem duas fases: Olá janela pessoal e uma janela de manutenção agendada.

Olá **janela autoatendimento** permite que você iniciar a manutenção de saudação em suas VMs. Durante esse tempo, você pode consultar cada VM toosee seu status e verificar o resultado de saudação de sua última solicitação de manutenção.

Quando você inicia a manutenção de autoatendimento, sua VM é nó movido tooa que já tenha sido atualizada e liga novamente. Como Olá VM for reinicializado, disco temporário Olá for perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados.

Se você iniciar a manutenção de autoatendimento e há um erro durante o processo de hello, Olá operação é interrompida, hello VM não é atualizada e ele também é removido do hello planejado iteração de manutenção. Você será contatado em um momento posterior com uma nova agenda e oferecida uma nova oportunidade toodo autoatendimento manutenção. 

Quando a janela de autoatendimento de saudação tiver passado, Olá **janela de manutenção agendada** começa. Durante essa janela de tempo, você pode ainda consultar para a janela de manutenção hello, mas deixará de ser capaz de toostart manutenção de saudação por conta própria.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerações sobre disponibilidade durante a manutenção planejada 

Se você decidir toowait até Olá planejado janela de manutenção, há alguns tooconsider coisas para manter a disponibilidade mais alta Olá das suas máquinas virtuais. 

### <a name="paired-regions"></a>Regiões emparelhadas

Cada região do Azure é emparelhado com outra região dentro de saudação mesmo geografia, junto, eles fazer um par regional. Durante a manutenção planejada, o Azure atualizará apenas Olá VMs em uma única região de um par de região. Por exemplo, ao atualizar Olá máquinas virtuais no Centro Norte dos EUA, Azure não atualizará todas as máquinas virtuais no Centro Sul dos EUA em Olá simultaneamente. No entanto, outras regiões como Norte da Europa pode estar em manutenção no hello mesmo tempo como Leste dos EUA. Noções básicas sobre como funcionam os pares de região podem ajudá-lo a melhor distribuir suas VMs entre regiões. Para obter mais informações, consulte [pares de regiões do Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Conjuntos de disponibilidade e conjuntos de dimensionamento

Ao implantar uma carga de trabalho em VMs do Azure, você pode criar VMs hello dentro de um aplicativo de tooyour disponibilidade conjunto tooprovide alta disponibilidade. Isso garante que, durante uma interrupção ou eventos de manutenção, pelo menos uma máquina virtual estará disponível.

Em um conjunto de disponibilidade, VMs individuais são distribuídas entre os domínios de atualização too20 (UDs). Durante a manutenção planejada, somente um único domínio de atualização é afetado em um período específico. Lembre-se de que ordem Olá de domínios de atualização sendo afetado não necessariamente acontece em sequência. 

Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure que permite que você toodeploy e gerenciam um conjunto de VMs idênticos como um único recurso. conjunto de escala de saudação é implantado automaticamente nos domínios de atualização, como máquinas virtuais em um conjunto de disponibilidade. Assim como com conjuntos de disponibilidade, com conjuntos de dimensionamento somente um domínio de atualização é afetado em um determinado momento.

Para obter mais informações sobre como configurar as máquinas virtuais para alta disponibilidade, consulte gerenciar disponibilidade de saudação de suas máquinas virtuais para Windows (... / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).
