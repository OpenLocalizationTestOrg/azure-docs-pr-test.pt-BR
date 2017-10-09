1. Faça logon no toohello [portal do Azure][Azure portal].
2. No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **integração corporativa**e, em seguida, clique em **retransmissão**.
3. Em Olá **criar namespace** caixa de diálogo, digite um nome de namespace. sistema de saudação imediatamente verifica toosee se Olá nome está disponível.
4. Em Olá **assinatura** campo, escolha uma assinatura do Azure no qual namespace de saudação toocreate.
5. Em Olá  **[grupo de recursos](../articles/azure-resource-manager/resource-group-portal.md)**  campo, escolha um grupo de recursos existente no qual Olá namespace ao vivo ou criar um novo.      
6. Em **local**, escolha o país de saudação ou região em que o namespace deve ser hospedado.
   
    ![Criar um namespace][create-namespace]
7. Clique em **Criar**. sistema de saudação agora cria seu namespace e permite que ele. Depois de alguns minutos, Olá sistema Provisione recursos para sua conta.

### <a name="obtain-hello-management-credentials"></a>Obter credenciais de gerenciamento Olá
1. Na lista de saudação de namespaces, clique Olá recém-criada em nome do namespace.
2. Na folha de namespace hello, clique em **políticas de acesso compartilhado**.
3. Em Olá **políticas de acesso compartilhado** folha, clique em **RootManageSharedAccessKey**.
   
    ![informações de conexão][connection-info]
4. Em Olá **política: RootManageSharedAccessKey** folha, clique o botão de cópia de Olá Avançar muito**chave primária cadeia de caracteres de Conexão**, toocopy Olá conexão cadeia tooyour na área de transferência para uso posterior. Cole esse valor no Bloco de notas ou em outro local temporário.
   
    ![connection-string][connection-string]

5. Etapa anterior Olá repetida, copiar e colar o valor de saudação do **chave primária** tooa o local temporário para uso posterior.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
