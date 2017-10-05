---
title: Problema ao usar o acesso de aplicativo de autoatendimento | Microsoft Docs
description: Solucione problemas relacionados ao acesso de aplicativo de autoatendimento
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="1733c-103">Problema ao usar o acesso de aplicativo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="1733c-103">Problem using self-service application access</span></span>

<span data-ttu-id="1733c-104">O acesso de aplicativo de autoatendimento é uma ótima maneira de permitir que os usuários descubram aplicativos por conta própria e, ainda, permitir que o grupo de negócios aprove o acesso a esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1733c-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="1733c-105">Você pode permitir que o grupo de negócios gerencie as credenciais atribuídas a esses usuários para Aplicativos de logon único com senha, diretamente de seus painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="1733c-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="1733c-106">Antes que seus usuários possam descobrir por conta própria aplicativos de seu painel de acesso, você precisa habilitar o **Acesso de aplicativo de autoatendimento** a todos os aplicativos que você quiser permitir que os usuários descubram e solicitem acesso por conta própria.</span><span class="sxs-lookup"><span data-stu-id="1733c-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="1733c-107">Problemas gerais a serem verificados primeiro</span><span class="sxs-lookup"><span data-stu-id="1733c-107">General issues to check first</span></span>

-   <span data-ttu-id="1733c-108">Verifique se o acesso do aplicativo de autoatendimento está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="1733c-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="1733c-109">Consulte "Como configurar o acesso de aplicativo de autoatendimento".</span><span class="sxs-lookup"><span data-stu-id="1733c-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="1733c-110">Verifique se o usuário ou o grupo foi habilitado para solicitar acesso de aplicativos de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="1733c-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="1733c-111">Verifique se o usuário está visitando o local correto para acesso de aplicativos de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="1733c-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="1733c-112">Os usuários poderão navegar para seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) e clicar no botão **+Adicionar** para encontrar os aplicativos aos quais você habilitou o acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="1733c-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="1733c-113">Se o acesso de aplicativo de autoatendimento tiver sido configurado recentemente, tente entrar e sair novamente do Painel de Acesso do usuário após alguns minutos para ver se as alterações de acesso de autoatendimento apareceram.</span><span class="sxs-lookup"><span data-stu-id="1733c-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="1733c-114">Como configurar o acesso de aplicativo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="1733c-114">How to configure self-service application access</span></span>

<span data-ttu-id="1733c-115">Para habilitar o acesso de aplicativos de autoatendimento a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="1733c-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="1733c-116">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1733c-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1733c-117">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="1733c-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1733c-118">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1733c-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1733c-119">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1733c-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1733c-120">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1733c-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1733c-121">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="1733c-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1733c-122">Selecione na lista o aplicativo ao qual você deseja habilitar o acesso do autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="1733c-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="1733c-123">Após o carregamento do aplicativo, clique em **Autoatendimento** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1733c-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1733c-124">Para habilitar o acesso de aplicativos de autoatendimento a este aplicativo, coloque o controle de alternância **Permitir aos usuários solicitar acesso a esse aplicativo?** na posição **Sim.**</span><span class="sxs-lookup"><span data-stu-id="1733c-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="1733c-125">Em seguida, para selecionar o grupo ao qual os usuários que solicitam acesso a esse aplicativo devem ser adicionados, clique no seletor ao lado do rótulo **A qual grupo os usuários atribuídos devem ser adicionados?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="1733c-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="1733c-126">**Opcional:** se quiser exigir uma aprovação de negócios antes que os usuários tenham permissão de acesso, coloque o controle de alternância **Exigir aprovação antes de conceder acesso a esse aplicativo?** na posição **Sim**.</span><span class="sxs-lookup"><span data-stu-id="1733c-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="1733c-127">**Opcional: somente para aplicativos que usam logon único com senha,** se quiser permitir que os aprovadores de negócios especifiquem as senhas que são enviadas para esse aplicativo aos usuários aprovados, coloque o controle de alternância **Permitir que os aprovadores definam senhas do usuário para este aplicativo?** na posição **Sim**.</span><span class="sxs-lookup"><span data-stu-id="1733c-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="1733c-128">**Opcional:** para especificar os aprovadores de negócios que têm permissão para aprovar o acesso ao aplicativo, clique no seletor ao lado do rótulo **Quem tem permissão para aprovar o acesso a esse aplicativo?** para selecionar até 10 aprovadores de negócios individuais.</span><span class="sxs-lookup"><span data-stu-id="1733c-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="1733c-129">Não há suporte para grupos.</span><span class="sxs-lookup"><span data-stu-id="1733c-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="1733c-130">**Opcional:** **para aplicativos que expõem funções**, se quiser atribuir usuários aprovados de autoatendimento a uma função, clique no seletor ao lado de **A que função os usuários devem ser atribuídos neste aplicativo?** para selecionar a função a que esses usuários devem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="1733c-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="1733c-131">Clique no botão **Salvar** na parte superior da folha para terminar.</span><span class="sxs-lookup"><span data-stu-id="1733c-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="1733c-132">Após você concluir a configuração do aplicativo de autoatendimento, os usuários poderão navegar para seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) e clicar no botão **+Adicionar** para encontrar os aplicativos aos quais você habilitou o acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="1733c-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="1733c-133">Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="1733c-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="1733c-134">Você pode habilitar um email que notifica a eles quando um usuário solicitar acesso a um aplicativo que requer sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="1733c-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="1733c-135">Essas aprovações dão suporte a fluxos de trabalho de aprovação únicos, o que significa que, se você especificar vários aprovadores, qualquer aprovador individual poderá aprovar o acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1733c-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="1733c-136">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="1733c-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="1733c-137">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="1733c-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="1733c-138">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="1733c-138">Correlation error ID</span></span>

-   <span data-ttu-id="1733c-139">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="1733c-139">UPN (user email address)</span></span>

-   <span data-ttu-id="1733c-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="1733c-140">TenantID</span></span>

-   <span data-ttu-id="1733c-141">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="1733c-141">Browser type</span></span>

-   <span data-ttu-id="1733c-142">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="1733c-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1733c-143">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="1733c-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1733c-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1733c-144">Next steps</span></span>
[<span data-ttu-id="1733c-145">Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="1733c-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
