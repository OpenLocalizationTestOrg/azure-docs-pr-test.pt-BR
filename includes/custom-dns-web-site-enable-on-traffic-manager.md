Depois de tem sido propagadas registros Olá para seu nome de domínio, você deve ser capaz de toouse tooverify seu navegador que seu nome de domínio personalizado pode ser usado tooaccess seu aplicativo web no serviço de aplicativo do Azure.

> [!NOTE]
> Ele pode levar algum tempo para sua toopropagate CNAME por meio de saudação sistema DNS. Você pode usar um serviço, como <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify que Olá CNAME está disponível.
> 
> 

Se você ainda não adicionou seu aplicativo web como um ponto de extremidade do Traffic Manager, você deve fazer isso antes de resolução de nomes funcione, como Olá domínio personalizado nome rotas tooTraffic Manager. Em seguida, o Traffic Manager roteia tooyour web app. Use as informações de saudação em [adicionar ou excluir pontos de extremidade](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd seu aplicativo da web como um ponto de extremidade no perfil do Traffic Manager.

> [!NOTE]
> Se seu aplicativo Web não estiver listado, ao adicionar um ponto de extremidade, verifique se ele está configurado como **Padrão** no modo do plano de Serviço de Aplicativo. Você deve usar **padrão** modo para seu aplicativo web em ordem toowork com o Gerenciador de tráfego.
> 
> 

1. No navegador, abra Olá [Portal do Azure](https://portal.azure.com).
2. Em Olá **aplicativos Web** , clique em nome de saudação do seu aplicativo web, selecione **configurações**e, em seguida, selecione **domínios personalizados**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Em Olá **domínios personalizados** folha, clique em **Adicionar nome de host**.
4. Saudação de uso **Hostname** texto caixas tooenter Olá Traffic Manager domínio nome tooassociate com este aplicativo web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Clique em **validar** toosave configuração de nome de domínio de saudação.
6. Ao clicar em **Validar** , o Azure iniciará o fluxo de trabalho de verificação de domínio. Isso irá verificar propriedade de domínio, bem como o sucesso de disponibilidade e o relatório de nome de host ou detalhadas de erro com a diretriz prescritiva sobre como toofix Olá erro.    
7. Após a validação bem-sucedida **Adicionar nome de host** botão se tornará ativo e você será capaz de toohello atribuir nome do host. Agora, navegar tooyour o nome de domínio personalizado em um navegador. Agora você verá seu aplicativo em execução usando seu nome de domínio personalizado. 
   
   Depois que a configuração for concluída, o nome de domínio personalizado Olá será listado no hello **nomes de domínio** seção de seu aplicativo web.

Neste ponto, você deve ser capaz de tooenter Olá Traffic Manager nome em seu navegador e veja que isso com êxito leva você tooyour web app.

