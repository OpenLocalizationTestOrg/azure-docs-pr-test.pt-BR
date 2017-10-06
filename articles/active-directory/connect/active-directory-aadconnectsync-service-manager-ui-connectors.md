---
title: "aaaConnectors em hello Azure o Gerenciador de serviço de sincronização do AD UI | Microsoft Docs"
description: "Entenda o guia conectores Olá Olá Synchronization Service Manager para conexão do AD do Azure."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="e9799-103">Usando conectores com hello Azure AD Connect sincronização Service Manager</span><span class="sxs-lookup"><span data-stu-id="e9799-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="e9799-105">Guia de conectores Olá é usado toomanage todos os mecanismos de sincronização de saudação sistemas está conectado ao.</span><span class="sxs-lookup"><span data-stu-id="e9799-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="e9799-106">Ações do Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-106">Connector actions</span></span>
| <span data-ttu-id="e9799-107">Ação</span><span class="sxs-lookup"><span data-stu-id="e9799-107">Action</span></span> | <span data-ttu-id="e9799-108">Comentário</span><span class="sxs-lookup"><span data-stu-id="e9799-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="e9799-109">Criação</span><span class="sxs-lookup"><span data-stu-id="e9799-109">Create</span></span> |<span data-ttu-id="e9799-110">Não use.</span><span class="sxs-lookup"><span data-stu-id="e9799-110">Do not use.</span></span> <span data-ttu-id="e9799-111">Para conectar-se tooadditional AD florestas, use o Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9799-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="e9799-112">Propriedades</span><span class="sxs-lookup"><span data-stu-id="e9799-112">Properties</span></span> |<span data-ttu-id="e9799-113">Usado para filtragem de domínio e de UO.</span><span class="sxs-lookup"><span data-stu-id="e9799-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="e9799-114">Excluir</span><span class="sxs-lookup"><span data-stu-id="e9799-114">Delete</span></span>](#delete) |<span data-ttu-id="e9799-115">Tooeither usado excluir dados de Olá Olá conector espaço ou toodelete conexão tooa floresta.</span><span class="sxs-lookup"><span data-stu-id="e9799-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="e9799-116">Configurar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="e9799-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="e9799-117">Exceto para o domínio de filtragem, nada tooconfigure aqui.</span><span class="sxs-lookup"><span data-stu-id="e9799-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="e9799-118">Você pode usar essa ação perfis de execução toosee já configurado.</span><span class="sxs-lookup"><span data-stu-id="e9799-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="e9799-119">Executar</span><span class="sxs-lookup"><span data-stu-id="e9799-119">Run</span></span> |<span data-ttu-id="e9799-120">Usado toostart um one-off executado de um perfil.</span><span class="sxs-lookup"><span data-stu-id="e9799-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="e9799-121">Parar</span><span class="sxs-lookup"><span data-stu-id="e9799-121">Stop</span></span> |<span data-ttu-id="e9799-122">Interrompe um Conector que, atualmente, executa um perfil.</span><span class="sxs-lookup"><span data-stu-id="e9799-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="e9799-123">Exportar Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-123">Export Connector</span></span> |<span data-ttu-id="e9799-124">Não use.</span><span class="sxs-lookup"><span data-stu-id="e9799-124">Do not use.</span></span> |
| <span data-ttu-id="e9799-125">Importar Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-125">Import Connector</span></span> |<span data-ttu-id="e9799-126">Não use.</span><span class="sxs-lookup"><span data-stu-id="e9799-126">Do not use.</span></span> |
| <span data-ttu-id="e9799-127">Atualizar Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-127">Update Connector</span></span> |<span data-ttu-id="e9799-128">Não use.</span><span class="sxs-lookup"><span data-stu-id="e9799-128">Do not use.</span></span> |
| <span data-ttu-id="e9799-129">Atualizar Esquema</span><span class="sxs-lookup"><span data-stu-id="e9799-129">Refresh Schema</span></span> |<span data-ttu-id="e9799-130">Atualiza o esquema em cache hello.</span><span class="sxs-lookup"><span data-stu-id="e9799-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="e9799-131">É preferencial toouse Olá opção no Assistente de instalação de saudação em vez disso, desde que também atualizações sincronizar regras.</span><span class="sxs-lookup"><span data-stu-id="e9799-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="e9799-132">Pesquisar Espaço do Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="e9799-133">Toofind objetos usados e muito[siga um objeto e seus dados por meio do sistema Olá](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="e9799-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="e9799-134">Exclusão</span><span class="sxs-lookup"><span data-stu-id="e9799-134">Delete</span></span>
<span data-ttu-id="e9799-135">ação de exclusão de saudação é usada para duas coisas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e9799-135">hello delete action is used for two different things.</span></span>  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="e9799-137">Olá opção **excluir apenas o espaço do conector** remove todos os dados, mas manter Olá configuração.</span><span class="sxs-lookup"><span data-stu-id="e9799-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="e9799-138">Olá opção **espaço do conector e excluir o conector** remove dados saudação e configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9799-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="e9799-139">Essa opção é usada quando você não deseja tooconnect tooa floresta mais.</span><span class="sxs-lookup"><span data-stu-id="e9799-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="e9799-140">Ambas as opções sincronizar todos os objetos e atualizar objetos do metaverso hello.</span><span class="sxs-lookup"><span data-stu-id="e9799-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="e9799-141">Essa ação é uma operação demorada.</span><span class="sxs-lookup"><span data-stu-id="e9799-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="e9799-142">Configurar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="e9799-142">Configure Run Profiles</span></span>
<span data-ttu-id="e9799-143">Essa opção permite que você toosee Olá perfis configurados para um conector de execução.</span><span class="sxs-lookup"><span data-stu-id="e9799-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="e9799-145">Pesquisar Espaço do Conector</span><span class="sxs-lookup"><span data-stu-id="e9799-145">Search Connector Space</span></span>
<span data-ttu-id="e9799-146">ação de espaço de conector de pesquisa de saudação é útil toofind objetos e solucionar problemas de dados.</span><span class="sxs-lookup"><span data-stu-id="e9799-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="e9799-148">Comece selecionando um **escopo**.</span><span class="sxs-lookup"><span data-stu-id="e9799-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="e9799-149">Você pode procurar dados com base em (RDN, DN, âncora, subárvore), ou de estado do objeto de saudação (todas as outras opções).</span><span class="sxs-lookup"><span data-stu-id="e9799-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="e9799-150">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="e9799-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="e9799-151">Por exemplo, se fizer uma pesquisa em Subárvore, você obterá todos os objetos em uma UO.</span><span class="sxs-lookup"><span data-stu-id="e9799-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="e9799-152">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="e9799-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="e9799-153">Dessa grade, você pode selecionar um objeto, selecione **propriedades**, e [segui-la](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) do espaço do conector Olá origem, por meio de metaverso Olá e toohello espaço do conector de destino.</span><span class="sxs-lookup"><span data-stu-id="e9799-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="e9799-154">Alterar a senha da conta Olá AD DS</span><span class="sxs-lookup"><span data-stu-id="e9799-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="e9799-155">Se você alterar a senha da conta Olá, Olá serviço de sincronização deixará de ser capaz de tooimport/exportação tooon alterações locais AD.</span><span class="sxs-lookup"><span data-stu-id="e9799-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="e9799-156">Você pode ver o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e9799-156">You may see hello following:</span></span>

- <span data-ttu-id="e9799-157">etapa de importação/exportação Olá para Olá conector AD falha com erro de "credenciais de início não".</span><span class="sxs-lookup"><span data-stu-id="e9799-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="e9799-158">Em Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com o evento ID 6000 e a mensagem "Olá toorun de agente"contoso.com"falhado de gerenciamento porque as credenciais de saudação eram inválidas."</span><span class="sxs-lookup"><span data-stu-id="e9799-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="e9799-159">Olá tooresolve emitir, conta de usuário Olá AD DS de atualização usando Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="e9799-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="e9799-160">Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).</span><span class="sxs-lookup"><span data-stu-id="e9799-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="e9799-161">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="e9799-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="e9799-162">Vá toohello **conectores** guia.</span><span class="sxs-lookup"><span data-stu-id="e9799-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="e9799-163">Selecione Olá conector do AD que é configurado toouse hello conta AD DS.</span><span class="sxs-lookup"><span data-stu-id="e9799-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="e9799-164">Em Ações, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e9799-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="e9799-165">Na caixa de diálogo pop-up Olá, selecione conectar tooActive diretório floresta:</span><span class="sxs-lookup"><span data-stu-id="e9799-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="e9799-166">nome da floresta Olá indica Olá correspondente local AD.</span><span class="sxs-lookup"><span data-stu-id="e9799-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="e9799-167">nome de usuário de saudação indica a conta do hello AD DS usada para sincronização.</span><span class="sxs-lookup"><span data-stu-id="e9799-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="e9799-168">Digite hello nova senha da conta do hello AD DS na caixa de texto de senha Olá ![do Azure AD conectar-se sincronização criptografia de chave de utilitário](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="e9799-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="e9799-169">Clique em nova senha do toosave Okey hello e reinicie Olá serviço de sincronização tooremove Olá senha antiga do cache de memória.</span><span class="sxs-lookup"><span data-stu-id="e9799-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e9799-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9799-170">Next steps</span></span>
<span data-ttu-id="e9799-171">Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.</span><span class="sxs-lookup"><span data-stu-id="e9799-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e9799-172">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e9799-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
