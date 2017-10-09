[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister seu aplicativo web, use configurações de saudação especificados na tabela de saudação.

![Exemplo de configurações de registro para nova aplicativo Web](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Configuração      | Valor de exemplo  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | Aplicativo B2C da Contoso | Insira um **nome** para aplicativo hello que descreve tooconsumers seu aplicativo. | 
| **Incluir aplicativo Web/API Web** | Sim | Selecione **Sim** para um aplicativo Web. |
| **Permitir fluxo implícito** | Sim | Escolha **Sim** se o seu aplicativo usar [Entrada do OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **URL de Resposta** | `https://localhost:44316` | As URLs de Resposta são pontos de extremidade para onde o Azure AD B2C retorna quaisquer tokens que seus aplicativo solicitarem. Insira uma **URL de Resposta** [apropriada](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url). Neste exemplo, seu aplicativo é local e escuta na porta 44316. |

Clique em **criar** tooregister seu aplicativo.

Seu aplicativo registrado recentemente é exibido na lista de aplicativos Olá para o locatário do hello B2C. Selecione o aplicativo web na lista de saudação. Painel de propriedades do aplicativo da web de saudação é exibido.

![Propriedades do aplicativo Web](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Anote Olá globalmente exclusivo **ID do aplicativo cliente**. Use o ID de saudação no código do aplicativo.
