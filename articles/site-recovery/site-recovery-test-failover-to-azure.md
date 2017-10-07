---
title: "aaaTest failover tooAzure na recuperação de Site | Microsoft Docs"
description: Saiba mais sobre como executar um failover de teste do local tooAzure
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Testar o Failover tooAzure na recuperação de Site



Este artigo fornece informações e instruções sobre como fazer um failover de teste ou uma simulação de recuperação de desastres de máquinas virtuais e servidores físicos que é protegidas com a recuperação de Site usando o Azure como local de recuperação de saudação.

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Failover de teste executam toovalidate sua estratégia de replicação ou executar uma simulação de recuperação de desastres sem nenhuma perda de dados ou o tempo de inatividade. Realizar um failover de teste não tem nenhum impacto na replicação contínua hello ou em seu ambiente de produção. O failover de teste pode ser feito em uma máquina virtual ou a [plano de recuperação](site-recovery-create-recovery-plans.md). Quando disparar um failover de teste, é preciso máquinas virtuais se conectaria ao teste de toowhich toospecify Olá rede. Depois de um failover de teste é disparado, você pode acompanhar o progresso em Olá **trabalhos** página.  


## <a name="supported-scenarios"></a>Cenários com suporte
Failover de teste é suportado em todos os cenários de implantação que [tooAzure de site VMware herdado](site-recovery-vmware-to-azure-classic-legacy.md). Failover de teste também não tem suporte quando a máquina virtual falhou em tooAzure.  


## <a name="run-a-test-failover"></a>Execute um teste de failover
Este procedimento descreve como toorun um failover de teste para a recuperação de um plano. Como alternativa você também pode executar o failover de teste para um único computador usando a opção apropriada Olá nele.

