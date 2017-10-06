---
title: compartilhamento de arquivos do aaaAutomate StorSimple DR com o Azure Site Recovery | Microsoft Docs
description: "Descreve as etapas de saudação e práticas recomendadas para criar uma solução de recuperação de desastres para compartilhamentos de arquivos hospedados no armazenamento do Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Solução de recuperação de desastre automatizada usando o Azure Site Recovery para compartilhamentos de arquivos hospedados no StorSimple
## <a name="overview"></a>Visão geral
Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida endereços Olá complexidades de comumente associadas a compartilhamentos de arquivos de dados não estruturados. StorSimple usa armazenamento em nuvem como uma extensão da saudação solução local e automaticamente de camadas de dados em armazenamento local e o armazenamento em nuvem. Integra a proteção de dados local e instantâneos em nuvem, que elimina a necessidade de saudação de uma infraestrutura de armazenamento amplas.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) é um serviço baseado no Azure que fornece recursos de DR (recuperação de desastre) por meio da orquestração de replicação, de failover e da recuperação de máquinas virtuais. Recuperação de Site do Azure dá suporte a um número de replicação de tooconsistently de tecnologias de replicação, proteger e realizará failover nuvens de máquinas virtuais e aplicativos de tooprivate/público ou hospedados.

Usando o Azure Site Recovery, replicação de máquina virtual e recursos de instantâneo de nuvem do StorSimple, você pode proteger o ambiente de servidor completo do arquivo hello. No evento de saudação de interrupção, você pode usar um toobring de único clique seus compartilhamentos de arquivos online no Azure em apenas alguns minutos.

Este documento explica detalhadamente como você pode criar uma solução de recuperação de desastre para seus compartilhamentos de arquivos hospedados no armazenamento do StorSimple e executar failovers planejados, não planejados e de teste usando um plano de recuperação de um clique. Em essência, ele mostra como você pode modificar Olá plano de recuperação no seu tooenable do cofre Azure Site Recovery StorSimple failovers nos cenários de desastre. Além disso, ele descreve as configurações e pré-requisitos com suporte. Este documento assume que você esteja familiarizado com conceitos básicos de saudação do Azure Site Recovery e StorSimple arquiteturas.

## <a name="supported-azure-site-recovery-deployment-options"></a>Opções de implantação com suporte do Azure Site Recovery
Os clientes podem implantar servidores de arquivos como servidores físicos ou VMs (máquinas virtuais) em execução no Hyper-V ou no VMware e, então, criar compartilhamentos de arquivos de volumes configurados fora do armazenamento do StorSimple. O Azure Site Recovery pode proteger tooeither ambas as implantações físicas e virtuais de um site secundário ou tooAzure. Este documento abrange detalhes de uma solução de recuperação de desastres com o Azure como local de recuperação de saudação para um servidor de arquivos que VM hospedada no Hyper-V e compartilhamentos de arquivos no armazenamento do StorSimple. Outros cenários em qual servidor de arquivo hello VM está em uma VM do VMware ou em um computador físico podem ser implementados de maneira semelhante.

## <a name="prerequisites"></a>Pré-requisitos
Implementar uma solução de recuperação de desastres de um clique que usa o Azure Site Recovery para compartilhamentos de arquivos hospedados no armazenamento do StorSimple possui Olá pré-requisitos a seguir:

* VM de servidor de arquivo do Windows Server 2012 R2 local hospedada no Hyper-V, no VMware ou em um computador físico
* Dispositivo de armazenamento do StorSimple local registrado com o Azure StorSimple Manager
* StorSimple Appliance de nuvem criado no Gerenciador do StorSimple do Azure hello (podem ser mantido em estado de desligamento)
* Compartilhamentos de arquivos, hospedados em volumes de saudação configurados no dispositivo de armazenamento do StorSimple Olá
* [Cofre de serviços do Azure Site Recovery](../site-recovery/site-recovery-vmm-to-vmm.md) criado em uma assinatura do Microsoft Azure

Além disso, se o Azure é o local de recuperação, executar Olá [ferramenta de avaliação de preparação de máquina Virtual do Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) em VMs tooensure que eles sejam compatíveis com VMs do Azure e o Azure Site Recovery services.

problemas de latência de tooavoid (que podem resultar em custos mais altos), certifique-se de que você criar seu dispositivo StorSimple de nuvem, conta de automação e Olá de conta (s) de armazenamento na mesma região.

