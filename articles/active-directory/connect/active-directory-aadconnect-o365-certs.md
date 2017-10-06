---
title: "renovação de aaaCertificate para os usuários do Office 365 e o Azure AD | Microsoft Docs"
description: "Este artigo explica tooOffice 365 usuários como tooresolve problemas de emails que notificação-lo sobre como renovar um certificado."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Renovar certificados de federação para o Office 365 e o Azure Active Directory
## <a name="overview"></a>Visão geral
Para federação bem-sucedida entre o Azure Active Directory (AD do Azure) e os serviços de Federação do Active Directory (AD FS), certificados de saudação usados por tooAzure de tokens de segurança do AD FS toosign AD devem corresponder a que está configurado no AD do Azure. Qualquer incompatibilidade pode levar toobroken confiança. O Azure AD garante que essas informações sejam mantidas em sincronia quando você implanta o AD FS e o Proxy de Aplicativo Web (para acesso à extranet).

Este artigo fornece a você informações adicionais toomanage seu certificados de assinatura de token e mantê-los em sincronia com o AD do Azure, em Olá casos a seguir:

* Você não está implantando Olá Proxy de aplicativo Web e, portanto, não estão disponível no Olá extranet de metadados de Federação Olá.
* Você não estiver usando a configuração padrão de saudação do AD FS para certificados de assinatura de token.
* Você está usando um provedor de identidade de terceiros.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Configuração padrão do AD FS para certificados de assinatura de token
assinatura de token Hello e certificados de descriptografia de token são normalmente os certificados autoassinados e são bons para um ano. Por padrão, o AD FS inclui um processo de renovação automática chamado **AutoCertificateRollover**. Se você estiver usando o AD FS 2.0 ou posterior, o Office 365 e o Azure AD atualizarão automaticamente o certificado antes que ele expire.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Notificação de renovação do portal do Office 365 de saudação ou um email
> [!NOTE]
> Se você recebeu um email ou uma notificação portal solicitando que você toorenew seu certificado para o Office, consulte [Gerenciando alterações tootoken certificados de assinatura](#managecerts) toocheck se você precisar tootake qualquer ação. A Microsoft está ciente de um possível problema que pode levar toonotifications para renovação de certificados que estão sendo enviada, mesmo quando nenhuma ação é necessária.
>
>

AD do Azure tentativas de metadados de Federação toomonitor hello e atualização Olá token certificados de assinatura, conforme indicado por esses metadados. 30 dias antes da expiração de saudação do token Olá certificados de assinatura, o AD do Azure verifica se novos certificados disponíveis consultando metadados de Federação hello.

* Se ele pode sondar Olá metadados de Federação e recuperar certificados novos Olá com êxito, nenhuma notificação por email ou o aviso no portal do Office 365 de saudação é emitido toohello usuário.
* Se não for possível recuperar certificados de assinatura do token novo hello, ou porque os metadados de Federação Olá não estão acessível ou substituição automática de certificado não estiver habilitada, Azure AD emite uma notificação por email e um aviso no portal do Office 365 de saudação.

![Notificação do portal do Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Se você estiver usando o AD FS, continuidade de negócios tooensure, verifique se os servidores possuem Olá atualizações a seguir para que não ocorram falhas de autenticação para problemas conhecidos. Isso reduz os problemas conhecidos de servidor de proxy do AD FS para essa renovação e períodos futuros de renovação:
>
> Server 2012 R2 - [Pacote cumulativo de atualizações do Windows Server de maio de 2014](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 e 2012 - [falha de autenticação por meio do proxy no Windows Server 2008 ou no Windows 2012 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Verifique se os certificados de saudação necessário toobe atualizado<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Etapa 1: Verificar o estado de AutoCertificateRollover Olá
No servidor do AD FS, abra o PowerShell. Verifique se o valor de AutoCertificateRollover Olá é definida tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Se você estiver usando o AD FS 2.0, primeiro execute Add-Pssnapin Microsoft.Adfs.Powershell.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Etapa 2: confirmar se o AD FS e o Azure AD estão em sincronia
No servidor do AD FS, abra o prompt do PowerShell do Azure AD hello e conecte tooAzure AD.

> [!NOTE]
> Você pode baixar o PowerShell do Azure AD [aqui](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Verificar certificados Olá configurado no AD FS e propriedades de confiança do AD do Azure para Olá o domínio especificaram.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Se as impressões digitais de saudação no hello saídas de correspondência, seus certificados são sincronizados com o Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Etapa 3: Verificar se o certificado está prestes a tooexpire
Na saída de saudação do Get-MsolFederationProperty ou Get-AdfsCertificate, verifique se a data Olá em "Não depois." Se a data de saudação é menos de 30 dias imediatamente, você deve tomar uma ação.

| AutoCertificateRollover | Certificados em sincronia com o Azure AD | Os metadados de federação do AD FS estão acessíveis publicamente | Validade | Ação |
|:---:|:---:|:---:|:---:|:---:|
| Sim |Sim |Sim |- |Nenhuma ação necessária. Confira [Renovar o certificado de assinatura de token automaticamente](#autorenew). |
| Sim |Não |- |Menos de 15 dias |Renovar imediatamente. Confira [Renovar manualmente o certificado de assinatura de token ](#manualrenew). |
| Não |- |- |Menos de 30 dias |Renovar imediatamente. Confira [Renovar manualmente o certificado de assinatura de token ](#manualrenew). |

\[-] Não importa

## Renove automaticamente o certificado de assinatura de token de saudação (recomendado)<a name="autorenew"></a>
Você não precisa tooperform todas as etapas manuais se as seguinte Olá forem verdadeiras:

* Você implantou o Proxy de aplicativo Web, permitindo acesso toohello metadados de federação de saudação à extranet.
* Você está usando a configuração padrão de saudação do AD FS (AutoCertificateRollover está habilitado).

Verifique a saudação tooconfirm que Olá certificado a seguir pode ser atualizada automaticamente.

**1. Olá propriedade do AD FS AutoCertificateRollover deve ser definido como tooTrue.** Isso indica que o AD FS gerará automaticamente novo token de assinatura e certificados de descriptografia de token, antes de saudação antigo aqueles expirarem.

**2. metadados de Federação Olá AD FS são publicamente acessível.** Verifique se os metadados de Federação estão publicamente acessível navegando toohello seguindo a URL de um computador na Olá internet pública (fora da rede corporativa da saudação):

https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml

onde `(your_FS_name) `é substituído pelo nome de host do hello federação serviço sua organização usa, por exemplo, fs.contoso.com.  Se você for capaz de tooverify dessas configurações com êxito, você não tem toodo qualquer outra coisa.  

Exemplo: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Renovar manualmente o certificado de assinatura de token de saudação<a name="manualrenew"></a>
Você pode escolher toorenew certificados de assinatura de token Olá manualmente. Por exemplo, hello cenários a seguir podem funcionar melhor para a renovação manual:

* Os certificados de assinatura de token não são certificados autoassinados. motivo mais comum de saudação para isso é que sua organização gerencia certificados do AD FS registrados de uma autoridade de certificação organizacional.
* Segurança de rede não permite toobe de metadados de federação de saudação publicamente disponível.

Nesses cenários, toda vez que você atualizar o token Olá certificados de assinatura, você deve também atualizar seu domínio do Office 365 usando o comando do PowerShell hello, Update-MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Etapa 1: verifique se o AD FS tem novos certificados de assinatura de token
**Configuração não padrão**

Se você estiver usando uma configuração não padrão do AD FS (onde **AutoCertificateRollover** está definido muito**False**), você provavelmente está usando certificados personalizados (não autoassinados). Para obter mais informações sobre como os certificados de autenticação token do toorenew Olá AD FS, consulte [orientação para os clientes usando o AD FS não certificados autoassinados](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Os metadados de federação não estão disponíveis publicamente**

Olá por outro lado, se **AutoCertificateRollover** está definido muito**True**, mas seus metadados de Federação não estão acessível publicamente, primeiro certifique-se de que os novos certificados de assinatura de token foram gerados pelo AD FS. Confirme que você tem o novo token assinando certificados Olá colocar as etapas a seguir:

1. Verifique se que você está conectado no servidor do toohello primário AD FS.
2. Verifique se os certificados de assinatura atual Olá no AD FS, abrindo uma janela de comando do PowerShell e executando Olá comando a seguir:

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > Se estiver usando o AD FS 2.0, você deverá executar Add-Pssnapin Microsoft.Adfs.Powershell primeiro.
   >
   >
3. Examine a saída do comando Olá em todos os certificados listados. Se o AD FS gerou um novo certificado, você deverá ver dois certificados na saída de hello: uma para a qual Olá **IsPrimary** valor é **True** e hello **NotAfter** data é dentro de 5 dias e um para o qual **IsPrimary** é **False** e **NotAfter** é cerca de um ano em Olá futuras.
4. Se você apenas ver um certificado e Olá **NotAfter** data é de 5 dias, você precisa toogenerate um novo certificado.
5. toogenerate um novo certificado, execute Olá comando em um prompt de comando do PowerShell a seguir: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Verificar atualização Olá executando Olá novamente comandos a seguir: PS c\>Get-ADFSCertificate – CertificateType autenticação de tokens

Dois certificados deverão ser listados agora, um dos quais tem uma **NotAfter** data de aproximadamente um ano Olá futuro e para quais Olá **IsPrimary** valor é **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Etapa 2: Atualizar novo token de saudação assinando certificados de confiança Olá Office 365
Atualize o Office 365 com hello novo token de assinatura certificados toobe usada para a relação de confiança hello, da seguinte maneira.

1. Abra Olá Microsoft Azure módulo Active Directory para Windows PowerShell.
2. Execute $cred = Get-Credential. Quando este cmdlet solicitar credenciais, digite as credenciais da conta de administrador de serviços de nuvem.
3. Execute Connect-MsolService –Credential $cred. Esse cmdlet conecta toohello serviço de nuvem. Criar um contexto que conecta o serviço de nuvem toohello é necessária antes de executar qualquer um dos cmdlets adicionais de saudação instalados pela ferramenta de saudação.
4. Se você estiver executando esses comandos em um computador que não seja o servidor de Federação primário saudação do AD FS, execute Set-MSOLAdfscontext-computador <AD FS primary server>, onde <AD FS primary server> é o nome FQDN interno de saudação do servidor do hello primário AD FS. Esse cmdlet cria um contexto que conecta você tooAD FS.
5. Execute Update-MSOLFederatedDomain –DomainName <domain>. Esse cmdlet atualiza as configurações de saudação do AD FS para o serviço de nuvem Olá e configura Olá a relação de confiança entre hello dois.

> [!NOTE]
> Se você precisar toosupport vários domínios de nível superior, como contoso.com e fabrikam.com, você deve usar o hello **SupportMultipleDomain** com qualquer cmdlet. Para obter mais informações, veja [Suporte para vários domínios de nível superior](active-directory-aadconnect-multiple-domains.md).
>
>

## Reparar a relação de confiança do Azure AD usando o Azure AD Connect <a name="connectrenew"></a>
Se você tiver configurado seu farm do AD FS e a confiança do AD do Azure usando o Azure AD Connect, você pode usar toodetect do Azure AD Connect se você precisar tootake qualquer ação para seu certificados de assinatura de token. Se você precisar de certificados de saudação toorenew, você pode usar do Azure AD Connect toodo assim.

Para obter mais informações, consulte [reparar confiança Olá](active-directory-aadconnect-federation-management.md).
