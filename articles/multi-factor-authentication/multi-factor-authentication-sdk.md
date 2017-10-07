---
title: aaaMFA software development kit para aplicativos personalizados | Microsoft Docs
description: "Este artigo mostra como toodownload e use Olá verificação do SDK do Azure MFA tooenable em duas etapas para seus aplicativos personalizados."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Criando uma autenticação multifator em aplicativos personalizados (SDK)

Olá possibilita a Azure multi-Factor Authentication Software Development Kit (SDK) Olá que criação de verificação em duas etapas diretamente na entrada ou transação processos de aplicativos no seu locatário do AD do Azure.

Olá SDK multi-Factor Authentication está disponível para c#, Visual Basic (.NET), Java, Perl, PHP e Ruby. Olá SDK fornece um wrapper fino em torno de verificação em duas etapas. Ele inclui tudo o que você precisa toowrite seu código, incluindo arquivos de código fonte comentados, arquivos de exemplo e um arquivo Leiame detalhado. Cada SDK também inclui um certificado e a chave privada para criptografar transações que são exclusivo tooyour provedor de autenticação multifator. Contanto que você tenha um provedor, você pode baixar Olá SDK nos tantos idiomas e formatos conforme necessário.

estrutura Olá Olá APIs no SDK multi-Factor Authentication da saudação é simple. Fazer com que uma função chamada tooan API com parâmetros de opção multifator hello (como o modo de verificação) e dados de usuário (como toocall de número de telefone de saudação ou Olá PIN número toovalidate). Olá, APIs traduzem Olá chamada de função em toohello de solicitações de serviços web serviço baseado em nuvem do Azure multi-Factor Authentication. Todas as chamadas devem incluir um certificado privado de toohello de referência que é incluído em cada SDK.

Como Olá APIs não têm acesso toousers registrado no Active Directory do Azure, você deve fornecer informações de usuário em um arquivo ou banco de dados. Além disso, Olá APIs não fornecem recursos de gerenciamento de registro ou de usuário, portanto, você precisa toobuild esses processos em seu aplicativo.

> [!IMPORTANT]
> toodownload Olá SDK, você precisa toocreate um provedor de autenticação multifator do Azure, mesmo se você tiver licenças de Azure MFA, AAD Premium ou EMS. Se você criar um provedor de autenticação multifator do Azure para essa finalidade e já tiver licenças, verifique se toocreate Olá provedor com hello **por usuário habilitado** modelo. Em seguida, vincule toohello diretório Olá provedor contém Olá licenças de Azure MFA, o Azure AD Premium ou EMS. Essa configuração garante que você será cobrado somente se você tiver mais de usuários exclusivos usando Olá SDK que número de saudação de licenças que você possui.


## <a name="download-hello-sdk"></a>Baixe o SDK de saudação
Baixar Olá SDK do Azure multi-Factor requer um [provedor do Azure multi-Factor Auth](multi-factor-authentication-get-started-auth-provider.md).  Isso requer uma assinatura completa do Azure, mesmo que você já possua as licenças do Azure MFA, Azure AD Premium ou Enterprise Mobility Suite.  Olá toodownload SDK, navegue toohello Portal de gerenciamento de vários fatores. Você pode acessar portal Olá Gerenciando Olá provedor de autenticação multifator diretamente, ou clicando Olá **"Go toohello portal"** link na página de configurações do serviço MFA de saudação.

### <a name="download-from-hello-azure-classic-portal"></a>Download de saudação portal clássico do Azure
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.
2. Olá esquerda, selecione **do Active Directory**.
3. Na página do Active Directory, Olá, em selecione top Olá **provedores de autenticação multifator**
4. Na parte inferior da saudação selecione **gerenciar**. Uma nova página é aberta.
5. Na saudação à esquerda, na parte inferior da saudação, clique em **SDK**.
   <center>![Baixar](./media/multi-factor-authentication-sdk/download.png)</center>
6. Selecione o idioma de saudação desejado e clicar em links de download associadas uma saudação.
7. Salve o download de saudação.

### <a name="download-from-hello-service-settings"></a>Fazer o download das configurações de serviço Olá
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.
2. Olá esquerda, selecione **do Active Directory**.
3. Clique duas vezes em sua instância do AD do Azure.
4. Com clique superior Olá **configurar**
5. Em autenticação multifator, selecione **Gerenciar configurações de serviço**
   ![Download](./media/multi-factor-authentication-sdk/download2.png)
6. Na página de configurações de serviços hello, na parte inferior da saudação da tela hello clique **Go toohello portal**. Uma nova página é aberta.
   ![Baixar](./media/multi-factor-authentication-sdk/download3a.png)
