---
title: "Restaurar um grupo do Office 365 excluído no Azure Active Directory | Microsoft Docs"
description: "Como restaurar um grupo excluído, exibir grupos restauráveis e excluir permanentemente um grupo no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="f429e-103">Restaurar um grupo do Office 365 excluído na visualização do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f429e-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="f429e-104">Quando você exclui um grupo do Office 365 no Azure AD (Azure Active Directory), o grupo excluído é mantido, mas não fica visível por 30 dias a partir da data de exclusão.</span><span class="sxs-lookup"><span data-stu-id="f429e-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="f429e-105">Isso é para que o grupo e seu conteúdo possam ser restaurados se necessário.</span><span class="sxs-lookup"><span data-stu-id="f429e-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="f429e-106">Essa funcionalidade é restrita exclusivamente a grupos do Office 365 no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f429e-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="f429e-107">Ele não fica disponível para grupos de segurança e de distribuição.</span><span class="sxs-lookup"><span data-stu-id="f429e-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="f429e-108">Não use `Remove-MsolGroup`, pois ele limpa o grupo permanentemente.</span><span class="sxs-lookup"><span data-stu-id="f429e-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="f429e-109">Sempre use `Remove-AzureADMSGroup` para excluir um grupo do O365.</span><span class="sxs-lookup"><span data-stu-id="f429e-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="f429e-110">As permissões necessárias para restaurar um grupo podem ser qualquer uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="f429e-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="f429e-111">Função</span><span class="sxs-lookup"><span data-stu-id="f429e-111">Role</span></span>  | <span data-ttu-id="f429e-112">Permissões</span><span class="sxs-lookup"><span data-stu-id="f429e-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="f429e-113">Administrador da Empresa, suporte de Camada 2 do Parceiro e Administradores de Serviço do InTune</span><span class="sxs-lookup"><span data-stu-id="f429e-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="f429e-114">Pode restaurar qualquer grupo do Office 365 excluído</span><span class="sxs-lookup"><span data-stu-id="f429e-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="f429e-115">Administrador da Conta de Usuário e suporte de Camada 1 do Parceiro</span><span class="sxs-lookup"><span data-stu-id="f429e-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="f429e-116">Pode restaurar qualquer grupo do Office 365 excluído, exceto aqueles atribuídos à função de Administrador de Empresa</span><span class="sxs-lookup"><span data-stu-id="f429e-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="f429e-117">Usuário</span><span class="sxs-lookup"><span data-stu-id="f429e-117">User</span></span> | <span data-ttu-id="f429e-118">Pode restaurar qualquer grupo do Office 365 excluído que era propriedade dele</span><span class="sxs-lookup"><span data-stu-id="f429e-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="f429e-119">Exibir os grupos do Office 365 excluídos que estão disponíveis para restauração</span><span class="sxs-lookup"><span data-stu-id="f429e-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="f429e-120">Os cmdlets a seguir podem ser usados para exibir os grupos excluídos para verificar que aqueles em que você está interessado ainda não foram permanentemente removidos.</span><span class="sxs-lookup"><span data-stu-id="f429e-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="f429e-121">Esses cmdlets são parte do módulo do [PowerShell do Azure AD](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="f429e-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="f429e-122">Mais informações sobre esse módulo podem ser encontradas no artigo [Azure Active Directory PowerShell Versão 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="f429e-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="f429e-123">Execute o cmdlet a seguir para exibir todos os grupos do Office 365 excluídos em seu locatário que ainda estão disponíveis para restauração.</span><span class="sxs-lookup"><span data-stu-id="f429e-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="f429e-124">Como alternativa, se você souber a objectID de um grupo específico (e você pode obtê-la do cmdlet na etapa 1), execute o cmdlet a seguir para verificar se o grupo excluído específico não ainda foi permanentemente removido.</span><span class="sxs-lookup"><span data-stu-id="f429e-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="f429e-125">Como restaurar seu grupo do Office 365 excluído</span><span class="sxs-lookup"><span data-stu-id="f429e-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="f429e-126">Após ter verificado que o grupo ainda está disponível para restauração, restaure o grupo excluído com uma das etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f429e-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="f429e-127">Se o grupo contém documentos, sites de SP ou outros objetos persistentes, pode levar até 24 horas para restaurar completamente um grupo e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f429e-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="f429e-128">Execute o cmdlet a seguir para restaurar o grupo e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f429e-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="f429e-129">Como alternativa, o cmdlet a seguir pode ser executado para remover permanentemente o grupo excluído.</span><span class="sxs-lookup"><span data-stu-id="f429e-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="f429e-130">Como saber se isso funcionou?</span><span class="sxs-lookup"><span data-stu-id="f429e-130">How do you know this worked?</span></span>
<span data-ttu-id="f429e-131">Para verificar se você restaurou com êxito um grupo do Office 365, execute o cmdlet `Get-AzureADGroup –ObjectId <objectId>` para exibir informações sobre o grupo.</span><span class="sxs-lookup"><span data-stu-id="f429e-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="f429e-132">Após a solicitação de restauração ser concluída:</span><span class="sxs-lookup"><span data-stu-id="f429e-132">After the restore request is completed:</span></span>
- <span data-ttu-id="f429e-133">O grupo será exibido na barra de navegação esquerda no Exchange</span><span class="sxs-lookup"><span data-stu-id="f429e-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="f429e-134">O plano para o grupo será exibido no Planner</span><span class="sxs-lookup"><span data-stu-id="f429e-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="f429e-135">Os sites do Sharepoint e todo o seu conteúdo estarão disponíveis</span><span class="sxs-lookup"><span data-stu-id="f429e-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="f429e-136">O grupo pode ser acessado de qualquer um dos pontos de extremidade do Exchange e outras cargas de trabalho do Office 365 que dão suporte a grupos do Office 365</span><span class="sxs-lookup"><span data-stu-id="f429e-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="f429e-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f429e-137">Next steps</span></span>
<span data-ttu-id="f429e-138">Esses artigos fornecem mais informações sobre grupos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f429e-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="f429e-139">Consultar grupos existentes</span><span class="sxs-lookup"><span data-stu-id="f429e-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="f429e-140">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="f429e-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="f429e-141">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="f429e-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="f429e-142">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="f429e-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="f429e-143">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="f429e-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
