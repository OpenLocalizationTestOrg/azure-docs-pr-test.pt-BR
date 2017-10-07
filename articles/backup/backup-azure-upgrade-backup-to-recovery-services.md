---
title: "aaaUpgrade um cofre de serviços de recuperação de tooa de Cofre de Backup (visualização) | Microsoft Docs"
description: "Instruções e tooupgrade de informações de suporte do Azure Backup cofre tooa Cofre de serviços de recuperação."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Atualizar um cofre de serviços de recuperação de tooa de Cofre de Backup

Este artigo explica como tooupgrade um cofre de Backup dos serviços de recuperação de tooa cofre. processo de atualização de saudação não afeta todos os trabalhos de backup em execução, e não há dados de backup serão perdidos. Olá primário motivos tooupgrade um tooa de Cofre de Backup Cofre de serviços de recuperação:
- Todos os recursos de um cofre de Backup são mantidos em um cofre de Serviços de Recuperação.
- Os cofres dos Serviços de Recuperação têm mais recursos que os cofres do Backup, incluindo: melhor segurança, monitoramento integrado, restaurações mais rápidas e restaurações no nível do item.
- Gerencie itens de backup em um portal aprimorado e simplificado.
- Novos recursos se aplicam somente a tooRecovery cofres de serviços.

## <a name="impact-toooperations-during-upgrade"></a>Impacto toooperations durante a atualização

Ao atualizar um cofre de serviços de recuperação de tooa de Cofre de Backup, há nenhum impacto de operações de plano de dados tooyour. Todos os trabalhos de backup continuam como normal e quaisquer trabalhos de restauração ativos continuam sem interrupção. Durante a atualização de hello, operações de gerenciamento incorrer em um curto tempo de inatividade, e você não pode proteger novos itens ou criar trabalhos de backups de ad hoc. Trabalhos de restauração para VMs de IaaS não são executados durante a atualização de saudação. Olá cofre atualização leva menos de uma hora toocomplete. Quando concluído, um cofre de serviços de recuperação substitui o Cofre de Backup hello.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Alterações tooyour automação e a ferramenta depois da atualização

