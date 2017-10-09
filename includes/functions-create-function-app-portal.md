1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

1. Clique em **Computação** > **Aplicativo de Funções** e selecione sua **Assinatura**. Em seguida, use as configurações de aplicativo de função hello conforme especificado na tabela de saudação.

    ![Criar aplicativo de função em Olá portal do Azure](./media/functions-create-function-app-portal/function-app-create-flow.png)

    | Configuração      | Valor sugerido  | Descrição                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome do aplicativo** | Nome globalmente exclusivo | Nome que identifica seu novo aplicativo de funções. | 
    | **[Grupo de Recursos](../articles/azure-resource-manager/resource-group-overview.md)** |  myResourceGroup | Nome para o novo grupo de recursos hello, no qual toocreate seu aplicativo de função. | 
    | **[Plano de hospedagem](../articles/azure-functions/functions-scale.md)** |   Plano de consumo | Plano de hospedagem que define como os recursos são alocados tooyour função app. No padrão de saudação **consumo planejar**, os recursos são adicionados dinamicamente conforme exigido por suas funções. Você só paga pelo tempo de saudação que executar suas funções.   |
    | **Localidade** | Europa Ocidental | Escolha uma localização perto de você ou perto de outros serviços que suas funções acessarão. |
    | **[Conta de armazenamento](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** |  Nome globalmente exclusivo |  Nome da conta de armazenamento novo Olá usada pelo seu aplicativo de função. Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas. Você também pode usar uma conta existente. |

1. Clique em **criar** tooprovision e implantar o novo aplicativo de função hello.
