Todos os blobs no armazenamento do Azure devem residir em um contêiner. Olá contêiner faz parte do nome do blob hello. Por exemplo, `mycontainer` é Olá nome do contêiner de saudação nesses URIs do blob de exemplo:

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Um nome de contêiner deve ser um nome DNS válido, toohello conformidade com as regras de nomenclatura a seguir:

1. Os nomes de contêiner devem começar com uma letra ou número e podem conter apenas letras, números e caracteres de traço (-) hello.
2. Cada caractere traço (-) deve ser imediatamente precedido e seguido por uma letra ou número. Não são permitidos traços consecutivos em nomes de contêiner.
3. Todas as letras do nome de um contêiner devem ser minúsculas.
4. Os nomes de contêiner devem ter de 3 a 63 caracteres.

> [!IMPORTANT]
> Observe que Olá nome de um contêiner deve sempre estar em minúscula. Se você incluir uma letra maiuscula em um nome de contêiner ou viola as regras de nomenclatura de contêiner de Olá, você poderá receber um erro 400 (solicitação incorreta). 
> 
> 

