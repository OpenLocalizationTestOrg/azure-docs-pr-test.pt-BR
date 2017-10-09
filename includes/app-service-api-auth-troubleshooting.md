A maioria dos erros de autenticação de tempo de saudação ser das definições de configuração inconsistentes ou incorretos. Aqui estão algumas sugestões específicos para toocheck coisas.

* Certifique-se de que você não perdeu Olá **salvar** botão em qualquer lugar. Isso geralmente é fácil toodo e resultado de saudação é que você vai estar olhando para valores corretos da saudação em uma página de portal, mas, na verdade, ainda não foram salvas no hello ambiente do Azure ou o aplicativo do AD do Azure.
* Para as configurações definidas no hello **configurações de aplicativo** folha de saudação portal do Azure, certifique-se de que Olá correto de aplicativo de API ou aplicativo web foi selecionado durante a saudação configurações foram inseridas.  Também verifique se as configurações de saudação foram inseridas como **configurações do aplicativo** e não **cadeias de caracteres de Conexão**, como o formato Olá seções Olá dois é semelhante.
* Para autenticação tooa front-end JavaScript, Olá download novamente manifesto tooverify que `oauth2AllowImplicitFlow` foi alterada com êxito muito`true`.
* Verifique se você usou HTTPS sempre ao configurar URLs:
  
  * No código do projeto
  * No CORS
  * Nas configurações do Aplicativo do ambiente do Azure para cada aplicativo de API e aplicativo Web
  * Nas configurações do aplicativo do Azure AD.
    
    Observe que se você copiar URL de um aplicativo de API do portal de saudação, ela geralmente tem `http://` e você tiver toomanually alterá-la muito`https://`.
* Certifique-se de que as alterações de código foram implantadas com êxito. Por exemplo, em uma solução de vários projetos é possível toochange um projeto do código e acidentalmente escolha uma das Olá outras pessoas quando você pretende alterar de saudação toodeploy.
* Certifique-se de que você vai tooHTTPS URLs no navegador, não as URLs de HTTP. Por padrão, o Visual Studio cria perfis com HTTP URLs de publicação, e isso é o que abre no navegador de saudação depois de implantar um projeto.
* Para autenticação tooa front-end JavaScript, certifique-se de que CORS está configurado corretamente no aplicativo de API Olá Olá chamadas de código JavaScript. Em caso de dúvida sobre se o problema de saudação está relacionado ao CORS, tente "*" como Olá permitido URL de origem. 
* Para um front-end JavaScript, abra tooget de guia Console de ferramentas de desenvolvedor do seu navegador mais informações de erro e examinar as solicitações HTTP em Olá rede. No entanto, mensagens de erro do Console podem ser confusas. Se você receber uma mensagem indicando um erro CORS, problema real Olá pode ser a autenticação. Você pode verificar se esse é o caso de Olá executando o aplicativo hello com autenticação temporariamente temporariamente desabilitada.
* Para um aplicativo de API .NET, verifique se você estiver obtendo as informações em mensagens de erro possível definindo [customErrors modo tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* Para um aplicativo de API .NET, iniciar um [sessão de depuração remota](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)e examinar os valores de saudação de variáveis de saudação que são passados toocode que usa ADAL tooacquire um token de portador ou código que verifica as declarações em relação a saudação esperada ID de serviço principal. Observe que o seu código pode selecionar valores de configuração de várias fontes diferentes, portanto, é possível toofind surpresas dessa maneira. Por exemplo, se você digitar incorretamente `ida:ClientId` como `ida:ClientID` quando definir as configurações de ambiente do serviço de aplicativo do Azure, código de saudação pode receber Olá `ida:ClientId` valor que está procurando do arquivo Web. config de hello, ignorando a configuração de serviço de aplicativo do Azure de saudação. 
* Se as coisas não funcionarem em uma janela normal do Internet Explorer, um logon existente poderá estar interferindo; tente usar a navegação InPrivate no Chrome ou Firefox.

