---
title: "aaaGetting iniciado com a segurança do Microsoft Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral dos recursos de segurança do Microsoft Azure e as considerações gerais para organizações que estão migrando de seu provedor de nuvem tooa ativos."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Introdução à segurança do Microsoft Azure
Quando você compila ou migra o provedor de nuvem de tooa de ativos de TI, você depender de tooprotect de recursos da organização seus aplicativos e dados com controles de saudação eles oferecem toomanage Olá segurança de seus ativos com base em nuvem e serviços hello.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender às suas necessidades de segurança. Além disso, Azure fornece uma ampla gama de segurança configuráveis toocontrol de capacidade de opções e hello-los para que você possa personalizar requisitos exclusivos de saudação do toomeet de segurança de suas implantações.

Neste artigo de visão geral sobre a segurança do Azure, examinaremos:

* Os serviços do Azure e recursos que você pode usar toohelp protegem seus serviços e dados no Azure.
* Como a Microsoft protege Olá toohelp de infraestrutura do Azure protegem seus dados e aplicativos.

## <a name="identity-and-access-management"></a>Gerenciamento de identidade e de acesso
Controlando a infraestrutura de acesso tooIT, dados e aplicativos é essencial. O Microsoft Azure oferece esses recursos por meio de serviços, como o Azure Active Directory (Azure AD), o Armazenamento do Azure e o suporte a vários padrões e APIs.

