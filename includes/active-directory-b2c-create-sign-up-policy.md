tooenable inscrição em seu aplicativo, você precisa de toocreate uma política de inscrição. Essa política descreve experiências Olá que os consumidores percorrer durante a inscrição e conteúdo de saudação de tokens que Olá aplicativo recebe em inscrições bem-sucedida.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Clique em **Políticas de inscrição**.

Clique em **+ adicionar** na parte superior de saudação da folha de saudação.

Olá **nome** determina Olá política inscrição nome usado pelo seu aplicativo. Por exemplo, insira **SiUp**.

Clique em **Provedores de identidade** e selecione **Inscrição de email**. Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado. Clique em **OK**.

Clique em **Atributos de inscrição**. Aqui você escolhe os atributos que você deseja toocollect do consumidor Olá durante a inscrição. Por exemplo, selecione **País/Região**, **Nome de Exibição** e **CEP**. Clique em **OK**.

Clique em **Declarações do aplicativo**. Aqui você escolhe as declarações que você deseja que sejam retornados nos tokens de saudação enviada tooyour back aplicativo depois de um processo de inscrição com êxito. Por exemplo, selecione **Nome de exibição**, **Provedor de identidade**, **CEP**, **Novo usuário** e **ID de objeto do usuário**.

Clique em **Criar**. diretiva Olá criada aparece como **B2C_1_SiUp** (Olá **B2C\_1\_**  fragmento é automaticamente adicionado) em hello **inscrição políticas** folha.

Abrir a diretiva de saudação clicando **B2C_1_SiUp**.

Selecione **aplicativo Contoso B2C** em Olá **aplicativos** suspenso e `https://localhost:44321/` em Olá **URL de resposta / URI de redirecionamento** lista suspensa.

Clique em **Executar agora**. Abre uma nova guia do navegador e você pode executar através da experiência do consumidor de saudação de inscrição em seu aplicativo.

> [!NOTE]
> Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.
>