---
title: "aaaReplicate VMs VMware ou site tooanother de servidores físicos (portal clássico do Azure) | Microsoft Docs"
description: "Use este artigo tooreplicate VMs VMware ou Windows/Linux servidores físicos tooa site secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Replicar máquinas virtuais VMware a local ou site secundário do tooa servidores físicos no portal do Azure clássico de saudação

## <a name="overview"></a>Visão geral
O InMage Scout no Azure Site Recovery fornece replicação em tempo real entre os sites do VMWare no local. O InMage Scout está incluído nas assinaturas para o serviço Azure Site Recovery. 

## <a name="prerequisites"></a>Pré-requisitos
**Conta do Azure**: você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site.

## <a name="step-1-create-a-vault"></a>Etapa 1: criar um cofre
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em Novo > Gerenciamento > Backup e Site Recovery (OMS). Como alternativa, é possível clicar em Procurar > Cofre de Serviços de Recuperação > Adicionar.
3. Em **nome** especificar um cofre de saudação tooidentify nome amigável. Se você tiver mais de uma assinatura, selecione uma delas.
4. No **Grupo de recursos**, crie um novo grupo de recursos ou selecione um existente. Especifica campos de toocomplete necessária uma região do Azure.
5. Em **local**, selecione Olá região geográfica para Olá cofre. regiões de toocheck com suporte, consulte [preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Se você quiser tooquickly acesso Olá cofre da saudação painel clique toodashboard de Pin e, em seguida, clique em criar.
7. novo cofre de Hello serão exibidos na Olá painel > todos os recursos, e em Olá principal dos serviços de recuperação cofres de folha.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Etapa 2: Configurar o cofre hello e baixar os componentes do InMage Scout
1. Na folha de cofres de serviços de recuperação de saudação selecione seu cofre e clique em configurações.
2. Em **Configurações** > **Introdução**, clique em **Site Recovery** > Etapa 1: **Preparar a Infraestrutura** > **Meta de proteção**.
3. Em **objetivo de proteção** selecione toorecovery site e selecionar Sim, com VMware vSphere hipervisor. Em seguida, clique em OK.
4. Em **instalação Scout**, clique em download toodownload InMage Scout 8.0.1 GA chave de registro e de software. arquivos de instalação Olá para todos os Olá necessários componentes estão no arquivo. ZIP baixado de saudação.

## <a name="step-3-install-component-updates"></a>Etapa 3: Instalar atualizações de componentes
Leia sobre hello mais recente [atualizações](#updates). Você instalará os arquivos de atualização de saudação em servidores em Olá ordem a seguir:

1. Servidor RX se houver um
2. Servidores de configuração
3. Servidores de processo
4. Servidores de destino mestre
5. Servidores vContinuum
6. Servidor de origem (Windows e Linux Server)

Instale atualizações de saudação da seguinte maneira:

1. Baixar Olá [atualizar](https://aka.ms/asr-scout-update5) arquivo. zip. Esse arquivo. zip contém Olá seguintes arquivos:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA update4 bits para RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Extraia os arquivos. zip de saudação.<br>
3. **Para o servidor de RX Olá**: cópia **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** toohello server de RX e extraia-o. Em Olá extraído pasta, execute **/install**.<br>
4. **Para o servidor de processo do servidor de configuração de saudação**: cópia **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello servidor de configuração e o servidor de processo. Clique duas vezes em toorun-lo.<br>
5. **Para o servidor de destino mestre Windows hello**: tooupdate Olá unificado agent, cópia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de destino mestre. Clique duas vezes nele toorun-lo. Observe que Olá agente unificada também é o servidor de origem toohello aplicável se a fonte não é atualizada até Update4. Você deve instalá-lo no servidor de origem Olá bem, conforme mencionado posteriormente na lista.<br>
6. **Para o servidor de vContinuum Olá**: cópia **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum server.  Certifique-se de que você fechou o Assistente de vContinuum hello. Clique duas vezes em toorun de arquivo hello.<br>
7. **Para o servidor de destino mestre Linux Olá**: tooupdate Olá unificado agent, cópia **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello o servidor de destino mestre e extraia-o. Em Olá extraído pasta, execute **/install**.<br>
8. **Para o servidor de origem do Windows hello**: você não precisa tooinstall atualização 5 agente na fonte se a origem já está em update4. Se ele for menor que update4, aplique o agente de atualização de 5 hello.
Olá tooupdate unified agent, cópia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de origem. Clique duas vezes nele toorun-lo. <br>
9. **Para o servidor de origem Linux Olá**: tooupdate Olá agente unificado, copie a versão correspondente UA toohello Linux do servidor de arquivos e extraí-lo. Em Olá extraído pasta, execute **/install**.  Exemplo: Para o servidor do RHEL 6.7 de 64 bits, copie **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello server e extraia-o. Em Olá extraído pasta, execute **/install**.

## <a name="step-4-set-up-replication"></a>Etapa 4: Configurar a replicação
1. Configure a replicação entre origem hello e o destino VMware sites.
2. Para obter orientações, use Olá documentação InMage Scout que é baixada com o produto de saudação. Como alternativa, você pode acessar a documentação de saudação da seguinte maneira:

   * [Notas de versão](https://aka.ms/asr-scout-release-notes)
   * [Matriz de compatibilidade](https://aka.ms/asr-scout-cm)
   * [Guia do usuário](https://aka.ms/asr-scout-user-guide)
   * [Guia do usuário do RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Guia de instalação rápida](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Atualizações
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 Atualização 5
A Atualização 5 do Scout é uma atualização cumulativa. Ele tem todas as correções de saudação do update1 até update4 e novas correções de bug e aprimoramentos a seguir.
Correções que são adicionadas do ASR Scout update4 tooupdate5 são componentes de destino e vContinuum tooMaster específico. Se todos os seus servidores de origem, destino mestre, o servidor de configuração, o servidor de processo e RX já estão no ASR Scout update4, em seguida, você precisa tooapply atualização 5 apenas no servidor de destino mestre. 

**Novo suporte de plataforma**
* SUSE Linux Enterprise Server 11 Service Pack 4 (SP4)

> [!NOTE]
> O SLES 11 SP4 64 bits **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** é empacotado com o pacote base **InMage_Scout_Standard_8.0.1 GA.zip** do Scout GA. Baixe o pacote Scout GA do portal conforme mencionado na [etapa 1](#step-1-create-a-vault).
>

**Correção de bugs e melhorias**

* Aumentar a confiabilidade de suporte de Cluster do Windows
    * Algum tempo fixo alguns Olá P2V MSCS tornam-se de discos de cluster RAW após a recuperação
    * Recuperação de cluster do MSCS de P2V Fixed-falha devido a incompatibilidade de ordem de toodisk
    * Corrigido – A operação de adicionar discos do cluster do MSCS falha com incompatibilidade de tamanho de disco
    * Corrigido – A verificação de preparação de mapeamento de cluster do MSCS de origem com LUNs de RDM falha na verificação de tamanho
    * Proteção de cluster de nó único Fixed-falha devido a problema de incompatibilidade de tooSCSI 
    * Fixed-proteger novamente do hello P2V Windows cluster server falhará se houver discos de cluster de destino. 
    
* Durante a proteção de failback se MT selecionado não está em Olá mesmo servidor ESXi como máquina de origem que Olá protegido (durante a proteção forward), vContinuum pega MT errado Olá durante a recuperação de Failback e subsequentemente Falha na operação de recuperação.

> [!NOTE]
> 
> * Acima P2V correções de cluster é tooonly aplicável esses cluster do MSCS físico protegidos com ASR Scout update5 recentemente. tooavail Olá cluster correções em Olá já protegido cluster MSCS P2V com as atualizações mais antigas, precisa toofollow Olá etapas de atualização que são mencionadas na seção Olá 12, atualização protegido P2V MSCS cluster tooScout Update5 de [ASR Scout versão Notas de](https://aka.ms/asr-scout-release-notes).
> 
> * Proteger novamente do cluster do MSCS físico pode reutilizar os discos de destino existentes somente se em tempo de saudação de nova proteção, Olá mesmo conjunto de discos estão ativos em cada um de nós em que estavam quando inicialmente protegidos de cluster de saudação. Se não, em seguida, há etapas manuais conforme mencionado na seção 12 [ASR Scout notas](https://aka.ms/asr-scout-release-notes) muito mover Olá destino discos toohello repositório de dados correto caminho toore-uso-los durante a nova proteção. Se proteja o cluster do MSCS Olá no modo de P2V sem seguir as etapas de atualização, em seguida, ele criará novo disco no servidor de ESXi do destino de saudação. Você precisa toomanually delete Olá antigo discos de armazenamento de dados de saudação.
> 
> * Origem sempre que SLES11 ou SLES11 com qualquer servidor do pacote de serviço é reinicializado normalmente, um deve marcar manualmente Olá **raiz** disco pares de replicação para sincronizar novamente, ele não será notificado na UI CX. Se você não ' marca Olá raiz disco para ressincronização, você poderá ver problemas de integridade (DI) de dados.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Atualização 4
Scout Atualização 4 é uma atualização cumulativa. Ele tem todas as correções de saudação do update1 até update3 e novas correções de bug e aprimoramentos a seguir.

**Novo suporte de plataforma**

* Foi adicionado suporte para o vCenter/vSphere 6.0, 6.1 e 6.2
* Foi adicionado suporte para os seguintes sistemas operacionais Linux
  * Red Hat Enterprise Linux (RHEL)7.0, 7.1 e 7.2
  * CentOS 7.0, 7.1 e 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> O RHEL/CentOS 7 64 bits **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** é empacotado com o pacote **InMage_Scout_Standard_8.0.1 GA.zip** do Scout GA. Baixe o pacote Scout GA do portal conforme mencionado na [etapa 1](#step-1-create-a-vault).
>
>

**Correção de bugs e melhorias**

* Desligamento melhor tratamento de seguir Linux OSes e clones tooprevent problemas ressincronização indesejados.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Para Linux, acesso completo da pasta permissões no diretório de instalação do agente unificado agora são restrito apenas toohello de usuário local.
* No Windows, o problema de tempo limite ao emitir o indicador de consistência comum distribuído em aplicativos distribuídos muito carregados como clusters SQL e SharePoint.
* Adicionado log relacionado à correção no instalador base do CX.
* Link de download do VMware vCLI 6.0 é adicionado tooWindows instalador de base de destino mestre.
* Adicionadas mais verificações e logs para alterações de configurações de rede durante o failover e análise de DR.
* Informações de retenção em algum momento não são relatado toohello CX.  
* Para o cluster físico, a operação de redimensionamento do volume por meio do assistente vContinuum falhará quando tiver ocorrido redução de volume.
* Cluster proteção falhou com o erro "Assinatura de disco com falha toofind hello" quando o disco de cluster é o disco PRDM.
* falha do servidor de transporte de cxps devido à exceção fora do intervalo.
* O nome do servidor e as colunas IP agora são redimensionáveis na página de instalação por push do assistente vContinuum.
* Melhorias de API do RX
  * Fornece os cinco pontos de consistência comuns disponíveis mais recentes (apenas marcas garantidas).
  * Fornece detalhes de espaço livre e de capacidade para todos os Olá dispositivos protegidos.
  * Fornece o estado do driver Scout no servidor de origem.

> [!NOTE]
> * O pacote base **InMage_Scout_Standard_8.0.1_GA.zip** agora atualizou o instalador base do CX **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** e o instalador base de Destino Mestre do Windows **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Para toda nova instalação, use os novos bits de GA de Destino Mestre do Windows e do CX.
> * A Atualização 4 pode ser aplicada diretamente no GA 8.0.1.
> * servidor de configuração de saudação e RX atualizações não podem ser revertidas depois que são aplicados no sistema de saudação.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Atualização 3 do Azure Site Recovery Scout 8.0.1
Atualização 3 inclui o seguinte Olá correções e aprimoramentos:

* servidor de configuração de saudação e RX falhar Cofre de recuperação de Site toohello tooregister quando eles estão por trás do proxy de saudação.
* Olá número de horas que Olá objetivo de ponto de recuperação (RPO) não for atendido não está sendo atualizada no relatório de integridade de saudação.
* servidor de configuração de saudação não está sincronizando com RX quando os detalhes de hardware Olá ESX ou detalhes de rede contêm caracteres UTF-8.
* Controladores de domínio do Windows Server 2008 R2 não tooboot após a recuperação.
* A sincronização offline não está funcionando conforme o esperado.
* Após o failover da máquina virtual (VM), exclusão do par de replicação fica preso Olá CX UI por um longo tempo, e os usuários não é possível concluir o failback de saudação ou retomar a operação.
* Geral operações de instantâneo que são feitas pelo trabalho de consistência Olá foram otimizadas toohelp reduzir aplicativo desconecta como clientes do SQL.
* saudação de desempenho da ferramenta de consistência da saudação (VACP.exe) foi aprimorada reduzindo o uso de memória de saudação que é necessário para a criação de instantâneos no Windows.
* Olá instale falhas de serviço quando senha Olá é maior que 16 caracteres.
* vContinuum não está verificando e solicitar novas credenciais vCenter quando as credenciais de saudação forem alteradas.
* No Linux, Gerenciador de cache de destino mestre hello (cachemgr) não está baixando arquivos de saudação do servidor de processo, que resulta na limitação de par de replicação.
* Quando ordem de disco de cluster (MSCS) Olá failover físico é não Olá iguais em todos os nós de hello, a replicação não está definida para alguns dos volumes de cluster hello.
  <br/>Observe que cluster Olá precisa toobe reprotegida tootake vantagem dessa correção.  
* Funcionalidade de SMTP não está funcionando conforme o esperado depois RX é atualizado de Scout 7.1 tooScout 8.0.1.
* Estatísticas mais foram adicionadas no log de saudação tempo Olá reversão operação tootrack Olá sua toocomplete-lo.
* Foi adicionado suporte para sistemas operacionais de Linux no servidor de origem hello:
  * Red Hat Enterprise Linux (RHEL) 6 atualização 7
  * CentOS 6 Atualização 7
* Olá CX e RX interface do usuário agora podem mostrar notificação Olá para o par de hello, entra no modo de bitmap.
* Olá seguintes correções de segurança foram adicionadas em RX:

| **Descrição do problema** | **Procedimentos de implementação** |
| --- | --- |
| Autorização ignorada por meio de violação de parâmetros |Usuários toonon aplicável de acesso restrito. |
| Solicitação entre sites forjada |Conceito de página token Olá implementado, que gera aleatoriamente para cada página. <br/>Com isso, você verá: <li> Há apenas uma única entrada instância para Olá mesmo usuário.</li><li>Atualização de página não funciona – ele redirecionará toohello painel.</li> |
| Carregamento de arquivo mal-intencionado |Extensões de toocertain arquivos restritos. Extensões permitidas: 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml e zip. |
| Script persistente entre sites |Validações de entrada adicionadas. |

> [!NOTE]
> * Todas as atualizações de Recuperação de Site são cumulativas. Atualização 3 tem todas as correções de saudação de atualização 1 e 2 da atualização. A Atualização 3 pode ser aplicada diretamente a 8.0.1 GA.
> * servidor de configuração de saudação e RX atualizações não podem ser revertidas depois que são aplicados no sistema de saudação.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Atualização 2 (atualização de 3 de dezembro de 2015)
As correções na Atualização 2 incluem:

* **Servidor de configuração**: para corrigir um problema que impediu o recurso de medição livre Olá 31 dias de trabalho conforme o esperado quando hello, servidor de configuração foi registrado na recuperação de Site.
* **Agente unificado**: para corrigir um problema na atualização 1 que resultaram em atualização de saudação não está sendo instalada no servidor de destino mestre hello quando ele foi atualizado da versão 8.0 too8.0.1.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Atualização 1
Atualização 1 inclui o seguinte Olá correções de bugs e novos recursos:

* 31 dias de proteção gratuita por instância de servidor. Isso permite que você tootest funcionalidade ou configurar uma prova de conceito.
  * Todas as operações no servidor de saudação, inclusive failover e failback, são gratuitas para Olá primeiro 31 dias, a partir do tempo de saudação que um servidor é protegido pela primeira vez com Scout de recuperação de Site.
  * De saudação 32nd dia em diante, cada servidor protegido será cobrado na taxa de instâncias padrão Olá para o site de propriedade do cliente do Azure Site Recovery proteção tooa.
  * A qualquer momento, o número de Olá dos servidores protegidos que estão atualmente sendo cobradas está disponível na página do painel de saudação do cofre do Azure Site Recovery hello.
* Foi adicionado suporte para vCLI (Interface de Linha de Comando de vSphere) em 5.5 Atualização 2.
* Suporte adicionado para sistemas operacionais de Linux no servidor de origem hello:
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Saudação de tooaddress de correções de bugs problemas a seguir:
  * Falha de registro do cofre para o servidor de configuração de saudação ou RX.
  * Os volumes de cluster não aparecem conforme o esperado quando máquinas virtuais clusterizadas são protegidas ao serem retomadas.
  * Failback falha quando o servidor de destino mestre hello está hospedado em um servidor de ESXi diferente da saudação em produção máquinas virtuais.
  * Permissões de arquivo de configuração são alteradas quando você atualizar too8.0.1, o que afeta a proteção e as operações.
  * limite de ressincronização Olá não é imposta conforme o esperado, o que leva o comportamento da replicação tooinconsistent.
  * configurações de RPO Olá não estão aparecendo corretamente na interface de servidor de configuração de saudação. valor dos dados Olá descompactado incorretamente mostra o valor de Olá compactado.
  * operação de remoção de saudação não exclui conforme esperado no Assistente de vContinuum hello e replicação não é excluída da interface de servidor de configuração de saudação.
  * No Assistente de vContinuum hello, disco hello está desmarcado automaticamente quando você clica em **detalhes** na exibição de disco Olá durante a proteção de máquinas virtuais MSCS.
  * Durante o cenário de (P2V) físico para virtual hello, serviços HP necessários, como CIMnotify e CqMgHost, não são movido toomanual na recuperação de máquina virtual. Isso resulta em tempo de inicialização adicional.
  * Proteção da máquina virtual Linux falhará quando houver mais de 26 discos no servidor de destino mestre hello.

## <a name="next-steps"></a>Próximas etapas
Poste perguntas que você tem em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
