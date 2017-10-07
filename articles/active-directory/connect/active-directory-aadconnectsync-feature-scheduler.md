---
title: "Sincronização do Azure AD Connect: agendador | Microsoft Docs"
description: "Este tópico descreve o recurso de agendador interno Olá na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Sincronização do Azure AD Connect: agendador
Este tópico descreve o agendador interno de saudação na sincronização do Azure AD Connect (também conhecido como mecanismo de sincronização).

Esse recurso foi introduzido com a compilação 1.1.105.0 (lançada em fevereiro de 2016).

## <a name="overview"></a>Visão geral
A sincronização do Azure AD Connect sincroniza mudanças ocorridas em seu diretório local usando um agendador. Há dois processos de agendador, um para sincronização de senha e outro para sincronização de atributo/objeto e tarefas de manutenção. Este tópico aborda Olá último.

Em versões anteriores, o Agendador de saudação para objetos e atributos foi toohello externo mecanismo de sincronização. Antes que o Agendador de tarefas do Windows ou um Windows service tootrigger Olá sincronização processo separado. Agendador de saudação está com hello mecanismo de sincronização de toohello internos versões 1.1 e permitem a alguma personalização. frequência de sincronização Olá novo padrão é 30 minutos.

Agendador de saudação é responsável por duas tarefas:

* **Ciclo de sincronização**. Olá processo tooimport, sincronização e alterações de exportação.
* **Tarefas de manutenção**. Renove as chaves e certificados para a redefinição de Senha e o DRS (Serviço de Registro de Dispositivo). Limpe as entradas antigas no log de operações de saudação.

Agendador de saudação em si está sempre em execução, mas pode ser configurado tooonly executar uma ou nenhuma dessas tarefas. Por exemplo, se você precisar toohave seu próprio processo de ciclo de sincronização, você pode desabilitar essa tarefa no Agendador de saudação mas tarefa de manutenção Olá execução ainda.

## <a name="scheduler-configuration"></a>Configuração do agendador
toosee as configurações atuais, vá tooPowerShell e executar `Get-ADSyncScheduler`. Ele mostra algo parecido com esta imagem:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Se você vir **Olá sincronização comando ou cmdlet não está disponível** quando você executar esse cmdlet, em seguida, Olá PowerShell módulo não está carregado. Esse problema pode ocorrer se você executar o Azure AD Connect em um controlador de domínio ou em um servidor com níveis mais altos de restrição do PowerShell que as configurações padrão de saudação. Se você vir esse erro, execute `Import-Module ADSync` toomake Olá cmdlet disponível.

* **AllowedSyncCycleInterval**. Olá menor tempo intervalo entre os ciclos de sincronização permitido pelo AD do Azure. Você não pode sincronizar com maior frequência do que a permitida por essa configuração e ainda ter suporte.
* **CurrentlyEffectiveSyncCycleInterval**. Olá agendamento atualmente em vigor. Ele tem Olá mesmo valor CustomizedSyncInterval (se definido) se não for mais frequente que AllowedSyncInterval. Se você usar uma versão anterior à 1.1.281 e alterar o CustomizedSyncCycleInterval, essa alteração entrará em vigor após o próximo ciclo de sincronização. Compilação 1.1.281 Olá alteração entrará em vigor imediatamente.
* **CustomizedSyncCycleInterval**. Se você quiser Olá Agendador toorun em qualquer outra frequência padrão Olá 30 minutos, você definir essa configuração. Na Figura Olá acima, Olá Agendador definido toorun a cada hora em vez disso. Se você definir o valor dessa configuração tooa inferior AllowedSyncInterval, Olá esta última é usada.
* **NextSyncCyclePolicyType**. Delta ou Inicial. Define se Olá próxima execução deve apenas as alterações de delta de processo ou se hello próxima execução deve fazer um completo importar e sincronizar. Olá último também seria reprocessar nenhuma regra nova ou alterada.
* **NextSyncCycleStartTimeInUTC**. Próxima inicialização Agendador Olá Olá próximo ciclo de sincronização.
* **PurgeRunHistoryInterval**. Olá a operação de tempo de logs devem ser mantidos. Esses logs podem ser examinados no Gerenciador de serviço de sincronização de saudação. Olá padrão é tookeep esses logs para 7 dias.
* **SyncCycleEnabled**. Indica se Agendador Olá está executando processos de exportação, sincronização e importação de saudação como parte de sua operação.
* **MaintenanceEnabled**. Mostra se o processo de manutenção de saudação está habilitado. Atualiza Olá certificados/chaves e limpa Olá log de operações.
* **StagingModeEnabled**. Mostra se o [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode) está habilitado. Se essa configuração estiver habilitada, ela suprime Olá exportações de execução, mas ainda executar importação e sincronização.
* **SchedulerSuspended**. Definido por conectar durante um agendador de saudação do bloco tootemporarily atualização seja executado.

