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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="4b219-104">Cmdlets da versão 2 do Azure Active Directory para gerenciamento de grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b219-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4b219-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="4b219-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4b219-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="4b219-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b219-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="4b219-108">Este artigo contém exemplos de como toouse PowerShell toomanage seus grupos no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4b219-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="4b219-109">Ele também explica como tooget configurado com o módulo do PowerShell do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="4b219-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="4b219-110">Primeiro, você deve [baixar o módulo do PowerShell do Azure AD Olá](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="4b219-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="4b219-111">Instalando o módulo do PowerShell do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="4b219-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="4b219-112">Olá tooinstall módulo PowerShell do Azure AD, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b219-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="4b219-113">tooverify que Olá módulo foi instalado, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b219-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="4b219-114">Agora você pode iniciar usando Olá cmdlets no módulo hello.</span><span class="sxs-lookup"><span data-stu-id="4b219-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="4b219-115">Para obter uma descrição completa de saudação cmdlets no módulo de saudação do AD do Azure, consulte documentação de referência online toohello para [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="4b219-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="4b219-116">Conectar-se o diretório toohello</span><span class="sxs-lookup"><span data-stu-id="4b219-116">Connecting toohello directory</span></span>
<span data-ttu-id="4b219-117">Antes de começar a gerenciar grupos usando os cmdlets do PowerShell do AD do Azure, você deve conectar o seu diretório de toohello de sessão do PowerShell ser toomanage.</span><span class="sxs-lookup"><span data-stu-id="4b219-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="4b219-118">Use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b219-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="4b219-119">Olá cmdlet solicitará que você para Olá credenciais que você deseja toouse tooaccess seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4b219-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="4b219-120">Neste exemplo, estamos usando karen@drumkit.onmicrosoft.com tooaccess Olá diretório de demonstração.</span><span class="sxs-lookup"><span data-stu-id="4b219-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="4b219-121">Olá cmdlet retorna uma sessão de saudação do tooshow de confirmação foi conectada com êxito tooyour diretório:</span><span class="sxs-lookup"><span data-stu-id="4b219-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="4b219-122">Agora você pode começar usando grupos de toomanage Olá doWindows Azure cmdlets em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4b219-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="4b219-123">Recuperando grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-123">Retrieving groups</span></span>
<span data-ttu-id="4b219-124">grupos de tooretrieve existente do seu diretório, que você pode usar Olá cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="4b219-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="4b219-125">tooretrieve todos os grupos no diretório hello, use o cmdlet Olá sem parâmetros:</span><span class="sxs-lookup"><span data-stu-id="4b219-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="4b219-126">Olá cmdlet retorna todos os grupos no diretório conectado hello.</span><span class="sxs-lookup"><span data-stu-id="4b219-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="4b219-127">Você pode usar o hello - objectID parâmetro tooretrieve um grupo específico para o qual você especificar o ID de objeto do grupo de saudação:</span><span class="sxs-lookup"><span data-stu-id="4b219-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="4b219-128">Olá cmdlet agora retorna grupo Olá cujo objectID corresponde o valor de saudação do parâmetro hello inserido:</span><span class="sxs-lookup"><span data-stu-id="4b219-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="4b219-129">Você pode procurar um grupo específico usando Olá - parâmetro de filtro.</span><span class="sxs-lookup"><span data-stu-id="4b219-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="4b219-130">Esse parâmetro usa uma cláusula de filtro ODATA e retorna todos os grupos que correspondem ao filtro hello, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="4b219-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="4b219-131">Olá cmdlets do AzureAD PowerShell implementar saudação padrão de consulta OData.</span><span class="sxs-lookup"><span data-stu-id="4b219-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="4b219-132">Para obter mais informações, consulte **$filter** na [opções de consulta do sistema OData usando o ponto de extremidade de OData Olá](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="4b219-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="4b219-133">Criando grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-133">Creating groups</span></span>
<span data-ttu-id="4b219-134">toocreate um novo grupo no seu diretório, use o cmdlet Olá AzureADGroup de novo.</span><span class="sxs-lookup"><span data-stu-id="4b219-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="4b219-135">Esse cmdlet cria um novo grupo de segurança chamado "Marketing":</span><span class="sxs-lookup"><span data-stu-id="4b219-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="4b219-136">Atualizando grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-136">Updating groups</span></span>
<span data-ttu-id="4b219-137">tooupdate um grupo existente, use cmdlet Olá AzureADGroup conjunto.</span><span class="sxs-lookup"><span data-stu-id="4b219-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="4b219-138">Neste exemplo, estamos alterando Olá propriedade DisplayName do grupo hello "Administradores do Intune."</span><span class="sxs-lookup"><span data-stu-id="4b219-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="4b219-139">Primeiro, vamos está localizando grupo hello usando o cmdlet de Get-AzureADGroup hello e filtrar usando o atributo DisplayName hello:</span><span class="sxs-lookup"><span data-stu-id="4b219-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="4b219-140">Em seguida, estamos alterando Olá descrição toohello novo valor da propriedade "Administradores do dispositivo Intune":</span><span class="sxs-lookup"><span data-stu-id="4b219-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="4b219-141">Agora se encontrarmos grupo Olá novamente, vemos que a propriedade de descrição de saudação é atualizada tooreflect Olá novo valor:</span><span class="sxs-lookup"><span data-stu-id="4b219-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="4b219-142">Excluindo grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-142">Deleting groups</span></span>
<span data-ttu-id="4b219-143">grupos de toodelete do seu diretório, use Olá remover AzureADGroup cmdlet como segue:</span><span class="sxs-lookup"><span data-stu-id="4b219-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="4b219-144">Gerenciando membros dos grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-144">Managing members of groups</span></span>
<span data-ttu-id="4b219-145">Se você precisar de novo grupo de tooa membros tooadd, use cmdlet Olá AzureADGroupMember adicionar.</span><span class="sxs-lookup"><span data-stu-id="4b219-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="4b219-146">Este comando adiciona um grupo de administradores do Intune do membro toohello que foram usados no exemplo anterior de saudação:</span><span class="sxs-lookup"><span data-stu-id="4b219-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="4b219-147">o parâmetro - ObjectId Hello é Olá ObjectID do hello grupo toowhich queremos tooadd um membro e - RefObjectId hello é hello ObjectID do usuário Olá queremos tooadd como um membro do grupo toohello.</span><span class="sxs-lookup"><span data-stu-id="4b219-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="4b219-148">membros existentes do hello tooget de um grupo, use cmdlet Get-AzureADGroupMember do hello, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="4b219-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="4b219-149">membro de saudação tooremove anteriormente adicionamos toohello grupo, use o cmdlet Olá remover AzureADGroupMember, conforme é mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="4b219-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="4b219-150">associações de grupo Olá tooverify de um usuário, use Olá selecione AzureADGroupIdsUserIsMemberOf cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b219-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="4b219-151">Esse cmdlet usa como seus parâmetros Olá ObjectId do usuário Olá para associações de grupo que toocheck Olá e uma lista de grupos que associações a saudação toocheck.</span><span class="sxs-lookup"><span data-stu-id="4b219-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="4b219-152">lista de saudação de grupos deve ser fornecido no formulário de saudação do complexo de variável do tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", portanto, primeiro deve criar uma variável com o tipo:</span><span class="sxs-lookup"><span data-stu-id="4b219-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="4b219-153">Em seguida, podemos fornecer valores para Olá IDs de grupo toocheck no atributo hello "IDs de grupo" dessa variável complexos:</span><span class="sxs-lookup"><span data-stu-id="4b219-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="4b219-154">Agora, se quisermos toocheck associações de grupo de saudação de um usuário com 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID nos grupos de saudação em $g, devemos usar:</span><span class="sxs-lookup"><span data-stu-id="4b219-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="4b219-155">valor de saudação retornado é uma lista de grupos dos quais esse usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="4b219-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="4b219-156">Você também pode aplicar essa toocheck método associação contatos, grupos ou entidades de serviço para uma determinada lista de grupos, usando Select-AzureADGroupIdsContactIsMemberOf, selecione AzureADGroupIdsGroupIsMemberOf ou Selecione AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="4b219-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="4b219-157">Gerenciando proprietários de grupos</span><span class="sxs-lookup"><span data-stu-id="4b219-157">Managing owners of groups</span></span>
<span data-ttu-id="4b219-158">grupo do tooa tooadd proprietários, use o cmdlet Olá AzureADGroupOwner adicionar:</span><span class="sxs-lookup"><span data-stu-id="4b219-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="4b219-159">o parâmetro - ObjectId Hello é Olá ObjectID do hello grupo toowhich queremos tooadd um proprietário e - RefObjectId hello é hello ObjectID do usuário Olá queremos tooadd como proprietário do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b219-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="4b219-160">proprietários de saudação tooretrieve de um grupo, use o cmdlet de Get-AzureADGroupOwner hello:</span><span class="sxs-lookup"><span data-stu-id="4b219-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="4b219-161">Olá cmdlet retorna a lista de saudação de proprietários do grupo especificado hello:</span><span class="sxs-lookup"><span data-stu-id="4b219-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="4b219-162">Se você quiser tooremove um proprietário de um grupo, use Olá remover AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b219-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="4b219-163">Aliases reservados</span><span class="sxs-lookup"><span data-stu-id="4b219-163">Reserved aliases</span></span> 
<span data-ttu-id="4b219-164">Quando um grupo é criado, determinados pontos de extremidade permitem Olá usuário final toospecify um toobe mailNickname ou alias usado como parte do endereço de email de saudação do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b219-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="4b219-165">Grupos com hello aliases de email com altos privilégios a seguir só podem ser criados por um administrador global do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b219-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="4b219-166">abuso</span><span class="sxs-lookup"><span data-stu-id="4b219-166">abuse</span></span> 
* <span data-ttu-id="4b219-167">admin</span><span class="sxs-lookup"><span data-stu-id="4b219-167">admin</span></span> 
* <span data-ttu-id="4b219-168">administrator</span><span class="sxs-lookup"><span data-stu-id="4b219-168">administrator</span></span> 
* <span data-ttu-id="4b219-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="4b219-169">hostmaster</span></span> 
* <span data-ttu-id="4b219-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="4b219-170">majordomo</span></span> 
* <span data-ttu-id="4b219-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="4b219-171">postmaster</span></span> 
* <span data-ttu-id="4b219-172">root</span><span class="sxs-lookup"><span data-stu-id="4b219-172">root</span></span> 
* <span data-ttu-id="4b219-173">seguro</span><span class="sxs-lookup"><span data-stu-id="4b219-173">secure</span></span> 
* <span data-ttu-id="4b219-174">segurança</span><span class="sxs-lookup"><span data-stu-id="4b219-174">security</span></span> 
* <span data-ttu-id="4b219-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="4b219-175">ssl-admin</span></span> 
* <span data-ttu-id="4b219-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="4b219-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4b219-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b219-177">Next steps</span></span>
<span data-ttu-id="4b219-178">Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="4b219-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="4b219-179">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b219-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="4b219-180">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b219-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
