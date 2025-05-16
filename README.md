
**Autor:** Henrique Ferreira Santos  
**Data de desenvolvimento:** 20/09/2020

Este projeto é um desafio proposto pela Semantix, focado em análise de logs da NASA utilizando tecnologias Big Data, especialmente Apache Spark com Scala. O objetivo principal é processar, analisar e extrair informações relevantes de grandes volumes de logs.

## Resumo do Projeto

Este projeto utiliza Apache Spark para processar arquivos de log (como logs da NASA), realizando operações como:

- Leitura de arquivos de texto contendo logs.
- Conversão dos dados em DataFrames e Datasets para processamento distribuído.
- Cálculo de estatísticas como:
  - Número de hosts únicos.
  - Total de erros 404.
  - URLs mais acessadas ou que mais geraram erros.
- Utilização de técnicas de otimização como cache para melhorar a performance.
- Demonstração de conceitos fundamentais do Spark, como RDDs, operações de transformação e ação, e diferenças entre `groupByKey` e `reduceByKey`.

## Perguntas e Respostas sobre Spark

**Qual o objetivo do comando cache em spark?**

O objetivo do comando cache é armazenar o resultado de um processamento em memória.  
A utilização deste comando evita que toda vez que o resultado do processamento é invocado o processamento seja realizado novamente.  
A utilização do cache é de grande importância para processamentos pesados, pois a cada utilização da variável a aplicação spark faria novamente o cálculo causando um grande decréscimo da performance da aplicação.

**O mesmo código implementado em spark é normalmente mais rápido que a implementação equivalente em MapReduce. Por que?**

A diferença de performance pode ser devido aos paradigmas "Lazy evaluation" e o processamento "in-memory" disponíveis no spark.  
O "Lazy evaluation" permite que o spark agregue operações semelhantes do mesmo dado juntas sem a necessidade do processamento do dado diversas vezes, isto faz processamentos grandes e que utilizem o mesmo dado mais de uma vez tenham uma grande eficiência frente ao MapReduce.  
Este paradigma permite que processos que são utilizados mais de uma vez no código sejam executados apenas uma vez, e o resultado de um processamento pode ainda ser armazenado em memória.

**Qual a função do sparkContext?**

Permitir a conexão entre o Driver Program e o Spark cluster. O sparkContext é o ponto de entrada para a funcionalidade do Spark.

**Explique com suas palavras o que é Resilient Distributed Datasets (RDD).**

É o dado distribuído em diferentes partições para permitir o processamento paralelo do dado em diferentes nós do cluster.

**GroupByKey é menos eficiente que reduceByKey em grandes datasets. Por que?**

Pelo tráfego de dados entre os nós pela rede.  
Com o groupByKey todo o dado é trafegado pela rede, reduceByKey trafega apenas o resultado da operação.  
GroupByKey irá transferir todo o conjunto de dados (Dataset) através da rede para os outros workers para que ele realize a operação.  
Enquanto o reduceByKey irá realizar a operação em cada partição e após realizar o cálculo transmitirá o resultado da operação para os outros workers.

**Explique o que o código scala abaixo faz**

O código abaixo abre um determinado arquivo de texto informado, contabiliza quantas vezes cada palavra é referenciada no texto e salva o resultado em um arquivo de texto.

## Instruções de Execução

- Colocar os dois arquivos em um único diretório
- Informar como parâmetro o diretório do arquivo

## Estrutura do Projeto

- `DesafioSemantix/`  
  Diretório principal do código-fonte e módulos Maven.
  - `processLogs/`  
    Módulo responsável pelo processamento dos logs.
    - Código principal em [`processLogs.scala`](DesafioSemantix/processLogs/src/main/scala/br/app/processLogs.scala)
  - `README.md`  
    Documentação principal do projeto.

## Tecnologias Utilizadas

- Scala
- Apache Spark
- Maven

---

Para mais detalhes sobre o processamento dos logs, consulte o arquivo [`processLogs.scala`](DesafioSemantix/processLogs/src/main/scala/br/app/processLogs.scala).
