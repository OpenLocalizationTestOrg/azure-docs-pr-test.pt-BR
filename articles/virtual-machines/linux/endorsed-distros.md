---
title: "aaaEndorsed distribuições do Linux | Microsoft Docs"
description: "Saiba mais sobre o Linux nas distribuições endossadas do Azure, incluindo diretrizes para Ubuntu, CentOS, Oracle e SUSE."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux em distribuições aprovadas pelo Azure
Parceiros fornecer imagens Linux em hello Azure Marketplace. Estamos trabalhando com várias tooadd de comunidades Linux ainda mais lista de distribuição aprovados toohello de tipos. Olá enquanto isso, para as distribuições que não estão disponíveis da saudação Marketplace, você pode sempre colocar sua própria Linux seguindo as diretrizes de saudação ao [criando e carregando um disco rígido virtual que contém o sistema operacional do Linux Olá](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Distribuições e versões com suporte
Olá tabela a seguir lista distribuições do Linux hello e versões com suporte no Azure. Consulte também[imagens do suporte para Linux no Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) para obter mais informações.

drivers de Integration Services LIS (Linux) de saudação do Hyper-V e do Azure são módulos de kernel que Microsoft diretamente contribui toohello upstream kernel do Linux.  Alguns drivers LIS são incorporados no kernel da distribuição Olá por padrão. Distribuições mais antigas que se baseiam no Red Hat Enterprise (RHEL)/CentOS estão disponíveis como um download separado em [Serviços de integração do Linux versão 4.1 para o Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Consulte [requisitos de kernel do Linux](create-upload-generic.md#linux-kernel-requirements) para obter mais informações sobre drivers de LIS hello.

Hello Azure Linux Agent já está instalado previamente imagens do Azure Marketplace hello e geralmente está disponível do repositório de pacotes de distribuição de saudação. O código-fonte pode ser encontrado no [GitHub](https://github.com/azure/walinuxagent).

| Distribuição | Versão | Drivers | Agente |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3: [download do LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +: no kernel |Pacote: no [repositório](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/), em "WALinuxAgent" <br/>Código-fonte: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |No kernel |Código-fonte: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+, 8.2+ |No kernel |Pacote: no repositório, em "waagent"  <br/>Código-fonte: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |No kernel |Pacote: no repositório, em "WALinuxAgent"  <br/>Código-fonte: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |No kernel |Pacote: no repositório, em "WALinuxAgent"  <br/>Código-fonte: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES para SAP<br>11 SP4<br>12 SP1+|No kernel |Pacote:<p> para 11, no repositório [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools)<br>para 12, incluído no módulo "Public Cloud" em "python-azure-agent"<br/>Código-fonte: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |No kernel |Pacote: no repositório [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) em "python-azure-agent" <br/>Código-fonte: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |No kernel |Pacote: no repositório, em "WALinuxAgent"  <br/>Código-fonte: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Parceiros

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Do site de CoreOS hello:

*O CoreOS foi projetado para segurança, consistência e confiabilidade. Em vez de instalar os pacotes por meio de yum ou apt, CoreOS usa toomanage de contêineres do Linux seus serviços em um nível mais alto de abstração. Um único código de serviço e todas as dependências são empacotados em um contêiner que pode ser executado em uma ou várias máquinas CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ é uma empresa de serviços especializada em desenvolvimento de saudação e a implementação de soluções profissionais usando software livre e de consultoria independentes. A Credative, por ser especialista e líder em software gratuito, é reconhecida internacionalmente com vários departamentos de TI que usam o suporte que a empresa fornece. Em conjunto com a Microsoft, a Credativ está preparando imagens correspondentes do Debian para Debian 8 (Jessie) e Debian antes do 7 (Wheezy). As duas imagens são especialmente projetado toorun no Azure e podem ser facilmente gerenciadas por meio de plataforma hello. Credativ também dará suporte a manutenção de longo prazo hello e atualização das imagens Debian Olá para o Azure por meio de seus centros de suporte do código-fonte aberto.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Estratégia da Oracle é toooffer um portfólio de soluções para nuvens públicas e privadas. estratégia de saudação oferece aos clientes opções e a flexibilidade em como implantar o software Oracle nas nuvens do Oracle e outras nuvens. Parceria da Oracle com o Microsoft permite que o software da Oracle toodeploy clientes em nuvens públicas e privadas da Microsoft com confiança Olá de certificação e o suporte da Oracle.  O compromisso e o investimento da Oracle em soluções de nuvem pública e privada Oracle permanecem inalterados.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Olá fornecedora líder mundo de soluções de software livre, Red Hat ajuda a mais de 90% das empresas Fortune 500 resolver desafios de negócios, alinhar sua estrutura de TI e estratégias de negócios e prepare-se para Olá futuro da tecnologia. A empresa faz isso fornecendo soluções seguras por meio de um modelo de negócios aberto e de um modelo de assinatura acessível e previsível.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

O SUSE Linux Enterprise Server no Azure é uma plataforma testada que fornece confiabilidade e segurança superiores para a computação em nuvem. Plataforma de Linux versátil do SUSE integra-se perfeitamente com toodeliver de serviços de nuvem do Azure um ambiente de nuvem facilmente gerenciáveis. Com mais de 9,200 aplicativos certificados mais de 1.800 fornecedores de software independentes para SUSE Linux Enterprise Server, SUSE garante que as cargas de trabalho em execução com suporte no Centro de dados Olá a implantação no Azure.

### <a name="canonical"></a>Canônico
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

O controle aberto da comunidade e a engenharia da Canonical impulsionam o sucesso do Ubuntu no cliente, no servidor e na computação em nuvem, que inclui serviços de nuvem pessoais para os consumidores. Visão do Canonical de uma plataforma unificada e livre no Ubuntu, de telefone toocloud, fornece uma família de interfaces coerentes para Olá telefone, tablet, TV e área de trabalho. Essa visão torna Ubuntu Olá primeira opção para diversas instituições de tomadores de toohello de provedores de nuvem pública de eletrônicos e um favorito entre especialistas em tecnologia individuais.

Com os desenvolvedores e engenharia centers Olá, mundo, Canonical é toopartner posicionada exclusivamente com tomadores de hardware, provedores de conteúdo e software desenvolvedores toobring Ubuntu soluções toomarket para PCs, servidores e dispositivos portáteis.