Você pode alterar algumas dessas configurações com `Set-ADSyncScheduler`. Olá parâmetros a seguir pode ser modificada:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

Em builds anteriores do Azure AD Connect, **isStagingModeEnabled** era exposto em Set-ADSyncScheduler. É **sem suporte** tooset essa propriedade. Olá propriedade **SchedulerSuspended** só deve ser modificado por conectar-se. É **sem suporte** tooset isso com o PowerShell diretamente.

configuração do Agendador Olá é armazenada no AD do Azure. Se você tiver um servidor de preparo, qualquer alteração no servidor primário Olá também afeta Olá preparação do servidor (exceto IsStagingModeEnabled).

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Sintaxe: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - dias, HH - horas, mm - minutos, ss - segundos

Exemplo: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Alterações Olá Agendador toorun a cada três horas.

Exemplo: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
As alterações de alteração Olá Agendador toorun diariamente.

### <a name="disable-hello-scheduler"></a>Desabilitar o Agendador Olá  
Se você precisar toomake alterações de configuração, você deseja toodisable Agendador de saudação. Por exemplo, quando você [configurar a filtragem de](active-directory-aadconnectsync-configure-filtering.md) ou [fazer alterações regras toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

Agendador de saudação toodisable, execute `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Desabilitar o Agendador Olá](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Quando você fez as alterações, não se esqueça de Agendador de saudação tooenable novamente com `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Inicie o Agendador de saudação
Agendador de saudação é por padrão são executados a cada 30 minutos. Em alguns casos, convém toorun ciclo de uma sincronização entre Olá agendado ciclos ou é necessário toorun um tipo diferente.

**Ciclo de sincronização delta**  
Um ciclo de sincronização delta inclui Olá etapas a seguir:

* Importação delta em todos os conectores
* Sincronização delta em todos os conectores
* Exportação em todos os conectores

É possível que você tenha um urgentes alterações que devem ser sincronizadas imediatamente, por isso, você precisa toomanually executar um ciclo. Se você precisar toomanually executar um ciclo, em seguida, de execução PowerShell `Start-ADSyncSyncCycle -PolicyType Delta`.

**Ciclo de sincronização completo**  
Se você fez uma saudação alterações de configuração a seguir, é necessário (também conhecido como toorun um ciclo de sincronização completa Inicial):

* Adicionados mais toobe objetos ou atributos importado de um diretório de origem
* Fez alterações toohello regras de sincronização
* Alterou a [filtragem](active-directory-aadconnectsync-configure-filtering.md) para incluir um número diferente de objetos

Se você fez uma dessas alterações, você precisa toorun ciclo de uma sincronização completa para que o mecanismo de sincronização de saudação tem espaços de conector Olá oportunidade tooreconsolidate hello. Um ciclo de sincronização completa inclui Olá etapas a seguir:

* Importação completa de todos os conectores
* Sincronização completa de todos os conectores
* Exportação em todos os conectores

tooinitiate um ciclo de sincronização completa, executar `Start-ADSyncSyncCycle -PolicyType Initial` em um prompt do PowerShell. Esse comando inicia um ciclo de sincronização completa.

## <a name="stop-hello-scheduler"></a>Parar o Agendador Olá
Se o Agendador hello está sendo executado um ciclo de sincronização, talvez seja necessário toostop-lo. Por exemplo, se você iniciar o Assistente de instalação de saudação e você receberá esse erro:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Se um ciclo de sincronização estiver em execução, você não poderá alterar a configuração. Você pode aguardar até que o Agendador Olá tiver concluído o processo de hello, mas você também pode interrompê-lo para que você possa fazer as alterações imediatamente. Parando Olá ciclo atual não é prejudicial e alterações pendentes são processadas da próxima execução.

1. Iniciar informando Olá Agendador toostop atual ciclo com o cmdlet do PowerShell Olá `Stop-ADSyncSyncCycle`.
2. Se você usar uma compilação antes 1.1.281, parando o Agendador de saudação não interrompe a saudação atual conector de sua tarefa atual. tooforce Olá conector toostop, levar Olá ações a seguir: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Iniciar **serviço de sincronização** saudação do menu de início. Vá muito**conectores**, realce Olá conector com o estado de saudação **executando**e selecione **parar** de saudação ações.

Agendador de saudação ainda está ativo e inicia novamente na próxima oportunidade.

## <a name="custom-scheduler"></a>Agendador personalizado
Olá cmdlets documentadas nesta seção estão disponíveis somente na compilação [1.1.130.0](active-directory-aadconnect-version-history.md#111300) e posterior.

Se o agendador interno Olá não atender às suas necessidades, você pode agendar Olá conectores usando o PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
Você pode iniciar um perfil para um Conector desta forma:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Olá nomes toouse para [nomes de conector](active-directory-aadconnectsync-service-manager-ui-connectors.md) e [nomes de perfil executar](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) podem ser encontradas no hello [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).

![Invocar perfil de execução](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Olá `Invoke-ADSyncRunProfile` cmdlet é síncrono, ou seja, ele não retorna o controle até que Olá conector concluiu a operação de hello, com êxito ou com um erro.

Quando você planejar seus conectores, recomendação de saudação é tooschedule em Olá ordem a seguir:

1. (Completo/Delta) Importar de diretórios locais, como o Active Directory
2. (Completo/Delta) Importar do Azure AD
3. (Completo/Delta) Sincronizar de diretórios locais, como o Active Directory
4. (Completo/Delta) Sincronização do Azure AD
5. Exportar tooAzure AD
6. Exportar diretórios tooon local, como o Active Directory

Essa ordem é como o agendador interno Olá executa Olá conectores.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
Você também pode monitorar Olá toosee de mecanismo de sincronização se ele estiver ocupado ou ocioso. Esse cmdlet retorna um resultado vazio se o mecanismo de sincronização de saudação está ocioso e não está em execução a um conector. Se um conector está em execução, ele retorna o nome de saudação do hello conector.

```
Get-ADSyncConnectorRunStatus
```

![Status de execução do conector](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
Imagem de saudação acima, Olá primeira linha é de um estado em que o mecanismo de sincronização hello está ocioso. Olá segunda linha quando Olá conector AD do Azure está em execução.

## <a name="scheduler-and-installation-wizard"></a>Agendador e o assistente de instalação
Se você iniciar o Assistente de instalação hello, Agendador Olá é suspenso temporariamente. Esse comportamento ocorre porque supõe-se fazer alterações de configuração e essas configurações não podem ser aplicadas se o mecanismo de sincronização de saudação ativamente está em execução. Por esse motivo, não deixe o Assistente de instalação Olá aberto desde que ele interrompe o mecanismo de sincronização de saudação de executar as ações de sincronização.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
