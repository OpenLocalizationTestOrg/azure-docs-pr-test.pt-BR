tooenable refinada redefinição de senha em seu aplicativo, você precisará toocreate uma política de redefinição de senha. Observe que essa senha de todo locatário Olá redefinir a opção especificada [aqui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Essa política descreve experiências Olá consumidores Olá revisará durante a redefinição de senha e conteúdo de saudação de tokens que Olá aplicativo receberá mediante a conclusão bem-sucedida.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na seção de políticas de saudação de configurações, selecione **políticas de redefinição de senha** e clique em **+ adicionar**.

![Selecione inscrever-se ou entrar políticas e clique no botão Adicionar de saudação](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Insira uma política **nome** para tooreference seu aplicativo. Por exemplo, insira: `SSPR`.

Selecione **Provedores de identidade** e marque **Redefinir senha usando endereço de email**. Clique em **OK**.

![Selecione a redefinição de senha usando o endereço de email como um provedor de identidade e clique botão de saudação Okey](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Selecione **Declarações do aplicativo**. Escolha declarações que ser retornado em tokens de autorização de saudação enviadas tooyour back aplicativo após a redefinição de senha bem-sucedida experiência. Por exemplo, selecione **ID de Objeto do Usuário**.

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Clique em **criar** tooadd política de saudação. Olá diretiva é listada como **B2C_1_SSPR**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a diretiva de saudação selecionando **B2C_1_SSPR**. Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Configuração      | Valor  |
| ------------ | ------ |
| **Aplicativos** | Aplicativo B2C da Contoso |
| **Selecionar URL de resposta** | `https://localhost:44316/` |

Abre uma nova guia do navegador e você pode verificar a experiência do consumidor em seu aplicativo de redefinição de senha de saudação.

> [!NOTE]
> Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.
>
