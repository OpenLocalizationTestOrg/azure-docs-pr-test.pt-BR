---
title: "O conjunto errado de usuários está sendo provisionado para um aplicativo da Galeria do Azure AD | Microsoft Docs"
description: "Descubra por que um conjunto diferente de usuários está sendo provisionado para um aplicativo em vez dos usuários esperados"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="36cac-103">O conjunto errado de usuários está sendo provisionado para um aplicativo da Galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="36cac-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="36cac-104">Quais usuários são provisionados para o aplicativo é algo orientado principalmente por quais usuários e grupos foram **atribuídos** ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36cac-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="36cac-105">Use os recursos a seguir para saber como verificar quais usuários e grupos foram atribuídos a um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36cac-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="36cac-106">Atribuir um usuário diretamente como administrador</span><span class="sxs-lookup"><span data-stu-id="36cac-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="36cac-107">Para atribuir um ou mais usuários diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36cac-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="36cac-108">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36cac-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36cac-109">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="36cac-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36cac-110">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36cac-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36cac-111">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36cac-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36cac-112">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="36cac-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="36cac-113">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="36cac-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="36cac-114">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="36cac-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="36cac-115">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36cac-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="36cac-116">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="36cac-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="36cac-117">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="36cac-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="36cac-118">Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="36cac-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="36cac-119">Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="36cac-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="36cac-120">Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="36cac-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="36cac-121">**Opcional:** caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="36cac-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="36cac-122">Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36cac-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="36cac-123">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="36cac-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="36cac-124">Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.</span><span class="sxs-lookup"><span data-stu-id="36cac-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="36cac-125">Se o provisionamento estiver configurado e em execução para um aplicativo, novos usuários deverão ser provisionados para um aplicativo em aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="36cac-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="36cac-126">Verifique os **Logs de auditoria** para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36cac-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="36cac-127">Atribuir um grupo diretamente a um aplicativo como administrador</span><span class="sxs-lookup"><span data-stu-id="36cac-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="36cac-128">Para atribuir um ou mais grupos diretamente a um aplicativo, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="36cac-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="36cac-129">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="36cac-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36cac-130">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="36cac-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36cac-131">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36cac-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36cac-132">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36cac-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36cac-133">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="36cac-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="36cac-134">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="36cac-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="36cac-135">Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.</span><span class="sxs-lookup"><span data-stu-id="36cac-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="36cac-136">Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36cac-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="36cac-137">Clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos** para abrir a folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="36cac-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="36cac-138">Clique no seletor **Usuários e grupos** da folha **Adicionar Atribuição**.</span><span class="sxs-lookup"><span data-stu-id="36cac-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="36cac-139">Digite o **nome completo do grupo** que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="36cac-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="36cac-140">Passe o mouse sobre o **grupo** na lista para mostrar uma **caixa de seleção**.</span><span class="sxs-lookup"><span data-stu-id="36cac-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="36cac-141">Clique na caixa de seleção próxima ao logotipo ou ao perfil do grupo para adicionar o usuário na lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="36cac-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="36cac-142">**Opcional:** caso queira **adicionar mais de um grupo**, digite outro **nome de grupo completo** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse grupo à lista **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="36cac-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="36cac-143">Ao concluir a seleção dos grupos, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36cac-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="36cac-144">**Opcional:** clique no seletor **Selecionar Função** na folha **Adicionar Atribuição** para selecionar uma função que será atribuída aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="36cac-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="36cac-145">Clique no botão **Atribuir** para atribuir o aplicativo aos grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="36cac-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="36cac-146">Se o provisionamento estiver configurado e em execução para um aplicativo, novos usuários contidos no grupo deverão ser provisionados para um aplicativo em aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="36cac-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="36cac-147">Verifique os **Logs de auditoria** para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="36cac-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="36cac-148">Provisionamento do nome do grupo e dos detalhes do grupo, além dos membros, se houver suporte para alguns aplicativos.</span><span class="sxs-lookup"><span data-stu-id="36cac-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="36cac-149">Você pode habilitar ou desabilitar essa funcionalidade, habilitando ou desabilitando o **Mapeamento** para objetos de grupo mostrados na guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="36cac-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="36cac-150">Se o provisionamento de grupos estiver habilitado, certifique-se de rever os mapeamentos de atributos para garantir que um campo apropriado esteja sendo usado para a "ID correspondente".</span><span class="sxs-lookup"><span data-stu-id="36cac-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="36cac-151">Este pode ser o nome de exibição ou alias de email, uma vez que o grupo e seus membros não serão provisionados se a propriedade correspondente estiver vazia ou não for preenchida para um grupo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36cac-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36cac-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36cac-152">Next steps</span></span>
[<span data-ttu-id="36cac-153">Automatizar o provisionamento e desprovisionamento de usuários para aplicativos SaaS com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36cac-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
