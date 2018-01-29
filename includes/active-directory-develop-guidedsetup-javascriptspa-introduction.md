# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Chamar a API do Microsoft Graph de um SPA (Aplicativo de Página Única) JavaScript

Este guia demonstra como um SPA (Aplicativo de Página Única) JavaScript pode entrar em contas pessoais, corporativas e de estudante, obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso do ponto de extremidade do Azure Active Directory v2.

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como o aplicativo de exemplo gerado por este guia funciona](media/active-directory-develop-guidedsetup-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Mais informações

O aplicativo de exemplo criado por este guia permite que um SPA JavaScript consulte a API do Microsoft Graph ou uma API Web que aceita tokens do ponto de extremidade do Azure Active Directory v2. Para esse cenário, depois que um usuário se conecta, um token de acesso é adicionado às solicitações HTTP por meio do cabeçalho de autorização. A aquisição e a renovação de tokens são manipuladas pela MSAL (Biblioteca de Autenticação da Microsoft).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotecas

Este guia usa a seguinte biblioteca:

|Biblioteca|DESCRIÇÃO|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Versão prévia da Biblioteca de Autenticação da Microsoft para JavaScript|

> [!NOTE]
> *msal.js* usa como destino o *ponto de extremidade do Azure Active Directory v2*, que permite que contas pessoais, corporativas e de estudante entrem e adquiram tokens. O *ponto de extremidade do Azure Active Directory v2* tem [algumas limitações](..\articles\active-directory\develop\active-directory-v2-limitations.md). Se você estiver interessado apenas em contas corporativas e de estudante, use *adal.js* e o *ponto de extremidade V1*. Para entender as diferenças entre os pontos de extremidade v1 e v2, leia a [comparação v1-v2](..\articles\active-directory\develop\active-directory-v2-compare.md).

<!--end-collapse-->
