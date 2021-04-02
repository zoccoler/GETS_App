# GETS_App: Aplicação Web para Análise Temporal de Dados do GETS

## Índice

[Descrição Geral](#geral)

[Instalação](#instacao)

[Utilização](#utilizacao)

[Financiamento](#financiamento)

[Licença](#licenca)

## Descrição Geral

Aplicação web para visualização inteligente de dados de equipamentos hospitalares e serviços relacionados do sistema de Gestão de Tecnologia para a Saúde (GETS), desenvolvido pelo Laboratório Nacional para Gerenciamento de Tecnologia em Saúde (LNGTS).

Utiliza as tabelas geradas pelo GETS para produção de gráficos interativos e gera modelos de séries temporais otimizados para construção de linhas de tendência em relação à manutenção de equipamentos médico-hospitalares.

Neste repositório, nós fornecemos os códigos-fonte para rodar a aplicação localmente pela plataforma como serviço Docker (Docker, Inc.).

## Instalação

1.	Baixar o Docker:
    - Faça o download e instale o [Docker para Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows);
    - É possível que, durante a instalação, seja requisitada a instalação/atualização do WSL2. Para isso, realize o passo 4 deste [link](https://docs.microsoft.com/pt-br/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package) e pressione o botão Restart da instalação;
  ![Figura_inst_WSL](/figuras/Figura_WSL.png)
2.	Abrir o Docker:
    - Abra o Docker (pode ser necessário reiniciar o sistema antes disso) e abra também qualquer prompt de comando (como por exemplo: clique em Iniciar -> digite “cmd” na barra de busca do Windows e pressione Enter; ou use o Powershell);
3. Baixar a imagem do GETS_App:	
    - No prompt de comando (com Docker aberto em segundo plano), digite o seguinte comando e aperte Enter para fazer o download da imagem do GETS_App:
  
    `docker pull zoccoler/gets_app`
  
4. Rodar a imagem do GETS_App com espelhamento para uma pasta local:
    -	Digite a seguinte linha de código para rodar a imagem do GETS_App, mas substitua a parte em azul pelo endereço absoluto de uma pasta local vazia, a qual será utilizada para armazenar os dados das tabelas.
    - **Importante**: digite todos os comandos em uma única linha, não aperte Enter antes que tudo tenha sido digitado, e preste atenção que alguns comandos estão separados por espaços enquanto outros não estão!
  
    ```docker run -d -it --name gets_app --mount type=bind,source=C:/Users/Username/data,target=/gets_app/data -p 44444:8866 zoccoler/gets_app```
  
5. Rodar o GETS_App localmente:
    - Abra qualquer navegador de internet e conecte no endereço http://localhost:44444;

Você deve visualizar a interface do GETS_App.
![Figura_interface](/figuras/figura_interface.png)
Feito! A aplicação estará disponível enquanto o Docker estiver rodando a imagem do GETS_App em segundo plano. Você pode parar ou reiniciar a aplicação por meio do Docker Desktop.
![Figura_docker](/figuras/Figura_docker.png)
Observações: A pasta local que você escolheu no passo 4 está espelhada dentro do container Docker como sendo a pasta “gets_app/data”. 
Você deve carregar as tabelas do GETS na sua pasta local antes de usar o GETS_App. Além disso, os aquivos de saída que você salvar serão armazenados numa pasta "Outputs" dentro da pasta “gets_app/data” e poderão ser recuperados pela sua pasta local.

## Utilização

1. Carregue/copie as tabelas do GETS (imagens de como obtê-las são mostradas no final desta página) na pasta local escolhida no passo 4 da instalação;
2. Clique no botão "Carregar Tabelas". Se alguma tabela estiver faltando, você será informado com uma mensagem abaixo do botão.
3. Selecione um ou mais equipamentos pelo campo "Equipamento";
4. Selecione uma data inicial de análise pelo campo "Data Inicial";
5. Selecione uma data final de análise pelo campo "Dara Final";
6. Pronto! O gráfico deve ser apresentado no centro da tela.

A aplicação contém 3 abas: Quantidade, Custo e Duração.

### Quantidade

Mostra a quantidade total do(s) equipamento(s) ativo(s) (curva azul) e disponíveis (curva laranja). A diferença entre as duas curvas corresponde à quantidade de equipamentos em manutenção corretiva.
A opção mostrar linhad e tendência abre novos campos para construção de uma linha de tendência a partir de uma data selecionada e pela duração escolhida (em semanas).
GETS_App automaticamente busca o melhor modelo de séries temporais (ARIMA, ARIMA com sazonalidade trimestral e Suavização Exponencial) usando como dados de treinamento todos os valores anteriores à data da previsão.

### Custo

Mostra os custos totais mensias (em R$) do(s) equipamento(s) selecionado(s), divididos em custos com materiais (barras verde-escuras) e custos com serviços externos (barras verde-claras).
As barras são interativas, clicar nelas gera um mini-gráfico à esquerda com os custos do mês selecionado ao longo de outros anos.
Os valores já são mostrados corrigidos pela inflação caso a tabela de IPCA tenha sido carregada. Do contrário, são mostrados valores não-corrigidos.

### Duração

Mostra as medianas das durações (em horas) das ordens de serviço (OS) do(s) equipamento(s) selecionado(s) (barras roxas).

## Financiamento

Este projeto foi financiado pelo [CNPq](http://www.cnpq.br/).

## Licença de Software


