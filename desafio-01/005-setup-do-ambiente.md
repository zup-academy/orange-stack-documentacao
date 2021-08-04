# Setup do Ambiente

## Objetivo

Antes de começarmos o desenvolvimento do Desafio PIX precisamos preparar e configurar nosso ambiente local de desenvolvimento, dessa forma não ficamos dependentes de um ambiente externo nas nuvens ou de uma VPN da empresa. Desse modo, precisamos rodar algumas aplicações e serviços de infraestrutura na nossa máquina.

## Descrição

Durante o ciclo de desenvolvimento do nosso projeto PIX, vamos precisar nos conectar a alguns serviços externos como por exemplo banco de dados, fila de mensagens, sistemas satélites utilizados pelo ITAÚ e serviços do Banco Central do Brasil (BCB) para efetuar transações via PIX, entre outros.

Agora você precisa fazer uma cópia do projeto no Github, temos um vídeo explicando o passo a passo de como fazer esta etapa: [Criando uma cópia do projeto (fork) para o seu usuário do github](https://github.com/zup-academy/orange-talents-06-template-pix-keymanager-grpc)

### Passo 1: baixando o `docker-compose.yml`

Primeiramente, baixe nosso arquivo `docker-compose.yml` que simulará toda a infraestrutura necessária para rodarmos o Desafio PIX:

* [`docker-compose.yml`](00-ambiente/docker-compose.yml)

Este arquivo contém todos os serviços (containers) que iremos precisar e consumir nesse desafio, como o Sistema ERP do Itáu, o Sistema PIX do BCB, um broker de mensagens Kafka, entre outros.

### Passo 2: levantando os serviços via Docker-Compose

Agora, copie o arquivo para algum pasta de sua escolha, e, em seguida, rode o seguinte comando do Docker-Compose no terminal para startar seu ambiente:

```sh
 docker-compose up -d
```

Essa operação pode levar alguns segundos, seja paciente! Ao fim, você deve perceber que todos os serviços levantaram com sucesso. Eles rodarão em background por causa do argumento `-d` no comando.

Caso algum deles tenha falhada no startup, você pode visualizar os logs destes serviços através do comando abaixo:

```sh
docker-compose logs <serviceName>
```

Lembrando que o `serviceName` é referente aos nomes dos serviços existentes dentro do arquivo `docker-compose.yml` que você acabou de fazer o download.

### Passo 3: verificando se os serviços estão rodando

Para ter certeza que todos os serviços estão de fato rodando, você pode executar o comando a seguir para verificar o status dos serviços:

```sh
docker-compose ps
```

Com esse comando, você visualiza não somente o status do serviço (`Up` significa que está rodando), como também a porta externa que cada serviço mapeou no Docker.

Outra forma de verificar quais as portas expostas mapeadas em cada serviço é verificando diretamente no arquivo `docker-compose.yml`. Além da porta, podemos verificar outras informações importantes como usuário, senha de alguns desses serviços.

### Passo 4: conhecendo e acessando os serviços satélites

Ao levantar todos os serviços, dois deles muito importantes estarão no ar:

* **Sistema ERP do ITAU**: representa o principal sistema do ITAÚ na qual, é justamente esse serviço que nos permitirá consumir os dados dos clientes, usuários e correntistas do banco, além da consulta de saldo e execução de operações financeiras. Por se tratar de um sistema muito grande e antigo, nosso container simulará apenas parte do todo, ou seja, somente o que nos interessa para o Desafio PIX;

* **Sistema Pix do Banco Central do Brasil (BCB)**: representa o serviço do Bacen (BCB) de registro e gerenciamento de chaves Pix de todos as pessoas físicas e jurídicas do Brasil, além de fornecer as algumas operações para efetuar transações financeiras através de chaves Pix;

Como desenvolvedor(a), para acessá-los, você precisa ler e estudar a documentação da API REST gerada pelo Swagger por ambos os serviços nos seguintes links:

* [Documentação da API REST do Sistema ERP do ITAÚ](http://localhost:9091/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/);
* [Documentação da API REST do Sistema Pix do Banco Central do Brasil (BCB)](http://localhost:8082/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/);

Não se preocupe com eles nesse momento, pois durante as atividades você saberá exatamente o que deve fazer. Agora, basta acessar os links acima e verificar se eles abrem corretamente no seu navegador.

## Resultado Esperado

Todos nossos serviços (containers) de infraestrutura no estado **UP**;

## Informações de suporte

* Caso você esteja se perguntando o que é um container, [esse link pode te ajudar a identificar os "porquês"](https://www.docker.com/resources/what-container);

* Ou ainda você pode estar se perguntando, por que eu iria querer usar Docker, [aqui tem algumas idéias para isso](https://www.docker.com/resources/what-container);

* Se você está procurando o caminho para instalação do Docker, [esse link pode te ajudar](https://docs.docker.com/get-docker/);

* Caso você esteja utilizando o sistema operacional Ubuntu, [esse link pode te ajudar caso você tenha tido alguns problemas para a instalação](https://docs.docker.com/engine/install/linux-postinstall/);

* Se você se interessou pelo Docker-Compose, [esse link tem uma visão rápida sobre a ferramenta](https://docs.docker.com/compose/);

* Caso você queira fazer um exemplo diferente com Docker-Compose do que temos aqui, [esse link da documentação pode te ajudar a praticar](https://docs.docker.com/compose/gettingstarted/);

* Mas caso você não tenha o Docker-Compose instalado, [esse link vai resolver seu problema](https://docs.docker.com/compose/install/);

* Se você quiser explorar mais os comandos do Docker-Compose, [esse link é a referência e pode te ajudar muito](https://docs.docker.com/compose/reference/);
