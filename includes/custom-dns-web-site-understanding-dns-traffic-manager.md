saudação de sistema de nome de domínio (DNS) é usado toolocate itens Olá internet. Por exemplo, quando você inserir um endereço no navegador, ou clique em um link em uma página da web, ele usa domínio DNS à saudação tootranslate em um endereço IP. endereço IP de saudação é semelhante a um endereço de rua, mas não é muito humana amigável. Por exemplo, é muito mais fácil tooremember um nome DNS como **contoso.com** que ele é tooremember um endereço IP como 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Olá sistema DNS se baseia *registros*. Os registros associam um determinado *nome*, como **contoso.com**, a um endereço IP ou a outro nome DNS. Quando um aplicativo, como um navegador da web, é um nome no DNS, ele localiza registro hello e usa tudo o que ele aponte tooas Olá endereço. Se Olá se o valor toois pontos de um endereço IP, o navegador Olá usará esse valor. Se ele aponta o nome DNS tooanother, aplicativo hello tem resolução toodo novamente. Em última análise, todas as resoluções de nome acabarão em um endereço IP.

Quando você cria um site do Azure, um nome DNS é automaticamente toohello site atribuído. Esse nome assume a forma de saudação de  **&lt;yoursitename&gt;. azurewebsites.net**. Quando você adiciona o seu site como um ponto de extremidade do Azure Traffic Manager, seu site seja acessível por meio de saudação  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** domínio.

> [!NOTE]
> Quando seu site estiver configurado como um ponto de extremidade do Traffic Manager, você usará Olá **. trafficmanager.net** endereço ao criar registros DNS.
> 
> Só é possível usar registros CNAME com o Gerenciador de Tráfego
> 
> 

Também há vários tipos de registros, cada um com suas próprias funções e limitações, mas para sites configurados tooas pontos de extremidade do Gerenciador de tráfego, só é importante para nós sobre um; *CNAME* registros.

### <a name="cname-or-alias-record"></a>Registro CNAME ou de alias
Um registro CNAME mapeia um *específico* nome DNS, como **mail.contoso.com** ou **www.contoso.com**, nome de domínio (canônico) tooanother. No caso de saudação de sites do Azure usando o Gerenciador de tráfego, o nome de domínio canônico Olá é hello  **&lt;myapp >. trafficmanager.net** nome de domínio do seu perfil do Gerenciador de tráfego. Depois de criado, Olá CNAME cria um alias para Olá  **&lt;myapp >. trafficmanager.net** nome de domínio. Olá entrada CNAME resolverá toohello endereço IP do seu  **&lt;myapp >. trafficmanager.net** nome de domínio automaticamente, para que se mudar de endereço IP de saudação do site hello, você não tem tootake qualquer ação.

Depois que o tráfego chega no Gerenciador de tráfego, em seguida, ele encaminha o hello tráfego tooyour site da Web, usando Olá método balanceamento de carga para que é configurado. Isso é completamente transparente toovisitors tooyour site. Eles verão somente o nome de domínio personalizado Olá no seu navegador.

> [!NOTE]
> Alguns registradores de domínio só permitem que você toomap subdomínios ao usar um registro CNAME, como **www.contoso.com**e não raiz nomes, como **contoso.com**. Para obter mais informações sobre os registros CNAME, consulte a documentação de saudação fornecida por seu registrador <a href="http://en.wikipedia.org/wiki/CNAME_record">Olá entrada da Wikipedia no registro CNAME</a>, ou hello <a href="http://tools.ietf.org/html/rfc1035">nomes de domínio IETF - implementação e especificação</a> documento.
> 
> 

