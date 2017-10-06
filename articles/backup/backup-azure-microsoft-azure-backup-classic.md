---
title: "aaaUse Azure Backup Server tooback o portal clássico do tooAzure de cargas de trabalho | Microsoft Docs"
description: "Verifique se o que seu ambiente está preparado adequadamente tooback cargas de trabalho usando o servidor de Backup do Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: servidor de backup do Azure; cofre de backup
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparando tooback cargas de trabalho usando o servidor de Backup do Azure
> [!div class="op_single_selector"]
> * [Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Servidor de Backup do Azure (clássico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clássico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artigo é sobre como preparar seu tooback ambiente cargas de trabalho usando o servidor de Backup do Azure. Com o Servidor de Backup do Azure, você pode proteger cargas de trabalho de aplicativo como VMs do Hyper-V, o Microsoft SQL Server, o SharePoint Server, o Microsoft Exchange e os clientes de um único console.

> [!WARNING]
> Servidor de Backup do Azure herda a funcionalidade de saudação do Data Protection Manager (DPM) para backup de cargas de trabalho. Você encontrará ponteiros tooDPM documentação para alguns desses recursos. No entanto, o Servidor de Backup do Azure não oferece proteção em fita ou se integra ao System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Computador do Windows Server
![etapa1](./media/backup-azure-microsoft-azure-backup/step1.png)

a primeira etapa Olá para colocar hello Azure Backup Server em execução é toohave uma máquina Windows Server.

| Local | Requisitos mínimos | Instruções adicionais |
| --- | --- | --- |
| As tabelas |Máquina virtual de IaaS do Azure<br><br>A2 Standard: 2 núcleos, 3,5 GB de RAM |Você pode começar com uma única imagem da galeria do Windows Server 2012 R2 Datacenter. [Protegendo cargas de trabalho IaaS usando o Servidor de Backup do Azure (DPM)](https://technet.microsoft.com/library/jj852163.aspx) apresenta várias nuances. Certifique-se de que você leia o artigo de saudação completamente antes de implantar a máquina de saudação. |
| Configuração local |VM do Hyper-V,<br> VM do VMWare<br> ou um host físico<br><br>2 núcleos e 4 GB de RAM |Você pode eliminar duplicação de armazenamento do DPM hello usando eliminação de duplicação do Windows Server. Saiba mais sobre como o [DPM e a eliminação de duplicação](https://technet.microsoft.com/library/dn891438.aspx) funcionam juntos quando implantados em VMs do Hyper-V. |

> [!NOTE]
> É recomendável que o Servidor de Backup do Azure esteja instalado em um computador com Windows Server 2012 R2 Datacenter. Muitos dos pré-requisitos Olá automaticamente são abordados com a versão mais recente de saudação do sistema de operacional do Windows hello.
>
>

Se você planejar toojoin domínio de tooa de servidor de Backup do Azure, é recomendável ingressar o servidor físico hello ou máquina virtual toohello domínio antes de instalar o software de servidor de Backup do Azure hello. Mover um servidor de Backup do Azure tooa novo domínio, após a implantação, é *não tem suporte*.

## <a name="2-backup-vault"></a>2. Cofre de backup
![etapa2](./media/backup-azure-microsoft-azure-backup/step2.png)

Se você envia dados de backup tooAzure ou mantê-lo localmente, hello Azure Backup Server deve ser registrado tooa cofre. Se você for um novo usuário de Backup do Azure e deseja toouse servidor de Backup do Azure, consulte hello Azure portal versão deste artigo - [preparar tooback cargas de trabalho usando o servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>



## <a name="3-software-package"></a>3. Pacote de software
![etapa3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Baixar o pacote de software Olá
Credenciais toovault semelhante, você pode baixar o Microsoft Azure Backup para cargas de trabalho de aplicativo da saudação **página início rápido** saudação do Cofre de backup.

1. Clique em **para cargas de trabalho aplicativos (disco tooDisk tooCloud)**. Isso o levará página do Centro de Download toohello de onde o pacote de software Olá pode ser baixado.

    ![Tela de boas-vindas do Backup do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Clique em **Download**.

    ![Centro de download 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Selecione todos os arquivos de saudação e clique em **próximo**. Download que todos Olá arquivos vem da página de download do Microsoft Azure Backup Olá e coloque todos Olá arquivos no hello mesma pasta.
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
2. Na tela de boas-vindas hello, clique em Olá **próximo** botão. Isso leva você toohello *Prerequisite Checks* seção. Nessa tela, clique em Olá **verificar** botão toodetermine se Olá pré-requisitos de hardware e software para o servidor de Backup do Azure foram atendidos. Se todos Olá são os pré-requisitos foram atendidos com êxito, você verá uma mensagem indicando que a máquina Olá atende aos requisitos de saudação. Clique em Olá **próximo** botão.

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

    Olá próxima etapa é tooconfigure Olá agente de serviços de recuperação do Microsoft Azure. Como parte da configuração do hello, você terá tooprovide seu Olá cofre credenciais tooregister Olá máquina toohello Cofre de backup. Você também irá fornecer um frase secreta tooencrypt/descriptografar Olá dados enviados entre o Azure e seus locais. Você pode gerar automaticamente uma senha ou fornecer sua própria senha mínima de 16 caracteres. Continue com o assistente Olá Olá agente foi configurado.

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
![etapa4](./media/backup-azure-microsoft-azure-backup/step4.png)

Servidor de Backup do Azure requer o serviço de Backup do Azure toohello conectividade para Olá produto toowork com êxito. toovalidate tenha máquina Olá Olá conectividade tooAzure, use Olá ```Get-DPMCloudConnection``` commandlet no console do PowerShell do Azure Backup Server hello. Se hello saída Olá commandlet é verdadeiro e conectividade de, ou não há nenhuma conectividade.

Ao hello, simultaneamente, Olá assinatura do Azure precisa toobe em um estado íntegro. toofind o estado de saudação da assinatura e toomanage-lo, o log em toohello [portal assinatura](https://account.windowsazure.com/Subscriptions).

Quando você souber o estado de saudação do hello conectividade do Azure e do hello assinatura do Azure, você pode usar a tabela de saudação abaixo toofind out impacto Olá na funcionalidade de backup/restauração Olá oferecida.

| Estado de conectividade | Assinatura do Azure | Backup tooAzure | Backup toodisk | Restaurar do Azure | Restaurar do disco |
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
