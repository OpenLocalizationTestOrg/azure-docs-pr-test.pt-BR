## <a name="webapi-project"></a>Projeto WebAPI
1. No Visual Studio, abra Olá **AppBackend** projeto que você criou no hello **notificar usuários** tutorial.
2. Em Notifications.cs, substitua Olá todo **notificações** classe com hello código a seguir. Ser se tooreplace Olá reservados sua cadeia de conexão (com acesso completo) para o hub de notificação e o nome do hub hello. Você pode obter esses valores de saudação [Portal clássico do Azure](http://manage.windowsazure.com). Este módulo representa agora Olá diferentes seguro notificações que serão enviadas. Em uma implementação completa, notificações de saudação serão armazenadas em um banco de dados; para simplificar, nesse caso, armazená-las na memória.
   
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

1. No NotificationsController.cs, substitua o código Olá Olá **NotificationsController** definição da classe com hello código a seguir. Esse componente implementa um modo para notificação de Olá Olá dispositivo tooretrieve com segurança e também fornece uma forma (para fins de saudação deste tutorial) tootrigger dispositivos tooyour de push segura. Observe que ao enviar o hub de notificação Olá notificação toohello, apenas enviar uma notificação bruta com a ID de saudação de notificação de saudação (e nenhuma mensagem real):
   
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


Observe que Olá `Post` método agora não envia uma notificação do sistema. Envia uma notificação bruta que contém a ID de notificação de saudação apenas e não qualquer conteúdo confidencial. Além disso, verifique se toocomment Olá operação para plataformas Olá para o qual você não tem credenciais configuradas em seu hub de notificação, conforme elas resultarão em erros de envio.

1. Agora podemos reimplantar esta tooan aplicativo site do Azure em ordem toomake-lo acessível de todos os dispositivos. Clique duas vezes em Olá **AppBackend** do projeto e selecione **publicar**.
2. Selecione o Site do Azure como seu destino de publicação. Faça logon com sua conta do Azure e selecione um site novo ou existente e anote Olá **URL de destino** propriedade Olá **Conexão** guia. Chamaremos toothis URL como o *ponto de extremidade de back-end* posteriormente neste tutorial. Clique em **Publicar**.

