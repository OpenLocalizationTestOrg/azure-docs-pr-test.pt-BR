---
title: "ferramenta de Planejador de capacidade aaaRun Olá Hyper-V para recuperação de Site | Microsoft Docs"
description: "Este artigo descreve como toorun Olá ferramenta do Planejador de capacidade de Hyper-V para o Azure Site Recovery"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Execute a ferramenta de Planejador de capacidade Olá Hyper-V para recuperação de Site

Como parte da implantação do Azure Site Recovery, você precisa toofigure sua replicação e os requisitos de largura de banda. ferramenta do Planejador de capacidade de saudação Hyper-V para recuperação de Site ajuda você toodo isso, para replicação de máquina virtual do Hyper-V.

Este artigo descreve como toorun Olá ferramenta do Planejador de capacidade de Hyper-V. Essa ferramenta deve ser usada junto com informações Olá [planejamento de capacidade para recuperação de Site](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Antes de começar
Você executa a ferramenta de saudação em um nó de cluster ou servidor do Hyper-V em seu site primário. servidores de host de Hyper-V toorun Olá ferramenta Olá precisa:

* Sistema operacional: Windows Server 2012 ou 2012 R2
* Memória: 20 MB (mínimo)
* CPU: sobrecarga de 5% (mínimo)
* Espaço em disco: 5 MB (mínimo)

Antes de executar a ferramenta Olá, é necessário site primário do tooprepare hello. Se você estiver replicando entre dois sites locais e você deseja toocheck largura de banda, é necessário tooprepare um servidor de réplica.

## <a name="step-1-prepare-hello-primary-site"></a>Etapa 1: Preparar o site primário Olá

1. No site primário do hello, faça uma lista de todos os Olá VMs Hyper-V que você deseja tooreplicate e Olá hosts/clusters de Hyper-V no qual está localizados. pode executar a ferramenta de saudação para vários hosts autônomos ou para um único cluster, mas não os dois juntos. Ele também precisa toorun separadamente para cada sistema operacional, então você deve reunir informações sobre servidores Hyper-V da seguinte maneira:

   * Servidores independentes Windows Server 2012
   * Clusters do Windows Server 2012
   * Servidores independentes Windows Server 2012 R2
   * Clusters do Windows Server 2012 R2
2. Habilite acesso remoto tooWMI em todos os hosts do Hyper-V hello e clusters. Execute este comando em cada servidor/cluster, as regras de firewall se toomake e permissões de usuário são definidas:

        netsh firewall set service RemoteAdmin enable
3. Habilite o monitoramento do desempenho nos servidores e clusters da seguinte maneira:

   * Olá abrir o Firewall do Windows com hello **segurança avançada** snap-in, e, em seguida, regras de entrada a seguir Olá enable: **acesso à rede COM+ (DCOM-IN)** e todas as regras em Olá **Log de eventos remoto Grupo de gerenciamento**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Etapa 2: Preparar um servidor de réplica (replicação do local tooon local)
Você não precisa toodo isso se você estiver replicando tooAzure.

É recomendável configurar um único host Hyper-V como um servidor de recuperação, para que uma VM fictícia possa ser replicadas tooit toocheck banda.  Você pode ignorar isso, mas não será capaz de toomeasure de largura de banda, a menos que você fazê-lo.

1. Se você quiser toouse um nó de cluster como réplica Olá configurar agente de réplica do Hyper-V:

   * Em **Gerenciador do Servidor**, abra **Gerenciador de Cluster de Failover**.
   * Conecte-se o cluster toohello, realce o nome do cluster hello e clique em **ações** > **configurar função** tooopen Assistente de alta disponibilidade de saudação.
   * Em **Selecionar Função**, clique em **Agente de Réplica do Hyper-V**. No Assistente de saudação fornecem um **nome NetBIOS** e hello **endereço IP** toobe usado como cluster de toohello de ponto de conexão hello (chamado de ponto de acesso de cliente). Olá **agente de réplica do Hyper-V** serão configurados, resultando em um nome de ponto de acesso de cliente que você deve observar.
   * Verifique se essa função de agente de réplica do Hyper-V Olá é colocada online com êxito e pode fazer failover entre todos os nós do cluster de saudação. toodo isso, clique com botão direito função hello, aponte muito**mover**e, em seguida, clique em **selecionar nó**. Selecione um nó > **OK**.
   * Se você estiver usando a autenticação baseada em certificado, verifique se cada nó de cluster e todos os de ponto de acesso de cliente à saudação ter certificado Olá instalado.
2. Habilite um servidor de réplica:

   * Para um cluster de abrir o Gerenciador de Cluster de falha, conecte-se toohello cluster e clique em **funções** > Selecionar função > **as configurações de replicação** > **habilitar este cluster como uma réplica servidor**. Se você usar um cluster como réplica Olá, você precisará de função do agente de réplica do Hyper-V de Olá toohave presente no cluster Olá no site primário Olá também.
   * Para um servidor autônomo, abra o Gerenciador Hyper-V. Em hello **ações** painel, clique em **configurações do Hyper-V** para o servidor de saudação você deseja tooenable e, em **configuração de replicação** clique **habilitar isso como um servidor de réplica**.
3. Configure a autenticação:

   * Em **autenticação e portas**, selecione como tooauthenticate Olá servidor primário e as portas de autenticação hello. Se você usar um certificado clique **Selecionar certificado** tooselect um. Usar o Kerberos se hosts de Hyper-V primário e de recuperação Olá estiverem em Olá mesmo domínio, ou em domínios confiáveis. Use certificados para domínios diferentes ou para uma implantação de grupo de trabalho.
   * Em **autorização e armazenamento**, permitir **qualquer** autenticado o servidor de réplica do servidor (primário) toosend replicação dados toothis.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Executar **netsh http show servicestate**, toocheck esse ouvinte hello está sendo executado para Olá protocolo/porta especificada:  
4. Configure os firewalls. Durante a instalação do Hyper-V, as regras de firewall são criadas tooallow tráfego em portas de padrão de saudação (HTTPS em 443, Kerberos em 80). Habilite essas regras da seguinte maneira:
  - Autenticação de certificado no cluster (443): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Autenticação Kerberos no cluster (80): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Autenticação de certificado no servidor independente: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Autenticação Kerberos no servidor independente: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Etapa 3: Executar a ferramenta do Planejador de capacidade de saudação
Depois que você preparou seu site primário, e configurar um servidor de recuperação, você pode executar a ferramenta de saudação.

1. [Baixar](https://www.microsoft.com/download/details.aspx?id=39057) ferramenta de saudação do hello Microsoft Download Center.
2. Execute a ferramenta de saudação de um dos servidores primários hello (ou um de nós de saudação do cluster primário Olá). Clique Olá .exe arquivo e, em seguida, escolha **executar como administrador**.
3. Em **antes de começar**, especifique por quanto tempo você deseja que os dados de toocollect. Recomendamos que você execute a ferramenta de saudação durante a produção horas tooensure dados são representativo. Se você estiver apenas tentando toovalidate conectividade de rede, você pode coletar apenas um minuto.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. Em **detalhes do site primário**, especifique o nome do servidor de saudação ou FQDN para um host autônomo ou para um cluster especifique Olá FQDN do cliente Olá aceitar ponto, o nome do cluster ou qualquer nó no cluster hello e, em seguida, clique em **próximo**. ferramenta de saudação detecta automaticamente o nome de saudação do servidor de saudação estiver executando no. Olá ferramenta seleciona máquinas virtuais que podem ser monitorados Olá servidores especificados.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. Em **detalhes do Site de réplica**, se você estiver replicando tooAzure ou se você estiver replicando o datacenter secundário tooa e ainda não tiver configurado um servidor de réplica, selecione **ignore os testes que envolvem o local da réplica**. Se você estiver replicando o datacenter secundário tooa e configurar um tipo de réplica, digite FQDN do servidor autônomo de saudação ou ponto de acesso para cliente Olá para cluster de saudação em **Server nome (ou) CAP de agente de réplica do Hyper-V**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. Em **detalhes da réplica estendida**, habilitar **Olá ignorar testa o site de réplica estendida que envolvem**. Não há suporte para eles no Site Recovery.
7. Em **escolha VMs tooReplicate**, ferramentas Olá conecta toohello servidor ou cluster e exibe as máquinas virtuais e discos em execução no servidor primário hello, acordo com as configurações de saudação você especificou no hello **detalhes do Site primário**  página. As VMs já foram habilitadas para replicação, ou as que não estão em execução não serão exibidas. Selecione VMs Olá para o qual você deseja toocollect métricas. Selecionar Olá VHDs automaticamente coleta dados de para Olá VMs muito.
8. Se você tiver configurado um servidor de réplica ou um cluster, em **informações de rede**, especifique Olá aproximado largura de banda WAN você acha que será usada entre os sites primário e de réplica de hello e certificados Olá selecione se você tiver configurado autenticação de certificado.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. Em **resumo**, verifique as configurações de saudação e clique em **próximo** toobegin coletar métricas. Progresso da ferramenta e o status é exibido na Olá **calcular capacidade** página. Quando a ferramenta Olá concluir a execução, clique em **Exibir relatório** tooview saída de hello. Por padrão, os relatórios e logs são armazenados em **%systemdrive%\Users\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Etapa 4: Interpretar os resultados de saudação

Aqui estão as métricas importantes hello. Você pode ignorar as métricas que não estão listadas aqui. Elas não são relevantes para a Recuperação de Site.

### <a name="on-premises-tooon-premises-replication"></a>Replicação de local tooon local

* Impacto da replicação na computação do host primário hello, memória
* Impacto da replicação em Olá primário, espaço de disco de armazenamento do grupo de hosts da recuperação, IOPS
* Largura de banda total necessária para a replicação delta (Mbps)
* Largura de banda de rede observado entre o host principal hello e host de recuperação da saudação (Mbps)
* Sugestão de número ideal de saudação paralelas de transferências de ativas entre dois hosts/clusters Olá

### <a name="on-premises-tooazure-replication"></a>Replicação do local tooAzure

* Impacto da replicação na computação do host primário hello, memória
* Impacto da replicação no espaço de disco de armazenamento do host primário hello, IOPS
* Largura de banda total necessária para a replicação delta (Mbps)

## <a name="more-resources"></a>Mais recursos
* Para obter informações detalhadas sobre a ferramenta hello, leia o documento de saudação que acompanha o download da ferramenta hello.
* Assista a um passo a passo de ferramenta de saudação de Keith Mayer [blog do TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Obter resultados Olá](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) de nosso teste de desempenho para replicação de Hyper-V local tooon local

## <a name="next-steps"></a>Próximas etapas

Depois de concluir o planejamento de capacidade, você pode iniciar a implantação do Site Recovery:

* [Replicar máquinas virtuais do Hyper-V no VMM nuvens tooAzure](site-recovery-vmm-to-azure.md)
* [Replicar máquinas virtuais do Hyper-V (sem VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Replicar VMs do Hyper-V entre sites do VMM](site-recovery-vmm-to-vmm.md)
