
1. Em Olá solução exibir (ou **Solution Explorer** no Visual Studio), Olá do botão direito do mouse **componentes** pasta, clique em **obter mais componentes...** , pesquise Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto.
2. Abrir o arquivo de projeto ToDoActivity.cs hello e adicione o seguinte hello usando instrução toohello classe:
   
        using Gcm.Client;
3. Em Olá **ToDoActivity** de classe, adicione Olá novo código a seguir: 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    Isso permite que você tooaccess instância de cliente móvel de saudação do processo de serviço do manipulador de envio por push hello.
4. Adicionar Olá toohello de código a seguir **OnCreate** método após Olá **MobileServiceClient** é criada:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Sua **ToDoActivity** agora está preparada para adicionar notificações por push.

