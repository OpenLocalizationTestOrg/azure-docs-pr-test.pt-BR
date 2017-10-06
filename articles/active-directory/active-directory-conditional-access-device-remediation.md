---
title: "aaaYou não pode chegar lá daqui em diante Olá portal do Azure de um dispositivo Windows | Microsoft Docs"
description: "Saiba onde não é possível obter aqui chega do e o que você pode verificar tooavoid em execução nesta caixa de diálogo."
services: active-directory
keywords: acesso condicional baseado em dispositivo, registro de dispositivo, habilitar registro de dispositivo, registro de dispositivo e MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Não é possível chegar lá a partir deste ponto em um dispositivo do Windows

Durante uma tentativa de, por exemplo, acessar a intranet do SharePoint Online de sua organização, você pode encontrar uma página informando que *não é possível ir daqui até lá*. Você está vendo esta página porque o administrador tiver configurado uma política de acesso condicional que impede que os recursos da empresa do acesso tooyour sob determinadas condições. Embora seja necessário toocontact helpdesk ou tooget seu administrador que esse problema é resolvido, há algumas coisas que você pode experimentar por conta própria, primeiro.

Se você estiver usando um **Windows** dispositivo, você deve verificar Olá a seguir:

- Você está usando um navegador com suporte?

- Você está executando uma versão com suporte do Windows em seu dispositivo?

- O dispositivo é compatível?






## <a name="supported-browser"></a>Navegador com suporte

Se o administrador tiver configurado uma política de acesso condicional, você só poderá acessar os recursos de sua organização usando um navegador com suporte. Em um dispositivo com Windows, há suporte apenas para o **Internet Explorer** e o **Edge**.

Você pode identificar facilmente se você não pode acessar um recurso devido navegador sem suporte tooan examinando a seção de detalhes de saudação da página de erro hello:

![Mensagem "Você não pode acessar esse lugar daqui" para navegadores sem suporte](./media/active-directory-conditional-access-device-remediation/02.png "Cenário")

correção somente Olá é toouse um navegador que oferece suporte a aplicativo hello para sua plataforma de dispositivo. Para obter uma lista completa dos navegadores com suporte, consulte [Navegadores com suporte](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Versões com suporte do Windows

Olá seguinte deve ser verdadeiro sobre o sistema de operacional do Windows hello em seu dispositivo: 

- Se você estiver executando um sistema operacional de desktop Windows em seu dispositivo, ele precisa toobe Windows 7 ou posterior.
- Se você estiver executando um sistema operacional do Windows server em seu dispositivo, ele precisa toobe Windows Server 2008 R2 ou posterior. 


## <a name="compliant-device"></a>Dispositivo em conformidade

O administrador pode ter configurado uma política de acesso condicional que permite que os recursos da organização de tooyour acesso somente de dispositivos compatíveis. toobe compatível, que o dispositivo deve ser qualquer tooyour ingressado no Active Directory local ou Unidos tooyour Active Directory do Azure.

Você pode identificar facilmente se você não pode acessar um recurso devido tooa dispositivo que não é compatível com examinando a seção de detalhes de saudação da página de erro hello:
 
![Mensagens "Você não pode acessar esse lugar daqui" para dispositivos não registrados](./media/active-directory-conditional-access-device-remediation/01.png "Cenário")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>É o seu dispositivo ingressado tooan do Active Directory local?

**Se o dispositivo é associado tooan local do Active Directory em sua organização:**

1. Certifique-se de que você entrar no tooWindows usando sua conta de trabalho (sua conta do Active Directory).
2. Conecte-se a rede corporativa tooyour por meio de uma rede virtual privada (VPN) ou DirectAccess.
3. Depois que você está conectado, pressione a tecla de logotipo do Windows hello + toolock chave Olá L a sessão do Windows.
4. Desbloqueie a sessão do Windows inserindo as credenciais de sua conta corporativa.
5. Aguarde um minuto e, em seguida, tente novamente tooaccess Olá aplicativo ou serviço.
6. Se você vir Olá mesma página, clique em hello **mais detalhes** link e, em seguida, contate o administrador com detalhes de saudação.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>É tooan seu dispositivo não fizer parte do Active Directory local?

Se seu dispositivo não tiver ingressado tooan do Active Directory local e execute o Windows 10, você tem duas opções:

* Executar o Ingresso do Azure AD
* Adicionar seu trabalho ou escolar tooWindows de conta

Para saber mais sobre como essas opções são diferentes, veja [Usando dispositivos Windows 10 em seu local de trabalho](active-directory-azureadjoin-windows10-devices.md).  
Se o seu dispositivo:

- Pertence tooyour organização, você deve executar a junção do Azure AD.
- É um dispositivo pessoal ou um Windows phone, você deve adicionar o seu trabalho ou de estudante tooWindows de conta 



#### <a name="azure-ad-join-on-windows-10"></a>Ingresso no Azure AD no Windows 10

Olá etapas toojoin tooAzure seu dispositivo AD são vinculados versão de saudação do Windows 10 que estão sendo executadas nele. versão de hello toodetermine do sistema operacional Windows 10, execute Olá **winver** comando: 

![Versão do Windows](./media/active-directory-conditional-access-device-remediation/03.png )


**Atualização de Aniversário do Windows 10 (Versão 1607):**

1. Olá abrir **configurações** aplicativo.
2. Clique em **Contas** > **Acesso corporativo ou de estudante**.
3. Clique em **Conectar**.
4. Clique em **ingressar tooAzure este dispositivo AD**.
5. Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.
6. Saia e entre com sua conta corporativa.
7. Tente novamente o aplicativo hello de tooaccess.

**Atualização do Windows de 10 de novembro de 2015 (Versão 1511):**

1. Olá abrir **configurações** aplicativo.
2. Clique em **Sistema** > **Sobre**.
3. Clique em **Ingressar no Azure AD**.
4. Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.
5. Saia e entre com sua conta corporativa (sua conta do Azure AD).
6. Tente novamente o aplicativo hello de tooaccess.


#### <a name="workplace-join-on-windows-81"></a>Workplace Join para Windows 8.1

Se o dispositivo não estiver associado ao domínio e executa o Windows 8.1, toodo um ingresso e registrar-se no Microsoft Intune, Olá seguintes etapas:

1. Abra **Configurações do PC**.
2. Clique em **Rede** > **Local de Trabalho**.
3. Clique em **Ingressar**.
4. Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.
5. Clique em **Ativar**.
6. Tente novamente o aplicativo hello de tooaccess.



#### <a name="add-your-work-or-school-account-toowindows"></a>Adicionar seu trabalho ou escolar tooWindows de conta 


**Atualização de Aniversário do Windows 10 (Versão 1607):**

1. Olá abrir **configurações** aplicativo.
2. Clique em **Contas** > **Acesso corporativo ou de estudante**.
3. Clique em **Conectar**.
4. Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.
5. Tente novamente o aplicativo hello de tooaccess.


**Atualização do Windows de 10 de novembro de 2015 (Versão 1511):**

1. Olá abrir **configurações** aplicativo.
2. Clique em **Contas** > **Suas contas**.
3. Clique em **Adicionar conta corporativa ou de estudante**.
4. Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.
5. Tente novamente o aplicativo hello de tooaccess.





## <a name="next-steps"></a>Próximas etapas
[Acesso condicional ao Azure Active Directory](active-directory-conditional-access.md)