Ao preparar sua infraestrutura para atualização de cofre hello, você deve atualizar sua automação existentes ou ferramentas tooensure que ele continua toowork após a atualização de saudação.
Consulte referências de cmdlets do PowerShell Olá Olá [modelo de implantação do Service Manager](backup-client-automation-classic.md) e hello [modelo de implantação do Gerenciador de recursos](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Antes de atualizar

Verifique o seguinte Olá emite antes da atualização os cofres de Backup tooRecovery cofres de serviço.

- **Versão mínima do agente**: tooupgrade seu cofre, certifique-se de saudação Microsoft Azure Recovery Services (MARS) agent é pelo menos versão 2.0.9070.0. Se o agente de MARS Olá for anterior à 2.0.9070.0, atualize o agente de saudação antes de iniciar o processo de atualização de saudação.
- **Modelo de cobrança com base em instância**: cofres de serviços de recuperação suportam apenas o modelo de cobrança com base em instância hello. Se você tiver um cofre de backup que está usando hello mais antigos com base em armazenamento modelo de cobrança, converta o modelo de cobrança Olá durante a atualização.
- **Nenhuma operação de configuração de backup contínuo**: durante a atualização, o plano de gerenciamento de toohello de acesso é restrito. Conclua todas as ações do plano de gerenciamento e, em seguida, inicie a atualização de saudação.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Usando os cofres de tooupgrade de scripts do PowerShell

Você pode usar o PowerShell scripts tooupgrade cofres de serviços tooRecovery os cofres de Backup. Verifique se você tiver Olá necessário atualização do PowerShell componentes tootrigger Olá cofre. Scripts do PowerShell para os cofres de Backup não funcionam para cofres dos Serviços de Recuperação. Prepare o ambiente de cofres de saudação tooupgrade:

1. Instalar ou atualizar [tooversion Windows Management Framework (WMF) 5](https://www.microsoft.com/download/details.aspx?id=50395) ou superior.
2. [Instale o MSI do Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Baixar Olá [script do PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade os cofres.

### <a name="run-hello-powershell-script"></a>Executar script do PowerShell Olá

Use os cofres de Olá tooupgrade de script a seguir. Olá, script de exemplo a seguir tem explicações de parâmetros de saudação.

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**SubscriptionID** -Olá número de ID de assinatura de cofre Olá que está sendo atualizado.<br/>
**VaultName** - Olá nome do Cofre de Backup Olá que está sendo atualizado.<br/>
**Local** -local do cofre hello está sendo atualizado.<br/>
**ResourceType** – use BackupVault.<br/>
**TargetResourceGroupName** - desde que você estiver atualizando Olá cofre tooa com base no Gerenciador de recursos de implantação, especifique um grupo de recursos. Você pode usar um Grupo de Recursos existente ou criar um fornecendo um novo nome. Se você digitar incorretamente o nome de saudação de um grupo de recursos, você pode criar um novo grupo de recursos. toolearn mais sobre grupos de recursos, leia este [visão geral sobre grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Nomes de Grupo de Recursos têm restrições. Orientação de saudação toofollow se; Falha toodo pode gerar toofail de atualizações do cofre.
>
>

Olá trecho de código a seguir é um exemplo do que o comando do PowerShell deve parecer com:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

Você também pode executar o script hello sem parâmetros, e você será solicitado tooprovide entradas para todos os parâmetros necessários.

Olá script do PowerShell solicitará que você tooenter suas credenciais. Insira suas credenciais duas vezes: uma vez para a conta do Service Manager hello e uma segunda vez para Olá conta do Gerenciador de recursos.

### <a name="pre-requisites-checking"></a>Verificação de pré-requisitos
Depois de inserir suas credenciais do Azure, o Azure verifica que seu ambiente atenda Olá pré-requisitos a seguir:

- **Versão mínima do agente** -Backup atualizando cofres tooRecovery serviços cofres requer Olá MARS agente toobe pelo menos versão 2.0.9070. Se você tiver itens registrados anteriores 2.0.9070 tooa Cofre de Backup com um agente, falha na verificação de pré-requisito hello. Se a verificação de pré-requisitos Olá falhar, atualizar agente hello e tente Cofre de saudação tooupgrade novamente. Você pode baixar a versão mais recente de saudação do agente de saudação do [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Tarefas de configuração em andamento**: se alguém está configurando o trabalho para um cofre de Backup definido toobe atualizado, ou o registro de um item, Olá falha de verificação de pré-requisitos. Concluir configuração hello, ou concluir o registro de item de saudação e inicie o processo de atualização de cofre hello.
- **Modelo de cobrança com base em armazenamento**: serviços de recuperação cofres suporte Olá instância com base em modelo de cobrança. Se você executar uma atualização de cofre Olá em um cofre de Backup que usa Olá modelo de cobrança com base em armazenamento, são solicitada tooupgrade o modelo de cobrança junto com hello cofre. Caso contrário, você pode atualizar o modelo de cobrança pela primeira vez, e, em seguida, executar a atualização de Cofre de saudação.
- Identifica um grupo de recursos para o Cofre de serviços de recuperação de saudação. Olá de tootake proveito dos recursos de implantação do Gerenciador de recursos, você deve colocar um cofre de serviços de recuperação em um grupo de recursos. Se você não souber qual toouse do grupo de recursos, fornecer que um nome e uma saudação o processo de atualização cria Olá grupo de recursos para você. o processo de atualização Olá também associa cofre Olá com hello novo grupo de recursos.

Depois que o processo de atualização de saudação conclui a verificação de pré-requisitos do hello, o processo de Olá solicita a você toostart Olá cofre atualização. Depois de confirmar, o processo de atualização Olá geralmente leva em torno de toocomplete de 15 a 20 minutos, dependendo do tamanho de saudação do seu cofre. Se você tiver um grande cofre, a atualização pode demorar até too90 minutos.

## <a name="managing-your-recovery-services-vaults"></a>Gerenciando seus cofres dos Serviços de Recuperação

Olá telas a seguir mostra um novo cofre de serviços de recuperação, atualizado do Cofre de Backup, em Olá portal do Azure. Olá primeira tela mostra o painel Cofre Olá que exibe as principais entidades para o cofre hello.

![exemplo de cofre dos Serviços de Recuperação atualizado de um cofre de Backup](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

segunda tela do Hello mostra links de ajuda Olá toohelp disponível começar a usar os serviços de recuperação de saudação cofre.

![links de folha de início rápido de saudação da Ajuda](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Etapas de pós-atualização
O cofre do Serviços de Recuperação dá suporte à especificação de informações de fuso horário na política de backup. Depois que o cofre é atualizado com êxito, vá tooBackup políticas no menu de configurações do cofre e atualizar informações de fuso horário de saudação para cada uma das políticas de saudação configuradas no cofre hello. Esta tela mostra já o tempo de agendamento de backup de saudação especificado por fuso horário local usado quando você criou a política. 

## <a name="enhanced-security"></a>Segurança aprimorada

Quando um cofre de Backup é atualizado o Cofre de serviços de recuperação de tooa, configurações de segurança de saudação para que os estão ativadas automaticamente. Quando as configurações de segurança Olá estão em determinadas operações como excluir backups, ou alterar uma senha exigem um [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PIN. Para obter mais informações sobre segurança Olá avançado, consulte o artigo Olá [tooprotect backups de híbrida de recursos de segurança](backup-azure-security-feature.md). 

Quando a segurança de saudação aprimorada estiver ativada, os dados são retidos backup too14 dias após a exclusão de informações de ponto de recuperação de saudação do cofre hello. Os clientes são cobrados pelo armazenamento de dados de segurança. Retenção de dados de segurança se aplica a pontos na toorecovery para o agente de Backup do Azure hello, servidor de Backup do Azure e System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Reunir dados no cofre

Quando você atualizar o Cofre de serviços de recuperação de tooa, configurar relatórios de Backup do Windows Azure (para as VMs de IaaS e Microsoft Azure Recovery Services (MARS)) e usar relatórios do Power BI tooaccess hello. Para obter informações adicionais sobre a coleta de dados, consulte o artigo Olá [configurar o Backup do Azure relatórios](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Plano de atualização de saudação afeta meus backups contínuos?**</br>
Não. Os backups em andamento continuam sem interrupções durante e após a atualização.

**Se eu não planeja atualizar em breve, o que acontece cofres toomy?**</br>
Desde que todos os novos recursos se apliquem a apenas os cofres de serviços tooRecovery, solicitamos que você tooupgrade os cofres. Microsoft eventualmente removerá o portal clássico do hello. Começando em 1 de setembro de 2017, Microsoft começará a atualização automática cofres de serviços tooRecovery os cofres de backup. Por 1 de novembro de 2017, Microsoft concluirá o processo de atualização de saudação. Seu cofre poderá ser automaticamente atualizado a qualquer momento em setembro ou outubro. A Microsoft recomenda que você atualize seu cofre assim que possível.

**O que esta atualização significa para as minhas ferramentas existentes?**</br>
Atualize seu modelo de implantação do Gerenciador de recursos de toohello ferramentas. Serviços de recuperação cofres foram criados para usam no modelo de implantação do Gerenciador de recursos de saudação. Planejamento para o modelo de implantação do Gerenciador de recursos de saudação e estatísticas de diferença de saudação em seus cofres são importante. 

**Durante a atualização de hello, há muito tempo de inatividade?**</br>
Depende do número de saudação de recursos que estão sendo atualizados. Para implantações menores (algumas dezenas de instâncias protegidas), atualização inteira Olá deve levar menos de 20 minutos. Para implantações maiores, deve levar um máximo de uma hora.

**Posso reverter após a atualização?**</br>
Não. A reversão não tem suporte depois recursos Olá foi atualizados com êxito.

**Pode validar o toosee minha assinatura ou recursos se eles são capazes de atualização?**</br>
Sim. a primeira etapa Olá na atualização valida que os recursos de saudação são capazes de atualização. No caso de falha de validação de saudação de pré-requisitos, você receberá mensagens para todos os motivos Olá Olá atualização não pode ser concluída.

**Quais permissões devo tootrigger cofre atualização?**</br>
Olá tooperform cofre a atualização, você deve ser adicionado como coadministrador para assinatura Olá Olá portal clássico do Azure. Isso é necessário mesmo se você já estiver listado como proprietário no hello portal do Azure. Tente tooadd coadministrador da assinatura de saudação no Azure toofind portal clássico out se você estiver coadministrador da assinatura de saudação. Se você não for capaz de tooadd um coadministrador, contate um administrador de serviço ou coadministrador para assinatura hello, que pode adicioná-lo como um coadministrador.

**Posso atualizar meu cofre de Backup baseado em CSP?**</br>
Não. No momento não é possível atualizar os cofres de backup baseados em CSP. Adicionaremos suporte para atualização cofres de Backup baseado no CSP em versões de Avançar hello.

**Posso exibir meu cofre clássico após a atualização?**</br>
Não. Você não pode exibir nem gerenciar o cofre clássico pós-atualização. Você só será capaz de toouse Olá novo portal do Azure para todas as ações de gerenciamento no cofre de saudação.

**Falha na atualização do meu, mas a máquina Olá mantidos agente Olá necessidade de atualizar, não existe mais. O que devo fazer nesse caso?**</br>
Se você precisar de armazenamento de saudação toouse, Olá backups do computador para retenção de longo prazo, em seguida, não será capaz de tooupgrade Cofre de saudação. Nas versões futuras, adicionaremos suporte para atualizar esse cofre.
Se você não precisa toostore backups de saudação dessa máquina mais, então, cancelar o registro neste computador usando o cofre hello e repita a atualização de saudação.

**Por que não consigo ver informações dos trabalhos Olá para meus recursos do local após a atualização**</br>
Monitoramento de local backups (agente de MARS, o DPM e o servidor de Backup do Azure) é um novo recurso que você obtém quando você atualizar seu Cofre de serviços de tooRecovery de Cofre de Backup. Olá, informações de monitoramento ocupa too12 horas toosync com o serviço de saudação.

**Como faço para relatar um problema?**</br>
Se qualquer parte do cofre Olá de atualização falhar, Olá Observação OperationId listado no erro hello. Microsoft Support proativamente funcionará tooresolve problema de saudação. Você pode alcançar tooSupport ou um e-mail para rsvaultupgrade@service.microsoft.com com sua ID de assinatura, nome do cofre e ID da operação. Tentaremos problema de saudação tooresolve assim que possível. Não repita a operação de saudação, a menos que explicitamente instruído toodo caso pela Microsoft.


## <a name="next-steps"></a>Próximas etapas
Use Olá artigo a seguir:</br>
[Fazer backup de uma VM IaaS](backup-azure-arm-vms-prepare.md)</br>
[Fazer backup de um Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)</br>
[Fazer backup de um Windows Server](backup-configure-vault.md).
