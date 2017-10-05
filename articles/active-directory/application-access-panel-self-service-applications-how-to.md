---
title: Como usar o acesso de aplicativo de autoatendimento | Microsoft Docs
description: "Habilite o acesso do aplicativo de autoatendimento para permitir que os usuários encontrem seus próprios aplicativos"
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
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="0b95f-103">Como usar o acesso de aplicativo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="0b95f-103">How to use self-service application access</span></span>

<span data-ttu-id="0b95f-104">Antes que seus usuários possam descobrir por conta própria aplicativos de seu painel de acesso, você precisa habilitar o **Acesso de aplicativo de autoatendimento** a todos os aplicativos que você quiser permitir que os usuários descubram e solicitem acesso por conta própria.</span><span class="sxs-lookup"><span data-stu-id="0b95f-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="0b95f-105">Esse recurso é uma ótima maneira de economizar tempo e dinheiro como um grupo de TI e é altamente recomendável como parte de uma implantação de aplicativos moderna com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b95f-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="0b95f-106">Usando esse recurso, você pode:</span><span class="sxs-lookup"><span data-stu-id="0b95f-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="0b95f-107">Permitir que os usuários descubram aplicativos por conta própria no [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) sem incomodar o grupo de TI.</span><span class="sxs-lookup"><span data-stu-id="0b95f-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="0b95f-108">Adicione esses usuários a um grupo pré-configurado para que você possa ver quem solicitou acesso, remover o acesso e gerenciar as funções atribuídas a eles.</span><span class="sxs-lookup"><span data-stu-id="0b95f-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="0b95f-109">Ou permita que um aprovador de negócios aprove solicitações de acesso ao aplicativo para que o grupo de TI não precise fazer isso.</span><span class="sxs-lookup"><span data-stu-id="0b95f-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="0b95f-110">Também é possível configurar até 10 pessoas que podem aprovar o acesso a esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b95f-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="0b95f-111">Opcionalmente, permita que um aprovador de negócios defina as senhas que esses usuários podem usar para entrar no aplicativo, diretamente no [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) do aprovador de negócios.</span><span class="sxs-lookup"><span data-stu-id="0b95f-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="0b95f-112">É possível, ainda, atribuir automaticamente o autoatendimento atribuído aos usuários diretamente a uma função de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b95f-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="0b95f-113">Habilite o acesso do aplicativo de autoatendimento para permitir que os usuários encontrem seus próprios aplicativos</span><span class="sxs-lookup"><span data-stu-id="0b95f-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="0b95f-114">O acesso de aplicativo de autoatendimento é uma ótima maneira de permitir que os usuários descubram aplicativos por conta própria e, ainda, permitir que o grupo de negócios aprove o acesso a esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0b95f-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="0b95f-115">Você pode permitir que o grupo de negócios gerencie as credenciais atribuídas a esses usuários para Aplicativos de logon único com senha, diretamente de seus painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="0b95f-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="0b95f-116">Para habilitar o acesso de aplicativos de autoatendimento a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="0b95f-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="0b95f-117">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0b95f-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0b95f-118">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="0b95f-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b95f-119">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b95f-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b95f-120">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b95f-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b95f-121">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0b95f-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0b95f-122">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="0b95f-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0b95f-123">Selecione na lista o aplicativo ao qual você deseja habilitar o acesso do autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="0b95f-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="0b95f-124">Após o carregamento do aplicativo, clique em **Autoatendimento** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b95f-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0b95f-125">Para habilitar o acesso de aplicativos de autoatendimento a este aplicativo, coloque o controle de alternância **Permitir aos usuários solicitar acesso a esse aplicativo?** na posição **Sim.**</span><span class="sxs-lookup"><span data-stu-id="0b95f-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="0b95f-126">Em seguida, para selecionar o grupo ao qual os usuários que solicitam acesso a esse aplicativo devem ser adicionados, clique no seletor ao lado do rótulo **A qual grupo os usuários atribuídos devem ser adicionados?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="0b95f-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="0b95f-127">**Opcional:** se quiser exigir uma aprovação de negócios antes que os usuários tenham permissão de acesso, coloque o controle de alternância **Exigir aprovação antes de conceder acesso a esse aplicativo?** na posição **Sim**.</span><span class="sxs-lookup"><span data-stu-id="0b95f-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="0b95f-128">**Opcional: somente para aplicativos que usam logon único com senha,** se quiser permitir que os aprovadores de negócios especifiquem as senhas que são enviadas para esse aplicativo aos usuários aprovados, coloque o controle de alternância **Permitir que os aprovadores definam senhas do usuário para este aplicativo?** na posição **Sim**.</span><span class="sxs-lookup"><span data-stu-id="0b95f-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="0b95f-129">**Opcional:** para especificar os aprovadores de negócios que têm permissão para aprovar o acesso ao aplicativo, clique no seletor ao lado do rótulo **Quem tem permissão para aprovar o acesso a esse aplicativo?** para selecionar até 10 aprovadores de negócios individuais.</span><span class="sxs-lookup"><span data-stu-id="0b95f-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="0b95f-130">Não há suporte para grupos.</span><span class="sxs-lookup"><span data-stu-id="0b95f-130">Groups are not supported.</span></span>

13. <span data-ttu-id="0b95f-131">**Opcional:** **para aplicativos que expõem funções**, se quiser atribuir usuários aprovados de autoatendimento a uma função, clique no seletor ao lado de **A que função os usuários devem ser atribuídos neste aplicativo?** para selecionar a função a que esses usuários devem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="0b95f-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="0b95f-132">Clique no botão **Salvar** na parte superior da folha para terminar.</span><span class="sxs-lookup"><span data-stu-id="0b95f-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="0b95f-133">Após você concluir a configuração do aplicativo de autoatendimento, os usuários poderão navegar para seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/) e clicar no botão **+Adicionar** para encontrar os aplicativos aos quais você habilitou o acesso de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="0b95f-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="0b95f-134">Aprovadores de negócios também recebem uma notificação em seu [Painel de Acesso do Aplicativo](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0b95f-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="0b95f-135">Você pode habilitar um email que notifica a eles quando um usuário solicitar acesso a um aplicativo que requer sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="0b95f-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="0b95f-136">Essas aprovações dão suporte a fluxos de trabalho de aprovação únicos, o que significa que, se você especificar vários aprovadores, qualquer aprovador individual poderá aprovar o acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b95f-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b95f-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b95f-137">Next steps</span></span>
[<span data-ttu-id="0b95f-138">Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="0b95f-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
