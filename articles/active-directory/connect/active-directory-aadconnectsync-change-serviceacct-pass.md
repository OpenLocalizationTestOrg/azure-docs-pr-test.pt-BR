---
title: "Sincronização do Azure AD Connect: Alterar conta de serviço de sincronização se conectar de saudação do AD do Azure | Microsoft Docs"
description: "Este documento de tópico descreve chave de criptografia hello e como tooabandon após a senha de saudação é alterado."
services: active-directory
keywords: "Conta do serviço de sincronização do Azure AD, senha"
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Alteração da senha de conta de serviço de sincronização do hello Azure AD Connect
Se você alterar a senha da conta de serviço para o Azure AD Connect sincronização de hello, Olá serviço de sincronização não será capaz de iniciar corretamente até ter abandonado a chave de criptografia de saudação e reiniciadas a senha da conta de serviço para o Azure AD Connect sincronização de saudação. 

Como parte da saudação serviços de sincronização do Azure AD Connect, usa uma criptografia toostore chave Olá senhas hello AD DS e contas de serviço do AD do Azure.  Essas contas são criptografadas antes de serem armazenadas no banco de dados de saudação. 

Olá chave de criptografia usada é protegida usando [proteção de dados do Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI protege a chave de criptografia de saudação usando Olá **senha da conta de serviço de sincronização do hello AD do Azure Connect**. 

Se você precisar de senha da conta de serviço toochange hello, você pode usar procedimentos Olá [chave de criptografia de sincronização se conectar de saudação do AD do Azure Abandoning](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish isso.  Esses procedimentos também devem ser usados se você precisar de chave de criptografia de saudação tooabandon por qualquer motivo.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problemas que surgem da alteração da senha Olá
Há duas coisas que precisam toobe feita quando você alterar a senha da conta de serviço hello.

Primeiro, é necessário toochange senha de saudação em Olá Gerenciador de controle de serviço do Windows.  Até que esse problema seja resolvido, você verá os seguintes erros:


- Se você tentar toostart Olá serviço de sincronização no Gerenciador de controle de serviço do Windows, você recebe o erro de hello "**Windows não pôde iniciar o serviço de sincronização do AD do Microsoft Azure Olá no computador Local**". **Erro 1069: o serviço de saudação não foi iniciado devido a falha de logon tooa.** "
- Em Visualizador de eventos do Windows, o log de eventos do sistema Olá contém um erro com **7038 de ID de evento** e a mensagem "**Olá serviço ADSync foi toolog não é possível em como com senha Olá configurado no momento devido toohello seguinte erro: Olá nome de usuário ou senha está incorreta.** "

Em segundo lugar, sob condições específicas, se Olá senha for atualizada, Olá serviço de sincronização não mais recuperar chave de criptografia Olá via DPAPI. Sem a chave de criptografia Olá Olá de que serviço de sincronização não é possível descriptografar Olá senhas necessárias toosynchronize local AD e o Azure AD.
Você verá erros, como:

- No Gerenciador de controle de serviços do Windows, se você tentar toostart Olá serviço de sincronização e ele não pode recuperar a chave de criptografia de saudação falhar com o erro "* * Windows não pôde iniciar Olá Microsoft Azure AD Sync no computador Local. Para obter mais informações, examine o log de eventos do sistema de saudação. Se este é um serviço de terceiros, entre em contato com o fornecedor do serviço de saudação e consulte o código de erro específico tooservice * *-21451857952 *. "
- No Visualizador de eventos do Windows, o log de eventos do aplicativo hello contém um erro com **6028 de ID de evento** e mensagem de erro *"**não é possível acessar a chave de criptografia do servidor de saudação.* *"*

tooensure que você não recebe esses erros, siga os procedimentos de saudação em [chave de criptografia de sincronização se conectar de saudação do AD do Azure Abandoning](#abandoning-the-azure-ad-connect-sync-encryption-key) ao alterar a senha de saudação.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Chave de criptografia do Azure AD Sync conectar Olá abandoná-la
>[!IMPORTANT]
>Olá procedimentos a seguir se aplicam somente tooAzure AD Connect compilação 1.1.443.0 ou anterior.

Use Olá chave de criptografia de saudação de tooabandon procedimentos a seguir.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Quais toodo se precisar de chave de criptografia de saudação tooabandon

Se você precisar de chave de criptografia tooabandon hello, use Olá tooaccomplish procedimentos a seguir.

1. [Abandone a chave de criptografia existente Olá](#abandon-the-existing-encryption-key)

2. [Fornecer a senha Olá Olá conta AD DS](#provide-the-password-of-the-ad-ds-account)

3. [Reinicializar senha Olá Olá conta de sincronização do AD do Azure](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Saudação de iniciar o serviço de sincronização](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Abandone a chave de criptografia existente Olá
Abandone a chave de criptografia existente Olá para que essa nova chave de criptografia pode ser criado:

1. Faça logon no tooyour servidor se conectar do AD do Azure como administrador.

2. Inicie uma nova sessão do PowerShell.

3. Navegue até toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Execute o comando hello:`./miiskmu.exe /a`

![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Fornecer a senha Olá Olá conta AD DS
Como as senhas existentes Olá armazenadas dentro do banco de dados de saudação não podem ser descriptografadas, você precisa tooprovide Olá serviço de sincronização com senha Olá conta Olá AD DS. Olá serviço de sincronização criptografa senhas hello usando a nova chave de criptografia hello:

1. Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Vá toohello **conectores** guia.
3. Selecione Olá **conector AD** que corresponde a tooyour AD local. Se você tiver mais de um conector do AD, repita Olá seguindo as etapas para cada um deles.
4. Em **Ações**, selecione **Propriedades**.
5. Na caixa de diálogo pop-up hello, selecione **conectar-se a floresta do diretório tooActive**:
6. Digite a senha de saudação da conta do AD DS de saudação em hello **senha** caixa de texto. Se você não souber a senha, você deve definir tooa conhecido valor antes de executar essa etapa.
7. Clique em **Okey** toosave Olá nova senha e a caixa de diálogo pop-up Olá fechar.
![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Reinicializar senha Olá Olá conta de sincronização do AD do Azure
Diretamente, você não pode fornecer senha Olá Olá AD do Azure serviço conta toohello serviço de sincronização. Em vez disso, você precisa toouse Olá cmdlet **ADSyncAADServiceAccount adicionar** tooreinitialize Olá conta de serviço do AD do Azure. Olá cmdlet redefine a senha da conta hello e facilita o serviço de sincronização de toohello disponível:

1. Inicie uma nova sessão do PowerShell no servidor do Azure AD Connect hello.
2. Execute o cmdlet `Add-ADSyncAADServiceAccount`.
3. Na caixa de diálogo pop-up hello, forneça credenciais de Administrador Global de saudação do AD do Azure para seu locatário do AD do Azure.
![Utilitário de chave de criptografia de sincronização do Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Se for bem-sucedida, você verá o prompt de comando do PowerShell hello.

#### <a name="start-hello-synchronization-service"></a>Saudação de iniciar o serviço de sincronização
Agora que Olá serviço de sincronização tem a chave de criptografia de toohello de acesso e todas as senhas de Olá precisa, você pode reiniciar o serviço de saudação em Olá Gerenciador de controle de serviços do Windows:


1. Vá tooWindows Gerenciador de controle de serviço (serviços de início →).
2. Selecione **Sincronização do Microsoft Azure AD** e clique em Reiniciar.

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)

* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
