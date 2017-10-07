---
title: "Azure AD Connect: atualizar de uma versão anterior | Microsoft Docs"
description: "Explica Olá diferentes métodos tooupgrade toohello versão mais recente do Azure Active Directory Connect, incluindo uma atualização in-loco e uma migração de movimento."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Do Azure AD Connect: A atualização de toohello uma versão anterior mais recente
Este tópico descreve métodos diferentes de saudação que você pode usar tooupgrade sua versão mais recente do Connect do Azure Active Directory (AD do Azure) instalação toohello. É recomendável que você mantenha-se atualizado com as versões de saudação do Azure AD Connect. Você também usar etapas Olá Olá [gire migração](#swing-migration) seção quando você alterar uma configuração significativa.

Se você quiser tooupgrade do DirSync, consulte [atualização da ferramenta de sincronização do AD do Azure (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) em vez disso.

Há algumas estratégias diferentes que você pode usar tooupgrade do Azure AD Connect.

| Método | Descrição |
| --- | --- |
| [Atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) |Este é o método mais fácil de saudação para clientes com uma instalação expressa. |
| [Atualização in-loco](#in-place-upgrade) |Se você tiver um único servidor, você pode atualizar Olá instalação local no mesmo servidor de hello. |
| [Migração swing](#swing-migration) |Com dois servidores, você pode preparar um dos servidores de saudação com a nova versão de hello ou configuração e alterar o servidor ativo hello quando você estiver pronto. |

Para obter informações de permissões, consulte Olá [permissões necessárias para uma atualização](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Depois de habilitar a sua nova conexão do AD do Azure server toostart sincronizando alterações tooAzure AD, não reverta toousing DirSync ou o Azure AD Sync. Downgrade de clientes de toolegacy de conexão do AD do Azure, incluindo o DirSync e sincronização do AD do Azure, não é suportado e pode levar tooissues como perda de dados no AD do Azure.

## <a name="in-place-upgrade"></a>Atualização in-loco
Uma atualização in-loco funciona para mudar do Azure AD Sync ou do Azure AD Connect. Ele não funcionará para a migração do DirSync ou para uma solução com o FIM (Forefront Identity Manager) + Azure AD Connector.

Esse será o método preferencial quando você tiver um único servidor e menos de cerca de 100.000 objetos. Se houver alterações de regras de sincronização de fora da caixa de toohello, uma importação completa e sincronização completa ocorrerem após a atualização de saudação. Esse método garante que Olá nova configuração é aplicada tooall os objetos existentes no sistema de saudação. Essa execução pode levar algumas horas, dependendo do número de saudação de objetos que estão no escopo do mecanismo de sincronização de saudação. Agendador de sincronização delta normal da saudação (que sincroniza a cada 30 minutos por padrão) é suspenso, mas continua a sincronização de senha. Você pode considerar fazer atualização in-loco de saudação durante um fim de semana. Se não houver nenhuma configuração de fora da caixa de toohello alterações com versão de conectar Olá novo AD do Azure, em seguida, um normal importação/sincronização delta inicia em vez disso.  
![Atualização in-loco](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Se você tiver feito alterações regras de sincronização de fora da caixa de toohello, em seguida, essas regras estiverem definidas volta configuração padrão de toohello na atualização. toomake-se de que sua configuração é mantida entre atualizações, certifique-se de que você faça alterações conforme eles são descritos em [as práticas recomendadas para alterar a configuração padrão de saudação](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Durante a atualização in-loco, pode haver alterações que requerem sincronização específica toobe de atividades (incluindo as etapas de importação completa e sincronização completa) executado após a conclusão da atualização. toodefer tais atividades, consulte toosection [como toodefer completo sincronização após a atualização](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Migração swing
Se você tiver uma implantação complexa ou muitos objetos, pode ser impraticável toodo uma atualização no local no sistema ao vivo hello. Para alguns clientes, o processo poderá levar vários dias e, durante esse tempo, nenhuma alteração delta será processada. Você também pode usar esse método quando você planejar a configuração de tooyour de alterações substanciais toomake e você deseja tootry-los out antes que elas são enviadas toohello nuvem.

Olá recomendado método para esses cenários é toouse uma migração de movimento. Você precisa de (pelo menos) dois servidores, um servidor ativo e um de preparo. servidor ativo de saudação (mostrado com linhas azuis sólidas em Olá figura abaixo) é responsável pela carga de produção ativo hello. saudação (mostrado com tracejadas roxas) do servidor de preparo está preparada com a nova versão de hello ou configuração. Quando estiver totalmente pronto, esse servidor ficará ativo. Olá anterior active server, que agora tem hello configuração instalado ou versão antiga, é feita no servidor de preparo Olá e é atualizado.

dois servidores de saudação podem usar diferentes versões. Por exemplo, o servidor ativo de saudação que você planeje toodecommission pode usar o Azure AD Sync e novo servidor de preparo Olá pode usar o Azure AD Connect. Se você usar o giro migração toodevelop uma nova configuração, ela é uma boa ideia toohave Olá mesmas versões em Olá dois servidores.  
![Servidor de preparo](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Alguns clientes preferem toohave três ou quatro servidores para este cenário. Quando Olá servidor de preparo é atualizado, você não tiver um servidor de backup para [a recuperação de desastres](active-directory-aadconnectsync-operations.md#disaster-recovery). Com três ou quatro servidores, você pode preparar um conjunto de servidores de principal/standby Olá nova versão, que garante que haja sempre um servidor de preparo está pronto tootake acima.

Essas etapas de trabalho também toomove de sincronização do AD do Azure ou uma solução com FIM + conector AD do Azure. Essas etapas não funcionam para DirSync, mas Olá mesmo movimento método de migração (também chamado de implantação paralela) com as etapas para DirSync está em [sincronização de atualizar o Active Directory do Azure (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Usar um tooupgrade de migração de movimento
1. Se você usar o Azure AD Connect em servidores e verifique tooonly de plano uma alteração de configuração, certifique-se de que o servidor ativo e o servidor de preparo estiverem usando Olá a mesma versão. Que torna mais fácil diferenças de toocompare mais tarde. Se você estiver atualizando do Azure AD Sync, esses servidores terão versões diferentes. Se você estiver atualizando de uma versão anterior do Azure AD Connect, é toostart uma boa ideia com hello dois servidores de Olá usando a mesma versão, mas não é obrigatório.
2. Se você fez uma configuração personalizada e o servidor de preparo não-lo, execute as etapas de saudação em [mover uma configuração personalizada de saudação do active server toohello servidor de preparo](#move-custom-configuration-from-active-to-staging-server).
3. Se você estiver atualizando de uma versão anterior do Azure AD Connect, atualize Olá versão mais recente do servidor toohello de preparo. Se estiver movendo do Azure AD Sync, instale o Azure AD Connect em seu servidor de preparo.
4. Permitem que a importação completa do mecanismo de execução Olá sincronização e sincronização completa em seu servidor de preparo.
5. Verifique se essa nova configuração de saudação não causar alterações inesperadas usando Olá etapas em "Verificar" no [Verificar configuração de saudação de um servidor](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Se algo não estiver correto, como esperado, execute importação hello e sincronização e verifique dados saudação até que parece bom, seguindo as etapas de saudação.
6. Comutador hello toobe Olá active servidor de preparo. Esta é a etapa de final de hello "Switch servidor ativo" no [Verificar configuração de saudação de um servidor](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Se você estiver atualizando do Azure AD Connect, atualize o servidor de saudação que é agora de preparo na versão mais recente do modo toohello. Siga Olá mesmo etapas antes tooget Olá dados e atualizado. Se estiver atualizando do Azure AD Sync, agora você poderá desativar e encerrar o servidor antigo.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Mover uma configuração personalizada do servidor de preparo Olá active server toohello
Se você fez o servidor ativo de toohello de alterações de configuração, você precisa toomake-se que Olá mesmo as alterações são aplicada toohello servidor de preparo. Mover toohelp com isso, você pode usar o hello [Documentador de configuração do Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

Você pode mover as regras de sincronização personalizadas Olá que você criou usando o PowerShell. Você deve aplicar outros Olá alterações maneira mesmo em ambos os sistemas e você não pode migrar alterações hello. Olá [Documentador configuração](https://github.com/Microsoft/AADConnectConfigDocumenter) pode ajudá-lo a comparar Olá dois sistemas toomake-se de que eles são idênticos. ferramenta de saudação também pode ajudar a automatizar etapas Olá encontradas nesta seção.

Você precisa tooconfigure Olá seguinte coisas Olá mesmo maneira em ambos os servidores:

* Conexão toohello mesmo florestas
* Qualquer filtragem de domínio e de unidade organizacional
* Olá mesmo recursos opcionais, como a sincronização de senha e Write-back de senha

**Mover regras de sincronização personalizadas**  
regras de sincronização personalizadas toomove, Olá a seguir:

1. Abra o **Editor de Regras de Sincronização** em seu servidor ativo.
2. Selecione uma regra personalizada. Clique em **Exportar**. Isso abre uma janela do Bloco de Notas. Salve o arquivo temporário Olá com uma extensão PS1. Isso o transforma em um script do PowerShell. Copie toohello de arquivo PS1 Olá servidor de preparo.  
   ![Exportação da regra de sincronização](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Olá GUID do conector é diferente em Olá servidor de preparo, e você deve alterá-la. Olá tooget GUID, iniciar **Editor de regras de sincronização**, selecione uma das regras de out-of-box Olá Olá que representam mesmo sistema conectado e clique em **exportar**. Substitua Olá GUID em seu arquivo PS1 Olá GUID da saudação servidor de preparo.
4. Em um prompt do PowerShell, execute o arquivo hello PS1. Isso cria a regra de sincronização personalizadas Olá em Olá servidor de preparo.
5. Repita essa etapa para todas as regras personalizadas.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Como toodefer completo sincronização após a atualização
Durante a atualização in-loco, pode haver alterações que requerem sincronização específica atividades (incluindo as etapas de importação completa e sincronização completa) toobe executado. Por exemplo, alterações de esquema do conector exigem **importação completa** requerem alterações de regra de sincronização de etapa e out-of-box **completo sincronização** etapa toobe executado nos conectores afetados. Durante a atualização, o Azure AD Connect determina quais atividades de sincronização são necessárias e registra-as como *substituições*. Em Olá após o ciclo de sincronização, Agendador de sincronização de saudação pega essas substituições e executa-los. Quando uma substituição é executada com êxito, ela é removida.

Pode haver situações em que você não quer local de tootake essas substituições imediatamente após a atualização. Por exemplo, você tem vários objetos sincronizados e você deseja que essas toooccur de etapas de sincronização depois do horário comercial. tooremove essas substituições:

1. Durante a atualização, **desmarque** Olá opção **iniciar o processo de sincronização de saudação quando configuração for concluída**. Isso desabilita o Agendador de sincronização hello e impede que ciclo de sincronização ocorra automaticamente antes de substituições de saudação são removidas.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Após a conclusão da atualização, execute Olá toofind cmdlet out quais substituições foram adicionadas a seguir:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > Olá substituições são específicas do conector. No hello exemplo a seguir, as etapas de importação completa e sincronização completa foram adicionados tooboth Olá conector AD local e conector AD do Azure.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Anote Olá existente substituições que foram adicionados.
   
4. Olá tooremove substituições para importação completa e sincronização completa em um conector arbitrária, executar Olá cmdlet a seguir:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   substituições de saudação tooremove em todos os conectores, execute Olá script do PowerShell a seguir:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. Agendador de saudação tooresume, execute Olá cmdlet a seguir:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Lembre-se tooexecute Olá necessárias etapas de sincronização assim que for possível. Manualmente você pode executar essas etapas usando Olá Synchronization Service Manager ou adicionar substituições hello usando Olá conjunto ADSyncSchedulerConnectorOverride cmdlet.

Olá tooadd substituições para importação completa e sincronização completa em um conector arbitrária, executar Olá cmdlet a seguir:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).
