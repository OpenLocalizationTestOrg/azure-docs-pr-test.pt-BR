
1. <span data-ttu-id="9bf75-101">Navegue toohello [Google nuvem Console](https://console.developers.google.com/project), entre com suas credenciais de conta do Google.</span><span class="sxs-lookup"><span data-stu-id="9bf75-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="9bf75-102">Clique em **Criar Projeto**, digite um nome de projeto, então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="9bf75-103">Se solicitado, realizar Olá verificação de SMS e clique em **criar** novamente.</span><span class="sxs-lookup"><span data-stu-id="9bf75-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Criar um novo projeto](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="9bf75-105">Digite o novo **Nome do projeto** e clique em **Criar projeto**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="9bf75-106">Clique em Olá **utilitários e muito mais** botão e, em seguida, clique em **informações sobre o projeto**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="9bf75-107">Anote Olá **projeto número**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="9bf75-108">Você precisará tooset esse valor como Olá `SenderId` variável no aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="9bf75-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Utilitários e mais](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="9bf75-110">Em Olá projeto dashboard, em **Mobile APIs**, clique em **Google Cloud Messaging**, em seguida, na próxima página do hello, clique em **Habilitar API** e aceite os termos de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="9bf75-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Habilitar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Habilitar o GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="9bf75-113">No painel de projeto hello, clique em **credenciais** > **Create Credential** > **chave API**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="9bf75-114">Em **Criar uma nova chave**, clique em **Chave do servidor**, digite um nome para a chave, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9bf75-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="9bf75-115">Anote Olá **chave API** valor.</span><span class="sxs-lookup"><span data-stu-id="9bf75-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="9bf75-116">Você irá usar esse valor de chave de API tooenable tooauthenticate do Azure com GCM e enviar notificações por push em nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9bf75-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

