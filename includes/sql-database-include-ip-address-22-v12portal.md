
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. Entre no [Portal do Azure](https://portal.azure.com/).

2. Na lista à esquerda, selecione **Procurar**. 

3. Role e selecione **servidores SQL**. 
   
    ![Encontre o seu servidor do Banco de Dados SQL no portal][b21-FindServerInPortal]
4. Para sua conveniência, minimizar a folha **Procurar**.

5. Na caixa de texto de filtro, comece digitando o nome do seu servidor. A linha é exibida.

6. Selecione a linha do servidor. Uma folha do servidor é exibida.

7. Na folha do seu servidor, selecione **Configurações**. 

8. Selecione **Firewall**. 
   
    ![Selecione Configurações > Firewall][b31-SettingsFirewallNavig]
9. Selecione **Adicionar Cliente IP**. Digite um nome para a nova regra na primeira caixa de texto.

10. Digite os valores baixos e altos de endereços IP para o intervalo que deseja habilitar.
    
    * Pode ser útil ter o valor baixo terminado com **0,0** e o valor alto terminado com **0,255**.
    
    ![Adicionar um intervalo de endereços IP para permitir][b41-AddRange]
11. Selecione **Salvar**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
