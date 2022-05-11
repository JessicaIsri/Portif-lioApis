# Jéssica Isri Dias Cruz

Me chamo Jéssica Isri Dias Cruz, estudante, cursando o 6º semestre de Banco de Dados na Fatec São José dos Campos e formada em Técnico de Informatica, pela ETEC Machado de Assis em 2019.

Iniciei na area do TI desde 2017 quando realizei um estágio junto ao técnico de informatica. Em 2018 fui efetivada no cargo de desenvolvedor fullstack, porém atuava em atividades mais relacionadas ao backend e processamento de dados financeiros provindos de diversas fontes e construção de bots com a função de WebScraping.

Em 2020 recebi a oportunidade de atuar como desenvolvedor fullstack na area de GIS, assim ganhando conhecimento nas aplicações baseadas em Google Maps. Posteriormente no fim do ano de 2020 e decorrer de 2021, iniciei atividades relacionadas a computação em nuvem, tendo como  principal base o uso do Google Maps Plataform.

Atualmente estou buscando conhecimento na area de big data e machine learning, no momento para além da finalizaçao da faculdade de banco de dados, estou orientando meus estudos para a realização da prova de certificaçao do Google Data Engineer

<p align="center">
  <a href="https://www.linkedin.com/in/jessica-dias1/">
    <img width="100px" src="https://img.shields.io/badge/-LinkedIn-blue?style=flat&logo=Linkedin&logoColor=white">
  </a>
  <a href="https://github.com/JessicaIsri">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
  <a href="https://github.com/JessicaIsri">
    <img width="100px" src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white">
  </a>
</p>


