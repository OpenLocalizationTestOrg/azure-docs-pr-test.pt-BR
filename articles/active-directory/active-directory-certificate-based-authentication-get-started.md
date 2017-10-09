---
title: "aaaAzure autenticação baseada em certificado do Active Directory - Introdução | Microsoft Docs"
description: "Saiba como a autenticação baseada em certificado em seu ambiente tooconfigure"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Inicie com uma autenticação baseada em certificado do Azure Active Directory

Autenticação baseada em certificado permite que você toobe autenticado pelo Active Directory do Azure com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar-se a sua conta do Exchange online para: 

- Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word   

- Clientes do EAS (Exchange ActiveSync) 

Configurar esse recurso elimina a necessidade de saudação tooenter um nome de usuário e combinação de senha em determinados email e aplicativos do Microsoft Office em seu dispositivo móvel. 

Este tópico:

- Fornece Olá tooconfigure as etapas e usar a autenticação baseada em certificado para usuários de locatários no Office 365 Enterprise, Business, educação e governo dos Estados Unidos planos. Esse recurso está disponível na visualização em planos do Office 365 para China, defesa governamental e governo federal. 

- Pressupõe que você já tem uma [infraestrutura de chave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [do AD FS](connect/active-directory-aadconnectfed-whatis.md) configurada.    


## <a name="requirements"></a>Requisitos

a autenticação baseada em certificado tooconfigure, Olá deverá ser a seguinte:  

- A CBA (Autenticação Baseada em Certificado) tem suporte apenas em ambientes Federados para aplicativos de navegador ou clientes nativos que usam autenticação moderna (ADAL). Olá uma exceção é Exchange Active Sync (EAS) para EXO que pode ser usado para contas, federadas e gerenciadas. 

- autoridade de certificação raiz Hello e autoridades de certificação intermediários devem ser configuradas no Active Directory do Azure.  

- Cada autoridade de certificação deve ter uma CRL (Lista de Certificados Revogados) que pode ser referenciada por meio de uma URL para a Internet.  

- Você deve ter pelo menos uma autoridade de certificação configurada no Azure Active Directory. Você pode encontrar etapas relacionadas no hello [Configurar autoridades de certificação Olá](#step-2-configure-the-certificate-authorities) seção.  

- Para clientes do Exchange ActiveSync, o certificado de cliente Olá deve ter Olá roteável email usuário endereço no Exchange online em qualquer nome de entidade hello ou Olá valor RFC822 nome do campo de nome alternativo da entidade de saudação. Active Directory do Azure mapeia o atributo de endereço Proxy Olá RFC822 valor toohello no diretório de saudação.  

- O dispositivo de cliente deve ter a autoridade de certificação tooat um mínimo de acesso que emite certificados de cliente.  

- Um certificado de cliente para autenticação de cliente deve ter sido emitido tooyour cliente.  




## <a name="step-1-select-your-device-platform"></a>Etapa 1: selecione a plataforma do dispositivo

Como a primeira etapa para a plataforma de dispositivo Olá importantes para você, você precisa fazer tooreview Olá seguinte:

- suporte de aplicativos móveis do Office Olá 
- requisitos de implementação de saudação  

Olá relacionados informações existem para Olá plataformas de dispositivo a seguir:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Etapa 2: Configurar autoridades de certificação Olá 

tooconfigure as autoridades de certificado no Active Directory do Azure, para cada autoridade de certificação, carregar Olá a seguir: 

* Olá parte pública do certificado de saudação em *. cer* formato 
* Olá para URLs onde hello Internet listas de certificados revogados (CRLs) residem

esquema de saudação para uma autoridade de certificação será semelhante ao seguinte: 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Para configuração de saudação, você pode usar o hello [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Inicie o Windows PowerShell com os privilégios de administrador. 
2. Instale o módulo de saudação do AD do Azure. Você precisa tooinstall versão [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou superior.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Como uma primeira etapa de configuração, você precisa tooestablish uma conexão com seu locatário. Assim que um locatário de tooyour conexão existe, você pode revisar, adicionar, excluir e modificar as autoridades de certificação Olá confiável que são definidas em seu diretório. 

### <a name="connect"></a>Connect

tooestablish uma conexão com seu locatário, use Olá [AzureAD conectar](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Recuperar 

autoridades de certificação do tooretrieve Olá confiável que são definidas em seu diretório, use Olá [AzureADTrustedCertificateAuthority Get](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Adicionar

toocreate uma autoridade de certificação confiável, use Olá [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet e conjunto hello **crlDistributionPoint** valor correto tooa do atributo: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Remover

tooremove uma autoridade de certificação confiável, use Olá [AzureADTrustedCertificateAuthority remover](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modificar

toomodify uma autoridade de certificação confiável, use Olá [AzureADTrustedCertificateAuthority conjunto](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Etapa 3: configurar a revogação

toorevoke um certificado de cliente do Active Directory do Azure busca certificado Olá a lista de revogação (CRL) de URLs Olá carregado como parte das informações de autoridade de certificado e armazena em cache. carimbo de hora da última publicação da saudação (**data de efetivação** propriedade) na Olá CRL é usada tooensure Olá CRL ainda é válido. Olá CRL é referenciado periodicamente toorevoke acesso toocertificates que fazem parte da lista de saudação.

Se um instantânea mais revogação for necessária (por exemplo, se um usuário perde um dispositivo), token de autorização de saudação do usuário Olá pode ser invalidado. saudação de token, defina de autorização de saudação do tooinvalidate **StsRefreshTokenValidFrom** campo para esse usuário específico usando o Windows PowerShell. Você deve atualizar Olá **StsRefreshTokenValidFrom** campo para cada usuário que você deseja acesso toorevoke.

tooensure revogação Olá persistente, você deve definir Olá **data de efetivação** da data de tooa CRL Olá após Olá valor definido por **StsRefreshTokenValidFrom** e certifique-se de saudação certificado em questão está no Olá CRL.

Olá seguindo as etapas da estrutura de tópicos Olá processo de atualização e invalidar o token de autorização Olá por configuração Olá **StsRefreshTokenValidFrom** campo. 

**revogação de tooconfigure:** 

1. Conecte-se com o serviço de MSOL de toohello de credenciais de administrador: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Recupere o valor atual de StsRefreshTokensValidFrom Olá para um usuário: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Configure um novo valor de StsRefreshTokensValidFrom para usuário de saudação toohello igual timestamp atual: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

Data de saudação definir deve estar no hello futuras. Se Olá data não estiver no hello futuras, Olá **StsRefreshTokensValidFrom** propriedade não está definida. Se for date de hello em Olá futura, **StsRefreshTokensValidFrom** é definido toohello hora atual (não data Olá indicada pelo comando Set-MsolUser). 


## <a name="step-4-test-your-configuration"></a>Etapa 4: testar a sua configuração

### <a name="testing-your-certificate"></a>Teste do seu certificado

Como um primeiro teste de configuração, você deve tentar toosign em muito[Outlook Web Access](https://outlook.office365.com) ou [SharePoint Online](https://microsoft.sharepoint.com) usando seu **navegador no dispositivo**.

Se a entrada for bem-sucedida, você saberá que:

- certificado de usuário Olá foi provisionado tooyour dispositivo de teste
- O AD FS está configurado corretamente  


### <a name="testing-office-mobile-applications"></a>Testando aplicativos móveis do Office

**tootest autenticação baseada em certificado em seu aplicativo móvel do Office:** 

1. No seu dispositivo de teste, instale um aplicativo móvel do Office (por exemplo, OneDrive).
3. Inicie o aplicativo hello. 
4. Insira seu nome de usuário e, em seguida, selecione o certificado de usuário de Olá que você deseja que o toouse. 

Você deve se conectar com êxito. 

### <a name="testing-exchange-activesync-client-applications"></a>Testando aplicativos cliente do Exchange ActiveSync

tooaccess do Exchange ActiveSync (EAS) por meio da autenticação baseada em certificado, um perfil EAS que contém o certificado de cliente Olá deve ser aplicativo toohello disponíveis. 

Olá perfil de EAS deve conter Olá informações a seguir:

- Olá toobe de certificado de usuário usado para autenticação 

- ponto de extremidade do Hello EAS (por exemplo, outlook.office365.com)

Um perfil de EAS pode ser configurado e colocado Olá dispositivo por meio da utilização de saudação do gerenciamento de dispositivo móvel (MDM) como o Intune ou colocando manualmente certificados Olá em Olá perfil de EAS em dispositivo hello.  

### <a name="testing-eas-client-applications-on-android"></a>Testando os aplicativos cliente do EAS no Android

**autenticação de certificado tootest:**  

1. Configure um perfil EAS em aplicativo hello que satisfaz os requisitos de saudação acima.  
2. Abra o aplicativo hello e verificar a sincronização de email. 

