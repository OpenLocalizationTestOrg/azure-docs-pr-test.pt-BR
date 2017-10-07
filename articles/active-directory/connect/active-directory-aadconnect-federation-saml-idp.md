---
title: "Azure AD Connect: Usar um Provedor de Identidade SAML 2.0 para Logon Único | Microsoft Docs"
description: "Este tópico descreve o uso de um provedor de identidade em conformidade com SAML 2.0 para logon único."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Usar um IdP (provedor de identidade) SAML 2.0 para logon único

Este tópico contém informações sobre como usar um SAML 2.0 perfil SP-Lite compatível com base em provedor de identidade como Olá preferencial serviço de Token de segurança (STS) / provedor de identidade. Isso é útil quando você já tem um diretório de usuários e um repositório de senhas locais que podem ser acessados usando SAML 2.0. Esse diretório de usuários existente pode ser usado para logon tooOffice 365 e outros recursos de protegidos pelo AD do Azure. Olá SAML 2.0 SP-Lite perfil baseia Olá amplamente usado tooprovide de padrão de identidade SAML Security Assertion Markup Language () federado um logon e troca de atributos.

>[!NOTE]
>Para obter uma lista de 3ª parte Idps que foram testados para uso com o Azure AD consulte Olá [lista de compatibilidade de Federação do AD do Azure](active-directory-aadconnect-federation-compatibility.md)

A Microsoft suporta esta experiência de logon como integração de saudação de um serviço de nuvem da Microsoft, como o Office 365, com seu SAML 2.0 corretamente configurado perfil baseado IdP. Provedores de identidade SAML 2.0 são produtos de terceiros e, portanto, Microsoft não dá suporte para implantação de hello, configuração e solução de problemas práticas recomendadas relativas a eles. Depois de configurada corretamente, integração de saudação com hello SAML 2.0 provedor de identidade pode ser testado para a configuração correta usando Olá, ferramenta de analisador de conectividade da Microsoft que é descrita em mais detalhes abaixo. Para obter mais informações sobre o provedor de identidade baseado no perfil SAML 2.0 SP-Lite, peça a organização Olá que o forneceu.

>[!IMPORTANT]
>Somente um conjunto limitado de clientes está disponível neste cenário de logon com provedores de identidade SAML 2.0, entre os quais:

>- Clientes baseados na Web, como o Outlook Web Access e o SharePoint Online
- Clientes de email avançados que usam autenticação básica e um método de acesso do Exchange com suporte, como IMAP, POP, Active Sync, MAPI, etc. (Olá toobe necessário implantado é de ponto de extremidade de protocolo de cliente avançado), incluindo:
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (diversas versões do iOS)
    - Diversos dispositivos Google Android
    - Windows Phone 7, Windows Phone 7.8 e Windows Phone 8.0
    - Cliente de email do Windows 8 e Cliente de email do Windows 8.1
    - Cliente de email do Windows 10

Todos os outros clientes estão indisponíveis neste cenário de logon com seu provedor de identidade SAML 2.0. Por exemplo, o cliente de desktop saudação Lync 2010 não é capaz de toologin no serviço de saudação com seu provedor de identidade SAML 2.0 configurado para logon único.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Requisitos de protocolo do SAML 2.0 no Azure AD
Este tópico contém requisitos detalhados na mensagem de formatação que seu provedor de identidade SAML 2.0 deve implementar toofederate com AD do Azure tooenable logon tooone ou mais serviços de nuvem do Microsoft (como o Office 365) e protocolo de saudação. Olá SAML 2.0 terceira parte confiável (SP-STS) para um serviço de nuvem da Microsoft usado neste cenário é o AD do Azure.

É recomendável que você verifique seu SAML 2.0 mensagens de saída do provedor de identidade ser como toohello semelhante fornecido rastreamentos de exemplo possível. Além disso, use valores de atributo específicos de saudação fornecidos metadados do AD do Azure sempre que possível. Quando estiver satisfeito com suas mensagens de saída, você pode testar com hello analisador de conectividade da Microsoft, conforme descrito abaixo.

metadados de saudação do AD do Azure podem ser baixado desta URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Para os clientes na China usando hello instância específica da China do Office 365, Olá após o ponto de extremidade de federação deve ser usado: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Requisitos do protocolo SAML
Esta seção detalha como pares de mensagens de solicitação e resposta de saudação são juntados toohelp ordem você tooformat suas mensagens corretamente.

O AD do Azure pode ser configurado toowork com provedores de identidade que usam o perfil SAML 2.0 SP Lite Olá com alguns requisitos específicos como listado abaixo. Usando Olá solicitação e resposta mensagens de exemplo SAML junto com a teste automático e manual, você pode trabalhar tooachieve interoperabilidade com o Azure AD.