## <a name="enable-dr-for-storsimple-file-shares"></a>Habilitar a DR para os compartilhamentos de arquivos do StorSimple
Cada componente do hello local ambiente precisar toobe protegido tooenable concluir a replicação e a recuperação. Esta seção descreve como:

* Configurar o Active Directory e a replicação do DNS (opcional)
* Usar a proteção do Azure Site Recovery tooenable saudação do servidor de arquivos VM
* Habilitar a proteção de volumes do StorSimple
* Configurar rede Olá

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Configurar o Active Directory e a replicação do DNS (opcional)
Se você quiser tooprotect Olá máquinas em execução do Active Directory e DNS para que fiquem disponíveis no site de saudação DR, você precisa tooexplicitly protegê-los (de forma que os servidores de arquivos de saudação são acessíveis após o failover com a autenticação). Há duas opções recomendadas com base em complexidade Olá Olá do local do ambiente de cliente.

#### <a name="option-1"></a>Opção 1
Se cliente Olá tem um pequeno número de aplicativos, um único controlador de domínio para Olá todo site local e estar falhando em todo o site hello, em seguida, é recomendável usar o computador de controlador de domínio do Azure Site Recovery replicação tooreplicate Olá site secundário do tooa (Isso é aplicável para o site a site e o site para o Azure).

#### <a name="option-2"></a>Opção 2
Se Olá cliente tem um grande número de aplicativos, está em execução para uma floresta do Active Directory e será estar falhando por alguns aplicativos cada vez, é recomendável configurar um controlador de domínio no site Olá DR (ou um site secundário ou no Azure).

