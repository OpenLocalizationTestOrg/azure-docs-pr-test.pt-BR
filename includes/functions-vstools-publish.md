1. Em **Solution Explorer**, clique com botão direito hello e selecione **publicar**. Escolha **Criar Novo** e em **Publicar**. 

    ![Publicar Criar novo aplicativo de funções](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Se você ainda não estiver conectado tooyour do Visual Studio conta do Azure, clique em **adicionar uma conta...** .  

3. Em Olá **criar serviço de aplicativo** caixa de diálogo, use Olá **hospedagem** configurações como Olá especificado na tabela a seguir: 

    ![Tempo de execução local do Azure](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Configuração      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome do aplicativo** | Nome globalmente exclusivo | Nome que identifica seu novo aplicativo de funções de forma exclusiva. |
    | **Assinatura** | Escolha sua assinatura | Olá toouse de assinatura do Azure. |
    | **[Grupo de Recursos](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nome do recurso de saudação do grupo no qual toocreate seu aplicativo de função. |
    | **[Plano do Serviço de Aplicativo](../articles/azure-functions/functions-scale.md)** | Plano de consumo | Verifique se Olá de toochoose **consumo** em **tamanho** quando você cria um novo plano.  |
    | **[Conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nome globalmente exclusivo | Use uma conta de armazenamento existente ou crie uma nova.   |

4. Clique em **criar** toocreate um aplicativo de função no Azure com essas configurações. Depois de saudação provisionamento for concluído, anote Olá **URL do Site** valor, que é o endereço de saudação do seu aplicativo de função no Azure. 

    ![Tempo de execução local do Azure](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
