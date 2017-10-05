---
title: "Como configurar a autenticação mútua TLS para Aplicativo Web"
description: "Saiba como configurar o aplicativo Web para usar a autenticação de certificado do cliente no TLS."
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
ms.openlocfilehash: db69852cffd1ff331ac4a640b04ea4360d00bf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="a0253-103">Como configurar a autenticação mútua TLS para Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a0253-103">How To Configure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="a0253-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a0253-104">Overview</span></span>
<span data-ttu-id="a0253-105">Você pode restringir o acesso ao aplicativo Web do Azure, permitindo diferentes tipos de autenticação para ele.</span><span class="sxs-lookup"><span data-stu-id="a0253-105">You can restrict access to your Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="a0253-106">Uma maneira de fazer isso é autenticar usando um certificado de cliente quando a solicitação for por TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="a0253-106">One way to do so is to authenticate using a client certificate when the request is over TLS/SSL.</span></span> <span data-ttu-id="a0253-107">Esse mecanismo é chamado de autenticação mútua TLS ou autenticação de certificado do cliente, e este artigo mostra detalhadamente como configurar o aplicativo Web para usar a autenticação de certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="a0253-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how to setup your web app to use client certificate authentication.</span></span>

> <span data-ttu-id="a0253-108">**Observação:** se acessar seu site via HTTP e não HTTPS, você não receberá nenhum certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="a0253-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="a0253-109">Por isso, se seu aplicativo exigir certificados de cliente, você não deve permitir solicitações ao seu aplicativo via HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0253-109">So if your application requires client certificates you should not allow requests to your application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="a0253-110">Configurar o aplicativo Web para autenticação de certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="a0253-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="a0253-111">Para que seu aplicativo web exija certificados do cliente, você precisa adicionar a definição de site clientCertEnabled para seu aplicativo Web e defini-lo como true.</span><span class="sxs-lookup"><span data-stu-id="a0253-111">To setup your web app to require client certificates you need to add the clientCertEnabled site setting for your web app and set it to true.</span></span> <span data-ttu-id="a0253-112">Atualmente, essa configuração não está disponível por meio da experiência de gerenciamento no Portal e será necessário usar a API REST para isso.</span><span class="sxs-lookup"><span data-stu-id="a0253-112">This setting is not currently available through the management experience in the Portal, and the REST API will need to be used to accomplish this.</span></span>

<span data-ttu-id="a0253-113">Você pode usar a [ferramenta ARMClient](https://github.com/projectkudu/ARMClient) para facilitar a chamada à API REST.</span><span class="sxs-lookup"><span data-stu-id="a0253-113">You can use the [ARMClient tool](https://github.com/projectkudu/ARMClient) to make it easy to craft the REST API call.</span></span> <span data-ttu-id="a0253-114">Depois de fazer logon com a ferramenta, você precisará emitir o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a0253-114">After you log in with the tool you will need to issue the following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="a0253-115">substituindo tudo que está entre {} pelas informações do seu aplicativo Web e criando um arquivo chamado enableclientcert.json com o seguinte conteúdo JSON:</span><span class="sxs-lookup"><span data-stu-id="a0253-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with the following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="a0253-116">Não se esqueça de alterar o valor de “location” em todo lugar que o aplicativo Web estiver localizado; por exemplo, região central do norte dos EUA ou oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="a0253-116">Make sure to change the value of "location" to wherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="a0253-117">Você também pode usar https://resources.azure.com para inverter a propriedade `clientCertEnabled` para `true`.</span><span class="sxs-lookup"><span data-stu-id="a0253-117">You can also use https://resources.azure.com to flip the `clientCertEnabled` property to `true`.</span></span>

> <span data-ttu-id="a0253-118">**Observação:** se você executar o ARMClient no Powershell, precisará usar o símbolo @ como o caractere de escape para o arquivo JSON com um acento grave \`.</span><span class="sxs-lookup"><span data-stu-id="a0253-118">**Note:** If you run ARMClient from Powershell, you will need to escape the @ symbol for the JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-the-client-certificate-from-your-web-app"></a><span data-ttu-id="a0253-119">Acessando o certificado do cliente do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a0253-119">Accessing the Client Certificate From Your Web App</span></span>
<span data-ttu-id="a0253-120">Se você estiver usando ASP.NET e configurar seu aplicativo para usar a autenticação de certificado de cliente, o certificado estará disponível por meio da propriedade **HttpRequest.ClientCertificate** .</span><span class="sxs-lookup"><span data-stu-id="a0253-120">If you are using ASP.NET and configure your app to use client certificate authentication, the certificate will be available through the **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="a0253-121">Para outras pilhas de aplicativo, o certificado do cliente estará disponível no seu aplicativo por meio de um valor codificado na base64 no cabeçalho da solicitação "X-ARR-ClientCert".</span><span class="sxs-lookup"><span data-stu-id="a0253-121">For other application stacks, the client cert will be available in your app through a base64 encoded value in the "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="a0253-122">O aplicativo pode criar um certificado a partir desse valor e, em seguida, usá-lo para fins de autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="a0253-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="a0253-123">Considerações especiais para validação de certificado</span><span class="sxs-lookup"><span data-stu-id="a0253-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="a0253-124">O certificado do cliente que é enviado ao aplicativo não passa por qualquer validação da plataforma de aplicativos da Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0253-124">The client certificate that is sent to the application does not go through any validation by the Azure Web Apps platform.</span></span> <span data-ttu-id="a0253-125">Validar o certificado é de responsabilidade do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a0253-125">Validating this certificate is the responsibility of the web app.</span></span> <span data-ttu-id="a0253-126">Veja o exemplo de código ASP.NET que valida as propriedades do certificado para fins de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a0253-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

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
            // Read the certificate from the header into an X509Certificate2 object
            // Display properties of the certificate on the page
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
                // In this example we will only accept the certificate as a valid certificate if all the conditions below are met:
                // 1. The certificate is not expired and is active for the current time on server.
                // 2. The subject name of the certificate has the common name nildevecc
                // 3. The issuer name of the certificate has the common name nildevecc and organization name Microsoft Corp
                // 4. The thumbprint of the certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained to a Trusted Root Authority (or revoked) on the server 
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

                // If you also want to test if the certificate chains to a Trusted Root Authority you can uncomment the code below
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