# Meus Projetos
1. [WEBBOT](https://github.com/JessicaIsri/PortifolioApis/blob/main/readMe.md#webbot)
2. [GANTT PLANNER](https://github.com/JessicaIsri/PortifolioApis/blob/main/readMe.md#gantt-planner)
3. [Valcode](https://github.com/JessicaIsri/PortifolioApis/blob/main/readMe.md#valcode)
4. [Nemo](https://github.com/JessicaIsri/PortifolioApis/blob/main/readMe.md#nemo)
5. [Nemosys](https://github.com/JessicaIsri/PortifolioApis/blob/main/readMe.md#nemosys)
## Webbot

Ano: 2019.2

Parceiro: FATEC

<p align="left">
  <a href="https://github.com/JessicaIsri/WebBot">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
</p>

O sistema em questão tinha como objetivo o desenvolvimento de um webbot que fosse capaz de solucionar um problema da atualidade. O problema a ser resolvido era de livre escolha dos participantes.
Tendo isso em mente a aplicação tem o objetivo de auxiliar na pesquisa de mercado para pequenas empresas da cidade de São José dos Campos, através da coleta de dados no portal da Receita Federal e com os dados de CEP localizar a latitude e longitude aproximada para além de de dados adicionais do endereço, dessa forma sendo possivel a analise da concorrencia de um determinado estabelecimento em um determinado ramo em um local especifico da cidade de São José dos Campos.

### Técnologias utilizadas na solução
As seguintes tecnologias foram adotadas na solução desenvolvida:
- Python: O python é uma linguagem de programação interpretada, muito utilizada para analises de dados. Possui como sua principal vantagem e facilidade de aprendizado, sintaxe amigavél além de ser poderosa para diversos usos.
- Django: Django é um framework para desenvolvimento rápido para web, escrito em Python, que utiliza o padrão model-template-view.
- Selenium: Selenium é um framework portátil para testar aplicativos web, porém pode ser adptado para o desenvolvimento de bots que necessitem de interação direta com uma interface.
- MongoDB: O MongoDB é um sistema de banco de dados NoSql orientado a documentos, com o uso similar ao JSON.

### Contribuições individuais/pessoais
Contribui com o desenvolvimento do bot que recuperava os arquivos fornecedos pela Receita Federal, rotinas de leitura dos arquivos dos quais cada um continha aproximadamente 5GB de dados. Para além do metodo de recuperação dos dados espaciais através do dado do CEP.

#### Motor de extração de dados Geograficos
- Class Driver
```
def __init__(self, cep):
        self.driver = webdriver.Chrome(executable_path='C:\\webbot\\chromedriver')
        self.wait = WebDriverWait(self.driver, 5)
        self.cep = cep
        self.openSite()
```
Como podemos observar pelo construtor da classe, temos algumas configurações padrões a serem feitas para o correto funcionamento do bot que irá extrair os arquivos, tais como
- Driver a ser utilizado pelo Selenium:  O driver é um executavél que permite a manipulação de ações automáticas em cima da janela do navegador, sendo assim é necessario indicar o caminho do executavel na inicialização do Webdriver. Esse arquivo varia de navegador para navegador, por exemplo no chrome e chromium utilizamos o chromedrive, enquanto que no Mozila Firefox temos o GeckoDrive
- Wait: semelhante a função sleep ele adiciona um modo de espera ao driver, algumas ações não tem reações imediatas, por exemplo ao clickar sobre um botão de refresh, temos de aguardar até que a ação seja concluida, desse modo precisamos aguardar esse evento se concluir. Com base nisso temos de definir um tempo máximo para que essa ação seja concluida.
- Class Driver, método openSite
```
 def openSite(self):
        self.driver.get("https://www.mapacep.com.br/index.php")
        self.wait.until(EC.presence_of_element_located((By.ID, 'keywords')))
        self.driver.find_element_by_id('keywords').send_keys(self.cep)
        self.driver.find_element_by_xpath('/html/body/header/div[1]/div/div[2]/div/form/span/button').click()
        sleep(10)
        try:
            text = self.driver.find_element_by_xpath('/html/body/main/div[3]/div/div[1]/p').text.split('\n')
            endereco = text[0]
            latitude = text[3]
            longitude = text[4]
            print(endereco, latitude, longitude)
        except:
            cnpj = self.driver.find_element_by_xpath('/html/body/main/div[7]/div/div[1]/p[1]').text
            print(cnpj)
```
O código acima traz uma exemplificação da extração dos dados presentes no site https://www.mapacep.com.br/index.php, após ser realizado o filtro por cep.
#### Processo de Leitura
```
b = 102400
kb = b*100
def read_in_chunks(file_object, chunk_size=kb):
    while True:
        data = file_object.read(chunk_size)
        if not data:
            break
        yield data


f = open('E:\\FATEC\\PI\\Files\\K3241.K03200DV.D90805.L00001')
count = 1
for piece in read_in_chunks(f):
    print(piece)
    new = open('E:\\FATEC\\PI\\Files\\frags\\frag'+str(count)+'.txt', 'w')
    new.writelines(piece)
    new.close()
    count += 1
```

**O uso do yield:** O yield cria um generator, uma lista de dados que serão consumidos sob demanda, sendo assim pode ser utilizado para uma melhor abstração do codigo. Nesse caso em especifico era necessário ele foi utilizado para fragmentar arquivos txt com mais de 5Gb, que seriam grandes demais para ler de uma unica vez. Logo o codigo retora os dados presentes para cara "pedaço" de 10mb, um novo arquivo é gerado.

### Hard Skills Desenvolvidas:
Python, Selenium

### Soft Skills Efetivamente Desenvolvidas:
Como softskills desenvolvidas, temos o aprendizado inicial do uso do scrum, mesmo que ainda longe de uma aplicaçao ideal, ainda sim tivemos a ideia de como se portavam cada papel e suas principais funções. Para além não posso deixar de destacar as habilidades interpessoais adiquiridas, pois para o total desenvolvimento do projeto foi necessário aprender a trabalhar e se relacionar em equipe. Pois desde a capacidade de reconhecer quando esta com dificuldade em algo, quanto a humildade de ajudar o colega.

### Aprendizados Efetivos
Com base nas rotinas desenvolvidas, pode se  absorver o uso do generator para criar estados de codigo que serão aproveitados ao longo da execução, posteriormente foi cogitado o uso do pandas para tal, uma vez que ele lida com a manipulação de dataframes, logo, além de apresentar melhor desempenho ainda entrega uma serie de funções uteis e facilidades para o uso dos dados principalmente quando está aliado ao numpy.
Para o caso do webbot, foi essencial o uso do wait para a espera dos eventos do navegador, e dessa maneira evitar erros relacionados a falta de algum elemento na pagina.
Contudo, pode se afirmar que o real aprendizado se deu em relação ao inicio da manipulação dos dados contanto quase que exclsivamente das bibliotecas nativas da propria linguagem do python.

## GANTT PLANNER

Ano: 2020.1

Parceiro: NECTO
<p align="left">
  <a href="https://github.com/JessicaIsri/GANTT-PLANNER">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
</p>

O Gantt Planner surgiu da necessidade da empresa Necto, da qual precisava de uma ferramenta que fosse facil de se utilizar, portatil e flexivél e que tivesse a capacidade de auxiliar no planejamento dos projetos presentes na empresa, visto que em uma breve comparação com ferramentas semelhantes as mesmas sempre possuiam algum fator dificultante, seja a visualização ou então a limitação do uso por todos os setores.
Logo o Gantt Planner nasceu com a proposa de ser uma ferramenta visual de planejamento, apesentando de forma grafica os projetos e recursos disponiveis no momento.

### Técnologias utilizadas na solução
- Python: O python é uma linguagem de programação interpretada, muito utilizada para analises de dados. Possui como sua principal vantagem e facilidade de aprendizado, sintaxe amigavél além de ser poderosa para diversos usos.
- Django: Django é um framework para desenvolvimento rápido para web, escrito em Python, que utiliza o padrão model-template-view.
- PostgreSql: PostgreSQL é um sistema gerenciador de banco de dados objeto relacional, desenvolvido como projeto de código aberto.
- JavaScript: JavaScript é uma linguagem de programação interpretada estruturada, de script em alto nível com tipagem dinâmica fraca e multiparadigma. 
- CSS: Cascading Style Sheets é um mecanismo para adicionar estilo a um documento web.

### Contribuições individuais/pessoais
Tive como pricipal contribuição a modelagem e administração das entidades presentes no banco de dados, onde as mesmas deveriam ser capaz  de atender a necessidade de exibição do front.
![image](https://user-images.githubusercontent.com/65822756/134255358-d701c31c-7da8-417b-b0ca-69a3ce30bfbd.png)
 O banco é composto pelas seguintes entidades:
 - tb_pessoa: Entidade responsavél por armazenar os dados de cada pessoa envolvida com a empresa.
 - tb_habilidade: Entidade responsavél por armazenas as habilidade de cada pessoa, onde seu relacionamento torna obridatória a existencia de uma pessoa e uma pessoa pode ter N habilidades, inclusive nenhuma habilidade
 - tb_tarefa: Entidade onde é armazenada as tarefas que compoem o projeto que esta sendo executado, essa entidade possúi um relacionamento com a entidade pessoa, onde uma tarefa não possúi a obrigatoriedade de possuir uma pessoa relacionada, podendo uma unica tarefa ter varias pessoas atreladas a ela, e uma pessoa pode estar atrelada a varias tarefas. Para além disso essa entidade possui um auto-relacionamento, pois uma tarefa pode depender da execução de uma tarefa anterior a ela, porém uma tarefa pode possuir no maximo uma tarefa anterior e/ou posterior.
 - tb_projeto: Entidade responsavél por armazenar os projetos que estão/serão desenvolvidos pela empresa, ela possui um relacionamento com a entidade tb_tarefa, onde um projeto pode ter N tarefas, inclusive nenhuma. 

Junto a isso temos as aplicações das 3 Formas Normais, sendo elas:

1ª Forma normal: todos os atributos de uma tabela devem ser atômicos, ou seja, a tabela não deve conter grupos repetidos e nem atributos com mais de um valor, ou seja não podemos ter campos multivalorados, podemos ver essa forma aplicada no uso de uma tabela especifica para habilidades e tarefas, uma vez que uma pessoa pode ter mais de uma tarefa e mais de uma habilidade.

2ª Forma normal: Primeiramente é preciso já estar de acordo com a 1ªFN para estar de acordo com a 2ªFN. Além disso todos os atributos não chave devem depender apenas da chave primária. Por exemplo, ainda na relação entre a pessoa e habilidade, caso na entidade pessoa houvesse a descrição de uma habilidade, essa por sua vez estaria fora da 2ªFN uma vez que essa informação depende do ID da habilidade e não do ID da pessoa.

3ª Forma normal: Como acontece anteriormente, é necesário já estar de acordo com a 2ªFN. A 3ªFN diz que os atributos não pertencente a chave primária devem ser mutuamente independentes e dependentes apenas da cahve identificadora, por exemplo no caso da relação entre projeto e tarefa, caso na tarefa tívessimos a informação do projeto junto de seu id, essa informação deveria ser removida apenas restando os dados referentes a tarefa e o id do projeto

### Hard Skills Desenvolvidas:
Python, Mysql, JavaScript

### Soft Skills Efetivamente Desenvolvidas:
O enfoque desse projeto esteve voltado principalmente a atuação em time, tanto o respeito com os parceiros, quato ao entendimento do real trabalho em time. Um ponto de destaque principal é o impacto da divisão de tarefas, saber assumir tarefas conforme sua real capacidade de desenvolvimento. Junto a isso a priorização e levantamento de requisitos, representam a base de qualquer projeto, pois com essas informações é possivél basear não só o banco de dados mas toda a aplicação.

### Aprendizados Efetivos
Como aprendizado efetivo, posso destacar o correto uso das formas normais para a modelagem correta do banco de dados. Os levantamentos de informações necessários para que o banco seja capaz de atender demanda exigida pelo conceito da aplicação e pela aplicação em si. Logo é preciso definir quais serão as informações a serem armazenadas, o nivél de detalhamento, as relações entre si e o uso das mesmas. Assim dessa maneira sendo possível o desenvolvimento dos scripts de criação do banco embasado no que foi anteriormente planejado.


## Valcode

Ano: 2020.2

Parceiro: SPC

<p align="left">
  <a href="https://github.com/JessicaIsri/Valcode">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
</p>
 
Esse projeto foi desenvolvido visando a capacidade de gerar valor aos usuários do Cadastro Positivo, clientes do SPC BRASIL.
O Valcode é uma plataforma que tem como objetivo auxiliar na obtenção de dados sobre o seu cadastro positivo, onde era possivél consultar seu score, saber quantas vezes o seu crédito foi consultado, a evolução do seu score com o passar do tempo, juntar pontos de recompensas para o icentivo da não inadiplencia e acessar a dicas de como ter uma vida financeira mais saudavél.
Os dados utilizados foram capturados a partir de fontes publicas  e de caráter público, sobre o histórico de crédito, dessa forma podendo ser utilizados diante do consentimento do usuário.
Um destaque importante a se fazer é que há uma grande quantia de pessoas que raramente consta na base de dados, por não participar de aquisições sucetíveis ás consultas de crédito, os nomeados "desbancarizados", compostos geralmente de pessoas que não possuem contas bancarias. 
Sendo assim o sistema deve ser capaz de aceitar fontes de dados externas para além das fornecidas pelo SPC.
![image](https://user-images.githubusercontent.com/65822756/141018970-18faf248-3c21-4748-85a4-e09849948422.png)


### Técnologias utilizadas na solução

Java - O java foi utilizado devido as especificações do projeto, porém como vantagem principal o Java se apresenta como uma linguagem muito estavél e segura

Spring Boot - O Spring Boot é um framework para java que permite o desenvolvimento web com base em apis REST e foi escolhido justamente por esse motivo

Angular - O angular é um framework para Java Script, que tem como grandes beneficios a sua modularidade e produtividade 

### Contribuições individuais/pessoais
### Desenvolimento dos Entity e Repositories: 
Os Entity e Repositories são classes de abstração das tabelas do banco de dados. A partir deles podemos acessar as colunas e seus respectivos dados. Para esse projeto foram utilizados as seguintes entidades:
- Fonte
- Modalidade
- Movimentos
- Operacoes
- Pagamentos
- PessoaFisica

```
import javax.persistence.*;
@AllArgsConstructor
@NoArgsConstructor
@Data
@Getter
@Setter
@Entity
@Table(name = "FONTE")
public class Fonte {

    @Id
    private Integer id;

    @Column(length = 50, nullable = false, name = "FONTE_NOME_COMERCIAL")
    private String fonte_nome;
}
```
Acima temos o exemplo de uma entidade referente a tabela fonte, explicando os elementos do código temos:
@AllArgsConstructor e @NoArgsConstructor são anotações pertencentes ao lombok que respectivamente criam um construto com todos os argumentos e um construtor sem os argumentos.

@Getter, @Setter, @Data são anotações pertencentes ao lombok que geram os getters e setters da classe.

@Entity sinaliza ao springboot que se trata de um componente de entidade.

@Table permite que indiquemos o nome da tabela que será referenciado pela classe em questão.

@Id indica que esse atributo se trata de uma coluna identificadora.

@Column permite que indiquemos os atributos da coluna, tais como o tamanho, se permite dado nulo o nome e etc (Muito util quando usamos o próprio hibernate para gerar os schemas.
```
package com.ExampleValcode.valcode.model.repository;

import com.ExampleValcode.valcode.model.entity.Fonte;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface FonteRepository extends JpaRepository<Fonte, Integer> {
}
```
Acima temos o repository da tabela, o mesmo extende os metódos da interface JpaRepository, para isso também precisamos passar qual entidade estamos utilizando e o tipo do seu campo identificador. 

### Serviços de Leitura dos csv's de entrada
Para além da maneira padrão de inserção através de crud, contavamos com um sistema de leitura de csv, que importava os dados para o banco. Segue abaixo um exemplo com a inserção dos dados de fonte:
```
@Service
public class CsvFonteService {


    private final FonteRepository repository;

    @Autowired
    public CsvFonteService(FonteRepository repository){
        this.repository = repository;
    }

    public void save(MultipartFile file){
        try{
            List<Fonte> fontes = CsvFonteHelper.csvToFonte(file.getInputStream());
            repository.saveAll(fontes);
        } catch (IOException e){
            throw new RuntimeException("Fail to Store csv data " + e.getMessage());
        }
    }

    public List<Fonte> getAllFontes(){
        return repository.findAll();
    }
}
```

O @Service indica ao springboot que se trata de um componente que contem as regras de negocio de uma determinada atividade, assim seno possivél o uso do @Autowired dessa classe. Iniciamos a mesma com o constructor que recebe o repository que sera utilizado para salvar os dados na base.
Em seguida temos o metódo save, ele ira utilizar a classe CsvFonteHelper para fazer a conversão do InputStream para um objeto da classe Fonte, a partir o uso de um buffer, percorrendo linha a linha e realizando o link entre a coluna do csv e a coluna do banco de dados:
```
public class CsvFonteHelper {
    public static String TYPE = "text/csv";
    public final String[] HEADERs = {"id", "nom_comercial"};
    public static List<Fonte> csvToFonte(InputStream is) {

        try (BufferedReader fileReader = new BufferedReader(new InputStreamReader(is, "UTF-8"));
             CSVParser csvParser = new CSVParser(fileReader,
                     CSVFormat.DEFAULT.withFirstRecordAsHeader().withIgnoreHeaderCase().withTrim());) {

            List<Fonte> fontes = new ArrayList<Fonte>();

            Iterable<CSVRecord> csvRecords = csvParser.getRecords();

            for (CSVRecord csvRecord : csvRecords) {
                Fonte fonte = new Fonte(
                        Integer.parseInt(csvRecord.get("id")),
                        csvRecord.get("nom_comercial")
                );

                fontes.add(fonte);
            }

            return fontes;
        } catch (IOException e) {
            throw new RuntimeException("fail to parse CSV file: " + e.getMessage());
        }
    }

}
```

Feito isso cada objeto é adicionado a um array que será retornado para o CsvFonteService e salvo a partir da instrução "saveAll()". A vantagem do "saveAll" em relação ao "save()" é que ao contrario do save que cria uma transação para cada registro, o saveAll utiliza uma unica transação para salva multiplos registros, dessa forma sendo muito mais perfomatico quando se é necessario salvar uma coleção de varias linhas no banco de dados.


### Hard Skills Desenvolvidas:
Java, Oracle Database, SpringBoot

### Soft Skills Efetivamente Desenvolvidas:
Como softskills desenvolvidas ressalto a habilidade de priorizar o desenvolvimento de tarefas, comunicação efetiva entre times.


### Aprendizados Efetivos
Como principais apreendizados, devo ressaltar o uso do design patterns e um aprimoramento do conhecimento da linguagem java juntamente com o uso de frameworks para o desenvolvimento web.
Outro ponto importante se dá na analise critica de dados, entender o que casa dado representa e como gerar valor a partir dele e claro sem infligir ou violar a lei geral de proteção de dados (lgpd), pois atualmente devemos ter o máximo cuidado com o uso e exposição de dados de terceiros.

## Nemo
Ano: 2021.1

Parceiro: GSW

<p align="left">
  <a href="https://github.com/JessicaIsri/Nemo">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
</p>

No primeiro semestre de 2021, no então 4º semestre, trabalhamos junto ao parceiro {Nome do parceiro} em uma aplicação que tinha por objetivo o macth entre o candidato e o contratante para uma determinada vaga, com base nas skills e experiência do candidato.

### Contribuições individuais/pessoais
Nesse projeto em especifico, fiquei responsável pelo sistema de calculo do “score” que cada candidato apresentava para a vaga, ou seja, o quanto o candidato se encaixava na vaga a ser disputada.

Como um dos grandes problemas apresentados pelo cliente era a questão de distancia e o valor que a empresa contratante precisaria desembolsar de vale transporte, a aplicação era munida de um modulo de integração geoespacial e o uso de uma das muitas API’s disponibilizada pelo Google em especial o seu produto Directions.

Essa integração consistia no calculo do quão “complexo” seria o transporte do candidato,  para isso utilizei do retorno da API Google Directions. Nela era possível verificar qual a distancia e tempo de locomoção, além de ter informações adicionais como por exemplo: Quantos ônibus eram necessários e qual tempo dentro de cada um. 

Em adição ao sistema provido de geolocalização, também fui responsável pelo desenvolvimento das buscas avançadas por candidatos e oportunidades, utilizando do recurso de critérios.

Para a busca mais avançada o sistema consistia de uma busca ponderada, inicialmente era feito uma busca simples pelos critérios desejados para a vaga de maneira bem genérica. Em seguida com aquele resultado era aplicado uma logica de pesos, onde cada critério atendido da vaga adicionava uma pontuação pré configurada pelo recrutador, assim obtendo um rank de candidatos, dentro dos possíveis candidatos

### Hard Skills Desenvolvidas:
Java, FeingCient, Postgis, Hibernate, JPA

### Soft Skills Efetivamente Desenvolvidas:
Como skill de destaque, devo ressaltar o desenvolvimento da capacidade analítica, como lidar com os dados retornados pela Directions, como usar esses dados ao nosso favor, como gerar valor em uma série de métricas para o nosso cliente.  Por mais do sistema não ser perfeito e acabar por cortar algumas pessoas da lista, ele acabava por apresentar um bom ranqueamento.

## Nemosys
Ano: 2021.2

Parceiro: NESS

<p align="left">
  <a href="https://github.com/api-fatec-bd/api">
    <img width="100px" src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
  </a>
</p>
Para o o 5 semestre tivemos como parceiros a empresa {Nome da empresa}, e o objetivo era o desenvolvimento de uma plataforma para o suporte ao ensino as distancia e oferta de conhecimento, sendo capaz de levantar métricas a partir do uso da plataforma.


### Contribuições Pessoais
Nesse projeto estive mais envolvida na parte de infra estrutura e dev-ops, dentre as atividades desenvolvidas estão: 

Implantação de uma ferramenta de chat, utilizando os serviços de cloud da Digital Ocean e dependências em containers docker, tais como o MongoDB e seu sistema de replicação entre 3 instancias. Nesse caso em especifico se tratavam de 3 imagens Docker que se comunicavam entre si.

Para a aplicação também utilizamos inicialmente uma imagem do SQLSever, porém devido a fatores de subutilização, foi adotado uma imagem de PostgreSql.

Adicionalmente, foi utilizado uma pipeline de deploy automático, que utilizava-se de um Container Repository da Digital Ocean, ou seja, era utilizado um repositório para as imagens docker geradas através do build do sistema, e no servidor onde a aplicação executava era utilizado uma tag para sempre utilizar a imagem mais recente, desse modo sempre que ocorria um merge aprovado para a master, automaticamente a aplicação era atualizada.

Para a realização do deploy era utilizada a seguinte workflow:
```
name: Build And Deploy

on:
  push:
    branches:
      - 'main'
      - 'develop'
jobs:
  setup-build-publish-deploy:
    name: Setup, Build, Publish, and Deploy
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@master
    - name: GitHub Action for DigitalOcean - doctl
      # You may pin to the exact commit or the version.
      # uses: digitalocean/action-doctl@d36a87b1d9c7bd55c8d8434ff2a991a6ee32a448
      uses: digitalocean/action-doctl@v2.1.0
      with:
        # Version of doctl to install
        version: # optional, default is latest
        # DigitalOcean API Token
        token: ${{ secrets.DO_TOKEN }}
    - name: Configure Docker
      run: |
        doctl registry login
    - name: BuildDocker
      run: |
        docker build --tag  registry.digitalocean.com/nemo-container/v1 --file etl/Dockerfile .
    - name: Push to Container Registry
      run: |
        docker push registry.digitalocean.com/nemo-container/v1
```

Por utilizarmos a Digital Ocean para hospedagem e execução, é necessário realizar a configuração de um token através dos secrets do github.

![image](https://user-images.githubusercontent.com/65822756/159380935-24edb62a-3055-4bf2-8db6-95ad3edd77fe.png)

Uma vez configurado o secret, podemos apenas atualizar ou apagar o mesmo.

Juto da aplicação utilizamos um serviço de chat desenvolvido por terceiros e disponibilizado através de uma imagem docker, porém para o seu correto funcionamento o chat dependia da utilização de 3 instancias do mongo, uma primaria e duas replicas.

Para realizar tal feito sem a necessidade de se utilizar 3 VMs da Digital Ocean, foi configurado 3 services do mongo em um arquivo docker-compose, utilizando uma rede para a comunicação entre eles.

```
version: '2'
networks:
    chatNetwork:
        external: true
services:
  mongo:
    image: mongo:4.0
    restart: unless-stopped
    command: mongod --smallfiles --oplogSize 128 --replSet rs0 --storageEngine=mmapv1 -port 27017
    labels:
      - "traefik.enable=false"
    ports:
      - 3002:27017
    networks:
      - chatNetwork
  mongo2:
    image: mongo:4.0
    restart: unless-stopped
    command: mongod --smallfiles --oplogSize 128 --replSet rs0 --storageEngine=mmapv1 -port 27017
    labels:
      - "traefik.enable=false"
    ports:
      - 3003:27017
    networks:
      - chatNetwork
  mongo3:
    image: mongo:4.0
    restart: unless-stopped
    command: mongod --smallfiles --oplogSize 128 --replSet rs0 --storageEngine=mmapv1 -port 27017
    labels:
      - "traefik.enable=false"
    ports:
      - 3004:27017
    networks:
      - chatNetwork
```


### Hard Skills Desenvolvidas:

Java, Git Workflow, Docker, Cloud Compute, MongoDb

### Soft Skills Efetivamente Desenvolvidas:

Como soft skill tive o desenvolvimento da comunicação com o time de desenvolvimento, uma vez que não programava porém precisava dar suporte de infra estrutura as aplicações desenvolvidas.
