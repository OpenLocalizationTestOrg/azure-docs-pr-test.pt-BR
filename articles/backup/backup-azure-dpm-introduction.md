---
title: aaaUse DPM tooback o portal de tooAzure de cargas de trabalho | Microsoft Docs
description: "Toobacking uma introdução a servidores DPM usando o serviço de Backup do Azure Olá"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: "Gerenciador de proteção de dados do System Center, gerenciador de proteção de dados, backup do dpm"
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparando tooback backup tooAzure de cargas de trabalho com o DPM
> [!div class="op_single_selector"]
> * [Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Servidor de Backup do Azure (clássico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clássico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artigo fornece uma tooprotect de Backup do Microsoft Azure Introdução toousing suas cargas de trabalho e servidores do System Center Data Protection Manager (DPM). Lendo-o, você entenderá:

* Como funciona o backup do servidor DPM do Azure
* Olá pré-requisitos tooachieve uma experiência positiva de backup
* Olá erros comuns e como toodeal com eles
* Cenários com suporte

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo fornece informações hello e procedimentos para restaurar as VMs implantadas usando o modelo do Gerenciador de recursos de saudação.
>
>

O System Center DPM faz backup dos dados de arquivos e aplicativos. Dados de backup tooDPM podem ser armazenados em fita, disco ou backup tooAzure com o Microsoft Azure Backup. O DPM interage com o Backup do Azure da seguinte maneira:

* **DPM implantado como uma máquina de virtual do servidor ou local física** — se o DPM é implantado como um servidor físico ou como uma máquina virtual de Hyper-V de local você pode fazer backup de dados tooa serviços de recuperação de cofre, além disso, toodisk e backup em fita.
* **DPM implantado como máquina virtual do Azure** — No System Center 2012 R2 com atualização 3, o DPM pode ser implantado como máquina virtual do Azure. Se o DPM é implantado como uma máquina virtual do Azure, que você pode fazer backup de dados tooAzure discos anexados a máquina de virtual do Azure do DPM toohello ou você pode descarregar o armazenamento de dados Olá fazendo backup tooa que Cofre de serviços de recuperação.

## <a name="why-backup-from-dpm-tooazure"></a>Por que fazer backup do DPM tooAzure?
benefícios de negócios de saudação do usando o Backup do Azure para fazer backup de servidores DPM incluem:

* Para a implantação do DPM no local, você pode usar o Azure como tootape de implantação um termo de toolong alternativo.
* Para implantações do DPM no Azure, o Backup do Azure permite armazenamento toooffload de saudação do disco do Azure, que você tooscale backup armazenando dados mais antigos no cofre de serviços de recuperação e novos dados no disco.

## <a name="prerequisites"></a>Pré-requisitos
Prepare o Azure Backup tooback backup de dados do DPM da seguinte maneira:

1. **Criar um cofre dos Serviços de Recuperação** – crie um cofre no portal do Azure.
2. **Baixe as credenciais do cofre** — baixar credenciais Olá que você usar tooregister Olá DPM server tooRecovery Cofre de serviços.
3. **Instalar hello Azure Backup Agent** — do Backup do Azure, instalar o agente de saudação em cada servidor DPM.
4. **Registrar o servidor de saudação** — o Cofre de serviços do registro Olá DPM server tooRecovery.

### <a name="1-create-a-recovery-services-vault"></a>1. Criar um cofre dos Serviços de Recuperação
Cofre de serviços de toocreate uma recuperação:

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **procurar** e, na lista de saudação de recursos, digite **dos serviços de recuperação**. Como começar a digitar, lista Olá filtra com base em sua entrada. Clique em **Cofre dos Serviços de Recuperação**.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    saudação de lista de cofres de serviços de recuperação é exibida.
3. Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.

    ![Criar Cofre de Serviços de Recuperação - etapa 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Para **nome**, insira um cofre de saudação tooidentify nome amigável. nome da saudação precisa toobe exclusivo Olá assinatura do Azure. Digite um nome que contenha de 2 a 50 caracteres. Ele deve começar com uma letra e pode conter apenas letras, números e hifens.
5. Clique em **assinatura** toosee Olá lista de assinaturas. Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura. Haverá várias opções somente se sua conta organizacional estiver associada a várias assinaturas do Azure.
6. Clique em **grupo de recursos** toosee Olá a lista de grupos de recursos disponíveis, ou clique em **novo** toocreate um novo grupo de recursos. Para obter informações completas sobre Grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Clique em **local** tooselect Olá região para o cofre hello.
8. Clique em **Criar**. Pode levar algum tempo para Olá toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status de saudação na área superior direito de saudação no portal de saudação.
   Depois de criar seu cofre, ele é aberto no portal de saudação.

### <a name="set-storage-replication"></a>Definir replicação de armazenamento
opção de replicação de armazenamento Olá permite toochoose entre o armazenamento com redundância geográfica e o armazenamento redundante localmente. Por padrão, seu cofre tem armazenamento com redundância geográfica. Deixe Olá opção set toogeo redundantes armazenamento se esta for sua principal de backup. Escolha o armazenamento com redundância local se quiser uma opção mais barata que não seja tão durável. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento no hello [visão geral de replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).

configuração de replicação de armazenamento de saudação tooedit:

1. Selecione o painel do cofre tooopen Olá cofre e a folha de configurações de saudação. Se hello **configurações** folha não abre, clique em **todas as configurações** no painel do cofre hello.
2. Em Olá **configurações** folha, clique em **Backup infraestrutura** > **configuração de Backup** tooopen Olá **deconfiguraçãodeBackup** folha. Em Olá **configuração de Backup** folha, escolha a opção de replicação de armazenamento Olá para seu cofre.

    ![Lista de cofres de backup](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Depois de escolher a opção de armazenamento de saudação para seu cofre, você está pronto tooassociate Olá VM com o cofre hello. associação de saudação toobegin, você deve descobrir e registrar Olá máquinas virtuais do Azure.

### <a name="2-download-vault-credentials"></a>2. Baixar as credenciais do cofre
o arquivo de credenciais de cofre Olá é um certificado gerado pelo portal Olá para cada Cofre de backup. portal de saudação carrega toohello chave pública Olá Access Control Service (ACS). chave privada de saudação do certificado de saudação é feita usuário toohello disponível como parte do fluxo de trabalho de saudação que é fornecido como uma entrada no fluxo de trabalho de registro de máquina hello. Isso autentica Olá máquina toosend dados de backup tooan identificado cofre em Olá serviço Backup do Azure.

credencial do cofre Olá é usado somente durante o fluxo de trabalho de registro de saudação. É tooensure de responsabilidade do usuário Olá que Olá as credenciais do cofre arquivo não seja comprometido. Se ela estiver em mãos Olá de qualquer usuário autorizado, o arquivo de credenciais de cofre Olá pode ser usado tooregister outras máquinas Olá mesmo cofre. No entanto, como dados de backup Olá são criptografados usando uma frase secreta que pertence o cliente toohello, dados de backup existentes não podem ser comprometidos. toomitigate essa preocupação, as credenciais do cofre são definidas tooexpire em 48hrs. Você pode baixar as credenciais do Cofre de serviços de recuperação de uma saudação qualquer número de vezes – mas somente hello mais recente cofre credencial arquivo aplicável durante o fluxo de trabalho do hello registro.

arquivo de credencial de cofre Olá é baixado por meio de um canal seguro de saudação portal do Azure. Olá serviço Backup do Azure não tem conhecimento da chave privada de saudação do certificado de saudação e chave privada Olá não é mantido no portal de saudação ou serviço hello. Use Olá seguindo as etapas toodownload Olá cofre credencial arquivo tooa máquina local.

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Abra Serviços de recuperação cofre toowhich toowhich tooregister DPM máquina.
3. A folha de configurações abre por padrão. Se ele estiver fechado, clique em **configurações** na folha de configurações do Cofre Painel tooopen hello. Na folha Configurações, clique em **Propriedades**.

    ![Abrir a folha do cofre](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Na página de propriedades de saudação, clique em **baixar** em **Backup credenciais**. portal de Hello gera o arquivo de credencial do cofre hello, que fica disponível para download.

    ![Baixar](./media/backup-azure-dpm-introduction/vault-credentials.png)

portal de saudação irá gerar uma credencial do cofre usando uma combinação de nome do cofre hello e hello data atual. Clique em **salvar** toodownload Olá cofre credenciais toohello da conta local baixa a pasta ou selecione Salvar como do hello salvar menu toospecify um local para as credenciais do cofre hello. Demorará tooa minuto para Olá toobe de arquivo gerado.

### <a name="note"></a>Observação
* Certifique-se de que esse arquivo de credenciais de cofre Olá é salvo em um local que pode ser acessado em seu computador. Se ele estiver armazenado em um compartilhamento de arquivo/SMB, verifique as permissões de acesso de saudação.
* o arquivo de credenciais de cofre Olá é usado somente durante o fluxo de trabalho de registro de saudação.
* o arquivo de credenciais de cofre Olá expira após 48hrs e pode ser baixado do portal de saudação.

### <a name="3-install-backup-agent"></a>3. Instalar o Backup Agent
Depois de criar o Cofre de Backup do Azure hello, um agente deve ser instalado em cada uma de suas máquinas do Windows (Windows Server, Windows client, servidor do System Center Data Protection Manager ou máquina do servidor de Backup do Azure) que permite fazer backup de dados e aplicativos tooAzure.

1. Abra Serviços de recuperação cofre toowhich toowhich tooregister DPM máquina.
2. A folha de configurações abre por padrão. Se ele estiver fechado, clique em **configurações** tooopen folha de configurações de saudação. Na folha Configurações, clique em **Propriedades**.

    ![Abrir a folha do cofre](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Na página de configurações de saudação, clique em **baixar** em **Azure Backup Agent**.

    ![Baixar](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Depois que o agente de saudação é baixado, clique duas vezes em instalação de saudação toolaunch MARSAgentInstaller.exe do agente de Backup do Azure hello. Escolha pasta de instalação hello e necessárias para o agente de saudação de pasta de rascunho. local do cache Olá especificado deve ter espaço livre, que é pelo menos 5% dos dados de backup de saudação.
4. Se você usar um toohello de tooconnect de servidor proxy internet, Olá **configuração de Proxy** tela, insira os detalhes do servidor proxy hello. Se você usar um proxy autenticado, insira os detalhes de nome e a senha do usuário Olá nesta tela.
5. Agente de Backup do Azure Olá realizou .NET Framework 4.5 e o Windows PowerShell (se já não estiver disponível) toocomplete Olá instalação.
6. Depois de instalar o agente hello, **fechar** janela hello.

   ![Feche](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. muito**Olá registrar servidor DPM** toohello cofre, em Olá **gerenciamento** guia, clique em **Online**. Em seguida, selecione **Registrar**. Ele será aberto Olá registrar o Assistente de instalação.
8. Se você usar um toohello de tooconnect de servidor proxy internet, Olá **configuração de Proxy** tela, insira os detalhes do servidor proxy hello. Se você usar um proxy autenticado, insira os detalhes de nome e a senha do usuário Olá nesta tela.

    ![Configuração de Proxy](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Na tela de credenciais do cofre hello, procure tooand Olá selecione cofre arquivo de credenciais que foi baixado anteriormente.

    ![Credenciais do cofre](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    o arquivo de credenciais de cofre Olá é válido somente para 48 horas (depois que ele é baixado do portal de saudação). Se você encontrar qualquer erro nesta tela (por exemplo, "Cofre de credenciais de arquivo fornecido expirou"), logon toohello arquivos do Azure portal e baixe Olá cofre credenciais novamente.

    Certifique-se de que esse arquivo de credenciais de cofre hello está disponível em um local que pode ser acessado pelo aplicativo de instalação hello. Se você encontrar erros relacionados de acesso, credenciais do cofre Olá cópia arquivo local temporário de tooa nesta máquina e repita a operação de saudação.

    Se você encontrar um erro de credencial de Cofre inválido (por exemplo, "inválido das credenciais do cofre fornecido") arquivo hello está corrompido ou não ter Olá credenciais mais recentes associadas ao serviço de recuperação de saudação. Repita a operação Olá após o download de um novo arquivo de credencial do cofre no portal de saudação. Esse erro é geralmente visto se usuário Olá clicar em Olá **credencial do cofre Download** opção no portal do Azure, em sucessão rápida de saudação. Nesse caso, somente Olá segundo cofre credencial arquivo é válido.
10. uso de saudação toocontrol de largura de banda de rede durante o trabalho e horas não úteis, Olá **configuração limitação** tela, você pode definir limites de uso de largura de banda hello e definir o trabalho de saudação e folga horas.

    ![Configuração de Limitação](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. Em Olá **configuração de recuperação da pasta** tela, navegue para a pasta Olá onde os arquivos de saudação baixados do Azure será preparada temporariamente.

    ![Configuração de Pasta de Recuperação](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. Em Olá **configuração de criptografia** tela, você pode gerar uma senha ou forneça uma senha (mínimo de 16 caracteres). Lembre-se toosave Olá senha em um local seguro.

    ![Criptografia](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Se hello senha for perdida ou esquecida; Microsoft não pode ajudar na recuperação de dados de backup hello. usuário final de saudação possui Olá senha de criptografia e a Microsoft não tem visibilidade Olá senha usada pelo usuário final de saudação. Salve o arquivo de saudação em um local seguro conforme necessário durante uma operação de recuperação.
    >
    >
13. Depois de clicar em Olá **registrar** botão, hello máquina é registrada com êxito toohello cofre e você agora está pronto toostart backup tooMicrosoft do Azure.
14. Ao usar o Data Protection Manager, você pode modificar configurações de saudação especificadas durante o fluxo de trabalho do hello registro clicando Olá **configurar** opção selecionando **Online** em Olá  **Gerenciamento** guia.

## <a name="requirements-and-limitations"></a>Requisitos (e limitações)
* O DPM pode ser executado como servidor físico ou máquina virtual Hyper-V instalado no System Center 2012 SP1 ou System Center 2012 R2. Também pode ser executado como máquina virtual do Azure em execução no System Center 2012 R2 com pelo menos Pacote cumulativo de atualizações 3 do DPM 2012 R2 ou máquina virtual do Windows em VMWare em execução no System Center 2012 R2 com pelo menos Pacote cumulativo de atualizações 5.
* Se você estiver executando o DPM com o System Center 2012 SP1, instale o Rollup de atualização 2 do System Center Data Protection Manager SP1. Isso é necessário antes de instalar o hello Azure Backup Agent.
* servidor DPM Olá deve ter o Windows PowerShell e .net Framework 4.5 instalado.
* O DPM pode fazer a maioria das cargas de trabalho tooAzure Backup. Para obter uma lista completa do que é compatível, consulte hello Azure Backup oferece suporte a itens abaixo.
* Os dados armazenados no Azure Backup não podem ser recuperados com a opção de "Copiar tootape" hello.
* Você precisará de uma conta do Azure com recurso de Backup do Azure Olá habilitado. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Leia sobre os [preços do Backup do Azure](https://azure.microsoft.com/pricing/details/backup/).
* Usando o Backup do Azure requer toobe do hello Azure Backup Agent instalado nos servidores de saudação que desejar tooback. Cada servidor deve ter pelo menos 5% do tamanho de saudação do dados Olá que está sendo feitos, disponível como livre de armazenamento local. Por exemplo, fazendo backup de 100 GB de dados requer um mínimo de 5 GB de espaço livre no local de rascunho hello.
* Os dados serão armazenados no hello armazenamento de cofre do Azure. Há um valor de toohello de limite de dados, que você pode fazer backup de Cofre de Backup do Azure tooan mas o tamanho de saudação de uma fonte de dados (por exemplo uma máquina virtual ou um banco de dados) não deve exceder 54400 GB.

Esses tipos de arquivo têm suporte para backup tooAzure:

* Criptografados (apenas backups completos)
* Compactados (suporte para backups incrementais)
* Esparsos (suporte para backups incrementais)
* Compactados e esparsos (tratados como esparsos)

E os seguintes não têm suporte:

* Não há suporte para servidores em sistemas de arquivo que diferenciam maiúsculas de minúsculas.
* Links físicos (ignorados)
* Pontos de nova análise (ignorados)
* Criptografados e compactados (ignorados)
* Criptografados e esparsos (ignorados)
* Fluxo compactado
* Fluxo esparso

> [!NOTE]
> No System Center 2012 DPM com SP1 em diante, você pode fazer backup de cargas de trabalho protegidas pelo DPM tooAzure usando o Microsoft Azure Backup.
>
>
