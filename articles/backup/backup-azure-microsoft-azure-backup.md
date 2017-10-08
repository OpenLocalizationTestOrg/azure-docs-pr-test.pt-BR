---
title: aaaUse tooback de servidor de Backup do Azure backup tooAzure de cargas de trabalho | Microsoft Docs
description: Usar o Azure Backup Server tooprotect ou fazer backup de cargas de trabalho toohello portal do Azure.
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: servidor de backup do Azure; proteger cargas de trabalho; fazer backup de cargas de trabalho
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparando tooback cargas de trabalho usando o servidor de Backup do Azure
> [!div class="op_single_selector"]
> * [Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Este artigo explica como tooprepare tooback seu ambiente cargas de trabalho usando o servidor de Backup do Azure. Com o Servidor de Backup do Azure, você pode proteger cargas de trabalho do aplicativo como VMs do Hyper-V, o Microsoft SQL Server, o SharePoint Server, o Microsoft Exchange e os clientes do Windows em um único console.

> [!NOTE]
> O Servidor de Backup do Azure agora pode proteger VMs do VMware e fornece recursos de segurança aprimorada. Instalar o produto Olá conforme explicado nas seções de saudação abaixo. Aplicar a atualização 1 e hello Azure Backup Agent mais recente. toolearn mais sobre o backup de servidores do VMware com o servidor de Backup do Azure, consulte o artigo Olá [tooback do servidor de Backup do Azure Use um servidor VMware](backup-azure-backup-server-vmware.md). toolearn sobre os recursos de segurança, consulte muito[documentação de recursos de segurança de backup do Azure](backup-azure-security-feature.md).
>
>

Você também pode proteger cargas de trabalho de IaaS (infraestrutura como serviço), como VMs no Azure.

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo fornece informações hello e procedimentos para restaurar as VMs implantadas usando o modelo do Gerenciador de recursos de saudação.
>
>

Servidor de Backup do Azure herda grande parte da funcionalidade de backup de cargas de trabalho de saudação do Data Protection Manager (DPM). Este artigo contém links tooDPM documentação tooexplain alguns Olá funcionalidade compartilhada. Embora o Azure Backup Server compartilha muitas das Olá mesma funcionalidade que o DPM. Servidor de Backup do Azure não fazer backup tootape nem, ele é integrado com o System Center.

## <a name="1-choose-an-installation-platform"></a>1. Escolher uma plataforma de instalação
a primeira etapa Olá para colocar hello Azure Backup Server em execução é tooset um servidor do Windows. Seu servidor pode estar no Azure ou ser local.

### <a name="using-a-server-in-azure"></a>Usando um servidor no Azure
Ao escolher um servidor executando o Servidor de Backup do Azure, é recomendável iniciar com uma imagem da galeria do Windows Server 2012 R2 Datacenter. artigo Hello, [criar sua primeira máquina virtual do Windows no portal do Azure de saudação](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), fornece um tutorial de Introdução ao Olá recomendado de máquina virtual no Azure, mesmo se você nunca usou o Azure antes. Olá recomendado requisitos mínimos para Olá server VM (máquina virtual) deve ser: A2 padrão com dois núcleos e 3,5 GB de RAM.

Proteger as cargas de trabalho com o Servidor de Backup do Azure tem muitas nuanças. artigo Hello, [instalar o DPM como uma máquina virtual do Azure](https://technet.microsoft.com/library/jj852163.aspx), ajuda a explicar essas nuances. Antes de implantar a máquina hello, leia este artigo completamente.

### <a name="using-an-on-premises-server"></a>Usando um servidor local
Se você não quiser toorun Olá básica de servidor no Azure, você pode executar o servidor de saudação em uma VM Hyper-V, uma VM do VMware ou um host físico. Olá recomendado requisitos mínimos de hardware do servidor de saudação são dois núcleos e 4 GB de RAM. sistemas operacionais de saudação com suporte são listados na Olá a tabela a seguir:

| Sistema operacional | Plataforma | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 e SPs mais recentes |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 e SPs mais recentes |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 e SPs mais recentes |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 e SPs mais recentes |64 bits |Standard, Workgroup |

Você pode eliminar duplicação de armazenamento do DPM hello usando eliminação de duplicação do Windows Server. Saiba mais sobre como o [DPM e a eliminação de duplicação](https://technet.microsoft.com/library/dn891438.aspx) funcionam juntos quando implantados em VMs do Hyper-V.

> [!NOTE]
> Servidor de Backup do Azure é toorun projetado em um servidor dedicado de finalidade única. Você não pode instalar o Servidor de Backup do Azure em:
> - Um computador que esteja sendo executado como um controlador de domínio
> - Um computador no qual servidor de aplicativos Olá função está instalada
> - Um computador que seja um servidor de gerenciamento do System Center Operations Manager
> - Um computador que o Exchange Server está executando
> - Um computador que seja um nó de um cluster

Ingresse em domínio do servidor de Backup do Azure tooa sempre. Se você planejar toomove Olá server tooa outro domínio, é recomendável que você associar Olá server toohello novo domínio antes de instalar o servidor de Backup do Azure. Mover um servidor de Backup do Azure existente tooa novo domínio do computador após a implantação *não tem suporte*.

## <a name="2-recovery-services-vault"></a>2. Cofre dos Serviços de Recuperação
Se você envia dados de backup tooAzure ou mantê-lo localmente, software Olá precisa tooAzure toobe conectado. toobe mais específico, precisa de máquina do Azure Backup Server Olá toobe registrado com um cofre de serviços de recuperação.

Cofre de serviços de toocreate uma recuperação:

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **procurar** e, na lista de saudação de recursos, digite **dos serviços de recuperação**. Como começar a digitar, Olá filtros de lista com base em sua entrada. Clique em **Cofre dos Serviços de Recuperação**.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    saudação de lista de cofres de serviços de recuperação é exibida.
3. Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.

    ![Criar Cofre de Serviços de Recuperação - etapa 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Para **nome**, insira um cofre de saudação tooidentify nome amigável. nome da saudação precisa toobe exclusivo Olá assinatura do Azure. Digite um nome que contenha de 2 a 50 caracteres. Ele deve começar com uma letra e pode conter apenas letras, números e hifens.
5. Clique em **assinatura** toosee Olá lista de assinaturas. Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura. Só haverá múltiplas opções se sua conta organizacional estiver associada a várias assinaturas do Azure.
6. Clique em **grupo de recursos** toosee Olá a lista de grupos de recursos disponíveis, ou clique em **novo** toocreate um novo grupo de recursos. Para obter informações completas sobre Grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Clique em **local** tooselect Olá região para o cofre hello.
8. Clique em **Criar**. Pode levar algum tempo para Olá toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status de saudação na área superior direito de saudação no portal de saudação.
   Depois de criar seu cofre, ele é aberto no portal de saudação.

### <a name="set-storage-replication"></a>Definir replicação de armazenamento
opção de replicação de armazenamento Olá permite toochoose entre o armazenamento com redundância geográfica e o armazenamento redundante localmente. Por padrão, seu cofre tem armazenamento com redundância geográfica. Se o cofre é seu compartimento primário, deixe Olá opção set toogeo redundância de armazenamento. Escolha o armazenamento com redundância local se quiser uma opção mais barata que não seja tão durável. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento no hello [visão geral de replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).

configuração de replicação de armazenamento de saudação tooedit:

1. Selecione o painel do cofre tooopen Olá cofre e a folha de configurações de saudação. Se hello **configurações** folha não abre, clique em **todas as configurações** no painel do cofre hello.
2. Em Olá **configurações** folha, clique em **Backup infraestrutura** > **configuração de Backup** tooopen Olá **deconfiguraçãodeBackup** folha. Em Olá **configuração de Backup** folha, escolha a opção de replicação de armazenamento Olá para seu cofre.

    ![Lista de cofres de backup](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Depois de escolher a opção de armazenamento de saudação para seu cofre, você está pronto tooassociate Olá VM com o cofre hello. associação de saudação toobegin, você deve descobrir e registrar Olá máquinas virtuais do Azure.

## <a name="3-software-package"></a>3. Pacote de software
### <a name="downloading-hello-software-package"></a>Baixar o pacote de software Olá
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Se você já tiver um cofre de serviços de recuperação aberta, vá toostep 3. Se você não tiver um aberto de Cofre de serviços de recuperação, mas está em Olá portal do Azure, no menu de Hub hello, clique em **procurar**.

   * Na lista de saudação de recursos, digite **dos serviços de recuperação**.
   * Como começar a digitar, lista Olá filtra com base em sua entrada. Quando vir a opção **Cofres de Serviços de Recuperação**, clique nela.

     ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     saudação de lista de cofres de serviços de recuperação é exibida.
   * Na lista de saudação de cofres de serviços de recuperação, selecione um cofre.

     painel do cofre selecionado Olá é aberto.

     ![Abrir a folha do cofre](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Olá **configurações** folha é aberto por padrão. Se ele estiver fechado, clique em **configurações** tooopen folha de configurações de saudação.

    ![Abrir a folha do cofre](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Clique em **Backup** Assistente de Introdução do tooopen hello.

    ![Guia de introdução ao backup](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    Em Olá **Introdução ao backup** folha que é aberta, **metas Backup** será selecionado automaticamente.

    ![Backup-metas-padrão-aberto](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. Em Olá **Backup meta** folha da saudação **onde sua carga de trabalho está executando** menu, selecione **local**.

    ![local e cargas de trabalho como metas](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    De saudação **o que fazer você deseja toobackup?** menu suspenso, cargas de trabalho Olá selecione você deseja tooprotect usando o servidor de Backup do Azure e, em seguida, clique em **Okey**.

    Olá **Introdução ao backup** Assistente comutadores Olá **preparar infraestrutura** tooback opção backup tooAzure de cargas de trabalho.

   > [!NOTE]
   > Se você desejar somente tooback backup de arquivos e pastas, é recomendável usando hello Azure Backup agent e seguindo a orientação Olá artigo Olá, [primeiro olhar: fazer backup de arquivos e pastas](backup-try-azure-backup-in-10-mins.md). Se você for tooprotect mais do que os arquivos e pastas ou você estiver planejando proteção de saudação tooexpand precisa no futuro hello, selecione essas cargas de trabalho.
   >
   >

    ![Guia de Introdução do assistente para alterar](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. Em Olá **preparar infraestrutura** folha que é aberta, clique em Olá **baixar** links para instalar o servidor de Backup do Azure e baixar credenciais do cofre. Você pode usar as credenciais do cofre Olá durante o registro do Cofre de serviços de recuperação de toohello do servidor de Backup do Azure. Olá links levam toohello onde hello pacote de software pode ser baixado do Centro de Download.

    ![Preparar a infraestrutura para o Servidor de Backup do Azure](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Selecione todos os arquivos de saudação e clique em **próximo**. Download que todos Olá arquivos vem da página de download do Microsoft Azure Backup Olá e coloque todos Olá arquivos no hello mesma pasta.

    ![Centro de download 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Como hello tamanho do download de todos os arquivos de saudação juntos > 3G, em um link de download de 10 Mbps pode levar até too60 minutos para Olá baixar toocomplete.

### <a name="extracting-hello-software-package"></a>Extrair o pacote de software Olá
Depois de baixar todos os arquivos de saudação, clique em **MicrosoftAzureBackupInstaller.exe**. Isso iniciará a saudação **Assistente de instalação do Microsoft Azure Backup** arquivos de instalação de saudação do tooextract tooa local especificado por você. Prossiga com o Assistente de saudação e clique em Olá **extrair** botão toobegin processo de extração de saudação.

> [!WARNING]
> Pelo menos 4GB de espaço livre é arquivos de instalação de saudação tooextract necessária.
>
>

![Assistente de Instalação do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Uma vez processo de extração de saudação completo, verificação Olá caixa toolaunch Olá recentemente extraído *setup.exe* toobegin instalando o servidor de Backup do Microsoft Azure e clique em Olá **concluir** botão.

### <a name="installing-hello-software-package"></a>Instalar o pacote de software Olá
1. Clique em **Backup do Microsoft Azure** toolaunch Assistente de instalação de saudação.

    ![Assistente de Instalação do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Na tela de boas-vindas hello, clique em Olá **próximo** botão. Isso leva você toohello *Prerequisite Checks* seção. Nessa tela, clique em **verificar** toodetermine se Olá pré-requisitos de hardware e software para o servidor de Backup do Azure foram atendidos. Se todos os pré-requisitos forem atendidos com êxito, você verá uma mensagem indicando que a máquina Olá atende aos requisitos de saudação. Clique em Olá **próximo** botão.

    ![Servidor de Backup do Azure - Boas-vindas e Verificação de pré-requisitos](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Servidor de Backup do Microsoft Azure requer o SQL Server Standard e pacote de instalação do servidor de Backup do Azure Olá é fornecido com binários do SQL Server apropriados Olá necessário. Ao iniciar com uma nova instalação do servidor de Backup do Azure, você deve escolher a opção de saudação **instalar nova instância do SQL Server com esta configuração** e clique em Olá **verificar e instalar** botão. Depois que os pré-requisitos de saudação são instalados com êxito, clique em **próximo**.

    ![Servidor de Backup do Azure - verificação do SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Se ocorrer uma falha com uma máquina de saudação toorestart recomendação, fazê-lo e clique em **verificar novamente**.

   > [!NOTE]
   > O Servidor de Backup do Azure não funcionará com uma instância remota do SQL Server. instância Hello está sendo usada pelo servidor de Backup do Azure precisa toobe local.
   >
   >
4. Forneça um local para instalação Olá dos arquivos do servidor de Backup do Microsoft Azure e clique em **próximo**.

    ![Pré-requisito 2 do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    local de rascunho Olá é um requisito para tooAzure de backup. Certifique-se de que o local de rascunho Olá é pelo menos 5% dos dados de saudação planejado toobe backup toohello nuvem. Para a proteção de disco separado de discos necessário toobe configurado após a conclusão da instalação de saudação. Para saber mais sobre pools de armazenamento, consulte [Configurar os pools de armazenamento e o armazenamento em disco](https://technet.microsoft.com/library/hh758075.aspx).
5. Forneça uma senha forte para as contas de usuário local restritas e clique em **Avançar**.

    ![Pré-requisito 2 do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Selecione se deseja toouse *Microsoft Update* toocheck para atualizações e clique em **próximo**.

   > [!NOTE]
   > É recomendável ter o Windows Update redirecionar tooMicrosoft atualização, que oferece segurança e atualizações importantes para o Windows e outros produtos como o servidor de Backup do Microsoft Azure.
   >
   >

    ![Pré-requisito 2 do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Saudação de revisão *resumo das configurações* e clique em **instalar**.

    ![Pré-requisito 2 do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. instalação de saudação acontece em fases. No primeiro Olá de fase Olá Microsoft Azure Recovery Services Agent está instalado no servidor de saudação. Assistente Olá também verifica a conectividade de Internet. Se a conectividade com a Internet está disponível pode continuar a instalação, caso contrário, você precisa tooprovide proxy detalhes tooconnect toohello da Internet.

    Olá próxima etapa é tooconfigure Olá agente de serviços de recuperação do Microsoft Azure. Como parte da configuração do hello, você terá tooprovide seus serviços de recuperação cofre credenciais tooregister Olá máquina toohello cofre. Você também irá fornecer um frase secreta tooencrypt/descriptografar Olá dados enviados entre o Azure e seus locais. Você pode gerar automaticamente uma senha ou fornecer sua própria senha mínima de 16 caracteres. Continue com o assistente Olá Olá agente foi configurado.

    ![Pré-requisito 2 do Servidor de Backup do Azure](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Após a conclusão com êxito do registro do servidor de Backup do Microsoft Azure hello, hello geral Assistente de instalação continuará toohello instalação e configuração do SQL Server e componentes de servidor de Backup do Azure hello. Após a conclusão do hello instalação de componentes do SQL Server, componentes de servidor de Backup do Azure Olá estão instalados.

    ![Servidor de Backup do Azure](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Quando tiver concluído a etapa de instalação hello, hello ícones de área de trabalho do produto terá sido criadas também. Basta clicar duas vezes o produto de Olá Olá ícone toolaunch.

### <a name="add-backup-storage"></a>Adicionar armazenamento de backup
primeira cópia de backup de saudação é mantida no armazenamento conectado toohello máquina do servidor de Backup do Azure. Para saber mais sobre a adição de discos, consulte [Configurar os pools de armazenamento e o armazenamento em disco](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Você precisa de armazenamento de backup de tooadd mesmo que você planeje toosend tooAzure de dados. Na arquitetura atual de saudação do servidor de Backup do Azure, o Cofre de Backup do Azure Olá contém Olá *segundo* cópia dos dados Olá enquanto o armazenamento local Olá contém a cópia de backup primeira (e obrigatório) hello.
>
>

## <a name="4-network-connectivity"></a>4. Conectividade de rede
Servidor de Backup do Azure requer o serviço de Backup do Azure toohello conectividade para Olá produto toowork com êxito. toovalidate tenha máquina Olá Olá conectividade tooAzure, use Olá ```Get-DPMCloudConnection``` cmdlet no console do PowerShell do Azure Backup Server hello. Se hello saída do cmdlet Olá é TRUE e conectividade existe, ou não há nenhuma conectividade.

Ao hello, simultaneamente, Olá assinatura do Azure precisa toobe em um estado íntegro. toofind o estado de saudação da assinatura e toomanage-lo, o log em toohello [portal assinatura](https://account.windowsazure.com/Subscriptions).

Quando você souber o estado de saudação do hello conectividade do Azure e do hello assinatura do Azure, você pode usar a tabela de saudação abaixo toofind out impacto Olá na funcionalidade de backup/restauração Olá oferecida.

| Estado de conectividade | Assinatura do Azure | Fazer backup tooAzure | Fazer backup toodisk | Restaurar do Azure | Restaurar do disco |
| --- | --- | --- | --- | --- | --- |
| Conectado |Ativo |Permitido |Permitido |Permitido |Permitido |
| Conectado |Expirado |Parada |Parada |Permitido |Permitido |
| Conectado |Provisionamento Cancelado |Parada |Parada |Parado e pontos de recuperação do Azure excluídos |Parada |
| Perda de conectividade > 15 dias |Ativo |Parada |Parada |Permitido |Permitido |
| Perda de conectividade > 15 dias |Expirado |Parada |Parada |Permitido |Permitido |
| Perda de conectividade > 15 dias |Provisionamento Cancelado |Parada |Parada |Parado e pontos de recuperação do Azure excluídos |Parada |

### <a name="recovering-from-loss-of-connectivity"></a>Recuperação de perda de conectividade
Se você tiver um firewall ou um proxy que está impedindo o acesso tooAzure, é necessário toowhitelist Olá endereços de domínio no perfil do firewall/proxy Olá a seguir:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Depois que tooAzure conectividade tiver sido restaurado toohello máquina de servidor de Backup do Azure, operações de saudação que podem ser executadas são determinadas pelo Olá estado da assinatura do Azure. tabela de saudação acima tem detalhes sobre operações de saudação permitidos depois que a máquina de saudação é "conectada".

### <a name="handling-subscription-states"></a>Tratando os estados de assinatura
É possível tootake uma assinatura do Azure a partir de um *expirado* ou *Deprovisioned* estado toohello *Active* estado. No entanto isso tem algumas implicações no comportamento de produto Olá ao estado de saudação não é *Active*:

* Um *Deprovisioned* assinatura perde a funcionalidade de período de saudação for desprovisionada. Na ativação *Active*, funcionalidade da saudação de produto de backup/restauração é reativada. Olá dados de backup em disco local Olá também podem ser recuperados se ele foi mantido com um período de retenção for grande o suficiente. No entanto, dados de backup de saudação no Azure são perdidos quando Olá entra em Olá *Deprovisioned* estado.
* Uma assinatura *Expirada* só perderá a funcionalidade até ficar *Ativa* novamente. Os backups agendados para o período de saudação Olá assinatura foi *expirado* não será executado.

## <a name="troubleshooting"></a>Solucionar problemas
Se o servidor do Microsoft Azure Backup falhar com erros durante a fase de instalação hello (ou backup ou restauração), consulte toothis [documento de códigos de erro](https://support.microsoft.com/kb/3041338) para obter mais informações.
Você também pode consultar muito[Backup do Azure relacionados perguntas frequentes](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Próximas etapas
Você pode obter informações detalhadas sobre [Preparando seu ambiente para o DPM](https://technet.microsoft.com/library/hh758176.aspx) no site da Microsoft TechNet hello. Ele também contém informações sobre as configurações com suporte, nas quais o Servidor de Backup do Azure pode ser implantado e usado.

Você pode usar esses toogain artigos uma compreensão mais profunda de proteção de cargas de trabalho usando o servidor de Backup do Microsoft Azure.

* [Backup do SQL Server](backup-azure-backup-sql.md)
* [Backup do servidor do SharePoint](backup-azure-backup-sharepoint.md)
* [Backup do servidor alternativo](backup-azure-alternate-dpm-server.md)
