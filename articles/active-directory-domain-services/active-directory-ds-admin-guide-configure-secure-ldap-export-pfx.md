---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4f830-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="4f830-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4f830-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4f830-104">Before you begin</span></span>
<span data-ttu-id="4f830-105">Não deixe de concluir a [Tarefa 1 – obter um certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="4f830-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="4f830-106">Tarefa 2: exportar Olá seguro LDAP certificado tooa. Arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="4f830-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="4f830-107">Antes de começar essa tarefa, certifique-se de que você obteve o certificado LDAP seguro de saudação de uma autoridade de certificação pública ou criar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="4f830-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="4f830-108">Executar Olá etapas a seguir, tooexport Olá LDAPS tooa do certificado. Arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="4f830-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="4f830-109">Olá pressione **iniciar** e digite **R**. Em Olá **executar** caixa de diálogo, digite **mmc** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4f830-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Inicie o console do MMC Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="4f830-111">Em Olá **User Account Control** , clique em **Sim** toolaunch MMC (Console de gerenciamento Microsoft) como administrador.</span><span class="sxs-lookup"><span data-stu-id="4f830-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="4f830-112">De saudação **arquivo** menu, clique em **Adicionar/Remover Snap-in...** .</span><span class="sxs-lookup"><span data-stu-id="4f830-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Adicionar o console do snap-in tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="4f830-114">Em Olá **adicionar ou Remover Snap-ins** caixa de diálogo, selecione Olá **certificados** snap-in e clique em Olá **Adicionar >** botão.</span><span class="sxs-lookup"><span data-stu-id="4f830-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Adicionar certificados tooMMC snap-in do console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="4f830-116">Em Olá **snap-in de certificados** assistente, selecione **conta de computador** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4f830-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Adicionar snap-in de certificados à conta do computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="4f830-118">Em Olá **Selecionar computador** , selecione **computador Local: (Olá computador em que este console está sendo executado)** e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4f830-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Adicionar snap-in de certificados - escolher computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="4f830-120">Em Olá **adicionar ou Remover Snap-ins** caixa de diálogo, clique em **Okey** tooadd Olá certificados snap-in tooMMC.</span><span class="sxs-lookup"><span data-stu-id="4f830-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Adicionar o certificados snap-in tooMMC - concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="4f830-122">Na janela do MMC hello, clique em tooexpand **raiz do Console**.</span><span class="sxs-lookup"><span data-stu-id="4f830-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="4f830-123">Você deve ver Olá snap-in de certificados carregados.</span><span class="sxs-lookup"><span data-stu-id="4f830-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="4f830-124">Clique em **certificados (computador Local)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="4f830-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="4f830-125">Clique em Olá tooexpand **pessoal** nó, seguido por Olá **certificados** nó.</span><span class="sxs-lookup"><span data-stu-id="4f830-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Abrir repositório de certificados pessoais](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="4f830-127">Você deve ver o certificado autoassinado hello, criamos.</span><span class="sxs-lookup"><span data-stu-id="4f830-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="4f830-128">Você pode examinar as propriedades de Olá Olá certificado tooensure Olá impressão digital de correspondências de que em janelas do PowerShell hello quando você criou o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f830-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="4f830-129">Selecione Olá certificado autoassinado e **clique direito**.</span><span class="sxs-lookup"><span data-stu-id="4f830-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="4f830-130">No menu de atalho hello, selecione **todas as tarefas** e selecione **exportar...** .</span><span class="sxs-lookup"><span data-stu-id="4f830-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportar o certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="4f830-132">Em Olá **Assistente para exportação de certificados**, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4f830-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Assistente de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="4f830-134">Em Olá **Exportar chave privada** página, selecione **Sim, exportar a chave privada Olá**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4f830-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Chave privada de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="4f830-136">Você deve exportar chave privada de saudação junto com o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f830-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="4f830-137">Se você fornecer um PFX que contém a chave privada Olá certificado Olá, habilitar LDAP seguro para seu domínio gerenciado falhará.</span><span class="sxs-lookup"><span data-stu-id="4f830-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="4f830-138">Em Olá **formato do arquivo de exportação** página, selecione **troca de informações pessoais - PKCS #12 (. PFX)** como formato de arquivo de saudação do hello o certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="4f830-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Formato de arquivo de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="4f830-140">Somente hello. Há suporte para o formato do arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="4f830-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="4f830-141">Não exporte Olá toohello de certificado. Formato de arquivo CER.</span><span class="sxs-lookup"><span data-stu-id="4f830-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="4f830-142">Em Olá **segurança** página, selecione Olá **senha** opção e digite uma saudação tooprotect de senha. Arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="4f830-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="4f830-143">Guarde essa senha, pois ele será necessário na próxima tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f830-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="4f830-144">Clique em **próximo** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="4f830-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="4f830-145">Senha para exportação de certificado</span><span class="sxs-lookup"><span data-stu-id="4f830-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="4f830-146">Anote essa senha.</span><span class="sxs-lookup"><span data-stu-id="4f830-146">Make a note of this password.</span></span> <span data-ttu-id="4f830-147">Necessário ao habilitar o LDAP seguro para este domínio gerenciado no [tarefa 3: habilitar o LDAP seguro para o domínio gerenciado Olá](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="4f830-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="4f830-148">Em Olá **tooExport arquivo** , especifique o nome do arquivo hello e o local onde deseja que o certificado de saudação tooexport.</span><span class="sxs-lookup"><span data-stu-id="4f830-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Caminho para exportação de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="4f830-150">No hello após a página, clique em **concluir** arquivo PFX do tooexport Olá certificado tooa.</span><span class="sxs-lookup"><span data-stu-id="4f830-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="4f830-151">Você deve ver a caixa de diálogo de confirmação quando Olá certificado foi exportado.</span><span class="sxs-lookup"><span data-stu-id="4f830-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Exportar certificado concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="4f830-153">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="4f830-153">Next step</span></span>
[<span data-ttu-id="4f830-154">Tarefa 3 - habilitar LDAP seguro para o domínio gerenciado Olá</span><span class="sxs-lookup"><span data-stu-id="4f830-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
