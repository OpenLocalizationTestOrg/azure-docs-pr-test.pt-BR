
1. <span data-ttu-id="1726e-101">Na exibição Solução (ou **Gerenciador de Soluções** no Visual Studio), clique com o botão direito do mouse na pasta **Componentes**, clique em **Obter Mais Componentes...**, procure pelo componente **Cliente Google Cloud Messaging** e adicione-o ao projeto.</span><span class="sxs-lookup"><span data-stu-id="1726e-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="1726e-102">Abra o arquivo de projeto ToDoActivity.cs e adicione a instrução using a seguir à classe:</span><span class="sxs-lookup"><span data-stu-id="1726e-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="1726e-103">Na classe **ToDoActivity** , adicione o seguinte código novo:</span><span class="sxs-lookup"><span data-stu-id="1726e-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="1726e-104">Isso permite que você acesse a instância do cliente móvel do processo de serviço do manipulador por push.</span><span class="sxs-lookup"><span data-stu-id="1726e-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="1726e-105">Adicione o código a seguir ao método **OnCreate**, após a criação do **MobileServiceClient**:</span><span class="sxs-lookup"><span data-stu-id="1726e-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="1726e-106">Sua **ToDoActivity** agora está preparada para adicionar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="1726e-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

