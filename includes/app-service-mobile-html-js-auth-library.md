### <a name="server-auth"></a>Como autenticar com um provedor (fluxo de servidor)
os aplicativos móveis toohave gerenciar o processo de autenticação de saudação em seu aplicativo, você deve registrar seu aplicativo com seu provedor de identidade. Em seguida, em seu serviço de aplicativo do Azure, você precisa tooconfigure Olá ID e segredo fornecida pelo seu provedor.
Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicativo](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Depois que você registrou o seu provedor de identidade, chamar hello `.login()` método com nome de saudação do seu provedor. Por exemplo, toologin com o Facebook usar Olá código a seguir:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

os valores válidos para o provedor de Olá Olá são 'aad', 'facebook', 'google', 'conta da Microsoft' e 'twitter'.

> [!NOTE]
> Atualmente, a Autenticação do Google não funciona por meio de Fluxo de Servidor.  tooauthenticate com o Google, você deve usar um [método cliente fluxo](#client-auth).

Nesse caso, o serviço de aplicativo do Azure gerencia o fluxo de autenticação Olá OAuth 2.0.  Exibe a página de logon de saudação do provedor selecionado hello e gera um token de autenticação do serviço de aplicativo após o logon com êxito com o provedor de identidade hello. função de logon Hello, quando concluído, retorna um objeto JSON que expõe Olá ID de usuário e o serviço de aplicativo token de autenticação nos campos de identificação do usuário e authenticationToken hello, respectivamente. Esse token pode ser armazenado em cache e reutilizado até que expire.

###<a name="client-auth"></a>Como autenticar com um provedor (fluxo de cliente)

Seu aplicativo pode também independentemente entre em contato com o provedor de identidade hello e forneça Olá retornado tooyour token do serviço de aplicativo para autenticação. Esse fluxo de cliente permite que você tooprovide uma experiência de logon único para usuários ou dados de usuário adicionais tooretrieve saudação do provedor de identidade.

#### <a name="social-authentication-basic-example"></a>Exemplo básico de autenticação social

Este exemplo usa o SDK de cliente do Facebook para a autenticação:

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
Este exemplo assume esse token Olá fornecido pelo provedor respectivos Olá SDK é armazenado na variável de token de saudação.

#### <a name="microsoft-account-example"></a>Exemplo de conta da Microsoft

Olá seguindo o exemplo usa Olá Live SDK, que oferece suporte a single-sign-on para aplicativos da Windows Store usando Account da Microsoft:

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

Este exemplo obtém um token do Live Connect, que é fornecido tooyour do serviço de aplicativo chamando a função de logon hello.

###<a name="auth-getinfo"></a>Como: obter informações sobre o usuário autenticado de saudação

informações de autenticação Olá podem ser recuperadas da saudação `/.auth/me` chamada de ponto de extremidade usando um HTTP com qualquer biblioteca AJAX.  Certifique-se de que você definir Olá `X-ZUMO-AUTH` token de autenticação do cabeçalho tooyour.  Olá token de autenticação é armazenado no `client.currentUser.mobileServiceAuthenticationToken`.  Por exemplo, toouse Olá busca API:

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

O Fetch está disponível como um [pacote npm](https://www.npmjs.com/package/whatwg-fetch) ou para download do navegador do [CDNJS](https://cdnjs.com/libraries/fetch). Você também pode usar outras informações de saudação de toofetch de API do AJAX ou jQuery.  Os dados são recebidos como um objeto JSON.
