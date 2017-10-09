Nesta etapa, você cria uma porta de investigação de saudação do firewall regra tooopen ponto de extremidade de balanceamento de carga de saudação (59999, conforme especificado anteriormente) e outra regra de porta de ouvinte de grupo de disponibilidade do tooopen hello. Porque você criou o ponto de extremidade com balanceamento de carga do hello em Olá VMs que contêm réplicas do grupo de disponibilidade, você precisa de porta de investigação de saudação tooopen e porta de ouvinte Olá Olá respectivas máquinas virtuais.

1. Em VMs que hospedam réplicas, inicie o **Firewall do Windows com segurança avançada**.

2. Clique em **Regras de entrada** e, em seguida, clique em **Nova Regra**.

3. Em Olá **tipo de regra** página, selecione **porta**e, em seguida, clique em **próximo**.

4. Em Olá **protocolo e portas** página, selecione **TCP**, tipo **59999** em Olá **portas locais específicas** caixa e, em seguida, clique em **Próxima**.

5. Em Olá **ação** página, mantenha **Permitir conexão Olá** selecionado e, em seguida, clique em **próximo**.

6. Em Olá **perfil** página, aceite as configurações padrão de saudação e, em seguida, clique em **próximo**.

7. Em Olá **nome** página Olá **nome** texto, especifique um nome de regra, como **sempre na investigação de porta do ouvinte**e, em seguida, clique em **concluir**.

8. Repita Olá etapas para a porta de ouvinte de grupo de disponibilidade de saudação (conforme especificado anteriormente no parâmetro hello $EndpointPort script hello) anteriores e, em seguida, especifique um nome de regra apropriado, como **sempre na porta do ouvinte**.

