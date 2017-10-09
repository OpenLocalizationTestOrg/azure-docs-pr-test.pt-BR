tooenable entrar em seu aplicativo, você precisará de política de toocreate uma entrada. Essa política descreve experiências Olá consumidores revisará durante o logon e conteúdo de saudação de tokens que Olá aplicativo receberá em logons com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na seção de políticas de saudação de configurações, selecione **políticas inscrever-se ou entrar** e clique em **+ adicionar**.

![Selecione as políticas de inscrição ou entrada e clique no botão Adicionar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Insira uma política **nome** para tooreference seu aplicativo. Por exemplo, insira: `SiUpIn`.

Selecione **Provedores de identidade** e marque **Inscrição por email**. Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado. Clique em **OK**.

![Selecione a assinatura de Email como um provedor de identidade e clique em botão Olá Okey](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Selecione **Atributos de inscrição**. Escolha os atributos desejados toocollect de consumidor Olá durante a inscrição. Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**. Clique em **OK**.

![Selecione alguns atributos e clique botão de saudação Okey](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Selecione **Declarações do aplicativo**. Escolha declarações que ser retornado em tokens de autorização de saudação enviadas tooyour back aplicativo após uma experiência de inscrição ou entrada bem-sucedida. Por exemplo, selecione **Nome de Exibição**, **Provedor de Identidade**, **CEP**, **Novo Usuário** e **ID de Objeto do Usuário**.

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Clique em **criar** tooadd política de saudação. Olá diretiva é listada como **B2C_1_SiUpIn**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a diretiva de saudação selecionando **B2C_1_SiUpIn**. Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Configuração      | Valor  |
| ------------ | ------ |
| **Aplicativos** | Aplicativo B2C da Contoso |
| **Selecionar URL de resposta** | `https://localhost:44316/` |

Abre uma nova guia do navegador e você pode verificar a experiência do consumidor de inscrever-se ou entrar hello como configurado.

> [!NOTE]
> Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.
>