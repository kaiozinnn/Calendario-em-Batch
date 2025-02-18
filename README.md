# Calendário em Batch (.bat)


## Introdução
Este script em Batch foi desenvolvido com o objetivo de automatizar a criação de diretórios baseados no número de dias de um mês específico de um ano, considerando se o ano é bissexto ou não. O script facilita a organização de arquivos em um formato hierárquico, onde cada dia do mês é representado por uma pasta numerada, criando uma estrutura de diretórios de forma simples e eficiente.

## Fluxo do Script
1. **Verificação e criação de pastas:** O script começa verificando se o diretório especificado para o ano e o mês existe. Se não  existir, ele cria as pastas necessárias.
2. **Cálculo de dias do mês:** O script calcula o número de dias de um mês específico, considerando se o ano é bissexto (fevereiro com 29 dias ou 28).
3. **Criação das pastas diárias:** Para o número de dias calculado, o script cria pastas com o nome do número de cada dia (1, 2, 3, ..., até o último dia do mês).
4. **Mensagem de confirmação:** Após a criação das pastas, o script exibe uma mensagem confirmando o número de dias no mês e o ano.

---

## Explicação Detalhada do Código
### Criação de Diretórios para Ano e Mês


```batch
if not exist "%1" (
    mkdir "%1"
)
cd "%1"
```

- O código começa verificando se o diretório do ano (passado como primeiro parâmetro %1) existe. Caso não exista, o script cria a pasta. Em seguida, ele entra no diretório recém-criado ou existente.


```batch
if not exist "%2" (
    mkdir "%2"
)
cd "%2"
```

- De forma similar, o script verifica e cria o diretório para o mês (passado como segundo parâmetro %2), em seguida acessa esse diretório.


### Definindo o Ano e o Mês


```batch
set mes=%2
set ano=%1
```


- As variáveis mes e ano são configuradas com os parâmetros recebidos ao rodar o script, representando respectivamente o mês e o ano para os quais as pastas serão criadas.


### Verificação de Ano Bissexto


```batch
set /a bissexto=0
set /a resto1=%ano% %% 4
set /a resto2=%ano% %% 100
set /a resto3=%ano% %% 400

if %resto1% == 0 (
    if %resto2% == 0 (
        if %resto3% == 0 (
            set bissexto=1
        ) else (
            set bissexto=0
        )
    ) else (
        set bissexto=1
    )
)
```


- O código verifica se o ano é bissexto, utilizando as regras de divisibilidade (divisível por 4, não divisível por 100, ou divisível por 400). O valor da variável bissexto é configurado para 1 caso seja bissexto e 0 caso contrário.


### Determinação do Número de Dias do Mês


```batch
if %mes%==1 set dias=31
if %mes%==2 (
    if %bissexto%==1 (
        set dias=29
    ) else (
        set dias=28
    )
)
if %mes%==3 set dias=31
...
```


- O número de dias de cada mês é determinado. Se o mês for fevereiro, o número de dias será ajustado conforme o valor da variável bissexto, garantindo que fevereiro tenha 29 dias em anos bissextos e 28 em anos não bissextos.


### Criação das Pastas Diárias


```batch
for /L %%i in (1,1,%dias%) do (
    mkdir %%i
)
```


- Utilizando um loop for, o script cria pastas numeradas de 1 até o número de dias do mês especificado.


### Mensagem de Confirmação


```batch
echo O numero de dias no mes %mes% do ano %ano% é %dias%.
```


- O script exibe uma mensagem informando o número de dias no mês especificado.


### Retorno ao Diretório Original


```batch
cd ..
```


- Após a criação das pastas, o script volta para o diretório anterior, mantendo a estrutura organizada.


---


## Desafios e Soluções

### Desafio 1: Verificação do Ano Bissexto
- **Problema:** Implementar corretamente a verificação de ano bissexto.
- **Solução:** Utilizei operações de módulo para verificar as condições de divisibilidade (divisível por 4, não por 100, ou divisível por 400).


### Desafio 2: Lidar com a criação de pastas de forma dinâmica
- **Problema:** Criar um número dinâmico de pastas, de acordo com o número de dias de cada mês.
- **Solução:** Utilizei o loop for /L para iterar de 1 até o número de dias e criar as pastas correspondentes.


## O que Aprendi
Ao desenvolver este script, aprendi a trabalhar com a linguagem Batch de maneira mais eficiente, compreendendo melhor o uso de variáveis, loops, e a lógica condicional. Além disso, entendi como automatizar tarefas de organização de arquivos de maneira simples e eficaz.
Esse tipo de automação é útil em muitos cenários, como organizar relatórios diários, documentos de trabalho ou até mesmo fazer backups de forma automatizada. Eu também aprendi a lidar com condições como anos bissextos e como fazer cálculos simples em Batch.


## Possíveis Melhorias
- **Validação de Entradas:** O script pode ser melhorado com validação de entradas, como garantir que o mês esteja entre 1 e 12 e que o ano seja um número válido.
- **Mensagens de Erro:** Melhorar a comunicação com o usuário, fornecendo mensagens de erro quando um diretório não possa ser criado ou quando as entradas forem inválidas.
- **Otimizando a Criação das Pastas:** Ao invés de criar pastas individualmente em um loop, é possível explorar métodos alternativos, como a criação de pastas com uma estrutura mais avançada (por exemplo, em árvore).


## Exemplo de Execução
### Entrada
- Ano: 2024
- Mês: 2
### Saída
O script cria a estrutura de diretórios:


```markdown
2024
  └── 2
      ├── 1
      ├── 2
      ├── ...
      └── 29
```


Ao final, a mensagem de confirmação será:


```perl
O número de dias no mês 2 do ano 2024 é 29.
```

---


## Considerações Finais
Esse desafio foi uma excelente oportunidade de aprendizado, pois me permitiu desenvolver um script prático, utilizando recursos básicos e avançados da linguagem Batch. A criação de pastas diárias é uma automação simples, mas que pode ser útil em muitos cenários do dia a dia. O processo me ajudou a entender melhor como escrever scripts para tarefas repetitivas e como fazer o código funcionar de forma eficiente.

---

Este modelo é uma explicação detalhada do script, com foco em aprendizado, dificuldades enfrentadas, e melhorias possíveis. Se precisar de mais alguma alteração ou quiser incluir algo específico, fico à disposição!