## <a name="signature-block-requirements"></a>Requisitos do bloco de assinatura
Dentro de saudação resposta SAML nó da assinatura Olá mensagem contém informações sobre a assinatura digital Olá para mensagem de saudação do próprio. o bloco de assinatura Olá tem Olá requisitos a seguir:

1. o próprio nó de asserção Olá deve ser assinado
2.  algoritmo de saudação RSA-sha1 deve ser usado como Olá DigestMethod. Outros algoritmos de assinatura digital não são aceitos.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Você também pode assinar um documento XML de saudação. 
4.  Olá Transform Algorithm deve corresponder valores Olá Olá exemplo a seguir:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Olá algoritmo do SignatureMethod deve corresponder a saudação de exemplo a seguir:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Associações com suporte
Associações são transporte Olá comunicações parâmetros que são necessários relacionados. Olá requisitos a seguir se aplicam a toohello associações

1. HTTPS é o transporte Olá necessário.
2.  O Azure AD exigirá o HTTP POST para envio do token durante o logon
3.  AD do Azure usará o HTTP POST para o provedor de identidade de toohello de solicitação de autenticação hello e REDIRECIONAR para o provedor de identidade do hello Logoff mensagem toohello.

## <a name="required-attributes"></a>Atributos obrigatórios
Esta tabela mostra os requisitos para atributos específicos na mensagem de saudação SAML 2.0.
 
|Atributo|Descrição|
| ----- | ----- |
|NameID|valor Olá dessa declaração deve ser Olá igual ao ImmutableID do usuário de saudação do AD do Azure. Ele pode ser o too64 usando caracteres alfanuméricos. Qualquer caractere seguro não HTML deve ser codificado, por exemplo, um caractere "+" é mostrado como ".2B".|
|IDPEmail|Olá Nome Principal do usuário (UPN) é listado em Olá SAML resposta como um elemento com hello nome idpemail isso é Olá UserPrincipalName (UPN) no Azure AD/Office 365. Olá UPN está no formato de endereço de email. Valor do UPN no Windows Office 365 (Azure Active Directory).|
|Emissor|Isso é necessário toobe um URI do provedor de identidade hello. Você não deve reutilizar Olá emissor de mensagens de saudação do exemplo. Se você tiver vários domínios de nível superior no seu Olá de locatários do AD do Azure que emissor deve corresponder Olá especificado configuração do URI configurado por domínio.|

>[!IMPORTANT]
>Atualmente, o AD do Azure oferece suporte a saudação seguindo o URI do formato NameID para SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-formato: persistente.

## <a name="sample-saml-request-and-response-messages"></a>Mensagens de exemplo de solicitação e resposta SAML
Um par de mensagem de solicitação e resposta é mostrado para troca de mensagens de logon de saudação.
Esta é uma mensagem de solicitação de exemplo que é enviada do provedor de identidade SAML 2.0 do AD do Azure tooa exemplo. provedor de identidade do SAML 2.0 de exemplo Hello é que os serviços de Federação do Active Directory (AD FS) configurado toouse SAML-P protocolo. Testes de interoperabilidade também foram concluídos com outros provedores de identidade SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Esta é uma mensagem de resposta de exemplo que é enviada de tooAzure do provedor de identidade compatível SAML 2.0 Olá exemplo AD / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Configurar seu provedor de identidade em conformidade com SAML 2.0
Este tópico contém diretrizes sobre como tooconfigure seu toofederate de provedor de identidade SAML 2.0 com tooone de acesso de logon único do AD do Azure tooenable ou mais Microsoft cloud services (como o Office 365) usando o protocolo de saudação SAML 2.0. Olá, SAML 2.0 da terceira parte de um serviço de nuvem da Microsoft usado neste cenário é o AD do Azure.

## <a name="add-azure-ad-metadata"></a>Adicionar metadados do Azure AD
Seu provedor de identidade SAML 2.0 deve tooinformation tooadhere sobre a terceira parte confiável Olá AD do Azure. O Azure AD publica metadados em https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

É recomendável que você importe sempre metadados hello mais recentes do AD do Azure quando configurar seu provedor de identidade SAML 2.0. Observe que o AD do Azure não lê metadados saudação do provedor de identidade.

## <a name="add-azure-ad-as-a-relying-party"></a>Adicionar o Azure AD como uma terceira parte confiável
Você tem tooenable comunicação entre o provedor de identidade SAML 2.0 e AD do Azure. Essa configuração será dependente de seu provedor de identidade específico e você deve consultar toodocumentation para ele. Normalmente, você definiria Olá terceira parte confiável ID toohello igual a saudação entityID de metadados de saudação do AD do Azure.

