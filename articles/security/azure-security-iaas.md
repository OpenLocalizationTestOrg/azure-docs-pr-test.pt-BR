---
title: "aaaSecurity melhor práticas para IaaS cargas de trabalho no Azure | Microsoft Docs"
description: " migração de saudação de cargas de trabalho tooAzure IaaS traz oportunidades tooreevaluate nossos designs "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Práticas recomendadas de segurança para as cargas de trabalho IaaS no Azure

Pensar sobre a infraestrutura de tooAzure movendo cargas de trabalho é iniciado como um serviço (IaaS), você provavelmente percebeu que algumas considerações estão familiarizadas. Talvez você já tenha experiência em proteger os ambientes virtuais. Quando você move tooAzure IaaS, você pode aplicar sua experiência na proteção de ambientes virtuais e usar um novo conjunto de opções toohelp proteger seus ativos.

Vamos começar dizendo que, não esperamos toobring recursos locais como tooAzure-para-um. Olá novos desafios e novas opções de saudação colocar oportunidade tooreevaluate existente deigns, ferramentas e processos.

A responsabilidade de segurança é baseada no tipo de saudação do serviço de nuvem. Olá gráfico a seguir resume o equilíbrio de saudação de responsabilidade pela Microsoft e você:


![Áreas de Responsabilidade](./media/azure-security-iaas/sec-cloudstack-new.png)


Vamos discutir algumas das opções de saudação disponíveis no Azure que pode ajudá-lo a atender aos requisitos de segurança da sua organização. Tenha em mente que os requisitos de segurança podem variar para tipos diferentes de cargas de trabalho. Nenhuma dessas práticas recomendadas pode, por si só, proteger seus sistemas. Como tudo na segurança, você tem opções apropriadas de saudação toochoose e veja como soluções Olá podem se complementam, preenchendo as lacunas.

## <a name="use-privileged-access-workstations"></a>Usar Estações de Trabalho com Acesso Privilegiado

Geralmente as organizações favorecer toocyberattacks porque os administradores executam ações durante o uso de contas com direitos elevados. Geralmente, isso não é feito com más intenções, mas porque a configuração existente e os processos permitem fazê-lo. A maioria desses usuários entender o risco de saudação dessas ações do ponto de vista conceitual, mas ainda escolher toodo-los.

Fazer coisas como verificar email e navegação Olá Internet parecerem inocentes o suficiente. Mas eles podem expor toocompromise de contas com privilégios elevados por atores mal-intencionados que podem usar atividades de navegação, especialmente criados emails ou enterprise de tooyour outras técnicas toogain acesso. É altamente recomendável o uso de saudação de estações de trabalho de gerenciamento seguro para realizar todas as tarefas de administração do Azure, como uma maneira de reduzir o comprometimento de tooaccidental exposição.

As Estações de Trabalho com Acesso Privilegiado (PAWs) fornecem um sistema operacional dedicado para as tarefas confidenciais protegido contra ataques da Internet e vetores de ameaça. Separando essas tarefas confidenciais e contas do hello estações de trabalho de uso diário e dispositivos fornece forte proteção contra ataques de phishing, aplicativo e vulnerabilidades de sistema operacional, vários ataques de representação e ataques de roubo de credenciais, como o pressionamento de tecla registro em log, passagem de Hash e passagem de tíquete.

Olá PAW abordagem é uma extensão da saudação bem estabelecida e recomendado prática toouse uma conta administrativa individualmente atribuída separada de uma conta de usuário padrão. Uma PAW fornece uma estação de trabalho confiável para essas contas confidenciais.