7. Na saudação à esquerda, na parte inferior da saudação, clique em **SDK**.
8. Selecione o idioma de saudação desejado e clicar em links de download associadas uma saudação.
9. Salve o download de saudação.

## <a name="whats-in-hello-sdk"></a>Novidades no hello SDK
Olá SDK inclui Olá itens a seguir:

* **LEIAME**. Explica como toouse Olá APIs de autenticação multifator em um aplicativo novo ou existente.
* **Arquivos de origem** para Autenticação Multifator
* **Certificado de cliente** que você use toocommunicate com hello serviço multi-Factor Authentication
* **Chave privada** certificado Olá
* **Resultados da chamada.** Uma lista de códigos do resultado da chamada. tooopen esse arquivo, use um aplicativo com formatação de texto, como o WordPad. Olá Use chamar tootest de códigos de resultado e solucionar problemas de implementação de saudação do multi-Factor Authentication em seu aplicativo. Eles não são códigos de status de autenticação.
* **Exemplos.** Código de exemplo para uma implementação básica de trabalho do Multi-Factor Authentication.

> [!WARNING]
> certificado de cliente de saudação é um certificado privado único que foi gerado especialmente para você. Não compartilhe nem perca este arquivo. É a segurança de saudação tooensuring chave das suas comunicações com o serviço de autenticação multifator hello.

## <a name="code-sample"></a>Exemplo de código
Este exemplo de código mostra como toouse Olá APIs em Olá voz de modo padrão do SDK do Azure multi-Factor Authentication tooadd chamar aplicativo tooyour de verificação. O modo padrão é uma chamada telefônica que Olá tooby do usuário responde pressionando a tecla # de saudação.

Este exemplo usa Olá c# .NET 2.0 SDK multi-Factor Authentication em um aplicativo ASP.NET básico com a lógica do lado do servidor c#, mas o processo de saudação é semelhante em outras linguagens. Como Olá SDK inclui arquivos de origem, arquivos não executáveis, você pode criar arquivos de saudação e faz referência a eles ou incluí-los diretamente em seu aplicativo.

> [!NOTE]
> Ao implementar a autenticação multifator, use métodos adicionais de saudação (chamada telefônica ou mensagem de texto) como toosupplement verificação secundária ou terciária seu método de autenticação primária (nome de usuário e senha). Esses métodos não foram desenvolvidos para serem usados como métodos de autenticação primária.

### <a name="code-sample-overview"></a>Visão geral do exemplo de código
Esse código de exemplo para um aplicativo de demonstração simples da web usa uma chamada telefônica com autenticação # resposta de chave tooverify saudação do usuário. Esse fator de chamada telefônica é conhecido no Multi-Factor Authentication como modo padrão.

código do lado do cliente Olá não inclui nenhum elemento específico de autenticação multifator. Como fatores de autenticação adicionais de saudação são independentes da autenticação primária Olá, você pode adicioná-los sem alterar a interface de logon existente hello. Olá APIs em Olá SDK multi-Factor lhe permitem personalizar a experiência do usuário hello, mas talvez não seja necessário toochange nada em todos os.

código do servidor de saudação adiciona a autenticação de modo padrão na etapa 2. Ele cria um objeto de PfAuthParams com parâmetros de saudação que são necessários para a verificação de modo padrão: nome de usuário, o número e o modo de telefone e Olá certificado de cliente caminho toohello (CertFilePath), que é necessário em cada chamada. Para ver uma demonstração de todos os parâmetros no PfAuthParams, consulte o arquivo de exemplo hello em Olá SDK.

Em seguida, o código de saudação passa função pf_authenticate() do hello PfAuthParams objeto toohello. valor de retorno de saudação indica êxito hello ou falha de autenticação de saudação. Olá parâmetros, callStatus e errorID, contêm informações de resultado de chamada adicional. códigos de resultado de chamada Hello estão documentados no arquivo de resultados de chamada hello em Olá SDK.

Essa implementação mínima pode ser escrita apenas em algumas linhas. No entanto, no código de produção, você inclui tratamento de erro mais sofisticado, código adicional de banco de dados e uma experiência de usuário aprimorada.

### <a name="web-client-code"></a>Código do cliente Web
a seguir Olá é código de cliente da web para uma página de demonstração.

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
Olá após o código do lado do servidor, autenticação multifator é configurada e executada na etapa 2. Modo padrão (MODE_STANDARD) é que um usuário de saudação do telefonema toowhich responde pressionando a tecla # de saudação.

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
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
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
