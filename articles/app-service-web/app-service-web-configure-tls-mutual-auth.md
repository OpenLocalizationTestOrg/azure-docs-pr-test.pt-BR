---
title: "aaaHow tooConfigure autenticação mútua do TLS para o aplicativo Web"
description: "Saiba como tooconfigure seu cliente de toouse do aplicativo web do certificado autenticação no TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>Como tooConfigure TLS de autenticação mútua para o aplicativo Web
## <a name="overview"></a>Visão geral
Você pode restringir o aplicativo do access tooyour web do Azure, permitindo que diferentes tipos de autenticação para ele. Portanto, toodo unidirecional é tooauthenticate usando um certificado de cliente quando a solicitação de saudação é por TLS/SSL. Esse mecanismo é chamado de autenticação mútua de TLS ou autenticação de certificado de cliente e este artigo mostra detalhadamente como toosetup a autenticação de certificado de cliente do web app toouse.

> **Observação:** se acessar seu site via HTTP e não HTTPS, você não receberá nenhum certificado de cliente. Então se seu aplicativo exigir certificados de cliente você não deve permitir solicitações de aplicativo tooyour via HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Configurar o aplicativo Web para autenticação de certificado do cliente
toosetup seus certificados de cliente web aplicativo toorequire que necessário tooadd Olá clientCertEnabled site configuração para seu aplicativo web e defina-a como tootrue. Essa configuração não está disponível no momento por meio de experiência de gerenciamento de Olá Olá Portal e Olá API REST precisará toobe usado tooaccomplish isso.

Você pode usar o hello [ARMClient ferramenta](https://github.com/projectkudu/ARMClient) toomake-toocraft fácil Olá chamada à API REST. Depois de você fazer logon com a ferramenta Olá precisará Olá tooissue comando a seguir:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

Substituir tudo {} com informações para seu aplicativo web e criando um arquivo chamado enableclientcert.json com hello JSON a seguir conteúdo:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Verifique se o valor toochange hello "local" toowherever que seu aplicativo web é localizado, por exemplo, Centro Norte dos EUA ou oeste dos EUA etc.

Você também pode usar https://resources.azure.com tooflip Olá `clientCertEnabled` propriedade muito`true`.

> **Observação:** se você executar o cliente do ARM do Powershell, você precisará Olá tooescape símbolo @ para arquivo JSON de saudação com um acento '.
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>Acessando Olá cliente certificado de seu aplicativo de Web
Se você estiver usando o ASP.NET e configurar a autenticação de certificado de cliente do aplicativo toouse, certificado Olá será disponível por meio de saudação **HttpRequest.ClientCertificate** propriedade. Para as pilhas de outros aplicativos, o certificado de cliente Olá estejam disponível no seu aplicativo por meio de um valor codificado na base64 no cabeçalho de solicitação de "X-ARR-ClientCert" hello. O aplicativo pode criar um certificado a partir desse valor e, em seguida, usá-lo para fins de autenticação e autorização.

## <a name="special-considerations-for-certificate-validation"></a>Considerações especiais para validação de certificado
certificado de cliente de saudação enviada toohello aplicativo não passar por nenhuma validação pela plataforma de aplicativos Web do Azure hello. Validar esse certificado é de responsabilidade de saudação do aplicativo web de saudação. Veja o exemplo de código ASP.NET que valida as propriedades do certificado para fins de autenticação.

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