Consulte também[solução de recuperação de desastres automatizada para o Active Directory e DNS usando o Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) para obter instruções ao disponibilizar um controlador de domínio no site Olá DR. Para restante Olá deste documento, vamos pressupor que um controlador de domínio está disponível no local de recuperação de desastres hello.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Usar a proteção do Azure Site Recovery tooenable saudação do servidor de arquivos VM
Esta etapa requer que você preparar o ambiente de servidor de arquivo hello local, cria e preparar um cofre do Azure Site Recovery e habilite a proteção de arquivo de saudação VM.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>Olá tooprepare ambiente de servidor de arquivos local
1. Saudação de conjunto **User Account Control** muito**nunca notificar**. Isso é necessário para que você pode usar os destinos iSCSI do automação do Azure scripts tooconnect Olá após falha com o Azure Site Recovery.

   1. Pressione a tecla do Windows hello + Q e procure **UAC**.
   2. Selecione **Alterar configurações de Controle de Conta de Usuário**.
   3. Olá arraste barra inferior toohello para **nunca notificar**.
   4. Clique em **OK** e, então, selecione **Sim** quando solicitado.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Instale Olá VM Agent em cada servidor de arquivo hello VMs. Isso é necessário para que você pode executar scripts de automação do Azure em Olá failover de máquinas virtuais.

   1. [Baixar o agente Olá](http://aka.ms/vmagentwin) muito`C:\\Users\\<username>\\Downloads`.
   2. Abrir o Windows PowerShell no modo de administrador (Executar como administrador) e, em seguida, digite Olá local de download do comando toonavigate toohello a seguir:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > nome do arquivo Hello pode mudar dependendo versão hello.
      >
      >
3. Clique em **Avançar**.
4. Aceitar Olá **termos do contrato de** e, em seguida, clique em **próximo**.
5. Clique em **Concluir**.
6. Crie os compartilhamentos de arquivos usando volumes criados fora do armazenamento do StorSimple. Para obter mais informações, consulte [usar Olá StorSimple Manager serviço toomanage volumes](storsimple-manage-volumes.md).

   1. Em suas VMs locais, pressione a tecla do Windows hello + Q e procure **iSCSI**.
   2. Selecione o **iniciador iSCSI**.
   3. Selecione Olá **configuração** guia e copiar o nome do iniciador hello.
   4. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
   5. Selecione Olá **StorSimple** guia e, em seguida, selecione Olá serviço StorSimple Manager que contém o dispositivo físico hello.
   6. Crie contêineres de volume e, em seguida, crie volumes. (Esses volumes são Olá compartilhamentos de arquivo no servidor de arquivos Olá VMs). Copie o nome do iniciador hello e dê um nome apropriado para Olá registros de controle de acesso ao criar volumes de saudação.
   7. Selecione Olá **configurar** guia e anote o endereço IP de saudação do dispositivo de saudação.
   8. Em suas VMs locais, acesse toohello **iniciador iSCSI** novamente e insira IP Olá Olá seção conexão rápida. Clique em **conexão rápida** (dispositivo Olá agora deve estar conectado).
   9. Olá Abrir portal do Azure e selecione Olá **Volumes e dispositivos** guia. Clique em **Configuração Automática**. volume de saudação que você criou deve aparecer.
   10. No portal de saudação, selecione Olá **dispositivos** guia e, em seguida, selecione **criar um novo dispositivo Virtual.** (Este dispositivo virtual será usado se ocorrer um failover). Este novo dispositivo virtual possa ser mantido em um estado offline tooavoid custos extras. tootake Olá toohello de dispositivo virtual offline, vá **máquinas virtuais** seção Olá Portal e desligá-lo.
   11. Voltar toohello VMs locais e abra o gerenciamento de disco (pressione a tecla do Windows hello + X e selecione **gerenciamento de disco**).
   12. Você observará algumas discos extras (dependendo do número de saudação de volumes que você criou). Com o botão direito Olá primeiro, selecione **inicializar disco**e selecione **Okey**. Saudação de atalho **não alocado** seção, selecione **Novo Volume simples**, atribuir uma letra de unidade e concluir o Assistente de saudação.
   13. Repita a etapa l para todos os discos de saudação. Agora você pode ver todos os discos de saudação em **este PC** em Olá Windows Explorer.
   14. Use Olá serviços de arquivo e armazenamento função toocreate compartilhamentos de arquivos nesses volumes.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate e preparar um cofre do Azure Site Recovery
Consulte toohello [documentação do Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget iniciado com o Azure Site Recovery antes de proteger a VM do servidor de arquivo hello.

#### <a name="tooenable-protection"></a>proteção de tooenable
1. Desconectar Olá iSCSI delimitar da saudação VMs que você deseja tooprotect por meio do Azure Site Recovery local:

   1. Pressione a tecla Windows + Q e pesquise por **iSCSI**.
   2. Selecione **Configurar o iniciador iSCSI**.
   3. Desconecte o dispositivo StorSimple Olá que você está conectado anteriormente. Como alternativa, você pode desativar o servidor de arquivos Olá por alguns minutos ao habilitar a proteção.

   > [!NOTE]
   > Isso fará com que toobe de compartilhamentos de arquivo de saudação temporariamente indisponível.
   >
   >
2. [Habilitar proteção da máquina virtual](../site-recovery/site-recovery-hyper-v-site-to-azure.md) saudação do servidor de arquivos VM do portal do Azure Site Recovery hello.
3. Quando a sincronização inicial Olá começa, você pode se reconectar destino Olá novamente. Vá toohello iniciador de iSCSI, selecione o dispositivo StorSimple hello e clique em **conectar**.
4. Quando sincronização Olá for concluída e status de saudação do hello VM é **protegidos**, selecione Olá VM, selecione Olá **configurar** guia e atualize a rede de saudação do hello VM adequadamente (Esta é a rede de saudação Esse Olá failover VMs farão parte do). Se a rede Olá não aparecer, significa sincronização Olá ainda está acontecendo.

### <a name="enable-protection-of-storsimple-volumes"></a>Habilitar a proteção de volumes do StorSimple
Se você não selecionou Olá **habilitar um backup padrão para este volume** opção para volumes do StorSimple hello, vá muito**políticas de Backup** Olá serviço StorSimple Manager e criar um backup adequado política para todos os volumes de saudação. É recomendável que você defina a frequência de saudação de backups toohello ponto de recuperação objetivo (RPO) que deseja toosee para o aplicativo hello.

### <a name="configure-hello-network"></a>Configurar rede Olá
Para o servidor de arquivo hello VM, definir configurações de rede no Azure Site Recovery para que as redes VM Olá são anexados toohello correto DR rede após o failover.

Você pode selecionar Olá VM Olá **replicadas itens** guia Configurações de rede Olá tooconfigure, conforme mostrado na ilustração a seguir de saudação.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
Você pode criar um plano de recuperação no processo de failover do ASR tooautomate Olá Olá de compartilhamentos de arquivos. Se ocorrer uma interrupção, você poderá exibir compartilhamentos de arquivo hello em poucos minutos, com apenas um único clique. tooenable essa automação, você precisará de uma conta de automação do Azure.

#### <a name="toocreate-an-automation-account"></a>toocreate uma conta de automação
1. Vá toohello portal do Azure &gt; **automação** seção.
2. Clique no botão **+ Adicionar** e a folha abaixo é aberta.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Nome – insira uma nova conta de automação
   * Assinatura – escolha uma assinatura
   * Grupo de recursos – crie um novo grupo de recursos ou escolha um grupo de recursos existente
   * Local - Escolher local, lembre-Olá mesmo/região geográfica na qual Olá StorSimple Appliance de nuvem e contas de armazenamento foram criadas.
   * Criar conta Executar Como do Azure – selecione a opção **Sim**.

3. Vá toohello conta de automação, clique em **Runbooks** &gt; **procurar galeria** tooimport todos Olá necessário runbooks na conta de automação de saudação.
4. Adicionar Olá runbooks a seguir, localizando **a recuperação de desastres** marca na Galeria de saudação:

   * Limpe os volumes do StorSimple após o TFO (failover de teste)
   * Faça failover de contêineres de volume do StorSimple
   * Monte volumes no dispositivo StorSimple após o failover
   * Desinstale a extensão de script personalizada na VM do Azure
   * Inicie a solução de virtualização StorSimple

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Publicar todos os scripts de saudação selecionando Olá runbook na conta de automação hello e clique em **editar** &gt; **publicar** e **Sim** toohello verificação Mensagem. Após essa etapa, Olá **Runbooks** guia será exibida da seguinte maneira:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Na conta de automação hello, selecione Olá **ativos** guia &gt; clique **variáveis** &gt; **adicionar uma variável** e adicione Olá variáveis a seguir. Você pode escolher tooencrypt esses ativos. Essas variáveis são específicas do plano de recuperação. Se a recuperação do plano (que você irá criar na próxima etapa do hello) nome for TestPlan, as variáveis devem ser StorSimRegKey do plano de teste, AzureSubscriptionName do plano de teste e assim por diante.

   * *RecoveryPlanName***- StorSimRegKey**: chave de registro de saudação para Olá serviço StorSimple Manager.
   * *RecoveryPlanName***- AzureSubscriptionName**: nome de saudação do hello assinatura do Azure.
   * *RecoveryPlanName***- ResourceName**: nome de saudação do hello recurso StorSimple com o dispositivo StorSimple hello.
   * *RecoveryPlanName***- DeviceName**: dispositivo Olá toobe failover.
   * *RecoveryPlanName***- VolumeContainers**: uma cadeia de caracteres separada por vírgulas de contêineres de volume presente no dispositivo de saudação que precisam toobe falha; por exemplo, volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: Olá StorSimple Appliance de nuvem na qual Olá contêineres são toobe falhou.
   * *RecoveryPlanName***- TargetDeviceDnsName**: nome do serviço de saudação do dispositivo de destino da saudação (pode ser encontrado na Olá **Máquina Virtual** seção: nome do serviço Olá é Olá mesmo como Olá Nome DNS).
   * *RecoveryPlanName***- StorageAccountName**: nome de conta de armazenamento Olá no qual script hello (que toorun em Olá falhou VM) serão armazenados. Isso pode ser qualquer conta de armazenamento que tem o script hello espaço toostore temporariamente.
   * *RecoveryPlanName***- StorageAccountKey**: chave de acesso de saudação de saudação acima de conta de armazenamento.
   * *RecoveryPlanName***- ScriptContainer**: nome de saudação do contêiner de saudação na qual Olá script será armazenado na nuvem hello. Se o contêiner de saudação não existir, ele será criado.
   * *RecoveryPlanName***- VMGUIDS**: após a proteção de uma VM, Azure Site Recovery atribui cada VM uma identificação exclusiva que fornece detalhes de saudação do hello Falha na VM. Olá tooobtain VMGUID, selecione Olá **dos serviços de recuperação** guia e clique em **Item protegido** &gt; **grupos de proteção** &gt; **Máquinas** &gt; **propriedades**. Se você tiver várias VMs, adicione Olá GUIDs como uma cadeia de caracteres separada por vírgulas.
   * *RecoveryPlanName***- AutomationAccountName** – hello nome da conta de automação Olá no qual você adicionou Olá runbooks e ativos de saudação.

  Por exemplo, se hello nome saudação do plano de recuperação é fileServerpredayRP, o **credenciais** & **variáveis** guias devem aparecer da seguinte maneira depois de adicionar todos os ativos de saudação.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Vá toohello **dos serviços de recuperação** seção e o cofre do Azure Site Recovery Olá selecione que você criou anteriormente.
8. Selecione Olá **planos de recuperação (recuperação de Site)** opção **gerenciar** grupo e crie um novo plano de recuperação da seguinte maneira:

   a.  Clique no botão **+ Plano de recuperação**, abra a folha abaixo.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Insira um nome de plano de recuperação, escolha valores de modelo de Implantação, Destino e Origem.

   c.  Selecione VMs Olá Olá do grupo de proteção que você deseja tooinclude no plano de recuperação de saudação e clique em **Okey** botão.

   d.  Selecione o plano de recuperação que você criou anteriormente, clique em **personalizar** botão exibição de personalização de plano de recuperação do tooopen hello.

   e.  Clique com o botão direito em **Desligamento de todos os grupos** e clique em **Adicionar ação prévia**.

   f.  Abre folha de ação de inserção, insira um nome, selecione **lado primário** opção onde toorun opção, selecione a conta de automação (no qual você adicionou Olá runbooks) e selecione Olá  **Failover-StorSimple-contêineres de Volume** runbook.

   g.  Clique com o botão direito em **grupo 1: Iniciar** e clique em **itens protegidos de adicionar** opção e selecione VMs Olá toobe protegida no plano de recuperação de saudação e clique em **Okey** botão. Opcional, caso as VMs já estejam selecionadas.

   h.  Clique com o botão direito em **grupo 1: Iniciar** e clique em **lançar ação** opção e adicione Olá a todos os scripts a seguir:

   * Runbook Start-StorSimple-Virtual-Appliance
   * Runbook Fail over-StorSimple-volume-containers
   * Runbook mount-volumes-after-failover
   * Runbook uninstall-custom-script-extension

   i.  Adicionar uma ação manual depois Olá superior a 4 scripts no hello mesmo **grupo 1: pós-etapas** seção. Esta ação é ponto Olá no qual você pode verificar se tudo está funcionando corretamente. Essa ação precisa toobe adicionado somente como parte do failover de teste (portanto, apenas selecione Olá **Failover de teste** caixa de seleção).

   j.  Após a ação manual do hello, adicionar Olá **limpeza** script usando Olá mesmo procedimento usado para Olá outros runbooks. **Salvar** plano de recuperação de saudação.

    > [!NOTE]
    > Ao executar um failover de teste, você deve verificar tudo na etapa de ação manual Olá porque os volumes do StorSimple Olá que tinham sido clonados no dispositivo de destino hello serão excluídos como parte da limpeza Olá após a conclusão da ação manual hello.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Executar um failover de teste
Consulte toohello [solução de recuperação de desastres do Active Directory](../site-recovery/site-recovery-active-directory.md) guia complementar para considerações específicas tooActive diretório durante o failover de teste de saudação. configuração do local de saudação não será afetada em todos os quando ocorre um failover de teste de saudação. Olá volumes do StorSimple que estavam anexados toohello a VM são clonado toohello StorSimple Appliance de nuvem no Azure no local. Uma VM para fins de teste é colocada no Azure e volumes clonados hello são anexado toohello VM.

#### <a name="tooperform-hello-test-failover"></a>failover de teste tooperform Olá
1. No portal do Azure de Olá, selecione seu Cofre de recuperação de site.
2. Clique em plano de recuperação de saudação criado para a VM do servidor de arquivo hello.
3. Clique em **Failover de Teste**.
4. Selecione toowhich de rede virtual do Azure Olá que VMs do Azure serão conectadas após o failover.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Clique em **Okey** toobegin Olá failover. Você pode acompanhar o progresso clicando no hello VM tooopen suas propriedades, ou em Olá **trabalho de failover de teste** no nome do cofre &gt; **trabalhos** &gt; **ostrabalhosderecuperaçãodeSite**.
6. Após a conclusão do failover hello, você também deve ser capaz de réplica de saudação toosee máquina do Azure aparecem no hello portal do Azure &gt; **máquinas virtuais**. Você pode executar suas validações.
7. Depois que as validações de saudação, clique em **validações completa**. Essa saudação de limpeza será Volumes do StorSimple e desligamento Olá StorSimple Appliance de nuvem.
8. Quando terminar, clique em **failover de teste de limpeza** no plano de recuperação de saudação. No registro de notas e salve todas as observações associadas Olá failover de teste. Isso excluirá a máquina virtual Olá que foram criados durante o failover de teste.

## <a name="perform-a-planned-failover"></a>Faça um failover planejado
   Durante um failover planejado, Olá local servidores de arquivos que VM desligar normalmente e uma nuvem de instantâneo de backup de volumes de saudação no dispositivo StorSimple é obtido. volumes do StorSimple Olá falharem em dispositivo virtual toohello, uma réplica de máquina virtual é colocado no Azure, e os volumes de saudação são anexado toohello VM.

#### <a name="tooperform-a-planned-failover"></a>tooperform um failover planejado
1. No portal do Azure de Olá, selecione **dos serviços de recuperação** cofre &gt; **planos de recuperação (recuperação de Site)** &gt; **recoveryplan_name** criado para servidor de arquivos Olá VM.
2. Na folha de plano de recuperação de saudação, clique em **mais** &gt; **failover planejado**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Em Olá **confirmar Failover planejado** folha, escolha Olá locais de destino e de rede de destino selecione e clique em processo de failover de Olá Olá seleção ícone ✓ toostart.
4. Depois que as máquinas virtuais de réplica são criadas, elas ficam em um estado de confirmação pendente. Clique em **confirmar** toocommit Olá failover.
5. Após a conclusão da replicação, máquinas virtuais de saudação iniciado no local secundário hello.

## <a name="perform-a-failover"></a>Executar um failover
Durante um failover não planejado, volumes do StorSimple Olá falharem em dispositivo virtual toohello, uma VM será levada no Azure, de réplica e volumes de Olá estão anexado toohello VM.

#### <a name="tooperform-a-failover"></a>tooperform um failover
1. No portal do Azure de Olá, selecione **dos serviços de recuperação** cofre &gt; **planos de recuperação (recuperação de Site)** &gt; **recoveryplan_name** criado para servidor de arquivos Olá VM.
2. Na folha de plano de recuperação de saudação, clique em **mais** &gt; **Failover**.  
3. Em Olá **confirmar Failover** folha, escolha a fonte de saudação e locais de destino.
4. Selecione **desligar máquinas virtuais e sincronize os dados mais recentes Olá** toospecify que recuperação de Site deve tente tooshut máquina virtual do hello protegida e sincronizar dados de Olá para que hello versão mais recente dos dados Olá será failover.
5. Após o failover hello, máquinas virtuais de saudação estão em um estado de confirmação pendente. Clique em **confirmar** toocommit Olá failover.


## <a name="perform-a-failback"></a>Executar um failback
Durante um failback, contêineres de volume StorSimple falha de dispositivo físico toohello voltar depois que um backup é feito.

#### <a name="tooperform-a-failback"></a>tooperform um failback
1. No portal do Azure de Olá, selecione **dos serviços de recuperação** cofre &gt; **planos de recuperação (recuperação de Site)** &gt; **recoveryplan_name** criado para servidor de arquivos Olá VM.
2. Na folha de plano de recuperação de saudação, clique em **mais** &gt; **Failover planejado**.  
3. Escolha os locais de origem e destino hello, a sincronização de dados apropriada Olá select e opções de criação de VM.
4. Clique em **Okey** botão o processo de failback toostart hello.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Práticas Recomendadas
### <a name="capacity-planning-and-readiness-assessment"></a>Planejamento da capacidade e avaliação de prontidão
#### <a name="hyper-v-site"></a>Site do Hyper-V
Saudação de uso [ferramenta Planejador de capacidade do usuário](http://www.microsoft.com/download/details.aspx?id=39057) toodesign Olá de servidor, armazenamento e infraestrutura de rede para seu ambiente de réplica do Hyper-V.

#### <a name="azure"></a>As tabelas
Você pode executar Olá [ferramenta de avaliação de preparação de máquina Virtual do Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) em VMs tooensure que eles sejam compatíveis com VMs do Azure e serviços de recuperação de Site do Azure. Olá, ferramenta de avaliação de prontidão verifica as configurações de VM e avisa quando as configurações são incompatíveis com o Azure. Por exemplo, ela emitirá um aviso se uma unidade C: tiver mais do que 127 GB.

O planejamento de capacidade é composto de, pelo menos, dois processos importantes:

* Mapeamento de tamanhos de VM do Hyper-V VMs tooAzure (por exemplo, A6, A7, A8 e A9) no local.
* Determinar Olá necessária largura de banda de Internet.

## <a name="limitations"></a>Limitações
* Atualmente, o dispositivo StorSimple somente 1 pode falhar (tooa único StorSimple Appliance de nuvem). cenário de saudação do servidor de arquivos que abrange vários dispositivos StorSimple ainda não é suportado.
* Se você receber um erro ao habilitar a proteção para uma máquina virtual, certifique-se de que você desconectou destinos iSCSI do hello.
* Todos os contêineres de volume Olá que foram agrupados devido a políticas de backup abrangência contêineres de volume realizarão failover juntos.
* Todos os volumes de saudação em contêineres de volume Olá escolhido serão submetidos a failover.
* Volumes que somam toomore de 64 TB não pode falhar porque a capacidade máxima de saudação de um único dispositivo de nuvem StorSimple é de 64 TB.
* Se falha de failover planejadas hello e Olá máquinas virtuais são criadas no Azure, em seguida, executar a limpeza não Olá VMs. Em vez disso, faça um failback. Se você excluir VMs hello, em seguida, Olá local VMs não podem ser ativadas novamente.
* Após um failover, se não for possível toosee Olá volumes, vá toohello VMs, abra o gerenciamento de disco, examinar novamente discos hello e, em seguida, colocá-los online.
* Em algumas instâncias, letras de unidade Olá no local de recuperação de desastres Olá podem ser diferentes do hello letras local. Se isso ocorrer, você precisará toomanually problema de saudação correto após a conclusão do failover de saudação.
* Autenticação multifator deve ser desabilitada para Olá credencial do Azure que é inserido na conta de automação hello como um ativo. Se essa autenticação não for desabilitada, scripts não poderão ser toorun automaticamente e o plano de recuperação de saudação falhará.
* Tempo limite do trabalho de failover: Olá StorSimple script atingirá o tempo limite se o failover de saudação de contêineres de volume leva mais tempo do que o limite do Azure Site Recovery Olá por script (atualmente 120 minutos).
* Tempo limite do trabalho de backup: Olá StorSimple script expira se Olá o backup de volumes demora mais tempo do que o limite do Azure Site Recovery Olá por script (atualmente 120 minutos).

  > [!IMPORTANT]
  > Executar backup Olá manualmente de saudação portal do Azure e execute novamente o plano de recuperação de saudação.

* Tempo limite do trabalho de clone: Olá StorSimple script expira se Olá clonagem de volumes leva mais tempo do que o limite do Azure Site Recovery Olá por script (atualmente 120 minutos).
* Erro de sincronização de hora: Olá StorSimple scripts erro dizendo que backups Olá tenham tido êxito mesmo que backup Olá seja bem-sucedida no portal de saudação. Uma causa possível para isso pode ser a que hora do dispositivo StorSimple que Olá pode ser fora de sincronia com hello hora atual no fuso horário de saudação.

  > [!IMPORTANT]
  > Sincronização Olá hora do dispositivo com hello hora atual no fuso horário de saudação.

* Erro de failover do dispositivo: Olá StorSimple script poderá falhar se houver um failover de dispositivo quando o plano de recuperação hello está sendo executado.

  > [!IMPORTANT]
  > Execute novamente o plano de recuperação Olá após a conclusão do failover de dispositivo de saudação.


## <a name="summary"></a>Resumo
Ao usar o Azure Site Recovery, você poderá criar um plano de recuperação de desastre automatizado completo para um servidor de arquivos de VM com compartilhamentos de arquivos hospedados no armazenamento do StorSimple. Você pode iniciar failover hello dentro de segundos de qualquer lugar no hello evento de interrupção e obter o aplicativo hello em funcionamento em poucos minutos.
