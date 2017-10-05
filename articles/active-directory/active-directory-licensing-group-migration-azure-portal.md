---
title: "Como migrar seus usuários individuais licenciados para um grupo no Azure Active Directory | Microsoft Docs"
description: "Como alternar licenças de usuário individuais para licenciamento baseado em grupo usando o Azure Active Directory"
services: active-directory
keywords: Licenciamento do AD do Azure
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b77dd4e9a6d361a05382397e89b575896fdad84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="97931-104">Como adicionar usuários licenciados a um grupo para o licenciamento no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97931-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="97931-105">É possível implantar licenças existentes em usuários nas organizações por meio da “atribuição direta”; ou seja, usando scripts do PowerShell ou outras ferramentas para atribuir licenças de usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="97931-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="97931-106">Se você quiser começar a usar o licenciamento baseado em grupo para gerenciar as licenças da sua organização, precisará de um plano de migração para substituir de forma direta as soluções existentes com licenciamento baseado em grupo.</span><span class="sxs-lookup"><span data-stu-id="97931-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="97931-107">A coisa mais importante para ter em mente é que você deve evitar uma situação onde a migração para o licenciamento baseado em grupo resultará em usuários temporariamente perdendo suas licenças atribuídas.</span><span class="sxs-lookup"><span data-stu-id="97931-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="97931-108">Deve-se evitar qualquer processo que pode resultar na remoção de licenças, a fim de remover o risco de os usuários perderem o acesso aos serviços e a seus dados.</span><span class="sxs-lookup"><span data-stu-id="97931-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="97931-109">Processo de migração recomendado</span><span class="sxs-lookup"><span data-stu-id="97931-109">Recommended migration process</span></span>

1. <span data-ttu-id="97931-110">Você tem a automação existente (por exemplo, PowerShell) gerenciando a atribuição e a remoção de licenças para usuários.</span><span class="sxs-lookup"><span data-stu-id="97931-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="97931-111">Deixe-o em execução como está.</span><span class="sxs-lookup"><span data-stu-id="97931-111">Leave it running as is.</span></span>

