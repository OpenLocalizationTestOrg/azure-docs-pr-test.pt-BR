Aplicativos .NET podem usar Olá **Stackexchange** cliente de cache, que pode ser configurado no Visual Studio usando um pacote NuGet que simplifica a configuração de saudação do aplicativos clientes de cache. 

> [!NOTE]
> Para obter mais informações, consulte Olá [Stackexchange](http://github.com/StackExchange/StackExchange.Redis) github página e hello [documentação do cliente de cache Stackexchange](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure um aplicativo cliente no Visual Studio usando Olá pacote NuGet stackexchange. Redis, clique com botão direito Olá em **Solution Explorer** e escolha **gerenciar pacotes NuGet**. 

![Gerenciar pacotes NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Tipo **Stackexchange** ou **Stackexchange** na caixa de texto de pesquisa hello, selecione a versão desejada de saudação nos resultados de saudação e clique em **instalar**.

> [!NOTE]
> Se você preferir toouse uma versão de nome forte do hello **Stackexchange** biblioteca de cliente, escolha **Stackexchange**; caso contrário, escolha **Stackexchange**.
> 
> 

![Pacote NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Olá NuGet pacote baixa e adiciona Olá necessárias referências de assembly para tooaccess seu aplicativo de cliente Cache Redis do Azure com o cliente de cache Stackexchange hello.

> [!NOTE]
> Se você já tiver configurado seu toouse Stackexchange do projeto, você pode verificar para o pacote de toohello atualizações de saudação **NuGet Package Manager**. toocheck para e versões de instalação atualizada do hello pacote NuGet stackexchange. Redis, clique em **atualizações** em Olá Olá **NuGet Package Manager** janela. Se um toohello de atualização de pacote NuGet Stackexchange estiver disponível, você pode atualizar sua versão do projeto toouse Olá atualizado.
> 
> 

Você também pode instalar Olá pacote NuGet Stackexchange clicando **NuGet Package Manager**, **Package Manager Console** de saudação **ferramentas** menu e Olá em execução Após o comando Olá **Package Manager Console** janela.
    
```
Install-Package StackExchange.Redis
```
