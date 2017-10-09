saudação de sistema de nome de domínio (DNS) é usado toolocate recursos Olá internet. Por exemplo, quando você inserir um endereço de aplicativo da web no navegador ou em um link em uma página da web, ele usa domínio DNS à saudação tootranslate em um endereço IP. endereço IP de saudação é semelhante a um endereço de rua, mas não é muito humana amigável. Por exemplo, é muito mais fácil tooremember um nome DNS como **contoso.com** que ele é tooremember um endereço IP como 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Olá sistema DNS se baseia *registros*. Os registros associam um determinado *nome*, como **contoso.com**, a um endereço IP ou a outro nome DNS. Quando um aplicativo, como um navegador da web, é um nome no DNS, ele localiza registro hello e usa tudo o que ele aponte tooas Olá endereço. Se Olá se o valor toois pontos de um endereço IP, o navegador Olá usará esse valor. Se ele aponta o nome DNS tooanother, aplicativo hello tem resolução toodo novamente. Em última análise, todas as resoluções de nome acabarão em um endereço IP.

Quando você cria um aplicativo web no serviço de aplicativo, um nome DNS é automaticamente atribuído toohello web app. Esse nome assume a forma de saudação de  **&lt;yourwebappname&gt;. azurewebsites.net**. Também há um endereço IP virtual disponível para uso quando a criação de DNS de registros, para que você pode criar registros que toohello ponto **. azurewebsites.net**, ou você pode apontar o endereço IP toohello.

> [!NOTE]
> endereço IP de saudação do seu aplicativo web será alterado se você excluir e recria seu aplicativo web ou alterar Olá modo do plano de serviço de aplicativo muito**livre** depois de ter sido definido muito**básica**, **compartilhado**, ou **padrão**.
> 
> 

Também existem vários tipos de registros, cada um com suas próprias funções e limitações, mas, para aplicativos Web, nos preocupamos apenas com dois, os registros *A* e *CNAME*.

### <a name="address-record-a-record"></a>Registro de endereço (registro A)
Um registro mapeia um domínio, como **contoso.com** ou **www.contoso.com**, *ou um domínio curinga* como  **\*. contoso.com**, endereço IP tooan. No caso de saudação de um aplicativo web no serviço de aplicativo, o hello IP virtual do serviço de saudação ou um endereço IP específico que você comprou para seu aplicativo web.

Olá principais benefícios de um registro em um registro CNAME são:

* Você pode mapear um domínio raiz, como **contoso.com** tooan endereço IP; muitos registradores permitem apenas esse registros usando
* É possível ter uma entrada que usa um curinga, como **\*.contoso.com**, que lidaria com solicitações para vários subdomínios, como **mail.contoso.com**, **blogs.contoso.com** ou **www.contso.com**.

> [!NOTE]
> Como um registro é mapeado tooa endereço IP, ele não é possível resolver automaticamente alterações toohello endereço IP de seu aplicativo web. Um endereço IP para uso com registros é fornecido quando você configura as configurações de nome de domínio personalizado para seu aplicativo da web; No entanto, esse valor pode ser alterado se você excluir e recria seu aplicativo web ou alterar Olá tooback de modo do plano de serviço de aplicativo muito**livre**.
> 
> 

### <a name="alias-record-cname-record"></a>Registro de Alias (registro CNAME)
Um registro CNAME mapeia um *específico* nome DNS, como **mail.contoso.com** ou **www.contoso.com**, nome de domínio (canônico) tooanother. No caso de saudação do serviço de aplicativo Web de aplicativos, o nome de domínio canônico Olá é hello  **&lt;yourwebappname >. azurewebsites.net** nome de domínio do seu aplicativo web. Depois de criado, Olá CNAME cria um alias para Olá  **&lt;yourwebappname >. azurewebsites.net** nome de domínio. Olá entrada CNAME resolverá toohello endereço IP do seu  **&lt;yourwebappname >. azurewebsites.net** nome de domínio automaticamente, para que se o endereço IP de saudação do aplicativo web de saudação for alterada, você não tem tootake qualquer ação.

> [!NOTE]
> Alguns registradores de domínio só permitem que você toomap subdomínios ao usar um registro CNAME, como **www.contoso.com**e não raiz nomes, como **contoso.com**. Para obter mais informações sobre os registros CNAME, consulte a documentação de saudação fornecida por seu registrador <a href="http://en.wikipedia.org/wiki/CNAME_record">Olá entrada da Wikipedia no registro CNAME</a>, ou hello <a href="http://tools.ietf.org/html/rfc1035">nomes de domínio IETF - implementação e especificação</a> documento.
> 
> 

### <a name="web-app-dns-specifics"></a>Dados específicos de DNS do aplicativo Web
Usar um registro com aplicativos da Web exige que você toofirst criar uma saudação registros TXT a seguir:

* **Para o domínio raiz da saudação** -registro TXT do DNS de um de  **@**  muito  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Para um subdomínio específico** -nome de DNS do  **&lt;subdomínio >** muito**&lt;yourwebappname&gt;. azurewebsites.net**. Por exemplo, **blogs** se Olá um registro é para **blogs.contoso.com**.
* **Para Olá curinga sub-dodmains** -registro TXT do DNS de um de * muito  **&lt;yourwebappname&gt;. azurewebsites.net**.

Esse registro TXT é usado tooverify que você possui o domínio Olá que você está tentando executar toouse. Além disso, este é o registro de toocreating um A apontando toohello de endereço IP virtual de seu aplicativo web.

Você pode encontrar o endereço IP hello e **. azurewebsites.net** Olá nomes para seu aplicativo web executando as etapas a seguir:

1. No navegador, abra Olá [Portal do Azure](https://portal.azure.com).
2. Em Olá **aplicativos Web** folha, clique em nome de saudação do seu aplicativo web e, em seguida, selecione **domínios personalizados** Olá página de baixo hello.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Em Olá **domínios personalizados** folha, você verá Olá endereço IP virtual. Salve essas informações, pois elas serão utilizadas na criação de registros DNS
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > Não é possível usar nomes de domínio personalizado com um **livre** aplicativo da web e atualize Olá plano de serviço de aplicativo muito**compartilhado**, **básica**, **padrão**, ou **Premium** camada. Para obter mais informações sobre saudação do serviço de aplicativo plano precificação do camadas, incluindo como toochange Olá preço de seu aplicativo web, consulte [como aplicativos de web tooscale](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

