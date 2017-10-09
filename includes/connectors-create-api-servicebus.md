### <a name="prerequisites"></a>Pré-requisitos
Você deve ter uma conta do [Barramento de Serviço](https://azure.microsoft.com/services/service-bus/).  

Antes de usar sua conta do Azure Service Bus em um aplicativo lógico, é necessário autorizar a conta do hello lógica aplicativo tooconnect tooyour service bus. Felizmente, você pode fazer isso facilmente a partir de dentro de seu aplicativo lógica em Olá portal do Azure.  

Aqui está Olá etapas tooauthorize tooyour de tooconnect de aplicativo sua lógica conta do barramento de serviço:  

1. toocreate tooService uma conexão barramento, no designer de aplicativo de lógica de saudação, selecione **APIs gerenciadas do Microsoft Mostrar** na lista suspensa de saudação. Em seguida, digite **barramento de serviço** na caixa de pesquisa de saudação. Selecione o disparador hello ou ação que você deseja toouse.  
    ![Imagem de conexão do Barramento de Serviço 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Se você não criou nenhum tooService conexões barramento antes, você será solicitado tooprovide suas credenciais do barramento de serviço. Essas credenciais são usada tooauthorize seu tooand de tooconnect lógica aplicativo acessar dados do sua conta barramento de serviço. conector do barramento de serviço Olá precisa de cadeia de caracteres de conexão Olá Olá namespace de barramento de serviço. Ele também precisa **Gerenciar** permissões. Tooknow uma boa maneira se sua cadeia de caracteres de conexão é para o namespace de saudação ou uma entidade específica é se ele contém Olá `EntityPath` parâmetro. Em caso afirmativo, não é cadeia de caracteres de conexão à direita de saudação para um aplicativo lógico.  
    ![Cadeia de conexão do Barramento de Serviço](./media/connectors-create-api-servicebus/connectionstring.png)
3. Depois que você recebeu a cadeia de caracteres de conexão de Olá Olá namespace, pode usá-lo para Olá conexão API em aplicativos lógicos.  
    ![Imagem de conexão do Barramento de Serviço 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Observe a conexão Olá foi criado e você está livre tooproceed com hello outra etapas em seu aplicativo de lógica.  
    ![Imagem de conexão do Barramento de Serviço 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

