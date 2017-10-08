---
title: "Azure AD Connect: atualização automática | Microsoft Docs"
description: "Este tópico descreve Olá internos recurso de atualização automática na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: atualização automática
Esse recurso foi introduzido com a compilação 1.1.105.0 (lançada em fevereiro de 2016).

## <a name="overview"></a>Visão geral
Certificando-se de sua instalação do Azure AD Connect está sempre toodate nunca foi tão fácil com hello **atualização automática** recurso. Esse recurso é habilitado por padrão para instalações rápidas e atualizações de DirSync. Quando uma nova versão for lançada, a instalação será atualizada automaticamente.

Atualização automática está habilitada por padrão para seguir hello:

* Instalação das configurações expressas e atualizações de DirSync.
* Usar o SQL Express LocalDB, que é o que as configurações Expressas sempre usam. O DirSync com o SQL Express também usa o LocalDB.
* Olá conta do AD é Olá MSOL_ conta criada as configurações Express e o DirSync.
* Tem menos de 100.000 objetos no metaverso hello.

estado atual de saudação da atualização automática pode ser exibido com o cmdlet do PowerShell Olá `Get-ADSyncAutoUpgrade`. Ele tem Olá estados a seguir:

| Estado | Comentário |
| --- | --- |
| Habilitado |A atualização automática está habilitada. |
| Suspenso |Definido pelo sistema de saudação apenas. Olá sistema não estiver mais atualizações automáticas tooreceive qualificados. |
| Desabilitado |A atualização automática está desabilitada. |

Você pode alterar entre **Habilitado** e **Desabilitado** com o `Set-ADSyncAutoUpgrade`. Apenas sistema Olá deve definir o estado de saudação **suspenso**.

A atualização automática está usando o Azure AD Connect Health para a infraestrutura de atualização de saudação. Para toowork de atualização automática, verifique se você abriu Olá URLs no servidor proxy para **Azure AD Connect Health** conforme documentado no [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Se hello **Synchronization Service Manager** interface do usuário está em execução no servidor de saudação, em seguida, hello atualização está suspenso até que seja fechado Olá da interface do usuário.

## <a name="troubleshooting"></a>Solucionar problemas
Se a instalação do Connect não atualizada conforme o esperado, siga essas toofind etapas out o que pode estar errado.

Primeiro, não espere Olá toobe de atualização automática tentada Olá primeiro dia de que uma nova versão for lançada. Há uma aleatoriedade intencional antes que ocorra uma tentativa de atualização. Sendo assim, não se assuste se a instalação não for atualizada imediatamente.

Se você achar que algo não está correto, primeiro execute `Get-ADSyncAutoUpgrade` tooensure a atualização automática está habilitada.

Em seguida, certifique-se de que abrir URLs Olá necessária no seu proxy ou firewall. Atualização automática está usando o Azure AD Connect Health, conforme descrito em Olá [visão geral](#overview). Se você usar um proxy, certifique-se de integridade foi configurado toouse um [servidor proxy](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Também testar Olá [conectividade integridade](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

Com hello conectividade tooAzure AD verificado, é hora toolook em logs de eventos de saudação. Iniciar o Visualizador de eventos hello e examinar Olá **aplicativo** log de eventos. Adicionar um filtro de log de eventos para a origem de saudação **do Azure AD conectar atualizar** e intervalo de id de evento Olá **300 399**.  
![Filtro de log de eventos para atualização automática](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Agora você pode ver os logs de eventos de saudação associado com o status de saudação para atualização automática.  
![Filtro de log de eventos para atualização automática](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

código de resultado Olá tem um prefixo com uma visão geral do estado de saudação.

| Prefixo do código de resultado | Descrição |
| --- | --- |
| Sucesso |instalação de saudação foi atualizada com êxito. |
| UpgradeAborted |Uma condição temporária interrompido atualização hello. Ele tentará novamente e expectativa de saudação é que ela é bem-sucedida mais tarde. |
| UpgradeNotSupported |sistema de saudação tem uma configuração que está bloqueando o sistema de saudação do que está sendo atualizado automaticamente. Ele poderá ser repetida toosee se a alteração do estado de hello, mas Olá expectativa é de que o sistema Olá deve ser atualizado manualmente. |

Aqui está uma lista de mensagens mais comuns de saudação que encontrar. Não lista todos os, mas a mensagem de saudação do resultado deve ser com o problema que Olá é.

| Mensagem de resultado | Descrição |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Não foi possível gravar o registro de toohello. |
| UpgradeAbortedInsufficientDatabasePermissions |grupo de administradores internos de saudação não tem o banco de dados de toohello de permissões. Atualize manualmente a versão mais recente toohello do Azure AD Connect tooaddress esse problema. |
| UpgradeAbortedInsufficientDiskSpace |Não é uma atualização insuficiente toosupport de espaço em disco. |
| UpgradeAbortedSecurityGroupsNotPresent |Não foi possível localizar e resolver todos os grupos de segurança usados pelo mecanismo de sincronização de saudação. |
| UpgradeAbortedServiceCanNotBeStarted |Olá serviço NT **Microsoft Azure AD Sync** toostart de falha. |
| UpgradeAbortedServiceCanNotBeStarted |Olá serviço NT **Microsoft Azure AD Sync** toostop de falha. |
| UpgradeAbortedServiceIsNotRunning |Olá serviço NT **Microsoft Azure AD Sync** não está em execução. |
| UpgradeAbortedSyncCycleDisabled |Olá SyncCycle opção Olá [Agendador](active-directory-aadconnectsync-feature-scheduler.md) foi desabilitada. |
| UpgradeAbortedSyncExeInUse |Olá [Gerenciador de serviço de sincronização da interface do usuário](active-directory-aadconnectsync-service-manager-ui.md) é aberta no servidor de saudação. |
| UpgradeAbortedSyncOrConfigurationInProgress |Olá Assistente de instalação está em execução ou uma sincronização foi agendada fora Olá Agendador. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Você adicionou seus próprios configuração toohello de regras personalizadas. |
| UpgradeNotSupportedDeviceWritebackEnabled |Você habilitou Olá [write-back de dispositivo](active-directory-aadconnect-feature-device-writeback.md) recurso. |
| UpgradeNotSupportedGroupWritebackEnabled |Você habilitou Olá [write-back de grupo](active-directory-aadconnect-feature-preview.md#group-writeback) recurso. |
| UpgradeNotSupportedInvalidPersistedState |Olá instalação não é um configurações Express ou uma atualização do DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Você tem mais de 100.000 objetos no metaverso hello. |
| UpgradeNotSupportedMultiForestSetup |Você está se conectando toomore de uma floresta. A configuração expressa só se conecta a floresta tooone. |
| UpgradeNotSupportedNonLocalDbInstall |Você não está usando um banco de dados SQL Server Express LocalDB. |
| UpgradeNotSupportedNonMsolAccount |Olá [conta de conector AD](active-directory-aadconnect-accounts-permissions.md#active-directory-account) não é saudação padrão MSOL_ conta mais. |
| UpgradeNotSupportedStagingModeEnabled |servidor de saudação é definido toobe no [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Você habilitou Olá [write-back de usuário](active-directory-aadconnect-feature-preview.md#user-writeback) recurso. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
