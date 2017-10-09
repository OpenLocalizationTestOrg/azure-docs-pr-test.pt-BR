---
title: "Executando novamente o Assistente para instalação do conectar Olá AD do Azure | Microsoft Docs"
description: "Explica como o Assistente de instalação Olá funciona Olá segunda vez que você executá-lo."
keywords: "Assistente de instalação do Hello AD do Azure Connect permite configurar Olá de configurações de manutenção segunda vez que você executá-lo"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="b7aee-104">Sincronização do Azure AD Connect: executando o Assistente de instalação de saudação uma segunda vez</span><span class="sxs-lookup"><span data-stu-id="b7aee-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="b7aee-105">Olá primeira vez que executar o Assistente de instalação do hello Azure AD Connect, ele orienta como tooconfigure sua instalação.</span><span class="sxs-lookup"><span data-stu-id="b7aee-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="b7aee-106">Se você executar o Assistente de instalação Olá novamente, ele oferece opções para manutenção.</span><span class="sxs-lookup"><span data-stu-id="b7aee-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="b7aee-107">Você pode encontrar o Assistente de instalação Olá no menu de início Olá denominado **do Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="b7aee-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Menu Iniciar](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="b7aee-109">Quando você inicia o Assistente de instalação hello, você pode ver uma página com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="b7aee-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Página com uma lista de tarefas adicionais](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="b7aee-111">Se tiver instalado o ADFS com o Azure AD Connect, você terá ainda mais opções.</span><span class="sxs-lookup"><span data-stu-id="b7aee-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="b7aee-112">Olá opções adicionais disponíveis para AD FS estão documentados em [gerenciamento do ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="b7aee-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="b7aee-113">Selecione uma das tarefas de saudação e clique em **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b7aee-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7aee-114">Com o Assistente de instalação Olá aberto, todas as operações no mecanismo de sincronização de saudação são suspensos.</span><span class="sxs-lookup"><span data-stu-id="b7aee-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="b7aee-115">Verifique se que você fechar o Assistente de instalação de saudação assim que você concluiu as alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b7aee-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="b7aee-116">Exibir a configuração atual</span><span class="sxs-lookup"><span data-stu-id="b7aee-116">View current configuration</span></span>
<span data-ttu-id="b7aee-117">Essa opção fornece uma visão rápida das opções configuradas no momento.</span><span class="sxs-lookup"><span data-stu-id="b7aee-117">This option gives you a quick view of your currently configured options.</span></span>

![Página com uma lista de todas as opções e seus estados](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="b7aee-119">Clique em **anterior** toogo novamente.</span><span class="sxs-lookup"><span data-stu-id="b7aee-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="b7aee-120">Se você selecionar **Exit**, feche o Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7aee-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="b7aee-121">Personalizar opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="b7aee-121">Customize synchronization options</span></span>
<span data-ttu-id="b7aee-122">Essa opção é a configuração de sincronização de toohello toomake usado alterações.</span><span class="sxs-lookup"><span data-stu-id="b7aee-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="b7aee-123">Você verá um subconjunto das opções do caminho de instalação de configuração personalizada de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7aee-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="b7aee-124">Você vê essa opção mesmo que tenha usado a instalação expressa inicialmente.</span><span class="sxs-lookup"><span data-stu-id="b7aee-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="b7aee-125">[Adicionar mais diretórios](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="b7aee-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="b7aee-126">Para remover um diretório, consulte [Excluir um Conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="b7aee-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="b7aee-127">[Alterar a filtragem de domínio e de unidade organizacional](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="b7aee-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="b7aee-128">Remova a filtragem de grupo.</span><span class="sxs-lookup"><span data-stu-id="b7aee-128">Remove Group filtering.</span></span>
* <span data-ttu-id="b7aee-129">[Alterar recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="b7aee-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="b7aee-130">Olá outras opções de instalação de saudação inicial não podem ser alteradas e não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b7aee-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="b7aee-131">Essas opções são:</span><span class="sxs-lookup"><span data-stu-id="b7aee-131">These options are:</span></span>

* <span data-ttu-id="b7aee-132">Alterar Olá atributo toouse para userPrincipalName e sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="b7aee-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="b7aee-133">Alterar Olá unindo o método para objetos de floresta diferente.</span><span class="sxs-lookup"><span data-stu-id="b7aee-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="b7aee-134">Habilite a filtragem baseada em grupo.</span><span class="sxs-lookup"><span data-stu-id="b7aee-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="b7aee-135">Atualizar esquema de diretório</span><span class="sxs-lookup"><span data-stu-id="b7aee-135">Refresh directory schema</span></span>
<span data-ttu-id="b7aee-136">Essa opção é usada se você tiver alterado o esquema de saudação em uma das suas instalações florestas do AD DS.</span><span class="sxs-lookup"><span data-stu-id="b7aee-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="b7aee-137">Por exemplo, você deve ter instalado o Exchange ou atualizar esquema tooa Windows Server 2012 com objetos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7aee-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="b7aee-138">Nesse caso, você precisa tooinstruct do Azure AD Connect tooread Olá esquema novamente do AD DS e atualizar seu cache.</span><span class="sxs-lookup"><span data-stu-id="b7aee-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="b7aee-139">Essa ação também regenera Olá regras de sincronização.</span><span class="sxs-lookup"><span data-stu-id="b7aee-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="b7aee-140">Se você adicionar o esquema de saudação do Exchange, como um exemplo, regras de sincronização de saudação do Exchange são adicionadas toohello configuração.</span><span class="sxs-lookup"><span data-stu-id="b7aee-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="b7aee-141">Quando você seleciona essa opção, todos os diretórios de saudação em sua configuração são listados.</span><span class="sxs-lookup"><span data-stu-id="b7aee-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="b7aee-142">Você pode manter a configuração padrão de saudação e atualizar todas as florestas ou desmarque algumas delas.</span><span class="sxs-lookup"><span data-stu-id="b7aee-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Página com uma lista de todos os diretórios no ambiente de saudação](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="b7aee-144">Configurar modo de preparo</span><span class="sxs-lookup"><span data-stu-id="b7aee-144">Configure staging mode</span></span>
<span data-ttu-id="b7aee-145">Essa opção permite que você tooenable e desabilitar o modo de preparo no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7aee-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="b7aee-146">Encontre mais informações sobre o modo de preparo e como ele é usado em [Operações](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="b7aee-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="b7aee-147">opção Olá mostra se o preparo está habilitado ou desabilitado no momento:</span><span class="sxs-lookup"><span data-stu-id="b7aee-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Opção que também está mostrando o estado atual de saudação do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="b7aee-149">toochange Olá estado, selecione essa opção e marque ou desmarque Olá caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="b7aee-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Opção que também está mostrando o estado atual de saudação do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="b7aee-151">Alterar a entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="b7aee-151">Change user sign-in</span></span>
<span data-ttu-id="b7aee-152">Essa opção permite que você toochange de toofederation de sincronização de senha ou Olá oposto.</span><span class="sxs-lookup"><span data-stu-id="b7aee-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="b7aee-153">Você não pode alterar muito**não configurar**.</span><span class="sxs-lookup"><span data-stu-id="b7aee-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="b7aee-154">Para obter mais informações sobre essa opção, consulte [entrada do usuário](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="b7aee-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7aee-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7aee-155">Next steps</span></span>
* <span data-ttu-id="b7aee-156">Saiba mais sobre o modelo de configuração de saudação usado pela sincronização do Azure AD Connect em [Noções básicas sobre o provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="b7aee-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="b7aee-157">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="b7aee-157">**Overview topics**</span></span>

* [<span data-ttu-id="b7aee-158">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="b7aee-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="b7aee-159">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b7aee-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
