---
title: "aaaOverview e arquitetura do HANA SAP no Azure (instâncias grandes) | Microsoft Docs"
description: "Visão geral da arquitetura de como tooDeploy HANA SAP no Azure (instâncias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Visão geral e arquitetura do SAP HANA (Instâncias Grandes) no Azure

## <a name="what-is-sap-hana-on-azure-large-instances"></a>O que é SAP HANA no Azure (Instâncias Grandes)?

SAP HANA no Azure (instância grande) é uma solução exclusiva tooAzure. Além disso tooproviding máquinas virtuais do Azure para finalidade de saudação da implantação e execução SAP HANA, o Azure oferece Olá possibilidade toorun e implante o SAP HANA em servidores de bare-metal que são tooyou dedicado como um cliente. Olá SAP HANA na solução do Azure (instâncias grandes) com base em hardware bare-metal de host/servidor não compartilhado que é atribuído tooyou como um cliente. hardware de servidor de saudação é inserido em carimbos maiores que contêm/servidor de computação, rede e infraestrutura de armazenamento. Isso, enquanto combinação, é certificado pela TDI do HANA. oferta de serviço de saudação do HANA SAP no Azure (instâncias grandes) oferece várias SKUs do servidor diferente ou tamanhos começando com unidades de 72 CPUs e toounits de memória de 768 GB que têm 960 CPUs e memória de 20 TB.

isolamento de cliente de saudação em carimbo de infraestrutura de saudação é executado em locatários, que se parece com detalhadamente:

- Rede: isolamento dos clientes dentro da pilha de infraestrutura por meio de redes virtuais por locatário atribuído pelo cliente. Um locatário é atribuído tooa único cliente. Um cliente pode ter vários locatários. isolamento de rede de saudação de locatários impede a comunicação de rede entre locatários no nível de carimbo de infraestrutura de saudação. Mesmo se locatários pertencem toohello mesmo cliente.
- Componentes de armazenamento: isolamento por meio de máquinas virtuais de armazenamento que têm volumes de armazenamento atribuído tooit. Volumes de armazenamento podem ser atribuídos tooone armazenamento máquina virtual. Uma máquina virtual de armazenamento é atribuída exclusivamente tooone de locatário único na pilha de infraestrutura de certificado do SAP HANA TDI hello. Como resultado volumes de armazenamento atribuídos tooa máquina de virtual de armazenamento podem ser acessados em um específico e relacionado locatário somente. E não são visíveis entre locatários implantado diferentes de saudação.
- Host ou servidor: uma unidade de host ou servidor não é compartilhada entre os clientes ou locatários. Um servidor ou host implantado tooa cliente, é uma unidade atômica computação do bare-metal atribuído tooone único locatário. **Não** é usado nenhum particionamento de hardware ou de software que possa resultar em você, enquanto cliente, compartilhar um host ou um servidor com outro cliente. Volumes de armazenamento que são atribuídos toohello armazenamento da máquina virtual do locatário específico Olá são montado toosuch um servidor. Um locatário pode ter um unidades do servidor toomany de diferentes SKUs atribuídas exclusivamente.
- Dentro de um SAP HANA no carimbo de infraestrutura do Azure (instância grande), vários locatários diferentes são implantados e isolados entre si por meio de conceitos de locatário Olá no nível de rede, armazenamento e computação. 


Essas unidades de bare-metal de servidor são suportada toorun SAP HANA somente. camada de aplicativo de SAP Hello ou intermediários de carga de trabalho está em execução em máquinas virtuais do Microsoft Azure. carimbos de infraestrutura Olá executando Olá HANA SAP no Azure (instância grande) as unidades são conectados toohello rede Azure backbones, assim, que a conectividade de baixa latência entre máquinas virtuais do Azure e o SAP HANA em unidades do Azure (instância grande) é fornecida.

Este documento é um dos cinco documentos, que abrangem o tópico de saudação do HANA SAP no Azure (instância grande). Neste documento, vamos pela arquitetura básica hello, responsabilidades, serviços fornecidos e em um alto nível por meio de recursos de solução de saudação. Para a maioria das áreas de saudação, como sistema de rede e conectividade de hello outros quatro documentos cobrem detalhes e drill análises. documentação de saudação do HANA SAP no Azure (instância grande) não aborda aspectos de instalação do SAP NetWeaver ou implantações do SAP NetWeaver em VMs do Azure. Este tópico é abordado na documentação separada encontrada no hello mesmo contêiner de documentação. 


cinco partes Olá deste guia abrangem Olá seguintes tópicos:

