
1. <span data-ttu-id="46a9a-101">Em Olá solução exibir (ou **Solution Explorer** no Visual Studio), Olá do botão direito do mouse **componentes** pasta, clique em **obter mais componentes...** , pesquise Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="46a9a-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="46a9a-102">Abrir o arquivo de projeto ToDoActivity.cs hello e adicione o seguinte hello usando instrução toohello classe:</span><span class="sxs-lookup"><span data-stu-id="46a9a-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="46a9a-103">Em Olá **ToDoActivity** de classe, adicione Olá novo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="46a9a-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
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
   
    <span data-ttu-id="46a9a-104">Isso permite que você tooaccess instância de cliente móvel de saudação do processo de serviço do manipulador de envio por push hello.</span><span class="sxs-lookup"><span data-stu-id="46a9a-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="46a9a-105">Adicionar Olá toohello de código a seguir **OnCreate** método após Olá **MobileServiceClient** é criada:</span><span class="sxs-lookup"><span data-stu-id="46a9a-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="46a9a-106">Sua **ToDoActivity** agora está preparada para adicionar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="46a9a-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

