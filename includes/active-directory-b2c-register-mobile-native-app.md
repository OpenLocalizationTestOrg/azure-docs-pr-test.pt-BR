[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister seu aplicativo móvel ou nativo, use configurações de saudação especificados na tabela de saudação.

![Exemplo de configurações de registro para o novo aplicativo móvel ou nativo](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Configuração      | Valor de exemplo  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | Aplicativo B2C da Contoso | Insira um **nome** para aplicativo hello que descreve tooconsumers seu aplicativo. |
| **Cliente nativo** | Sim | Selecione **Sim** para um aplicativo móvel ou nativo. |
| **URI de Redirecionamento Personalizado** | `com.onmicrosoft.contoso.appname://redirect/path` | Insira um URI de redirecionamento com um esquema personalizado. Escolha um [bom URI de redirecionamento](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) e não inclua caracteres especiais, como sublinhados. |

Clique em **criar** tooregister seu aplicativo.

Seu aplicativo registrado recentemente é exibido na lista de aplicativos Olá para o locatário do hello B2C. Selecione seu aplicativo móvel ou nativo Olá lista. Painel de propriedades do aplicativo Hello é exibido.

![Propriedades do aplicativo](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Anote Olá globalmente exclusivo **ID do aplicativo cliente**. Use o ID de saudação no código do aplicativo.

Se o aplicativo nativo chamar uma API da Web protegida pelo Azure AD B2C, execute estas etapas:
   1. Criar um segredo do aplicativo, vai toohello **chaves** folha e clicando em Olá **gerar chave** botão. Anote Olá **chave do aplicativo** valor. Valor de saudação é usado como o segredo do aplicativo hello no código do aplicativo.
   2. Clique em **Acesso à API**, clique em **Adicionar** e selecione sua API da Web e escopos (permissões).

> [!NOTE]
> Um **Segredo de Aplicativo** é uma credencial de segurança importante e deve ser protegido adequadamente.
> 
