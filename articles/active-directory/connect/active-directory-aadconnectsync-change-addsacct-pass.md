---
title: "Sincronização do Azure AD Connect: alterando a senha da conta do AD DS | Microsoft Docs"
description: "Este documento de tópico descreve como atualizar o Azure AD Connect depois que a senha da conta do AD DS é alterada."
services: active-directory
keywords: Conta do AD DS, conta do Active Directory, senha
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="6230a-104">Alterando a senha da conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="6230a-104">Changing the AD DS account password</span></span>
<span data-ttu-id="6230a-105">A conta do AD DS refere-se à conta de usuário usada pelo Azure AD Connect para se comunicar com o Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="6230a-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="6230a-106">Se você alterar a senha da conta do AD DS, será necessário atualizar o Azure AD Connect Synchronization Service com a nova senha.</span><span class="sxs-lookup"><span data-stu-id="6230a-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="6230a-107">Caso contrário, o serviço não poderá mais sincronizar corretamente com o Active Directory local e você encontrará os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="6230a-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="6230a-108">No Synchronization Service Manager, qualquer operação de importação ou de exportação com o AD local falha com o erro **no-start-credentials**.</span><span class="sxs-lookup"><span data-stu-id="6230a-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="6230a-109">No Visualizador de Eventos do Windows, o log de eventos do aplicativo contém um erro com **ID do evento 6000** e com a mensagem **'O agente de gerenciamento "contoso.com" falhou, porque as credenciais eram inválidas'**.</span><span class="sxs-lookup"><span data-stu-id="6230a-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="6230a-110">Como atualizar o Synchronization Service com a nova senha de conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="6230a-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="6230a-111">Para atualizar o Synchronization Service com a nova senha:</span><span class="sxs-lookup"><span data-stu-id="6230a-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="6230a-112">Inicie o Synchronization Service Manager (INICIAR → Serviço de Sincronização).</span><span class="sxs-lookup"><span data-stu-id="6230a-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="6230a-113">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="6230a-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="6230a-114">Vá para a guia **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="6230a-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="6230a-115">Selecione o **Conector AD** que corresponde à conta do AD DS para a qual a sua senha foi alterada.</span><span class="sxs-lookup"><span data-stu-id="6230a-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="6230a-116">Em **Ações**, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6230a-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="6230a-117">Na caixa de diálogo pop-up, selecione **Conectar-se à Floresta do Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="6230a-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="6230a-118">Insira a nova senha da conta do AD DS na caixa de texto **Senha**.</span><span class="sxs-lookup"><span data-stu-id="6230a-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="6230a-119">Clique em **OK** para salvar a nova senha e fechar a caixa de diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="6230a-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="6230a-120">Reinicie o Azure AD Connect Synchronization Service no Gerenciador de Controle de Serviço Windows.</span><span class="sxs-lookup"><span data-stu-id="6230a-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="6230a-121">Isso é para garantir que qualquer referência à senha antiga é removida do cache de memória.</span><span class="sxs-lookup"><span data-stu-id="6230a-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6230a-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6230a-122">Next steps</span></span>
<span data-ttu-id="6230a-123">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="6230a-123">**Overview topics**</span></span>

* [<span data-ttu-id="6230a-124">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="6230a-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="6230a-125">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6230a-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
