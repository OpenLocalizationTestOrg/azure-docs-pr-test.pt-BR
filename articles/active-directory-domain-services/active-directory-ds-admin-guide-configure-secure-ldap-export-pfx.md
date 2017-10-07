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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services

## <a name="before-you-begin"></a>Antes de começar
Não deixe de concluir a [Tarefa 1 – obter um certificado para LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Tarefa 2: exportar Olá seguro LDAP certificado tooa. Arquivo PFX
Antes de começar essa tarefa, certifique-se de que você obteve o certificado LDAP seguro de saudação de uma autoridade de certificação pública ou criar um certificado autoassinado.

Executar Olá etapas a seguir, tooexport Olá LDAPS tooa do certificado. Arquivo PFX.

1. Olá pressione **iniciar** e digite **R**. Em Olá **executar** caixa de diálogo, digite **mmc** e clique em **Okey**.

    ![Inicie o console do MMC Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Em Olá **User Account Control** , clique em **Sim** toolaunch MMC (Console de gerenciamento Microsoft) como administrador.
3. De saudação **arquivo** menu, clique em **Adicionar/Remover Snap-in...** .

    ![Adicionar o console do snap-in tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. Em Olá **adicionar ou Remover Snap-ins** caixa de diálogo, selecione Olá **certificados** snap-in e clique em Olá **Adicionar >** botão.

    ![Adicionar certificados tooMMC snap-in do console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. Em Olá **snap-in de certificados** assistente, selecione **conta de computador** e clique em **próximo**.

    ![Adicionar snap-in de certificados à conta do computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Em Olá **Selecionar computador** , selecione **computador Local: (Olá computador em que este console está sendo executado)** e clique em **concluir**.

    ![Adicionar snap-in de certificados - escolher computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. Em Olá **adicionar ou Remover Snap-ins** caixa de diálogo, clique em **Okey** tooadd Olá certificados snap-in tooMMC.

    ![Adicionar o certificados snap-in tooMMC - concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Na janela do MMC hello, clique em tooexpand **raiz do Console**. Você deve ver Olá snap-in de certificados carregados. Clique em **certificados (computador Local)** tooexpand. Clique em Olá tooexpand **pessoal** nó, seguido por Olá **certificados** nó.

    ![Abrir repositório de certificados pessoais](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Você deve ver o certificado autoassinado hello, criamos. Você pode examinar as propriedades de Olá Olá certificado tooensure Olá impressão digital de correspondências de que em janelas do PowerShell hello quando você criou o certificado de saudação.
10. Selecione Olá certificado autoassinado e **clique direito**. No menu de atalho hello, selecione **todas as tarefas** e selecione **exportar...** .

    ![Exportar o certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. Em Olá **Assistente para exportação de certificados**, clique em **próximo**.

    ![Assistente de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Em Olá **Exportar chave privada** página, selecione **Sim, exportar a chave privada Olá**e clique em **próximo**.

    ![Chave privada de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > Você deve exportar chave privada de saudação junto com o certificado de saudação. Se você fornecer um PFX que contém a chave privada Olá certificado Olá, habilitar LDAP seguro para seu domínio gerenciado falhará.
    >
    >
13. Em Olá **formato do arquivo de exportação** página, selecione **troca de informações pessoais - PKCS #12 (. PFX)** como formato de arquivo de saudação do hello o certificado exportado.

    ![Formato de arquivo de Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Somente hello. Há suporte para o formato do arquivo PFX. Não exporte Olá toohello de certificado. Formato de arquivo CER.
    >
    >
14. Em Olá **segurança** página, selecione Olá **senha** opção e digite uma saudação tooprotect de senha. Arquivo PFX. Guarde essa senha, pois ele será necessário na próxima tarefa de saudação. Clique em **próximo** tooproceed.

    ![Senha para exportação de certificado ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Anote essa senha. Necessário ao habilitar o LDAP seguro para este domínio gerenciado no [tarefa 3: habilitar o LDAP seguro para o domínio gerenciado Olá](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Em Olá **tooExport arquivo** , especifique o nome do arquivo hello e o local onde deseja que o certificado de saudação tooexport.

    ![Caminho para exportação de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. No hello após a página, clique em **concluir** arquivo PFX do tooexport Olá certificado tooa. Você deve ver a caixa de diálogo de confirmação quando Olá certificado foi exportado.

    ![Exportar certificado concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Próxima etapa
[Tarefa 3 - habilitar LDAP seguro para o domínio gerenciado Olá](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
