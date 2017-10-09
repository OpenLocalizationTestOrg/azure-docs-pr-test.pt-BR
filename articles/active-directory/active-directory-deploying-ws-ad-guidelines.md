---
title: "aaaGuidelines para implantar o Active Directory do Windows Server em máquinas virtuais do Azure | Microsoft Docs"
description: "Se você sabe como os serviços de domínio toodeploy AD e os serviços de Federação do AD no local, saber como eles funcionam em máquinas virtuais do Azure."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Diretrizes para implantar o Active Directory do Windows Server em máquinas virtuais do Azure
Este artigo explica diferenças importantes de saudação entre implantação Windows Server Active Directory Domain Services (AD DS) e os serviços de Federação do Active Directory (AD FS) no local em vez de implantá-los em máquinas virtuais do Microsoft Azure.

## <a name="scope-and-audience"></a>Escopo e público
artigo de saudação destina-se para aqueles que já tiveram com a implantação do Active Directory local. Ele aborda as diferenças de saudação entre a implantação do Active Directory em redes virtuais do Microsoft Azure máquinas virtuais/Azure e implantações do Active Directory local tradicional. Máquinas virtuais do Azure e redes virtuais do Azure fazem parte de um infraestrutura-como-um-oferta de serviço (IaaS) para organizações tooleverage recursos na nuvem de saudação de computação.

