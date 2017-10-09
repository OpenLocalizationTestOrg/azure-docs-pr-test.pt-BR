perfil de tooenable edição em seu aplicativo, você precisará toocreate um política de edição de perfil. Essa política descreve as experiências de saudação consumidores revisará durante o conteúdo de edição e saudação do perfil de tokens que o aplicativo hello receberá mediante a conclusão bem-sucedida.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Na seção de políticas de saudação de configurações, selecione **políticas de edição de perfil** e clique em **+ adicionar**.

![Selecione a edição de políticas de perfil e clique no botão Adicionar de saudação](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Insira uma política **nome** para tooreference seu aplicativo. Por exemplo, insira: `SiPe`.

Clique em **Provedores de identidade** e marque **Entrada na Conta Local**. Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado. Clique em **OK**.

![Selecione o Local de conta como um provedor de identidade e clique em botão Olá Okey](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Selecione **Atributos do perfil**. Escolha o consumidor de saudação de atributos pode exibir e editar seu perfil. Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**. Clique em **OK**.

![Selecione alguns atributos e clique botão de saudação Okey](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Selecione **Declarações do aplicativo**. Escolha a ser retornado em tokens de autorização de saudação de declarações enviadas tooyour back aplicativo após um experiência de edição de perfil bem-sucedida. Por exemplo, selecione **Nome de Exibição** e **CEP**.

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Clique em **criar** tooadd política de saudação. Olá diretiva é listada como **B2C_1_SiPe**. Olá **B2C_1_** prefixo é o nome de toohello anexado.

Abrir a diretiva de saudação selecionando **B2C_1_SiPe**. Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.

![Selecione a política e execute-a](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Configuração      | Valor  |
| ------------ | ------ |
| **Aplicativos** | Aplicativo B2C da Contoso |
| **Selecionar URL de resposta** | `https://localhost:44316/` |

Abre uma nova guia do navegador e você pode verificar o perfil de saudação editando experiência do consumidor, conforme configurado.

> [!NOTE]
> Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.
>