- [Visão geral e arquitetura do SAP HANA (instâncias grandes) no Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infraestrutura e conectividade do SAP HANA (instâncias grandes) no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Como tooinstall e configure o SAP HANA (instâncias grandes) no Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Alta disponibilidade e recuperação de desastre do SAP HANA (instâncias grandes) no Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Solução de problemas e monitoramento do SAP HANA (instâncias grandes) no Azure](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definições

Várias definições comuns são amplamente usadas no guia de implantação técnica e Olá arquitetura. Saudação de Observação termos e seus significados a seguir:

- **IaaS:** Infraestrutura como Serviço
- **PaaS:** Plataforma como Serviço
- **SaaS:** Software como Serviço
- **Componente SAP:** um aplicativo SAP individual como ECC, BW, Solution Manager ou EP. Os componentes SAP podem ser baseados em tecnologias ABAP ou Java tradicionais ou em um aplicativo não baseado em NetWeaver, como o Business Objects.
- **Ambiente SAP:** um ou mais componentes SAP logicamente agrupados tooperform uma função de negócios, como desenvolvimento, QAS, treinamento, DR ou produção.
- **Estrutura SAP:** refere-se ativos SAP inteiros de toohello em seu cenário de TI. Olá estrutura SAP inclui todos os ambientes de produção e não seja de produção.
- **Sistema SAP:** Olá combinação de camada DBMS e camada de aplicativo de um sistema de desenvolvimento SAP ERP, sistema de teste do SAP BW, sistema de produção SAP CRM etc. Implantações do Azure não dão suporte a divisão essas duas camadas entre local e o Azure. Isso significa que um sistema SAP é implantado localmente ou no Azure. No entanto, você pode implantar sistemas diferentes de saudação de uma estrutura SAP no Azure ou no local. Por exemplo, pode implantar os sistemas Olá desenvolvimento e teste de SAP CRM no Azure, durante a implantação Olá SAP CRM produção sistema local. Para o SAP HANA no Azure (instâncias grandes), destina-se que você hospede a camada do aplicativo SAP Olá de sistemas SAP em VMs do Azure e Olá instância SAP HANA relacionada em uma unidade no carimbo de instância grande HANA hello.
- **Grande carimbo da instância:** uma pilha de infraestrutura de hardware que é o SAP HANA TDI certificada e dedicado de instâncias do SAP HANA toorun dentro do Azure.
- **SAP HANA no Azure (instâncias grande):** nome oficial da oferta de saudação em instâncias do HANA toorun do Azure no SAP HANA TDI certified hardware que é implantado em carimbos de instância grande em diferentes regiões do Azure. Olá relacionados ao termo **instância grande HANA** é curta para o SAP HANA no Azure (instâncias grandes) e é amplamente usada neste guia de implantação técnica.
- **Entre locais:** descreve um cenário onde as VMs são implantada tooan assinatura do Azure que tem conectividade de rota expressa entre Olá local datacenter(s) e o Azure, de vários locais ou de site a site. Na documentação comum do Azure, esses tipos de implantações também são descritas como cenários entre instalações. Olá motivo conexão Olá é tooextend domínios locais, Active Directory/OpenLDAP local e local DNS no Azure. Olá paisagem local é estendido toohello ativos do Azure de saudação assinaturas do Azure. Com esta extensão, Olá VMs pode ser parte do domínio de local de saudação. Usuários de domínio do domínio do hello local podem acessar servidores hello e podem executar serviços nas VMs (como serviços DBMS). A comunicação e resolução de nomes entre máquinas virtuais implantadas localmente e VMs implantadas no Azure são possíveis. Como é um cenário típico de saudação SAP que a maioria dos ativos são implantados. Consulte os guias de saudação [de planejamento e design para o Gateway de VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [criar uma rede virtual com uma conexão Site a Site usando o portal do Azure de saudação](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações.
- **Locatário:** um cliente implantado no selo de Instâncias Grandes do HANA é isolado em um "locatário". Um locatário seja isolado em Olá rede, armazenamento e a camada de computação de outros locatários. Portanto, que unidades de armazenamento e computação toohello atribuído diferentes locatários não podem ver uns aos outros ou se comunicam entre si em Olá instância grande HANA carimbo nível. Um cliente pode escolher toohave implantações em diferentes locatários. Mesmo assim, não há nenhuma comunicação entre locatários em Olá nível de carimbo de data / instância grande HANA.

Há uma variedade de recursos adicionais que foram publicados no tópico de saudação de implantação de carga de trabalho do SAP na nuvem pública do Microsoft Azure. É altamente recomendável que qualquer pessoa, planejar e executar uma implantação do SAP HANA no Azure é experientes e ciente das entidades de saudação do IaaS do Azure e implantação de saudação de cargas de trabalho do SAP no Azure IaaS. Olá recursos a seguir fornecem mais informações e devem ser consultados antes de continuar:


- [Uso das soluções SAP em máquinas virtuais do Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certificação

Além de hello NetWeaver certificação, o SAP requer uma certificação especial para toosupport SAP HANA SAP HANA em determinados infraestruturas, como IaaS do Azure.

Olá core nota da SAP NetWeaver e o grau de tooa certificação SAP HANA, é [1928533 de # nota SAP – aplicativos SAP no Azure: tipos de produtos com suporte e a VM do Azure](https://launchpad.support.sap.com/#/notes/1928533).

Este [SAP Note nº 2316233 - SAP HANA no Microsoft Azure (Instâncias Grandes)](https://launchpad.support.sap.com/#/notes/2316233/E) também é significativo. Ele abrange a solução Olá descrita neste guia. Além disso, você está com suporte toorun SAP HANA no tipo de VM GS5 de saudação do Azure. [Informações para este caso são publicadas no site do SAP Olá](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

SAP HANA na solução do Azure (instâncias grandes) Hello chamado tooin SAP Observação #2316233 fornece à Microsoft e os clientes da SAP Olá toodeploy capacidade grande SAP Business Suite, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA ou outras cargas de trabalho do SAP HANA no Azure. Olá solução se baseia no hello SAP-HANA certificada carimbo de hardware dedicado ([SAP HANA personalizado Datacenter integração – TDI](https://scn.sap.com/docs/DOC-63140)). Executando como um TDI do HANA SAP configurada solução fornece com confiança Olá certeza de que todos os aplicativos baseados no SAP HANA (incluindo SAP Business Suite no SAP HANA, SAP Business Warehouse (BW) no SAP HANA, S4/HANA e BW4/HANA) serão toowork Olá infraestrutura de hardware.

Toorunning em comparação com o SAP HANA em máquinas virtuais do Azure esta solução tem um benefício — fornece para volumes de memória muito maiores. Se você quiser tooenable essa solução, há alguns aspectos-chave toounderstand:

- camada do aplicativo SAP Hello e aplicativos SAP não executados em máquinas virtuais do Azure (VMs) que são hospedados em carimbos de hardware do Azure comum hello.
- Cliente de infraestrutura, centros de dados no local e implantações de aplicativo são plataforma de nuvem do Microsoft Azure toohello conectados por meio de rota expressa do Azure (recomendado) ou de rede Virtual privada (VPN). Active Directory (AD) e DNS também se estendem para o Azure.
- instância de banco de dados SAP HANA Olá para carga de trabalho do HANA é executado no SAP HANA no Azure (instâncias grandes). carimbo de instância grande Hello está conectado em rede do Azure, para que software em execução em VMs do Azure possa interagir com a instância do HANA Olá em execução em instâncias grandes HANA.
- Hardware do SAP HANA no Azure (Instâncias Grandes) é fornecido em uma infraestrutura como serviço (IaaS) com o SUSE Linux Enterprise Server de hardware dedicado ou Red Hat Enterprise Linux, pré-instalado. Como com as máquinas virtuais do Azure, mais as atualizações e manutenção toohello operacional sistema é sua responsabilidade.
- Instalação do HANA ou quaisquer componentes adicionais necessários toorun SAP HANA em unidades do HANA grandes instâncias é sua responsabilidade, assim como todos os respectivos operações em andamento e administração do HANA SAP no Azure.
- Além disso toohello as soluções descritas aqui, você pode instalar outros componentes na sua assinatura do Azure que se conecta tooSAP HANA no Azure (instâncias grandes).  Por exemplo, os componentes que permitem a comunicação com e/ou diretamente o banco de dados do toohello SAP HANA (servidores de salto, servidores de RDP do SAP HANA Studio, serviços de dados do SAP para cenários SAP BI, ou soluções de monitoramento de rede).
- Assim como no Azure, as Instâncias Grandes do HANA dão suporte às funcionalidades de Alta Disponibilidade e de Recuperação de Desastre.

## <a name="architecture"></a>Arquitetura

Em um nível alto, hello SAP HANA na solução do Azure (instâncias grandes) tem camada do aplicativo que residem em VMs do Azure e hello camada de banco de dados que residem em hardware configurado a TDI SAP localizado em um carimbo de instância grande no SAP Olá Olá mesma região do Azure que está conectado tooAzure IaaS.

> [!NOTE]
> Precisa de camada do aplicativo SAP toodeploy Olá no hello mesma região do Azure como camada de DBMS SAP hello. Essa regra é bem documentada em informações publicadas sobre carga de trabalho do SAP no Azure. 

Olá arquitetura geral do HANA SAP no Azure (instâncias grandes) fornece uma configuração de hardware certificado SAP TDI (não-virtualizados, bare metal, o servidor de alto desempenho para o banco de dados do SAP HANA Olá) e a capacidade de saudação e a flexibilidade de tooscale do Azure recursos para Olá SAP toomeet de camada de aplicativo a suas necessidades.

![Visão geral da arquitetura do SAP HANA no Azure (Instâncias Grandes)](./media/hana-overview-architecture/image1-architecture.png)

arquitetura de saudação mostrada é dividida em três seções:

- **Direita:** uma infraestrutura local executando aplicativos diferentes em data centers com usuários finais acesso a aplicativos de LOB (como SAP). Idealmente, esse local infraestrutura é conectada tooAzure com o Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Centro:** mostra Azure IaaS e, nesse caso, uso de máquinas virtuais do Azure toohost SAP ou outros aplicativos que usam o SAP HANA como um sistema DBMS. Instâncias HANA menores que fornecem função com memória Olá VMs do Azure são implantadas em máquinas virtuais do Azure junto com sua camada de aplicativo. Saiba mais sobre [Máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/).
<br />Rede do Azure é sistemas SAP de toogroup usada junto com outros aplicativos em redes virtuais do Azure (VNets). Essas VNets conectar sistemas tooon locais, bem como tooSAP HANA no Azure (instâncias grandes).
<br />Para aplicativos do SAP NetWeaver e bancos de dados com suporte toorun no Microsoft Azure, consulte [1928533 de n º de observação de suporte do SAP – aplicativos SAP no Azure: tipos de produtos com suporte e a VM do Azure](https://launchpad.support.sap.com/#/notes/1928533). Para obter a documentação sobre como implantar soluções SAP no Azure, examine:

  -  [Uso do SAP em VMs (máquinas virtuais) do Windows](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Uso das soluções SAP em máquinas virtuais do Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **À esquerda:** mostra Olá SAP HANA TDI certified hardware em carimbo de instância grande Azure hello. unidades de instância grande HANA Olá são conectado toohello VNets do Azure de sua assinatura usando Olá Olá conectividade com a mesma tecnologia local no Azure.

carimbo de instância grande Azure Olá próprio combina Olá componentes a seguir:

- **Computação:** servidores baseados em processadores Intel Xeon E7-8890v3 ou Intel Xeon E7-8890v4 que fornecem a capacidade de computação necessários hello e SAP HANA certificados.
- **Rede:** unificado de uma malha de rede de alta velocidade que interconexões Olá computação, armazenamento e componentes de rede local.
- **Armazenamento:** uma infraestrutura de armazenamento que é acessada por meio de uma malha de rede unificada. Capacidade de armazenamento específica é fornecido dependendo Olá específico do SAP HANA na configuração do Azure (instâncias grandes) que está sendo implantado (mais capacidade de armazenamento está disponível a um custo mensal adicional).

Na infraestrutura de multilocatário Olá de carimbo de instância grande hello, os clientes são implantados como locatários isolados. Na implantação do locatário Olá, é necessário tooname uma assinatura do Azure dentro de seu registro do Azure. Este será toobe Olá assinatura do Azure, Olá instâncias grandes HANA será toobe cobrado em relação. Esses locatários tenham uma relação de 1:1 de toohello assinatura do Azure. Rede aconselhável é possível tooaccess uma unidade de instância grande HANA implantado em um locatário em uma região do Azure de diferentes VNets do Azure, que pertence a toodifferent assinaturas do Azure. Embora as assinaturas do Azure precisam toobelong toohello mesmo registro do Azure. 

Assim como acontece com VMs do Azure, SAP HANA no Azure (Instâncias Grandes) é oferecido em várias regiões do Azure. Recursos de recuperação de desastres de toooffer ordem, você pode escolher tooopt no. Carimbos de instância grande diferentes dentro de uma região geográfica políticas são conectado tooeach outros. Por exemplo, carimbos de instância grande HANA em US West e US East estão conectados através de um link de rede dedicado para finalidade de saudação de replicação de recuperação de desastres. 

Assim como você pode escolher entre diferentes tipos de VM com as máquinas virtuais do Azure, você pode escolher entre diferentes SKUs do HANA em Instâncias Grandes que são personalizados para tipos diferentes de carga de trabalho do SAP HANA. SAP aplica-se taxas de soquete tooprocessor memória às cargas de trabalho com base em gerações de processador Intel hello – há quatro tipos diferentes de SKU oferecidos:

A partir de julho de 2017, o SAP HANA no Azure (instâncias grandes) está disponível em diversas configurações no hello Azure regiões de US West e Leste dos EUA, Leste da Austrália, Sudeste da Austrália, Europa Ocidental e Norte da Europa:

| Solução SAP | CPU | Memória | Armazenamento | Disponibilidade |
| --- | --- | --- | --- | --- |
| Otimizado para OLAP: SAP BW, BW/4HANA<br /> ou SAP HANA para carga de trabalho OLAP genérica | SAP HANA no Azure S72<br /> – 2 x processadores Intel® Xeon® E7-8890 v3<br /> 36 núcleos de CPU e 72 threads de CPU |  768 GB |  3 TB | Disponível |
| --- | SAP HANA no Azure S144<br /> – 4 x processadores Intel® Xeon® E7-8890 v3<br /> 72 núcleos de CPU e 144 threads de CPU |  1,5 TB |  6 TB | Não é mais oferecido |
| --- | SAP HANA no Azure S192<br /> – 4 x processadores Intel® Xeon® E7-8890 v4<br /> 96 núcleos de CPU e 192 threads de CPU |  2,0 TB |  8 TB | Disponível |
| --- | SAP HANA no Azure S384<br /> – 8 x processadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  4,0 TB |  16 TB | TooOrder pronto |
| Otimizado para OLTP: SAP Business Suite<br /> no SAP HANA ou S/4HANA (OLTP),<br /> OLTP genérico | SAP HANA no Azure S72m<br /> – 2 x processadores Intel® Xeon® E7-8890 v3<br /> 36 núcleos de CPU e 72 threads de CPU |  1,5 TB |  6 TB | Disponível |
|---| SAP HANA no Azure S144m<br /> – 4 x processadores Intel® Xeon® E7-8890 v3<br /> 72 núcleos de CPU e 144 threads de CPU |  3,0 TB |  12 TB | Não é mais oferecido |
|---| SAP HANA no Azure S192m<br /> – 4 x processadores Intel® Xeon® E7-8890 v4<br /> 96 núcleos de CPU e 192 threads de CPU  |  4,0 TB |  16 TB | Disponível |
|---| SAP HANA no Azure S384m<br /> – 8 x processadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  6,0 TB |  18 TB | TooOrder pronto |
|---| SAP HANA no Azure S384xm<br /> – 8 x processadores Intel® Xeon® E7-8890 v4<br /> 192 núcleos de CPU e 384 threads de CPU |  8,0 TB |  22 TB |  TooOrder pronto |
|---| SAP HANA no Azure S576<br /> – 12 x processadores Intel® Xeon® E7-8890 v4<br /> 288 núcleos de CPU e 576 threads de CPU |  12,0 TB |  28 TB | TooOrder pronto |
|---| SAP HANA no Azure S768<br /> – 16 x processadores Intel® Xeon® E7-8890 v4<br /> 384 núcleos de CPU e 768 threads de CPU |  16,0 TB |  36 TB | TooOrder pronto |
|---| SAP HANA no Azure S960<br /> – 20 x processadores Intel® Xeon® E7-8890 v4<br /> 480 núcleos de CPU e 960 threads de CPU |  20,0 TB |  46 TB | TooOrder pronto |

- Núcleos de CPU = soma de núcleos de CPU não-hyper-threading de soma de saudação de processadores de saudação de unidade do servidor de saudação.
- Threads de CPU = soma de threads de computação fornecidas pelo hyper-threading núcleos de CPU da soma de saudação de processadores de saudação de unidade do servidor de saudação. Todas as unidades são configuradas por padrão toouse Hyper-Threading.


Olá configurações diferentes acima que estão disponíveis ou 'não são oferecidas mais' são referenciadas na [2316233 de # de observação de suporte do SAP – SAP HANA no Microsoft Azure (instâncias grandes)](https://launchpad.support.sap.com/#/notes/2316233/E). configurações de saudação, que são marcadas como 'TooOrder pronto' encontrará sua entrada em Olá nota da SAP em breve. No entanto, os SKUs de instância pode ser solicitados já para Olá seis diferentes regiões do Azure Olá serviço instância grande HANA está disponível.

configurações específicas de saudação escolhidas dependem da carga de trabalho, os recursos de CPU e memória desejada. É possível Olá tooleverage da carga de trabalho OLTP SKUs que são otimizados para cargas de trabalho OLAP. 

hardware de saudação base para todas as ofertas de saudação são SAP HANA TDI certificados. No entanto, fazemos distinção entre duas classes diferentes de hardware, que divide Olá SKUs em:

- S72, S72m, S144, S144m, S192 e S192m, que chamamos tooas Olá ', classe de tipo' de SKUs.
- S384, S384m, S384xm, S576, S768 e S960, que chamamos tooas Olá 'Classe de tipo II' de SKUs.

É importante toonote um carimbo de instância grande HANA completo não será alocada exclusivamente para um único cliente &#39; s usam. Esse fato aplica toohello racks de recursos de computação e armazenamento conectado por meio de uma malha de rede implantada no Azure também. Infraestrutura do HANA grandes instâncias, como o Azure, implanta o cliente diferentes &quot;locatários&quot; que estão isoladas uma da outra no hello três níveis a seguir:

- Rede: Isolamento por meio de redes virtuais dentro de carimbo de instância grande HANA hello.
- Armazenamento: isolamento por meio de máquinas virtuais de armazenamento que têm volumes de armazenamento atribuídos e isolam volumes de armazenamento entre locatários.
- Computação: Dedicado a atribuição de locatário único de tooa de unidades de servidor. Nenhum particionamento de hardware ou de software das unidades de servidor. Nenhum compartilhamento de uma única unidade de host ou de servidor entre locatários. 

Como tal, implantações de saudação de unidades de grandes instâncias do HANA entre locatários diferentes não são visível tooeach outros. Nem unidades instância grande HANA implantado em diferentes locatários podem se comunicar diretamente com o outro no nível de carimbo de data / instância grande HANA hello. Apenas HANA grande instância unidades dentro de um locatário pode se comunicar tooeach em Olá nível de carimbo de data / instância grande HANA.
Um locatário implantado no carimbo de instância grande Olá recebe tooone prudente e cobrança de assinatura do Azure. No entanto, rede inteligente pode ser acessado a partir VNets do Azure de outras assinaturas do Azure em Olá mesmo registro do Azure. Se você implantar com outra assinatura do Azure no hello mesma região do Azure, você também pode escolher tooask para um locatário de instância grande HANA separado.

Existem diferenças significativas entre executar o SAP HANA em Instâncias Grandes do HANA e executar o SAP HANA em VMs do Azure implantadas no Azure:

- Não há nenhuma camada de virtualização para o SAP HANA no Azure (Instâncias Grandes). Obtenha o desempenho de saudação do hardware subjacente de bare-metal hello.
- Ao contrário do Azure, Olá SAP HANA no servidor do Azure (instâncias grandes) é dedicado tooa específicas do cliente. Não há nenhuma possibilidade de uma unidade de host ou de servidor ter hardware ou software particionado. Como resultado, uma unidade de instância grande HANA é usada como atribuído como um locatário tooa inteira e com que tooyou como um cliente. Uma reinicialização ou desligamento do servidor de saudação não começar automaticamente toohello sistema de operacional e SAP HANA que está sendo implantado em outro servidor. (Para o tipo, classe SKUs, Olá única exceção é se um servidor pode encontrar problemas e reimplantação precisa toobe executada em outro servidor.)
- Ao contrário do Azure, em que tipos de processador do host são selecionados para taxa de preço e desempenho melhor hello, tipos de processador Olá escolhidos para o SAP HANA no Azure (instâncias grandes) são Olá maior desempenho de linha de processador Intel E7v3 e E7v4 hello.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Executando várias instâncias do SAP HANA em uma unidade de Instância Grande do HANA
É toohost possível mais de uma instância ativa do SAP HANA em unidades de instância grande HANA hello. Em ordem toostill oferecem recursos de saudação de instantâneos de armazenamento e recuperação de desastres, essa configuração requer um volume definido por instância. A partir de agora, unidades de instância grande HANA Olá podem ser subdivididas da seguinte maneira:

- S72, S72m, S144, S192: Iniciando unidade em incrementos de 256 GB por 256 GB hello menor. Incrementos diferentes como 256 GB, 512 GB e assim por diante, podem ser combinado toohello máximo de memória de saudação da unidade de saudação.
- S144m e S192m: em incrementos de 256 GB com a menor unidade de saudação de 512 GB. Incrementos diferentes como 512 GB, 768 GB e assim por diante, podem ser combinado toohello máximo de memória de saudação da unidade de saudação.
- Tipo de classe II: em incrementos de 512 GB com hello menor de iniciar a unidade de 2 TB. Incrementos diferentes como 512 GB, 1 TB, 1,5 TB e assim por diante, podem ser combinado toohello máximo de memória de saudação da unidade de saudação.

Alguns exemplos de como executar várias instâncias do SAP HANA seriam semelhantes ao seguinte:

| SKU | Tamanho da memória | Tamanho do Armazenamento | Tamanhos com vários bancos de dados |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1x instância do HANA de 768 GB<br /> ou 1x instância de 512 GB + 1x instância de 256 GB<br /> ou 3x instâncias de 256 GB | 
| S72m | 768 GB | 3 TB | 3x instâncias do HANA de 512GB<br />ou 1x instância de 512 GB + 1x instância de 1 TB<br />ou 6x instâncias de 256 GB<br />ou 1x instância de 1,5 TB | 
| S192m | 4 TB | 16 TB | 8x instâncias de 512 GB<br />ou 4x instâncias de 1 TB<br />ou 4x instâncias de 512 GB + 2x instâncias de 1 TB<br />ou 4x instâncias de 768 GB + 2x instâncias de 512 GB<br />ou 1x instância de 4 TB |
| S384xm | 8 TB | 22 TB | 4x instâncias de 2 TB<br />ou 2x instâncias de 4 TB<br />ou 2x instâncias de 3 TB + 1x instância de 2 TB<br />ou 2x instâncias de 2,5 TB + 1x instância de 3 TB<br />ou 1x instância de 8 TB |


Você obtém ideia hello. Certamente, há também outras variações. 


## <a name="operations-model-and-responsibilities"></a>Responsabilidades e modelo de operações

serviço de saudação fornecido com o SAP HANA no Azure (instâncias grandes) é alinhado com os serviços do Azure IaaS. Você obtém uma instância do HANA em Instâncias Grandes com um sistema operacional instalado otimizado para o SAP HANA. Como com VMs de IaaS do Azure, a maioria das tarefas de saudação de proteção de saudação sistema operacional, instalar software adicional que você precisa instalar HANA, operacional Olá SO e HANA e atualizando Olá SO e HANA é sua responsabilidade. A Microsoft não força atualizações do sistema operacional ou HANA para você.

![Responsabilidades do SAP HANA no Azure (Instâncias Grandes)](./media/hana-overview-architecture/image2-responsibilities.png)

Como você pode ver no diagrama de saudação acima, o SAP HANA no Azure (instâncias grandes) é multilocatário infraestrutura como uma oferta de serviço. E como resultado, divisão de saudação de responsabilidade é no limite de infraestrutura do sistema operacional hello, para hello mais parte. Microsoft é responsável por todos os aspectos do serviço de saudação abaixo da linha de saudação do sistema operacional de saudação e você é responsável acima da linha hello, incluindo o sistema operacional de saudação. Para mais recentes métodos local que você pode aplicar para gerenciamento de conformidade, segurança, gerenciamento de aplicativos, base e sistema operacional podem continuar toobe usado. sistemas de saudação aparecem como se estivessem em sua rede em todos os aspectos.

No entanto, esse serviço é otimizado para SAP HANA, portanto, há áreas em que você e a Microsoft precisam de recursos de infraestrutura subjacente do toowork toouse juntos Olá para obter melhores resultados.

Olá lista a seguir fornece mais detalhes sobre cada uma das camadas de saudação e suas responsabilidades:

**Rede:** todos Olá redes internas para carimbo de instância grande Olá executando SAP HANA, seu armazenamento de toohello access, conectividade entre instâncias de saudação (para expansão e outras funções), paisagem de toohello de conectividade e conectividade tooAzure onde a camada do aplicativo SAP hello está hospedada em máquinas virtuais do Azure. Ele também inclui conectividade WAN entre Data Centers do Azure para replicação de objetivos de Recuperação de Desastre. Todas as redes são particionadas por locatário hello e aplicou QOS.

**Armazenamento:** Olá virtualizado particionado armazenamento para todos os volumes necessários pelos servidores do SAP HANA hello, bem como para instantâneos. 

**Servidores:** Olá dedicado de servidores físicos toorun Olá SAP HANA bancos de dados atribuído tootenants. Olá servidores de hello, classe de tipo de SKUs são abstraído de hardware. Com esses tipos de servidores, a configuração do servidor de saudação é coletada e mantida em perfis, que podem ser movidos de um hardware físico tooanother de hardware físico. Tal uma movimentação (manual) de um perfil por operações pode ser comparada um pouco tooAzure serviço de recuperação. servidores de saudação do hello SKUs de classe de tipo II não oferecem esse recurso.

**SDDC:** centros de software de gerenciamento de saudação dados toomanage usados como entidades definidas pelo software. Ele permite que a Microsoft toopool recursos de motivos de desempenho, disponibilidade e dimensionamento.

**Sistema operacional:** Olá o sistema operacional que você escolher (SUSE Linux ou Red Hat Linux) que é executado em servidores de saudação. imagens de Olá SO que são fornecidas são imagens de Olá fornecidas pelo Olá individuais Linux fornecedor tooMicrosoft para finalidade de saudação da execução do SAP HANA. Você está toohave necessária uma assinatura com o fornecedor do Linux Olá para a imagem Olá específico otimização SAP HANA. Suas responsabilidades incluem o registro de imagens de saudação com o fornecedor do sistema operacional hello. Do ponto de saudação de passar pela Microsoft, você também é responsável por qualquer ainda mais a aplicação de patch do sistema de operacional Linux hello. Esse patch também inclui pacotes adicionais que podem ser necessários para uma instalação bem-sucedida do HANA SAP (consulte da tooSAP documentação de instalação do HANA e observações sobre o SAP) e que não foram incluídas pelo fornecedor de Linux específico Olá em seus SAP HANA otimização de imagens do sistema operacional. responsabilidade de saudação do cliente Olá também inclui a aplicação de patch de hello, sistema operacional é toomalfunction/otimização relacionada do hello sistema operacional e o hardware de servidor específico drivers toohello relacionados. Ou qualquer segurança ou funcional aplicação de patch de sistema operacional do hello. Também é responsabilidade do cliente monitorar e planejar a capacidade do(s):

- Consumo de recursos de CPU
- Consumo de memória
- Espaço em disco volumes toofree relacionados, IOPS e latência
- Tráfego de volume de rede entre o Hana Instância Grande e a camada do aplicativo SAP

infraestrutura subjacente de saudação do HANA grandes instâncias fornece a funcionalidade de backup e restauração de volume do sistema operacional hello. Usar essa funcionalidade também é sua responsabilidade.

**Middleware:** Olá a instância do SAP HANA, principalmente. Administração, operações e monitoramento são de sua responsabilidade. Não há funcionalidade fornecida que permite a você toouse instantâneos de armazenamento para fins de recuperação de desastres e backup/restauração. Esses recursos são fornecidos pela infraestrutura de saudação. No entanto, suas responsabilidades incluem também a criação de um design de Alta Disponibilidade ou Recuperação de Desastre com essas funcionalidades, aproveitando-as e monitorando para conferir que instantâneos de armazenamento tenham sido executados com êxito.

**Dados:** seus dados gerenciados pelo SAP HANA e outros dados, como backups de arquivos localizados em volumes ou compartilhamentos de arquivos. Suas responsabilidades incluem monitoramento de espaço livre em disco e gerenciamento de conteúdo de saudação em volumes hello e monitorando a execução bem-sucedida do Olá dos backups de volumes de disco e instantâneos de armazenamento. No entanto, a execução bem-sucedida dos sites de tooDR de replicação de dados é responsabilidade de saudação do Microsoft.

**Aplicativos:** Olá instâncias de aplicativos SAP ou, no caso de aplicativos não-SAP, camada de aplicativo hello desses aplicativos. Suas responsabilidades incluem a implantação, administração, operações e monitoramento desses aplicativos relacionados toocapacity planejamento de consumo de recursos de CPU, consumo de memória, consumo de armazenamento do Azure e consumo de largura de banda de rede em VNets do Azure e a partir do Azure VNets tooSAP HANA no Azure (instâncias grandes).

**WANs:** Olá conexões estabelecer de implantações de tooAzure local para cargas de trabalho. Todos os nossos clientes de Instâncias Grandes do HANA usam o Azure ExpressRoute para conectividade. Esta conexão não é parte da saudação SAP HANA na solução do Azure (instâncias grandes), você é responsável pela instalação de saudação dessa conexão.

**Arquivamento:** talvez você prefira tooarchive cópias de dados usando seus próprios métodos nas contas de armazenamento. O arquivamento requer gerenciamento, conformidade, custos e operações. Você é responsável por gerar cópias de arquivos e backups no Azure e armazená-los de uma maneira em conformidade.

Consulte Olá [SLA para o SAP HANA no Azure (instâncias grandes)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Dimensionamento

O dimensionamento do HANA em Instâncias Grandes não é diferente de dimensionamento para o HANA em geral. Existentes e a implantação de sistemas, você deseja toomove de outros tooHANA RDBMS, SAP fornece vários relatórios que são executados em seus sistemas SAP. Se o banco de dados de saudação tooHANA movido, esses relatórios verificar Olá dados e calculam requisitos de memória para a instância do HANA hello. Olá Observações sobre o SAP tooget a seguir para obter mais informações em como toorun esses relatórios e como tooobtain seus patches/versões mais recentes:

- [Nota SAP nº 1793345 – Dimensionamento do SAP Suite no HANA](https://launchpad.support.sap.com/#/notes/1793345)
- [Nota SAP nº 1872170 – Relatório de dimensionamento do Suite no HANA e S/4 HANA](https://launchpad.support.sap.com/#/notes/1872170)
- [Nota SAP nº 2121330 – Perguntas frequentes: relatório de dimensionamento do SAP BW no HANA](https://launchpad.support.sap.com/#/notes/2121330)
- [Nota SAP nº 1736976 – Relatório de dimensionamento do BW no HANA](https://launchpad.support.sap.com/#/notes/1736976)
- [Nota SAP nº 2296290 – Novo relatório de dimensionamento do BW no HANA](https://launchpad.support.sap.com/#/notes/2296290)

Para implementações de campo verde, dimensionar rápido SAP é requisitos de memória disponível toocalculate da implementação de saudação do software SAP na parte superior do HANA.

Requisitos de memória para HANA estão aumentando à medida que aumenta o volume de dados, para que você deseja toobe com reconhecimento de saudação consumo de memória agora e ser capaz de toopredict o que é toobe contínuo em Olá futuras. Com base nos requisitos de memória Olá, é possível mapear a demanda em uma saudação HANA grande SKUs de instância.

## <a name="requirements"></a>Requisitos

Estes são os requisitos para execução SAP HANA no Azure (Instâncias Grandes).

**Microsoft Azure:**

- Uma assinatura do Azure que pode ser vinculados tooSAP HANA no Azure (instâncias grandes).
- Contrato do Suporte Premier da Microsoft. Consulte [2015553 de n º de observação de suporte do SAP – SAP no Microsoft Azure: pré-requisitos de suporte](https://launchpad.support.sap.com/#/notes/2015553) para obter informações específicas relacionadas toorunning SAP no Azure. Com unidades de instância grande HANA 384 e mais CPUs, é necessário também Olá tooextend tooinclude de contrato de suporte Premier resposta rápida do Azure (ARR).
- Reconhecimento de instâncias do hello HANA grandes SKUs é necessário depois de executar um dimensionamento exercício com o SAP.

**Conectividade de rede:**

- Rota expressa do Azure entre locais tooAzure: tooconnect seu tooAzure de datacenter local, certifique-se de que tooorder pelo menos uma conexão Gbps 1 de seu ISP. 

**Sistema operacional:**

- Licenças para SUSE Linux Enterprise Server 12 para aplicativos SAP.

> [!NOTE] 
> saudação de sistema operacional fornecido pela Microsoft não está registrada com o SUSE nem está conectado com uma instância SMT.

- O SMT da assinatura do SUSE Linux é implantado no Azure em uma VM do Azure. Isso fornece a capacidade de saudação para o SAP HANA no Azure (instâncias grandes) toobe registrados e respectivamente atualizados pelo SUSE (pois não há nenhum acesso à internet no data center do HANA grandes instâncias). 
- Licenças para Red Hat Enterprise Linux 6.7 ou 7.2 para SAP HANA.

> [!NOTE]
> Olá sistema operacional fornecido pela Microsoft não está registrado com o Red Hat, nem é it conectado tooa Red Hat assinatura Manager instância.

- Gerenciador do Red Hat assinatura implantado no Azure em uma VM do Azure. Olá Red Hat assinatura Manager fornece a capacidade de Olá para o SAP HANA no Azure (instâncias grandes) toobe registrados e respectivamente atualizados pelo Red Hat (pois não há nenhum acesso direto à internet de dentro do locatário Olá implantado no carimbo de instância grande Azure Olá).
- SAP requer toohave um suporte entrar em contato com seu fornecedor do Linux. Esse requisito não é apagado pela solução de saudação do HANA grandes instâncias ou hello fato que o Linux em execução no Azure. Ao contrário com algumas imagens de galeria do Azure do Linux Olá, taxa de saudação do serviço não está incluída na oferta de solução de saudação do HANA grandes instâncias. É você como um cliente toofulfill Olá requisitos do SAP sobre contratos de suporte com o distribuidor do Linux hello.   
   - Para SUSE Linux, pesquisar Olá requisitos de suporte de contrato no [1984787 de # nota SAP - SUSE LINUX Enterprise Server 12: notas de instalação](https://launchpad.support.sap.com/#/notes/1984787) e [SAP Observação #1056161 - SUSE prioridade oferecem suporte para aplicativos SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Para Red Hat Linux, você precisa de níveis de assinatura correta de saudação toohave que incluem o suporte e o serviço (atualizações de sistemas operacionais de toohello do HANA grandes instâncias. O Red Hat recomenda obter uma assinatura "RHEL for SAP Business Applications". Com relação a suporte e serviços, confira [Nota SAP nº 2002167 – Red Hat Enterprise Linux 7.x: Instalação e atualização](https://launchpad.support.sap.com/#/notes/2002167) e [Nota SAP nº 1496410 – Red Hat Enterprise Linux 6.x: Instalação e atualização](https://launchpad.support.sap.com/#/notes/1496410) para obter detalhes.

**Banco de dados:**

- As licenças e os componentes de instalação de software para SAP HANA (plataforma ou enterprise edition).

**Aplicativos:**

- Licenças e os componentes de instalação de software para todos os aplicativos SAP conectando tooSAP HANA e contratos de suporte relacionados do SAP.
- Licenças e os componentes de instalação de software para todos os aplicativos SAP não usado na relação tooSAP HANA no ambiente do Azure (instâncias grandes) e relacionadas a contratos de suporte.

**Habilidades:**

- Experiência e conhecimento sobre IaaS do Azure e seus componentes.
- Experiência e conhecimento sobre a implantação da carga de trabalho do SAP no Azure.
- Instalação do SAP HANA certificados pessoal.
- SAP arquiteto habilidades toodesign alta disponibilidade e recuperação de desastres em torno do SAP HANA.

**SAP:**

- Expectativa é que você seja um cliente do SAP e tenha suporte de um contrato com o SAP
- Especialmente para implementações de saudação classe de tipo II de SKUs do HANA grande instância, é altamente recomendável tooconsult com o SAP em versões do HANA SAP e eventuais configurações em hardware de expansão de tamanho grande.


## <a name="storage"></a>Armazenamento

Olá layout de armazenamento para o SAP HANA no Azure (instâncias grandes) é configurado pelo SAP HANA no gerenciamento de serviço do Azure por meio de SAP recomendado diretrizes, documentadas no hello [requisitos de armazenamento do SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper.

Olá HANA grandes instâncias de tipo, classe de hello vêm com o volume de memória Olá quatro vezes como volume de armazenamento. Olá tipo de classe II de unidades de instância grande HANA, armazenamento Olá não vai toobe mais quatro vezes. unidades de saudação vem com um volume, o que deve é usado para armazenar backups de log de transações do HANA. Para obter mais detalhes em [como tooinstall e configure o SAP HANA (instâncias grandes) no Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consulte Olá em termos de alocação de armazenamento a tabela a seguir. tabela de saudação aproximadamente lista capacidade Olá para volumes de diferentes Olá fornecido com diferentes unidades de instância grande HANA hello.

| SKU de Instância Grande do HANA | hana/data | Hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3.328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4.608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11.520 GB | 1536 GB | 1.792 GB | 1536 GB |
| S384 | 11.520 GB | 1536 GB | 1.792 GB | 1536 GB |
| S384m | 12.000 GB | 2.050 GB | 2.050 GB | 2.040 GB |
| S384xm | 16.000 GB | 2.050 GB | 2.050 GB | 2.040 GB |
| S576 | 20.000 GB | 3.100 GB | 2.050 GB | 3.100 GB |
| S768 | 28.000 GB | 3.100 GB | 2.050 GB | 3.100 GB |
| S960 | 36.000 GB | 4.100 GB | 2.050 GB | 4.100 GB |


Volumes implantados reais podem variar um pouco com base na implantação e a ferramenta de tamanhos de volume Olá tooshow usado.

Se você subdividir um SKU de Instância Grande do HANA, alguns exemplos de partes de divisão possíveis pareceriam com:

| Partição de memória em GB | hana/data | Hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1.792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3.328 GB | 768 GB | 1280 GB | 768 GB |


Esses tamanhos são números de volume aproximada que podem variar ligeiramente com base na implantação e ferramentas usadas toolook em volumes de saudação. Também há outros tamanhos de partição possíveis, como 2,5 TB. Esses tamanhos de armazenamento serão calculados com uma fórmula semelhante usados para partições de saudação acima. termo de saudação 'partições' não indica que recursos de CPU, memória ou sistema operacional de saudação são de qualquer forma particionados. Ele indica apenas partições de armazenamento para instâncias HANA diferentes Olá talvez você queira toodeploy em um uma unidade de instância grande HANA. 

É necessário como um cliente pode ter mais armazenamento, você terá Olá possibilidade tooadd toopurchase adicionais de armazenamento em unidades de 1 TB. Esse armazenamento adicional pode ser adicionado como volume adicional ou pode ser usado tooextend um ou mais dos volumes existentes hello. Não é toodecrease possíveis tamanhos de saudação de volumes hello como implantado originalmente e documentado principalmente pelo Olá tabela (s) acima. Também não é possível toochange Olá nomes de volumes de saudação ou de montagem. volumes de armazenamento Olá conforme descrito acima são unidades de instância grande HANA toohello anexado como NFS4 volumes.

Você, como um cliente pode escolher toouse instantâneos de armazenamento para backup/restauração e desastres fins de recuperação. Mais detalhes sobre esse tópico são fornecidos em [Alta disponibilidade e recuperação de desastre do SAP HANA (instâncias grandes) no Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Criptografia de dados em repouso
armazenamento Olá usado para instâncias grandes HANA permite uma criptografia transparente de dados Olá conforme eles são armazenados em discos de saudação. No momento da implantação de uma unidade de instância HANA grandes, você tem a saudação opção toohave esse tipo de criptografia habilitada. Você também pode escolher toochange tooencrypted volumes depois da implantação de saudação já. Olá movimentação dos volumes tooencrypted não criptografado é transparente e não requer um tempo de inatividade. 

Com a saudação tipo, classe SKUs, inicialização de saudação do volume Olá LUN é armazenado no, é criptografada. No caso de tipo hello classe II de SKUs do HANA grandes instâncias, é necessário tooencrypt Olá LUN de inicialização com métodos de sistema operacional. 


## <a name="networking"></a>Rede

arquitetura de saudação de rede do Azure é uma implantação de toosuccessful de componente-chave de aplicativos SAP HANA grandes instâncias. Normalmente, as implantações do SAP HANA no Azure (Instâncias Grandes) têm uma estrutura SAP maior com diversas soluções SAP com vários tamanhos de bancos de dados, consumo de recursos de CPU e a utilização de memória. É muito provável que nem todos esses sistemas SAP se baseiem no SAP HANA, de forma que seu cenário SAP provavelmente seja um híbrido que utiliza:

- Sistemas SAP implantados no local. Devido a tootheir tamanhos, esses sistemas atualmente não podem ser hospedados no Azure. um exemplo clássico seria um sistema de ERP SAP de produção em execução no Microsoft SQL Server (como o banco de dados Olá) que requer mais CPU ou podem fornecer recursos de memória de máquinas virtuais do Azure.
- Sistemas SAP baseados em SAP HANA implantados localmente.
- Sistemas SAP implantados em VMs do Azure. Esses sistemas podem estar em desenvolvimento, teste, a área restrita, ou instâncias de produção para qualquer um dos aplicativos baseados no SAP NetWeaver Olá que podem implantar com êxito no Azure (em máquinas virtuais), com base na demanda de memória e consumo de recursos. Esses sistemas também pode ser baseados em bancos de dados como o SQL Server (consulte [Nota de Suporte SAP n. 1928533 – Aplicativos SAP no Azure: tipos de VM do Azure e produtos com suporte](https://launchpad.support.sap.com/#/notes/1928533/E)) ou SAP HANA (consulte [Plataformas IaaS certificadas do SAP HANA](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- Servidores de aplicativos SAP implantados no Azure (em VMs) que aproveitam o SAP HANA no Azure (Instância Grande) em carimbos de Instância Grande do Azure.

Enquanto um cenário de SAP (com quatro ou mais diferentes cenários de implantação) híbrido é típico, há muitos casos de cliente com cenário de SAP completo em execução no Azure. Como VMs do Microsoft Azure estão se tornando mais potentes, aumento do número de saudação de clientes mover todas as suas soluções do SAP no Azure.

Rede no contexto de saudação de sistemas SAP implantados no Azure do Azure não é complicado. Ele se baseia Olá princípios a seguir:

- Redes virtuais do Azure (VNets) necessário circuito de rota expressa do Azure de toohello toobe conectado que se conecta a rede local tooon.
- Um circuito de rota expressa conexão local tooAzure geralmente deve ter uma largura de banda de 1 Gbps ou superior. Essa largura de banda mínima permite que a largura de banda adequada para transferir dados entre sistemas locais e em execução em máquinas virtuais do Azure (bem como sistemas de tooAzure de conexão de usuários finais no local).
- Todos os sistemas SAP no Azure necessidade toobe definidos no toocommunicate VNets do Azure com o outro.
- O Active Directory e o DNS hospedados localmente são estendidos para o Azure por meio do ExpressRoute por meio do local.


> [!NOTE] 
> Do ponto de vista cobrança apenas uma única assinatura do Azure pode ser vinculada somente tooone único locatário em um carimbo de instância grande em uma região do Azure específica e, por outro lado um único locatário de carimbo de data / instância grande pode ser vinculado somente tooone assinatura do Azure. Esse fato é tooany não são diferente de outros faturáveis objetos no Azure

Resulta em um locatário separada toobe Implantando HANA SAP no Azure (instâncias grandes) em várias regiões do Azure diferentes, implantado em Olá carimbo da instância grande. No entanto, você pode executar ambos no hello cenário de SAP mesmo com a mesma assinatura do Azure, desde que essas instâncias são parte da saudação. 

> [!IMPORTANT] 
> Implantação de gerenciamento de recursos do Azure só é compatível com SAP HANA no Azure (Instâncias Grandes).

 

### <a name="additional-azure-vnet-information"></a>Informações adicionais de rede virtual do Azure

Na ordem tooconnect tooExpressRoute uma rede virtual do Azure, um gateway do Azure deve ser criado (consulte [sobre gateways de rede virtual para o ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Um gateway do Azure pode ser usado com a infraestrutura do ExpressRoute tooan fora do Azure (ou carimbo da instância do Azure grande tooan), ou tooconnect entre VNets do Azure (consulte [configurar uma conexão de rede virtual a rede para o Gerenciador de recursos usando o PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Você pode conectar hello Azure gateway tooa máximo, quatro diferentes conexões de rota expressa como essas conexões são provenientes de roteadores MS Enterprise bordas (MSEE) diferentes.  Para obter mais informações, consulte [Infraestrutura e conectividade do SAP HANA (instâncias grandes) no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Olá taxa de transferência fornece um gateway do Azure é diferente para os dois casos de uso (consulte [sobre o Gateway de VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). taxa de transferência máxima Olá que podemos alcançar com um gateway de rede virtual é de 10 Gbps, usando uma conexão de rota expressa. Tenha em mente que copiar arquivos entre uma VM do Azure que residem em uma rede virtual do Azure e um sistema local (como um fluxo de cópia única) não atingir a taxa de transferência total de gateway diferente de saudação SKUs hello. tooleverage Olá completa largura de banda do gateway de rede virtual hello, você deve usar vários fluxos ou arquivos diferentes de cópia em fluxos paralelos de um único arquivo.


### <a name="networking-architecture-for-hana-large-instances"></a>Arquitetura de rede para Instâncias Grandes do HANA
Olá a arquitetura de rede para grandes instâncias do HANA conforme mostrado abaixo, pode ser separada em quatro partes diferentes:

- Local de rede e tooAzure de conexão de rota expressa. Esta parte é o domínio de clientes de saudação e tooAzure conectado por meio de rota expressa. Isso faz parte de saudação no canto direito inferior do gráfico de saudação abaixo hello.
- Rede do Azure conforme discutido acima com VNets do Azure, que novamente têm gateways. Essa é uma área em que você precisa designs apropriado do toofind Olá para seus requisitos de aplicativos, segurança e requisitos de conformidade. Usando as instâncias grandes HANA é outro ponto de consideração em termos de número de VNets e o Azure toochoose SKUs de gateway do. Isso faz parte de saudação no canto superior direito Olá dos gráficos de saudação.
- Conectividade de Instâncias Grandes do HANA por meio da tecnologia do ExpressRoute no Azure. Essa parte é implantada e feita pela Microsoft. Você só precisa toodo como um cliente é tooprovide alguns intervalos de endereços IP e depois da implantação de saudação de seus ativos na conexão do HANA grandes instâncias Olá rota expressa circuito toohello VNet(s) do Azure (consulte [infra-estrutura do SAP HANA (grandes instâncias) e conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Rede em Instâncias Grandes do HANA, o que geralmente é transparente para você como um cliente.

![Rede virtual do Azure conectado tooSAP HANA no Azure (instâncias grandes) e no local](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

fato Olá que você use HANA grandes instâncias não altera Olá requisito tooget seus ativos locais são conectados por meio de tooAzure de rota expressa. Ele também altera requisito Olá para ter uma ou várias VNets que executam máquinas virtuais do Azure Olá qual camada de aplicativo hello host que conecta-se a instâncias do HANA toohello hospedadas em unidades de instância grande HANA. 

Olá diferença tooSAP implantações puro Azure, vem com fatos Olá que:

- unidades de instância grande HANA saudação do seu locatário do cliente são conectadas por meio de outro circuito de rota expressa em seu VNet(s) do Azure. Em condições de carga de tooseparate ordem, Olá Olá local tooAzure VNets ExpressRoute links e links entre os VNets do Azure e HANA grandes instâncias não compartilham mesmo roteadores.
- perfil de carga de trabalho de saudação entre a camada do aplicativo SAP hello e hello HANA instância é uma natureza diferente de muitas solicitações de pequenas e intermitência como dados transfere (conjuntos de resultados) do SAP HANA na camada de aplicativo hello.
- Olá arquitetura do aplicativo SAP é mais confidencial latência toonetwork cenários típicos onde dados obtém trocados entre local e o Azure.
- gateway de rede virtual Olá tem pelo menos duas conexões de rota expressa e ambas as conexões compartilham largura de banda máxima para dados de entrada do gateway de rede virtual Olá Olá.

latência de rede Olá experiente entre máquinas virtuais do Azure e unidades de instância HANA grande pode ser maior que um típica latência ida e volta da rede de máquina virtual para virtual. Dependente Olá região do Azure, os valores hello medidos podem exceder latência completa do ms 0,7 Olá classificada como abaixo da média em [1100926 de # nota SAP - perguntas Frequentes: desempenho de rede](https://launchpad.support.sap.com/#/notes/1100926/E). Mesmo assim, os clientes implantaram aplicativos SAP de produção com base no SAP HANA muito com êxito em Instâncias Grandes do SAP HANA. os clientes de saudação que implantaram relataram grandes melhorias executando seus aplicativos SAP no SAP HANA usando unidades de instância grande HANA. No entanto, você deve testar os processos de negócios integralmente em Instâncias Grandes do HANA no Azure.
 
Na latência de rede determinística ordem tooprovide entre máquinas virtuais do Azure e instância grande HANA, a escolha de saudação do hello SKU de Gateway de rede virtual do Azure é essencial. Ao contrário de padrões de tráfego de saudação entre locais e VMs do Azure, padrão do hello tráfego entre máquinas virtuais do Azure e HANA grandes instâncias pode desenvolver intermitências pequenas, mas alta de solicitações e toobe de volumes de dados transmitidos. Na ordem toohave esses picos tratados, é altamente recomendável uso Olá Olá UltraPerformance SKU de Gateway. Para Olá classe de tipo II de SKUs do HANA grande instância, o uso de saudação do gateway de UltraPerformance Olá SKU como Gateway de rede virtual do Azure é obrigatório.  

> [!IMPORTANT] 
> Fornecido Olá geral tráfego de rede entre o aplicativo do SAP hello e camadas de banco de dados, somente Olá HighPerformance ou gateway UltraPerformance SKUs para VNets tem suporte para conexão tooSAP HANA no Azure (instâncias grandes). Para a instância grande HANA tipo II SKUs, Olá UltraPerformance SKU de Gateway é suportado como Gateway de rede virtual do Azure.



### <a name="single-sap-system"></a>Único sistema SAP

infraestrutura local de saudação mostrada acima é conectada por meio de rota expressa no Azure e Olá circuito de rota expressa conecta-se em um roteador de borda do Microsoft Enterprise (MSEE) (consulte [visão geral técnica do ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Uma vez estabelecido, essa rota que se conecta backbone do Microsoft Azure hello e todas as regiões do Azure são acessíveis.

> [!NOTE] 
> Para executar os cenários SAP no Azure, conecte-se toohello mais próximo do toohello MSEE região do Azure no ambiente do SAP hello. Carimbos de instância grande do Azure são conectados por meio de dedicado MSEE dispositivos toominimize latência de rede entre VMs do Azure no IaaS do Azure e instância grande carimbos.

gateway de rede virtual para Olá VMs do Azure, hospedam instâncias do aplicativo SAP, Hello é conectado toothat circuito de rota expressa e mesma rede virtual hello é conectado tooa separada MSEE roteador dedicado tooconnecting tooLarge instância carimbos.

Este é um exemplo simples de um sistema SAP, onde hello camada do aplicativo SAP é hospedada no Azure e banco de dados do SAP HANA Olá é executado no SAP HANA no Azure (instâncias grandes). Olá suposição é a largura de banda de gateway de rede virtual que Olá de 2 Gbps ou taxa de transferência de 10 Gbps não representa um afunilamento.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Vários sistemas SAP ou grandes sistemas SAP

Se vários sistemas SAP ou grandes sistemas SAP são implantados conectando tooSAP HANA no Azure (instâncias grandes), ele &#39; a taxa de transferência do s tooassume razoável saudação do gateway de rede virtual Olá pode se tornar um afunilamento. Nesse caso, você precisa de camadas do aplicativo hello toosplit em múltiplas VNets do Azure. Ele também pode ser recomendável toocreate VNets especial que se conectam tooHANA grandes instâncias para casos, como:

- Executar backups diretamente da saudação HANA instâncias tooa HANA grandes instâncias VM no Azure que hospeda compartilhamentos de NFS
- Copiando backups grandes ou outros arquivos de instância grande HANA unidades toodisk espaço gerenciado no Azure.

Usando VNets separadas que VMs que gerencia o armazenamento de saudação do host evita impacto por arquivos grandes ou transferência de dados do HANA grandes instâncias tooAzure em Olá Gateway de rede virtual que serve Olá VMs em execução a camada do aplicativo SAP hello. 

Uma arquitetura de rede mais escalonável:

- Aproveite diversas redes virtuais do Azure para uma camada de aplicativo SAP única e maior.
- Implantar uma VNet do Azure separado para cada sistema SAP, comparado toocombining esses sistemas SAP em sub-redes separadas em Olá mesma rede virtual.

 Uma arquitetura de rede mais escalonável para o SAP HANA no Azure (Instâncias Grandes):

![Implantação de camada do aplicativo SAP em várias redes virtuais do Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Implantar a camada do aplicativo SAP hello, ou componentes, por múltiplas VNets do Azure, como mostrado acima, introduziu a sobrecarga de latência inevitável que ocorreu durante a comunicação entre aplicativos Olá hospedado nas VNets do Azure. Por padrão, o tráfego de rede Olá entre máquinas virtuais do Azure localizado na rota VNets diferente por meio de saudação roteadores MSEE nessa configuração. No entanto, desde setembro de 2016, esse roteamento pode ser otimizado. Olá toooptimize de maneira e reduzir a latência de saudação na comunicação entre dois VNets por emparelhamento VNets do Azure em Olá mesma região. Mesmo que essas VNets estejam em assinaturas diferentes. Usando a rede virtual do Azure emparelhamento, comunicação de saudação entre VMs em dois VNets diferentes do Azure pode usar hello Azure rede backbone toodirectly comunicam entre si. Assim, mostrando a latência semelhantes como se Olá VMs estaria em Olá mesma rede virtual. Enquanto o tráfego, o endereçamento de intervalos de endereços IP que são conectados por meio do gateway de rede virtual do Azure Olá, é roteado por Olá individual gateway de rede virtual de saudação VNet. Você pode obter detalhes sobre a rede virtual do Azure emparelhamento no artigo Olá [emparelhamento VNet](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Roteamento no Azure

Há duas considerações de roteamento de rede importantes para SAP HANA no Azure (Instâncias Grandes):

1. SAP HANA no Azure (instâncias grandes) só pode ser acessado por máquinas virtuais do Azure na conexão de rota expressa Olá dedicado; não diretamente no local. Alguns clientes de administração e quaisquer aplicativos que precisam de acesso direto, como o SAP Solution Manager em execução no local, não é possível conectar o banco de dados do SAP HANA toohello.

2. SAP HANA em unidades do Azure (instâncias grandes) tem um endereço IP atribuído do endereço do Pool de IP do servidor de saudação intervalo você como cliente de saudação enviado (consulte [infra-estrutura do SAP HANA (grandes instâncias) e a conectividade no Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes).  Esse endereço IP é acessível por meio de hello Azure assinaturas e rota expressa que se conecta tooHANA VNets do Azure no Azure (instâncias grandes). Olá endereço IP atribuído fora desse intervalo de endereços do Pool de IP do servidor está diretamente atribuído toohello unidade de hardware e não é NAT'ed mais como era caso Olá em implantações de primeira Olá dessa solução. 

> [!NOTE] 
> Se você precisa tooconnect tooSAP HANA no Azure (instâncias grandes) em um _do data warehouse_ cenário, em que os aplicativos e/ou usuários finais necessário tooconnect toohello SAP HANA banco de dados (executado diretamente), deve ser outro componente de rede usado: um proxy reverso tooroute dados, tooand do. Por exemplo, F5 BIG-IP, NGINX com o Gerenciador de Tráfego implantado no Azure como uma solução de roteamento de tráfego/firewall virtual.

### <a name="internet-connectivity-of-hana-large-instances"></a>Conectividade com a Internet das Instâncias Grandes do HANA
As Instâncias Grandes do HANA NÃO têm conectividade direta com a Internet. Isso está restringindo suas habilidades para, por exemplo registrar a imagem do sistema operacional Olá diretamente com o fornecedor do sistema operacional hello. Portanto, talvez seja necessário toowork com o servidor SMT SLES local ou RHEL Gerenciador de assinatura

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Criptografia de dados entre VMs do Azure e Instâncias Grandes do HANA
Os dados transferidos entre as Instâncias Grandes do HANA e as VMs do Azure não são criptografados. No entanto, apenas para exchange Olá entre hello lado HANA DBMS e aplicativos com base em JDBC/ODBC, você pode habilitar criptografia de tráfego. Consulte [esta documentação da SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Usando unidades de Instância Grande do HANA em várias regiões

Você pode ter outros motivos toodeploy HANA SAP no Azure (instâncias grandes) em várias regiões do Azure, além de recuperação de desastres. Talvez você queira tooaccess HANA grandes instâncias de cada uma das VMs Olá implantadas em Olá VNets diferentes em regiões de saudação. Como os endereços IP de saudação atribuídos toohello diferente unidades HANA grandes instâncias não são propagadas além Olá VNets do Azure (que estão diretamente conectados por meio de suas instâncias de toohello de gateway), não há um pouco alterar toohello introduzido acima de design de rede virtual: um Gateway de rede virtual do Azure pode lidar com quatro diferentes circuitos do ExpressRoute sem MSEEs diferentes, e cada rede virtual que está conectada tooone de carimbos de instância grande Olá pode ser conectado toohello o carimbo de data / instância grande em outra região do Azure.

![VNets do Azure conectado tooAzure carimbos de instância grande em diferentes regiões do Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Olá acima mostra a figura como Olá diferentes VNets do Azure em ambas as regiões são circuitos ExpressRoute de diferentes tootwo conectados que são usadas tooconnect tooSAP HANA no Azure (instâncias grandes) em ambas as regiões do Azure. conexões de saudação introduzida recentemente são linhas vermelhas retangular de saudação. Com essas conexões, fora do hello VNets do Azure, Olá VMs em execução em um desses VNets podem acessar cada uma das unidades HANA grandes instâncias diferentes Olá implantadas em duas regiões de saudação. Como ver nos gráficos de saudação acima, presume-se que você tenha duas conexões de rota expressa do local toohello duas regiões do Azure; é recomendável por questões de recuperação de desastres.

> [!IMPORTANT] 
> Se forem usados vários circuitos de rota expressa, acrescentando caminho porque e configurações BGP de preferência Local devem ser usado tooensure adequada de roteamento de tráfego.


