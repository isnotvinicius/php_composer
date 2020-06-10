# Composer PHP


## O que é e como utilizar em um projeto

- O Composer é, basicamente, um gerenciador de dependências que instala as dependências de acordo com a necessidade do projeto, nada é instalado no sistema operacional.

- Algumas IDEs, como o phpStorm, permitem iniciar o composer de forma automática, mas também é possível iniciar pelo terminal, basta navegar até a pasta do projeto e dar o comando "composer init". No final será gerado um arquivo .json.

- Normalmente para se criar o pacote utilizamos (<vendor>/<name>), onde vendor é quem está oferendo o pacote (seu nome, nome da empresa, etc.) e name é o nome do pacote.

- Por padrão o campo type vem como library, mas podemos especificar o tipo que preferirmos.


## Instalando dependências

- Para instalarmos uma dependência podemos buscar por ela em sites como packagist.org e instalar de duas formas diferentes:
  
    1 - Podemos utilizar o comando "composer require <nome do pacote>" pelo terminal.
    2 - Podemos adicionar a dependência no campo require do arquivo json e utilizar os comandos "composer install" e "composer update" no terminal.

- Caso precisemos instalar algo que fique apenas no ambiente de desenvolvimento podemos utilizar o "composer require --dev", isso permite que quando formos rodar a aplicação em ambiente de produção utilizemos o comando "composer install --no-dev" para eliminarmos as instalações usadas apenas no desenvolvimento evitando coisas desnecessárias no ambiente de produção.

- Neste projeto estamos utilizando o guzzle para requisições http e o DomCrawler para percorrer arquivos html.

- Para a utilização correta das dependências é de suma importância a leitura da documentação.


## PSR-4

- o PSR de Autoload é um meio de "ensinar" o composer o caminho das nossas classes através do namespace delas, fazendo com que seja possível utilizarmos apenas o "require autoload.php".

- Todas as classes possuem um namespace que será o namespace principal, no nosso exemplo temos "Alura\BuscadorCursos", e mapeamos este namespace para uma pasta, src no exemplo.
Com isso informamos que todas as classes dentro do namespace Alura\BuscadorCursos estão dentro da pasta src. Se tivermos mais namespaces além destes estaremos informando que o namespace está na pasta src/pastaNova.

- O PSR-4 é implementado no arquivo json do composer, lá nós especificamos o namespace e a pasta raiz: ("namespace\\" : "pasta/").

- Depois de configurado basta executar o comando "composer dumpautoload" no terminal para atualizar o arquivo de autoload.


## Classmap e Files

- O classmap e o File são utilizados para configurar o arquivo autoload para bibliotecas ou classes que não utilizam o padrão PSR-4, ou seja, não possuem namespace.

- Para utilizar o classmap colocamos ele dentro da chave autoload do arquivo json e informamos todos os diretórios que possuem classes e não possuem namespace.

- O files segue o mesmo princípio, basta adicionarmos o array de files dentro do autoload do json e colocar o caminho dos arquivos que serão necessários.

- Também é necessário o comando dumpautoload para atualizar o arquivo.


## Scripts

- Dentro do arquivo json podemos adicionar uma chave "scripts", nela podemos dar nomes aos scripts, que normalmente são grandes, executados no terminal. 

- ("nome_script": "comando + arquivo.php").

- Isso deixa o script mais curto e fácil de se lembrar, basta digitar "composer + nome_script". Lembrando que não é necessário colocar o caminho vendor/bin.

- É possível executar vários comandos num comando só, basta colocar o nome_script e os comandos a serem associados a ele entre [], caso seja necessário referenciar outros scripts já criados colocamos uma @ na frente do script. ("nome_script": ["@script1", "@script2"]).

- Com as chaves "scripts-description" podemos adicionar descrições aos scripts criados. Podemos acessar a descrição com o comando "composer list".

- Também é possível executar qualquer comando php ou comandos de sistema operacional através do composer. Um exemplo disto é que para vermos os arquivos de um diretório em linux utilizamos ls e no windows utilizamos dir, para alguém acostumado com um dos dois sistemas é difícil lembrar os comandos do outro sistema ou digitar corretamente sempre e através do script do composer podemos associar os dois comandos para utilizá-los no terminal. ("ls": "dir") ou vice-versa.