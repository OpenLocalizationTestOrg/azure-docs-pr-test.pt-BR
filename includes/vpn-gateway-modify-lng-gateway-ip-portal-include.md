### <a name="gwipnoconnection"></a>endereço IP do gateway da rede local de saudação toomodify - nenhuma conexão de gateway

Use toomodify de exemplo hello um gateway de rede local que não tem uma conexão de gateway. Ao modificar esse valor, você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente.

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **configuração**.
2. Em Olá **endereço IP** caixa, modifique o endereço IP hello.
3. Clique em **salvar** toosave configurações de saudação.

### <a name="gwipwithconnection"></a>toomodify Olá local de rede gateway endereço IP do gateway - existente de conexão de gateway

toomodify um gateway de rede local que tem uma conexão, você precisa de conexão de saudação do toofirst remover. Após a conexão de saudação for removido, você pode modificar o endereço IP do gateway de saudação e recriar uma nova conexão. Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente. Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar o endereço IP do gateway hello, gateway VPN Olá toodelete não é necessário. Você só precisa de conexão de saudação tooremove.
 
#### <a name="1-remove-hello-connection"></a>1. Remova conexão hello.

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **conexões**.
2. Clique em Olá **...**  na linha de saudação para conexão hello, em seguida, clique em **excluir**.
3. Clique em **salvar** toosave suas configurações.

#### <a name="2-modify-hello-ip-address"></a>2. Modifique o endereço IP hello.

Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente.

1. Em Olá **endereço IP** caixa, modifique o endereço IP hello.
2. Clique em **salvar** toosave configurações de saudação.

#### <a name="3-recreate-hello-connection"></a>3. Recrie a conexão de saudação.

1. Navegue toohello Gateway de rede Virtual para sua rede virtual. (Não hello Gateway de rede Local.)
2. Em Olá Gateway de rede Virtual, no hello **configurações** seção, clique em **conexões**.
3. Clique em Olá **+ adicionar** tooopen Olá **Adicionar conexão** folha.
4. Recrie sua conexão.
5. Clique em **Okey** toocreate conexão de saudação.
