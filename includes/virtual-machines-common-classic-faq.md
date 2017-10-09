


Este artigo aborda algumas perguntas comuns que os usuários perguntar sobre máquinas virtuais do Azure criadas com o modelo de implantação clássico hello.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Posso migrar meu VM criada no hello modelo toohello novo Gerenciador de recursos modelo de implantação clássico?
Sim. Para obter instruções sobre como toomigrate, consulte:

* [Migração de clássico tooAzure Gerenciador de recursos usando o Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migração de clássico tooAzure Gerenciador de recursos usando a CLI do Azure](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>O que eu posso executar em uma VM do Azure?
Todos os assinantes podem executar software para servidores em uma máquina virtual do Azure. Você pode executar versões recentes do Windows Server, bem como uma variedade de distribuições Linux. Para obter detalhes sobre o suporte, consulte:

• Para VMs do Windows – [Suporte de software para servidores da Microsoft para Máquinas Virtuais do Azure](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Para VMs do Linux – [Linux em distribuições endossadas pelo Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Para imagens de cliente do Windows, determinadas versões do Windows 7 e Windows 8.1 são disponíveis tooMSDN Azure beneficie assinantes e assinantes do MSDN de desenvolvimento e teste pré-pago, para tarefas de desenvolvimento e teste. Para obter detalhes, incluindo instruções e limitações, veja [Imagens do Windows Client para assinantes do MSDN](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>Por que os grupos de afinidades estão sendo preteridos?
Os grupos de afinidade são um conceito herdado para um agrupamento geográfico de implantações de serviço de nuvem do cliente e contas de armazenamento no Azure. Desempenho de rede de máquina virtual para virtual tooimprove nos designs de rede do Azure antecipado Olá fosse fornecido originalmente. Eles também suporte para a versão de saudação inicial de redes virtuais (VNets), que eram limitadas tooa um conjunto pequeno de hardware em uma região.

rede atual do Azure de saudação dentro de uma região é projetado para que os grupos de afinidade não são mais necessários. As redes virtuais também estão em um escopo regional e, portanto, não é mais necessário ter um grupo de afinidades ao usar uma rede virtual. Devido a melhorias toothese, não recomendamos que os clientes usam grupos de afinidade, porque eles podem ser limitando em alguns cenários. Usar grupos de afinidade desnecessariamente associará o hardware toospecific VMs que limita a escolha de saudação de tamanhos de VM tooyou disponível. Também, isso pode levar erros relacionados a toocapacity quando você tenta tooadd novas VMs se hardware específico Olá associados ao grupo de afinidade hello está perto de capacidade.

Recursos do grupo de afinidade já foram preteridos no modelo de implantação do Azure Resource Manager hello e no hello portal do Azure. Para o portal do Azure clássico de Olá, podemos estiver reprovando suporte para criar grupos de afinidade e criar recursos de armazenamento que são fixados tooan grupo de afinidade. Você não precisa toomodify existente serviços de nuvem que estão usando um grupo de afinidade. No entanto, você não deve usar os grupos de afinidades para os novos serviços de nuvem, a menos que isso seja recomendado por um profissional do suporte do Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanto armazenamento eu posso usar com uma máquina virtual?
Cada disco de dados pode ser até too1 TB. número de saudação de discos de dados, que você pode usar depende Olá tamanho da saudação máquina virtual. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Uma conta de armazenamento do Azure fornece armazenamento para o disco do sistema operacional hello e eventuais discos de dados. Cada disco é um arquivo .vhd armazenado como um blob de páginas. Para obter detalhes sobre preços, veja [Detalhes de preços de armazenamento](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Quais tipos de disco rígido virtual eu posso usar?
O Azure dá suporte apenas a discos rígidos virtuais fixos no formato VHD. Se você tiver um VHDX que você deseja toouse no Azure, será necessário toofirst convertê-lo usando o Gerenciador do Hyper-V ou hello [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) cmdlet. Depois de fazer isso, use [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) Olá tooupload de cmdlet (no modo de gerenciamento de serviço) VHD tooa conta de armazenamento do Azure para que você pode usá-lo com máquinas virtuais.

* Para obter instruções do Linux, consulte [criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Para obter instruções do Windows, consulte [criar e carregar um VHD do Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Olá essas máquinas virtuais são iguais às máquinas virtuais Hyper-V?
Em muitos aspectos, elas são muito semelhantes VMs do Hyper-V "Geração 1", mas eles são não exatamente Olá mesmo. Ambos os tipos oferecem hardware virtualizado e discos rígidos virtuais de formato VHD Olá são compatíveis. Isso significa que você pode movê-los entre o Hyper-V e o Azure. Três diferenças principais que às vezes surpreendem os usuários do Hyper-V são:

* O Azure não fornece acesso do console tooa VM. Não há nenhuma maneira tooaccess uma VM até que isso seja feito inicialização.
* As VMs do Azure na maioria dos [tamanhos](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) têm apenas um adaptador de rede virtual, o que significa que elas também podem ter apenas um endereço IP externo. (hello A8 e A9 tamanhos usam um segundo adaptador de rede para comunicação de aplicativos entre instâncias em situações limitadas).
* As VMs do Azure não são compatíveis com recursos de VM do Hyper-V de geração 2. Para obter detalhes sobre esses recursos, confira [Especificações de máquina virtual do Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) e [Visão geral da máquina virtual geração 2](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Essas máquinas virtuais podem usar minha infraestrutura de rede local existente?
Para máquinas virtuais criadas no modelo de implantação clássico Olá, você pode usar a rede Virtual do Azure tooextend sua infraestrutura existente. abordagem de saudação é como configurar uma filial. Você pode provisionar e gerenciar redes virtuais privadas (VPNs) no Azure, bem como se conectar com segurança-los tooon local infraestrutura de TI. Para obter detalhes, veja [Visão geral da Rede Virtual](../articles/virtual-network/virtual-networks-overview.md).

Você precisará toospecify Olá rede Olá a máquina virtual toobelong toowhen criar máquina virtual de saudação. Você não pode unir a máquina virtual tooa rede virtual existente. No entanto, você pode contornar esse problema desanexar Olá virtual VHD (disco rígido) de máquina virtual existente de saudação e, em seguida, usá-lo toocreate uma nova máquina virtual com configuração de rede Olá desejada.

## <a name="how-can-i-access--my-virtual-machine"></a>Como posso acessar minha máquina virtual?
É necessário tooestablish toolog uma conexão remota na máquina virtual de toohello usando a Conexão de área de trabalho remota para uma VM do Windows ou o Secure Shell (SSH) para uma VM do Linux. Para obter instruções, consulte:

* [Como tooLog no tooa Máquina Virtual executando o Windows Server](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Um máximo de conexões simultâneas 2 têm suporte, a menos que o servidor de saudação é configurado como um host de sessão de serviços de área de trabalho remota.  
* [Como tooLog no tooa Máquina Virtual que executa o Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Por padrão, o SSH permite um máximo de 10 conexões simultâneas. Você pode aumentar esse número editando o arquivo de configuração de saudação.

Se você estiver tendo problemas com a área de trabalho remota ou SSH, instalar e usar o hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema de saudação de correção de toohelp de extensão.

Para VMs Windows, as opções adicionais incluem:

* Olá portal clássico do Azure, localize Olá VM e clique em **acesso remoto redefinir** na barra de comandos de saudação.
* Revisão [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Usar o Windows PowerShell Remoting tooconnect toohello VM ou criar pontos de extremidade adicionais para outros toohello de tooconnect recursos VM. Para obter detalhes, consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se você estiver familiarizado com o Hyper-V, você poderá ser procurando um tooVMConnect semelhante de ferramenta. O Azure não oferece uma ferramenta semelhante, porque não há suporte para acessar o console tooa computador virtual.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>É possível usar dados de toostore saudação em disco temporário (Olá unidade d: para Windows ou /dev/sdb1 para Linux)?
Você não deve usar dados de toostore saudação em disco temporário (Olá unidade d: por padrão para o Windows ou /dev/sdb1 para Linux). Elas são apenas um armazenamento temporário, você se arriscaria a perder dados que não podem ser recuperados. Isso pode ocorrer quando a máquina virtual de saudação move tooa outro host. Redimensionamento de uma máquina virtual, atualizar host hello, ou uma falha de hardware no host de saudação é alguns dos motivos Olá que pode mover uma máquina virtual.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Como alterar a letra da unidade de saudação do disco temporário Olá?
Em uma máquina virtual do Windows, você pode alterar a letra de unidade de saudação pelo arquivo de página móvel hello e reatribuindo letras de unidade, mas você precisará toomake se que Olá etapas em uma ordem específica. Para obter instruções, consulte [alterar a letra da unidade saudação do disco temporário do Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Como atualizar o sistema operacional Olá?
Olá termo atualizar geralmente significa tooa móvel mais recente versão do sistema operacional, mantendo Olá mesmo hardware. Para VMs do Azure, Olá processo para transferir tooa versão mais recente é diferente do Linux e do Windows:

* Para VMs do Linux, use ferramentas de gerenciamento de pacotes de saudação e os procedimentos apropriados para a distribuição de saudação.
* Para uma máquina virtual do Windows, você precisará de servidor de saudação do toomigrate usando algo como Olá ferramentas de migração do Windows Server. Não tente tooupgrade Olá SO enquanto ele estiver no Azure. Ele não é suportado por causa do risco de saudação de perda de acesso toohello VM. Se ocorrerem problemas durante a atualização de saudação, você poderá perder Olá capacidade toostart uma área de trabalho remota sessão e não será capaz de tootroubleshoot problemas hello.

Para obter detalhes gerais sobre as ferramentas de saudação e processos para migrar um servidor do Windows, consulte [tooWindows migrar funções e recursos de servidor](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>O que é Olá nome de usuário e senha na máquina virtual de Olá?
imagens de saudação fornecidas pelo Azure não tem um nome de usuário pré-configurado e uma senha. Quando você criar a máquina virtual usando uma dessas imagens, será necessário um nome de usuário e senha, que você usará tooprovide toolog na máquina virtual de toohello.

Se você esqueceu Olá nome de usuário ou senha e instalou Olá agente de VM, você pode instalar e usar o hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problema de saudação do toofix de extensão.

Detalhes adicionais:

* Para imagens do Linux hello, se você usar Olá portal clássico do Azure, "azureuser" é fornecido como um nome de usuário padrão, mas você pode alterar isso usando 'Da galeria' em vez de 'Criação rápida' como máquina virtual do hello maneira toocreate hello. Usar 'Da galeria' também permite que você decida se toouse uma senha, uma chave SSH ou ambas as toolog no. Olá, conta de usuário é um usuário sem privilégios que tem acesso de 'sudo' toorun de comandos com privilégios. conta de 'root' Hello está desabilitada.
* Para imagens do Windows, você precisará tooprovide um nome de usuário e senha ao criar hello VM. conta de saudação é adicionada toohello grupo de administradores.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>O Azure pode executar antivírus nas minhas máquinas virtuais?
O Azure oferece várias opções para soluções de antivírus, mas cabe tooyou toomanage-lo. Por exemplo, talvez seja necessário uma assinatura separada para software antimalware, e você precisará toodecide quando toorun verifica e instala atualizações. Você pode adicionar suporte antivírus com uma extensão de VM para Antimalware da Microsoft, o Symantec Endpoint Protection ou o TrendMicro Deep Security Agent quando criar uma máquina virtual do Windows ou em um momento posterior. Olá Symantec e TrendMicro extensões permitem que você usar uma assinatura de avaliação gratuita de tempo limitado ou uma assinatura empresarial existente. O Antimalware da Microsoft é gratuito. Para obter mais informações, consulte:

* [Como tooinstall e configurar o Symantec Endpoint Protection em uma VM do Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Como tooinstall e configurar o Trend Micro Deep Security como um serviço em uma VM do Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Implantando soluções antimalware em máquinas virtuais do Azure](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Quais são minhas opções de backup e recuperação?
O Backup do Azure está disponível como visualização em determinadas regiões. Para obter detalhes, veja [Fazer backup de máquinas virtuais do Azure](../articles/backup/backup-azure-vms.md). Existem outras soluções de parceiros certificados. toofind o que está disponível no momento, pesquise hello Azure Marketplace.

Uma opção adicional é toouse capacidades de instantâneo de saudação do armazenamento de blob. toodo isso, você precisará tooshut inativo saudação VM antes de qualquer operação que precise de um instantâneo de blob. Isso salva gravações de dados pendentes e coloca o sistema de arquivos de saudação em um estado consistente.

## <a name="how-does-azure-charge-for-my-vm"></a>Como o Azure cobra pela minha VM?
Azure cobra um preço por hora com base no tamanho da VM hello e o sistema operacional. Para horas parciais, Azure cobra apenas pelos minutos de saudação de uso. Se você criar hello VM com uma imagem de VM com determinado software pré-instalado, podem ser aplicadas taxas adicionais de software por hora. O Azure cobra separadamente pelo armazenamento para discos de dados e o sistema operacional da VM hello. Armazenamento em disco temporário é gratuito.

Você será cobrado quando Olá status da VM está em execução ou parado, mas que não seja cobrado quando Olá status da VM é parada (desalocada). tooput uma VM em Olá parado (desalocado) estado, proceda de uma das seguintes hello:

* Desligar ou excluir Olá VM da saudação portal clássico do Azure.
* Use o cmdlet de Stop-AzureVM do hello, disponível no módulo do Azure PowerShell hello.
* Usar operação da função de desligamento de saudação no hello API de REST de gerenciamento de serviços e especifique StoppedDeallocated para o elemento PostShutdownAction de saudação.

Para obter mais detalhes, veja [Preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>O Azure reinicializará minha VM para manutenção?
Às vezes, o Azure reiniciará sua VM como parte de atualizações de manutenção regulares e planejadas nos datacenters do Azure de saudação.

Eventos de manutenção não planejados podem ocorrer quando o Azure detectar um problema sério de hardware que afete sua VM. Para eventos não planejados, o Azure migra host tooa Íntegro da VM Olá automaticamente e reinicia Olá VM.

Para qualquer VM autônoma (ou seja, Olá VM não fizer parte de um conjunto de disponibilidade), o Azure notifica Olá administrador do serviço assinatura por email pelo menos uma semana antes da manutenção planejada porque Olá VMs pode ser reiniciada durante a atualização de saudação. Aplicativos em execução nas VMs Olá podem apresentar tempo de inatividade.

Você também pode usar Olá portal clássico do Azure ou registros de reinicialização do Azure PowerShell tooview hello quando reinicialização Olá ocorreu devido a manutenção de tooplanned. Para obter detalhes, veja [Exibindo logs de reinicialização de VM](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

tooprovide redundância, coloque duas ou mais da mesma forma configurado VMs em Olá mesmo conjunto de disponibilidade. Isso ajuda a garantir que pelo menos uma VM esteja disponível durante a manutenção planejada ou não planejada. O Azure garante determinados níveis de disponibilidade de VM para essa configuração. Para obter detalhes, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Recursos adicionais
[Sobre máquinas virtuais do Azure](../articles/virtual-machines/virtual-machines-linux-about.md)

[Criar e gerenciar máquinas virtuais Linux com hello CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Criar e Gerenciar as VMs do Windows com o Azure PowerShell ](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