2. <span data-ttu-id="97931-112">Crie um novo grupo de licenciamento (ou decida quais grupos existentes serão usados) e verifique se todos os usuários necessários foram adicionados como membros.</span><span class="sxs-lookup"><span data-stu-id="97931-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="97931-113">Atribua as licenças necessárias para esses grupos; sua meta deve ser refletir o estado de licenciamento mesmo que sua automação existente (por exemplo, PowerShell) esteja sendo aplicada aos usuários.</span><span class="sxs-lookup"><span data-stu-id="97931-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="97931-114">Verifique se as licenças foram aplicadas a todos os usuários nesses grupos.</span><span class="sxs-lookup"><span data-stu-id="97931-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="97931-115">Isso pode ser feito verificando o estado de processamento em cada grupo e verificando os Logs de Auditoria.</span><span class="sxs-lookup"><span data-stu-id="97931-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="97931-116">Você pode identificar usuários individuais ao examinar os detalhes de suas licenças.</span><span class="sxs-lookup"><span data-stu-id="97931-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="97931-117">Você verá que eles têm as licenças atribuídas "diretamente" e "herdadas" de grupos.</span><span class="sxs-lookup"><span data-stu-id="97931-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="97931-118">Você pode executar um script do PowerShell para [verificar como as licenças são atribuídas a usuários](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span><span class="sxs-lookup"><span data-stu-id="97931-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="97931-119">Quando a mesma licença do produto é atribuída para o usuário diretamente e por meio de um grupo, apenas uma licença é consumida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="97931-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="97931-120">Portanto, não há nenhuma licença adicional é necessária para realizar uma migração.</span><span class="sxs-lookup"><span data-stu-id="97931-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="97931-121">Verifique se nenhuma atribuição de licença falhou ao verificar cada grupo de usuários em estado de erro.</span><span class="sxs-lookup"><span data-stu-id="97931-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="97931-122">Para saber mais, veja [Identificar e resolver problemas de licença para um grupo](active-directory-licensing-group-problem-resolution-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="97931-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="97931-123">Considere remover as atribuições diretas originais; talvez você deseje fazer isso gradualmente, em “ondas”, para monitorar o resultado em um subconjunto de usuários primeiro.</span><span class="sxs-lookup"><span data-stu-id="97931-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="97931-124">Você poderia deixar as atribuições diretas originais em usuários, mas quando os usuários deixarem seus grupos licenciados, eles ainda manterão a licença original, o que provavelmente não é o que você quer.</span><span class="sxs-lookup"><span data-stu-id="97931-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="97931-125">Um exemplo</span><span class="sxs-lookup"><span data-stu-id="97931-125">An example</span></span>

<span data-ttu-id="97931-126">Temos uma organização com 1.000 usuários.</span><span class="sxs-lookup"><span data-stu-id="97931-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="97931-127">Todos os usuários exigem licenças EMS (Enterprise Mobility + Security).</span><span class="sxs-lookup"><span data-stu-id="97931-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="97931-128">200 usuários estão no departamento de finanças e exigem licenças do Office 365 Enterprise E3.</span><span class="sxs-lookup"><span data-stu-id="97931-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="97931-129">Temos um script do PowerShell em execução no local, adicionando e removendo licenças de usuários à medida que eles vêm e vão.</span><span class="sxs-lookup"><span data-stu-id="97931-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="97931-130">Queremos substituir o script com o licenciamento baseado em grupo para que licenças sejam gerenciadas automaticamente pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97931-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="97931-131">Veja como deve se parecer o processo de migração:</span><span class="sxs-lookup"><span data-stu-id="97931-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="97931-132">Usando o portal do Azure, atribua as licenças EMS ao grupo **Todos os usuários** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97931-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="97931-133">Atribua a licença E3 ao grupo **departamento financeiro** que contém todos os usuários exigidos.</span><span class="sxs-lookup"><span data-stu-id="97931-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="97931-134">Para cada grupo, confirme que a atribuição de licença foi concluída para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="97931-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="97931-135">Vá até a folha de cada grupo, selecione **Licenças** e verifique o status de processamento na parte superior da folha **Licenças**.</span><span class="sxs-lookup"><span data-stu-id="97931-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="97931-136">Procure "As alterações mais recentes de licença foram aplicadas a todos os usuários" para confirmar que o processamento foi concluído.</span><span class="sxs-lookup"><span data-stu-id="97931-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="97931-137">Procure uma notificação na parte superior sobre quaisquer usuários para os quais as licenças talvez não tenham sido atribuídas com êxito.</span><span class="sxs-lookup"><span data-stu-id="97931-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="97931-138">Nós não temos mais licenças para alguns usuários?</span><span class="sxs-lookup"><span data-stu-id="97931-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="97931-139">Alguns usuários têm SKUs com licenças conflitantes que os impedem de herdar as licenças de grupo?</span><span class="sxs-lookup"><span data-stu-id="97931-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="97931-140">Verifique alguns usuários para ver se eles têm as licenças diretas ou de grupo aplicadas.</span><span class="sxs-lookup"><span data-stu-id="97931-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="97931-141">Vá até a folha de um usuário, selecione **Licenças** e examine o estado das licenças.</span><span class="sxs-lookup"><span data-stu-id="97931-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="97931-142">Este é o estado do usuário esperado durante a migração:</span><span class="sxs-lookup"><span data-stu-id="97931-142">This is the expected user state during migration:</span></span>

      ![estado do usuário esperado](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="97931-144">Isso confirma que o usuário tem licenças diretas e herdadas.</span><span class="sxs-lookup"><span data-stu-id="97931-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="97931-145">Podemos ver que **EMS** e **E3** estão atribuídas.</span><span class="sxs-lookup"><span data-stu-id="97931-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="97931-146">Selecione cada licença para mostrar os detalhes sobre os serviços habilitados.</span><span class="sxs-lookup"><span data-stu-id="97931-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="97931-147">Isso pode ser usado para verificar se as licenças diretas e de grupo permitem exatamente os mesmos planos de serviço para o usuário.</span><span class="sxs-lookup"><span data-stu-id="97931-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![planos do serviço de aplicativo](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="97931-149">Depois de confirmar que as licenças direta e de grupo são equivalentes, você poderá começar a remover as licenças diretas dos usuários.</span><span class="sxs-lookup"><span data-stu-id="97931-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="97931-150">É possível testar isso removendo-as para usuários individuais no portal e, em seguida, executar scripts de automação para removê-las em massa.</span><span class="sxs-lookup"><span data-stu-id="97931-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="97931-151">Este é um exemplo do mesmo usuário com as licenças diretas removidas por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="97931-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="97931-152">Observe que o estado da licença permanece inalterado, mas não vemos mais as atribuições diretas.</span><span class="sxs-lookup"><span data-stu-id="97931-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![licenças diretas removidas](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="97931-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97931-154">Next steps</span></span>

<span data-ttu-id="97931-155">Para saber mais sobre outros cenários de gerenciamento de licença por meio de grupos, leia</span><span class="sxs-lookup"><span data-stu-id="97931-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="97931-156">Atribuição de licenças a um grupo no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97931-156">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="97931-157">O que é o licenciamento baseado em grupo no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97931-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="97931-158">Identificar e resolver problemas de licença para um grupo no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97931-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="97931-159">Cenários adicionais de licenciamento baseado em grupo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97931-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
