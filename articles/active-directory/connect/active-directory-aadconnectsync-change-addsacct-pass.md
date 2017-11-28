---
title: "Sincronização do Azure AD Connect: alterar senha da conta Olá AD DS | Microsoft Docs"
description: "Este documento de tópico descreve como tooupdate do Azure AD Connect após a senha de saudação da conta de saudação AD DS é alterada."
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="4058d-104">Alterar a senha da conta Olá AD DS</span><span class="sxs-lookup"><span data-stu-id="4058d-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="4058d-105">conta do Hello AD DS refere-se a conta de usuário toohello usada pelo Azure AD Connect toocommunicate com o Active Directory no local.</span><span class="sxs-lookup"><span data-stu-id="4058d-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="4058d-106">Se você alterar a senha Olá Olá conta AD DS, você deve atualizar o serviço de sincronização se conectar do Azure AD com hello nova senha.</span><span class="sxs-lookup"><span data-stu-id="4058d-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="4058d-107">Caso contrário, Olá que sincronização não poderá sincronizar corretamente com hello Active Directory local e você encontrará Olá os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="4058d-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="4058d-108">Em Olá operação do Gerenciador de serviço de sincronização, nenhuma importação ou exportação com local AD falha com **credenciais de início não** erro.</span><span class="sxs-lookup"><span data-stu-id="4058d-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="4058d-109">No Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com **evento ID 6000** e mensagem **'Agente de gerenciamento hello "contoso.com" com falha toorun porque as credenciais de saudação eram inválidas'** .</span><span class="sxs-lookup"><span data-stu-id="4058d-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="4058d-110">Como tooupdate Olá o serviço de sincronização com a nova senha para a conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="4058d-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="4058d-111">Olá tooupdate serviço de sincronização com a nova senha hello:</span><span class="sxs-lookup"><span data-stu-id="4058d-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="4058d-112">Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).</span><span class="sxs-lookup"><span data-stu-id="4058d-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="4058d-113">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="4058d-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="4058d-114">Vá toohello **conectores** guia.</span><span class="sxs-lookup"><span data-stu-id="4058d-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="4058d-115">Selecione Olá **conector AD** que corresponde a conta do toohello AD DS para que sua senha foi alterada.</span><span class="sxs-lookup"><span data-stu-id="4058d-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="4058d-116">Em **Ações**, selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="4058d-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="4058d-117">Na caixa de diálogo pop-up hello, selecione **conectar-se a floresta do diretório tooActive**:</span><span class="sxs-lookup"><span data-stu-id="4058d-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="4058d-118">Insira Olá nova senha da conta de saudação AD DS no hello **senha** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4058d-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="4058d-119">Clique em **Okey** toosave Olá nova senha e a caixa de diálogo pop-up Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="4058d-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="4058d-120">Reinicialização hello Azure AD conectar serviço de sincronização no Gerenciador de controle de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="4058d-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="4058d-121">Isso é tooensure que qualquer senha antiga de toohello de referência é removida do cache de memória de saudação.</span><span class="sxs-lookup"><span data-stu-id="4058d-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4058d-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4058d-122">Next steps</span></span>
<span data-ttu-id="4058d-123">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="4058d-123">**Overview topics**</span></span>

* [<span data-ttu-id="4058d-124">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="4058d-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="4058d-125">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4058d-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
