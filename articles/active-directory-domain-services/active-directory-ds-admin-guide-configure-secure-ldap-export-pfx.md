---
title: "Configurar o LDAP Seguro (LDAPS) nos Serviços de Domínio do Azure AD |Microsoft Docs"
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
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="32685-103">Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="32685-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32685-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="32685-104">Before you begin</span></span>
<span data-ttu-id="32685-105">Não deixe de concluir a [Tarefa 1 – obter um certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="32685-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="32685-106">Tarefa 2 – exportar o certificado LDAP seguro para um arquivo .PFX</span><span class="sxs-lookup"><span data-stu-id="32685-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="32685-107">Antes de iniciar esta tarefa, verifique se você obteve o certificado LDAP seguro de sua autoridade de certificação pública ou se criou um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="32685-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="32685-108">Execute as etapas a seguir para exportar o certificado LDAPS para um arquivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="32685-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="32685-109">Pressione o botão **Iniciar** e digite **R**. Na caixa de diálogo **Executar**, digite **mmc** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="32685-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Iniciar o console do MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="32685-111">No prompt **Controle de Conta de Usuário**, clique em **SIM** para iniciar o MMC (Console de Gerenciamento Microsoft) como administrador.</span><span class="sxs-lookup"><span data-stu-id="32685-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="32685-112">No menu **Arquivo**, clique em **Adicionar/Remover Snap-in...**.</span><span class="sxs-lookup"><span data-stu-id="32685-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Adicionar snap-in ao console do MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="32685-114">Na caixa de diálogo **Adicionar ou Remover Snap-ins**, escolha o snap-in **Certificados** e clique no botão **Adicionar >**.</span><span class="sxs-lookup"><span data-stu-id="32685-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Adicionar snap-in de certificados ao console do MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="32685-116">No assistente do **Snap-in de certificados**, escolha **Conta de computador** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="32685-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Adicionar snap-in de certificados à conta do computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="32685-118">Na página **Selecionar Computador**, escolha **Computador local: (o computador no qual este console está sendo executado)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="32685-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Adicionar snap-in de certificados - escolher computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="32685-120">Na caixa de diálogo **Adicionar ou Remover Snap-ins**, clique em **OK** para adicionar o snap-in de certificados ao MMC.</span><span class="sxs-lookup"><span data-stu-id="32685-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Adicionar snap-in de certificados ao MMC - concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="32685-122">Na janela do MMC, clique para expandir **Raiz do Console**.</span><span class="sxs-lookup"><span data-stu-id="32685-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="32685-123">Você deve ver o snap-in de Certificados carregado.</span><span class="sxs-lookup"><span data-stu-id="32685-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="32685-124">Clique em **Certificados (Computador Local)** para expandir.</span><span class="sxs-lookup"><span data-stu-id="32685-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="32685-125">Clique para expandir o nó **Pessoal**, seguido pelo nó **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="32685-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Abrir repositório de certificados pessoais](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="32685-127">Você deve ver o certificado autoassinado que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="32685-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="32685-128">É possível examinar as propriedades do certificado para garantir que a impressão digital corresponda àquela relatada nas janelas do PowerShell quando você criou o certificado.</span><span class="sxs-lookup"><span data-stu-id="32685-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="32685-129">Escolha o certificado autoassinado e **clique com o botão direito do mouse**.</span><span class="sxs-lookup"><span data-stu-id="32685-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="32685-130">No menu de clique com o botão direito do mouse, escolha **Todas as Tarefas** e **Exportar...**.</span><span class="sxs-lookup"><span data-stu-id="32685-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportar o certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="32685-132">No **Assistente para Exportação de Certificados**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="32685-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Assistente de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="32685-134">Na página **Exportar Chave Privada**, escolha **Sim, exporte a chave privada** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="32685-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Chave privada de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="32685-136">Você DEVE exportar a chave privada junto com o certificado.</span><span class="sxs-lookup"><span data-stu-id="32685-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="32685-137">Se você fornecer um PFX que não contém a chave privada do certificado, a habilitação do LDAP seguro para seu domínio gerenciado falhará.</span><span class="sxs-lookup"><span data-stu-id="32685-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="32685-138">Na página **Exportar Formato de Arquivo**, escolha **Personal Information Exchange – PKCS #12 (.PFX)** como o formato de arquivo para o certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="32685-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Formato de arquivo de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="32685-140">Somente o formato de arquivo .PFX tem suporte.</span><span class="sxs-lookup"><span data-stu-id="32685-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="32685-141">Não exporte o certificado para o formato de arquivo .CER.</span><span class="sxs-lookup"><span data-stu-id="32685-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="32685-142">Na página **Segurança**, escolha a opção **Senha** e digite uma senha para proteger o arquivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="32685-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="32685-143">Guarde essa senha, pois ela será necessária na próxima tarefa.</span><span class="sxs-lookup"><span data-stu-id="32685-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="32685-144">Clique em **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="32685-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="32685-145">Senha para exportação de certificado</span><span class="sxs-lookup"><span data-stu-id="32685-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="32685-146">Anote essa senha.</span><span class="sxs-lookup"><span data-stu-id="32685-146">Make a note of this password.</span></span> <span data-ttu-id="32685-147">Você precisará dela ao habilitar o LDAP seguro para este domínio gerenciado na [Tarefa 3 – habilitar o LDAP seguro para o domínio gerenciado](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="32685-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="32685-148">Na página **Arquivo a ser Exportado** , especifique o nome do arquivo e o local para onde você deseja exportar o certificado.</span><span class="sxs-lookup"><span data-stu-id="32685-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Caminho para exportação de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="32685-150">Na página seguinte, clique em **Concluir** para exportar o certificado para um arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="32685-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="32685-151">Você verá o diálogo de confirmação quando o certificado tiver sido exportado.</span><span class="sxs-lookup"><span data-stu-id="32685-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Exportar certificado concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="32685-153">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="32685-153">Next step</span></span>
[<span data-ttu-id="32685-154">Tarefa 3 – habilitar o LDAP seguro para o domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="32685-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
