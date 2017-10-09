---
title: "aaaResolution para VMs e instâncias de função"
description: "Cenários de resolução de nomes para o Azure IaaS, soluções híbridas, entre diferentes serviços de nuvem, Active Directory e usando o seu próprio servidor DNS  "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Resolução de nomes de máquinas virtuais e instâncias de função
Dependendo de como você usa toohost Azure IaaS, PaaS e soluções híbridas, talvez seja necessário tooallow Olá VMs e instâncias de função que você crie toocommunicate entre si. Embora essa comunicação pode ser feita usando endereços IP, é muito mais simples nomes toouse que podem ser facilmente lembrados e não são alterados. 

Quando instâncias de função e as máquinas virtuais hospedadas no Azure precisam de endereços IP do tooresolve domínio nomes toointernal, eles podem usar um destes dois métodos:

* [Resolução de nomes fornecida pelo Azure](#azure-provided-name-resolution)
* [Resolução de nomes usando seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) (que pode encaminhar consultas toohello servidores DNS fornecidos pelo Azure) 

tipo de Olá de resolução de nome que você usa depende de como suas máquinas virtuais e instâncias de função necessário toocommunicate uns com os outros.

**Olá tabela a seguir ilustra os cenários e soluções de resolução de nome correspondente:**

| **Cenário** | **Solução** | **Suffix** |
| --- | --- | --- |
| Resolução de nomes entre instâncias de função ou máquinas virtuais localizadas em Olá mesmo serviço de nuvem ou rede virtual |[Resolução de nomes fornecida pelo Azure](#azure-provided-name-resolution) |nome de host ou FQDN |
| Resolução de nomes entre instâncias de função ou máquinas virtuais localizadas em redes virtuais diferentes |Servidores DNS gerenciados pelo cliente que encaminham consultas entre redes virtuais para resolução pelo Azure (proxy DNS).  Confira [Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Somente FQDN |
| Resolução de nomes de serviço e de computador locais em instâncias de função ou VMs no Azure |Servidores DNS gerenciados pelo cliente (por exemplo, controlador de domínio local, controlador de domínio somente leitura local ou DNS secundário sincronizado usando transferências de zona).  Confira [Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Somente FQDN |
| Resolução de nomes de host do Azure de computadores locais |Encaminhar consultas tooa gerenciada pelo cliente proxy servidor DNS na rede virtual correspondente de saudação, servidor de proxy de saudação encaminha consultas tooAzure para resolução. Confira [Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |Somente FQDN |
| DNS inverso para IPs internos |[Resolução de nome usando o seu próprio servidor DNS](#name-resolution-using-your-own-dns-server) |n/d |
| Resolução de nomes entre VMs ou instâncias de função localizadas em serviços de nuvem diferente, não em uma rede virtual |Não aplicável. Não há suporte para a conectividade entre máquinas virtuais e instâncias de função em diferentes serviços de nuvem fora de uma rede virtual. |n/d |

## <a name="azure-provided-name-resolution"></a>Resolução de nomes fornecida pelo Azure
Junto com a resolução de nomes DNS públicos, o Azure fornece resolução de nome interno para VMs e Olá de instâncias de função que residem no mesmo serviço de nuvem ou rede virtual.  Máquinas virtuais/instâncias em um serviço de nuvem compartilham Olá DNS mesmo sufixo (forma Olá hostname sozinho é suficiente), mas em serviços de nuvem diferentes redes virtuais clássicas tem vários sufixos DNS Olá FQDN é necessário tooresolve nomes entre diferentes serviços de nuvem.  Em redes virtuais no modelo de implantação do Gerenciador de recursos de Olá, sufixo DNS Olá é consistente entre a rede virtual hello (por Olá FQDN não é necessário) e nomes DNS podem ser atribuídos NICs tooboth e VMs. Embora a resolução de nomes fornecida pelo Azure não requer qualquer configuração, não é a opção apropriada Olá para todos os cenários de implantação, como mostrado na tabela de saudação acima.

> [!NOTE]
> No caso de saudação de funções da web e de trabalho, você também pode acessar os endereços IP internos Olá de instâncias de função com base em produtos de número de nome e a instância de função hello usando Olá API de REST do gerenciamento de serviços do Azure. Para obter mais informações, veja [Referência da API REST de Gerenciamento de Serviços](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Recursos e considerações
**Recursos:**

* Facilidade de uso: nenhuma configuração é necessária na ordem toouse resolução de nomes fornecida pelo Azure.
* serviço de resolução de nome de fornecida pelo Azure de saudação é altamente disponível, salvando você hello necessário toocreate e gerenciar clusters de servidores DNS.
* Pode ser usado em conjunto com seu próprios tooresolve de servidores DNS locais e nomes de host do Azure.
* Resolução de nomes é fornecida entre instâncias de função/VMs em Olá mesmo serviço sem a necessidade de um FQDN na nuvem.
* Resolução de nomes é fornecida entre VMs em redes virtuais que usam o modelo de implantação do Gerenciador de recursos de hello, sem necessidade de saudação FQDN. Redes virtuais no modelo de implantação clássico Olá exigem Olá FQDN durante a resolução de nomes em diferentes serviços de nuvem. 
* Você pode usar nomes de host que descrevem melhor as suas implantações, em vez de trabalhar com nomes gerados automaticamente.

**Considerações:**

* sufixo DNS criado pelo Azure Olá não pode ser modificado.
* Não é possível registrar manualmente seus próprios registros.
* Não há suporte para o WINS e NetBIOS. (Você não pode ver suas VMs no Windows Explorer.)
* Os nomes de host devem ser compatíveis com DNS (eles devem usar somente 0-9, a-z e '-' e não podem começar ou terminar com um '-'. Consulte o RFC 3696, seção 2).
* O tráfego da consulta DNS é restrita a cada VM. Isso não deve afetar a maioria dos aplicativos.  Se a limitação da solicitação for observada, certifique-se de que o armazenamento em cache do cliente está habilitado.  Para obter mais detalhes, consulte [obtendo hello mais da resolução de nomes fornecida pelo Azure](#Getting-the-most-from-Azure-provided-name-resolution).
* Apenas as VMs no hello primeiro 180 serviços de nuvem são registradas para cada rede virtual em um modelo de implantação clássico. Isso não se aplica a redes toovirtual em modelos de implantação do Gerenciador de recursos.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Obtendo hello mais da resolução de nomes fornecida pelo Azure
**Armazenamento em cache no lado cliente:**

Nem todas as consultas DNS precisa toobe enviado pela rede hello.  O cache do cliente ajuda a reduzir a latência e melhorar a pontos de luz resiliência toonetwork Resolvendo recorrentes consultas DNS de um cache local.  Os registros DNS contêm um tempo de vida (TTL) que permite que o registro de saudação do hello cache toostore por tempo possível sem afetar a atualização de registro, portanto, o cache do cliente é adequado para a maioria das situações.

padrão de saudação cliente DNS do Windows tem um cache DNS interno.  Alguns Linux distribuições não incluem o armazenamento em cache por padrão, é recomendável que um seja adicionada tooeach VM do Linux (depois de verificar se há um cache local estiver).

Há um número de diferentes DNS cache pacotes disponíveis, por exemplo, dnsmasq, aqui estão Olá etapas tooinstall dnsmasq em distribuições mais comuns de saudação:

* **Ubuntu (usa resolvconf)**:
  * apenas instalação Olá dnsmasq pacote ("sudo apt get install dnsmasq").
* **SUSE (usa netconf)**:
  * instalar o pacote de dnsmasq hello ("sudo zypper instalar dnsmasq") 
  * Habilitar o serviço de dnsmasq hello ("systemctl habilitar dnsmasq.service") 
  * Iniciar o serviço de dnsmasq hello ("systemctl início dnsmasq.service") 
  * Editar "/ etc/sysconfig/rede/configuração" e alterar NETCONFIG_DNS_FORWARDER = "" muito "dnsmasq"
  * atualizar o cache resolv. conf ("atualização netconfig") tooset hello como Olá resolvedor DNS local
* **OpenLogic (usa NetworkManager)**:
  * instalar o pacote de dnsmasq hello ("sudo yum install dnsmasq")
  * Habilitar o serviço de dnsmasq hello ("systemctl habilitar dnsmasq.service")
  * Iniciar o serviço de dnsmasq hello ("systemctl início dnsmasq.service")
  * Adicionar "preceda o nome-domínio-servidores 127.0.0.1;" too"/etc/dhclient-eth0.conf"
  * Reinicie o cache tooset saudação do ("rede reiniciar o serviço") de serviço de rede Olá Olá resolvedor DNS local

> [!NOTE]
> pacote de 'dnsmasq' Hello é apenas uma saudação vários caches DNS disponíveis para Linux.  Antes de usá-lo, verifique sua adequação para suas necessidades específicas e se nenhum outro cache está instalado.
> 
> 

**Tentativa no lado do cliente:**

O DNS é principalmente um protocolo UDP.  Como Olá protocolo UDP não garante a entrega de mensagens, lógica de repetição é processada no próprio protocolo DNS hello.  Cada cliente DNS (sistema operacional) pode apresentar a lógica de repetição diferente dependendo da preferência de criadores de saudação:

* Sistemas operacionais Windows tentam novamente depois de 1 segundo e, em seguida, novamente após outros 2, 4 e outros 4 segundos. 
* Olá tentativas de instalação Linux padrão depois de 5 segundos.  É recomendável toochange este tooretry 5 vezes intervalos de 1 segundo.  

toocheck Olá configurações atuais em uma VM do Linux, 'cat /etc/resolv.conf' e procure na linha de 'Opções' hello, por exemplo:

    options timeout:1 attempts:5

arquivo de resolv. conf Olá é normalmente gerado automaticamente e não deve ser editado.  etapas específicas de saudação para adicionar a linha 'Opções' hello variam de acordo com a distribuição:

* **Ubuntu** (usa resolvconf):
  * Adicionar Olá opções linha too'/etc/resolveconf/resolv.conf.d/head' 
  * executar tooupdate 'resolvconf -u'
* **SUSE** (usa netconf):
  * Adicione 'tentativas timeout:1: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = "" parâmetro em '/ etc/sysconfig/rede/configuração' 
  * executar tooupdate 'netconfig update'
* **OpenLogic** (usa NetworkManager):
  * Adicionar too'/etc/NetworkManager/dispatcher.d/11-dhclient 'echo "opções timeout:1 tentativas: 5" ' ' 
  * Execute o 'serviço rede restart' tooupdate

## <a name="name-resolution-using-your-own-dns-server"></a>Resolução de nome usando o seu próprio servidor DNS
Há várias situações em que as suas necessidades de resolução de nome podem ir além dos recursos de saudação fornecidos pelo Azure, por exemplo quando usando domínios do Active Directory ou quando precisar de resolução DNS entre redes virtuais (vnets).  toocover nesses cenários, o Azure fornece a capacidade de saudação para você toouse seus próprios servidores DNS.  

Servidores DNS em uma rede virtual podem encaminhar resolvedores de recursiva do DNS consultas tooAzure tooresolve hostnames dentro da rede virtual.  Por exemplo, um controlador de domínio (DC) em execução no Azure pode responder a consultas tooDNS para seus domínios e encaminhar todos os outros tooAzure de consultas.  Isso permite que as VMs toosee seus recursos locais (via Olá controlador de domínio) e o fornecida pelo Azure nomes de host (por meio do encaminhador de saudação).  Resolvedores de recursiva do acesso tooAzure é fornecido através da saudação IP virtual 168.63.129.16.

Encaminhamento de DNS também permite a resolução de DNS inter-rede virtual e permite que seu tooresolve de máquinas locais hostnames fornecida pelo Azure.  Em ordem tooresolve nome do host da VM, VM do servidor DNS Olá deve residir no hello mesmo virtual de rede e ser configurado tooforward tooAzure de consultas de nome de host.  Como o sufixo DNS Olá é diferente em cada rede virtual, você pode usar o encaminhamento condicional regras toosend DNS consulta toohello corrigir a rede virtual para resolução.  Olá a imagem a seguir mostra dois vnets e uma rede local fazendo usando esse método de resolução de DNS inter-vnet.  Um encaminhador DNS de exemplo está disponível no hello [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) e [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS entre redes virtuais](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Ao usar a resolução de nomes fornecida pelo Azure, um sufixo de DNS interno (*. internal.cloudapp.net) é fornecido tooeach VM usando DHCP.  Isso permite que a resolução de nome de host de nome de host de saudação são registros na zona de internal.cloudapp.net hello.  Ao usar sua própria solução de resolução de nome, Olá IDNS sufixo não é fornecido tooVMs porque interfira com outras arquiteturas DNS (como cenários de domínio).  Em vez disso, fornecemos um espaço reservado que não funciona (reddog.microsoft.com).  

Se necessário, sufixo de DNS interno Olá pode ser determinado usando a API do PowerShell ou hello:

* Para redes virtuais nos modelos de implantação do Gerenciador de recursos, sufixo hello está disponível por meio de saudação [placa de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx) recurso ou por meio de saudação [AzureRmNetworkInterface Get](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet.    
* Em modelos de implantação clássico, sufixo hello está disponível por meio de saudação [obter API de implantação](https://msdn.microsoft.com/library/azure/ee460804.aspx) chamar ou por meio de saudação [Get-AzureVM-depurar](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet.

Se o encaminhamento de consultas tooAzure não atender às suas necessidades, você precisará tooprovide sua própria solução DNS.  A solução DNS precisará:

* Forneça uma resolução de nomes do host apropriada, por exemplo, por meio do [DDNS](virtual-networks-name-resolution-ddns.md).  Observe que, se usar DDNS talvez seja necessário toodisable DNS limpeza de registro como concessões de DHCP do Azure são muito longas e eliminação pode remover o DNS registra prematuramente. 
* Fornece a resolução recursiva apropriado de tooallow de resolução de nomes de domínio externo.
* Ser acessível (TCP e UDP na porta 53) de clientes Olá serve e ser capaz de tooaccess Olá da internet.
* Ser protegida contra o acesso de saudação à internet, ameaças de toomitigate impostas por agentes externos.

> [!NOTE]
> Para melhor desempenho, ao usar máquinas virtuais do Azure como servidores DNS, o IPv6 deve ser desabilitado e uma [IP público em nível de instância](virtual-networks-instance-level-public-ip.md) devem ser atribuídas a VM do servidor DNS tooeach.  Se você escolher toouse Windows Server como seu servidor DNS, [neste artigo](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) fornece análise de desempenho adicionais e otimizações.
> 
> 

### <a name="specifying-dns-servers"></a>Especificar servidores DNS
Ao usar seus próprios servidores DNS, o Azure fornece Olá capacidade toospecify vários servidores DNS por rede virtual ou por rede interface (Gerenciador de recursos) / (clássico) do serviço de nuvem.  Os servidores DNS especificados para uma interface de rede/serviço de nuvem obtém precedência sobre os especificados para a rede virtual hello.

> [!NOTE]
> Propriedades de conexão de rede, como o servidor DNS IPs, não devem ser editados diretamente em máquinas virtuais do Windows como eles podem obter apagados durante o serviço de reparo quando o adaptador de rede virtual Olá é substituído. 
> 
> 

Ao usar o modelo de implantação do Gerenciador de recursos de hello, servidores DNS podem ser especificados em Olá Portal, API/modelos ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) ou o PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [nic](https://msdn.microsoft.com/library/mt619370.aspx)).

Ao usar o modelo de implantação clássico hello, servidores DNS para a rede virtual Olá pode ser especificado em Olá Portal ou [Olá *configuração de rede* arquivo](https://msdn.microsoft.com/library/azure/jj157100).  Para serviços de nuvem, os servidores DNS Olá são especificados por meio de [Olá *configuração do serviço* arquivo](https://msdn.microsoft.com/library/azure/ee758710) ou do PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Se você alterar as configurações de DNS Olá para um computador de rede virtual/virtual que já foi implantado, você precisa toorestart cada VM afetado para Olá alterações tootake efeito.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Modelo de implantação do Gerenciador de Recursos:

* [Criar ou atualizar uma rede virtual](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Criar ou atualizar uma placa de interface de rede](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Modelo de implantação clássico:

* [Esquema de configuração de serviço do Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Esquema de configuração de Rede Virtual](https://msdn.microsoft.com/library/azure/jj157100)
* [Configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md) 

