---
title: "aaaDNS opções de resolução de nome para máquinas virtuais Linux no Azure"
description: "Cenários de resolução de nomes para máquinas virtuais Linux no Azure IaaS, incluindo serviços DNS fornecidos, o servidor traga seu próprio DNS e DNS externo híbrido."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Opções de resolução de nomes DNS para máquinas virtuais Linux no Azure
O Azure fornece resolução de nomes DNS por padrão para todas as máquinas virtuais que estão em uma única rede virtual. Você pode implementar sua própria solução de resolução de nomes DNS configurando seus próprios serviços DNS em suas máquinas virtuais que o Azure hospeda. Olá cenários a seguir devem ajudar a escolher Olá que funciona para sua situação.

* [Resolução de nomes que o Azure fornece](#azure-provided-name-resolution)
* [Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server)

tipo de saudação de resolução de nome que você usa depende de como suas máquinas virtuais e instâncias de função necessário toocommunicate uns com os outros.

Olá tabela a seguir ilustra os cenários e soluções de resolução de nome correspondente:

| **Cenário** | **Solução** | **Suffix** |
| --- | --- | --- |
| Resolução de nomes entre instâncias de função ou máquinas virtuais no hello mesma rede virtual |[Resolução de nomes que o Azure fornece](#azure-provided-name-resolution) |nome de host ou FQDN (nome de domínio totalmente qualificado) |
| Resolução de nomes entre as instâncias de função ou as máquinas virtuais em redes virtuais diferentes |Servidores DNS gerenciados pelo cliente que encaminham consultas entre redes virtuais para resolução pelo Azure (proxy DNS). Confira [Resolução de nomes usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Somente FQDN |
| Resolução de nomes de serviço e de computador locais em instâncias de função ou máquinas virtuais no Azure |Servidores DNS gerenciados pelo cliente (por exemplo, controlador de domínio local, controlador de domínio somente leitura local ou DNS secundário sincronizados usando transferências de zona). Confira [Resolução de nomes usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Somente FQDN |
| Resolução de nomes de host do Azure de computadores locais |Encaminhar consultas tooa gerenciada pelo cliente proxy servidor DNS na rede virtual correspondente de saudação. servidor de proxy Olá encaminha consultas tooAzure para resolução. Confira [Resolução de nomes usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server). |Somente FQDN |
| DNS inverso para IPs internos |[Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |n/d |

## <a name="name-resolution-that-azure-provides"></a>Resolução de nomes que o Azure fornece
Junto com a resolução de nomes DNS públicos, o Azure fornece resolução de nome interno para máquinas virtuais e Olá de instâncias de função que estão na mesma rede virtual. Em redes virtuais que são baseadas no Gerenciador de recursos do Azure, o sufixo DNS Olá é consistente entre a rede virtual do hello; Olá FQDN não é necessária. Os nomes DNS podem ser atribuídos a máquinas virtuais e placas de interface de rede (NICs) tooboth. Embora a resolução de nomes de hello Azure fornece não requer qualquer configuração, não é a opção apropriada Olá para todos os cenários de implantação, como visto no hello anterior da tabela.

### <a name="features-and-considerations"></a>Recursos e considerações
**Recursos:**

* Nenhuma configuração é necessária toouse resolução de nomes que o Azure fornece.
* serviço de resolução de nome de saudação que o Azure fornece está altamente disponível. Você não precisa toocreate e gerenciar clusters de servidores DNS.
* serviço de resolução de nome de saudação que o Azure fornece pode ser usado junto com sua própria tooresolve de servidores DNS locais e nomes de host do Azure.
* Resolução de nomes é fornecida entre máquinas virtuais em redes virtuais sem necessidade de saudação FQDN.
* Você pode usar nomes de host que descrevem melhor as suas implantações, em vez de trabalhar com nomes gerados automaticamente.

**Considerações:**

* sufixo DNS de Hello Azure cria não pode ser modificado.
* Não é possível registrar manualmente seus próprios registros.
* Não há suporte para o WINS e NetBIOS.
* Os nomes de host devem ser compatíveis com DNS.
    Os nomes devem usar somente 0-9, a-z e '-' e não podem começar ou terminar com um '-'. Veja a RFC 3696, seção 2.
* O tráfego da consulta DNS é restrita a cada máquina virtual. Essa limitação não deve afetar a maioria dos aplicativos.  Se a limitação da solicitação for observada, certifique-se de que o armazenamento em cache do cliente está habilitado.  Para obter mais informações, consulte [obtendo hello mais da resolução de nomes que o Azure fornece](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Obtendo hello mais da resolução de nomes que o Azure fornece
**Armazenamento em cache no lado cliente:**

Algumas consultas DNS não são enviadas pela rede hello. O cache do cliente ajuda a reduzir a latência e melhorar inconsistências de toonetwork resiliência Resolvendo recorrentes consultas DNS de um cache local. Os registros DNS contêm um tempo de vida (TTL), que permite que o registro de saudação do hello cache toostore por tempo possível sem afetar a atualização do registro. Como resultado disso, o cache do lado do cliente é adequado para a maioria das situações.

Algumas distribuições do Linux não incluem o armazenamento em cache por padrão. É recomendável que você adicione uma máquina virtual do cache tooeach Linux depois de verificar se há não um cache local já.

Vários pacotes de cache DNS diferentes, como dnsmasq, estão disponíveis. Aqui estão Olá etapas tooinstall dnsmasq em distribuições de hello mais comuns:

**Ubuntu (usa resolvconf)**
  * Instale o pacote de dnsmasq de saudação ("sudo apt get install dnsmasq").

**SUSE (usa netconf)**:
1. Instale o pacote de dnsmasq de saudação ("sudo zypper instalar dnsmasq").
2. Habilite o serviço de dnsmasq de saudação ("systemctl habilitar dnsmasq.service").
3. Inicie serviço de dnsmasq hello ("systemctl início dnsmasq.service").
4. Editar "/ etc/sysconfig/rede/configuração" e alterar NETCONFIG_DNS_FORWARDER = "" muito "dnsmasq".
5. Atualize resolv. conf ("atualização netconfig") tooset Olá cache como Olá resolvedor DNS local.

**CentOS por Rogue Wave Software (anteriormente OpenLogic) (usa o NetworkManager)**
1. Instale o pacote de dnsmasq de saudação ("sudo yum install dnsmasq").
2. Habilite o serviço de dnsmasq de saudação ("systemctl habilitar dnsmasq.service").
3. Inicie serviço de dnsmasq hello ("systemctl início dnsmasq.service").
4. Adicionar "preceda o nome-domínio-servidores 127.0.0.1;" too"/etc/dhclient-eth0.conf".
5. Reinicie o cache tooset saudação do ("rede reiniciar o serviço") de serviço de rede Olá Olá resolvedor DNS local

> [!NOTE]
> : pacote de 'dnsmasq' hello é apenas uma das Olá muitos DNS armazena em cache que estão disponíveis para Linux. Antes de usá-lo, verifique sua adequação para suas necessidades e se nenhum outro cache está instalado.
>
>

**Tentativa no lado do cliente**

O DNS é principalmente um protocolo UDP. Porque Olá protocolo UDP não garante a entrega de mensagens, Olá próprio protocolo DNS lida com a lógica de repetição. Cada cliente DNS (sistema operacional) pode apresentar a lógica de repetição diferente dependendo da preferência do criador de saudação:

* Os sistemas operacionais Windows tentam novamente após um segundo e, em seguida, novamente após mais dois, quatro e outros quatro segundos.
* Olá tentativas de instalação Linux padrão depois de cinco segundos.  Você deve alterar esse tooretry cinco vezes em intervalos de um segundo.  

toocheck Olá configurações atuais em uma máquina de virtual do Linux, 'cat /etc/resolv.conf' e observar a linha de 'Opções' hello, por exemplo:

    options timeout:1 attempts:5

arquivo de resolv. conf Olá é gerado automaticamente e não deve ser editado. Olá etapas específicas que adicionar Olá 'Opções' linha variam por distribuição:

**Ubuntu** (usa resolvconf)
1. Adicionar Olá opções linha too'/etc/resolveconf/resolv.conf.d/head'.
2. Execute tooupdate 'resolvconf -u'.

**SUSE** (usa netconf)
1. Adicione 'tentativas timeout:1: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parâmetro em '/ etc/sysconfig/rede/configuração'.
2. Execute tooupdate 'netconfig update'.

**CentOS por Rogue Wave Software (anteriormente OpenLogic)** (usa o NetworkManager)
1. Adicionar too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo "opções timeout:1 tentativas: 5" ' '.
2. Execute tooupdate 'rede reiniciar o serviço'.

## <a name="name-resolution-using-your-own-dns-server"></a>Resolução de nome usando o seu próprio servidor DNS
Suas necessidades de resolução de nome podem ir além dos recursos de saudação que o Azure fornece. Por exemplo, você pode exigir a resolução DNS entre redes virtuais. toocover neste cenário, você pode usar seus próprios servidores DNS.  

Os servidores DNS em pode uma rede virtual DNS encaminhar consultas toorecursive resolvedores de nomes de host tooresolve do Azure que estão em Olá mesma rede virtual. Por exemplo, um servidor DNS que é executado no Azure pode responder consultas tooDNS para seu próprio DNS arquivos de zonas e encaminham todos os outros tooAzure de consultas. Essa funcionalidade permite que máquinas virtuais toosee ambas as suas entradas nos arquivos de zona e os nomes de host que o Azure fornece (via encaminhador Olá). Resolvedores de recursiva toohello acesso do Azure é fornecido por meio de IP virtual de saudação 168.63.129.16.

Encaminhamento de DNS também permite a resolução de DNS entre redes virtuais e permite que o seu local máquinas tooresolve os nomes de host que o Azure fornece. tooresolve nome de host da máquina virtual, Olá máquina de virtual do servidor DNS deve residir em Olá mesma rede virtual e ser configurado tooforward tooAzure de consultas de nome de host. Como o sufixo DNS Olá é diferente em cada rede virtual, você pode usar o encaminhamento condicional regras toosend DNS consulta toohello corrigir a rede virtual para resolução. Olá imagem a seguir mostra duas redes virtuais e uma rede local fazendo a resolução DNS entre redes virtuais usando esse método:

![resolução do DNS entre redes virtuais](./media/azure-dns/inter-vnet-dns.png)

Quando você usa a resolução de nome que o Azure fornece, sufixo DNS interno Olá é fornecido máquina de virtual tooeach usando DHCP. Quando você usa sua própria solução de resolução de nome, esse sufixo não é máquinas toovirtual fornecido como sufixo Olá interfere outras arquiteturas DNS. toorefer toomachines pelo FQDN ou tooconfigure sufixo Olá em suas máquinas virtuais, você pode usar o PowerShell ou hello o sufixo de saudação do API toodetermine:

* Para redes virtuais que são gerenciadas pelo Gerenciador de recursos do Azure, sufixo hello está disponível por meio de saudação [placa de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx) recursos. Você também pode executar Olá `azure network public-ip show <resource group> <pip name>` comando toodisplay detalhes de saudação do seu IP público, o que inclui Olá FQDN do hello NIC.

Se o encaminhamento de consultas tooAzure não atender às suas necessidades, você precisa tooprovide sua própria solução DNS.  A solução do DNS precisa:

* Fornecer resolução de nome de host apropriada, por exemplo, [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Se você usar DDNS, talvez seja necessário toodisable limpeza de registro DNS. As concessões de DHCP do Azure são muito longas e a eliminação pode remover os registros DNS prematuramente.
* Fornece a resolução recursiva apropriado de tooallow de resolução de nomes de domínio externo.
* Ser acessível (TCP e UDP na porta 53) de clientes Olá serve e ser capaz de tooaccess Olá da Internet.
* Ser protegida contra o acesso de ameaças de toomitigate de Internet Olá impostas por agentes externos.

> [!NOTE]
> Para melhor desempenho, quando você usar máquinas virtuais em servidores DNS do Azure, desabilitar IPv6 e atribuir uma [IP público em nível de instância](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach máquina de virtual do servidor DNS.  
>
>
