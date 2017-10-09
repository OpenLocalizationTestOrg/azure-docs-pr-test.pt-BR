---
title: "aaaCreate planos de recuperação para failover e recuperação no Azure Site Recovery | Microsoft Docs"
description: "Descreve como toocreate e personalizar planos de recuperação no Azure Site Recovery, toofail sobre e recupere máquinas virtuais e servidores físicos"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Criar planos de recuperação


Este artigo fornece informações sobre como criar e personalizar planos de recuperação em [Azure Site Recovery](site-recovery-overview.md).

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Crie hello de toodo de planos de recuperação a seguir:

* Defina grupos de computadores que fazem failover juntos e então inicialize-os juntos.
* Modele as dependências entre os computadores juntando-os em um grupo de planos de recuperação. Por exemplo, toofail sobre e abrir um aplicativo específico, você agrupa todas as VMs Olá para o aplicativo em Olá mesmo grupo de plano de recuperação.
* Executar um failover. Você pode executar um failover de teste planejado ou não planejado em um plano de recuperação.


## <a name="create-a-recovery-plan"></a>Criar um plano de recuperação

1. Clique em **Planos de Recuperação** > **Criar Plano de Recuperação**.
   Especifique um nome para o plano de recuperação Olá e uma origem e destino. local de origem Olá deve ter as máquinas virtuais que são habilitadas para failover e recuperação.

    - Para replicação de tooVMM do VMM, selecione **tipo de fonte de** > **VMM**e hello de origem e destino servidores do VMM. Clique em **Hyper-V** toosee nuvens que estão protegidas.
    - Para tooAzure do VMM, selecione **tipo de fonte de** > **VMM**.  Servidor do VMM de origem Olá Select, e **Azure** como destino de saudação.
    - Para tooAzure de replicação do Hyper-V (sem VMM), selecione **tipo de fonte de** > **site Hyper-V**. Site selecione hello como fonte de saudação e **Azure** como destino de saudação.
    - Para uma VM do VMware ou físico local tooAzure de servidor, selecione um servidor de configuração como fonte de saudação e **Azure** como destino de saudação.
    - Para um plano de recuperação de tooAzure do Azure, selecione uma região do Azure como origem hello e uma região secundária do Azure como destino de saudação. regiões do Azure secundário de saudação são que somente as máquinas virtuais do toowhich estão protegidas.
2. Em **selecionar máquinas virtuais**, selecione as máquinas virtuais de hello (ou grupo de replicação) que você deseja o grupo padrão de toohello tooadd (grupo 1) no plano de recuperação de saudação.

## <a name="customize-and-extend-recovery-plans"></a>Personalizar e estender os planos de recuperação

Você pode personalizar e estender os planos de recuperação:

