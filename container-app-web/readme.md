# Criando um Container de uma Aplicação Web

Esse repositório visa documentação e apresentação de como criar um container com uma aplicação Web rodando em Docker

### O que é Docker ?

A palavra Docker, segundo consta no site da [Red Hat](https://www.redhat.com/pt-br/topics/containers/what-is-docker) possui várias definições: m projeto da comunidade open source; as ferramentas resultantes desse projeto; a empresa Docker Inc., principal apoiadora do projeto; e as ferramentas compatíveis formalmente com a empresa.
Mas podemos resumir Docker como uma tecnologia de conteinerização para criação de uso de conteiners, que são "aplicações" empacotadas e isoladas com todo o ambiente de execução delas, ou seja, com todos os arquivos necessários para executá-los. Uma analogia bastante usada seria como se você decorasse a sala de estar dos seus sonhos, com os movéis desejados, porém você tivesse que mudar de casa. Então, você monta essa sala em um container de carga e pode levá-la para onde desejar.

### Vamos para a prática

Para a criação desse container, iremos utilizar o Docker Compose, que é uma ferramenta desenvolvida para ajudar a definir e compartilhar aplicativos com vários contêineres. Com o Compose, você pode criar um arquivo YAML para definir os serviços e com um unico comando, pode rodar todos os conteineres ou para-los.
Em máquinas Linux, por padrão o Compose não é instalado junto com o Docker, sendo necessária a instalação do seu pacote. No caso de máquinas Windows ele é instalado junto ao Docker Desktop.

#### Volumes
Antes de iniciar a criação do ambiente, devemos lembrar que os dados que forem armazenados dentro do conteiner serão perdidos no momento em que o mesmo for parado. Para evitar a perda desses dados devemos criar os volumes, que são locais na sua maquina hospedeira que servirão para armazenar e transferir arquivos para o seu conteiner.
Para a nossa aplicação, eu criei uma pasta chamada htdocs no disco C: e dentro dela eu criei um arquivo em HTML simples apenas para a demonstração.

![Pasta criada para ser usada como Volume. ](/container-app-web/images/volume-host.JPG)

![Conteudo arquivo index.html](/container-app-web/images/index.JPG)

#### Arquivo YML
Iremos agora criar um arquivo chamado **compose.yml**. Esse arquivo terá a estrutura demonstrada na imagem abaixo.

![Estrutura do arquivo compose](/container-app-web/images/compose.JPG)

Iremos iniciar informando a versão do Docker Compose instalado na sua maquina. Após isso iniciaremos a configuração dos serviços que estarão rodando no seu conteiner. No nosso caso nós nomeamos o serviço como o apache e informamos a imagem Docker a ser utilizada. Acessando ao [Docker Hub](https://hub.docker.com) você poderá ter acesso as mais variadas imagens disponiveis para serem utilizadas. No nosso caso iremos utilizar a imagem httpd que é a imagem do Apache Web Server. Após os dois-pontos(:) nós designamos a tag que iremos utilizar, que no caso seria a versão que queremos utilizar. Caso não especifiquemos qual versão queremos, ele irá buscar a versão mais recente chamada de *latest*.
Próximo passo foi dar um nome ao container e designar as portas TCP que serão utilizadas. No caso eu estou informando que as requisições que chegarem na porta 80 (HTTP) da minha maquina hospedeira, serão redirecionadas para a porta 80 do meu conteiner
E por ultimo eu especifiquei o volume que foi o arquivo que eu criei anteriormente na minha pasta C:\htdocs e que deverá ser salvo dentro da pasta padrão dos arquivos html do meu conteiner (/usr/local/apache2/htdocs)


### Inicialização do Conteiner

Para inicializar o conteiner, eu irei executar o comando `docker-compose up -d`, sendo o atributo "-d" indicado pra informar que a minha aplicação irá rodar em segundo plano

![Inicialização do conteiner](/container-app-web/images/docker-compose.JPG)

Caso a imagem ainda não ter sido baixada anteriormente para a sua maquina, ela será e após isso o conteiner será iniciado

![Conteiner em execução](/container-app-web/images/localhost.JPG)

Para encerrá-lo, basta digitar o comando `docker-compose down`

![Conteiner desligando](/container-app-web/images/compose%20down.JPG)
