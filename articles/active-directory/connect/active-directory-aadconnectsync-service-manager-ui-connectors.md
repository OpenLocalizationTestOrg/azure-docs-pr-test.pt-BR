---
title: "Conectores na Sincronização do Azure AD Connect: interface de usuário do Synchronization Service Manager | Microsoft Docs"
description: Entenda como usar a guia Conectores no Synchronization Service Manager para o Azure AD Connect.
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
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="dd29e-103">Usando conectores com o Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="dd29e-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="dd29e-105">A guia Conectores é usada para gerenciar todos os sistemas aos quais o mecanismo de sincronização está conectado.</span><span class="sxs-lookup"><span data-stu-id="dd29e-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="dd29e-106">Ações do Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-106">Connector actions</span></span>
| <span data-ttu-id="dd29e-107">Ação</span><span class="sxs-lookup"><span data-stu-id="dd29e-107">Action</span></span> | <span data-ttu-id="dd29e-108">Comentário</span><span class="sxs-lookup"><span data-stu-id="dd29e-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="dd29e-109">Criação</span><span class="sxs-lookup"><span data-stu-id="dd29e-109">Create</span></span> |<span data-ttu-id="dd29e-110">Não use.</span><span class="sxs-lookup"><span data-stu-id="dd29e-110">Do not use.</span></span> <span data-ttu-id="dd29e-111">Para se conectar a florestas adicionais do AD, use o assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="dd29e-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="dd29e-112">Propriedades</span><span class="sxs-lookup"><span data-stu-id="dd29e-112">Properties</span></span> |<span data-ttu-id="dd29e-113">Usado para filtragem de domínio e de UO.</span><span class="sxs-lookup"><span data-stu-id="dd29e-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="dd29e-114">Excluir</span><span class="sxs-lookup"><span data-stu-id="dd29e-114">Delete</span></span>](#delete) |<span data-ttu-id="dd29e-115">Usado para excluir os dados no espaço do conector ou para excluir a conexão a uma floresta.</span><span class="sxs-lookup"><span data-stu-id="dd29e-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="dd29e-116">Configurar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="dd29e-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="dd29e-117">Com exceção do domínio de filtragem, não há nada a ser configurado aqui.</span><span class="sxs-lookup"><span data-stu-id="dd29e-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="dd29e-118">Você pode usar essa ação para ver os perfis de execução já configurados.</span><span class="sxs-lookup"><span data-stu-id="dd29e-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="dd29e-119">Executar</span><span class="sxs-lookup"><span data-stu-id="dd29e-119">Run</span></span> |<span data-ttu-id="dd29e-120">Usado para iniciar uma execução única de um perfil.</span><span class="sxs-lookup"><span data-stu-id="dd29e-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="dd29e-121">Parar</span><span class="sxs-lookup"><span data-stu-id="dd29e-121">Stop</span></span> |<span data-ttu-id="dd29e-122">Interrompe um Conector que, atualmente, executa um perfil.</span><span class="sxs-lookup"><span data-stu-id="dd29e-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="dd29e-123">Exportar Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-123">Export Connector</span></span> |<span data-ttu-id="dd29e-124">Não use.</span><span class="sxs-lookup"><span data-stu-id="dd29e-124">Do not use.</span></span> |
| <span data-ttu-id="dd29e-125">Importar Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-125">Import Connector</span></span> |<span data-ttu-id="dd29e-126">Não use.</span><span class="sxs-lookup"><span data-stu-id="dd29e-126">Do not use.</span></span> |
| <span data-ttu-id="dd29e-127">Atualizar Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-127">Update Connector</span></span> |<span data-ttu-id="dd29e-128">Não use.</span><span class="sxs-lookup"><span data-stu-id="dd29e-128">Do not use.</span></span> |
| <span data-ttu-id="dd29e-129">Atualizar Esquema</span><span class="sxs-lookup"><span data-stu-id="dd29e-129">Refresh Schema</span></span> |<span data-ttu-id="dd29e-130">Atualiza o esquema em cache.</span><span class="sxs-lookup"><span data-stu-id="dd29e-130">Refreshes the cached schema.</span></span> <span data-ttu-id="dd29e-131">É preferível usar a opção no assistente de instalação, já que ela também atualiza as regras de sincronização.</span><span class="sxs-lookup"><span data-stu-id="dd29e-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="dd29e-132">Pesquisar Espaço do Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="dd29e-133">Usado para encontrar objetos e [Seguir um objeto e seus dados por meio do sistema](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="dd29e-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="dd29e-134">Excluir</span><span class="sxs-lookup"><span data-stu-id="dd29e-134">Delete</span></span>
<span data-ttu-id="dd29e-135">A ação de exclusão é usada com duas finalidades diferentes.</span><span class="sxs-lookup"><span data-stu-id="dd29e-135">The delete action is used for two different things.</span></span>  
![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="dd29e-137">A opção **Excluir apenas o espaço do conector** remove todos os dados, mas mantém a configuração.</span><span class="sxs-lookup"><span data-stu-id="dd29e-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="dd29e-138">A opção **Excluir Conector e Espaço** remove os dados e a configuração.</span><span class="sxs-lookup"><span data-stu-id="dd29e-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="dd29e-139">Essa opção é usada quando você não deseja mais se conectar a uma floresta.</span><span class="sxs-lookup"><span data-stu-id="dd29e-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="dd29e-140">Ambas as opções sincronizam todos os objetos e atualizam os objetos do metaverso.</span><span class="sxs-lookup"><span data-stu-id="dd29e-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="dd29e-141">Essa ação é uma operação demorada.</span><span class="sxs-lookup"><span data-stu-id="dd29e-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="dd29e-142">Configurar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="dd29e-142">Configure Run Profiles</span></span>
<span data-ttu-id="dd29e-143">Esta opção permite que você veja os perfis de execução configurados para um Conector.</span><span class="sxs-lookup"><span data-stu-id="dd29e-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="dd29e-145">Pesquisar Espaço do Conector</span><span class="sxs-lookup"><span data-stu-id="dd29e-145">Search Connector Space</span></span>
<span data-ttu-id="dd29e-146">A ação de espaço do conector de pesquisa é útil para encontrar objetos e solucionar problemas de dados.</span><span class="sxs-lookup"><span data-stu-id="dd29e-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="dd29e-148">Comece selecionando um **escopo**.</span><span class="sxs-lookup"><span data-stu-id="dd29e-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="dd29e-149">É possível pesquisar com base nos dados (RDN, DN, Âncora, Subárvore) ou no estado do objeto (todas as outras opções).</span><span class="sxs-lookup"><span data-stu-id="dd29e-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="dd29e-150">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="dd29e-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="dd29e-151">Por exemplo, se fizer uma pesquisa em Subárvore, você obterá todos os objetos em uma UO.</span><span class="sxs-lookup"><span data-stu-id="dd29e-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="dd29e-152">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="dd29e-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="dd29e-153">Nessa grade, é possível selecionar um objeto, selecionar **propriedades** e [segui-lo](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) do espaço conector de origem, passando pelo metaverso, até o espaço conector de destino.</span><span class="sxs-lookup"><span data-stu-id="dd29e-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="dd29e-154">Alterando a senha da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="dd29e-154">Changing the AD DS account password</span></span>
<span data-ttu-id="dd29e-155">Se você alterar a senha da conta, o Serviço de Sincronização não poderá mais importar/exportar alterações para o AD local.</span><span class="sxs-lookup"><span data-stu-id="dd29e-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="dd29e-156">Você poderá ver o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd29e-156">You may see the following:</span></span>

- <span data-ttu-id="dd29e-157">A etapa de importação/exportação do conector do AD falha com o erro “no-start-credentials”.</span><span class="sxs-lookup"><span data-stu-id="dd29e-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="dd29e-158">No Visualizador de Eventos do Windows, o log de eventos do aplicativo contém um erro com a ID do Evento 6000 e a mensagem “O agente de gerenciamento "contoso.com" não foi executado porque as credenciais eram inválidas”.</span><span class="sxs-lookup"><span data-stu-id="dd29e-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="dd29e-159">Para resolver o problema, atualize a conta de usuário do AD DS usando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd29e-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="dd29e-160">Inicie o Synchronization Service Manager (INICIAR → Serviço de Sincronização).</span><span class="sxs-lookup"><span data-stu-id="dd29e-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="dd29e-161">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="dd29e-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="dd29e-162">Vá para a guia **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="dd29e-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="dd29e-163">Selecione o Conector do AD que está configurado para usar a conta do AD DS.</span><span class="sxs-lookup"><span data-stu-id="dd29e-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="dd29e-164">Em Ações, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dd29e-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="dd29e-165">Na caixa de diálogo pop-up, selecione Conectar-se à Floresta do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="dd29e-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="dd29e-166">O Nome da floresta indica o AD local correspondente.</span><span class="sxs-lookup"><span data-stu-id="dd29e-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="dd29e-167">O Nome de usuário indica a conta do AD DS usada para sincronização.</span><span class="sxs-lookup"><span data-stu-id="dd29e-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="dd29e-168">Insira a nova senha da conta do AD DS na caixa de texto ![Utilitário de Chave de Criptografia de Sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png) da Senha</span><span class="sxs-lookup"><span data-stu-id="dd29e-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="dd29e-169">Clique em OK para salvar a nova senha e reinicie o Serviço de Sincronização para remover a senha antiga do cache de memória.</span><span class="sxs-lookup"><span data-stu-id="dd29e-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="dd29e-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd29e-170">Next steps</span></span>
<span data-ttu-id="dd29e-171">Saiba mais sobre a configuração de [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="dd29e-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="dd29e-172">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="dd29e-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
