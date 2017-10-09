tooenable entrar em seu aplicativo, você precisará de política de toocreate uma entrada. Essa política descreve experiências Olá consumidores revisará durante o logon e conteúdo de saudação de tokens que Olá aplicativo receberá em logons com êxito.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)] Clique em **Políticas de entrada**.

Clique em **+ adicionar** na parte superior de saudação da folha de saudação.

Olá **nome** determina o nome de política de entrada hello usado pelo seu aplicativo. Por exemplo, insira **SiIn**.

Clique em **Provedores de identidade** e selecione **Entrada na Conta Local**. Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado. Clique em **OK**.

Clique em **Declarações do aplicativo**. Aqui você escolhe as declarações que você deseja que sejam retornados nos tokens de saudação enviada tooyour back aplicativo após uma experiência de logon com êxito. Por exemplo, selecione **Nome de Exibição**, **Provedor de Identidade**, **CEP** e **ID de Objeto do Usuário**. Clique em **OK**.

Clique em **Criar**. Observe que a política Olá recém-criada aparece como **B2C_1_SiIn** (Olá **B2C\_1\_**  fragmento é automaticamente adicionado) em Olá **entrar políticas**folha.

Abrir a diretiva de saudação clicando **B2C_1_SiIn**.

Selecione **aplicativo Contoso B2C** em Olá **aplicativos** suspenso e `https://localhost:44321/` em Olá **URL de resposta / URI de redirecionamento** lista suspensa.

Clique em **Executar agora**. Abre uma nova guia do navegador e você pode executar através da experiência do consumidor de saudação da assinatura em seu aplicativo.

> [!NOTE]
> Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.
>