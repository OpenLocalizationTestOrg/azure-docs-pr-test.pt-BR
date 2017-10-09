

1. Em seu Mac, inicie **Acesso ao Conjunto de Chaves**. Na saudação esquerda a barra de navegação, em **categoria**, abra **meus certificados**. Localizar o certificado SSL Olá baixado na seção anterior hello e divulgar seu conteúdo. Selecione apenas Olá certificado (não selecione a chave privada do hello), e [exportá-lo](https://support.apple.com/kb/PH20122?locale=en_US).
2. Em Olá [portal do Azure](https://portal.azure.com/), clique em **procurar todos os** > **serviços de aplicativos**e clique em seu back-end de aplicativos móveis. Em **Configurações**, clique em **Push do Serviço de Aplicativo** e clique no nome do hub de notificação. Vá muito**Apple Push Notification Services** > **carregar certificado**. Carregar arquivo. p12 hello, selecionando Olá correto **modo** (dependendo se o SSL do cliente de certificado anteriores é seguro ou produção). Salve as alterações.

O serviço agora é configurado toowork notificações por push no iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
