---
title: exemplos de aaaPowerShell para gerenciar grupos no Active Directory do Azure | Microsoft Docs
description: "Esta página fornece toohelp de exemplos do PowerShell você gerenciar os grupos no Active Directory do Azure"
keywords: Azure AD, Azure Active Directory, PowerShell, Grupos, Gerenciamento de grupos
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Cmdlets da versão 2 do Azure Active Directory para gerenciamento de grupos
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-groups-create-azure-portal.md)
> * [Portal clássico do Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Este artigo contém exemplos de como toouse PowerShell toomanage seus grupos no Azure Active Directory (AD do Azure).  Ele também explica como tooget configurado com o módulo do PowerShell do Azure AD hello. Primeiro, você deve [baixar o módulo do PowerShell do Azure AD Olá](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Instalando o módulo do PowerShell do Azure AD Olá
Olá tooinstall módulo PowerShell do Azure AD, use Olá comandos a seguir:

    PS C:\Windows\system32> install-module azuread

tooverify que Olá módulo foi instalado, use Olá comando a seguir:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Agora você pode iniciar usando Olá cmdlets no módulo hello. Para obter uma descrição completa de saudação cmdlets no módulo de saudação do AD do Azure, consulte documentação de referência online toohello para [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Conectar-se o diretório toohello
Antes de começar a gerenciar grupos usando os cmdlets do PowerShell do AD do Azure, você deve conectar o seu diretório de toohello de sessão do PowerShell ser toomanage. Use Olá comando a seguir:

    PS C:\Windows\system32> Connect-AzureAD

Olá cmdlet solicitará que você para Olá credenciais que você deseja toouse tooaccess seu diretório. Neste exemplo, estamos usando karen@drumkit.onmicrosoft.com tooaccess Olá diretório de demonstração. Olá cmdlet retorna uma sessão de saudação do tooshow de confirmação foi conectada com êxito tooyour diretório:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Agora você pode começar usando grupos de toomanage Olá doWindows Azure cmdlets em seu diretório.

## <a name="retrieving-groups"></a>Recuperando grupos
grupos de tooretrieve existente do seu diretório, que você pode usar Olá cmdlet Get-AzureADGroups. tooretrieve todos os grupos no diretório hello, use o cmdlet Olá sem parâmetros:

    PS C:\Windows\system32> get-azureadgroup

Olá cmdlet retorna todos os grupos no diretório conectado hello.

Você pode usar o hello - objectID parâmetro tooretrieve um grupo específico para o qual você especificar o ID de objeto do grupo de saudação:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

Olá cmdlet agora retorna grupo Olá cujo objectID corresponde o valor de saudação do parâmetro hello inserido:

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Você pode procurar um grupo específico usando Olá - parâmetro de filtro. Esse parâmetro usa uma cláusula de filtro ODATA e retorna todos os grupos que correspondem ao filtro hello, como no exemplo a seguir de saudação:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> Olá cmdlets do AzureAD PowerShell implementar saudação padrão de consulta OData. Para obter mais informações, consulte **$filter** na [opções de consulta do sistema OData usando o ponto de extremidade de OData Olá](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Criando grupos
toocreate um novo grupo no seu diretório, use o cmdlet Olá AzureADGroup de novo. Esse cmdlet cria um novo grupo de segurança chamado "Marketing":

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Atualizando grupos
tooupdate um grupo existente, use cmdlet Olá AzureADGroup conjunto. Neste exemplo, estamos alterando Olá propriedade DisplayName do grupo hello "Administradores do Intune." Primeiro, vamos está localizando grupo hello usando o cmdlet de Get-AzureADGroup hello e filtrar usando o atributo DisplayName hello:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Em seguida, estamos alterando Olá descrição toohello novo valor da propriedade "Administradores do dispositivo Intune":

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Agora se encontrarmos grupo Olá novamente, vemos que a propriedade de descrição de saudação é atualizada tooreflect Olá novo valor:

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>Excluindo grupos
grupos de toodelete do seu diretório, use Olá remover AzureADGroup cmdlet como segue:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Gerenciando membros dos grupos
Se você precisar de novo grupo de tooa membros tooadd, use cmdlet Olá AzureADGroupMember adicionar. Este comando adiciona um grupo de administradores do Intune do membro toohello que foram usados no exemplo anterior de saudação:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

o parâmetro - ObjectId Hello é Olá ObjectID do hello grupo toowhich queremos tooadd um membro e - RefObjectId hello é hello ObjectID do usuário Olá queremos tooadd como um membro do grupo toohello.

membros existentes do hello tooget de um grupo, use cmdlet Get-AzureADGroupMember do hello, como neste exemplo:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

membro de saudação tooremove anteriormente adicionamos toohello grupo, use o cmdlet Olá remover AzureADGroupMember, conforme é mostrado aqui:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

associações de grupo Olá tooverify de um usuário, use Olá selecione AzureADGroupIdsUserIsMemberOf cmdlet. Esse cmdlet usa como seus parâmetros Olá ObjectId do usuário Olá para associações de grupo que toocheck Olá e uma lista de grupos que associações a saudação toocheck. lista de saudação de grupos deve ser fornecido no formulário de saudação do complexo de variável do tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", portanto, primeiro deve criar uma variável com o tipo:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

Em seguida, podemos fornecer valores para Olá IDs de grupo toocheck no atributo hello "IDs de grupo" dessa variável complexos:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Agora, se quisermos toocheck associações de grupo de saudação de um usuário com 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID nos grupos de saudação em $g, devemos usar:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


valor de saudação retornado é uma lista de grupos dos quais esse usuário é membro. Você também pode aplicar essa toocheck método associação contatos, grupos ou entidades de serviço para uma determinada lista de grupos, usando Select-AzureADGroupIdsContactIsMemberOf, selecione AzureADGroupIdsGroupIsMemberOf ou Selecione AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Gerenciando proprietários de grupos
grupo do tooa tooadd proprietários, use o cmdlet Olá AzureADGroupOwner adicionar:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

o parâmetro - ObjectId Hello é Olá ObjectID do hello grupo toowhich queremos tooadd um proprietário e - RefObjectId hello é hello ObjectID do usuário Olá queremos tooadd como proprietário do grupo de saudação.

proprietários de saudação tooretrieve de um grupo, use o cmdlet de Get-AzureADGroupOwner hello:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

Olá cmdlet retorna a lista de saudação de proprietários do grupo especificado hello:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Se você quiser tooremove um proprietário de um grupo, use Olá remover AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Aliases reservados 
Quando um grupo é criado, determinados pontos de extremidade permitem Olá usuário final toospecify um toobe mailNickname ou alias usado como parte do endereço de email de saudação do grupo de saudação. Grupos com hello aliases de email com altos privilégios a seguir só podem ser criados por um administrador global do AD do Azure. 
  
* abuso 
* admin 
* administrator 
* hostmaster 
* majordomo 
* postmaster 
* root 
* seguro 
* segurança 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>Próximas etapas
Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
