## <a name="what-are-service-bus-topics-and-subscriptions"></a>O que são os tópicos e as assinaturas do Barramento de Serviço?
Os tópicos e assinaturas do Barramento de Serviço dão suporte a um modelo de comunicação de mensagens de *publicação/assinatura* . Durante o uso de tópicos e assinaturas, os componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, eles trocam mensagens por meio de um tópico, que atua como um intermediário.

![Conceitos de tópico](./media/howto-service-bus-topics/sb-topics-01.png)

Em contraste com as filas do Barramento de Serviço, em que cada mensagem é processada por um único consumidor, tópicos e assinaturas fornecem uma forma de comunicação de um para muitos usando um padrão de publicação/assinatura. É possível registrar o tópico de tooa várias assinaturas. Quando uma mensagem é enviada tooa tópico, ele é feito tooeach disponível assinatura toohandle/processo independentemente.

Um tópico de tooa de assinatura é semelhante a uma fila virtual que recebe cópias das mensagens de saudação enviadas toohello tópico. Opcionalmente, você pode registrar as regras de filtro para um tópico em uma base por assinatura, que permite que você toofilter ou restringir o tópico de tooa quais mensagens são recebidas por quais assinaturas de tópico.

As assinaturas e tópicos do barramento de serviço permitem que você tooscale e processam um número muito grande de mensagens entre vários usuários e aplicativos.

## <a name="create-a-namespace"></a>Criar um namespace
toobegin usando assinaturas e tópicos do barramento de serviço no Azure, você deve primeiro criar um *namespace de serviço*. Um namespace fornece um contêiner de escopo para endereçar recursos do barramento de serviço dentro de seu aplicativo.

toocreate um namespace:

1. Faça logon no toohello [portal do Azure][Azure portal].
2. No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, em seguida, clique em **integração corporativa**e, em seguida, clique em **barramento de serviço**.
3. Em Olá **criar namespace** caixa de diálogo, digite um nome de namespace. sistema de saudação imediatamente verifica toosee se Olá nome está disponível.
4. Depois de fazer o nome do namespace Olá-se de que está disponível, escolha Olá preço (Basic, Standard ou Premium).
5. Em Olá **assinatura** campo, escolha uma assinatura do Azure no qual namespace de saudação toocreate.
6. Em Olá **grupo de recursos** campo, escolha um grupo de recursos existente no qual Olá namespace ao vivo ou criar um novo.      
7. Em **local**, escolha o país de saudação ou região em que o namespace deve ser hospedado.
   
    ![Criar um namespace][create-namespace]
8. Clique em Olá **criar** botão. sistema de saudação agora cria seu namespace e permite que ele. Você pode ter toowait vários minutos como recursos de provisões de sistema Olá para sua conta.

### <a name="obtain-hello-credentials"></a>Obter credenciais Olá
1. Na lista de saudação de namespaces, clique Olá recém-criada em nome do namespace.
2. Em Olá **namespace de barramento de serviço** folha, clique em **políticas de acesso compartilhado**.
3. Em Olá **políticas de acesso compartilhado** folha, clique em **RootManageSharedAccessKey**.
   
    ![informações de conexão][connection-info]
4. Em Olá **política: RootManageSharedAccessKey** folha, clique o botão de cópia de Olá Avançar muito**chave primária cadeia de caracteres de Conexão**, toocopy Olá conexão cadeia tooyour na área de transferência para uso posterior.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


