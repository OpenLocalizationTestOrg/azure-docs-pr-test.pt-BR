---
title: "eventos de relatório de auditoria de Active Directory aaaAzure | Microsoft Docs"
description: "Eventos de auditoria que estão disponíveis para exibição e download no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Eventos de relatório de auditoria do Azure Active Directory
*Esta documentação é parte da saudação [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).*

Olá relatório de auditoria do Azure Active Directory ajuda os clientes a identificar as ações privilegiadas que ocorreram no seu Active Directory do Azure. Ações privilegiadas incluem alterações de elevação (por exemplo, criação de função ou redefinições de senha), alterar configurações de política (por exemplo políticas de senha), ou a configuração de toodirectory de alterações (por exemplo, alterações toodomain configurações de federação). relatórios de Olá fornecem o registro de auditoria Olá para o nome do evento hello, ator Olá que executou a ação hello, o recurso de destino Olá afetada pela alteração Olá e data de saudação (em UTC). Os clientes são tooretrieve capaz de lista de saudação de eventos de auditoria para seu Azure Active Directory por meio de saudação [Portal do Azure](https://portal.azure.com/), conforme descrito em [Exibir Logs de auditoria](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lista de eventos de relatório de auditoria
<!--- audit event descriptions should be in hello past tense --->

| Eventos | Descrição do evento |
| --- | --- |
| **Eventos de usuário** | |
| Adicionar usuário |Adicionar um diretório de toohello do usuário. |
| Excluir usuário |Excluir um usuário do diretório de saudação. |
| Definir propriedades de licença |Definir propriedades de licença de saudação para um usuário no diretório de saudação. |
| Redefinir senha de usuário |Redefina a senha de saudação para um usuário no diretório de saudação. |
| Alterar senha de usuário |Olá senha para um usuário no diretório Olá alterada. |
| Alterar licença de usuário |Alterado licença Olá tooa usuário no diretório Olá atribuída. toosee quais licenças foram atualizadas, procure no hello [atualizar usuário](#update-user-attributes) propriedades abaixo |
| Atualizar usuário |Atualizar um usuário no diretório de saudação. [Veja abaixo](#update-user-attributes) os atributos que podem ser atualizados. |
| Definir alteração forçada de senha de usuário |Defina propriedade de saudação que força um usuário toochange sua senha no logon. |
| Atualizar credenciais de usuário |Senha do usuário Olá alterada |
| **Eventos de grupo** | |
| Adicionar grupo |Criado um grupo no diretório de saudação. |
| Atualizar grupo |Um grupo no diretório Olá atualizado. toosee quais propriedades de grupo foram atualizadas, consulte muito[auditada de propriedades de grupo](#update-group-attributes) Olá abaixo na seção |
| Excluir grupo |Excluiu um grupo do diretório de saudação. |
| CreateGroupSettings |Configurações de grupo criadas |
| UpdateGroupSettings |Configurações de grupo atualizadas. toosee quais configurações de grupo foram atualizadas, consulte muito[auditada de propriedades de grupo](#update-group-attributes) Olá abaixo na seção |
| DeleteGroupSettings |Configurações de grupo excluídas |
| SetGroupLicense |Definir licença de grupo. |
| SetGroupManagedBy |Definir toobe grupo gerenciado por usuário |
| AddGroupMember |Membro adicionado toogroup |
| RemoveGroupMember |Remover membro do grupo |
| AddGroupOwner |Proprietário adicionado toogroup |
| RemoveGroupOwner |Proprietário removido do grupo |
| **Eventos de aplicativo** | |
| Adicionar entidade de serviço |Adicionar um diretório de toohello principal do serviço. |
| Remover entidade de serviço |Removidos uma entidade de serviço do diretório de saudação. |
| Adicionar credenciais de entidade de serviço |Entidade de serviço tooa adicional de credenciais. |
| Remover credenciais de entidade de serviço |Credenciais removidas de uma entidade de serviço. |
| Adicionar entrada de delegação |Criado um [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) no diretório de saudação. |
| Definir entrada de delegação |Atualizar um [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) no diretório de saudação. |
| Remover entrada de delegação |Excluir um [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) no diretório de saudação. |
| **Eventos de função** | |
| Adicionar função membro tooRole |Adicionada uma função de diretório do usuário tooa. |
| Remover membro de função da Função |Um usuário foi removido de uma função de diretório. |
| AddRoleDefinition |Obter definição da função. |
| UpdateRoleDefinition |Atualizar definição de função. toosee quais definições de função foram atualizadas, consulte muito[auditada de propriedades de definição de função](#update-role-definition-attributes) na seção de saudação abaixo |
| DeleteRoleDefinition |Definição de função excluída. |
| AddRoleAssignmentToRoleDefinition |Adicionar definição de toorole de atribuição de função. |
| RemoveRoleAssignmentFromRoleDefinition |Atribuição de função removida da definição de função. |
| AddRoleFromTemplate |Função adicionada de modelo. |
| UpdateRole |Função atualizada. |
| AddRoleScopeMemberToRole |Adicionado toorole no escopo do membro. |
| RemoveRoleScopedMemberFromRole |Membro de escopo removido da função. |
| **Eventos de Dispositivo (todos os novos eventos)** | |
| AddDevice |Dispositivo adicionado. |
| UpdateDevice |Dispositivo atualizado. toosee quais propriedades do dispositivo foram atualizadas, consulte muito[propriedades do dispositivo auditadas](#update-device-attributes) Olá abaixo na seção |
| DeleteDevice |Dispositivo excluído. |
| AddDeviceConfiguration |Configuração de dispositivo adicionado. |
| UpdateDeviceConfiguration |Configuração de dispositivo atualizado. toosee quais propriedades de configuração do dispositivo foram atualizadas, consulte muito[propriedades de configuração de dispositivo auditadas](#update-device-configuration-attributes) Olá abaixo na seção |
| DeleteDeviceConfiguration |Configuração de dispositivo excluído. |
| AddRegisteredOwner |Adicionado toodevice proprietário registrado. |
| AddRegisteredUsers |Adicionado toodevice usuários registrados. |
| RemoveRegisteredOwner |Remover proprietário registrado do dispositivo. |
| RemoveRegisteredUsers |Remover usuários registrados do dispositivo. |
| RemoveDeviceCredentials |Remover credenciais de dispositivo. |
| **Eventos B2B** | |
| Convites do Lote carregados. |Um administrador tiver carregado um arquivo que contém toobe convites enviado toopartner usuários. |
| Convites do Lote processados. |Um arquivo que contém os usuários toopartner de convites foi processado. |
| Convide um usuário externo. |Um usuário externo foi convidado toohello directory. |
| Resgate um convite para usuário externo. |Um usuário externo foi resgatado seu diretório de toohello do convite. |
| Adicione toogroup de usuário externo. |Grupo de tooa de associação no diretório Olá foi atribuído um usuário externo. |
| Atribua tooapplication de usuário externo. |Um usuário externo recebeu o aplicativo de tooan acesso direto. |
| Criação de locatário viral. |Um novo locatário foi criado no AD do Azure pelo resgate de convite hello. |
| Criação de usuário viral. |Um usuário foi criado em um locatário existente no AD do Azure pelo resgate de convite hello. |
| **Unidades Administrativas (todos os novos eventos)** | |
| AddAdministrativeUnit |Adicionar unidade administrativa. |
| UpdateAdministrativeUnit |Atualizar unidade administrativa. toosee quais propriedades de unidade administrativa foram atualizadas, consulte muito[propriedades de unidade administrativa auditada](#update-administrative-unit-attributes) Olá abaixo na seção |
| DeleteAdministrativeUnit |Excluir unidade administrativa. |
| AddMemberToAdministrativeUnit |Adicione membro tooadministrative unidade. |
| RemoveMemberFromAdministrativeUnit |Remover membro de unidade administrativa. |
| **Eventos de diretório** | |
| Adicionar toocompany de parceiro |Adicionar um diretório de toohello do parceiro. |
| Remover o parceiro da empresa |Removido um parceiro do diretório de saudação. |
| DemotePartner |Rebaixar parceiro. |
| Adicionar domínio toocompany |Adicionar um diretório de toohello do domínio. |
| Remover o domínio da empresa |Um domínio foi removido do diretório de saudação. |
| Domínio de atualização |Atualizar um domínio no diretório de saudação. toosee quais propriedades de domínio foram atualizadas, consulte muito[propriedades do domínio auditada](#update-domain-attributes) Olá abaixo na seção |
| Definir a autenticação de domínio |Alterar a configuração de domínio de padrão de saudação do empresa hello. |
| Definir informações de contato da empresa |Defina preferências de contato do nível da empresa. Isso inclui endereços de email para marketing, bem como notificações técnicas sobre os Serviços Online da Microsoft. |
| Definir configurações de federação no domínio |Configurações de Federação Olá atualizado para um domínio. |
| Verificar domínio |Verificar um domínio no diretório de saudação. |
| Verificar domínio por email |Verificar um domínio no diretório hello usando a verificação de email. |
| Definir o sinalizador DirSyncEnabled na empresa |Definir a propriedade Olá que permite que um diretório para sincronização do AD do Azure. |
| Definir política de senha |Defina as restrições de comprimento e de caractere para senhas de usuário. |
| Definir informações da empresa |Informações de nível de empresa Olá atualizado. Consulte Olá [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) cmdlet do PowerShell para obter mais detalhes. |
| SetCompanyAllowedDataLocation |Definir local de dados permitidos da empresa. |
| SetCompanyDirSyncEnabled |Definir sinalizador DirSyncEnabled. |
| SetCompanyDirSyncFeature |Definir recurso DirSync. |
| SetCompanyInformation |Definir Informações da Empresa. |
| SetCompanyMultiNationalEnabled |Definir recurso multinacional de empresa habilitado. |
| SetDirectoryFeatureOnTenant |Definir recurso de diretório no locatário. |
| SetTenantLicenseProperties |Definir propriedades de licença de locatário. |
| CreateCompanySettings |Criar configurações da empresa |
| UpdateCompanySettings |Atualizar configurações da empresa. toosee quais propriedades da empresa foram atualizadas, consulte muito[propriedades de empresa auditada](#update-company-attributes) Olá abaixo na seção |
| DeleteCompanySettings |Excluir configurações da empresa |
| SetAccidentalDeletionThreshold |Definir limite de exclusão acidental. |
| SetRightsManagementProperties |Definir propriedades de gerenciamento de direitos. |
| PurgeRightsManagementProperties |Limpar propriedades de gerenciamento de direitos. |
| UpdateExternalSecrets |Atualizar segredos externos |
| **Eventos de Política (todos os novos eventos)** | |
| AddPolicy |Adicionar política. |
| UpdatePolicy |Atualizar política. |
| DeletePolicy |Excluir política. |
| AddDefaultPolicyApplication |Adicione política tooapplication. |
| AddDefaultPolicyServicePrincipal |Adicione política tooservice entidade. |
| RemoveDefaultPolicyApplication |Remover política do aplicativo. |
| RemoveDefaultPolicyServicePrincipal |Remover política da entidade de serviço. |
| RemovePolicyCredentials |Remover credenciais de política. |

## <a name="audit-report-retention"></a>Retenção do relatório de auditoria

Para obter informações mais recentes sobre retenção hello, consulte [políticas de retenção de relatório do Active Directory do Azure](active-directory-reporting-retention.md).


Para clientes interessados no armazenamento de seus eventos de auditoria por longos períodos de retenção, hello API de relatório pode ser usado tooregularly eventos de auditoria de pull em um repositório de dados separado. Consulte [Getting Started with Olá Reporting API](active-directory-reporting-api-getting-started.md) para obter detalhes.

## <a name="properties-included-with-each-audit-event"></a>Propriedades incluídas com cada evento de auditoria
| Propriedade | Descrição |
| --- | --- |
| Data e hora |Data de saudação e a hora que Olá eventos de auditoria ocorreu |
| Ator |usuário Hello ou entidade de serviço que executou a ação de saudação |
| Ação |ação de saudação que foi executada |
| Destino |usuário de saudação ou entidade de serviço Olá ação foi executada em |

## <a name="update-user-attributes"></a>Atributos de “Atualizar Usuário”
evento de auditoria Hello "usuário" inclui informações adicionais sobre quais atributos de usuário foram atualizados. Para cada atributo, ambos Olá valor anterior e Olá novo valor é incluído.

| Atributo | Descrição |
| --- | --- |
| AccountEnabled |Olá usuário possa acessar. |
| AssignedLicense |Todas as licenças que foram atribuídas toohello usuário. |
| AssignedPlan |Planos de serviço resultante de licenças Olá atribuído toohello usuário. |
| LicenseAssignmentDetail |Obter detalhes sobre licenças atribuídas toohello usuário. Por exemplo, se o licenciamento baseado em grupo estava envolvido, isso inclui grupo Olá Olá concedida licença. |
| Móvel |celular do usuário Hello. |
| OtherMail |Olá endereço de email alternativo do usuário. |
| OtherMobile |Olá celular alternativo do usuário. |
| StrongAuthenticationMethod |Uma lista de métodos de verificação configurado pelo usuário Olá para autenticação multifator, como o código de chamada de voz, SMS ou verificação de um aplicativo móvel. |
| StrongAuthenticationRequirement |Se a Multi-Factor Authentication é imposta, habilitada ou desabilitada para este usuário. |
| StrongAuthenticationUserDetails |usuário Olá telefone email e número de telefone alternativo, número de endereço usado para autenticação multifator e verificação de redefinição de senha. |
| StrongAuthenticationPhoneAppDetail |Aplicativos de telefone forof detalhes registrado tooperform 2FA logon |
| TelephoneNumber |número de telefone do usuário Hello. |
| AlternativeSecurityId |Uma ID de segurança alternativa para o objeto de saudação. |
| CreationType |Método de criação de usuário hello (ou por convite viral). |
| InviteTicket |Lista de permissões de convite para usuário hello. |
| InviteReplyUrl |Lista de urls tooreply mediante a aceitação de convite. |
| InviteResources |Lista de recursos toowhich Olá usuários foi convidada. |
| LastDirSyncTime |Hora da última hello objeto foi atualizado devido a sincronização de saudação autoridade (local cliente) directory. |
| MSExchRemoteRecipientType |Mapeia os tipos de destinatário tooMSO. Consulte também https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [tipos de destinatário MSO] para tipos de destinatário |
| PreferredDataLocation |Olá local preferido para do usuário hello, do grupo, contato, pasta pública, ou dados do dispositivo. |
| ProxyAddresses |endereço de saudação pelo qual um objeto de destinatário do Exchange Server é reconhecido em um sistema de email externos. |
| StsRefreshTokensValidFrom |Carrega informações de revogação de token de atualização - qualquer token de atualização STS emitido antes desse momento serão considerados como expirados. |
| UserPrincipalName |Olá UPN é um nome de logon de estilo da Internet para um usuário. |
| UserState |Status de User PendingApproval/PendingAcceptance/Accepted/PendingVerification. |
| UserStateChangedOn |Carimbo de hora do último tooUserState de alteração. Fluxos de trabalho de ciclo de vida tootrigger usado. |
| UserType |Tipo de usuário. Membro (0), Convidado (1), Viral(2). |

## <a name="update-group-attributes"></a>Atributos de "Atualizar Grupo"
| Atributo | Descrição |
| --- | --- |
| classificação |classificação de saudação para um grupo unificado (alto impacto nos negócios, ICM etc.). |
| Descrição |Legível frases descritivos sobre o objeto de saudação. |
| DisplayName |nome de exibição de saudação para um objeto |
| DirSyncEnabled |Indica se a sincronização ocorre de um diretório autoritativo (cliente, local). |
| GroupLicenseAssignment |Atribuição de licença de um grupo |
| GroupType |Tipo de Grupo, Unificado (0) |
| IsMembershipRuleLocked |Indica que hello MembershipRule propriedade é definida pelo serviço de gerenciamento de grupo de autoatendimento hello e não pode ser alterado pelos usuários. Aplicável toogroups somente onde GroupType inclui GroupType.DynamicMembership |
| IsPublic |Sinalizador tooindicate se o grupo de saudação é pública/privada. |
| LastDirSyncTime |Hora da última hello objeto foi atualizado como resultado da sincronização de saudação autoritativa (cliente, no local) directory. |
| Email |Endereço de email principal |
| MailEnabled |Indica se este grupo tem a funcionalidade de email. |
| MailNickname |Moniker para um objeto de catálogo de endereços, normalmente parte de saudação do seu nome de email que precede hello "@" símbolo. |
| MembershipRule |Uma cadeia de caracteres expressar critérios Olá usados pelo toodetermine de serviço de gerenciamento de grupo de autoatendimento Olá quais membros devem pertencer toothis grupo. Veja também IsMembershipRuleLocked. Aplicável somente toogroups onde GroupType inclui GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Um valor de enumeração definido pelo serviço de gerenciamento de grupo de autoatendimento Olá definindo status de saudação da associação de processamento para esse grupo. Aplicável somente toogroups onde GroupType inclui GroupType.DynamicMembership. |
| ProxyAddresses |endereço de saudação pelo qual um objeto de destinatário do Exchange Server é reconhecido em um sistema de email externos. |
| RenewedDateTime |Registro de carimbo de data/hora de quando um grupo foi renovado pela última vez. |
| SecurityEnabled |Indica se a associação no grupo de saudação pode influenciar as decisões de autorização. |
| WellKnownObject |Rotula um objeto de diretório, indicando-o como parte de um conjunto predefinido. |

## <a name="update-device-attributes"></a>Atributos de "Atualizar Dispositivo"
| Atributo | Descrição |
| --- | --- |
| AccountEnabled |Indica se uma entidade de segurança pode ser autenticada. |
| CloudAccountEnabled |Indica se uma entidade de segurança pode ser autenticada. Gravados pelo InTune quando o dispositivo de saudação é controlado no local. |
| CloudDeviceOSType |Tipo de dispositivo de saudação com base em Olá SO, por exemplo, o Windows RT, iOS. Quando definido por um serviço de nuvem (por exemplo, o Intune), esse atributo se torna autoritativo no diretório de saudação para DeviceOSType. |
| CloudDeviceOSVersion |Versão do SO de saudação. Quando definido por um serviço de nuvem (por exemplo, o Intune), esse atributo se torna autoritativo no diretório de saudação para DeviceOSVersion. |
| CloudDisplayName |Valor do atributo LDAP Olá displayName. Quando definido por um serviço de nuvem (por exemplo, o Intune), esse atributo se torna autoritativo no diretório de saudação do displayName. |
| CloudCreated |Indica se o objeto de saudação foi criado pelos serviços de nuvem. |
| CompliantUntil |Até que horas o dispositivo será considerado compatível. |
| DeviceMetadata |Metadados personalizados para dispositivo Olá |
| DeviceObjectVersion |Esse atributo é usado tooidentify Olá esquema versão dispositivo hello. |
| DeviceOSType |Tipo de dispositivo de saudação com base em Olá SO, por exemplo, o Windows RT, iOS. Gravados pelo hello toobe pretendido e serviço de registro atualizado por Olá serviço de gerenciamento do MDM ou STS claro o serviço de gerenciamento. |
| DeviceOSVersion |Versão do SO de saudação. Gravados pelo hello toobe pretendido e serviço de registro atualizado por Olá serviço de gerenciamento do MDM ou STS claro o serviço de gerenciamento. |
| DevicePhysicalIds |Atributo multivalorado deve toostore identificadores de dispositivo físico hello. Isso pode incluir IDs de BIOS, impressões digitais de TPM, IDs específicas do hardware etc. |
| DirSyncEnabled |Indica se a sincronização ocorre de um diretório autoritativo (cliente, local). |
| DisplayName |nome de exibição de saudação para um objeto |
| IsCompliant |Esse atributo é o status de gerenciamento de dispositivo móvel toomanage usado Olá do dispositivo hello. |
| IsManaged |Este atributo é usado tooindicate dispositivo de saudação é gerenciado por uma nuvem de MDM. |
| LastDirSyncTime |Hora da última hello objeto foi atualizado devido a sincronização de saudação autoritativa (cliente, no local) directory. |

## <a name="update-device-configuration-attributes"></a>Atributos de "Atualizar Configuração do Dispositivo"
| Atributo | Descrição |
| --- | --- |
| MaximumRegistrationInactivityPeriod |número máximo de saudação de dias de um dispositivo pode ficar inativo antes de ser considerada para remoção. |
| RegistrationQuota |Política usada toolimit número de saudação de registros de dispositivo permitido para um único usuário. |

## <a name="update-service-principal-configuration-attributes"></a>Atributos de "Atualizar Configuração de Entidade de Serviço"
| Atributo | Descrição |
| --- | --- |
| AccountEnabled |Indica se uma entidade de segurança pode ser autenticada. |
| AppPrincipalId |Identidade externa, definida pelo aplicativo para uma entidade de segurança. |
| DisplayName |nome de exibição de saudação para um objeto |
| ServicePrincipalName |Um nome principal do serviço, que contém "nome/autoridade" onde nome Especifica um valor de classe do aplicativo e autoridade contém pelo menos hostname [: porta] ou "name" que especifica um identificador para a entidade de serviço hello. |

## <a name="update-app-attributes"></a>Atributos de "Atualizar Aplicativo"
| Atributo | Descrição |
| --- | --- |
| AppAddress |conjunto de saudação de endereços (URLs de redirecionamento) que são atribuídos a entidade de serviço tooa. |
| AppId |ID do aplicativo de saudação |
| AppIdentifierUri |Aplicativo URI que identifica o aplicativo hello.  É normalmente Olá URL de acesso do aplicativo. |
| AppLogoUrl |Olá url de imagem de logotipo do aplicativo hello armazenada em uma CDN. |
| AvailableToOtherTenants |Olá True é aplicativo multilocatário (ou seja, pode ser usado por outros locatários). |
| DisplayName |nome para exibição Olá para um nome de aplicativo |
| Direito |Lista de direitos do aplicativo. |
| ExternalUserAccountDelegationsAllowed |Sinalizador que indica se o aplicativo de recurso é confiável e se pode criar entradas de delegação para contas de usuário externo. |
| GroupMembershipClaims |associação de grupo Olá declarações de política. |
| PublicClient |True se o cliente Olá não é possível manter em segredo (ou seja, não confidenciais do cliente no OAuth 2.0) |
| RecordConsentConditions |Tipos de condições de consentimento, conforme definido pelo Olá termos do contrato: None (0), SilentConsentForPartnerManagedApp(1). Esse valor será exposta no esquema de API do Graph hello e só pode ser definido/alterado por administradores de inquilinos. |
| RequiredResourceAccess |Conteúdo XML de um valor da propriedade RequiredResourceAccess de saudação. |
| WebApp |Se verdadeiro, indica que esse aplicativo é um aplicativo Web. |
| WwwHomepage |Olá a página da Web principal. |

## <a name="update-role-attributes"></a>Atributos de "Atualizar Função"
| Atributo | Descrição |
| --- | --- |
| AppAddress |conjunto de saudação de endereços (URLs de redirecionamento) que são atribuídos a entidade de serviço tooa. |
| BelongsToFirstLoginObjectSet |Se for true, indica que esse objeto pertence toohello conjunto do logon de tooenable necessário de objetos de saudação primeiro administrador de um novo locatário. |
| Builtin |Indica se tempo de vida de saudação de um objeto é de propriedade de sistema hello. |
| Descrição |Legível frases descritivos sobre o objeto de saudação. |
| DisplayName |nome de exibição de saudação para um objeto |
| MailNickname |Moniker para um objeto de catálogo de endereços, normalmente parte de saudação do seu nome de email que precede hello "@" símbolo. |
| RoleDisabled |Indica se a função hello deve ser ignorada para fins de verificações de acesso. |
| RoleTemplateId |Identidade do modelo de função hello. |
| ServiceInfo |Informações que podem ser consumidas por MOAC e/ou em outras instâncias do serviço de provisionamento específico ao serviço (de saudação iguais ou diferente tipos de serviço). |
| TaskSetScopeReference |Identifica um TaskSet e um conjunto de Escopos associados a uma Função ou RoleTemplate. |
| ValidationError |Informações publicadas por um serviço federado que descreve um erro não transitório, específico do serviço sobre propriedades de saudação ou link de um tooresolve de ação do administrador de objeto. |
| WellKnownObject |Rotula um objeto de diretório, indicando-o como parte de um conjunto predefinido. |

## <a name="update-role-definition-attributes"></a>Atributos "Atualizar Definição de Função"
| Atributo | Descrição |
| --- | --- |
| AssignableScopes |Coleção de escopos de autorização que podem ser referenciados ao atribuir essa entidade de segurança de tooa RoleDefinition. |
| DisplayName |nome de exibição de saudação para um objeto |
| GrantedPermissions |Permissões concedidas por esta RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Atributos de "Atualizar Unidade Administrativa"
| Atributo | Descrição |
| --- | --- |
| Descrição |Essa propriedade é atualizada quando você alterar a descrição de saudação de uma unidade administrativa. |
| DisplayName |Essa propriedade é atualizada quando você alterar o nome de saudação de uma unidade administrativa. |

## <a name="update-company-attributes"></a>Atributos de "Atualizar Empresa"
| Atributo | Descrição |
| --- | --- |
| AllowedDataLocation |Um local no qual Olá usuários da empresa são permitidos toobe provisionado. |
| AuthorizedServiceInstance |Nomes de instâncias de serviço toowhich um plano podem ser implantados. |
| DirSyncEnabled |Indica se a sincronização ocorre de um diretório autoritativo (cliente, local). |
| DirSyncStatus |Indica se a sincronização de objetos de catálogo de endereços neste contexto de locatário ocorre de um autoridade (cliente, no local) diretório; uma expansão da saudação DirSyncEnabled propriedade em objetos da empresa. |
| DirSyncFeatures |Faixa de tookeep de sinalizador de bit do conjunto de recursos de dirsync habilitados e desabilitados para o locatário hello. |
| DirectoryFeatures |Recursos de diretório habilitados/desabilitados. |
| DirSyncConfiguration |Contém todos os DirSync configuração toohello específico locatário atual. |
| DisplayName |nome de exibição de saudação para um objeto |
| IsMnc |Uma empresa de saudação do sinalizador booliano conjunto muito "verdadeiro" se está habilitada para o recurso de empresa multinacional de saudação. |
| ObjectSettings |Uma coleção de escopo de toohello aplicável de configurações de objeto de saudação. |
| PartnerCommerceUrl |Site de comércio do parceiro de toohello URL. |
| PartnerHelpUrl |Site de Ajuda do parceiro de toohello URL. |
| PartnerSupportEmail |Email de suporte do parceiro de toohello URL. |
| PartnerSupportTelephone |Telefone de suporte do parceiro de toohello URL. |
| PartnerSupportUrl |Site de suporte do parceiro de toohello URL. |
| StrongAuthenticationDetails |Detalhes relacionados à tooStrongAuthentication. |
| StrongAuthenticationPolicy |Política de autenticação forte para a empresa de saudação. |
| TechnicalNotificationMail |Email endereço toonotify problemas técnicos relativos tooa empresa. |
| TelephoneNumber |Números de telefone que estão em conformidade com hello e. 123 de recomendação ITU. |
| TenantType |tipo de saudação de um locatário. Se esse valor não for especificado, o locatário Olá é uma empresa. Caso contrário, os valores possíveis são: MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2) BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Um conjunto de nomes de domínio DNS associado tooa da empresa. |

## <a name="update-domain-attributes"></a>Atributos de "Atualizar Domínio"
| Atributo | Descrição |
| --- | --- |
| Funcionalidades |Os sinalizadores de bit que descreve recursos de saudação do domínio hello, se houver. |
| Padrão |Indica se o domínio de saudação é o valor de padrão de saudação; Por exemplo, Olá UserPrincipalName sufixo padrão quando um administrador cria um novo usuário em MOAC. |
| Inicial |Indica se Olá domínio é saudação inicial para a empresa hello, como alocado pelo OCP. domínio de saudação inicial é um subdomínio exclusivo de um domínio do Microsoft Online; e.g.contoso3.microsoftonline.com. |
| LiveType |Tipo de saudação do Windows Live namespace correspondente, se houver. |
| Nome |Identificador de ponto de extremidade de saudação. |
| PasswordNotificationWindowDays |número de saudação de dias antes que uma senha expire usuário Olá é notificado. |
| PasswordValidityPeriodDays |Olá o número de dias que é bom para uma senha antes que deva ser alterada. |

Registros de auditoria são um controle necessário para muitas regulamentações de conformidade. Para clientes que usam hello Azure Active Directory auditoria relatório toomeet suas regulamentações de conformidade, é recomendável cliente Olá enviar uma cópia deste tópico de ajuda com cópia de saudação do cliente hello exportada toohelp explicam o relatório de saudação do relatório de auditoria detalhes. Se auditor Olá gostaria regulamentações de conformidade do hello toounderstand Azure atende atualmente, direcionar Olá auditor toohello [página conformidade](https://azure.microsoft.com/support/trust-center/compliance/) de saudação do Microsoft Azure Trust Center.

