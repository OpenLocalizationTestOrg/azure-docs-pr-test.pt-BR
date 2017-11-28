---
title: "Executar novamente o assistente de instalação do Azure AD Connect | Microsoft Docs"
description: "Explica como o assistente de instalação funciona na segunda vez que é executado."
keywords: "O assistente de instalação do Azure AD Connect permite configurar as configurações de manutenção da segunda vez que é executado"
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="007d2-104">Sincronização do Azure AD Connect: executar o assistente de instalação pela segunda vez</span><span class="sxs-lookup"><span data-stu-id="007d2-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="007d2-105">Na primeira vez que você executa o assistente de instalação do Azure AD Connect, ele explica como configurar a instalação.</span><span class="sxs-lookup"><span data-stu-id="007d2-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="007d2-106">Se você executar o assistente de instalação novamente, ele oferecerá opções para manutenção.</span><span class="sxs-lookup"><span data-stu-id="007d2-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="007d2-107">Você pode encontrar o assistente de instalação no menu Iniciar chamado **Azure Connect AD**.</span><span class="sxs-lookup"><span data-stu-id="007d2-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Menu Iniciar](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="007d2-109">Ao iniciar o assistente de instalação, você vê uma página com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="007d2-109">When you start the installation wizard, you see a page with these options:</span></span>

![Página com uma lista de tarefas adicionais](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="007d2-111">Se tiver instalado o ADFS com o Azure AD Connect, você terá ainda mais opções.</span><span class="sxs-lookup"><span data-stu-id="007d2-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="007d2-112">As opções adicionais disponíveis para ADFS estão documentadas em [Gerenciamento do ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="007d2-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="007d2-113">Selecione uma das tarefas e clique em **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="007d2-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="007d2-114">Enquanto o assistente de instalação estiver aberto, todas as operações no mecanismo de sincronização serão suspensas.</span><span class="sxs-lookup"><span data-stu-id="007d2-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="007d2-115">Lembre-se de fechar o assistente de instalação assim que concluir as alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="007d2-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="007d2-116">Exibir a configuração atual</span><span class="sxs-lookup"><span data-stu-id="007d2-116">View current configuration</span></span>
<span data-ttu-id="007d2-117">Essa opção fornece uma visão rápida das opções configuradas no momento.</span><span class="sxs-lookup"><span data-stu-id="007d2-117">This option gives you a quick view of your currently configured options.</span></span>

![Página com uma lista de todas as opções e seus estados](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="007d2-119">Clique em **Voltar** para voltar.</span><span class="sxs-lookup"><span data-stu-id="007d2-119">Click **Previous** to go back.</span></span> <span data-ttu-id="007d2-120">Se você selecionar **Sair**, o assistente de instalação será fechado.</span><span class="sxs-lookup"><span data-stu-id="007d2-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="007d2-121">Personalizar opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="007d2-121">Customize synchronization options</span></span>
<span data-ttu-id="007d2-122">Esta opção é usada para fazer alterações na configuração de sincronização.</span><span class="sxs-lookup"><span data-stu-id="007d2-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="007d2-123">Você vê um subconjunto das opções do caminho de instalação de configuração personalizada.</span><span class="sxs-lookup"><span data-stu-id="007d2-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="007d2-124">Você vê essa opção mesmo que tenha usado a instalação expressa inicialmente.</span><span class="sxs-lookup"><span data-stu-id="007d2-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="007d2-125">[Adicionar mais diretórios](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="007d2-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="007d2-126">Para remover um diretório, consulte [Excluir um Conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="007d2-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="007d2-127">[Alterar a filtragem de domínio e de unidade organizacional](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="007d2-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="007d2-128">Remova a filtragem de grupo.</span><span class="sxs-lookup"><span data-stu-id="007d2-128">Remove Group filtering.</span></span>
* <span data-ttu-id="007d2-129">[Alterar recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="007d2-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="007d2-130">As outras opções de instalação inicial não podem ser alteradas e não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="007d2-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="007d2-131">Essas opções são:</span><span class="sxs-lookup"><span data-stu-id="007d2-131">These options are:</span></span>

* <span data-ttu-id="007d2-132">Altere o atributo a ser usado para userPrincipalName e sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="007d2-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="007d2-133">Altere o método de ingresso para objetos de uma floresta diferente.</span><span class="sxs-lookup"><span data-stu-id="007d2-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="007d2-134">Habilite a filtragem baseada em grupo.</span><span class="sxs-lookup"><span data-stu-id="007d2-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="007d2-135">Atualizar esquema de diretório</span><span class="sxs-lookup"><span data-stu-id="007d2-135">Refresh directory schema</span></span>
<span data-ttu-id="007d2-136">Essa opção é usada se você alterou o esquema em uma das suas florestas do AD DS locais.</span><span class="sxs-lookup"><span data-stu-id="007d2-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="007d2-137">Por exemplo você pode ter instalado o Exchange ou atualizado para um esquema do Windows Server 2012 com objetos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="007d2-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="007d2-138">Nesse caso, você precisa instruir o Azure AD Connect para ler o esquema novamente do AD DS e atualizar seu cache.</span><span class="sxs-lookup"><span data-stu-id="007d2-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="007d2-139">Essa ação também regenera as Regras de Sincronização.</span><span class="sxs-lookup"><span data-stu-id="007d2-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="007d2-140">Se você adicionar o esquema do Exchange, por exemplo, as Regras de Sincronização para o Exchange serão adicionadas à configuração.</span><span class="sxs-lookup"><span data-stu-id="007d2-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="007d2-141">Quando você seleciona essa opção, todos os diretórios na sua configuração são listados.</span><span class="sxs-lookup"><span data-stu-id="007d2-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="007d2-142">Você pode manter a configuração padrão e atualizar todas as florestas ou desmarcar algumas delas.</span><span class="sxs-lookup"><span data-stu-id="007d2-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Página com uma lista de todos os diretórios no ambiente](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="007d2-144">Configurar modo de preparo</span><span class="sxs-lookup"><span data-stu-id="007d2-144">Configure staging mode</span></span>
<span data-ttu-id="007d2-145">Essa opção permite habilitar e desabilitar o modo de preparo no servidor.</span><span class="sxs-lookup"><span data-stu-id="007d2-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="007d2-146">Encontre mais informações sobre o modo de preparo e como ele é usado em [Operações](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="007d2-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="007d2-147">A opção mostra se o teste está habilitado ou desabilitado atualmente: </span><span class="sxs-lookup"><span data-stu-id="007d2-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Opção que também está mostrando o estado atual do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="007d2-149">Para alterar o estado, selecione essa opção e marque ou desmarque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="007d2-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Opção que também está mostrando o estado atual do modo de preparo](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="007d2-151">Alterar a entrada do usuário</span><span class="sxs-lookup"><span data-stu-id="007d2-151">Change user sign-in</span></span>
<span data-ttu-id="007d2-152">Esta opção permite mudar da sincronização de senha para federação ou o oposto.</span><span class="sxs-lookup"><span data-stu-id="007d2-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="007d2-153">Você não pode alterar para **não configurar**.</span><span class="sxs-lookup"><span data-stu-id="007d2-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="007d2-154">Para obter mais informações sobre essa opção, consulte [entrada do usuário](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="007d2-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="007d2-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="007d2-155">Next steps</span></span>
* <span data-ttu-id="007d2-156">Saiba mais sobre o modelo de configuração usado pela sincronização do Azure AD Connect em [Noções básicas do provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="007d2-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="007d2-157">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="007d2-157">**Overview topics**</span></span>

* [<span data-ttu-id="007d2-158">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="007d2-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="007d2-159">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="007d2-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