![Failover de Teste](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Selecione **Planos de Recuperação** > *recoveryplan_name*. Clique em **Failover de Teste**.
1. Selecione um **ponto de recuperação** toofailover para. Você pode usar uma saudação as opções a seguir:
    1.  **Mais recentes processados**: essa opção Falha em todas as máquinas virtuais Olá recuperação plano toohello mais recente do ponto de recuperação que já foi processado pelo serviço de recuperação de Site. Quando você estiver realizando failover de teste de uma máquina virtual, o carimbo de hora do último ponto de recuperação processados Olá também é mostrado. Se você estiver fazendo o failover de um plano de recuperação, você pode ir de máquina virtual de tooindividual e examinar **pontos de recuperação mais recente** bloco tooget essas informações. Como não há tempo é gasto tooprocess Olá dados não processados, essa opção fornece uma opção de failover baixo RTO (objetivo de tempo de recuperação).
    1.  **Mais recente consistente de aplicativo**: essa opção Falha em todas as máquinas virtuais de Olá plano toohello mais recente aplicativo recuperação consistentes com o ponto de recuperação que já foi processado pelo serviço de recuperação de Site. Quando você estiver realizando failover de teste de uma máquina virtual, o carimbo de data / hora do último ponto de recuperação consistentes com o aplicativo hello também é mostrado. Se você estiver fazendo o failover de um plano de recuperação, você pode ir de máquina virtual de tooindividual e examinar **pontos de recuperação mais recente** bloco tooget essas informações.
    1.  **Mais recente**: essa opção primeiro processa todos os dados de saudação que tem sido enviada tooSite recuperação serviço toocreate um ponto de recuperação para cada máquina virtual antes de eles failover tooit. Essa opção fornece Olá menor RPO (objetivo de ponto de recuperação) como máquina de virtual de saudação criado após o failover terá todos os dados de saudação que tenha sido replicada tooSite o serviço de recuperação quando Olá failover foi disparado.
    1.  **Várias VMs processadas mais recentemente**: essa opção só está disponível para os planos de recuperação que têm pelo menos uma máquina virtual com consistência de várias VMs ativada. Ponto de máquinas virtuais que fazem parte de uma grupo failover toohello mais recente comuns várias VMs consistente recuperação da replicação. Outro máquinas virtuais failover tootheir mais recentes processados ponto de recuperação.  
    1.  **Várias VMs mais recentes consistentes com aplicativo**: essa opção só está disponível para os planos de recuperação que têm pelo menos uma máquina virtual com consistência de várias VMs ativada. Máquinas virtuais que fazem parte de uma replicação de grupo failover toohello mais recente várias VMs consistente com o aplicativo de ponto de recuperação comum. Outra máquinas virtuais failover tootheir mais recente consistente com o aplicativo de ponto de recuperação. 
    1.  **Personalizar**: se você estiver fazendo o failover de teste de uma máquina virtual, você pode usar essa opção toofailover tooa determinado ponto de recuperação.
1. Selecione um **rede virtual do Azure**: forneça uma rede virtual do Azure onde máquinas de virtuais de teste Olá seria criadas. Tentativas de recuperação de site toocreate máquinas de virtuais de teste em uma sub-rede de mesmo nome e usando Olá mesmo IP que é fornecida em **de computação e rede** configurações de máquina virtual de saudação. Se a sub-rede de mesmo nome não está disponível no hello rede virtual do Azure fornecido para failover de teste de máquina virtual de teste será criado na sub-rede primeiro Olá em ordem alfabética. Se o mesmo IP não está disponível na sub-rede hello, máquina virtual obtém outro endereço IP disponível na sub-rede hello. Leia esta seção para obter [mais detalhes](#creating-a-network-for-test-failover)
1. Se você estiver realizando o failover tooAzure e criptografia de dados está habilitada, no **chave de criptografia** certificado Olá selecione emitido quando você tiver habilitado a criptografia de dados durante a instalação do provedor. Você pode ignorar esta etapa se você não tiver habilitado a criptografia na máquina virtual de saudação.
1. Controlar o progresso de failover Olá **trabalhos** guia. Você deve estar toosee capaz de máquina de réplica de teste Olá no hello portal do Azure.
1. uma conexão de RDP na máquina virtual de saudação do tooinitiate, você precisará de muito[adicionar um ip público](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) na Olá Olá interface de rede não pôde pela máquina virtual. Se você realizar o failover de máquina de virtual tooa clássico, você precisará de muito[adicionar um ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md) na porta 3389
1. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. Em **notas** registrar e salvar todas as observações associadas Olá failover de teste. Isso exclui as máquinas virtuais Olá que foram criadas durante o failover de teste.


> [!TIP]
> Tentativas de recuperação de site toocreate máquinas de virtuais de teste em uma sub-rede de mesmo nome e usando Olá mesmo IP que é fornecida em **de computação e rede** configurações de máquina virtual de saudação. Se a sub-rede de mesmo nome não está disponível no hello rede virtual do Azure fornecido para failover de teste de máquina virtual de teste será criado na sub-rede primeiro Olá em ordem alfabética. Se fizer parte de Olá escolhido sub-rede IP de destino Olá, recuperação de site tenta máquina toocreate Olá teste failover virtual usando o IP de destino de saudação. Se Olá IP de destino não é parte da saudação escolhida sub-rede máquina de virtual de failover de teste é criada usando qualquer IP disponível em Olá escolhido sub-rede.
>
>

## <a name="test-failover-job"></a>Trabalho de failover de teste

![Failover de Teste](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Quando é disparado, um failover de teste envolve as seguintes etapas:

1. Verificação de pré-requisitos: Essa etapa garante que todas as condições necessárias para o failover sejam atendidas
1. Failover: Essa etapa processa dados hello e torna pronto para que uma máquina virtual do Azure pode ser criada fora dele. Se você tiver escolhido **mais recente** ponto de recuperação, esta etapa cria um ponto de recuperação de dados de saudação que enviou toohello serviço.
1. Início: Essa etapa cria uma máquina virtual do Azure usando dados Olá processados na etapa anterior hello.

## <a name="time-taken-for-failover"></a>Tempo necessário para failover

Em certos casos, o failover de máquinas virtuais requer uma etapa intermediária extra que geralmente leva aproximadamente 8 toocomplete de minutos too10. Esses casos são os seguintes:

* Máquinas virtuais VMware a usando uma versão do hello anteriores 9,8 do serviço de mobilidade
* Servidores físicos
* Máquinas virtuais VMware Linux
* Máquinas virtuais Hyper-V protegidas como servidores físicos
* Máquinas virtuais VMware em que os drivers a seguir não estão presentes como drivers de inicialização
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* Máquinas virtuais VMware que não têm o serviço DHCP habilitado, independentemente de estarem usando endereços DHCP ou IP estáticos

Em Olá todos os outros casos essa etapa intermediária não é necessária e tempo Olá Olá failover é significativamente mais baixo.


## <a name="creating-a-network-for-test-failover"></a>Criar uma rede para failover de teste
É recomendável que, quando você estiver fazendo um failover de teste você escolher uma rede isolada de sua rede de site de recuperação de produção que você forneceu na **de computação e rede** configurações de máquina virtual de saudação. Por padrão quando você cria uma rede virtual do Azure, é isolado de outras redes. Essa rede deve imitar a sua rede de produção:

1. Rede de teste deve ter o mesmo número de sub-redes que em sua rede de produção e com o mesmo nome que as sub-redes de saudação em sua rede de produção de hello.
1. Rede de teste deve usar Olá mesmo intervalo IP da rede de produção.
1. Saudação de atualização DNS de saudação rede de teste como Olá IP que você atribuiu como IP de destino para a máquina de virtual DNS Olá em **de computação e rede** configurações. Leia a seção [considerações sobre failover de teste para o Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obter mais detalhes.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Rede de produção de tooa de failover de teste no site de recuperação
É recomendável que, quando você estiver fazendo um failover de teste você escolher uma rede que é diferente da sua rede de site de recuperação de produção que você forneceu na **de computação e rede** configurações de máquina virtual de saudação. Mas se você realmente deseja conectividade de rede de tooend toovalidate final em uma máquina virtual, observe Olá pontos a seguir:

1. Verifique se a que máquina virtual primária Olá é desligado quando você estiver realizando o failover de teste de saudação. Se você não fizer isso, haverá duas máquinas virtuais com hello mesma identidade em execução no hello rede mesmo em Olá simultaneamente e que pode causar consequências tooundesired.
1. As alterações que você fizer Olá teste de failover em máquinas virtuais em poderiam ser perdidas quando você limpeza Olá teste máquinas virtuais. Essas alterações não serão replicadas toohello back máquina de virtual primária.
1. Essa maneira de realizar testes leva tempo de inatividade tooa de seu aplicativo de produção. Os usuários do aplicativo hello devem ser feitos com o aplicativo de saudação do toonot usar quando Olá DR drill está em andamento.  



## <a name="prepare-active-directory-and-dns"></a>Preparar o Active Directory e o DNS
toorun um failover de teste para testes de aplicativos, você precisa de uma cópia do ambiente do Active Directory de produção de hello em seu ambiente de teste. Leia a seção [considerações sobre failover de teste para o Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obter mais detalhes.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Preparar tooconnect tooAzure VMs após o failover

Se você quiser tooconnect tooAzure máquinas virtuais usando RDP após o failover, certifique-se de Olá ações resumidas na tabela de saudação.

**Failover** | **Localidade** | **Ações**
--- | --- | ---
**VM do Azure executando o Windows** | No computador local antes do failover | tooaccess Olá VM do Azure sobre Olá internet, habilitar o RDP, certifique-se de TCP e UDP regras são adicionadas para Olá **pública**, e que o RDP é permitido em **Firewall do Windows** > **permitidos Aplicativos**, para todos os perfis.<br/><br/> tooaccess sobre uma conexão site a site, habilite o RDP no computador de saudação e certifique-se de que o RDP é permitida em Olá **Firewall do Windows** -> **aplicativos e recursos permitidos** para  **Domínio e particulares** redes.<br/><br/>  Certifique-se de diretiva de SAN do sistema de operacional hello está definida muito**OnlineAll**. [Saiba mais](https://support.microsoft.com/kb/3031135).<br/><br/> Verifique se não existem Windows atualizações pendentes na máquina virtual de hello quando você dispara um failover. O Windows update pode iniciar quando o failover e você não será capaz de toologin toohello VM até a conclusão da atualização de saudação. <br/><br/>
**VM do Azure executando o Windows** | Na VM do Azure após o failover | Para uma máquina virtual clássica, [adicionar um ponto de extremidade público](../virtual-machines/windows/classic/setup-endpoints.md) para Olá protocolo RDP (porta 3389)<br/><br/>  Para uma máquina virtual do Resource Manager, [adicione um IP público](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) a ela.<br/><br/> Olá regras de grupo de segurança de rede em Olá Falha na VM e toowhich de sub-rede do Azure está conectada hello necessário tooallow porta RDP de toohello entrada conexões.<br/><br/> Para uma máquina virtual de Gerenciador de recursos, você pode verificar **diagnósticos de inicialização** toolook em uma captura de tela da máquina virtual de saudação<br/><br/> Se você não pode se conectar, verifique que Olá VM está em execução e, em seguida, examinar esses [dicas de solução de problemas](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**VM do Azure executando Linux** | No computador local antes do failover | Certifique-se de que Olá serviço Secure Shell em hello Azure VM é definida toostart automaticamente na inicialização do sistema.<br/><br/> Verifique se as regras de firewall permitem um tooit de conexão SSH.
**VM do Azure executando Linux** | VM do Azure após o failover | Olá regras de grupo de segurança de rede em Olá Falha na VM e toowhich de sub-rede do Azure está conectada hello necessário a porta do tooallow entrada conexões toohello SSH.<br/><br/> Para uma máquina virtual clássica, [adicionar um ponto de extremidade público](../virtual-machines/windows/classic/setup-endpoints.md) devem ser criados, tooallow conexões de entrada hello porta SSH (porta TCP 22 por padrão).<br/><br/> Para uma máquina virtual do Resource Manager, [adicione um IP público](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) a ela.<br/><br/> Para uma máquina virtual de Gerenciador de recursos, você pode verificar **diagnósticos de inicialização** toolook em uma captura de tela da máquina virtual de saudação<br/><br/>



## <a name="next-steps"></a>Próximas etapas
Depois de tentar executar um failover de teste com êxito, você poderá tentar executar um [failover](site-recovery-failover.md).
