---
title: Kit de desenvolvimento de software MFA para aplicativos personalizados | Microsoft Docs
description: "Este artigo mostra como baixar e usar o SDK do Azure MFA para habilitar a verificação em duas etapas para seus aplicativos personalizados."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: joflore
ms.openlocfilehash: 7ae89241c67655fbcaa747c4cac224b898947f39
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Criando uma autenticação multifator em aplicativos personalizados (SDK)

> [!IMPORTANT]
> A reprovação do SDK (Software Development Kit) da Autenticação Multifator do Azure foi anunciada. Não haverá mais suporte para esse recurso para novos clientes. Os clientes atuais podem continuar usando o SDK até 14 de novembro de 2018. Após essa data, as chamadas para o SDK falharão. 

O SDK (Software Development Kit) da Autenticação Multifator do Azure permite que você crie verificação em duas etapas diretamente nos processos de transação ou entrada de aplicativos no locatário do Azure AD.

O SDK da Autenticação Multifator está disponível para C#, Visual Basic (.NET), Java, Perl, PHP e Ruby. O SDK fornece um thin wrapper em torno da verificação em duas etapas. Ele inclui tudo o que você precisa para escrever seu código, incluindo arquivos de código-fonte comentados, arquivos de exemplo e um arquivo Leiame detalhado. Cada SDK também inclui um certificado e a chave privada para criptografar transações, que é exclusiva do seu Provedor de Autenticação Multifator. Desde que você tenha um provedor, é possível baixar o SDK em quantos formatos e idiomas precisar.

A estrutura das APIs no SDK da Autenticação Multifator é bastante simples. Você faz uma única chamada de função a uma API com os parâmetros de opção de multifator, como o modo de verificação, e dados do usuário (como o número de telefone para o qual ligar ou o número PIN a ser validado). As APIs convertem a chamada de função em solicitações de serviço Web para o Serviço de Autenticação Multifator do Azure baseado na nuvem. Todas as chamadas devem incluir uma referência ao certificado privado que é incluído em cada SDK.

Como as APIs não têm acesso aos usuários registrados no Active Directory do Azure, você deve fornecer informações do usuário, como números de telefone e códigos PIN, em um arquivo ou banco de dados. Além disso, as APIs não fornecem recursos de gerenciamento de usuários e registros, de modo que você precisa criar esses processos em seu aplicativo.

> [!IMPORTANT]
> Para baixar o SDK, crie um Provedor de Autenticação Multifator do Azure mesmo que você tenha as licenças MFA, AAD Premium ou EMS do Azure. Se você criar um Provedor de Autenticação Multifator do Azure para essa finalidade e já tiver licenças, crie o Provedor com o modelo **Por Usuário Habilitado**. Em seguida, vincule o Provedor ao diretório que contém as licenças MFA, Azure AD Premium ou EMS do Azure. Isso garantirá que você não será cobrado, caso tenha mais usuários exclusivos usando o SDK do que o número de licenças possuídas.


## <a name="download-the-sdk"></a>Baixar o SDK
Baixar o SDK do Azure Multi-Factor requer um [Provedor do Azure Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).  Isso requer uma assinatura completa do Azure, mesmo que você já possua as licenças do Azure MFA, Azure AD Premium ou Enterprise Mobility Suite. Os métodos públicos para fazer o download do SDK foram desativados uma vez que o SDK tornou-se preterido. Caso precise baixar o SDK, será necessário abrir um caso de suporte com a Microsoft. O SDK é fornecido apenas para clientes que já estão usando o SDK. Novos clientes não poderão ser incorporados.

## <a name="whats-in-the-sdk"></a>O que há no SDK
O SDK inclui os seguintes itens:

* **LEIAME**. Explica como usar as APIs da Autenticação Multifator em um aplicativo novo ou existente.
* **Arquivos de origem** para Autenticação Multifator
* **Certificado do cliente** que você usa para se comunicar com o serviço de Autenticação Multifator
* **Chave privada** do certificado
* **Resultados da chamada.** Uma lista de códigos do resultado da chamada. Para abrir esse arquivo, use um aplicativo com formatação de texto, como o WordPad. Use os códigos do resultado da chamada para testar e solucionar problemas de implementação da Autenticação Multifator no aplicativo. Eles não são códigos de status de autenticação.
* **Exemplos.** Código de exemplo para uma implementação básica de trabalho da Autenticação Multifator.

> [!WARNING]
> O certificado do cliente é um certificado privado único que foi gerado especialmente para você. Não compartilhe nem perca este arquivo. Ele é sua chave para garantir a segurança da comunicação com o serviço de Autenticação Multifator.

## <a name="code-sample"></a>Exemplo de código
Este exemplo de código mostra como usar as APIs no SDK da Autenticação Multifator do Azure para adicionar verificação de chamada de voz no modo padrão ao seu aplicativo. O modo padrão é uma chamada telefônica à qual o usuário responde pressionando a tecla #.

Este exemplo usa o SDK da Autenticação Multifator .NET 2.0 do C# em um aplicativo básico ASP.NET com a lógica do servidor C#, mas o processo é bastante semelhante a implementações simples em outras linguagens. Como o SDK inclui arquivos de origem, e não arquivos executáveis, você pode criar os arquivos e fazer referência a eles ou incluí-los diretamente no aplicativo.

> [!NOTE]
> Ao implementar a Autenticação Multifator, use os fatores adicionais (chamada telefônica ou mensagem de texto) como verificação secundária ou terciária para complementar seu método de autenticação primária (senha e usuário). Esses métodos não foram desenvolvidos para serem usados como métodos de autenticação primária.

### <a name="code-sample-overview"></a>Visão geral do exemplo de código
Este código de exemplo de um aplicativo de demonstração na Web bastante simples usa uma chamada telefônica com uma resposta pela tecla # para concluir a autenticação do usuário. Esse fator de chamada telefônica é conhecido na Autenticação Multifator como modo padrão.

O código do lado do cliente não inclui nenhum elemento específico da Autenticação Multifator. Como os fatores de autenticação adicionais são independentes da autenticação primária, você pode adicioná-los sem alterar a interface de logon existente. As APIs no SDK do Multi-Factor permitem personalizar a experiência do usuário, mas talvez você não precise alterar nada.

O código do servidor adiciona a autenticação no modo padrão na Etapa 2. Ele cria um objeto PfAuthParams com os parâmetros que são necessários para a verificação no modo padrão: nome do usuário, número de telefone, modo e o caminho para o certificado do cliente (CertFilePath), que é necessário em cada chamada. Para uma demonstração de todos os parâmetros no PfAuthParams, consulte o arquivo de exemplo no SDK.

Em seguida, o código passa do objeto PfAuthParams para a função pf_authenticate(). O valor de retorno indica o êxito ou a falha da autenticação. Os parâmetros de saída, callStatus e errorID, contêm informações adicionais do resultado da chamada. Os códigos do resultado da chamada são documentados no arquivo de resultados da chamada no SDK.

Essa implementação mínima pode ser escrita apenas em algumas linhas. No entanto, no código de produção, você inclui tratamento de erro mais sofisticado, código adicional de banco de dados e uma experiência de usuário aprimorada.

### <a name="web-client-code"></a>Código do cliente Web
Veja a seguir o código do cliente Web para uma página de demonstração.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Código do servidor
No código de servidor a seguir, a Autenticação Multifator é configurado e executado na Etapa 2. O modo padrão (MODE_STANDARD) é uma chamada telefônica à qual o usuário responde pressionando a tecla #.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