O [Azure AD](../active-directory/active-directory-whatis.md) é um repositório de identidades e mecanismo que fornece autenticação, autorização e controle de acesso para usuários, grupos e objetos de uma organização. O AD do Azure também oferece aos desenvolvedores um gerenciamento de identidade toointegrate de maneira efetiva em seus aplicativos. Os protocolos padrão do setor, como [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) e [OpenID Connect](http://openid.net/connect/) possibilitam o acesso a plataformas, como .NET, Java, Node.js e PHP.

Olá baseado em REST API do Graph permite que os desenvolvedores tooread e gravação toohello diretório de qualquer plataforma. Por meio do suporte para [OAuth 2.0](http://oauth.net/2/), os desenvolvedores podem criar aplicativos Web e para dispositivos móveis que se integram às APIs da Web de terceiros e da Microsoft, bem como criar suas próprias APIs da Web seguras. As bibliotecas de cliente de software livre estão disponíveis para .Net, Windows Store, iOS e Android, e ainda há novas bibliotecas em desenvolvimento.

### <a name="how-azure-enables-identity-and-access-management"></a>Como o Azure habilita o gerenciamento de identidade e de acesso
O AD do Azure pode ser usado como um diretório de nuvem autônomo para sua organização ou como uma solução integrada ao Active Directory local existente. Alguns recursos de integração incluem a sincronização de diretórios e o logon único (SSO). Esses estendem o alcance de saudação de suas identidades locais existentes para a nuvem hello e melhorar a experiência de administrador e usuário hello.

Alguns outros recursos para gerenciamento de identidade e acesso incluem:

* Habilita do AD do Azure [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS aplicativos, independentemente de onde eles estão hospedados. Alguns aplicativos são federados com o AD do Azure e outros usam SSO com senha. Os aplicativos federados também podem dar suporte ao provisionamento do usuário e o armazenamento de senha no cofre.
* Acesso toodata em [armazenamento do Azure](https://azure.microsoft.com/services/storage/) é controlado através da autenticação. Cada conta de armazenamento tem uma chave primária ([chave da conta de armazenamento](https://msdn.microsoft.com/library/azure/ee460785.aspx), ou SAK) e uma chave de segredo secundária (assinatura de acesso compartilhado hello, ou SAS).
* O Azure AD fornece identidade como um serviço de federação usando [Serviços de Federação do Active Directory](../active-directory/fundamentals-identity.md), sincronização e replicação com diretórios locais.
* [Autenticação multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md) é o serviço de autenticação multifator Olá que exige que os usuários tooverify entradas usando um aplicativo móvel, chamada telefônica ou mensagem de texto. Ele pode ser usado com recursos do AD do Azure toohelp local seguro com o servidor de autenticação multifator do Azure Olá e também com diretórios usando Olá SDK e aplicativos personalizados.
* [Serviços de domínio do AD do Azure](https://azure.microsoft.com/services/active-directory-ds/) permite você entrar no domínio de tooa de máquinas virtuais do Azure sem implantar controladores de domínio. Você pode entrar em máquinas virtuais de toothese com suas credenciais corporativas do Active Directory e administrar computadores que ingressaram no domínio virtual com linhas de base de segurança de tooenforce política de grupo em todas as suas máquinas virtuais do Azure.
* [B2C de diretório ativo do Azure](https://azure.microsoft.com/services/active-directory-b2c/) fornece um serviço de gerenciamento de identidade global altamente disponíveis para aplicativos voltados para o consumidor que pode ser dimensionado toohundreds de milhões de identidades. Ele pode ser integrado a plataformas móveis e da Web. Seus consumidores podem entrar tooall seus aplicativos por meio de experiências personalizáveis com suas contas sociais existentes ou criando novas credenciais.

## <a name="data-access-control-and-encryption"></a>Controle de acesso de dados e criptografia
Microsoft emprega princípios de saudação de separação de tarefas e [privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) durante operações do Azure. Acesso toodata pela equipe de suporte do Azure requer a permissão explícita e é concedida em uma base de "just-in-time" que é registrada e auditada, em seguida, revogado após a conclusão do contrato de saudação.

O Azure também oferece vários recursos para proteger dados em trânsito e em repouso. Isso inclui criptografia de dados, arquivos, aplicativos, serviços, comunicações e unidades. Você pode criptografar informações antes de colocá-las no Azure, bem como armazenar chaves em seus datacenters locais.

![Microsoft Antimalware no Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Tecnologias de criptografia do Azure
Você pode obter detalhes sobre o ambiente de assinatura tooyour acesso administrativo usando [relatórios do AD do Azure](../active-directory/active-directory-reporting-audit-events.md). Você pode configurar a [Criptografia de Unidade de Disco BitLocker](https://technet.microsoft.com/library/cc732774.aspx) em VHDs com informações confidenciais no Azure.

Outros recursos no Azure que irá ajudá-lo tookeep que proteger seus dados incluem:

* Os desenvolvedores de aplicativos podem criar a criptografia em aplicativos de saudação implantação no Azure usando o Windows hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) e do .NET Framework.
* Controle completamente chaves Olá com criptografia do lado do cliente para o armazenamento de BLOBs do Azure. serviço de armazenamento de saudação nunca vê as chaves de saudação e é capaz de descriptografar dados saudação.
* [O Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (com hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) fornece o arquivo e prevenção de vazamento de dados e criptografia de nível de dados por meio do gerenciamento de acesso baseado em políticas.
* O Azure oferece suporte à [criptografia no nível de tabela e de coluna (TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) em máquinas virtuais do SQL Server e a servidores de gerenciamento de chaves de terceiros locais em datacenters.
* Chaves da conta de armazenamento, assinaturas de acesso compartilhado, certificados de gerenciamento e outras chaves são exclusivo tooeach locatário do Azure.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) armazenamento híbrido criptografa dados por meio de um par de chaves pública/privada 128 bits antes de carregá-lo tooAzure armazenamento.
* O Azure oferece suporte e usa vários mecanismos de criptografia, incluindo SSL/TLS, IPsec e AES, dependendo de transportes, contêineres e tipos de dados de saudação.

## <a name="virtualization"></a>Virtualização
Olá plataforma Windows Azure usa um ambiente virtualizado. Instâncias de usuário funcionam como máquinas virtuais autônomas que não têm o servidor do acesso tooa host físico, e esse isolamento é imposto por meio físico [níveis de privilégio de processador (anel-0/anel-3)](https://en.wikipedia.org/wiki/Protection_ring).

Anel 0 é hello mais privilegiada e 3 é hello menos. sistema operacional convidado de saudação é executado em um anel de menor privilégio 1 e aplicativos executados em hello 3 de anel com menos privilégios. Essa virtualização dos recursos físicos leva tooa clara separação entre o sistema operacional convidado e do hipervisor, resultando na separação de segurança adicional entre hello dois.

Hello Azure hipervisor age como um micro-kernel e passa todas as solicitações de acesso de hardware do host de toohello de máquinas virtuais de convidados para processamento usando uma interface de memória compartilhada chamada VMBus. Isso impede que os usuários obtenham o sistema de toohello de acesso de leitura/gravação/execução bruto e reduz o risco de saudação do compartilhamento de recursos do sistema.

![Microsoft Antimalware no Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Como o Azure implementa a virtualização
O Azure usa um firewall de hipervisor (filtro de pacote) que é implementado no hipervisor hello e configurado por um agente de controlador de malha. Isso ajuda a proteger locatários contra o acesso não autorizado. Por padrão, todo o tráfego é bloqueado quando uma máquina virtual é criada e, em seguida, agente de controlador de malha Olá configura Olá pacote filtro tooadd *regras e exceções* tooallow autorizado tráfego.

Há duas categorias de regras que são programadas aqui:

* **Configuração de máquina ou regras de infraestrutura**: por padrão, toda a comunicação é bloqueada. Há é exceções tooallow toosend uma máquina virtual e receber o tráfego DHCP e DNS. Máquinas virtuais também podem enviar tráfego toohello "público" da internet e enviar tráfego tooother máquinas virtuais em cluster hello e o servidor de ativação do sistema operacional hello. lista de saudação das máquinas virtuais de destinos permitidos de saída não inclui sub-redes do roteador do Azure, gerenciamento do Azure de volta final e outras propriedades de Microsoft.
* **Arquivo de configuração de função**: define Olá entrada controle listas de acesso (ACLs) com base no modelo de serviço do locatário hello. Por exemplo, se um locatário tiver um front-end da Web na porta 80 em um determinado computador virtual, em seguida, Azure abre TCP porta 80 tooall IPs se você estiver configurando um ponto de extremidade no hello [modelo de implantação clássico do Azure](../azure-resource-manager/resource-manager-deployment-model.md). Se máquina virtual de saudação possui uma função de final ou de trabalho back, em execução, em seguida, ele abre Olá trabalho função toohello máquina virtual somente em Olá mesmo locatário.

## <a name="isolation"></a>Isolamento
Outro requisito de segurança de nuvem importante é tooprevent de separação não autorizada e não intencional a transferência de informações entre implantações em uma arquitetura de multilocatária compartilhada.

O Azure implementa o [controle de acesso à rede](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) e a segregação por meio do isolamento de VLAN, ACLs, filtros IP e balanceadores de carga. Ela restringe o tráfego externo de entrada tooports e protocolos de suas máquinas virtuais que você definir. Azure implementa o tráfego de tooprevent falsificado filtragem de rede e restringir os componentes de plataforma tootrusted tráfego de entrada e saída. As políticas de fluxo de tráfego são implementadas em dispositivos de proteção de limite que negam o tráfego por padrão.

![Microsoft Antimalware no Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Conversão de endereço de rede (NAT) é usado tooseparate tráfego interno da rede de tráfego externo. O tráfego interno não é roteável externamente. Os [endereços IP virtuais](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) que são externamente roteáveis são convertidos em endereços [IP dinâmico interno](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) que só são roteáveis dentro do Azure.

Máquinas de virtuais tooAzure tráfego externo é ativar o firewall por meio de ACLs em roteadores, balanceadores de carga e comutadores de camada 3. Somente os protocolos conhecidos específicos são permitidos. As ACLs estão no local toolimit tráfego originado de máquinas virtuais convidadas VLANs tooother usados para gerenciamento. Além disso, o tráfego filtrado por meio de filtros IP hello SO mais limites Olá tráfego do host em ambas as camadas de link e rede de dados.

### <a name="how-azure-implements-isolation"></a>Como o Azure implementa o isolamento
Olá controlador de malha do Azure é responsável pela alocação de recursos de infraestrutura tootenant cargas de trabalho e gerencia a comunicação unidirecional de máquinas de toovirtual Olá host. Olá hipervisor do Azure impõe a memória e separação do processo entre máquinas virtuais e o roteamento seguro de locatários de tooguest SO de tráfego de rede. O Azure também implementa o isolamento para locatários, armazenamento e redes virtuais.

* Cada locatário do Azure AD é logicamente isolado por meio de limites de segurança.
* Contas de armazenamento do Azure são exclusivos tooeach assinatura e acesso deve ser autenticado usando uma chave de conta de armazenamento.
* As redes virtuais são logicamente isoladas por meio de uma combinação de endereços IP privados, firewalls e ACLs de IP exclusivos. Balanceadores de carga rotear tráfego toohello apropriado os locatários com base nas definições de ponto de extremidade.

## <a name="virtual-networks-and-firewalls"></a>Redes virtuais e firewalls
Olá [redes virtuais e distribuídas](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) na Ajuda do Azure, verifique se o tráfego de rede privada é isolado logicamente do tráfego em outras redes virtuais do Azure.

![Microsoft Antimalware no Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Sua assinatura pode conter várias redes privadas isoladas (e incluir firewall, balanceamento de carga e conversão de endereços de rede).

O Azure fornece três níveis principais de diferenciação de rede em cada Azure tráfego segregate toologically de cluster. [Redes locais virtuais](https://azure.microsoft.com/services/virtual-network/) (VLANs) são usados o tráfego de cliente tooseparate restante de saudação do hello rede do Azure. Acesso toohello rede Azure de cluster de saudação externa é restrito por meio de balanceadores de carga.

Tooand de tráfego de rede de máquinas virtuais deve passar pelo comutador hello hipervisor. componente de filtro IP Olá no sistema operacional raiz de saudação isola Olá raiz virtual máquina Olá máquinas de virtuais de convidado e máquinas de virtuais de convidados Olá uns dos outros. Ele executa a filtragem de comunicação de toorestrict do tráfego entre nós de um locatário e hello Internet pública (com base na configuração de serviço do cliente Olá), isolá-los de outros locatários.

filtro IP Hello ajuda a evitar máquinas virtuais de convidados do:

* Gerem tráfego falsificado.
* Receber o tráfego não resolvidos toothem.
* Direcionando tráfego tooprotected infraestrutura pontos de extremidade.
* Enviem ou recebam tráfego de difusão inadequado.

Você pode adicionar suas máquinas virtuais a [redes virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-network/). Essas redes virtuais são semelhantes redes toohello configurar em ambientes locais, onde eles são geralmente associados um comutador virtual. Máquinas virtuais conectadas toohello mesma rede virtual pode se comunicar uns com os outros sem configuração adicional. Também é possível configurar sub-redes diferentes em sua rede virtual.

Você pode usar o hello seguindo comunicações seguras de toohelp de tecnologias de rede Virtual do Azure na sua rede virtual:

* [**Grupos de Segurança de Rede (NSG)**](../virtual-network/virtual-networks-nsg.md). Você pode usar um tooone de tráfego do NSG toocontrol ou mais instâncias de máquina virtual em sua rede virtual. Um NSG contém regras de controle de acesso que permitem ou negam o tráfego com base na direção do tráfego, no protocolo, no endereço e porta de origem e no endereço e porta de destino.
* [**Roteamento definido pelo usuário**](../virtual-network/virtual-networks-udr-overview.md). Você pode controlar a saudação roteamento de pacotes por meio de um dispositivo virtual com a criação de rotas definidas pelo usuário que especificam o próximo salto Olá para pacotes que fluem de dispositivo de segurança de rede virtual tooa sub-rede específica toogo tooa.
* [**Encaminhamento IP**](../virtual-network/virtual-networks-udr-overview.md). Um dispositivo de segurança de rede virtual deve ser capaz de tooreceive tráfego de entrada que não seja endereçado tooitself. tooallow tráfego de tooreceive uma máquina virtual resolvido tooother destinos, você ativar o encaminhamento IP para a máquina virtual de saudação.
* [**Túnel forçado**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). O túnel forçado permite redirecionar ou "forçar" todo o tráfego direcionado à Internet gerado por suas máquinas virtuais em uma rede virtual tooyour back local por meio de um túnel VPN site a site para inspeção e auditoria
* [**ACLs de ponto de extremidade**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Você pode controlar quais computadores são permitidos conexões de entrada de máquina virtual do hello Internet tooa em sua rede virtual, definindo as ACLs de ponto de extremidade.
* [**Soluções de segurança de rede de parceiros**](https://azure.microsoft.com/marketplace/). Há um número de soluções de segurança de rede do parceiro que você pode acessar de saudação do Azure Marketplace.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Como o Azure implementa redes virtuais e firewalls
Por padrão, o Azure implementa firewalls de filtragem de pacotes em todos os hosts e máquinas virtuais convidadas. Imagens do sistema operacional Windows de saudação do Azure Marketplace também tem o Firewall do Windows habilitado por padrão. Balanceadores de carga no perímetro Olá das comunicações de controle de redes voltado ao público do Azure com base nas ACLs de IP gerenciados por administradores do cliente.

Se o Azure mover dados de um cliente como parte das operações normais ou durante um desastre, ele fará isso em canais de comunicações privados criptografados. Outros recursos usados pelo Azure toouse em firewalls e redes virtuais são:

* **Firewall de host nativo**: o Azure Service Fabric e o Armazenamento do Azure são executados em um sistema operacional nativo sem um hipervisor. Portanto, firewall do windows hello é configurado com hello anterior dois conjuntos de regras. Armazenamento executa desempenho toooptimize nativo.
* **O firewall do host**: firewall de host de saudação é tooprotect Olá sistema operacional do host que executa o hipervisor hello. regras de saudação são o único controlador de malha do serviço Olá tooallow programadas e ir caixas tootalk toohello SO do host em uma porta específica. Olá outras exceções são tooallow resposta DHCP e respostas de DNS. O Azure usa um arquivo de configuração de máquina que tem o modelo de saudação de regras de firewall para o sistema operacional do host de saudação. host de saudação em si está protegido contra ataque externo por uma comunicação de toopermit do Windows firewall configurado somente de fontes conhecidas e autenticados.
* **Firewall de convidado**: replica regras Olá no filtro de pacote de comutador hello máquina virtual mas programadas no software diferente (como parte do Firewall do Windows hello do sistema operacional convidado de saudação). firewall de máquina virtual do convidado Olá pode ser configurado toorestrict comunicações tooor da máquina de virtual do convidado Olá, mesmo se a comunicação de saudação é permitida por configurações no host Olá filtro IP. Por exemplo, você poderá toouse Olá convidado firewall toorestrict comunicação da máquina virtual entre dois dos seus VNets que foram configurados tooconnect tooone outro.
* **Firewall de armazenamento (FW)**: firewall front-end de armazenamento Olá Olá filtros de tráfego toobe somente nas portas 80/443 e outras portas necessárias do utilitário. firewall de saudação no back-end de armazenamento Olá restringe toocome comunicações apenas de servidores de front-end de armazenamento.
* **Gateway de rede virtual**: Olá [Gateway de rede Virtual do Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) atua como gateway entre locais de saudação conectar suas cargas de trabalho na rede Virtual do Azure tooyour de sites no local. É necessário tooconnect sites tooon local por meio de [túneis VPN site a site IPsec](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), ou por meio [ExpressRoute](../expressroute/expressroute-introduction.md) circuitos. Para túneis VPN IPsec/IKE, gateways Olá executam handshakes de IKE e estabelecer Olá túneis de VPN S2S de IPsec entre redes virtuais hello e sites no local. Os gateways de rede virtual também encerram [VPNs de ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Acesso remoto seguro
Os dados armazenados na nuvem Olá devem ter suficiente explorações de tooprevent garantias habilitadas e manter a confidencialidade e integridade ao mesmo tempo em trânsito. Isso inclui controles de rede que se integram à identidade auditável baseada em política de uma organização e a mecanismos de gerenciamento de acesso.

Tecnologia de criptografia interna permite que você tooencrypt comunicações dentro e entre as implantações, entre regiões do Azure e de data centers do Azure tooon local. Máquinas de toovirtual de acesso de administrador por meio de [sessões de área de trabalho remota](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [Windows PowerShell remoto](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), e hello portal do Azure é sempre criptografado.

toosecurely estender seus locais de datacenter toohello nuvem, o Azure fornece ambos [VPN site a site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) e [VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md), além de links dedicados com [ExpressRoute](../expressroute/expressroute-introduction.md)(conexões tooAzure redes virtuais pela VPN são criptografadas).

### <a name="how-azure-implements-secure-remote-access"></a>Como o Azure implementa o acesso remoto seguro
Conexões toohello portal do Azure sempre deve ser autenticado e eles requerem SSL/TLS. Você pode configurar certificados tooenable segura do gerenciamento. Os protocolos de segurança padrão do setor, como [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) e [IPsec](https://en.wikipedia.org/wiki/IPsec), têm suporte completo.

O [Azure ExpressRoute](../expressroute/expressroute-introduction.md) permite criar conexões privadas entre os datacenters do Azure e a infraestrutura no seu local ou em um ambiente de colocalização. Conexões de rota expressa não passam pela Olá Internet pública. Eles oferecem mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que os links típicos baseados na Internet. Em alguns casos, transferir dados entre armazenamentos locais e o Azure usando conexões do ExpressRoute pode proporcionar um custo/benefício significativo.

## <a name="logging-and-monitoring"></a>Log e monitoramento
O Azure fornece autenticado o log de eventos de segurança relevantes que geram uma trilha de auditoria e é engenharia tootampering toobe resistente. inclui informações do sistema, como logs de eventos de segurança em VMs de infraestrutura do Azure e o AD do Azure. Monitoramento de eventos de segurança inclui a coleta de eventos, como as alterações nos endereços IP de servidor DHCP ou DNS; tentativa de acesso tooports, protocolos ou endereços IP que estão bloqueados pelo design; alterações nas configurações de firewall ou diretiva de segurança; criação de conta ou grupo. e processos inesperados ou instalação do driver.

![Microsoft Antimalware no Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

O acesso de usuário privilegiado de registro de logs de auditoria e atividades, as tentativas de acesso autorizado e não autorizado, as exceções do sistema e os eventos de segurança de informação são mantidos por um período estabelecido. retenção de saudação dos seus logs é a seu critério como configurar coleta de log e os próprios requisitos de retenção de tooyour.

### <a name="how-azure-implements-logging-and-monitoring"></a>Como o Azure implementa os logs e o monitoramento
O Azure implanta agentes de gerenciamento (MA) e o Monitor de segurança do Azure (ASM) tooeach de agentes computação, armazenamento ou o nó do fabric sob gerenciamento sejam nativo ou virtual. Cada agente de gerenciamento é a conta de armazenamento de equipe configurado tooauthenticate tooa serviço com um certificado obtido do repositório de certificados do Azure de saudação e encaminhar pré-configurado diagnóstico e a conta de armazenamento de toohello de dados de evento. Esses agentes não são máquinas virtuais dos toocustomers implantado.

Administradores do Azure acessam logs por meio de um portal da web para acesso autenticado e controlado toohello logs. Um administrador pode analisar, filtrar, correlacionar e analisar logs. contas de armazenamento de equipe saudação do serviço do Azure para logs são protegidos contra toohelp de acesso de administrador direto impedem contra violação de log.

A Microsoft coleta logs de dispositivos de rede usando o protocolo de Syslog de saudação e de servidores de host usando serviços de coleta de auditoria da Microsoft (ACS). Esses logs são armazenados em um banco de dados de log do qual os alertas de eventos suspeitos serão gerados. administrador de saudação pode acessar e analisar esses logs.

[Diagnóstico do Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) é um recurso do Azure que permite que você toocollect dados de diagnóstico de um aplicativo em execução no Azure. Eles são dados de diagnóstico para tarefas de depuração e solução de problemas, medição de desempenho, monitoramento de uso de recursos, análise de tráfego, planejamento da capacidade e auditoria. Após a coleta de dados de diagnóstico hello, pode ser transferido tooan conta de armazenamento do Azure para persistência. As transferências podem ser agendadas ou sob demanda.

## <a name="threat-mitigation"></a>Redução de ameaças
Em adição tooisolation, criptografia e filtragem, o Azure emprega um número de mecanismos de mitigação de ameaça e infraestrutura de tooprotect processos e serviços. Isso inclui controles internos e tecnologias usadas toodetect e corrigir ameaças avançadas, como DDoS, elevação de privilégios e Olá [OWASP Top-10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

controles de segurança Hello e processos de gerenciamento de riscos Microsoft tem em vigor toosecure reduzir sua infraestrutura de nuvem Olá risco de incidentes de segurança. Olá evento um incidente ocorre, equipe de gerenciamento de incidentes de segurança (SIM) hello dentro da equipe Microsoft Online Services de segurança e conformidade (OSSC) do hello está pronto toorespond a qualquer momento.

### <a name="how-azure-implements-threat-mitigation"></a>Como o Azure implementa a atenuação de ameaças
O Azure tem controles de segurança em redução de ameaças tooimplement local e também toohelp clientes reduzir as ameaças potenciais em seus ambientes. Olá lista a seguir resume os recursos de mitigação de ameaça Olá oferecidos pelo Azure:

* O [Antimalware do Azure](azure-security-antimalware.md) está habilitado por padrão em todos os servidores de infraestrutura. Você tem a opção de habilitá-lo em suas próprias máquinas virtuais.
* Microsoft mantém contínua de monitoramento entre servidores, redes e aplicativos ameaças de toodetect e evitar explorações. Alertas automatizados notificam os administradores de comportamentos anormais, permitindo que uma ação corretiva tootake contra ameaças internas e externas.
* Você pode implantar soluções de segurança de terceiros em suas assinaturas, como firewalls de aplicativo da Web do [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Da Microsoft abordagem toopenetration teste inclui "[agrupamento vermelho](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," que envolve os profissionais de segurança da Microsoft sistemas de produção (não cliente) no Azure tootest defesas reais, o ataque avançado , ameaças persistentes.
* Integrado de implantação de sistemas gerenciam instalação de patches de segurança e distribuição Olá Olá plataforma Windows Azure.

## <a name="next-steps"></a>Próximas etapas
[Central de Confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/)

[Blog da equipe de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

[Blog do Active Directory](http://blogs.technet.com/b/ad/)
