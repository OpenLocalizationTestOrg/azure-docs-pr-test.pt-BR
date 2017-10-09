## <a name="webapi-project"></a><span data-ttu-id="e359f-101">Projeto WebAPI</span><span class="sxs-lookup"><span data-stu-id="e359f-101">WebAPI Project</span></span>
1. <span data-ttu-id="e359f-102">No Visual Studio, abra Olá **AppBackend** projeto que você criou no hello **notificar usuários** tutorial.</span><span class="sxs-lookup"><span data-stu-id="e359f-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="e359f-103">Em Notifications.cs, substitua Olá todo **notificações** classe com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e359f-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="e359f-104">Ser se tooreplace Olá reservados sua cadeia de conexão (com acesso completo) para o hub de notificação e o nome do hub hello.</span><span class="sxs-lookup"><span data-stu-id="e359f-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="e359f-105">Você pode obter esses valores de saudação [Portal clássico do Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e359f-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="e359f-106">Este módulo representa agora Olá diferentes seguro notificações que serão enviadas.</span><span class="sxs-lookup"><span data-stu-id="e359f-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="e359f-107">Em uma implementação completa, notificações de saudação serão armazenadas em um banco de dados; para simplificar, nesse caso, armazená-las na memória.</span><span class="sxs-lookup"><span data-stu-id="e359f-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="e359f-108">No NotificationsController.cs, substitua o código Olá Olá **NotificationsController** definição da classe com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e359f-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="e359f-109">Esse componente implementa um modo para notificação de Olá Olá dispositivo tooretrieve com segurança e também fornece uma forma (para fins de saudação deste tutorial) tootrigger dispositivos tooyour de push segura.</span><span class="sxs-lookup"><span data-stu-id="e359f-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="e359f-110">Observe que ao enviar o hub de notificação Olá notificação toohello, apenas enviar uma notificação bruta com a ID de saudação de notificação de saudação (e nenhuma mensagem real):</span><span class="sxs-lookup"><span data-stu-id="e359f-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="e359f-111">Observe que Olá `Post` método agora não envia uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="e359f-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="e359f-112">Envia uma notificação bruta que contém a ID de notificação de saudação apenas e não qualquer conteúdo confidencial.</span><span class="sxs-lookup"><span data-stu-id="e359f-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="e359f-113">Além disso, verifique se toocomment Olá operação para plataformas Olá para o qual você não tem credenciais configuradas em seu hub de notificação, conforme elas resultarão em erros de envio.</span><span class="sxs-lookup"><span data-stu-id="e359f-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="e359f-114">Agora podemos reimplantar esta tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e359f-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="e359f-115">Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e359f-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="e359f-116">Selecione o Site do Azure como seu destino de publicação.</span><span class="sxs-lookup"><span data-stu-id="e359f-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="e359f-117">Faça logon com sua conta do Azure e selecione um site novo ou existente e anote Olá **URL de destino** propriedade Olá **Conexão** guia. Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e359f-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="e359f-118">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e359f-118">Click **Publish**.</span></span>

