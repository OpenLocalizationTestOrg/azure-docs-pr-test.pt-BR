---
title: "aaaJust na máquina virtual do tempo de acesso na Central de segurança do Azure | Microsoft Docs"
description: "Este documento orienta como apenas em tempo de acesso da máquina virtual na Ajuda da Central de segurança do Azure você controlar o acesso tooyour Azure máquinas virtuais."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Gerenciar o acesso à máquina virtual usando o just in time

Just-in-time VM (máquina virtual) o acesso pode ser usado toolock para baixo tráfego de entrada tooyour VMs do Azure, reduzindo a exposição tooattacks enquanto fornecem acesso fácil tooconnect tooVMs quando necessário.

> [!NOTE]
> Olá apenas no recurso de tempo está no modo de visualização e disponível no hello camada padrão da Central de segurança.  Consulte [preços](security-center-pricing.md) camadas de preços do toolearn mais sobre o Centro de segurança.
>
>

## <a name="attack-scenario"></a>Cenário de ataque

Força bruta ataques geralmente as portas de gerenciamento de destino como um tooa de acesso significa toogain VM. Se for bem-sucedido, um invasor pode assumir controle Olá VM e estabelecer destaque em seu ambiente.

Ataque de força bruta tooreduce unidirecional exposição tooa é toolimit Olá período de tempo que uma porta está aberta. As portas de gerenciamento fazer não abrir de toobe necessário em todos os momentos. Eles só precisarem de toobe aberto enquanto você conectado toohello VM, por exemplo tooperform de são tarefas de manutenção ou gerenciamento. Quando está habilitada no momento, a Central de segurança usa [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regras (NSG), que restringem o acesso toomanagement portas para que eles não podem ser alvo de invasores.

![Cenário just in time][1]

## <a name="how-does-just-in-time-access-work"></a>Como funciona o acesso just in time?

Quando está habilitada no momento, a Central de segurança bloqueia o tráfego de entrada tooyour VMs do Azure, criando uma regra NSG. Selecione as portas de saudação em Olá VM toowhich o tráfego de entrada será bloqueado para baixo. Essas portas são controladas por Olá apenas na solução de tempo.

Quando um usuário solicita acesso tooa VM, Central de segurança verifica se o usuário Olá tem [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) permissões que fornecem acesso de gravação para Olá recursos do Azure. Se eles têm permissões de gravação, Olá solicitação for aprovada e Central de segurança configura automaticamente os grupos de segurança de rede (NSGs) hello tooallow portas de gerenciamento de toohello de tráfego de entrada quantidade de saudação de tempo especificado. Depois que o tempo de saudação expirou, Central de segurança restaura estados anteriores da saudação NSGs tootheir.

> [!NOTE]
> O acesso just in time à VM da Central de Segurança atualmente dá suporte somente a VMs implantadas por meio do Azure Resource Manager. toolearn mais sobre hello clássico e modelos de implantação do Gerenciador de recursos, consulte [do Azure Resource Manager versus implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Usando o acesso just in time

Olá **apenas no acesso de tempo de VM** bloco Olá **Central de segurança** folha mostra o número de saudação de máquinas virtuais configuradas para apenas no tempo acesso e Olá o número de solicitações de acesso aprovado feitas no hello última semana.

Selecione Olá **apenas no acesso de tempo de VM** lado a lado e hello **apenas no acesso de tempo de VM** folha é aberta.

![Bloco acesso à VM just in time][2]

Olá **apenas no acesso de tempo de VM** folha fornece informações sobre o estado de saudação das suas máquinas virtuais:

- **Configurado** -VMs que foram toosupport configurado apenas no acesso de tempo de VM. dados Olá apresentados para Olá na semana passada e incluem para cada número de saudação do VM de solicitações aprovadas, a data do último acesso e a hora e do último usuário.
- **Recomendada** – VMs que podem dar suporte ao acesso à VM just in time, mas não foram configurados para isso. É recomendável que você habilite o controle de acesso à VM just in time para essas VMs. Consulte [Habilitar acesso à VM just in time](#enable-just-in-time-vm-access).
- **Nenhuma recomendação** -razões que podem causar uma VM não toobe recomendado são:
  - Ausente NSG - Olá apenas no tempo solução requer um toobe NSG em vigor.
  - VM Clássica – o acesso à VM just in time da Central de Segurança atualmente dá suporte apenas às VMs implantadas por meio do Azure Resource Manager. Uma implantação clássica não é suportada pelo Olá apenas na solução de tempo.
  - Outros - uma VM é nesta categoria se Olá no momento a solução está desativada na política de segurança de saudação da assinatura de saudação ou grupo de recursos hello, ou que hello VM está faltando um IP público e não tiver um NSG em vigor.

## <a name="configuring-a-just-in-time-access-policy"></a>Configurando uma política de acesso just in time

Olá tooselect VMs que você deseja tooenable:

1. Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **recomendado** guia.

  ![Habilitar o acesso just in time][3]

2. Em **VMs**, selecione Olá VMs que você deseja tooenable. Isso coloca uma tooa de marca de seleção próxima VM.
3. Selecione **Habilitar JIT nas VMs**.
4. Selecione **Salvar**.

### <a name="default-ports"></a>Portas padrão

Você pode ver as portas padrão Olá Central de segurança recomenda habilitar no momento.

1. Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **recomendado** guia.

  ![Exibir portas padrão][6]

2. Em **VMs**, selecione uma VM. Isso coloca uma saudação do marca de seleção próxima toohello VM e abre **configuração de acesso de JIT VM** folha. Esta folha exibe as portas padrão de saudação.

### <a name="add-ports"></a>Adicionar portas

De saudação **configuração de acesso de JIT VM** folha, você pode também adicionar e configurar uma nova porta na qual você deseja tooenable Olá apenas na solução de tempo.

1. Em Olá **configuração de acesso de JIT VM** folha, selecione **adicionar**. Isso abre o hello **Adicionar configuração de porta** folha.

  ![Configuração de portas][7]

2. Em **Adicionar configuração de porta** folha, identificar porta hello, tipo de protocolo, tempo de solicitação de IPs de origem e o máximo permitida.

  Permitido IPs de origem são Olá IP intervalos tooget permitido acesso após uma solicitação aprovado.

  Tempo máximo de solicitação é a janela de tempo máximo de saudação que uma porta específica pode ser aberta.

3. Selecione **OK**.

## <a name="requesting-access-tooa-vm"></a>Solicitando acesso tooa VM

acesso de toorequest tooa VM:

1. Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **configurado** guia.
2. Em **VMs**, selecione Olá VMs que você deseja acesso tooenable. Isso coloca uma tooa de marca de seleção próxima VM.
3. Selecione **Solicitar acesso**. Isso abre o hello **solicitar acesso** folha.

  ![Solicitar acesso tooa VM][4]

4. Em Olá **solicitar acesso** folha, que você configurar para cada tooopen de portas VM Olá junto com o IP de origem de Olá Olá porta está aberta tooand janela de tempo de saudação para o qual Olá porta está aberta. Você pode solicitar portas de toohello apenas de acesso que são configuradas no hello apenas na diretiva de tempo. Cada porta tem um tempo máximo permitido derivado Olá apenas na diretiva de tempo.
5. Selecione **Abrir portas**.

## <a name="editing-a-just-in-time-access-policy"></a>Edição de uma política de acesso just in time

Você pode alterar uma VM existente apenas na diretiva de tempo adicionando e configurando um novo tooopen de porta para a VM ou alterando a qualquer outro parâmetro tooan relacionada já protegido porta.

Em ordem tooedit um existente apenas na diretiva de tempo de uma VM, hello **configurado** guia é usada:

1. Em **VMs**, selecione uma VM tooadd um tooby porta clicando em pontos de saudação três na linha de saudação para a VM. Isso abre um menu.
2. Selecione **editar** no menu de saudação. Isso abre o hello **configuração de acesso de JIT VM** folha.

  ![Editar política][8]

3. Em Olá **configuração de acesso de JIT VM** folha, você pode editar as configurações existentes de uma porta já protegida Olá clicando em sua porta, ou você pode selecionar **adicionar**. Isso abre o hello **Adicionar configuração de porta** folha.

  ![Adicionar uma porta][7]

4. Em **Adicionar configuração de porta** folha identificar porta hello, tipo de protocolo, IPs de origem permitido e tempo máximo de solicitações.
5. Selecione **OK**.
6. Selecione **Salvar**.

## <a name="auditing-just-in-time-access-activity"></a>Auditoria em atividades de acesso just in time

Você pode obter informações sobre as atividades de VM usando a pesquisa de logs. logs de tooview:

1. Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **configurado** guia.
2. Em **VMs**, selecione um tooview de VM informações sobre clicando em pontos de saudação três na linha de saudação para a VM. Isso abre um menu.
3. Selecione **Log de atividades** no menu de saudação. Isso abre o hello **log de atividades** folha.

![Selecionar o log de atividades][9]

Olá **log de atividades** folha fornece uma exibição filtrada de operações anteriores para a VM junto com a assinatura, data e hora.

![Exibir log de atividades][5]

Você pode baixar informações do log Olá selecionando **clique aqui toodownload todos os itens de saudação como CSV**.

Modificar filtros hello e selecione **aplicar** toocreate uma pesquisa e log.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Usando o acesso à VM just in time por meio do PowerShell

Na saudação de toouse ordem apenas na solução de tempo por meio do PowerShell, certifique-se de ter Olá [mais recente](/powershell/azure/install-azurerm-ps) versão do PowerShell do Azure.
Depois que você fizer isso, você precisa Olá tooinstall [mais recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Central de segurança do Azure da Galeria do PowerShell hello.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Configurando uma política just in time para uma VM

tooconfigure apenas na diretiva de tempo em uma VM específica, você precisa de toorun esse comando em sua sessão do PowerShell: Set-ASCJITAccessPolicy.
Siga Olá cmdlet documentação toolearn mais.

### <a name="requesting-access-tooa-vm"></a>Solicitando acesso tooa VM

tooaccess uma VM específica que é protegida com Olá apenas na solução de tempo, você precisa toorun esse comando em sua sessão do PowerShell: ASCJITAccess invocar.
Siga Olá cmdlet documentação toolearn mais.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como apenas em tempo de acesso da máquina virtual na Central de segurança ajuda controlar o acesso tooyour Azure máquinas virtuais.

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

- [Definir políticas de segurança](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
- [Gerenciar recomendações de segurança](security-center-recommendations.md) – saiba como as recomendações ajudam a proteger seus recursos do Azure.
- [Monitoramento de integridade de segurança](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
- [Gerenciando e responder a alertas toosecurity](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.
- [Monitoramento de soluções de parceiros](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
- [Perguntas frequentes sobre o Centro de segurança](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
- [Blog de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