Para obter mais informações e orientações de implementação, confira [Estações de trabalho de acesso privilegiado](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Usar Autenticação Multifator

Olá anterior, o perímetro da rede foi toocorporate toocontrol usado acessar os dados. Em um mundo de nuvem, móveis, primeiro, a identidade é o plano de controle de saudação: você usar serviços de tooIaaS toocontrol acesso de qualquer dispositivo. Você também usar isso tooget visibilidade e informações sobre onde e como seus dados estão sendo usados. Protegendo a identidade digital Olá dos usuários do Azure é a base de saudação de proteger suas assinaturas do roubo de identidade e aos outros cybercrimes.

Uma das etapas vantajoso hello, que você pode seguir toosecure uma conta é tooenable autenticação de dois fatores. Autenticação de dois fatores é uma maneira de autenticar usando algo na senha de tooa de adição. Ajuda a atenuar o risco de saudação do access por alguém que gerencia tooget senha de outra pessoa.

[Autenticação multifator do Azure](../multi-factor-authentication/multi-factor-authentication.md) ajuda a proteger aplicativos e acesso toodata atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de opções de fácil verificação: chamada telefônica, mensagem de texto ou notificação de aplicativo móvel. Os usuários escolher método hello que preferem.

toouse de maneira mais fácil de saudação multi-Factor Authentication é Olá Microsoft Authenticator aplicativo móvel que pode ser usado em dispositivos móveis que executam Windows, iOS e Android. Com a versão mais recente de saudação do Windows 10 e a integração do Active Directory local com o Azure Active Directory (AD do Azure), Olá [Windows Hello para empresas](../active-directory/active-directory-azureadjoin-passport-deployment.md) pode ser usado para perfeita único logon tooAzure recursos. Nesse caso, o dispositivo de saudação Windows 10 é usado como o segundo fator de saudação para autenticação.

Contas que gerenciam sua assinatura do Azure e para contas que podem entrar em máquinas de toovirtual, usando a autenticação multifator fornece um nível muito maior de segurança que o uso de apenas uma senha. Outras formas de autenticação de dois fatores podem funcionar muito bem, mas implantá-las pode ser complicado se ainda não estiverem em produção.

Olá seguinte captura de tela mostra algumas das opções de saudação disponíveis para o Azure multi-Factor Authentication:

![Opções da Autenticação Multifator](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Limitar e restringir o acesso administrativo

É extremamente importante proteger contas Olá que podem gerenciar sua assinatura do Azure. comprometimento de saudação de qualquer uma dessas contas nega valor Olá Olá todas as outras etapas que você pode levar a confidencialidade de saudação tooensure e integridade dos dados. Recentemente ilustrada Olá [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) vazamento de informações confidenciais, ataques internos representem uma ameaça enorme toohello geral de segurança de qualquer organização.

Avalie o indivíduos para direitos administrativos toothese semelhante do seguintes critérios:

- Eles estão realizando tarefas que exigem privilégios administrativos?
- Frequência são executadas as tarefas Olá?
- Há um motivo específico por tarefas de saudação não podem ser executadas por outro administrador em nome deles?

Documente todos os outros privilégios de saudação toogranting abordagens alternativas conhecidos e por que cada não é aceitável.

uso de saudação da administração just-in-time impede a existência desnecessários Olá de contas com direitos elevados durante períodos quando esses direitos não são necessários. Contas que têm direitos elevados por tempo limitado para que os administradores possam fazer seus trabalhos. Em seguida, esses direitos são removidos no final de saudação de um turno ou quando uma tarefa é concluída.

Você pode usar [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, monitorar e controlar o acesso em sua organização. Ele ajuda você a permanecer ciente de ações de saudação que indivíduos executar em sua organização. Ele também traz administração just-in-time tooAzure AD introduzindo o conceito de saudação do grupo administradores qualificados. Esses são os indivíduos que têm contas com toobe potencial Olá concedido direitos de administrador. Esses tipos de usuários podem passar por um processo de ativação e receber direitos de administrador por um tempo limitado.


## <a name="use-devtest-labs"></a>Usar DevTest Labs

Usando o Azure para ambientes de desenvolvimento e laboratórios habilita a agilidade toogain organizações de teste e desenvolvimento por atrasos Olá longe levando que apresenta a aquisição de hardware. Infelizmente, a falta de familiaridade com o Azure ou um toohelp desejo agilizar sua adoção pode levar Olá administrador toobe excessivamente permissivo com atribuição de direitos. Esse risco pode expor acidentalmente Olá organização toointernal ataques. Alguns usuários podem receber muito mais acesso do que deveriam.

Olá [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) serviço usa [o controle de acesso](../active-directory/role-based-access-control-what-is.md) (RBAC). Usando o RBAC, você pode separar as tarefas dentro de sua equipe em funções que concedem apenas o nível de saudação de acesso necessário para os usuários toodo seus trabalhos. O RBAC vem com funções predefinidas (proprietário, usuário do laboratório e colaborador). Você pode usar essas funções tooassign direitos tooexternal os parceiros e simplificam bastante a colaboração.

Como o DevTest Labs usa RBAC, é possível toocreate adicional, [funções personalizadas](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs não apenas simplifica o gerenciamento de saudação de permissões, ele simplifica o processo de saudação da obtenção de ambientes provisionados. Ele também ajuda a lidar com outros desafios típicos de equipes que trabalham em ambientes de desenvolvimento e teste. Requer alguma preparação, mas a longo prazo de hello, ele será facilitar as coisas para sua equipe.

Os principais recursos do Azure DevTest Labs incluem:

- Controle administrativo sobre Olá opções toousers disponíveis. administrador de saudação pode gerenciar centralmente as coisas como permitidos tamanhos de VM, o número máximo de VMs e quando máquinas virtuais são iniciadas e desligar.
- Automação da criação do ambiente de laboratório.
- Controle de custos.
- Distribuição simplificada das VMs para o trabalho colaborativo temporário.
- Autoatendimento que permite que os usuários tooprovision seus laboratórios usando modelos.
- Gerenciando e limitando o consumo.

![Usando o DevTest Labs toocreate um laboratório](./media/azure-security-iaas/devtestlabs.png)

Sem custo adicional está associado com o uso de saudação do DevTest Labs. criação de saudação de laboratórios, políticas, modelos e artefatos é gratuita. Você paga apenas hello Azure recursos usados em seus laboratórios, como máquinas virtuais, contas de armazenamento e redes virtuais.



## <a name="control-and-limit-endpoint-access"></a>Controlar e limitar o acesso do ponto de extremidade

Hospedagem laboratórios ou sistemas de produção no Azure significa que os sistemas toobe acessível de saudação à Internet. Por padrão, uma nova máquina virtual Windows tem porta do RDP Olá acessível de saudação à Internet, e uma máquina virtual Linux tem porta SSH de saudação aberto. Medidas toolimit exposto pontos de extremidade é necessário toominimize risco de saudação de acesso não autorizado.

Tecnologias do Azure podem ajudar a limitar Olá acesso toothose administrativas pontos de extremidade. No Azure, você pode usar os [NSGs](../virtual-network/virtual-networks-nsg.md) (grupos de segurança de rede). Quando você usa o Gerenciador de recursos do Azure para implantação, NSGs limitam o acesso de saudação de todas as redes toojust Olá gerenciamento pontos de extremidade (RDP ou SSH). Quando você pensar em NSGs, considere as ACLs do roteador. Você pode usá-los tootightly comunicação de rede de saudação controle entre vários segmentos de suas redes do Azure. Isso é semelhante redes toocreating em redes de perímetro ou outras redes isoladas. Eles não inspecionar o tráfego de hello, mas eles ajudam com a segmentação de rede.


No Azure, você pode configurar um [VPN site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) da sua rede local. Uma VPN site a site estende seu local de nuvem de toohello de rede. Isso oferece outra oportunidade toouse NSGs, porque você também pode modificar Olá toonot NSGs permitem acesso em qualquer lugar em vez de rede local hello. Em seguida, você pode exigir que a administração é feita por toohello primeiro conectar uma rede do Azure por meio de VPN.

opção de VPN site a site Olá pode ser muito atraente em casos onde você hospeda os sistemas de produção estão estritamente integrados com seus recursos locais no Azure.

Como alternativa, você pode usar o hello [ponto a site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) opção em situações em que você deseja toomanage sistemas que não precisa acessar recursos locais tooon. Esses sistemas podem ser isolados em sua própria rede virtual do Azure. Os administradores podem VPN em hello Azure hospedado ambiente a partir de sua estação de trabalho administrativa.

>[!NOTE]
>Você pode usar qualquer Olá de tooreconfigure opção VPN que ACLs no hello NSGs toonot permitem acesso toomanagement pontos de extremidade de saudação à Internet.

Outra opção que vale a pena considerar é uma implantação do [Gateway da Área de Trabalho Remota](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md). Você pode usar esta implantação toosecurely conecte os servidores de área de trabalho tooRemote via HTTPS, enquanto a aplicação mais detalhadas controla conexões toothose.

Recursos que você teria acesso tooinclude:

- Opções do administrador toolimit toorequests de conexões de sistemas específicos.
- Autenticação com cartão inteligente ou autenticação multifator do Azure.
- Controle sobre quais sistemas alguém pode gateway de conexão toovia hello.
- Controle sobre o redirecionamento do dispositivo e do disco.

## <a name="use-a-key-management-solution"></a>Uso de uma solução de gerenciamento de chaves

Gerenciamento de chave seguro é essencial tooprotecting dados na nuvem de saudação. Com o [Cofre de Chaves do Azure](../key-vault/key-vault-whatis.md), você pode armazenar com segurança as chaves de criptografia e pequenos segredos, como senhas nos módulos de segurança do hardware (HSMs). Para garantia extra, você pode importar ou gerar chaves em HSMs.

A Microsoft processará suas chaves em HSMs FIPS 140-2 Nível 2 validados (hardware e firmware). Execute o monitoramento e a auditoria do uso das chaves com o registro em log do Azure: redirecione logs no Azure ou em seu sistema SIEM (gerenciamento de eventos e de informações de segurança) para obter mais análises e detecções de ameaças.

Qualquer pessoa com uma assinatura do Azure pode criar e usar os cofres de chaves. Embora o Key Vault beneficie os desenvolvedores e administradores de segurança, ele pode ser implementado e gerenciado pelo administrador responsável por gerenciar os serviços do Azure em uma organização.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Criptografar discos virtuais e o armazenamento de discos

[Criptografia de disco do Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) endereços Olá ameaças de roubo de dados ou exposição contra acesso não autorizado é obtido pela movimentação de um disco. disco Olá pode ser anexado tooanother sistema como uma forma de Ignorar outros controles de segurança. Usa criptografia de disco [BitLocker](https://technet.microsoft.com/library/hh831713) no Windows e DM-Crypt no sistema de operacional Linux tooencrypt e unidades de dados. Criptografia de disco do Azure se integra ao Cofre de chaves toocontrol e gerenciar chaves de criptografia de saudação. Ele está disponível para VMs padrão e VMs com armazenamento premium.

Para saber mais, confira [Azure Disk Encryption em VMs IaaS com Windows e Linux](azure-security-disk-encryption.md).

A [Criptografia do Serviço de Armazenamento do Azure](../storage/common/storage-service-encryption.md) ajuda a proteger seus dados em repouso. Ele é habilitado no nível de conta de armazenamento hello. Ela criptografa os dados conforme eles são gravados em nossos data centers e eles são descriptografados automaticamente quando você a acessa. Ele dá suporte a saudação os seguintes cenários:

- Criptografia de blobs de bloco, blobs de acréscimo e blobs de páginas
- Criptografia de modelos e VHDs arquivados colocado tooAzure do local
- Criptografia de sistema operacional subjacente e discos de dados para VMs de IaaS criadas com seus VHDs

Antes de prosseguir com a Criptografia de Armazenamento do Azure, você deve estar ciente de duas limitações:

- não está disponível nas contas de armazenamento clássicas.
- só criptografa os dados gravados após a criptografia estar habilitada.

## <a name="use-a-centralized-security-management-system"></a>Usar um sistema de gerenciamento de segurança centralizado

Os servidores precisam toobe monitorado para aplicação de patch, configuração, eventos e as atividades que podem ser consideradas questões de segurança. tooaddress as preocupações, você pode usar [Central de segurança](https://azure.microsoft.com/services/security-center/) e [Operations Management Suite segurança e conformidade](https://azure.microsoft.com/services/security-center/). Ambas as opções vão além da configuração de saudação no sistema operacional de saudação. Eles também fornecem monitoramento da configuração de saudação do hello subjacente de infraestrutura, como configuração de rede e o uso do dispositivo virtual.

## <a name="manage-operating-systems"></a>Gerenciar sistemas operacionais

Em uma implantação de IaaS, você ainda é responsáveis por gerenciamento Olá sistemas de saudação que você implanta, assim como qualquer outro servidor ou estação de trabalho em seu ambiente. Aplicação de patches, proteção, atribuições de direitos e qualquer outra atividade relacionada toohello manutenção do seu sistema ainda são de sua responsabilidade. Para sistemas que são integrados com seus recursos locais, talvez você queira toouse Olá mesmas ferramentas e procedimentos que você está usando no local para coisas como antivírus, antimalware, aplicação de patch e backup.

### <a name="harden-systems"></a>Proteger sistemas
Todas as máquinas virtuais no Azure IaaS devem ser protegidas para que eles expõem apenas pontos de extremidade que são necessários para aplicativos de saudação que estão instalados. Para máquinas virtuais do Windows, siga as recomendações de saudação que a Microsoft publica como linhas de base de saudação [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) solução.

O Security Compliance Manager é uma ferramenta gratuita. Você pode usá-lo tooquickly configurar e gerenciar áreas de trabalho, datacenter tradicional e nuvem pública e privada usando a diretiva de grupo e o System Center Configuration Manager.

O Security Compliance Manager fornece políticas prontas para implantar e pacotes de configuração de DCM testados. Essas linhas de base são baseadas em recomendações das [Diretrizes de segurança da Microsoft](https://technet.microsoft.com/en-us/library/cc184906.aspx) e práticas recomendadas do setor. Elas ajudam a gerenciar os descompassos de configuração, atender aos requisitos de conformidade e reduzir as ameaças de segurança.

Você pode usar a configuração atual do Security Compliance Manager tooimport Olá dos computadores usando dois métodos diferentes. Primeiro, você pode importar as políticas de grupo baseadas no Active Directory. Em segundo lugar, é possível importar a configuração de saudação do "mestra dourada" computador de referência usando Olá [LocalGPO ferramenta](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback a diretiva de grupo local de saudação. Você pode importar política de grupo local de saudação em Security Compliance Manager.

Comparar suas práticas recomendadas para padrões tooindustry, personalizá-las e criar novas políticas e pacotes de configuração de gerenciamento de configurações desejadas. Linhas de base foram publicadas para todos os sistemas operacionais suportados, incluindo o Windows 10 Atualização de Aniversário e o Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Instalar e gerenciar o antimalware

Para ambientes hospedados separadamente do seu ambiente de produção, você pode usar um toohelp de extensão antimalware proteger suas máquinas virtuais e serviços em nuvem. Ela se integra à [Central de segurança do Azure](../security-center/security-center-intro.md).


O [Microsoft Antimalware](azure-security-antimalware.md) inclui recursos como a proteção em tempo real, verificação agendada, remediação de malware, atualizações de assinatura, atualizações do mecanismo, exemplos de relatório, coleta de eventos de exclusão e [suporte PowerShell](https://msdn.microsoft.com/library/dn771715.aspx).

![Antimalware do Azure](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Instalar atualizações de segurança mais recentes Olá
Algumas das cargas de trabalho primeiro Olá aos clientes movem tooAzure são laboratórios e sistemas de externo. Se as máquinas virtuais hospedado no Azure hospedar aplicativos ou serviços que precisam de toohello de toobe acessível da Internet, ser observa a aplicação de patch. Além do sistema operacional de saudação do patch. Vulnerabilidades sem patch em aplicativos de terceiros também podem levar a tooproblems que pode ser evitado se o gerenciamento de patches de BOM está em vigor.

### <a name="deploy-and-test-a-backup-solution"></a>Implantar e testar uma solução de backup

Assim como atualizações de segurança, um backup precisa toobe tratado Olá mesma maneira que você manipule qualquer outra operação. Isso é verdadeiro para sistemas que fazem parte de seu ambiente de produção estendendo toohello nuvem. Sistemas de teste e desenvolvimento devem seguir as estratégias de backup que fornecem recursos de restauração que são semelhantes aos usuários de toowhat já estão acostumados a, com base em sua experiência com ambientes locais.

Cargas de trabalho de produção movidas tooAzure devem integrar soluções de backup existentes quando possível. Ou, você pode usar [Backup do Azure](../backup/backup-azure-arm-vms.md) toohelp atender seus requisitos de backup.


## <a name="monitor"></a>Monitoramento

[Central de segurança](../security-center/security-center-intro.md) fornece a avaliação contínua do estado de segurança de saudação de seus recursos do Azure tooidentify possíveis vulnerabilidades de segurança. Uma lista de recomendações orienta você pelo processo de saudação de configuração de controles necessários.

Os exemplos incluem:

- Provisionamento antimalware toohelp identificar e remover softwares mal-intencionados.
- Configuração de segurança e grupos de regras toocontrol tráfego toovirtual máquinas de rede.
- O provisionamento de firewalls de aplicativo web toohelp se proteger contra ataques que seus aplicativos web de destino.
- Implantando atualizações de sistema ausentes.
- Configurações de sistema operacional que não correspondem a saudação de endereçamento recomendado linhas de base.

Olá imagem a seguir mostra algumas das opções de saudação que você pode habilitar na Central de segurança.

![Políticas da Central de Segurança do Azure](./media/azure-security-iaas/security-center-policies.png)

O [Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura de nuvem e local. Como o Operations Management Suite é implementado como um serviço baseado em nuvem, ele pode ser implantado rapidamente e com um investimento mínimo em recursos de infraestrutura.

Os novos recursos são entregues automaticamente, evitando os custos contínuos com manutenção e atualização. O Operations Management Suite também se integra com o System Center Operations Manager. Ele tem diferentes componentes toohelp você gerenciar melhor suas cargas de trabalho do Azure, incluindo um [segurança e conformidade](../operations-management-suite/oms-security-getting-started.md) módulo.

Você pode usar os recursos de segurança e conformidade Olá nas informações do Operations Management Suite tooview sobre seus recursos. Olá informações são organizadas em quatro categorias principais:

- **Domínios de segurança**: explorar mais registros de segurança ao longo do tempo. Acessar a avaliação de malware, atualizar a avaliação, informações de segurança de rede, informações de identidade e acesso e computadores com eventos de segurança. Tirar proveito do painel de controle do acesso rápido toohello Central de segurança do Azure.
- **Problemas importantes**: identificar Olá número de problemas ativos e Olá severidade desses problemas rapidamente.
- **Detecções** (visualização): identifique os padrões de ataque visualizando os alertas de segurança à medida que eles ocorrem em relação aos recursos.
- **Inteligência de ameaça**: identificar ataques padrões visualizando o número total de saudação de servidores com tráfego de IP mal-intencionado saída, Olá tipo ameaças e um mapa que mostra onde esses IPs são provenientes.
- **Consultas comuns de segurança**: consulte uma lista de segurança mais comuns de saudação consultas que você pode usar toomonitor seu ambiente. Quando você clicar em uma das consultas, Olá **pesquisa** folha é aberto e mostra os resultados de saudação para essa consulta.

Hello seguinte captura de tela mostra um exemplo de informações de saudação que pode exibir Operations Management Suite.

![Linhas de base de segurança do Operations Management Suite](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Próximas etapas


* [Blog da equipe de segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)
* [Padrões e práticas recomendadas de segurança do Azure](security-best-practices-and-patterns.md)
