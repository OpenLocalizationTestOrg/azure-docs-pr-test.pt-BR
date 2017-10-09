
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Faça logon no toohello [portal do Azure](https://portal.azure.com/) em http://portal.azure.com/.
2. Na faixa de saudação à esquerda, clique em **procurar todas as**. Olá **procurar** folha é exibida.
3. Role e clique em **servidores SQL**. Olá **servidores SQL** folha é exibida.
   
    ![Localize o servidor de banco de dados SQL no portal de saudação][b21-FindServerInPortal]
4. Para sua conveniência, clique em Olá minimizar controle Olá anteriormente **procurar** folha.
5. Na caixa de texto de filtro Olá, comece a digitar o nome de saudação do servidor. A linha é exibida.
6. Clique em linha de saudação do servidor. Uma folha do servidor é exibida.
7. Na folha do seu servidor, clique em **Configurações**. Olá **configurações** folha é exibida.
8. Clique em **Firewall**. Olá **as configurações do Firewall** folha é exibida.
   
    ![Clique em Configurações > Firewall][b31-SettingsFirewallNavig]
9. Clique em **Adicionar Cliente IP**. Digite um nome para a nova regra na primeira caixa de texto de saudação.
10. Valores de intervalo de saudação desejado de endereços IP tipo no hello baixa e alta tooenable.
    
    * Ele pode ser útil toohave Olá baixo valor final com **.0** e hello alta com **.255**.
    
    ![Adicionar um tooallow de intervalo de endereço IP][b41-AddRange]
11. Clique em **Salvar**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
