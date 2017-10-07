---
title: "aaaSet uma política de replicação para o site secundário do Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset uma política para a VM do Hyper-V replicação tooa VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Etapa 8: Configurar uma política de replicação

Depois de configurar [mapeamento de rede](vmm-to-vmm-walkthrough-network-mapping.md), use tooset este artigo a uma política de replicação para o Hyper-V máquina virtual (VM) replicação tooa site secundário, usando [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de começar

- Quando você cria uma política de replicação, todos os hosts usando a política de saudação deve ter Olá mesmo sistema operacional. saudação de nuvem do VMM pode conter hosts Hyper-V executando diferentes versões do Windows Server, mas nesse caso, você precisa de várias políticas de replicação.
- Você pode executar Olá a replicação inicial offline.

## <a name="configure-replication-settings"></a>Definir configurações de replicação

1. toocreate uma nova política de replicação, clique em **preparar infraestrutura** > **as configurações de replicação** > **+ criar e associar**.

    ![Rede](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. Em **Criar e associar política**, especifique um nome de política. Olá tipo de origem e destino deve ser **Hyper-V**.
3. Em **versão de host do Hyper-V**, selecione o sistema operacional que está em execução no host de saudação.
4. Em **tipo de autenticação** e **porta de autenticação**, especifique como o tráfego será autenticado entre hello primário e servidores de host do Hyper-V de recuperação. Selecione **Certificado** , a menos que você tenha um ambiente Kerberos em funcionamento. A Recuperação de Site do Azure configurará automaticamente os certificados para autenticação HTTPS. Você não precisa toodo nada manualmente. Por padrão, as portas 8083 e 8084 (para certificados) serão aberta no hello Firewall do Windows nos servidores de host do Hyper-V hello. Se você selecionar **Kerberos**, um tíquete Kerberos será usado para autenticação mútua dos servidores de host de saudação. Observe que esta configuração só é relevante para servidores de host Hyper-V no Windows Server 2012 R2.
5. Em **frequência de cópia**, especifique com que frequência tooreplicate delta dados após a replicação inicial da saudação (a cada 30 segundos, 5 ou 15 minutos).
6. Em **retenção de ponto de recuperação**, especifique, em horas, quanto tempo uma janela de retenção Olá será possível para cada ponto de recuperação. Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela.
7. Em **Frequência do instantâneo consistente com aplicativo**, especifique com que frequência (1 a 12 horas) são criados os pontos de recuperação que contêm instantâneos consistentes com o aplicativo. Hyper-V usa dois tipos de instantâneos — um instantâneo padrão que fornece um instantâneo incremental da saudação toda a máquina virtual e um instantâneo consistente com o aplicativo que usa um instantâneo point-in-time dos dados de aplicativo hello dentro da máquina virtual de saudação. Instantâneos consistentes com o aplicativo usam tooensure Volume Shadow Copy Service (VSS) que os aplicativos estejam em um estado consistente quando Olá instantâneo é tirado. Se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de saudação de aplicativos executados em máquinas virtuais de origem. Verifique se o valor de saudação definido é menor do que o número de saudação de pontos de recuperação adicionais que você configurar.
8. Em **Compactação da transferência de dados**, especifique se os dados replicados transferidos devem ser compactados.
9. Selecione **excluir réplica VM**, toospecify que Olá a máquina virtual de réplica deve ser excluída se você desabilitar a proteção para a VM de origem hello. Se você habilitar essa configuração, quando você desativar a proteção para a fonte de saudação VM, ele será removido do console de recuperação de Site hello, configurações de recuperação de Site para Olá VMM serão removidas do console do VMM hello e Olá réplica será excluída.
10. Em **inicial do método de replicação**, se você estiver replicando em rede hello, especifique se toostart Olá a replicação inicial ou agendá-la. toosave a largura de banda de rede, talvez você queira tooschedule-lo fora do horário de ocupado. Em seguida, clique em **OK**.

     ![Política de replicação](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Quando você cria uma nova política está associado automaticamente Olá nuvem do VMM. Em **Política de replicação**, clique em **OK**. Você pode associar nuvens do VMM adicionais (e Olá VMs neles) com esta política de replicação em **replicação** > nome da política > **associar VMM nuvem**.

     ![Política de replicação](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline

Você pode fazer a replicação offline para cópia de dados iniciais de saudação. Você pode preparar isso da seguinte maneira:

* No servidor de origem Olá, você deve especificar um caminho local do qual Olá exportação de dados ocorrerá. Atribua controle total para permissões de NTFS e compartilhamento de serviço do VMM toohello no caminho de exportação de saudação. No servidor de destino hello, você especificar um caminho local do qual importar dados de saudação ocorrerá. Atribua Olá mesmas permissões neste caminho de importação.
* Se hello importar ou exportar caminho for compartilhado, atribua a associação de grupo de administrador, usuário avançado, operador de impressão ou operador de servidor para a conta de serviço do VMM Olá no computador remoto Olá no qual Olá compartilhado está localizado.
* Se você estiver usando quaisquer hosts de tooadd da contas executar como, em Olá importar e exportar caminhos, atribuir a leitura e permissões de gravação toohello as contas executar como no VMM.
* Olá importar e exportar compartilhamentos não deve estar localizado em qualquer computador usado como um servidor de host do Hyper-V, porque não há suporte para a configuração de loopback pelo Hyper-V.
* No Active Directory, em cada servidor de host do Hyper-V que contém máquinas virtuais que você deseja tooprotect, habilitar e configurar a delegação restrita tootrust Olá computadores remotos nos quais Olá importação e exportação do caminhos estão localizados, da seguinte maneira:
  1. No controlador de domínio hello, abra **computadores e usuários do Active Directory**.
  2. Na árvore de console hello, clique em **DomainName** > **computadores**.
  3. Nome do servidor de host com o botão direito Olá Hyper-V > **propriedades**.
  4. Em Olá **delegação** , clique em **confiar no computador para delegação toospecified dos serviços somente**.
  5. Clique em **Usar qualquer protocolo de autenticação**.
  6. Clique em **Adicionar** > **Usuários e Computadores**.
  7. Nome do tipo saudação do computador de saudação que hospeda o caminho de exportação hello > **Okey**. Na lista de saudação de serviços disponíveis, mantenha pressionada a tecla CTRL de saudação e clique em **cifs** > **Okey**. Repita para nome de saudação do computador Olá desse caminho de importação de saudação hosts. Repita conforme necessário para servidores host Hyper-V adicionais.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 9: habilitar replicação](vmm-to-vmm-walkthrough-enable-replication.md).
