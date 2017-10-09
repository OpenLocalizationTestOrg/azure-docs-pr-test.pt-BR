---
title: "Azure AD Connect: solucionar problemas do Logon Único Contínuo | Microsoft Docs"
description: "Este tópico descreve como tootroubleshoot do Azure Active Directory perfeita SSO (Azure AD perfeita SSO)."
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Solucionar problemas do Logon Único Contínuo do Azure Active Directory

Este artigo ajuda você a localizar informações de solução de problemas comuns relacionados ao Logon Único Contínuo do Azure AD.

## <a name="known-issues"></a>Problemas conhecidos

- Se você estiver sincronizando 30 ou mais florestas do AD, não será possível habilitar o SSO Contínuo usando o Azure AD Connect. Como alternativa, você pode [habilitar manualmente](#manual-reset-of-azure-ad-seamless-sso) recurso Olá em seu locatário.
- Zona de "Sites confiáveis" do toohello de URLs (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) de serviço de adição do AD do Azure a em vez de zona de "intranet Local" hello **impede que os usuários de entrar no**.
- O SSO Contínuo não funciona no modo de navegação particular no Firefox e no Edge. E também no Internet Explorer quando o modo de Proteção Avançada está ativado.

>[!IMPORTANT]
>Podemos recentemente revertida suporte para a borda tooinvestigate problemas reportados por clientes.

## <a name="check-status-of-hello-feature"></a>Verificar o status do recurso de saudação

Certifique-se de que esse recurso de SSO contínuo Olá ainda é **habilitado** em seu locatário. Você pode verificar o status, vai toohello **do Azure AD Connect** folha no hello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/).

