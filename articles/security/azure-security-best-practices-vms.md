---
title: "práticas recomendadas de segurança de máquina virtual aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma variedade de segurança toobe de práticas recomendada usada em máquinas virtuais localizadas no Azure."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Práticas recomendadas para a segurança de VM do Azure

Na infraestrutura a maioria dos cenários de serviço (IaaS), [máquinas virtuais (VMs) do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/) é computação de carga de trabalho principal para organizações que usam nuvem hello. Esse fato é especialmente evidente em [cenários híbridos](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) em que as organizações deseja tooslowly migrar nuvem de toohello de cargas de trabalho. Nesses cenários, siga Olá [considerações gerais de segurança para IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)e aplicar tooall de práticas recomendada de segurança suas VMs.

Este artigo aborda várias práticas recomendadas de segurança VM, cada derivada de nossos clientes e nossas próprias experiências diretas com VMs.

práticas recomendadas de saudação baseiam-se em um consenso de opinião e trabalhar com recursos de plataforma do Azure atuais e conjuntos de recursos. Como as tecnologias e opiniões podem mudar ao longo do tempo, pretendemos tooupdate este artigo regularmente tooreflect essas alterações.

Cada prática recomendada, artigo Olá explica:

* Quais Olá a prática recomendada é.
* Por isso, é uma boa ideia tooenable-lo.
* Como você pode aprender tooenable-lo.
* O que poderia acontecer se você não tooenable-lo.
* Prática recomendada de toohello possíveis alternativas.

artigo Olá examina Olá VM práticas recomendadas de segurança a seguir:

* Autenticação e controle de acesso de VM
* Acesso de rede e a disponibilidade de VM
* Proteger dados em repouso em VMs por meio da imposição de criptografia
* Gerenciar as atualizações de VM
* Gerenciar sua postura de segurança de VM
* Monitorar o desempenho de VM

## <a name="vm-authentication-and-access-control"></a>Autenticação e controle de acesso de VM

Olá primeira etapa na proteção de sua VM é tooensure que somente usuários autorizados são tooset capaz de se novas VMs. Você pode usar [políticas do Azure Resource Manager](../azure-resource-manager/resource-manager-policy.md) tooestablish convenções para recursos em sua organização, criar políticas personalizadas e aplicar tooresources essas políticas, como [grupos de recursos](../azure-resource-manager/resource-group-overview.md).

Máquinas virtuais que pertencem a grupo de recursos tooa naturalmente herdam suas políticas. Embora recomendemos essa abordagem toomanaging VMs, você também pode políticas de controle de acesso tooindividual VM usando [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md).

Quando você habilita o acesso VM de toocontrol RBAC e políticas do Gerenciador de recursos, você ajuda a melhorar a segurança geral de VM. É recomendável que você consolidar VMs com hello ciclo de vida do mesmo em Olá mesmo grupo de recursos. Usando grupos de recursos, você pode implantar, monitorar e acumular custos para os seus recursos de cobrança. tooenable usuários tooaccess e configurar máquinas virtuais, use um [abordagem de privilégios mínimos](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). Quando você atribuir privilégios toousers, plano e Olá toouse funções do Azure internas a seguir:

