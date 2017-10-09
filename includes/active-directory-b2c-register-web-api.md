[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister sua API da web, use configurações de saudação especificadas na tabela de saudação.

![Exemplo de configurações de registro para nova API Web](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Configuração      | Valor de exemplo  | Descrição                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nome** | API B2C da Contoso | Insira um **nome** para aplicativo hello que descreve o tooconsumers API. | 
| **Incluir aplicativo Web/API Web** | Sim | Selecione **Sim** para uma API Web. |
| **Permitir fluxo implícito** | Sim | Escolha **Sim** se o seu aplicativo usar [Entrada do OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **URL de Resposta** | `https://localhost:44316/` | As URLs de Resposta são pontos de extremidade para onde o Azure AD B2C retorna quaisquer tokens que seus aplicativo solicitarem. Insira uma **URL de Resposta** [apropriada](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url). Neste exemplo, a sua API Web é local e escuta na porta 44316. |
| **URI da ID do Aplicativo** | api | Olá URI da ID do aplicativo é o identificador de saudação usada para sua API da web. Olá identificador completo, incluindo o domínio de saudação do URI é gerado para você. |

Clique em **criar** tooregister seu aplicativo.

Seu aplicativo registrado recentemente é exibido na lista de aplicativos Olá para o locatário do hello B2C. Selecione sua API da web na lista de saudação. Saudação da API do painel de propriedade é exibida.

![Propriedades da API Web](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Anote Olá globalmente exclusivo **ID do aplicativo cliente**. Use o ID de saudação no código do aplicativo.