![Centro de administração do Azure Active Directory - folha Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Motivos de falha no logon no Centro de administração do Active Directory do Azure Olá

Um toostart bom problemas do usuário entrar com o SSO contínuo é toolook em Olá [relatório de atividade de entrada](../active-directory-reporting-activity-sign-ins.md) em Olá [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/).

![Centro de administração do Azure Active Directory - relatório Entradas](./media/active-directory-aadconnect-sso/sso9.png)

Navegue muito**Active Directory do Azure** -> **entradas** em Olá [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/) e clique em atividade de entrada de um usuário específico. Procure Olá **código de erro de entrada** campo. Mapear o valor de saudação do motivo da falha do campo tooa e resolução usando Olá a tabela a seguir:

|Código de erro de logon|Motivo da falha no logon|Resolução
| --- | --- | ---
| 81001 | O tíquete Kerberos do usuário é muito grande. | Reduza as associações de grupo do usuário e tente novamente.
| 81002 | Tíquete de Kerberos do usuário toovalidate não é possível. | Consulte a [Lista de verificação de solução de problemas](#troubleshooting-checklist).
| 81003 | Tíquete de Kerberos do usuário toovalidate não é possível. | Consulte a [Lista de verificação de solução de problemas](#troubleshooting-checklist).
| 81004 | Falha na tentativa de autenticação Kerberos. | Consulte a [Lista de verificação de solução de problemas](#troubleshooting-checklist).
| 81008 | Tíquete de Kerberos do usuário toovalidate não é possível. | Consulte a [Lista de verificação de solução de problemas](#troubleshooting-checklist).
| 81009 | "Tíquete do Kerberos não é possível toovalidate do usuário. | Consulte a [Lista de verificação de solução de problemas](#troubleshooting-checklist).
| 81010 | SSO contínuo falhou porque o tíquete de Kerberos do usuário Olá expirou ou é inválido. | Os usuários precisam toosign no meio de um dispositivo ingressado no domínio dentro da rede corporativa.
| 81011 | Objeto de usuário toofind não é possível com base nas informações no tíquete de Kerberos do usuário hello. | Use informações de usuário do Azure AD Connect toosynchronize no AD do Azure.
| 81012 | usuário Olá tentar toosign em tooAzure AD é diferente do usuário de saudação conectado ao dispositivo hello. | Entre em um dispositivo diferente.
| 81013 | Objeto de usuário toofind não é possível com base nas informações no tíquete de Kerberos do usuário hello. |Use informações de usuário do Azure AD Connect toosynchronize no AD do Azure. 

## <a name="troubleshooting-checklist"></a>Lista de verificação de solução de problemas

Use Olá problemas de SSO contínuo de tootroubleshoot de lista de verificação a seguir:

- Verifique se o recurso de SSO contínuo hello está habilitado no Azure AD Connect. Se você não pode habilitar o recurso de saudação (por exemplo, devido a porta tooa bloqueado), certifique-se de que você tenha todos os Olá [pré-requisitos](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) em vigor.
- Verifique se as duas essas URLs do Azure de AD (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) são parte das configurações de zona de Intranet do usuário hello.
- Certifique-se de dispositivo corporativo Olá é unida toohello AD de domínio.
- Certifique-se de saudação usuário está conectado no dispositivo toohello usando uma conta de domínio do AD.
- Certifique-se de que Olá da conta de usuário é de uma floresta do AD onde SSO contínuo foi definida.
- Certifique-se de saudação dispositivo está conectado na rede corporativa hello.
- Verifique se Olá a hora de dispositivo está sincronizado com o tempo Olá Active Directory e controladores de domínio hello e está dentro de cinco minutos entre si.
- Lista os tíquetes Kerberos existentes no dispositivo hello usando Olá **klist** comando em um prompt de comando. Verifique se tíquetes emitidos para Olá `AZUREADSSOACCT` conta de computador estão presentes. Os tíquetes Kerberos dos usuários são normalmente válidos durante 12 horas. Você pode ter configurações diferentes no seu Active Directory.
- Limpar os tíquetes Kerberos existentes são de dispositivo de saudação usando Olá **klist limpar** de comando e tente novamente.
- toodetermine se houver problemas relacionados a JavaScript, analise logs do console de saudação do navegador de saudação (em "ferramentas de desenvolvedor").
- Saudação de revisão [controlador de domínio registrará](#domain-controller-logs) também.

### <a name="domain-controller-logs"></a>Logs do controlador de domínio

Se a auditoria de êxito é habilitada no controlador de domínio, em seguida, sempre que um usuário faz logon usando o SSO contínuo uma segurança entrada é registrada no log de eventos de saudação. Você pode encontrar esses eventos de segurança usando Olá consulta a seguir (procure o evento **4769** associada à conta de computador Olá **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Redefinição manual do recurso de saudação

Se a solução de problemas não ajudarem, você pode redefinir manualmente o recurso de saudação em seu locatário. Siga estas etapas no servidor de local de saudação onde você está executando o Azure AD Connect:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Etapa 1: Importe o módulo do PowerShell de SSO contínuo de saudação

1. Primeiro, baixe e instale Olá [assistente Microsoft Online Services entrar](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Baixe e instale Olá [módulo do Active Directory do Azure de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` pasta.
4. Módulo do PowerShell de SSO contínuo de Olá de importação usando este comando: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Etapa 2: Obter a lista de saudação de florestas do AD no qual SSO contínuo foi habilitado

1. Execute o PowerShell como Administrador. No PowerShell, chame `New-AzureADSSOAuthenticationContext`. Quando solicitado, insira as suas credenciais de Administrador global do locatário.
2. Chame `Get-AzureADSSOStatus`. Esse comando fornece que Olá lista de florestas do AD (consulte a lista de domínios"hello") em que esse recurso foi habilitado.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Etapa 3: desabilitar o SSO Contínuo para cada floresta do AD em que ele foi configurado

1. Chame `$creds = Get-Credential`. Quando solicitado, insira as credenciais de administrador de domínio Olá para Olá se destina a floresta do AD.
2. Chame `Disable-AzureADSSOForest -OnPremCredentials $creds`. Este comando remove Olá `AZUREADSSOACCT` conta de computador da saudação local controlador de domínio para essa floresta AD específico.
3. Repita Olá etapas para cada floresta do AD que você configurou o recurso de saudação em anteriores.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Etapa 4: habilitar o SSO Contínuo para cada floresta do AD

1. Chame `Enable-AzureADSSOForest`. Quando solicitado, insira as credenciais de administrador de domínio Olá para Olá se destina a floresta do AD.
2. Repita Olá etapas para cada floresta do AD que você deseja tooset recurso Olá nos anteriores.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Etapa 5. Habilitar o recurso de saudação em seu locatário

Chamar `Enable-AzureADSSO` e digite "true" no hello `Enable: ` tooturn prompt no recurso de saudação em seu locatário.