- [Máquina virtual Colaborador](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): pode gerenciar VMs, mas não Olá toowhich de conta de armazenamento ou de rede virtual estão conectados.
- [Colaborador clássico de máquina Virtual](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): pode gerenciar máquinas virtuais criadas usando o modelo de implantação clássico hello, mas não Olá virtual rede ou armazenamento conta toowhich Olá VMs estão conectadas.
- [Gerente de Segurança](../active-directory/role-based-access-built-in-roles.md#security-manager): pode gerenciar componentes de segurança, políticas de segurança e VMs.
- [Usuário do DevTest Labs](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): pode exibir tudo e se conectar a VMs, iniciá-las, reiniciá-las e desligá-las.

Não compartilhe contas e senhas entre administradores nem reutilize senhas em várias contas de usuário ou serviços, particularmente, as senhas destinadas à mídia social ou outras atividades não administrativas. Idealmente, você deve usar [do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modelos tooset suas máquinas virtuais com segurança. Usando essa abordagem, você pode aumentar as opções de implantação e aplicar configurações de segurança em toda a implantação de saudação.

As organizações que não impõem o controle de acesso a dados, tirando proveito dos recursos, como o RBAC podem estar concedendo aos usuários mais privilégios do que o necessário. Dados do usuário inadequado acesso toocertain diretamente podem comprometer a esses dados.

## <a name="vm-availability-and-network-access"></a>Acesso de rede e a disponibilidade de VM

Se sua VM executa aplicativos essenciais que precisam de toohave alta disponibilidade, é altamente recomendável que você use várias VMs. Para melhorar a disponibilidade, crie pelo menos duas VMs em Olá [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).

[O balanceador de carga do Azure](../load-balancer/load-balancer-overview.md) também requer máquinas virtuais com balanceamento de carga pertencem toohello mesmo conjunto de disponibilidade. Se essas VMs devem ser acessados de saudação à Internet, você deve configurar um [balanceador de carga para a Internet](../load-balancer/load-balancer-internet-overview.md).

Quando as VMs são toohello exposto à Internet, é importante que você [controlar o fluxo de tráfego de rede com grupos de segurança de rede (NSGs)](../virtual-network/virtual-networks-nsg.md). Como os NSGs podem ser aplicadas toosubnets, você pode minimizar o número de saudação do NSGs agrupando os recursos de sub-rede e, em seguida, aplicando os NSGs toohello sub-redes. intenção de saudação é toocreate uma camada de isolamento de rede, que pode ser feito configurando corretamente Olá [segurança de rede](../best-practices-network-security.md) recursos no Azure.

Você também pode usar o recurso de acesso de VMs (JIT) Olá just-in-time de toocontrol Central de segurança do Azure que tenha acesso remoto tooa VM específica e por quanto tempo.

As organizações que não impõem restrições de acesso à rede tooInternet voltado para as máquinas virtuais serão expostas toosecurity riscos, como um ataque de força bruta do protocolo de área de trabalho remota (RDP).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Proteger dados em repouso em VMs por meio da imposição de criptografia

A [criptografia de dados em repouso](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) é uma etapa obrigatória para garantir a privacidade de dados, conformidade e soberania. [Criptografia de disco do Azure](../security/azure-security-disk-encryption.md) permite que os administradores IT tooencrypt Windows e discos de VM de IaaS do Linux. Criptografia de disco combina o recurso de Windows BitLocker de padrão da indústria de saudação e Olá Linux dm crypt recurso tooprovide criptografia de volume para hello SO e discos de dados de saudação.

Você pode aplicar a criptografia de disco toohelp proteger seu dados toomeet seus requisitos de segurança e conformidade organizacionais. Sua organização deve considerar o uso de criptografia toohelp reduzir riscos relacionados toounauthorized acesso a dados. Também recomendamos que você criptografe as unidades antes de gravar toothem dados confidenciais.

Ser tooencrypt-se de que seu tooprotect de volumes de dados VM-las em rest em sua conta de armazenamento do Azure. Proteger as chaves de criptografia de saudação e o segredo usando [Azure Key Vault](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

As organizações que não impõem criptografia de dados são mais problemas de integridade toodata exposto. Por exemplo, os usuários não autorizados ou invasores podem roubar dados nas contas comprometidas ou obter acesso não autorizado toodata codificado em ClearFormat. Além de assumir esses riscos, toocomply com regulamentos do setor, as empresas devem provar que eles são exercer a auditoria e usar segurança correto controla tooenhance sua segurança de dados.

toolearn mais informações sobre criptografia de disco, consulte [Azure criptografia de disco do Windows e VMs de IaaS Linux](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Gerenciar as atualizações de VM

Como VMs do Azure, como todos os locais VMs, são toobe pretendido gerenciadas pelo usuário, o Azure não push toothem de atualizações do Windows. No entanto, você está incentivados tooleave Olá Windows Update configuração automática habilitada. Outra opção é toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) ou outro produto adequadas de gerenciamento de atualizações em outra VM ou no local. O WSUS e o Windows Update mantêm as VMs atualizadas. Também recomendamos que você use uma verificação tooverify do produto que todas as suas VMs de IaaS estão toodate.

Imagens de estoque fornecidas pelo Azure são sempre atualizado tooinclude hello mais recente round de atualizações do Windows. No entanto, não há nenhuma garantia de que as imagens de saudação atuais no momento da implantação. Um pequeno intervalo (de não mais do que algumas semanas) versões públicas a seguir pode ser possível. Verificar e instalar todas as atualizações do Windows devem ser a primeira etapa saudação de cada implantação. Essa medida é especialmente importante tooapply ao implantar imagens que vêm de você ou sua própria biblioteca. Imagens que são fornecidas como parte do hello Azure Marketplace são atualizadas automaticamente por padrão.

As organizações que não impõem políticas de atualização de software são mais exposto toothreats que exploram vulnerabilidades conhecidas e fixas anteriormente. Além de colocar em risco essas ameaças, toocomply com regulamentos do setor, empresas devem provar que eles são exercer a auditoria e usando toohelp de controles de segurança correto garantir a segurança de saudação de sua carga de trabalho localizada na nuvem hello.

É importante tooemphasize que as práticas recomendadas para data centers tradicionais de atualização de software e IaaS do Azure têm muitas semelhanças. Portanto, recomendamos que você avalie seu tooinclude de políticas da atualização do software atual VMs.

## <a name="manage-your-vm-security-posture"></a>Gerenciar sua postura de segurança de VM

Surgimento de ameaças e proteger suas VMs requer um conjunto de recurso de monitoramento de avançado que pode rapidamente detectar ameaças, impedir que os recursos do acesso não autorizado tooyour, disparam alertas e reduzir os falsos positivos. postura de segurança Olá para uma carga de trabalho consiste em todos os aspectos de segurança de saudação VM, de acesso de rede de toosecure de gerenciamento de atualização.

postura de segurança da saudação toomonitor seu [Windows](../security-center/security-center-virtual-machine.md) e [VMs do Linux](../security-center/security-center-linux-virtual-machine.md), use [Central de segurança do Azure](../security-center/security-center-intro.md). Na Central de segurança do Azure, proteger suas VMs, aproveitando o hello recursos a seguir:

* Aplicar configurações de segurança do sistema operacional com as regras de configuração recomendada
* Identificar e fazer o download de segurança do sistema e atualizações críticas que podem estar ausentes
* Implantar as recomendações de proteção do ponto de extremidade antimalware
* Validar a criptografia de disco
* Avaliar e corrigir vulnerabilidades
* Detectar ameaças

A Central de Segurança pode monitorar as ameaças de forma ativa e essas potenciais ameaças são expostas em **Alertas de Segurança**. As ameaças correlacionadas são agregadas em uma única exibição chamada **Incidente de Segurança**.

toounderstand a Central de segurança pode ajudar a identificar possíveis ameaças em suas máquinas virtuais localizadas no Azure, assista a saudação de vídeo a seguir:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

As organizações que não impõem uma postura de segurança forte para suas VMs permanecem sem reconhecimento de tentativas possíveis por controles de segurança toocircumvent estabelecida usuários não autorizados.

## <a name="monitor-vm-performance"></a>Monitorar o desempenho de VM

Abuso de recursos pode ser um problema quando os processos VM consomem mais recursos do que deveriam. Problemas de desempenho com uma máquina virtual podem levar a interrupção tooservice, o que viola o princípio de segurança de saudação de disponibilidade. Por esse motivo, é fundamental toomonitor acesso da máquina virtual não apenas reativo, enquanto estiver ocorrendo um problema, mas também de forma proativa, em relação ao desempenho de linha de base, conforme medido durante a operação normal.

Analisando [arquivos de log de diagnóstico do Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), você pode monitorar os recursos VM e identificar problemas potenciais que podem comprometer o desempenho e disponibilidade. Olá extensão de diagnóstico do Azure fornece recursos de monitoramento e diagnóstico em VMs com base em Windows. Você pode habilitar esses recursos, incluindo a extensão do hello como parte da saudação [modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

Você também pode usar [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain visibilidade da integridade do recurso.

As organizações que não monitoram o desempenho de VM são toodetermine não é possível se certas alterações em padrões de desempenho são normais ou anormais. Se Olá VM está consumindo mais recursos que o normal, essa é uma anomalia pode indicar um ataque potencial de um recurso externo ou um processo comprometido em execução no hello VM.