Para aqueles que não estão familiarizados com a implantação do AD, consulte Olá [guia de implantação do AD DS](https://technet.microsoft.com/library/cc753963) ou [planejar sua implantação do AD FS](https://technet.microsoft.com/library/dn151324.aspx) conforme apropriado.

Este artigo pressupõe que o leitor Olá esteja familiarizado com hello conceitos a seguir:

* Gerenciamento e implantação do AD DS do Windows Server
* Implantação e configuração da infraestrutura do DNS toosupport um Windows Server AD DS
* Gerenciamento e implantação do AD FS do Windows Server
* Implantando, configurando e gerenciando aplicativos confiáveis (sites e serviços Web) que podem consumir tokens do AD FS do Windows Server
* Conceitos gerais de máquina virtual, como como tooconfigure um virtual da máquina, virtual discos e redes virtuais

Este artigo realça os requisitos de saudação para um cenário de implantação híbrido no qual o Windows Server AD DS ou AD FS são implantados no local e em parte em máquinas virtuais do Azure. documento de saudação primeiro aborda diferenças críticas de saudação entre executando o Windows Server AD DS e AD FS em máquinas virtuais do Azure versus local e os pontos de decisão importante que afetam o design e implantação. Olá restante papel Olá apresenta diretrizes para cada um dos pontos de decisão de saudação em mais detalhes e como tooapply Olá cenários de implantação de toovarious diretrizes.

Este artigo não aborda a configuração de saudação do [Active Directory do Azure](http://azure.microsoft.com/services/active-directory/), que é um serviço baseado em REST que fornece recursos de controle de acesso e gerenciamento de identidade para aplicativos em nuvem. Azure Active Directory (AD do Azure) e Windows Server AD DS são, no entanto, toowork projetado juntos tooprovide uma solução de gerenciamento de identidade e acesso para o ambiente de TI híbrido atuais ambientes e aplicativos modernos. toohelp entender as diferenças de saudação e as relações entre o Windows Server AD DS e AD do Azure, considere Olá seguinte:

1. Você pode executar Windows Server AD DS na nuvem Olá no máquinas virtuais do Azure quando você estiver usando o Azure tooextend seu datacenter local para nuvem hello.
2. Você pode usar o AD do Azure toogive seus aplicativos de única logon tooSoftware-como um serviço (SaaS) de usuários. Por exemplo, o Microsoft Office 365 utiliza essa tecnologia, e aplicativos executados no Azure ou outras plataformas na nuvem também podem usá-lo.
3. Você pode usar o AD do Azure (seu Access Control Service) toolet os usuários se conectam usando identidades do Facebook, Google, Microsoft e outros tooapplications de provedores de identidade que são hospedados em nuvem hello ou local.

Para saber mais sobre essas diferenças, confira [Identidade do Azure](fundamentals-identity.md).

## <a name="related-resources"></a>Recursos relacionados
Você pode baixar e executar Olá [avaliação de prontidão de máquina Virtual do Azure](https://www.microsoft.com/download/details.aspx?id=40898). Olá avaliação automaticamente inspecionar o seu ambiente local e gerar um relatório personalizado com base em Olá orientação encontrado no toohelp tópico migrar Olá ambiente tooAzure.

É recomendável que você examine primeiro Olá tutoriais, guias e vídeos que abrangem Olá seguintes tópicos:

* [Configurar uma rede Virtual somente em nuvem no hello Portal do Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Configurar uma VPN Site a Site no hello Portal do Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalar uma nova floresta do Active Directory em uma rede virtual do Azure](active-directory-new-forest-virtual-machine.md)
* [Instalar uma réplica do controlador de domínio do Active Directory no Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS para profissionais de TI: (01) conceitos básicos de máquina virtual](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profissionais de TI: (05) Criando redes virtuais e conectividade entre instalações](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Introdução
Olá requisitos básicos para implantar o Active Directory do Windows Server em máquinas virtuais do Azure diferem muito pouco de implantá-lo em máquinas virtuais em locais (e, toosome ponto, computadores físicos). Por exemplo, no hello caso do Windows Server AD DS, se os controladores de domínio da saudação (DCs) que você implantar em máquinas virtuais do Azure forem réplicas em um existente local domínio corporativo/floresta, Olá implantação do Azure pode ser tratada em grande parte Olá mesma maneira que você pode tratar qualquer outro site adicional do Active Directory do Windows Server. Isto é, sub-redes devem ser definidas no Windows Server AD DS, um site criado, Olá sub-redes vinculados toothat site e conectados tooother sites usando os links de site apropriados. No entanto, há algumas diferenças que são comuns tooall Azure implantações e algumas que variam de acordo cenário de implantação específico toohello. Duas diferenças fundamentais são demonstradas abaixo:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Máquinas virtuais do Azure pode ser necessário rede corporativa da conectividade toohello local.
Conectar máquinas virtuais do Azure tooan voltar a rede corporativa requer a rede virtual do Azure, que inclui uma site a site ou ponto de site de rede virtual privada (VPN) no local tooseamlessly de componente capaz de se conectar máquinas virtuais do Azure e computadores locais. Esse componente VPN também pode habilitar local domínio membro computadores tooaccess um domínio do Active Directory do Windows Server cujos controladores de domínio são hospedados exclusivamente em máquinas virtuais do Azure. É importante toonote, no entanto, se a VPN apresentará falha se hello, autenticação e outras operações que dependem do Active Directory do Windows Server também falharão. Enquanto os usuários podem ser capaz de toosign usando credenciais armazenadas em cache existentes, todos os ponto a ponto ou tentativas de autenticação de cliente para servidor para quais tíquetes tem ainda toobe emitido ou se tornou obsoleta falhará.

Consulte [rede Virtual](http://azure.microsoft.com/documentation/services/virtual-network/) para ver uma demonstração em vídeo e uma lista de tutoriais passo a passo, incluindo [configurar uma VPN Site a Site no portal do Azure de saudação](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Você também pode implantar o Active Directory do Windows Server em uma rede virtual do Azure que não tenha conectividade com uma rede local. diretrizes de saudação neste tópico, no entanto, supõem que uma rede virtual do Azure é usada porque ele fornece recursos que são essenciais tooWindows Server de endereçamento IP.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Os endereços IP estáticos devem ser configurados com o Azure PowerShell.
Os endereços dinâmicos são alocados por padrão, mas usam tooassign de cmdlet Set-AzureStaticVNetIP do hello um endereço IP estático em vez disso. Que define um endereço IP que será mantido por meio da recuperação de serviço e desligamento/reinício da VM. Para saber mais, confira [Endereço IP interno estático para máquinas virtuais](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>Termos e definições
a seguir Olá é uma lista parcial de termos para diversas tecnologias do Azure que serão referenciados neste artigo.

* **Máquinas virtuais do Azure**: oferta de IaaS Olá no Azure que permite que os clientes toodeploy VMs que executam praticamente qualquer tradicionalmente carga de trabalho do servidor local.
* **Rede virtual do Azure**: Olá tootheir próprio do serviço no Azure que permite que os clientes criem e gerenciem redes virtuais no Azure e vinculá-las com segurança de rede na infraestrutura de rede local usando uma rede virtual privada (VPN).
* **Endereço IP virtual**: um para a internet de endereços IP que é tooa não é vinculado específico computador ou rede placa de interface. Serviços de nuvem são atribuídos a um endereço IP virtual para receber o tráfego de rede que é redirecionado tooan VM do Azure. Um endereço IP virtual é uma propriedade de um serviço de nuvem que pode conter uma ou mais máquinas virtuais do Azure. Observe também que uma rede virtual do Azure pode conter um ou mais serviços de nuvem. Os endereços IP virtuais fornecem recursos nativos de balanceamento de carga.
* **Endereço IP dinâmico**: esse é o endereço IP de saudação que é somente interno. Ele deve ser configurado como um endereço IP estático (usando cmdlet Set-AzureStaticVNetIP do hello) para VMs que hospedam funções de servidor DC/DNS hello.
* **Recuperação de serviço**: Olá processo no qual o Azure retorna automaticamente tooa um serviço estado em execução novamente após detectar esse serviço Olá falhou. Recuperação de serviço é um dos aspectos de saudação do Azure que dá suporte à disponibilidade e resiliência. Embora seja improvável, resultado Olá após um incidente de recuperação para um controlador de domínio em execução em uma VM de serviço é reinicialização não planejada de tooan semelhantes, mas tem alguns efeitos colaterais:
  
  * adaptador de rede virtual Olá Olá VM será alterado
  * Olá endereço MAC do adaptador de rede virtual Olá será alterado
  * Olá ID de processador/CPU da saudação VM será alterado
  * Hello configuração de IP do adaptador de rede virtual Olá não mudará contanto que Olá VM é a rede virtual tooa anexado e hello endereço IP da VM é estático.
  
  Nenhum desses comportamentos afetam o Active Directory do Windows Server porque ele não tem dependências em endereço MAC de saudação ou ID de processador/CPU, e todas as implantações do Active Directory do Windows Server no Azure são recomendadas toobe executado em uma rede virtual do Azure conforme descrito acima .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Trata-se de controladores de domínio do Active Directory do Windows Server toovirtualize seguro?
Implantar DCs do Active Directory para Windows Server em máquinas virtuais do Azure é o assunto toohello mesmas diretrizes que a execução de DCs locais em uma máquina virtual. Executar controladores de domínio virtualizados é uma prática de segurança desde que sejam seguidas as diretrizes para fazer backup e restaurar controladores de domínio. Para saber mais sobre restrições e diretrizes para a execução de controladores de domínio virtualizados, confira [Executando Controladores de Domínio no Hyper-V](https://technet.microsoft.com/library/dd363553).

Os hipervisores fornecem ou banalizam tecnologias que podem causar problemas para muitos sistemas distribuídos, incluindo o Active Directory do Windows Server. Por exemplo, em um servidor físico, você pode clonar um disco ou usar métodos sem suporte tooroll Olá back estado de um servidor, inclusive usar SANs e assim por diante, mas fazer isso em um servidor físico é muito mais difícil do que a restauração de um instantâneo de máquina virtual em um hipervisor. Azure oferece a funcionalidade que pode resultar em Olá mesma condição indesejável. Por exemplo, você não deve copiar os arquivos VHD de DCs em vez de executar backups regulares porque restaurá-los pode resultar em um recursos de restauração do instantâneo de toousing situação semelhante.

Essas reversões apresentam bolhas de USN que podem levar a estados divergentes toopermanently entre controladores de domínio. Isso pode causar problemas como:

* Objetos persistentes
* Senhas inconsistentes
* Valores de atributo inconsistentes
* Incompatibilidade de esquema se o mestre de esquema Olá é revertida

Para saber mais sobre como os controladores de domínio são afetados, confira [USN e Reversão do USN](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

Começando com o Windows Server 2012, [proteções adicionais são incorporados no tooAD DS](https://technet.microsoft.com/library/hh831734.aspx). Essas proteções ajudam a proteger controladores de domínio virtualizados contra os problemas mencionados acima do hello, desde que a plataforma do hipervisor subjacente Olá dá suporte a VM-GenerationID. Azure oferece suporte a VM-GenerationID, o que significa que os controladores de domínio que executam o Windows Server 2012 ou máquinas virtuais do Azure posteriormente tem proteções adicionais hello.

> [!NOTE]
> Você deve desligar e reiniciar uma VM que executa a função de controlador de domínio Olá no Azure no sistema de operacional convidado Olá em vez de usar o hello **desligar** opção Olá portal do Azure. Hoje, usando a tooshut portal Olá uma VM faz com que o hello VM toobe desalocada. Uma VM desalocada tem a vantagem de saudação de não incorrer em encargos, mas ele também redefine Olá VM-GenerationID, que é indesejável para um controlador de domínio. Quando Olá VM-GenerationID é redefinida, Olá invocationID do banco de dados do hello AD DS também é redefinido, Olá pool RID é descartado e SYSVOL é marcado como não autoritativo. Para obter mais informações, consulte [tooActive Introdução Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) e [virtualização segura da DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Por que implantar o AD DS do Windows Server em Máquinas Virtuais do Azure?
Muitos cenários de implantação do AD DS do Windows Server são apropriados para implantação como máquinas virtuais no Azure. Por exemplo, suponha que você tenha uma empresa na Europa que precisa tooauthenticate usuários em um local remoto na Ásia. Olá empresa não implantou anteriormente Active Directory DCs do Windows Server na Ásia devido toohello custo toodeploy-los e a experiência limitada toomanage Olá pós-implantação de servidores. Como resultado, as solicitações de autenticação da Ásia são atendidas pelos controladores de domínio na Europa com resultados de qualidade inferiores. Nesse caso, você pode implantar um controlador de domínio em uma VM que você especificou que deve ser executado dentro de saudação do datacenter do Azure na Ásia. Anexando que tooan rede virtual do Azure que está conectado diretamente local remoto toohello melhorará o desempenho de autenticação do controlador de domínio.

O Azure também é bem-apropriado como um substituto toootherwise sites desastres muito caros (Disaster recovery). Olá custo relativamente baixo de hospedar um número pequeno de controladores de domínio e uma única rede virtual no Azure representa uma alternativa atrativa.

Por fim, talvez você queira toodeploy um aplicativo de rede no Azure, como o SharePoint, o que requer o Windows Server Active Directory, mas não tem dependência Olá no local de rede ou Olá corporativa Windows Server Active Directory. Nesse caso, os requisitos do servidor Implantando uma floresta isolada no Azure toomeet saudação do SharePoint é ideal. Novamente, também há suporte para implantação de aplicativos de rede que exigem conectividade toohello local de rede e Olá corporativo do Active Directory.

> [!NOTE]
> Como ele fornece uma conexão de camada 3, Olá componente de VPN que fornece conectividade entre uma rede virtual do Azure e uma rede local também pode habilitar os servidores de membro que são executados no local tooleverage DCs executados como máquinas virtuais do Azure no Azure rede virtual. Mas se Olá VPN não estiver disponível, a comunicação entre computadores locais e controladores de domínio baseados no Azure não funcionará, resultando em erros de autenticação e vários outros.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Contrastes entre a implantação de controladores de domínio do Active Directory do Windows Server em máquinas virtuais do Azure versus localmente
* Para qualquer cenário de implantação do Windows Server Active Directory que inclui mais de uma única VM, é necessário toouse uma rede virtual do Azure para consistência de endereço IP. Observe que este guia pressupõe que os controladores de domínio estejam sendo executados em uma rede virtual do Azure.
* Como ocorre com os controladores de domínio locais, recomenda-se o uso de endereços IP estáticos. Um endereço IP estático só pode ser configurado usando o Azure PowerShell. Confira [Endereço IP estático interno para VMs](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) para obter mais detalhes. Se você tiver sistemas de monitoramento ou outras soluções que verifica a configuração do endereço IP estática no sistema de operacional convidado hello, você pode atribuir Olá mesmo estático toohello rede adaptador propriedades do endereço IP de saudação VM. Mas, lembre-se de que o adaptador de rede hello será descartado se hello VM passa por recuperação de serviço ou for desligada no portal de saudação e tem seu endereço desalocado. Nesse caso, o endereço IP estático de saudação no convidado Olá precisará toobe redefinir.
* Implantar máquinas virtuais em uma rede virtual não implica (ou exigir) conectividade tooan back local rede; rede virtual Olá simplesmente habilita essa possibilidade. Você deve criar uma rede virtual para comunicação privada entre o Azure e sua rede local. É necessário toodeploy um ponto de extremidade VPN na rede de local de saudação. Olá VPN é aberta da rede do local de toohello do Azure. Para obter mais informações, consulte [visão geral da rede Virtual](../virtual-network/virtual-networks-overview.md) e [configurar uma VPN Site a Site no hello Azure Portal](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Uma opção muito[criar uma VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md) é tooconnect disponível em computadores individuais baseados em Windows diretamente tooan rede virtual do Azure.
> 
> 

* Independentemente de criar uma rede virtual ou não, o Azure cobra pelo tráfego de saída, mas não pelo de entrada. Várias opções de design do Active Directory do Windows Server podem afetar a quantidade de tráfego de saída gerada por uma implantação. Por exemplo, a implantação de um RODC (controlador de domínio somente leitura) limita o tráfego de saída porque ele não replica a saída. Mas a decisão de saudação toodeploy um RODC precisa toobe ponderada em relação a saudação necessidade tooperform gravar operações em relação a saudação DC e hello [compatibilidade](https://technet.microsoft.com/library/cc755190) aplicativos e serviços no site de saudação têm com os RODCs. Para saber mais sobre encargos de tráfego, confira [Visão geral de preços do Azure](http://azure.microsoft.com/pricing/).
* Embora você tenha controle total sobre quais toouse de recursos de servidor para VMs locais, como RAM, tamanho do disco e assim por diante, no Azure, você deve selecionar em uma lista de tamanhos de servidor pré-configurados. Para um controlador de domínio, um disco de dados é necessário em disco do sistema operacional toohello adição no banco de dados do pedido toostore saudação do Active Directory do Windows Server.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>É possível implantar o AD FS do Windows Server em máquinas virtuais do Azure?
Sim, você pode implantar o Windows Server AD FS em máquinas virtuais do Azure e Olá [as práticas recomendadas para implantação do AD FS](https://technet.microsoft.com/library/dn151324.aspx) local se aplicam igualmente tooAD FS implantação no Azure. Mas algumas das práticas recomendadas de hello como o balanceamento de carga e alta disponibilidade, exigem tecnologias além do que o AD FS oferece. Elas devem ser fornecidas pela infraestrutura subjacente hello. Vamos examinar algumas dessas práticas recomendadas e ver como elas podem ser alcançadas usando VMs do Azure e uma rede virtual do Azure.

1. **Nunca exponha servidores de serviço de token (STS) de segurança toohello diretamente da Internet.**
   
    Isso é importante porque Olá STS emite tokens de segurança. Como resultado, os servidores de STS, como servidores do AD FS devem ser tratados com hello mesmo nível de proteção como um controlador de domínio. Se um STS estiver comprometido, usuários mal-intencionados têm os tokens de acesso tooissue capacidade Olá podendo conter declarações de seus aplicativos de terceiros toorelying escolhendo e outros servidores de STS nas organizações confiáveis.
2. **Implante controladores de domínio do Active Directory para todos os domínios de usuário Olá mesma rede como servidores de saudação do AD FS.**
   
    Servidores do AD FS usam usuários do Active Directory Domain Services tooauthenticate. É recomendável toodeploy controladores de domínio em Olá mesma rede como servidores do hello AD FS. Isso fornece continuidade dos negócios no caso de link de saudação entre Olá rede do Azure e sua rede local será interrompida e permite que a latência mais baixa e melhor desempenho para logons.
3. **Implante vários nós do AD FS para alta disponibilidade e balanceamento de carga de saudação.**
   
    Na maioria dos casos, falha de saudação de um aplicativo que o AD FS permite é inaceitável porque os aplicativos de saudação que requerem tokens de segurança geralmente são de missão crítica. Como resultado, e como o AD FS agora reside no hello caminho crítico tooaccessing aplicativos essenciais, o serviço de saudação AD FS deverá estar altamente disponível por meio de vários proxies do AD FS e servidores do AD FS. distribuição de tooachieve de solicitações, balanceadores de carga normalmente são implantados na frente dos Proxies do hello AD FS e servidores de saudação do AD FS.
4. **Implante um ou mais nós de Proxy de Aplicativo Web para acessar a Internet.**
   
    Quando os usuários precisam tooaccess aplicativos protegidos pelo serviço do hello AD FS, Olá AD FS serviço necessidades toobe disponíveis do hello da internet. Isso é feito ao implantar o serviço de Proxy de aplicativo Web hello. É altamente recomendável toodeploy mais de um nó para fins de saudação de alta disponibilidade e balanceamento de carga.
5. **Restringir o acesso de recursos de rede toointernal de nós de Proxy de aplicativo Web hello.**
   
    tooallow usuários externos tooaccess do AD FS do Olá da internet, você precisa de nós de Proxy de aplicativo Web toodeploy (ou Proxy do AD FS em versões anteriores do Windows Server). Olá proxy de aplicativo Web nós são diretamente expostos toohello da Internet. Eles não são necessário toobe ingressado no domínio e eles só precisam acessar servidores do toohello AD FS em portas TCP 443 e 80. É altamente recomendável que tooall comunicação outros computadores (especialmente controladores de domínio) está bloqueada.
   
    Isso é normalmente obtido no local por meio de uma DMZ. Os firewalls usam um modo de lista branca de tráfego de toorestrict de operação de rede de local de toohello Olá DMZ (ou seja, somente endereços IP especificados de tráfego de saudação e over especificado portas é permitida e todos os outros tráfegos são bloqueados).

Olá diagrama a seguir mostra um tradicional implantação do AD FS no local.

![Diagrama de uma implantação tradicional dos Serviços de Federação do Active Directory local](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

No entanto, como o Azure não fornece recursos de firewall nativo, completo, outras opções necessário toobe usado toorestrict tráfego. Olá tabela a seguir mostra cada opção e suas vantagens e desvantagens.

| Opção | Vantagem | Desvantagem |
| --- | --- | --- |
| [ACLs da rede do Azure](../virtual-network/virtual-networks-acl.md) |Configuração inicial mais simples e com menor custo |Configuração da ACL de rede adicional necessário se novas VMs são adicionadas toohello implantação |
| [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) |Modo de lista branca de operação e não requer configurações de ACL de rede |Aumento de custo e complexidade da configuração inicial |

Olá toodeploy de etapas de alto nível do AD FS neste caso são os seguintes:

1. Crie uma rede virtual com conectividade entre locais usando uma VPN ou a [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Implante controladores de domínio na rede virtual hello. Esta etapa é opcional, mas recomendada.
3. Implante servidores de AD FS ingressados em domínio na rede virtual hello.
4. Criar um [conjunto com balanceamento de carga interno](http://azure.microsoft.com/blog/internal-load-balancing/) que inclui servidores de saudação do AD FS e usa um novo endereço IP privado na rede virtual da saudação (um endereço IP dinâmico).
   
   1. Atualize DNS toocreate Olá FQDN toopoint toohello (dinâmico) endereço IP privado do conjunto de balanceamento de carga interno hello.
5. Crie um serviço de nuvem (ou uma rede virtual separada) para Olá nós de Proxy de aplicativo Web.
6. Implantar Olá nós de Proxy de aplicativo Web no serviço de nuvem hello ou rede virtual
   
   1. Crie um conjunto de balanceamento de carga externo que inclui nós de Proxy de aplicativo Web hello.
   2. Atualize Olá DNS FQDN (nome) toopoint toohello nuvem serviço público endereço IP externo (Olá endereço IP virtual).
   3. Configure o AD FS proxies toouse Olá FQDN que corresponde a toohello conjunto de balanceamento de carga interno para servidores do hello AD FS.
   4. Atualizar sites baseados em declarações toouse hello FQDN externo para seu provedor de declarações.
7. Restringir o acesso entre a máquina do Proxy de aplicativo Web tooany na rede virtual do hello AD FS.

tráfego toorestrict, conjunto de balanceamento de carga Olá para o balanceador de carga interno do Azure Olá precisa toobe configurada para apenas o tráfego tooTCP portas 80 e 443 e todos os outros tráfego toohello dinâmico endereço IP interno do conjunto de balanceamento de carga de saudação é descartado.

![Diagrama de ACLs de Rede ADFS com TCP 443 + 80 permitido.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Servidores com tráfego toohello AD FS seriam permitidos apenas por Olá as origens a seguir:

* Balanceador de carga interno do Azure Hello.
* endereço IP de saudação de um administrador de rede do local de saudação.

> [!WARNING]
> design Olá deve impedir a alcançar outras VMs na rede virtual do Azure de saudação ou todos os locais na rede de local de saudação de nós de Proxy de aplicativo Web. Isso pode ser feito configurando regras de firewall no dispositivo do local de saudação para conexões de rota expressa ou dispositivo VPN de saudação para conexões VPN site a site.
> 
> 

Uma opção de toothis desvantagem é Olá necessidade tooconfigure Olá ACLs de rede para vários dispositivos, incluindo o balanceador de carga interno, os servidores de saudação do AD FS e outros servidores que são adicionados a rede virtual toohello. Se qualquer dispositivo for adicionado toohello implantação sem configurar rede ACLs toorestrict tráfego tooit, toda a implantação Olá pode estar em risco. Se os endereços IP de saudação de nós de Proxy de aplicativo Web hello mudar, ACLs de rede Olá devem ser redefinida (que significa que os proxies Olá deve ser configurado toouse [estáticos endereços IP dinâmicos](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![ADFS no Azure com ACLS de rede.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Outra opção é Olá toouse [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) tráfego do dispositivo toocontrol entre servidores de proxy do AD FS e servidores de saudação do AD FS. Essa opção está em conformidade com as práticas recomendadas para segurança e alta disponibilidade e requer menos administração após a instalação inicial do hello porque Olá Barracuda NG Firewall oferece um modo de lista branca de administração do firewall e pode ser instalado diretamente em uma rede virtual do Azure. Que elimina ACLs de rede do hello necessidade tooconfigure qualquer momento em que um novo servidor é adicionado toohello implantação. Mas essa opção adiciona custo e complexidade à implantação inicial.

Nesse caso, duas redes virtuais são implantadas em vez de uma. Vamos chamá-las de VNet1 e VNet2. VNet1 contém proxies hello e VNet2 contém STSs hello e rede corporativa do hello rede conexão toohello voltar. VNet1 é, portanto, fisicamente (embora virtualmente) isolada da VNet2 e, por sua vez, da rede corporativa hello. VNet1 é, em seguida, tooVNet2 conectado usando uma tecnologia de túnel especial conhecida como Transport Independent Network Architecture (TINA). Olá, túnel TINA é anexado tooeach de redes virtuais hello, usando um firewall Barracuda NG — um Barracuda em cada uma das redes virtuais hello.  Para alta disponibilidade, é recomendável que você implante dois Barracudas em cada rede virtual. um ativo, Olá outro passivo. Eles oferecem recursos de firewall extremamente avançados que nos permitem toomimic operação de saudação de um DMZ local tradicional no Azure.

![ADFS no Azure com firewall.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Para obter mais informações, consulte [do AD FS: estender um aplicativo front-end de local com reconhecimento de declarações toohello Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Uma implantação tooAD alternativo FS se a meta de saudação é apenas o Office 365 SSO
Há outra alternativa toodeploying AD FS totalmente se sua meta for apenas tooenable entrar para o Office 365. Nesse caso, você pode implantar o DirSync com sincronização de senha no local e obter simplesmente Olá mesmo resultado final com mínima complexidade de implantação porque essa abordagem não exige o AD FS ou o Azure.

Olá tabela a seguir compara como os processos de entrada hello funcionam com e sem implantar o AD FS.

| Logon único do Office 365 usando o AD FS e DirSync | Mesmo logon do Office 365 usando DirSync + Sincronização de Senha |
| --- | --- |
| 1. Olá usuário registra na rede corporativa tooa e é autenticado tooWindows servidor Active Directory. |1. Olá usuário registra na rede corporativa tooa e é autenticado tooWindows servidor Active Directory. |
| 2. usuário de Olá tenta tooaccess Office 365 (eu sou @contoso.com). |2. usuário de Olá tenta tooaccess Office 365 (eu sou @contoso.com). |
| 3. O Office 365 redireciona Olá usuário tooAzure AD. |3. O Office 365 redireciona Olá usuário tooAzure AD. |
| 4. Como o AD do Azure não pode autenticar o usuário hello e entende que há uma relação de confiança do AD FS local, ele redireciona Olá usuário tooAD FS. |4. O AD do Azure não pode aceitar tickets de Kerberos diretamente e não existe nenhuma relação de confiança para que ele solicita que o usuário Olá credenciais. |
| 5. Olá usuário envia uma Kerberos ticket toohello AD FS STS. |5. usuário de Olá insere Olá mesma senha local e o AD do Azure valida em relação a saudação nome e a senha que foram sincronizada pelo DirSync. |
| 6. O AD FS transforma Olá toohello de tíquete Kerberos necessário formato/as declarações de token e redireciona Olá usuário tooAzure AD. |6. AD do Azure redireciona Olá usuário tooOffice 365. |
| 7. usuário de Olá autentica tooAzure AD (outra transformação ocorre). |7. Olá usuário possa acessar tooOffice 365 e OWA usando o token de saudação do AD do Azure. |
| 8. AD do Azure redireciona Olá usuário tooOffice 365. | |
| 9. usuário de Olá é conectado silenciosamente tooOffice 365. | |

No Office 365 com o DirSync Olá com cenário de sincronização de senha (sem AD FS), é substituído logon único por "mesmo logon" onde "mesmo" significa apenas que os usuários devem digitar novamente as mesmas credenciais locais ao acessar o Office 365. Observe que esses dados podem ser lembrados pelo toohelp do navegador do usuário Olá reduzir avisos subsequentes.

### <a name="additional-food-for-thought"></a>Ideias adicionais
* Se você implantar um proxy do AD FS em uma máquina virtual do Azure, servidores do conectividade toohello AD FS é necessário. Se eles estiverem no local, é recomendável aproveitar a conectividade VPN site a site Olá fornecida pelo toocommunicate de nós de Proxy de aplicativo Web hello rede virtual tooallow Olá com seus servidores do AD FS.
* Se você implantar um servidor do AD FS em um Azure virtual da máquina, controladores de domínio do Active Directory do servidor do tooWindows de conectividade, repositórios de atributos, e bancos de dados de configuração é necessários e também pode exigir um ExpressRoute ou uma conexão de VPN site a site entre a rede de saudação do Azure virtual hello e rede local.
* Os encargos são aplicados tooall tráfego de máquinas virtuais do Azure (tráfego de saída). Se os custos forem um fator importante Olá, é aconselhável toodeploy nós de Proxy de aplicativo Web Olá no Azure, deixando os servidores de saudação do AD FS no local. Se servidores do hello AD FS são implantados em máquinas virtuais do Azure também, custos adicionais serão incorridos tooauthenticate local usuários. O tráfego de saída incorre em custo independentemente de estarem ou não atravessando Olá rota expressa ou hello conexão do VPN site a site.
* Se você optar por recursos de alta disponibilidade dos servidores do AD FS de balanceamento de carga de servidor nativo do Azure toouse, observe que o balanceamento de carga fornece investigações que são usados toodetermine Olá integridade das máquinas virtuais de saudação no serviço de nuvem Olá. No caso de saudação de máquinas virtuais do Azure (como funções de trabalho ou tooweb contrário), uma investigação personalizada deve ser usada como agente de saudação que responde toohello investigações de padrão não está presente em máquinas virtuais do Azure. Para simplificar, você pode usar uma investigação TCP personalizada — isso exige somente que uma conexão TCP (um segmento SYN TCP enviado e respondido toowith um segmento TCP SYN ACK) seja estabelecida com êxito toodetermine integridade da máquina virtual. Você pode configurar Olá investigação personalizada toouse qualquer toowhich de porta TCP que suas máquinas virtuais estão ouvindo ativamente.

> [!NOTE]
> Máquinas virtuais que precisam Olá tooexpose que mesmo conjunto de portas diretamente toohello da Internet (como a porta 80 e 443) não é possível compartilhar Olá mesmo serviço de nuvem. Recomenda-se, portanto, que você criar um serviço de nuvem dedicados para os servidores do Windows Server AD FS em ordem tooavoid potencial sobreposto entre requisitos de porta para um aplicativo e o Windows Server AD FS.
> 
> 

## <a name="deployment-scenarios"></a>Cenários de implantação
Olá seção a seguir descreve comuns cenários toodraw atenção tooimportant considerações de implantação que devem ser levadas em conta. Cada cenário tem detalhes de toomore links sobre decisões hello e tooconsider de fatores.

1. [AD DS: implantar um aplicativo com reconhecimento de AD DS sem a necessidade de conectividade à rede corporativa](#BKMK_CloudOnly)
   
    Por exemplo, um serviço do SharePoint da Internet é implantado em uma máquina virtual do Azure. aplicativo Hello não tem dependências nos recursos de rede corporativa. Olá aplicativo requer o Windows Server AD DS, mas não exige Olá corporativa Windows Server AD DS.
2. [AD FS: Estender um aplicativo front-end de local com reconhecimento de declarações toohello da Internet](#BKMK_CloudOnlyFed)
   
    Por exemplo, um aplicativo com reconhecimento de declarações que foi implantado com êxito no local e usado por usuários corporativos precisa toobecome acessível de saudação à Internet. aplicativo Hello precisa toobe acessado diretamente pela Internet da saudação parceiros comerciais usando suas próprias identidades corporativas e por usuários corporativos existentes.
3. [AD DS: Implantar um aplicativo Windows Server reconhecimento do AD DS que exige a rede corporativa de toohello de conectividade](#BKMK_HybridExt)
   
    Por exemplo, um aplicativo com reconhecimento de LDAP que dá suporte à autenticação integrada do Windows e usa o AD DS do Windows Server como um repositório de dados de configuração e perfil do usuário é implantado em uma máquina virtual do Azure. É recomendável Olá Olá de tooleverage de aplicativo existente corporativa Windows Server AD DS e fornecer logon único. aplicativo Hello não é compatível com declarações.

### <a name="BKMK_CloudOnly"></a>1. AD DS: implantar um aplicativo com reconhecimento de AD DS sem precisar conectar-se à rede corporativa
![Implantação do AD DS somente na nuvem](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**Figura 1**

#### <a name="description"></a>Descrição
O SharePoint é implantado em uma máquina virtual do Azure e o aplicativo hello não tem nenhuma dependência dos recursos da rede corporativa. Olá aplicativos exigem Windows Server AD DS, mas não *não* exigem Olá corporativa Windows Server AD DS. Nenhuma confiança de Kerberos ou federada é necessária porque os usuários são autoprovisionados pelo aplicativo hello no domínio do Windows Server AD DS de saudação que também está hospedado na nuvem de saudação em máquinas virtuais do Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerações do cenário e como aplicam as áreas tecnológicas toohello cenário
* [Topologia de rede](#BKMK_NetworkTopology): criar uma rede virtual do Azure sem conectividade entre locais (também conhecida como conectividade site a site).
* [Configuração de implantação do controlador de domínio](#BKMK_DeploymentConfig): implantar um novo controlador de domínio em uma nova floresta do Active Directory do Windows Server de domínio único. Isso deve ser implantado junto com o servidor de DNS do Windows hello.
* [Topologia de site do Active Directory do Windows Server](#BKMK_ADSiteTopology): site de Active Directory do Windows Server usar saudação padrão (todos os computadores estarão no Default-First-Site-Name).
* [Endereçamento IP e DNS](#BKMK_IPAddressDNS):
  
  * Defina um endereço IP estático para Olá DC utilizando Olá Set-AzureStaticVNetIP do Azure PowerShell cmdlet.
  * Instalar e configurar o DNS do Windows Server nos controladores de domínio de saudação do Azure.
  * Configure propriedades de rede virtual Olá com nome hello e endereço IP do hello VM que hospeda as funções de servidor DNS e DC hello.
* [Catálogo global](#BKMK_GC): hello primeiro controlador de domínio na floresta Olá deve ser um servidor de catálogo global. Os DCs adicionais também devem ser configurados como GCs porque em uma floresta de domínio único, catálogo global Olá não exige nenhum trabalho adicional do hello DC.
* [Colocação do banco de dados de saudação do Windows Server AD DS e SYSVOL](#BKMK_PlaceDB): adicionar um tooDCs de disco de dados em execução como VMs do Azure no banco de dados do pedido toostore Olá Windows Server Active Directory, logs e SYSVOL.
* [Backup e restauração](#BKMK_BUR): determinar onde você deseja que os backups de estado do sistema toostore. Se necessário, adicione outro dados toohello VM do controlador de domínio toostore backups em disco.

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS: estender um aplicativo front-end de local com reconhecimento de declarações toohello da Internet
![Federação com conectividade entre locais](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**Figura 2**

#### <a name="description"></a>Descrição
Um aplicativo com reconhecimento de declarações que foi implantado com êxito no local e usado por usuários corporativos necessidades toobecome acessível diretamente da saudação da Internet. aplicativo Hello serve como um web front-end tooa banco de dados SQL que armazena dados. servidores SQL Olá usados pelo aplicativo hello também estão localizados na rede corporativa hello. Dois STSs de FS do AD do Windows Server e um balanceador de carga foram usuários corporativos de toohello implantado no local de acesso tooprovide. aplicativo Hello agora precisa toobe acessado diretamente pela Internet da saudação parceiros comerciais usando suas próprias identidades corporativas e por usuários corporativos existentes.

Em um esforço toosimplify e necessidades de implantação e configuração de saudação atendem esse novo requisito, decidiu-se que dois adicionais da web front-ends e dois servidores de proxy do Windows Server AD FS ser instalados em máquinas virtuais do Azure. Todas as quatro máquinas virtuais serão expostas diretamente toohello Internet e rede de local de toohello conectividade usando a funcionalidade de VPN site a site da rede Virtual do Azure será fornecido.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerações do cenário e como aplicam as áreas tecnológicas toohello cenário
* [Topologia de rede](#BKMK_NetworkTopology): criar uma rede virtual do Azure e [configurar a conectividade entre locais](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Para cada um dos certificados do Windows Server AD FS Olá, certifique-se de que hello URL definida no modelo de certificado hello e certificados resultantes Olá podem ser alcançados pelas instâncias de saudação do Windows Server AD FS em execução no Azure. Isso pode exigir tooparts de conectividade entre locais de sua infraestrutura PKI. Por exemplo, se o ponto de extremidade do CRL Olá é baseado em LDAP e hospedado exclusivamente no local, em seguida, a conectividade entre locais será necessário. Se isso não for desejável, pode ser necessário toouse certificados emitidos por uma CA cujo CRL seja acessível pela Internet da saudação.
  > 
  > 
* [Configuração de serviços de nuvem](#BKMK_CloudSvcConfig): verifique se você tem dois serviços de nuvem a fim de fornecer dois endereços IP virtuais com carga balanceada. endereço IP virtual Olá primeiro do serviço de nuvem será direcionado toohello dois Windows Server AD FS máquinas virtuais de proxy nas portas 80 e 443. Olá proxy do Windows Server AD FS que VMs serão configurado toopoint toohello endereço IP de saudação local balanceador de carga que está à frente Olá STSs do Windows Server AD FS. endereço IP virtual Olá segundo do serviço de nuvem será direcionado toohello duas VMs em execução Olá front-end da web novamente nas portas 80 e 443. Configure uma investigação personalizada tooensure Olá balanceador de carga direcione somente o tráfego toofunctioning Windows Server AD FS proxy e web front-end VMs.
* [Configuração do servidor de Federação](#BKMK_FedSrvConfig): configurar o Windows Server AD FS como segurança federação (STS) do servidor toogenerate tokens para floresta do Active Directory do Windows Server Olá criada na nuvem hello. Definir relações de confiança de provedor de declarações de federação com parceiros diferentes de saudação de que desejar tooaccept identidades e configurar relações de confiança de terceira parte confiável com hello diferentes aplicativos toogenerate tokens.
  
    Na maioria dos cenários, os servidores proxy do AD FS do Windows Server são implantados em um recurso de acesso à Internet para fins de segurança, ao passo que suas correspondentes de federação do AD FS do Windows Server permanecem isoladas da conectividade direta com a Internet. Independentemente de seu cenário de implantação, você deve configurar seu serviço de nuvem com um endereço IP virtual que forneça um endereço IP e uma porta que é capaz de saldo de tooload em suas duas instâncias do Windows Server AD FS STS ou instâncias de proxy exposto publicamente.
* [Configuração de alta disponibilidade do Windows Server AD FS](#BKMK_ADFSHighAvail): é recomendável toodeploy um farm do Windows Server AD FS com pelo menos dois servidores para failover e balanceamento de carga. Você pode desejar tooconsider usando Olá banco de dados interno do Windows (WID) para dados de configuração do Windows Server AD FS e usar Olá interno balanceamento de carga recurso toodistribute do Azure de solicitações de entrada em servidores de saudação no farm de saudação.

Para obter mais informações, consulte Olá [guia de implantação do AD DS](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. AD DS: Implantar um aplicativo Windows Server reconhecimento do AD DS que exige a rede corporativa de toohello de conectividade
![Implantação do AD DS entre instalações](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**Figura 3**

#### <a name="description"></a>Descrição
Um aplicativo com reconhecimento de LDAP é implantado em uma máquina virtual do Azure. Ele é compatível com a autenticação integrada do Windows e usa o AD DS do Windows Server como um repositório para dados de perfil de usuário e de configuração. meta de Olá Olá Olá de tooleverage de aplicativo existente corporativa Windows Server AD DS e logon único. aplicativo Hello não é compatível com declarações. Os usuários também precisam aplicativo hello de tooaccess diretamente da saudação da Internet. toooptimize desempenho e os custos, decidiu-se que dois controladores de domínio adicionais que fazem parte do domínio corporativo Olá ser implantada juntamente com o aplicativo hello no Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerações do cenário e como aplicam as áreas tecnológicas toohello cenário
* [Topologia de rede](#BKMK_NetworkTopology): criar uma rede virtual do Azure com [conectividade entre locais](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Método de instalação](#BKMK_InstallMethod): implante DCs de domínio do Active Directory do Windows Server corporativo de saudação réplica. Para uma réplica de controlador de domínio, você pode instalar o Windows Server AD DS em Olá VM e, opcionalmente, use Olá instalar da mídia (IFM) recurso tooreduce Olá quantidade de dados que precisa toobe replicadas toohello novo controlador de domínio durante a instalação. Para obter um tutorial, confira [Instalar um controlador de domínio do Active Directory de réplica no Azure](active-directory-install-replica-active-directory-domain-controller.md). Mesmo se você usar o IFM, pode ser mais eficiente Olá toobuild DC virtual local e move nuvem toohello disco rígido Virtual (VHD) de saudação inteira em vez de replicar o Windows Server AD DS durante a instalação. Para segurança, é recomendável que você exclua Olá VHD da rede do local de saudação depois que ele foi copiado tooAzure.
* [Topologia do site do Active Directory do Windows Server](#BKMK_ADSiteTopology): criar um novo site do Azure em Serviços e Sites do Active Directory. Crie uma saudação de toorepresent de objeto de sub-rede do Active Directory do Windows Server rede virtual do Azure e adicionar Olá sub-rede toohello site. Crie um novo link de site que inclui o novo site do Azure de saudação e site Olá no qual hello Azure ponto de extremidade VPN de rede virtual está localizado em ordem toocontrol e otimizar tooand de tráfego do Windows Server Active Directory do Azure.
* [Endereçamento IP e DNS](#BKMK_IPAddressDNS):
  
  * Defina um endereço IP estático para Olá DC utilizando Olá Set-AzureStaticVNetIP do Azure PowerShell cmdlet.
  * Instalar e configurar o DNS do Windows Server nos controladores de domínio de saudação do Azure.
  * Configure propriedades de rede virtual Olá com nome hello e endereço IP do hello VM que hospeda as funções de servidor DNS e DC hello.
* [Controladores de domínio distribuídos geograficamente](#BKMK_DistributedDCs): configure redes virtuais adicionais conforme a necessidade. Se sua topologia de site do Active Directory exige DCs nas geografias que correspondem a toodifferent Azure regiões, que você deseja os sites do Active Directory toocreate adequadamente.
* [Controladores de domínio somente leitura](#BKMK_RODC): você pode implantar um RODC em Olá site do Azure, dependendo de seus requisitos para executar operações de gravação em relação a saudação DC e hello compatibilidade de aplicativos e serviços no site de saudação com os RODCs. Para obter mais informações sobre compatibilidade de aplicativos, consulte Olá [guia de compatibilidade de aplicativo de controladores de domínio somente leitura](https://technet.microsoft.com/library/cc755190).
* [Catálogo global](#BKMK_GC): GCs são necessários tooservice solicitações de logon em florestas de vários domínios. Se você não implantar um GC no hello site do Azure, incorrerá em custos de tráfego de saída porque as solicitações de autenticação causam consultas de GCs em outros sites. toominimize que o tráfego, você pode habilitar o cache de site do Azure em serviços e Sites do Active Directory para saudação de membros de grupos universais.
  
    Se você implantar um GC, configurar links de site e os custos de links de site para que o GC Olá no hello site do Azure não seja preferido como um DC de origem por outros GCs que precisam tooreplicate Olá mesmas partições de domínio parcial.
* [Colocação do banco de dados de saudação do Windows Server AD DS e SYSVOL](#BKMK_PlaceDB): adicionar um tooDCs de disco de dados em execução em VMs do Azure no banco de dados do pedido toostore Olá Windows Server Active Directory, logs e SYSVOL.
* [Backup e restauração](#BKMK_BUR): determinar onde você deseja que os backups de estado do sistema toostore. Se necessário, adicione outro dados toohello VM do controlador de domínio toostore backups em disco.

## <a name="deployment-decisions-and-factors"></a>Fatores e decisões de implantação
Esta tabela resume as áreas de tecnologia do Windows Server Active Directory Olá que são afetadas em Olá anterior cenários e Olá correspondente tooconsider decisões, com detalhes de toomore links abaixo. Algumas áreas tecnológicas podem não ser aplicável tooevery cenário de implantação, e algumas áreas tecnológicas podem ser mais críticos do cenário de implantação tooa que outras áreas tecnológicas.

Por exemplo, se você implantar um DC de réplica em uma rede virtual e sua floresta tiver apenas um domínio único, escolhendo toodeploy um servidor de catálogo global nesse caso não poderá ser toohello crítico cenário de implantação porque ele não criará adicionais de replicação requisitos. Em Olá outro lado, se Olá floresta tiver vários domínios e, em seguida, Olá decisão toodeploy um catálogo global em uma rede virtual pode afetar a largura de banda disponível, desempenho, autenticação, pesquisas de diretório e assim por diante.

| Área de tecnologia do Active Directory do Windows Server | Decisões | Fatores |
| --- | --- | --- |
| [Topologia de rede](#BKMK_NetworkTopology) |Você cria uma rede virtual? |<li>Requisitos tooaccess recursos da corporação</li> <li>Autenticação</li> <li>Gerenciamento de Contas</li> |
| [Configuração de implantação do controlador de domínio](#BKMK_DeploymentConfig) |<li>Implantar uma floresta separada sem nenhuma relações de confiança?</li> <li>Implantar uma nova floresta com federação?</li> <li>Implantar uma nova floresta com a relação de confiança da floresta do Active Directory do Windows Server ou Kerberos?</li> <li>Estender a floresta da corporação implantando um controlador de domínio de réplica?</li> <li>Estender a floresta da corporação implantando um novo domínio filho ou árvore de domínio?</li> |<li>Segurança</li> <li>Conformidade</li> <li>Custo</li> <li>Resiliência e tolerância a falhas</li> <li>Compatibilidade de aplicativos</li> |
| [Topologia do site do Active Directory do Windows Server](#BKMK_ADSiteTopology) |Como você configurar sub-redes, sites e links de sites com tráfego de toooptimize de rede Virtual do Azure e minimizar o custo? |<li>Definições de sub-rede e site</li> <li>Propriedades do link do site e notificação de alteração</li> <li>Compactação de replicação</li> |
| [Endereçamento IP e DNS](#BKMK_IPAddressDNS) |Como tooconfigure endereços IP e a resolução de nome? |<li>Use Olá Use Olá Set-AzureStaticVNetIP cmdlet tooassign um endereço IP estático</li> <li>Instalar o servidor DNS do Windows Server e configurar as propriedades de rede virtual de saudação com Olá nome e o endereço IP do hello VM que hospeda as funções de servidor DNS e DC Olá</li> |
| [Controladores de domínio distribuídos geograficamente](#BKMK_DistributedDCs) |Como tooDCs tooreplicate em separar redes virtuais? |Se sua topologia de site do Active Directory exige DCs nas geografias que correspondem a toodifferent Azure regiões, que você deseja os sites do Active Directory toocreate adequadamente. [Configurar rede virtual toovirtual rede conectividade](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate entre os controladores de domínio em redes virtuais separadas. |
| [Controladores de domínio somente leitura](#BKMK_RODC) |Usar controladores de domínio somente leitura ou graváveis? |<li>Filtrar atributos HBI/PII</li> <li>Filtrar segredos</li> <li>Limitar o tráfego de saída</li> |
| [Catálogo global](#BKMK_GC) |Instalar o catálogo global? |<li>Para uma floresta de domínio único, verifique todos os GCs de DCs</li> <li>Para uma floresta de vários domínios, os GCs são necessários para autenticação</li> |
| [Método de instalação](#BKMK_InstallMethod) |Como tooinstall DC no Azure? |Você pode: <li>Instalar o AD DS usando o Windows PowerShell ou o Dcpromo</li> <li>Mover o VHD de um DC virtual local</li> |
| [Colocação do banco de dados de saudação do Windows Server AD DS e SYSVOL](#BKMK_PlaceDB) |Onde os logs de banco de dados toostore Windows Server AD DS e o SYSVOL? |Altere os valores padrão de Dcpromo.exe. Esses arquivos críticos do Active Directory *têm que* ser colocados em Discos de Dados do Azure, em vez de discos do Sistema Operacional que implementa o cache de gravação. |
| [Backup e restauração](#BKMK_BUR) |Como toosafeguard e recuperar dados? |Criar backups de estado do sistema |
| [Configuração do servidor de federação](#BKMK_FedSrvConfig) |<li>Implantar uma nova floresta com federação na nuvem Olá?</li> <li>Implantar o AD FS local e expor um proxy na nuvem Olá?</li> |<li>Segurança</li> <li>Conformidade</li> <li>Custo</li> <li>Acesso tooapplications por parceiros de negócios</li> |
| [Configuração de serviços de nuvem](#BKMK_CloudSvcConfig) |Um serviço de nuvem é implantado implicitamente Olá a primeira vez que você criar uma máquina virtual. Você precisa de serviços de nuvem adicionais toodeploy? |<li>Uma máquina virtual ou máquinas virtuais exigem toohello exposição direta à Internet?</li> <li> Serviço de saudação que requer o balanceamento de carga?</li> |
| [Requisitos do servidor de federação para endereçamento IP público e privado (IP dinâmico versus IP virtual)](#BKMK_FedReqVIPDIP) |<li>Instância de saudação do Windows Server AD FS precisa toobe acessado diretamente da saudação da Internet?</li> <li>Aplicativo hello está sendo implantado na nuvem Olá requer seu próprio endereço IP da Internet e porta?</li> |Criar um serviço de nuvem para cada endereço IP virtual que é exigido pela sua implantação |
| [Configuração de alta disponibilidade do AD FS do Windows Server](#BKMK_ADFSHighAvail) |<li>Quantos nós em meu farm de servidores do AD FS do Windows Server?</li> <li>Quantos toodeploy de nós no meu farm de proxy do Windows Server AD FS?</li> |Resiliência e tolerância a falhas |

### <a name="BKMK_NetworkTopology"></a>Topologia de rede
Consistência de endereço IP do pedido toomeet hello e requisitos de DNS do Windows Server AD DS, é necessário criar toofirst uma [rede virtual do Azure](../virtual-network/virtual-networks-overview.md) e anexar tooit suas máquinas virtuais. Durante a criação, você deve decidir se toooptionally estender a conectividade tooyour locais corporativos de rede que conecta de maneira transparente virtual do Azure máquinas máquinas tooon locais — isso é obtido usando tecnologias de VPN tradicionais e requer que um ponto de extremidade VPN seja exposto na borda de saudação da rede corporativa hello. Ou seja, Olá VPN é iniciada na rede corporativa toohello do Azure, não vice-versa.

Observe que encargos adicionais se aplicam ao estender uma rede de local de tooyour de rede virtual além dos encargos padrão de saudação que se aplicam a tooeach VM. Especificamente, há encargos para o tempo de CPU do gateway de rede Virtual do Azure hello e Olá tráfego de saída gerado por cada VM que se comunica com computadores locais pela VPN de saudação. Para saber mais sobre encargos de tráfego de rede, confira [Visão geral de preços do Azure](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Configuração de implantação do controlador de domínio
forma Olá configurar Olá DC depende dos requisitos de Olá Olá de serviço você deseja toorun no Azure. Por exemplo, você pode implantar uma nova floresta, isolada de sua própria floresta corporativa, para testar uma prova de conceito, um novo aplicativo ou outro projeto de curto prazo que requer serviços de diretório, mas não específicas acessar toointernal os recursos corporativos.

Como um benefício, uma floresta isolada de com que controlador de domínio não replica DCs locais, resultando em saída menos tráfego de rede gerado pelo sistema hello, reduzindo custos diretamente. Para saber mais sobre encargos de tráfego de rede, confira [Visão geral de preços do Azure](http://azure.microsoft.com/pricing/).

Como outro exemplo, suponha que você tem requisitos de privacidade para um serviço, mas Olá serviço depende de acesso tooyour interno Windows Server Active Directory. Se você tem permissão toohost dados de Olá serviço em nuvem hello, você pode implantar um novo domínio filho para sua floresta interna no Azure. Nesse caso, você pode implantar um controlador de domínio para um novo domínio filho hello (sem o catálogo global de saudação em problemas de privacidade do endereço de toohelp de ordem). Esse cenário, junto com uma implantação de controlador de domínio de réplica, requer uma rede virtual para conectividade com seus controladores de domínio locais.

Se você criar uma nova floresta, escolha se toouse [relações de confiança do Active Directory](https://technet.microsoft.com/library/cc771397) ou [relações de confiança de Federação](https://technet.microsoft.com/library/dd807036). Equilibrar os requisitos de saudação ditados por compatibilidade, segurança, conformidade, custo e resiliência. Por exemplo, a vantagem tootake de [autenticação seletiva](https://technet.microsoft.com/library/cc755844) você pode escolher toodeploy uma nova floresta no Azure e criar uma relação de confiança entre a floresta de local de saudação e floresta de nuvem de saudação do Active Directory do Windows Server. Se o aplicativo hello com reconhecimento de declarações, no entanto, você pode implantar a confiança de Federação em vez de confiança de floresta do Active Directory. Outro fator será Olá custo tooeither replicar mais dados estendendo seu local nuvem do Windows Server Active Directory toohello ou gerar mais tráfego de saída como resultado da autenticação e a carga de consulta.

Os requisitos de disponibilidade e tolerância a falhas também afetam sua escolha. Por exemplo, se o link de saudação for interrompido, aplicativos que usam uma relação de confiança de Kerberos ou uma relação de confiança de Federação são todos descontinuados totalmente a menos que você tenha implantado a infraestrutura suficiente no Azure. Configurações de implantação alternativos, como controladores de domínio de réplica (graváveis ou RODCs) aumentam Olá probabilidade de ser capaz de tootolerate interrupções de link.

### <a name="BKMK_ADSiteTopology"></a>Topologia do site do Active Directory do Windows Server
Você precisa toocorrectly definir sites e links de site toooptimize de ordem de tráfego e minimizar o custo. Sites, links de sites e sub-redes afetam a topologia de replicação de saudação entre controladores de domínio e o fluxo de saudação do tráfego de autenticação. Considere Olá taxas de tráfego a seguir e, em seguida, implantar e configurar controladores de domínio de acordo com os requisitos de toohello do seu cenário de implantação:

* Há uma taxa nominal por hora para o próprio gateway hello:
  
  * Ele pode ser iniciado e interrompido conforme você quiser
  * Se for interrompido, máquinas virtuais do Azure serão isoladas da rede corporativa Olá
* O tráfego de entrada está livre
* Tráfego de saída é cobrado de acordo com muito[do Azure de uma visão geral de preços](http://azure.microsoft.com/pricing/). Você pode otimizar propriedades de link de site entre sites locais e sites da nuvem de saudação da seguinte maneira:
  
  * Se você estiver usando várias redes virtuais, configurar links de site hello e seus custos apropriadamente tooprevent Windows Server AD DS de priorizar hello Azure site em um que possa fornecer o hello mesmos níveis de serviço sem custos. Você também pode considerar desabilitar ponte Olá todos os site opção link (BASL) (que é habilitada por padrão). Isso faz com que somente os sites conectados diretamente repliquem entre si. Controladores de domínio em sites conectados transitivamente não são mais capaz de tooreplicate diretamente entre si, mas devem replicar por meio de um site ou sites comuns. Se Olá sites intermediários se tornarem indisponíveis por algum motivo, a replicação entre controladores de domínio em sites conectados transitivamente não ocorrerá mesmo se a conectividade entre os sites de saudação está disponível. Finalmente, onde seções do comportamento de replicação transitiva permanecerem desejáveis, crie sites pontes de link que contêm links de site apropriado hello e sites, como sites de rede corporativa no local.
  * [Configurar custos de link de site](https://technet.microsoft.com/library/cc794882) tooavoid adequadamente o tráfego não intencional. Por exemplo, se **tentar Site mais próximo** está ativa, certifique-se de que Olá virtual de rede sites não são Olá lado mais próximo aumentando o custo de saudação associado do objeto de link de site Olá que se conecta a saudação do Azure site back toohello rede corporativa.
  * Configurar o link de site [intervalos](https://technet.microsoft.com/library/cc794878) e [agendas](https://technet.microsoft.com/library/cc816906) de acordo com os requisitos de tooconsistency e a taxa de alterações do objeto. Alinhe a agenda de replicação com a tolerância à latência. Os DCs replicam somente Olá último estado de um valor para que o intervalo de replicação de saudação decrescente pode economizar custos se há uma taxa de alteração de objeto suficientes.
* Se a minimização de custos for uma prioridade, verifique se a replicação está agendada e se a notificação de alteração não está habilitada. Essa é a configuração de padrão de saudação ao replicar entre sites. Isso não é importante se você estiver implantando um RODC em uma rede virtual porque Olá RODC não replicará nenhuma alteração de saída. Mas, se você implantar um DC gravável, assegure-se de link de site Olá não está configurado tooreplicate atualizações com frequência desnecessária. Se você implantar um servidor de catálogo global (GC), verifique se todos os outros sites que contêm um GC replicam as partições de domínio de um DC de origem em um site que está conectado com um link de site ou links de site que têm um custo mais baixo de Olá GC no site do Azure hello.
* É possível toofurther ainda reduzir o tráfego de rede gerado pela replicação entre sites alterando o algoritmo de compactação de replicação hello. algoritmo de compactação de saudação é controlado pelo algoritmo de compactação de HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator de entrada do hello REG_DWORD do registro. valor de padrão de saudação é 3, que se correlaciona toohello algoritmo de compactação Xpress. Você pode alterar Olá too2 de valor, as alterações que Olá tooMSZip de algoritmo. Na maioria dos casos, isso aumentará a compactação hello, mas isso é feito em despesas de saudação da utilização da CPU. Para saber mais, confira [Como funciona a topologia de replicação do Active Directory](https://technet.microsoft.com/library/cc755994).

### <a name="BKMK_IPAddressDNS"></a>Endereçamento IP e DNS
As máquinas virtuais do Azure recebem "endereços arrendados para DHCP" por padrão. Como os endereços dinâmicas da rede virtual do Azure persistem com uma máquina virtual para tempo de vida de saudação da máquina virtual de saudação, requisitos de saudação do Windows Server AD DS são atendidos.

Como resultado, quando você usa um endereço dinâmico no Azure, você está de fato usando um endereço IP estático porque ele é roteável para o período de saudação de concessão de saudação e período de saudação de concessão de saudação é tempo de vida toohello igual saudação do serviço de nuvem.

No entanto, o endereço dinâmico Olá é desalocado se Olá VM for desligada. endereço IP tooprevent Olá seja desalocado, você pode [usar Set-AzureStaticVNetIP tooassign um endereço IP estático](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Resolução de nomes, implante sua própria (ou utilize uma existente) infraestrutura de servidor DNS; DNS fornecida pelo Azure não atende Olá avançado necessidades de resolução de nomes do Windows Server AD DS. Por exemplo, ele não é compatível com registros SRV dinâmicos e assim por diante. A resolução de nomes é um item de configuração essencial para clientes ingressados no domínio e controladores de domínio. Os controladores de domínio devem ser capazes de gravar registros de recursos e resolver registros de recursos de outros controladores de domínio.
Por razões de desempenho e tolerância a falhas, é serviço de DNS do Windows Server Olá tooinstall ideal em Olá DCs em execução no Azure. Configure propriedades de rede virtual do Azure Olá com nome hello e endereço IP do servidor DNS hello. Quando outras VMs na rede virtual Olá inicia, suas configurações do resolvedor de cliente DNS serão configuradas com o servidor DNS como parte da alocação de endereços IP dinâmicos hello.

> [!NOTE]
> Você não pode ingressar no local tooa do Active Directory do Windows Server AD DS domínio dos computadores que é hospedado no Azure diretamente pela Internet da saudação. Olá requisitos de porta para o Active Directory e a operação de ingresso no domínio Olá renderizam portas necessárias do toodirectly impraticável expor hello e em vigor, um inteiro toohello de controlador de domínio da Internet.
> 
> 

As máquinas virtuais registram automaticamente seu nome DNS na inicialização ou quando há uma alteração no nome.

Para obter mais informações sobre esse exemplo e outro exemplo que mostra como tooprovision Olá primeira VM e instalar o AD DS, consulte [instalar uma nova floresta do Active Directory no Microsoft Azure](active-directory-new-forest-virtual-machine.md). Para saber mais sobre como usar o Windows PowerShell, confira [Instalar o Azure PowerShell](/powershell/azureps-cmdlets-docs) e [Cmdlets de gerenciamento do Azure](/powershell/module/azurerm.compute/#virtual_machines).

### <a name="BKMK_DistributedDCs"></a>Controladores de domínio distribuídos geograficamente
O Azure oferece vantagens ao hospedar vários controladores de domínio em redes virtuais diferentes:

* Tolerância a falhas de vários sites
* Escritórios de toobranch proximidade física (latência mais baixa)

Para obter informações sobre como configurar a comunicação direta entre redes virtuais, consulte [configurar conectividade de rede rede virtual toovirtual](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Controladores de domínio somente leitura
Necessário toochoose se toodeploy leitura-gravação ou somente controladores de domínio. Você pode ser toodeploy decidido RODCs porque você não terá controle físico sobre eles, mas os RODCs projetado toobe implantado em locais onde a segurança física está em risco, como filiais.

Azure não apresenta riscos de segurança física saudação de uma filial, mas os RODCs podem ainda toobe mais econômicos porque os recursos Olá que eles fornecem são apropriados toothese ambientes embora por razões muito diferentes. Por exemplo, os RODCs não têm nenhuma replicação de saída e são tooselectively capaz de preencher segredos (senhas). Em desvantagem Olá, falta de saudação desses segredos pode exigir toovalidate de tráfego de saída sob demanda-los como autentica um usuário ou computador. Mas os segredos podem ser seletivamente preenchidos previamente e armazenados em cache.

Os RODCs fornecem uma vantagem adicional ao redor de preocupações HBI e PII porque você pode adicionar atributos que contêm dados confidenciais toohello RODC filtrado o conjunto de atributos (FAS). Olá FAS é um conjunto de atributos que não são replicadas tooRODCs personalizável. Você pode usar o hello FAS como proteção caso você não tem permissão ou não quiser toostore PII ou HBI no Azure. Para saber mais, confira [conjunto de atributos filtrados do RODC[(https://technet.microsoft.com/library/cc753459)]

Certifique-se de que os aplicativos serão compatíveis com os RODCs planejar toouse. Muitos aplicativos habilitados para Active Directory do Windows Server funcionam bem com RODCs, mas alguns aplicativos podem executar de maneira ineficiente ou falhar se não tiverem acesso tooa DC gravável. Para saber mais, confira [Guia de compatibilidade de aplicativos de controladores de domínio somente leitura](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Catálogo global
Se precisar toochoose tooinstall um catálogo global (GC). Em uma floresta de domínio único, você deve configurar todos os controladores de domínio como servidores de catálogo global. Ele não aumentará o custo porque não haverá tráfego de replicação adicional.

Em uma floresta de vários domínios, GCs são membros do grupo Universal tooexpand necessário durante o processo de autenticação hello. Se você não implantar um GC, cargas de trabalho na rede virtual Olá autenticar em um controlador de domínio no Azure indiretamente irá gerar tráfego de autenticação de saída tooquery GCs locais durante cada tentativa de autenticação.

os custos de saudação associados com os GCs serão menos previsível porque eles hospedam todos os domínios (parcialmente). Se a carga de trabalho Olá hospeda um serviço da Internet e autentica usuários no Windows Server AD DS, os custos de saudação poderão ser completamente imprevisíveis. toohelp reduzir consultas de GC fora do site de nuvem Olá durante a autenticação, você pode [habilitar o cache de associação de grupo Universal](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Método de instalação
Você precisa toochoose como tooinstall Olá controladores de domínio na rede virtual hello:

* Promova novos controladores de domínio. Para saber mais, confira [Instalar uma nova floresta do Active Directory em uma rede virtual do Azure](active-directory-new-forest-virtual-machine.md).
* Mova Olá VHD de uma nuvem de toohello do controlador de domínio virtual local. Nesse caso, você deve garantir que Olá a controlador de domínio virtual foi "movido" não "copiado" ou "clonado". no local

Use máquinas virtuais do Azure somente para controladores de domínio (como tooAzure contrário "web" ou "trabalho" VMs de função). Elas são duráveis e é necessário ter durabilidade de estado para um controlador de domínio. As máquinas virtuais do Azure são projetadas para cargas de trabalho como controladores de domínio.

Não use SYSPREP toodeploy ou clonar controladores de domínio. Olá capacidade tooclone controladores de domínio está disponível somente a partir do Windows Server 2012. saudação de recurso de clonagem exige suporte para VMGenerationID no hipervisor subjacente hello. O Hyper-V no Windows Server 2012 e as redes virtuais do Azure dão suporte a VMGenerationID, como fornecedores de software de virtualização de terceiros.

### <a name="BKMK_PlaceDB"></a>Colocação do banco de dados de saudação do Windows Server AD DS e SYSVOL
Selecione onde toolocate Olá banco de dados do Windows Server AD DS, logs e SYSVOL. Eles devem ser implantados em discos de dados do Azure.

> [!NOTE]
> Discos de dados do Azure são restritos too1 TB.
> 
> 

Por padrão, as unidades de disco de dados não fazem gravações em cache. Unidades de disco de dados que estão anexado tooa VM usar cache de gravação. Gravação por cache torna se Olá gravação seja confirmada toodurable armazenamento do Azure antes da conclusão da perspectiva de saudação do sistema operacional da VM Olá transação hello. Ele fornece a durabilidade, à custa de saudação de gravações um pouco mais lentas.

Isso é importante para o Windows Server AD DS porque o cache de write-behind disco invalida as suposições feitas pelo Olá DC. Windows Server AD DS tentativas toodisable gravação em cache, mas cabe toohello toohonor de sistema de e/s de disco-lo. Cache de gravação de toodisable falha pode, em determinadas circunstâncias, introduzir a reversão do USN resultando em objetos persistentes e outros problemas.

Como prática recomendada para DCs virtuais, Olá a seguir:

* Defina configuração de preferência de Cache do Host de saudação em disco de dados do Azure Olá para nenhum. Isso evita problemas com o cache de gravação para operações do AD DS.
* Armazenar o banco de dados hello, logs e SYSVOL em Olá qualquer um dos mesmos dados em disco ou discos de dados separam. Normalmente, isso é um disco separado do disco Olá usado para o próprio sistema de operacional hello. consideração importante Olá é esse banco de dados do Windows Server AD DS hello e SYSVOL não deve ser armazenado em um tipo de disco do sistema operacional Azure. Por padrão, hello o processo de instalação do AD DS instala esses componentes na pasta % systemroot %, que não é recomendada para o Azure.

### <a name="BKMK_BUR"></a>Backup e restauração
Lembre-se do que tem ou não suporte para backup e restauração de um controlador de domínio em geral e, mais especificamente, aqueles em execução em uma VM. Confira [Considerações de Backup e Restauração para Controladores de Domínio Virtualizados](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Crie backups do estado de sistema usando apenas o software de backup que está especificamente ciente dos requisitos de backup do AD DS do Windows Server, como o Backup do Windows Server.

Não copie nem clone arquivos VHD de controladores de domínio em vez de executar backups regulares. Se houver a necessidade de restauração, faça-a usando VHDs clonados ou copiados sem o Windows Server 2012 e um hipervisor com suporte introduzirá bolhas de USN.

### <a name="BKMK_FedSrvConfig"></a>Configuração do servidor de federação
configuração de saudação de servidores de Federação (STSs) do AD FS do Windows Server depende em parte se hello aplicativos que você deseja toodeploy no Azure precisam tooaccess recursos em sua rede local.

Se aplicativos Olá atendem Olá critérios a seguir, você pode implantar aplicativos de saudação em isolamento de sua rede local.

* Eles aceitam tokens de segurança SAML
* Eles são toohello exposto à Internet
* Eles não acessam recursos locais

Nesse caso, configure os STSs do AD FS do Windows Server da seguinte maneira:

1. Configure uma floresta isolada de domínio único no Azure.
2. Fornece acesso federado toohello floresta Configurando um farm de servidores de Federação do Windows Server AD FS.
3. Configure o Windows Server AD FS (farm de servidores de Federação e farm de proxy de servidor de federação) na floresta local de saudação.
4. Estabelecer uma relação de confiança de federação entre Olá local e instâncias do Azure do AD FS do Windows Server.

Em Olá outro lado, se a aplicativos de saudação precisarem acessar os recursos locais de tooon, você poderá configurar Windows Server AD FS com o aplicativo hello no Azure da seguinte maneira:

1. Configure a conectividade entre redes locais e o Azure.
2. Configure um farm de servidores de Federação do Windows Server AD FS na floresta local de saudação.
3. Configure um farm de proxy de servidor de federação do AD FS do Windows Server no Azure.

Essa configuração tem a vantagem de saudação de reduzir a exposição de saudação de recursos locais, semelhante tooconfiguring Windows Server AD FS com aplicativos em uma rede de perímetro.

Observe que, em qualquer cenário, você pode estabelecer relações de confiança com mais provedores de identidade se houver necessidade de colaboração entre empresas.

### <a name="BKMK_CloudSvcConfig"></a>Configuração de serviços de nuvem
Serviços de nuvem são necessários se você desejar tooexpose uma VM diretamente toohello Internet ou tooexpose um com a Internet com balanceamento de carga aplicativo. Isso é possível porque cada serviço de nuvem oferece um único endereço IP virtual configurável.

### <a name="BKMK_FedReqVIPDIP"></a>Requisitos do servidor de federação para endereçamento IP público e privado (IP dinâmico versus IP virtual)
Cada máquina virtual do Azure recebe um endereço IP dinâmico. Um endereço IP dinâmico é um endereço privado que só pode ser acessado dentro do Azure. Na maioria dos casos, no entanto, será necessário tooconfigure um endereço IP virtual para suas implantações do AD FS do Windows Server. IP virtual Olá é necessário tooexpose toohello de pontos de extremidade do AD FS do Windows Server da Internet e será usado por clientes e parceiros federados para autenticação e gerenciamento contínuo. Um endereço IP virtual é uma propriedade de um serviço de nuvem que contém uma ou mais máquinas virtuais do Azure. Se o aplicativo com reconhecimento de declarações de hello implantado no Azure e o Windows Server AD FS é conectados à Internet e o compartilhamento de portas comuns, cada um exigirá um endereço IP virtual de seu próprio e, portanto, será necessário toocreate um serviço de nuvem para o aplicativo hello e um segundo, do Windows Server AD FS.

Para obter definições de endereço IP virtual de termos hello e endereço IP dinâmico, consulte [termos e definições](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Configuração de alta disponibilidade do AD FS do Windows Server
Embora seja possível toodeploy os serviços de Federação autônomo do Windows Server AD FS, é recomendável toodeploy um farm com pelo menos dois nós para STS do AD FS e proxies para ambientes de produção.

Consulte [considerações de topologia do AD FS 2.0 deployment](https://technet.microsoft.com/library/gg982489) em Olá [AD FS 2.0 Design Guide](https://technet.microsoft.com/library/dd807036) toodecide a configuração de implantação opções melhor atender às suas necessidades específicas.

> [!NOTE]
> No balanceamento de carga de tooget ordem para pontos de extremidade do Windows Server AD FS no Azure, configure todos os membros do farm de saudação do Windows Server AD FS no hello mesmo serviço de nuvem e use Olá balanceamento de carga recurso do Azure para HTTP (padrão 80) e portas HTTPS (padrão 443). Para saber mais, confira [Investigação do balanceador de carga do Azure](https://msdn.microsoft.com/library/azure/jj151530).
> Não há suporte para o NLB (balanceamento de carga de rede) do Windows Server no Azure.
> 
> 

