---
title: Exemplos do PowerShell para gerenciamento de grupos no Azure Active Directory | Microsoft Docs
description: "Esta página fornece exemplos do PowerShell para ajudar no gerenciamento de seus grupos no Azure Active Directory"
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
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="5daec-104">Cmdlets da versão 2 do Azure Active Directory para gerenciamento de grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5daec-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5daec-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="5daec-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="5daec-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="5daec-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5daec-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="5daec-108">Este artigo contém exemplos de como usar o PowerShell para gerenciar grupos no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5daec-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="5daec-109">Ele também explica como configurar usando o módulo PowerShell do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5daec-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="5daec-110">Primeiramente, você deve [baixar o módulo PowerShell do Azure AD](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="5daec-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="5daec-111">Instalando o módulo PowerShell do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5daec-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="5daec-112">Para instalar o módulo PowerShell do Azure AD, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5daec-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="5daec-113">Para verificar se o módulo foi instalado, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5daec-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="5daec-114">Agora você pode começar a usar os cmdlets do módulo.</span><span class="sxs-lookup"><span data-stu-id="5daec-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="5daec-115">Para obter uma descrição completa dos cmdlets no módulo do Azure AD, veja a documentação de referência online do [PowerShell versão 2 do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="5daec-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="5daec-116">Conectando-se ao diretório</span><span class="sxs-lookup"><span data-stu-id="5daec-116">Connecting to the directory</span></span>
<span data-ttu-id="5daec-117">Antes de começar a gerenciar grupos usando cmdlets do PowerShell do Azure AD, você deve conectar a sessão do PowerShell ao diretório que deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="5daec-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="5daec-118">Use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5daec-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="5daec-119">O cmdlet solicita as credenciais que você deseja usar para acessar o diretório.</span><span class="sxs-lookup"><span data-stu-id="5daec-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="5daec-120">Neste exemplo, estamos usando karen@drumkit.onmicrosoft.com para acessar o diretório de demonstração.</span><span class="sxs-lookup"><span data-stu-id="5daec-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="5daec-121">O cmdlet retorna uma confirmação para mostrar que a conexão da sessão com o diretório foi bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="5daec-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="5daec-122">Agora você pode começar a usar os cmdlets do AzureAD para gerenciar grupos no diretório.</span><span class="sxs-lookup"><span data-stu-id="5daec-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="5daec-123">Recuperando grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-123">Retrieving groups</span></span>
<span data-ttu-id="5daec-124">Para recuperar grupos existentes do diretório, você pode usar o cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="5daec-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="5daec-125">Para recuperar todos os grupos no diretório, use o cmdlet sem parâmetros:</span><span class="sxs-lookup"><span data-stu-id="5daec-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="5daec-126">O cmdlet retorna todos os grupos no diretório conectado.</span><span class="sxs-lookup"><span data-stu-id="5daec-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="5daec-127">Você pode usar o parâmetro -objectID para recuperar um grupo específico, para o qual especifica o objectID do grupo:</span><span class="sxs-lookup"><span data-stu-id="5daec-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="5daec-128">Agora, o cmdlet retorna o grupo cujo objectID corresponde ao valor do parâmetro inserido:</span><span class="sxs-lookup"><span data-stu-id="5daec-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="5daec-129">Você pode procurar um grupo específico usando o parâmetro -filter.</span><span class="sxs-lookup"><span data-stu-id="5daec-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="5daec-130">Esse parâmetro usa uma cláusula de filtro ODATA e retorna todos os grupos que correspondem ao filtro, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5daec-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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
> <span data-ttu-id="5daec-131">Os cmdlets do PowerShell do Azure AD implementam o padrão de consulta OData.</span><span class="sxs-lookup"><span data-stu-id="5daec-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="5daec-132">Para saber mais, confira **$filter** em [Opções de consulta do sistema OData usando o ponto de extremidade do OData](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="5daec-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="5daec-133">Criando grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-133">Creating groups</span></span>
<span data-ttu-id="5daec-134">Para criar um novo grupo no seu diretório, use o cmdlet New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="5daec-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="5daec-135">Esse cmdlet cria um novo grupo de segurança chamado "Marketing":</span><span class="sxs-lookup"><span data-stu-id="5daec-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="5daec-136">Atualizando grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-136">Updating groups</span></span>
<span data-ttu-id="5daec-137">Para atualizar um grupo existente, use o cmdlet Set-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="5daec-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="5daec-138">Neste exemplo, estamos alterando a propriedade DisplayName do grupo "Intune Administrators".</span><span class="sxs-lookup"><span data-stu-id="5daec-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="5daec-139">Primeiramente, vamos localizar o grupo usando o cmdlet Get-AzureADGroup e filtrar usando o atributo DisplayName:</span><span class="sxs-lookup"><span data-stu-id="5daec-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="5daec-140">Em seguida, vamos mudar a propriedade Description para o novo valor "Intune Device Administrators":</span><span class="sxs-lookup"><span data-stu-id="5daec-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="5daec-141">Agora, se localizarmos o grupo novamente, veremos que a propriedade Description foi atualizada para refletir o novo valor:</span><span class="sxs-lookup"><span data-stu-id="5daec-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="5daec-142">Excluindo grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-142">Deleting groups</span></span>
<span data-ttu-id="5daec-143">Para excluir grupos do diretório, use o cmdlet Remove-AzureADGroup da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5daec-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="5daec-144">Gerenciando membros dos grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-144">Managing members of groups</span></span>
<span data-ttu-id="5daec-145">Se você precisa adicionar novos membros a um grupo, use o cmdlet Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="5daec-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="5daec-146">Esse comando adiciona um membro ao grupo Intune Administrators que usamos no exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="5daec-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="5daec-147">O parâmetro -ObjectId é o ObjectID do grupo ao qual queremos adicionar um membro, e -RefObjectId é o ObjectID do usuário que queremos adicionar como um membro ao grupo.</span><span class="sxs-lookup"><span data-stu-id="5daec-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="5daec-148">Para obter os membros existentes de um grupo, use o cmdlet Get-AzureADGroupMember, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="5daec-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="5daec-149">Para remover o membro que adicionamos anteriormente ao grupo, use o cmdlet Remove-AzureADGroupMember, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="5daec-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="5daec-150">Para verificar as associações de um usuário do grupo, use o cmdlet Select-AzureADGroupIdsUserIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="5daec-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="5daec-151">Esse cmdlet utiliza como seus parâmetros o ObjectId do usuário do qual verifica as associações de grupo e uma lista de grupos da qual verifica as associações.</span><span class="sxs-lookup"><span data-stu-id="5daec-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="5daec-152">A lista de grupos deve ser fornecida na forma de uma variável complexa do tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck". Desse modo, devemos criar primeiro uma variável com esse tipo:</span><span class="sxs-lookup"><span data-stu-id="5daec-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="5daec-153">Em seguida, fornecemos valores de groupIds para verificação no atributo "GroupIds" dessa variável complexa:</span><span class="sxs-lookup"><span data-stu-id="5daec-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="5daec-154">Agora, se quisermos verificar as associações de grupo de um usuário com o ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea nos grupos em $g, devemos usar:</span><span class="sxs-lookup"><span data-stu-id="5daec-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="5daec-155">O valor retornado é uma lista de grupos dos quais esse usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="5daec-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="5daec-156">Você também pode aplicar esse método para verificar a associação de Contatos, Grupos ou Entidades de Serviço para uma determinada lista de grupos, usando Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf ou Select-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="5daec-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="5daec-157">Gerenciando proprietários de grupos</span><span class="sxs-lookup"><span data-stu-id="5daec-157">Managing owners of groups</span></span>
<span data-ttu-id="5daec-158">Para adicionar proprietários a um grupo, use o cmdlet Add-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="5daec-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="5daec-159">O parâmetro -ObjectId é o ObjectID do grupo ao qual queremos adicionar um proprietário, e -RefObjectId é o ObjectID do usuário que queremos adicionar como um proprietário do grupo.</span><span class="sxs-lookup"><span data-stu-id="5daec-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="5daec-160">Para recuperar os proprietários de um grupo, use o cmdlet Get-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="5daec-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="5daec-161">O cmdlet retorna a lista de proprietários para o grupo especificado:</span><span class="sxs-lookup"><span data-stu-id="5daec-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="5daec-162">Se quiser remover um proprietário de um grupo, use o cmdlet Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="5daec-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="5daec-163">Aliases reservados</span><span class="sxs-lookup"><span data-stu-id="5daec-163">Reserved aliases</span></span> 
<span data-ttu-id="5daec-164">Quando um grupo é criado, certos pontos de extremidade permitem que o usuário final especifique um mailNickname ou o alias a ser usado como parte do endereço de email do grupo.</span><span class="sxs-lookup"><span data-stu-id="5daec-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="5daec-165">Os grupos com os seguintes aliases de email altamente privilegiados só podem ser criados por um administrador global do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5daec-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="5daec-166">abuso</span><span class="sxs-lookup"><span data-stu-id="5daec-166">abuse</span></span> 
* <span data-ttu-id="5daec-167">admin</span><span class="sxs-lookup"><span data-stu-id="5daec-167">admin</span></span> 
* <span data-ttu-id="5daec-168">administrator</span><span class="sxs-lookup"><span data-stu-id="5daec-168">administrator</span></span> 
* <span data-ttu-id="5daec-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="5daec-169">hostmaster</span></span> 
* <span data-ttu-id="5daec-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="5daec-170">majordomo</span></span> 
* <span data-ttu-id="5daec-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="5daec-171">postmaster</span></span> 
* <span data-ttu-id="5daec-172">root</span><span class="sxs-lookup"><span data-stu-id="5daec-172">root</span></span> 
* <span data-ttu-id="5daec-173">seguro</span><span class="sxs-lookup"><span data-stu-id="5daec-173">secure</span></span> 
* <span data-ttu-id="5daec-174">segurança</span><span class="sxs-lookup"><span data-stu-id="5daec-174">security</span></span> 
* <span data-ttu-id="5daec-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="5daec-175">ssl-admin</span></span> 
* <span data-ttu-id="5daec-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="5daec-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5daec-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5daec-177">Next steps</span></span>
<span data-ttu-id="5daec-178">Você pode encontrar mais documentação do PowerShell do Azure Active Directory em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="5daec-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="5daec-179">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5daec-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="5daec-180">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5daec-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