>[!NOTE]
>Verifique se Olá relógio em seu servidor do provedor de identidade SAML 2.0 está sincronizado tooan fonte de tempo precisa. Uma hora do relógio inexata pode causar toofail logons federados.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Instalar o Windows PowerShell para fazer logon no provedor de identidade SAML 2.0
Depois de configurar seu provedor de identidade SAML 2.0 para uso com o logon do AD do Azure, o hello próxima etapa é toodownload e instalar hello Azure módulo Active Directory para Windows PowerShell. Uma vez instalado, você usará esses cmdlets tooconfigure seus domínios do AD do Azure como domínios federados.

Hello Azure módulo Active Directory para Windows PowerShell é um download para gerenciar os dados da sua organização no AD do Azure. Este módulo instala um conjunto de cmdlets tooWindows PowerShell; executar tooset esses cmdlets o acesso de logon único tooAzure AD e por sua vez tooall de saudação você se inscreveu de serviços em nuvem. Para obter instruções sobre como toodownload e instale Olá cmdlets, consulte [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Configurar uma relação de confiança entre seu provedor de identidade SAML e o Azure AD
Antes de configurar a federação em um domínio do Azure AD, ele precisa ter um domínio personalizado configurado. Você não pode federar o domínio padrão de saudação que é fornecido pela Microsoft. domínio padrão de saudação da Microsoft termina com "m".
Você irá executar uma série de cmdlets em tooadd de interface de linha de comando do Windows PowerShell hello ou converter domínios para logon único.

Cada domínio do Active Directory do Azure que você deseja toofederate usando seu provedor de identidade SAML 2.0 deve ser adicionado como um domínio de logon único ou convertido toobe um domínio de logon único de um domínio padrão. Adicionar ou converter um domínio configura uma relação de confiança entre seu provedor de identidade SAML 2.0 e Azure AD.

Olá procedimento a seguir descreve a conversão de um domínio padrão tooa domínio federado existente usando o SAML 2.0 SP-Lite. Observe que o seu domínio pode sofrer uma interrupção que afeta os usuários se too2 horas depois de realizar esta etapa.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Configurar um domínio em seu diretório do Azure AD para federação


1. Conecte-se tooyour diretório do AD do Azure como um administrador de locatário: MsolService se conectar.
2.  Configure a federação desejada do Office 365 domínio toouse com SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Você pode obter Olá assinatura de cadeia de caracteres do certificado codificado na base64 do arquivo de metadados IDP. Um exemplo desse local foi fornecido, mas ele pode diferir ligeiramente dependendo de sua implementação.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Para obter mais informações sobre "Set-MsolDomainAuthentication", consulte: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Você precisa executar “$ecpUrl = “https://WS2012R2-0.contoso.com/PAOS“” somente se configurar uma extensão ECP para seu provedor de identidade. Clientes do Exchange Online, exceto pelo aplicativo OWA (Outlook Web Application), dependem de ponto de extremidade ativa baseado em POST. Se seu SAML 2.0 STS implementar a implementação do ECP do tooShibboleth semelhante um ponto de extremidade ativo de um ponto de extremidade ativo pode ser possível toointeract esses clientes avançados com hello serviço Exchange Online.

Depois de configurar a federação você pode alternar back muito "não federada" (ou "gerenciada"), no entanto, essa alteração ocupa tootwo horas toocomplete e requer designar senhas novas aleatórias para a nuvem com base em usuário tooeach entrar. Alternar de volta muito "" gerenciado pode ser necessário em alguns cenários tooreset um erro em suas configurações. Para obter mais informações sobre a conversão de domínio, consulte: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Provisionar tooAzure de entidades de usuário AD / Office 365
Antes que possa autenticar seu usuários tooOffice 365 deve provisionar o AD do Azure com os objetos que correspondem a asserção toohello em Olá SAML 2.0 de declaração de usuário. Se esses objetos de usuário não são conhecidos com antecedência tooAzure AD, em seguida, eles não podem ser usados para logon federado. Conexão do AD do Azure ou o Windows PowerShell pode ser usado tooprovision capitais de usuários.

Conexão do AD do Azure pode ser usado tooprovision entidades tooyour domínios em seu diretório do AD do Azure de saudação do Active Directory local. Para obter informações mais detalhadas, consulte [Integrar seus diretórios locais com o Azure Active Directory](active-directory-aadconnect.md).

O Windows PowerShell também podem ser usado tooautomate adicionando novos usuários tooAzure AD e toosynchronize muda de diretório local de saudação. Olá toouse cmdlets do Windows PowerShell você deve baixar Olá [módulos do Azure Active Directory](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Este procedimento mostra como tooadd tooAzure um único usuário AD.


1. Conecte-se tooyour diretório do AD do Azure como um administrador de locatário: MsolService se conectar.
2.  Crie uma nova entidade de usuário: ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Para obter mais informações sobre "New-MsolUser", consulte [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>saudação do "UserPrinciplName" valor deve corresponder o valor de saudação que você enviará para "IDPEmail" na sua declaração SAML 2.0 e hello "ImmutableID" o valor deve corresponder Olá valor enviado na sua declaração de "NameID".

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Verificar o logon único com seu IDP SAML 2.0
Como administrador Olá, antes de verificar e gerenciar logon único (também chamado federação de identidades), examine as informações de saudação e executar etapas Olá Olá artigos tooset o logon único com seu provedor de identidade baseado no SAML 2.0 SP-Lite a seguir:


1.  Você revisou Olá requisitos de protocolo do SAML 2.0 do AD do Azure
2.  Você configurou seu provedor de identidade SAML 2.0
3.  Instalar o Windows PowerShell para logon único no provedor de identidade SAML 2.0
4.  Configure uma relação de confiança entre seu provedor de identidade SAML 2.0 e o Azure AD
5.  Provisionado um tooAzure de principal do usuário de teste conhecido do Active Directory (Office 365) por meio do Windows PowerShell ou do Azure AD Connect.
6.  Configure a sincronização de diretório usando o [Azure AD Connect](active-directory-aadconnect.md).

Após configurar o logon único com seu provedor de identidade baseado em SP-Lite compatível com SAML 2.0, verifique se ele está funcionando corretamente.

>[!NOTE]
>Se você converteu um domínio, em vez de adicionar um, pode levar até too24 horas tooset o logon único.
Antes de verificar o logon único, termine de configurar a sincronização do Active Directory, sincronize seus diretórios e ative seus usuários sincronizados.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Use Olá ferramenta tooverify que o logon único foi configurado corretamente
tooverify esse logon único foi configurado corretamente, você pode executar Olá seguindo o procedimento tooconfirm que você é capaz de toosign no serviço de nuvem toohello com suas credenciais corporativas.

A Microsoft forneceu uma ferramenta que você pode usar tootest seu SAML 2.0 com base no provedor de identidade. Antes de executar Olá teste ferramenta, você deve ter configurado um toofederate de locatário do AD do Azure com seu provedor de identidade.

>[!NOTE]
>Olá Connectivity Analyzer requer o Internet Explorer 10 ou posterior.



1. Download Olá analisador de conectividade, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Clique em Instalar agora toobegin baixar e instalar ferramenta de saudação.
3.  Selecione "Não é possível configurar a federação com o Office 365, o Azure ou outros serviços que usam o Azure Active Directory".
4.  Depois que a ferramenta de saudação é baixado e em execução, você verá a janela de diagnóstico de conectividade de saudação. ferramenta de saudação guiará você por meio de testar sua conexão de Federação.
5.  Olá analisador de conectividade será aberta seu SAML 2.0 IDP para você toologon, insira credenciais Olá UPN Olá você está testando: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Em Olá federação teste na janela de logon que você deve inserir um nome de conta e senha para o locatário do AD do Azure Olá que é configurado toobe federado com seu provedor de identidade SAML 2.0. ferramenta Olá tentará toosign-in usando as credenciais e os resultados detalhados de testes realizados durante a tentativa de logon hello serão fornecidos como saída.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. Esta janela mostra o resultado de um teste com falha. Clicando em rever resultados detalhados mostrará informações sobre os resultados de saudação de cada teste que foi executado. Você também pode salvar Olá resultados toodisk em ordem tooshare-los.
 
>[!NOTE]
>Olá analisador de conectividade também testa a federação ativa usando Olá WS *-protocolos baseados em e ECP/paos;. Se você não estiver usando esses recursos, você pode ignorar Olá erro a seguir: teste Olá o fluxo de entrada ativo usando o ponto de extremidade de federação ativa do seu provedor de identidade.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Verifique manualmente se o logon único foi configurado corretamente
A verificação manual fornece etapas adicionais que você pode tomar tooensure que seu provedor de identidade SAML 2.0 está funcionando corretamente em muitos cenários.
tooverify que o logon único foi configurado corretamente, execute o seguinte Olá etapas:


1. Em um computador ingressado no domínio, entrar no serviço de nuvem tooyour usando o mesmo nome que você usa para suas credenciais corporativas de logon de saudação.
2.  Clique dentro da caixa de senha hello. Se o logon único está configurado, caixa de senha Olá ficará sombreada e você verá a seguinte mensagem de saudação: "Agora você está toosign necessária no <your company>."
3.  Clique em Olá entra em <your company> link. Se você for capaz de toosign em, em seguida, o logon único configurado.

## <a name="next-steps"></a>Próximas etapas


- [Gerenciamento e personalização dos Serviços de Federação do Active Directory (AD FS) com o Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Lista de compatibilidade de federação do AD do Azure](active-directory-aadconnect-federation-compatibility.md)
- [Instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
