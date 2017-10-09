
Por padrão, APIs em um back-end de Aplicativos Móveis podem ser chamadas de forma anônima. Em seguida, você precisa toorestrict os clientes tooonly autenticado de acesso.  

* **Node. js volta terminar (via Olá portal do Azure)** :  

    Nas configurações de seus Aplicativos Móveis, clique em **Tabelas Fáceis** e selecione a tabela. Clique em **Alterar permissões**, selecione **Apenas acesso autenticado** para todas as permissões e clique em **Salvar**.
* **Back-end do .NET (C#)**:  

    No projeto do servidor de saudação, navegue muito**controladores** > **TodoItemController.cs**. Adicionar Olá `[Authorize]` atributo toohello **TodoItemController** classe, da seguinte maneira. toorestrict somente toospecific os métodos de acesso, você também pode aplicar métodos de toothose apenas esse atributo, em vez de classe hello. Republicar o projeto do servidor de saudação.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Back-end do Node.js (por meio de código Node.js)** :  

    toorequire autenticação para acesso à tabela, adicionar Olá de script de servidor Node. js toohello linha a seguir:

        table.access = 'authenticated';

    Para obter mais detalhes, consulte [como: exigir autenticação para acesso tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn como o projeto de código de início rápido toodownload saudação do seu site, consulte [como: Download Olá Node. js back-end quickstart projeto de código usando Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
