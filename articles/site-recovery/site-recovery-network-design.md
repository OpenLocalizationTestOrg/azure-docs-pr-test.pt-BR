---
title: "aaaDesigning sua infraestrutura de rede para a recuperação de desastres | Microsoft Docs"
description: "Este artigo analisa as considerações de design de rede para o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Projetar sua rede para recuperação de desastre

Este artigo é direcionado tooIT profissionais que é responsável por arquitetar, implementação e suporte de infra-estrutura (BCDR) de recuperação de desastres e continuidade de negócios e que queiram tooleverage Microsoft Azure Site Recovery (ASR) toosupport e Aprimore seus serviços BCDR. Este artigo aborda considerações práticas para a estruturação de rede no site de recuperação de desastre, seja no Azure ou em outro site local. 

## <a name="overview"></a>Visão geral
[Recuperação de Site do Azure (ASR)](https://azure.microsoft.com/services/site-recovery/) é um serviço do Microsoft Azure que coordena a proteção de saudação e recuperação de seus aplicativos virtualizados para fins de recuperação (BCDR) de desastres de continuidade de negócios. Este documento é pretendido tooguide Olá leitor pelo processo de saudação da criação de redes hello, concentrando-se na arquitetura de intervalos de IP e sub-redes no site de recuperação de desastres hello, ao replicar máquinas virtuais (VMs) usando o Site Recovery.

Além disso, este artigo demonstra como recuperação de Site permite que a arquitetura e implementação dos serviços de BCDR um datacenter virtual multissite toosupport em tempo de teste ou um desastre.

Em um mundo onde todos esperam que a conectividade de 24 horas, 7, é mais importante do que nunca tookeep sua infra-estrutura e os aplicativos em funcionamento. Olá finalidade continuidade dos negócios e recuperação de desastres (BCDR) é toorestore falhado componentes para a organização Olá rapidamente pode retomar as operações normais. Desenvolvendo toodeal estratégias de recuperação de desastres com eventos improváveis, devastadores é muito difícil. Isso é devido a dificuldade de toohello inerentes de prever Olá futuro, particularmente quando se trata eventos tooimprobable e Olá alto custo tooprovide as medidas adequadas de proteção contra catástrofes abrangentes.

É crucial que o planejamento BCDR, Objetivo do Tempo de Recuperação (RTO) e Objetivo do Ponto de Recuperação (RPO) sejam definidos como parte de um plano de recuperação de desastres. Quando um desastre ocorrer Centro de dados do cliente de saudação do, usando o Azure Site Recovery, os clientes podem rapidamente (baixo RTO) colocar online suas máquinas virtuais replicadas localizadas no hello data center secundário ou o Microsoft Azure com perda mínima de dados (RPO baixo).

Failover é possibilitado pela ASR que copia inicialmente designadas máquinas de virtuais de saudação dados primários center toohello data center secundário ou tooAzure (dependendo do cenário de saudação) e, em seguida, atualiza periodicamente as réplicas de saudação. Durante o planejamento da infraestrutura, o design da rede deve ser considerado como um afunilamento em potencial que pode impedir que você atenda os objetivos RTO e RPO da empresa.  

Quando os administradores estiver planejando toodeploy uma solução de recuperação de desastres, uma das perguntas mais importantes Olá em suas mentes é como máquina virtual de saudação seria inacessível após a conclusão do failover de saudação. A ASR permite Olá administrador toochoose Olá rede toowhich uma máquina virtual será conectado tooafter failover. Se o site primário Olá é o Azure ou é um site local gerenciado por um servidor do VMM, e isso é feito usando o mapeamento de rede. Saiba mais sobre [mapeamento de rede no Azure tooAzure DR](site-recovery-network-mapping-azure-to-azure.md) e [mapeamento de rede do VMM](site-recovery-network-mapping.md)


Durante a criação de rede Olá para o site de recuperação hello, administrador Olá tem duas opções:

* Use um intervalo de endereço IP diferente para a rede de saudação no local de recuperação. Neste cenário Olá VM após o failover receberá um novo endereço IP e Olá que administrador toodo uma atualização de DNS. 
* Use o mesmo intervalo de endereços IP para rede Olá no local de recuperação de saudação. Em determinados cenários administradores prefere tooretain Olá endereços que têm no site primário Olá mesmo após o failover de saudação. Em um cenário comum, um administrador teria tooupdate Olá rotas tooindicate Olá novo local de endereços IP hello. Mas, no cenário Olá onde uma sub-rede ampliada é implantada entre hello primário e sites de recuperação Olá, reter os endereços IP Olá para máquinas virtuais de saudação se torna uma opção atraente. Não é possível ampliar uma sub-rede de uma rede de local tooan rede do Azure ou entre duas redes do Azure.  

Quando os administradores estiver planejando toodeploy uma solução de recuperação de desastres, uma das perguntas mais importantes Olá em mente é como aplicativos hello serão acessíveis após a conclusão do failover de saudação. Aplicativos modernos quase sempre são dependentes do grau de toosome de rede fisicamente movendo um serviço de um site tooanother representa um desafio de rede. Há duas maneiras principais desse problema ser abordado nas soluções de recuperação de desastres. Olá primeira abordagem é toomaintain endereços IP fixos. Apesar dos serviços Olá movendo e Olá em locais físicos diferentes de servidores de hospedagem, aplicativos se a configuração do endereço IP hello com eles toohello novo local. Olá segunda abordagem envolve alterar completamente o endereço IP de Olá durante a transição de saudação no site recuperado hello. Cada abordagem possui diversas variações de implementação que são resumidas abaixo.

Durante a criação de rede Olá para o site de recuperação hello, administrador Olá tem duas opções:

## <a name="option-1-retain-ip-addresses"></a>Opção 1: Manter os endereços IP
De uma perspectiva de processo de recuperação de desastres, usando endereços IP fixos aparece toobe hello mais fácil método tooimplement, mas ele tem um número de possíveis desafios que, na prática, tornar Olá abordagem menos popular. Recuperação de Site do Azure fornece a capacidade de saudação endereços IP hello tooretain em todos os cenários. Antes de decide tooretain IP, pensamento apropriado deve ser dada toohello restrições impõe nos recursos de failover de saudação. Vamos dar uma olhada em fatores de saudação que podem ajudá-lo a toomake que um decisão tooretain de endereços IP, ou não. Isso pode ser feito de duas maneiras, por meio de uma sub-rede ampliada ou pela realização de um failover de sub-rede completo.

### <a name="stretched-subnet"></a>Sub-rede ampliada
Aqui sub-rede Olá é disponibilizado simultaneamente no primário e os locais de recuperação de desastres. Em termos simples, isso significa você pode mover um servidor e seu site segundo de toohello de configuração de IP (camada 3) e rede Olá roteará o novo local do hello tráfego toohello automaticamente. Isso é trivial toodeal da perspectiva do servidor, mas ele tem um número de desafios:

* Do ponto de vista da Camada 2 (camada do link de dados), irá requerer um equipamento de rede que possa gerenciar uma VLAN ampliada, mas isto se tornou um problema menor pois, agora, está amplamente disponível. Olá segundo e mais difícil problema é que alongando Olá domínio de falha potencial Olá VLAN é estendido tooboth sites, essencialmente se tornar um ponto único de falha. Embora seja uma ocorrência improvável, pode acontecer de uma tempestade de transmissão iniciar, mas não conseguir ser isolada. Encontramos opiniões mistas sobre esse último problema e vimos muitas implementações bem-sucedidas, bem como "nunca implementaremos essa tecnologia aqui".
* Ampliada de sub-rede não é possível se você estiver usando o Microsoft Azure como Olá site de recuperação de desastres.

### <a name="subnet-failover"></a>Failover da sub-rede
É possível tooimplement sub-rede failover tooobtain Olá benefícios Olá ampliado sub-rede solução descrita acima sem alongamento sub-rede Olá em vários sites. Aqui, qualquer sub-rede dada estaria presente no Site 1 ou Site 2, mas nunca em ambos os sites simultaneamente. Em ordem toomaintain Olá espaço de endereço IP no evento de saudação de um failover, é possível organizar tooprogrammatically Olá roteador infraestrutura toomove Olá subredes de tooanother de um site. Em uma saudação do cenário de failover sub-redes seriam mover com hello associados VMs protegidas. Olá principal desvantagem toothis consiste na saudação de uma falha tem toomove Olá toda sub-rede, que pode ser Okey, mas poderá afetar considerações de granularidade Olá failover.

Vamos examinar como uma empresa fictícia chamada Contoso é capaz de tooreplicate seu local de recuperação de tooa VMs ao failover de sub-rede inteira hello. Primeiro veremos como Contoso é capaz de toomanage suas sub-redes enquanto replicar máquinas virtuais entre dois locais locais e, em seguida, vamos discutir como funciona o failover de sub-rede quando [Azure é usado como local de recuperação de desastres Olá](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Failover de local tooAzure 
Recuperação de Site do Azure (ASR) permite que o Azure toobe usado como um local de recuperação de desastres para suas máquinas virtuais.  

Examinemos um cenário no qual uma empresa fictícia, denominada Banco Woodgrove, tem uma infraestrutura local que hospeda sua linha de aplicativos de negócios e eles estão hospedando seus aplicativos móveis no Azure. A conectividade entre as VMs do Woodgrove Bank no Azure e os servidores locais é fornecida por uma VPN (rede virtual privada) site a site (S2S) ou ExpressRoute. VPN S2S permite que a rede virtual do Woodgrove Bank no Azure toobe visto como uma extensão do Woodgrove Bank rede local. Essa comunicação é habilitada pela VPN S2S entre a borda do Banco Woodgrove e a rede virtual do Azure. Agora, o Woodgrove deseja toouse ASR tooreplicate suas cargas de trabalho região primária do Azure tooanother região do Azure. Essa opção atende às necessidades de saudação do Woodgrove, o que quer uma opção de recuperação de desastres econômica e é capaz de toostore dados em ambientes de nuvem pública. Woodgrove tem toodeal com aplicativos e configurações que dependem de endereços IP embutidos, portanto, têm endereços IP de tooretain um requisito para seus aplicativos depois do failover em região tooanother no Azure.

O Woodgrove decidiu tooassign endereços IP de recursos de tooits IP endereço intervalo (172.16.1.0/24, 172.16.2.0/24) em execução no Azure.

Para Woodgrove toobe capaz de tooreplicate tooAzure suas máquinas virtuais enquanto retém os endereços IP hello, uma rede Virtual do Azure precisa toobe criado. Ele deve ser uma extensão da rede do local de saudação para que os aplicativos possam realizar failover de saudação local site tooAzure perfeitamente. O Azure permite tooadd site a site como ponto a site VPN conectividade toohello redes virtuais criadas no Azure. Ao configurar sua conexão site a site, a rede do Azure permite que você tooroute tráfego toohello local (Azure chamá-lo da rede local) somente se o intervalo de endereços IP hello é diferente do intervalo de endereços IP do local hello, porque o Azure não suporte a sub-redes de alongamento.  Isso significa que, se você tiver 192.168.1.0/24 uma sub-rede local, não é possível adicionar uma rede local 192.168.1.0/24 no hello rede do Azure. Isso é esperado, pois o Azure não sabe que não há nenhuma VM active na sub-rede hello e sub-rede hello está sendo criada apenas para fins de recuperação de desastres. toobe toocorrectly capaz de rotear o tráfego de rede fora de um Azure Olá sub-redes na rede de saudação e saudação da rede local não deve estar em conflito.

![Antes do failover de sub-rede](./media/site-recovery-network-design/network-design7.png)

Antes do failover

toohelp Woodgrove atender seus requisitos de negócios, precisamos Olá tooimplement fluxos de trabalho a seguir:

* Criar uma rede adicional, vamos chamá-la a rede de recuperação, onde Olá failover virtual máquinas seria criadas.
* tooensure que Olá IP para uma máquina virtual é mantido após um failover, acesse a guia Configurar de toohello em Propriedades da VM, especifique Olá mesmo IP hello VM tem local e, em seguida, clique em Salvar. Quando Olá VM é feito o failover, Azure Site Recovery atribuirá Olá fornecido IP toohello VM.

![Propriedades da rede](./media/site-recovery-network-design/network-design8.png)

Depois de Olá failover é acionado e máquinas virtuais de saudação são criadas no hello rede de recuperação com IP hello desejado, rede de toothis de conectividade pode ser estabelecida com um [Vnet tooVnet Conexão](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Se requerido, essa ação poderá ser por script.  Conforme abordado na seção anterior Olá sobre o failover de sub-rede, mesmo no caso de saudação de failover tooAzure, rotas seria toobe adequadamente modificou tooreflect que 192.168.1.0/24 agora foi movido tooAzure.

![Após o failover da sub-rede](./media/site-recovery-network-design/network-design9.png)

Após o failover

Se você não tiver uma rede do Azure' ' conforme mostrado na imagem de saudação acima. Você pode criar uma conexão de vpn site toosite entre o 'Site primário' e 'Recuperação rede' após o failover de saudação.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Failover tooa secundário site local
Vamos dar uma olhada em um cenário em que queremos manter Olá IP de cada uma das VMs de saudação e saudação de failover concluir sub-rede juntos. site primário Olá tem aplicativos executados na sub-rede 192.168.1.0/24. Quando ocorre failover hello, todas as máquinas virtuais de saudação que fazem parte dessa sub-rede serão submetidas a failover de local de recuperação de toohello e manter seus endereços IP. Rotas terá toobe fatos de saudação tooreflect que todas as máquinas virtuais de saudação pertencentes toosubnet 192.168.1.0/24 agora moveu o site de recuperação toohello modificado da maneira apropriada.

No Olá Olá de ilustração a seguir roteia entre o site primário e site de recuperação de site de terceiro e site primário e site de terceiro e o site de recuperação terá toobe modificado da maneira apropriada.

Olá imagens a seguir mostra as sub-redes Olá antes do failover de saudação. Subrede 192.168.0.1/24 está ativa no Olá Site primário antes do failover hello e se torna ativa de saudação Site de recuperação após o failover de saudação

![Antes do failover](./media/site-recovery-network-design/network-design2.png)

Antes do failover

imagem de saudação abaixo mostra redes e sub-redes depois do failover.

![Após o failover](./media/site-recovery-network-design/network-design3.png)

Após o failover

No site secundário é local e você estiver usando um toomanage do servidor do VMM em seguida, quando a habilitação da proteção para uma máquina virtual específica, o ASR alocará toohello fluxo de trabalho a seguir de acordo com recursos de rede:

* ASR aloca um endereço IP para cada interface de rede na máquina virtual de saudação do hello endereço IP estático definido na rede de saudação relevantes para cada instância do System Center VMM.
* Se Olá administrador define Olá endereços de IP mesmo pool de rede Olá no site de recuperação hello como que Olá pool de endereços IP de saudação rede no site primário hello, durante a alocação de ASR de máquina virtual de réplica Olá IP endereço toohello alocará Olá mesmo Endereço IP da máquina virtual primária de saudação.  Olá IP é reservado no VMM, mas não definido como o IP de failover no host do Hyper-v hello. IP de Failover em um host Hyper-v é definido apenas antes do failover de saudação.


Se hello mesmo IP não estiver disponível, ASR alocará um outro endereço IP disponível do pool de endereços IP hello definido.

Após a saudação que VM está habilitada para proteção, você pode usar exemplo script tooverify Olá IP que foi alocado a máquina virtual de toohello a seguir. Olá mesmo IP seria definido como o IP de Failover e atribuído toohello VM em tempo de saudação de failover:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> Cenário Olá onde as máquinas virtuais usar DHCP, o gerenciamento Olá de endereços IP está completamente fora de controle de saudação de ASR. Um administrador tem tooensure Olá DHCP atendendo Olá endereços IP do servidor no site de recuperação Olá podem servir de saudação mesmo intervalo do site primário hello.
>
>



## <a name="option-2-changing-ip-addresses"></a>Opção 2: alterar os endereços IP
Essa abordagem parece mais frequente toobe Olá com base no que vimos. Ele assume a forma de saudação de alterar o endereço IP de saudação de cada VM que está envolvido no failover de saudação. Uma desvantagem dessa abordagem requer Olá entrada rede too'learn' aplicativo hello que estava no IPx está agora no IPy. Mesmo se IPx e IPy nomes lógicos, entradas DNS normalmente têm toobe alterados ou liberado em toda a rede Olá e entradas em cache em tabelas de rede tem toobe atualizado ou liberado, portanto um tempo de inatividade pode ser visto, dependendo do modo como a infraestrutura de DNS Olá tem foi instalado. Esses problemas podem ser reduzidos usando valores baixos de TTL no caso de saudação de aplicativos de intranet e [Gerenciador de tráfego do Azure com ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) para internet com base em aplicativos

### <a name="changing-hello-ip-addresses---illustration"></a>A alteração dos endereços IP hello - ilustração
Vamos dar uma olhada no cenário de saudação onde você está planejando toouse IPs diferentes em sites de recuperação de saudação e Olá primário. No exemplo a seguir de saudação também temos um terceiro local de onde aplicativos Olá hospedados no site primário ou de recuperação podem ser acessados.

![IP diferente - antes do failover](./media/site-recovery-network-design/network-design10.png)


Na imagem de saudação acima, há alguns aplicativos hospedados na sub-rede de 192.168.1.0/24 da sub-rede no site primário Olá, e eles foram configurado toocome backup no site de recuperação Olá na sub-rede 172.16.1.0/24 após um failover. Rotas de rede/conexões de VPN foram configuradas corretamente para que todos os três sites possam acessar um ao outro.

Como a imagem Olá abaixo mostra, depois do failover de um ou mais aplicativos, eles serão restaurados na sub-rede de recuperação de saudação. Nesse caso não estamos toofailover restrita Olá toda sub-rede em Olá simultaneamente. Nenhuma alteração é necessária tooreconfigure VPN rotas de rede. Um failover e algumas atualizações DNS manterão os aplicativos acessíveis. Se Olá DNS é configurado tooallow atualizações dinâmicas de máquinas virtuais de saudação seria registrar por conta própria usando Olá novo IP quando eles são iniciados depois de um failover.

![IP diferente - após o failover](./media/site-recovery-network-design/network-design11.png)


Depois de máquina de virtual de réplica Olá falha pode ter um endereço IP que não seja Olá mesmo como endereço IP de saudação da máquina virtual primária de saudação. Máquinas virtuais atualizará o servidor DNS Olá que eles estão usando depois que eles são iniciados. As entradas DNS normalmente têm toobe alterados ou liberado em toda a rede Olá, e entradas em cache em tabelas de rede tem toobe atualizado ou liberado, portanto, não é incomum toobe enfrentam tempo de inatividade enquanto as alterações de estado ocorrem. Esse problema pode ser reduzido:

* Usando valores TTL baixos para aplicativos de intranet.
* Usando o Gerenciador de Tráfego do Azure com o ASR para aplicativos baseados na Internet.
* Usando os seguintes Olá script dentro de sua recuperação planejar tooupdate Olá servidor DNS tooensure uma atualização em tempo hábil (script hello não é necessário se Olá registro de DNS dinâmico estiver configurado)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Alteração Olá endereços IP – tooAzure DR
Olá [instalação da infraestrutura de rede para o Microsoft Azure como um local de recuperação de desastres](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) postagem de blog explica como Olá toosetup necessárias a infraestrutura de rede do Azure ao reter os endereços IP não é um requisito. Ele começa com que descreve o aplicativo hello e, em seguida, procure em como toosetup rede local e no Azure e, em seguida, concluindo com como toodo um failover de teste e um failover planejado.

## <a name="next-steps"></a>Próximas etapas
[Saiba](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) como recuperação de Site mapeia redes de origem e destino, quando um servidor do VMM está sendo site primário do hello toomanage usado.
