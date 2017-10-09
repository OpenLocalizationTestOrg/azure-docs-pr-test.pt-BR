---
title: "grupo de aaaRestore um Office 365 excluído no Active Directory do Azure | Microsoft Docs"
description: "Como toorestore um grupo excluído, exibir restauráveis grupos e permamnently excluir um grupo no Active Directory do Azure"
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="dde43-103">Restaurar um grupo do Office 365 excluído na visualização do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dde43-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="dde43-104">Quando você exclui um grupo do Office 365 em hello Azure Active Directory (AD do Azure), o grupo de saudação excluído é retido, mas não é visível por 30 dias da data de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="dde43-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="dde43-105">Isso é para que o grupo de saudação e seu conteúdo pode ser restaurado se necessário.</span><span class="sxs-lookup"><span data-stu-id="dde43-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="dde43-106">Essa funcionalidade é restrita exclusivamente tooOffice 365 grupos no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dde43-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="dde43-107">Ele não fica disponível para grupos de segurança e de distribuição.</span><span class="sxs-lookup"><span data-stu-id="dde43-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="dde43-108">Não use `Remove-MsolGroup` porque ele limpa grupo Olá permanentemente.</span><span class="sxs-lookup"><span data-stu-id="dde43-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="dde43-109">Sempre use `Remove-AzureADMSGroup` toodelete um O365 grupo.</span><span class="sxs-lookup"><span data-stu-id="dde43-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="dde43-110">permissões de saudação necessárias toorestore um grupo pode ser qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="dde43-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="dde43-111">Função</span><span class="sxs-lookup"><span data-stu-id="dde43-111">Role</span></span>  | <span data-ttu-id="dde43-112">Permissões</span><span class="sxs-lookup"><span data-stu-id="dde43-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="dde43-113">Administrador da Empresa, suporte de Camada 2 do Parceiro e Administradores de Serviço do InTune</span><span class="sxs-lookup"><span data-stu-id="dde43-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="dde43-114">Pode restaurar qualquer grupo do Office 365 excluído</span><span class="sxs-lookup"><span data-stu-id="dde43-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="dde43-115">Administrador da Conta de Usuário e suporte de Camada 1 do Parceiro</span><span class="sxs-lookup"><span data-stu-id="dde43-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="dde43-116">Pode restaurar qualquer grupo excluído do Office 365 exceto esses toohello atribuído a função de administrador da empresa</span><span class="sxs-lookup"><span data-stu-id="dde43-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="dde43-117">Usuário</span><span class="sxs-lookup"><span data-stu-id="dde43-117">User</span></span> | <span data-ttu-id="dde43-118">Pode restaurar qualquer grupo do Office 365 excluído que era propriedade dele</span><span class="sxs-lookup"><span data-stu-id="dde43-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="dde43-119">Saudação de exibição excluído grupos do Office 365 que estão disponível toorestore</span><span class="sxs-lookup"><span data-stu-id="dde43-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="dde43-120">Olá cmdlets a seguir pode ser usado tooview Olá excluído grupos tooverify que Olá um ou os em que você estiver interessado não ainda foram permanentemente removidos.</span><span class="sxs-lookup"><span data-stu-id="dde43-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="dde43-121">Esses cmdlets são parte da saudação [módulo PowerShell do AD do Azure](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="dde43-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="dde43-122">Para obter mais informações sobre esse módulo podem ser encontradas no hello [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0) artigo.</span><span class="sxs-lookup"><span data-stu-id="dde43-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="dde43-123">Execute Olá cmdlet excluído toodisplay todos os grupos do Office 365 em seu locatário que estão disponível ainda toorestore a seguir.</span><span class="sxs-lookup"><span data-stu-id="dde43-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="dde43-124">Como alternativa, se você souber objectID Olá de um grupo específico (e você pode obtê-lo do hello cmdlet na etapa 1), execução Olá tooverify cmdlet que Olá grupo excluído específico a seguir não ainda foi permanentemente removido.</span><span class="sxs-lookup"><span data-stu-id="dde43-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="dde43-125">Como toorestore o grupo excluído do Office 365</span><span class="sxs-lookup"><span data-stu-id="dde43-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="dde43-126">Depois que você verificou que grupo Olá é toorestore disponível ainda, restaure o grupo de saudação excluído com uma saudação etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="dde43-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="dde43-127">Se o grupo Olá contém documentos, sites de SP ou outros objetos persistentes, pode levar até too24 horas toofully restaurar um grupo e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="dde43-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="dde43-128">Execução hello seguinte grupo de saudação do cmdlet toorestore e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="dde43-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="dde43-129">Como alternativa, hello cmdlet a seguir pode ser executado toopermanently remover grupo de saudação excluído.</span><span class="sxs-lookup"><span data-stu-id="dde43-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="dde43-130">Como saber se isso funcionou?</span><span class="sxs-lookup"><span data-stu-id="dde43-130">How do you know this worked?</span></span>
<span data-ttu-id="dde43-131">tooverify que você tenha restaurado com êxito um grupo do Office 365, executar Olá `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay informações sobre o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="dde43-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="dde43-132">Após a restauração de saudação solicitação é concluída:</span><span class="sxs-lookup"><span data-stu-id="dde43-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="dde43-133">grupo de saudação será exibido na barra de navegação à esquerda de saudação do Exchange</span><span class="sxs-lookup"><span data-stu-id="dde43-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="dde43-134">plano Olá para o grupo de hello serão exibidos no planejador</span><span class="sxs-lookup"><span data-stu-id="dde43-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="dde43-135">Os sites do Sharepoint e todo o seu conteúdo estarão disponíveis</span><span class="sxs-lookup"><span data-stu-id="dde43-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="dde43-136">Olá grupo pode ser acessado de qualquer um dos pontos de extremidade de troca de saudação e outras cargas de trabalho do Office 365 que dão suporte a grupos do Office 365</span><span class="sxs-lookup"><span data-stu-id="dde43-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="dde43-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dde43-137">Next steps</span></span>
<span data-ttu-id="dde43-138">Esses artigos fornecem mais informações sobre grupos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dde43-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="dde43-139">Consultar grupos existentes</span><span class="sxs-lookup"><span data-stu-id="dde43-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="dde43-140">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="dde43-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="dde43-141">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="dde43-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="dde43-142">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="dde43-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="dde43-143">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="dde43-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