- **Adicionar novos grupos**— adicionar grupo de padrão de toohello de grupos (até tooseven) de plano de recuperação adicionais e, em seguida, adicionar mais máquinas ou replicação grupos toothose grupos do plano de recuperação. Grupos são numerados em ordem de saudação na qual você adicioná-los. Uma máquina virtual ou um grupo de replicação pode ser incluído apenas em um grupo de planos de recuperação.
- **Adicionar uma ação manual**: você pode adicionar ações manuais que são executadas antes ou depois de um grupo de planos de recuperação. Quando o plano de recuperação de saudação é executado, ele parar no ponto de saudação em que você inseriu a ação manual Olá. Uma caixa de diálogo solicita que você toospecify que ação manual Olá foi concluída.
- **Adicionar um script** — você pode adicionar scripts executados antes ou depois de um grupo de planos de recuperação. Quando você adiciona um script, ele adiciona um novo conjunto de ações para o grupo de saudação. Por exemplo, um conjunto de pré-etapas do grupo 1 será criado com o nome da saudação: grupo 1: pré-etapas. Todas as pré-etapas serão listadas dentro desse conjunto. Você só pode adicionar um script no site primário hello, se você tiver um servidor VMM implantado.
- **Adicionar runbooks do Azure**— você pode estender os planos de recuperação com runbooks do Azure. Por exemplo, tarefas tooautomate ou recuperação de etapa única toocreate. [Saiba mais](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Adicionar scripts

Você pode usar scripts do PowerShell em seus planos de recuperação.

 - Certifique-se de que os scripts usam blocos try-catch para que Olá exceções sejam tratadas normalmente.
    - Se houver uma exceção no script hello, sua execução for interrompida e tarefa Olá mostra como falha.
    - Se ocorrer um erro, qualquer parte restante do script hello não é executado.
    - Se ocorrer um erro ao executar um failover não planejado, o plano de recuperação Olá continua.
    - Se ocorrer um erro ao executar um failover planejado, o plano de recuperação hello interrompe. Você precisa de script de saudação toofix, verifique se ele é executado como esperado e execute novamente plano de recuperação de saudação.
- Olá comando Write-Host não funciona em um script de plano de recuperação e script hello falhará. toocreate de saída, crie um script de proxy que por sua vez executa o script principal. Certifique-se de que todas as saídas são redirecionadas para fora usando Olá >> comando.
  * script de saudação expira se ele não retorna em 600 segundos.
  * Se nada for gravado em tooSTDERR, o script hello é classificado como falha. Essas informações são exibidas nos detalhes de execução de script hello.

Se você estiver usando a VMM em sua implantação:

* Scripts em um plano de recuperação é executado no contexto Olá Olá conta de serviço do VMM. Verifique se que essa conta tem permissões de leitura para o compartilhamento remoto de saudação em qual Olá script está localizado. Teste Olá script toorun em Olá nível de privilégio da conta de serviço do VMM.
* Os cmdlets do VMM são entregues em um módulo do Windows PowerShell. módulo de saudação é instalado quando você instala o console do VMM hello. Pode ser carregado em seu script, usando Olá comando no script hello a seguir:
   - Import-Module-Name virtualmachinemanager. [Saiba mais](https://technet.microsoft.com/library/hh875013.aspx).
* Verifique se você possui pelo menos um servidor de biblioteca na sua implantação do VMM. Por padrão, o caminho de compartilhamento de biblioteca Olá para um servidor do VMM é localizado localmente no hello servidor VMM, com o nome da pasta Olá MSCVMMLibrary.
    * Se seu caminho de compartilhamento de biblioteca for remoto (ou local, mas não compartilhado com MSCVMMLibrary), configurar o compartilhamento de saudação da seguinte maneira (usando \\libserver2.contoso.com\share\ como um exemplo):
      * Abra Olá Editor do registro e navegue muito**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure Site Recovery\Registration**.
      * Editar valor Olá **ScriptLibraryPath** e colocá-lo como \\libserver2.contoso.com\share\. Especificar Olá FQDN completo. Forneça permissões toohello compartilhamento local.
      * Certifique-se de que você teste o script hello com uma conta de usuário que tem Olá a mesma conta de serviço permissões conforme Olá do VMM. Isso verifica que o autônomo Olá testados scripts executados mesmo maneira que eles serão em planos de recuperação. No servidor do VMM hello, configure Olá toobypass de política de execução da seguinte maneira:
        * Abra o console de Windows PowerShell de 64 bits hello usando privilégios elevados.
        * Digite: **Set-executionpolicy bypass**. [Saiba mais](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Adicionar um script ou um plano de tooa ação manual

Você pode adicionar um grupo de plano de recuperação do script toohello padrão depois que você adicionou VMs ou tooit de grupos de replicação e criar plano de saudação.

1. Plano de recuperação de saudação aberto.
2. Clique em um item no hello **etapa** lista e, em seguida, clique em **Script** ou **ação Manual**.
3. Especifique se o script de saudação do toowant tooadd ou ação antes ou depois de saudação selecionado item. Saudação de uso **mover para cima** e **mover para baixo** botões toomove posição de saudação do script hello para cima ou para baixo.
4. Se você adicionar um script do VMM, selecione **Failover tooVMM script**. Em **caminho de Script**, compartilhamento de toohello do tipo hello caminho relativo. Exemplo hello VMM abaixo, você especifica o caminho de saudação: **\rpscripts\rpscript.ps1.**.
5. Se você adicionar uma livro de executar a automação do Azure, especifique a conta de automação do Azure de saudação no qual Olá runbook é o script de runbook do Azure apropriada de Olá localizado e selecione.
6. Execute um failover de saudação do plano de recuperação, toomake se Olá script funcione conforme esperado.


### <a name="add-a-vmm-script"></a>Criar um script do VMM

Se você tiver um site de origem do VMM, você pode criar um script no servidor do VMM hello e incluí-lo em seu plano de recuperação.

1. Crie uma nova pasta no compartilhamento de biblioteca hello. Por exemplo, \<VMMServerName > \MSSCVMMLibrary\RPScripts. Coloque-o na fonte de saudação e servidores do VMM de destino.
2. Crie o script hello (por exemplo, RPScript) e verifique funciona conforme o esperado.
3. Coloque o script hello no local de saudação \<VMMServerName > \MSSCVMMLibrary, nos servidores VMM de origem e destino hello.


## <a name="next-steps"></a>Próximas etapas

[Saiba mais](site-recovery-failover.md) sobre a execução de failovers.
