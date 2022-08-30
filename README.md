# Minicurso: Pyhton para Manipulação e Análise de Dados

### Ministrado em parceria com o Programa de Educação Tutorial(PET) do curso de Ciências Sociais da UFMG nos dias 30 e 31 de agosto de 2022.

---

## Introdução

Esse curso tem como objetivo facilitar o contato com a linguagem Python e suas possibilidades básicas na área de dados, além de trazer segurança e coragem para que qualquer pessoa se aventure nesse universo!

Para isso, foi utilizado um banco de dados da PNAD (Pesquisa Nacional de Amostra Domiciliar) disponibilizado neste repositório com o nome de [df_Minicurso.xlsx](../df_Minicurso.xlsx), o qual conta com o arquivo de dicionário de variáveis ([dicionario.xls](../dicionario_PNADC_microdados_trimestre4_20220224.xls)).

Em um primeiro momento, tivemos a parte teórica abrangendo os seguintes temas:

* Visão abrangente sobre Pyhton (e R) e suas possibilidades;

* Linha Histórica da PNAD;

* Estrutura de Banco de dados;

* Conceitos de Variáveis, Tipos e Estruturas de Dados;

Em seguida, tivemos a parte prática no Ambiente de Desenvolvimento do Google COLAB, disponível [aqui](https://colab.research.google.com/drive/1M88teWhAczc3CSpxYitFmRuNU6wB9iFP#scrollTo=3pkH1Qm8BySv) e também a seguir. 

Por isso, nada referente à instalação e configuração do Pyhton foi necessário.

</details>

<details>
      <summary>
            <b><u><font size="+2"> Boas Vindas </font></u></b>
      </summary>

Para dar boa sorte nesse processos e testar nosso ambiente de programação, vamos imprimir "Olá, Mundo!" na nossa tela.

```
print('Olá, Mundo!')
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Google Colab </font></u></b>
      </summary>

O Colaboratory ou “Colab” é um produto do Google Research, que permite que qualquer pessoa escreva e execute código Python arbitrário pelo navegador. Não requer nenhuma configuração e é sem custo financeiro.

* Seu Notebook

Você pode criar um notebook (livro de código) em Arquivos > Novo notebook para acompanhar o curso, testar seus códigos e fazer anotações OU fazer uma cópia desse  em Arquivos> Salvar uma Cópia, assim você terá acesso à esse arquivo no seu drive...


* Upload de Arquivos

O Google Colab não consegue ler um arquivo que está no nosso computador, por isso é importante colocar esse arquivo aqui dentro do nosso notebook todas as vezes que formos utilizá-los. Esse arquivo será excluído automaticamente após o encerramento do ambiente de excecução.

Para isso, clicar na pasta no canto esquerdo "Arquivos". Em seguida, clicar no primeiro item para fazer upload do arquivo que está no computador, encontrá-lo e clicar em Abrir, conforme a imagem:

<img src="https://github.com/abicego/Minicurso_Python/blob/master/images/colab_arquivos.jpg">

</details>

<details>
      <summary>
            <b><u><font size="+2"> Importando Biblioteca </font></u></b>
      </summary>

Neste primeiro momento, importaremos apenas a Biblioteca [PANDAS](https://pandas.pydata.org/) (com o "apelido" de pd), que é utilizada para manipulação e análise de dados, escrita em Python.

Obs: Biblioteca pode ser entendido como um conjunto de funções/ vários códigos que já foram escritos e estão disponíveis para serem usadas por qualquer pessoa ao utilizar essa linguagem

```
import pandas as pd
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Lendo a PNAD </font></u></b>
      </summary>

Agora, utilizamos uma função da biblioteca pandas para importar nosso arquivo de dados para esse ambiente

* Caso estivessemos usando Microdados:

1. Para abrir o arquivo usei a função read_fwf, porque ela "lê uma tabela de linhas formatadas de largura fixa no DataFrame" (há varias funções p/ diferentes a extensão: excel, csv, stata)

2. Já que a base de dados original não possui o separador de colunas enquanto delimitador (exemplo: " ; |), usei a propriedade width (largura) da função read_fwf para colocar as infos da coluna "Tamanho" (disponibilizadas no arquivo Dicionário da PNAD).
Ela tem que ser definida antes da função, para que consiga ser lida

3. O df original não possui um cabeçalho com o nome de cada coluna, por isso, defini o nome das colunas com o atributo .columns

```
width_df = [copiar e colar aqui a sequência numérica da coluna "Tamanho" presente no dicionário, exemplo: 4, 1, 2, 2, 2, 9, 7, ...]
df = pd.read_fwf('C:/Users/seucaminho/Arquivo.txt', header=None, dtype=str, widths=width_df)
df.columns = [copiar e colar aqui a sequência numérica da coluna "Código da variável" presente no dicionário, exemplo: 'Ano', 'Trimestre', 'Capital', 'RM_RIDE', 'UPA', ... ]
```

* Nosso arquivo (neste ambiente):

1. Fazer Upload do Arquivo no google Colab conforme descrito
2. Copiar Caminho deste arquivo
3. Usar a função pd.read_excel ler nossa base de dados


```
df_pnad = pd.read_excel('/content/df_Minicurso.xlsx')
```


Criar uma cópia do dataframe original, para garantir a integridade caso algo aconteça: ˋdf=df_pnadˋ

</details>

<details>
      <summary>
            <b><u><font size="+2"> DataFrame / Visualização dos dados: Tabelas </font></u></b>
      </summary>

Para fins didáticos, aqui o DataFrame pode ser ententido apenas como o banco de dados em si. 

Essa seção é dedicada para códigos que trazem uma visão mais ampla ou até mesmo individual de cada coluna, para analisarmos se ele foi lido corretamente, também tirar frequência das variáveis; fazer cruzamentos; agrupar colunas para melhorar a visualização....

Código para ver as 5 primeiras linhas do Dataframe (pode colocar numero no parenteses para aumentar a quantidade de linhas): `df_pnad.head()ˋ

Quantidade de linhas: `len(df)`

Quantidade de linhas e colunas: `df.shape`

Nome das colunas: `df.columns`

Banco de dados, de acordo com ascendência (ou não) em determinada coluna 

```
df.sort_values('V2010', ascending=True).head(20)
df.sort_values('V2010', ascending=False).head(20)
```

Visualização de duas (ou +) colunas, lado a lado

```
df[['V2007','V2010']]
df[['V2007','V2010']].head()
```

Ver a distribuição de acordo com determinada condição

```
df[df['V2005']==8][['UF',V2007','V2010']]
```

Cruzar 2 variáveis

```
pd.crosstab(index=df['V2007'], columns=df['V2010'])
```

Cruzar 3 variáveis

```
pd.crosstab(df['V2005'], [(df['V2007']), df['V2010']], rownames=['Condição'], colnames=['sexo', 'cor'])
```

Cruzar 3 variáveis de acordo com determinadas condições

```
pd.crosstab(df['V2005']=='8', [(df['V2007']=='01'), df['V2010']], rownames=['Condição'], colnames=['sexo', 'cor'])
```

Contagem de casos de determinada coluna de acordo com a categoria

```
df['V2007'].value_counts()
```

Agrupamento de casos por atributo e a média de outra caracteristica

```
df.groupby('V2007')['V2009'].mean()
```

Panorama geral da estatística descritiva do dataframe

```
df.describe()
```

Panorama geral estatística descritiva de uma coluna ou mais colunas

```
df_final[['V2009', 'VD4019']].describe()
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Atribuição de rótulos </font></u></b>
      </summary>

Aqui, veremos como alterar o nome das colunas e o rotulos dos dados. Vale ressaltar que quando um dado é do tipo string, este deve estar entre aspas (duplas ou simples), já se for numérico, tem que ser informado sem as aspas.

Relembrando nome das colunas: `df_pnad.columns`

Renomear Colunas

```
df=df.rename(columns={
      'V1022': 'Situação_do_domicílio',
      'V2005': 'Condição_no_domicílio',
      'V2007': 'Sexo',
      'V2009': 'Idade_do_morador',
      'V2010': 'Cor_ou_raça',
      'V3001': 'Sabe_ler_escrever',
      'V3009A': 'Curso_mais_elevado_que_frequentou',
      'V3014': 'Concluiu_este_curso',
      'V4001': 'Trabalhou_remunerado_dinheiro',
      'V4009': 'Quantos_trabalhos',
      'S01021': 'Quantos_moradores_celular',
      'S01022': 'Domicílio_telefone_fixo',
      'S01029': 'Algum_morador_acesso_internet',
      'S07009': 'Quem_foi_o_informante_deste_módulo',
      'VD3004': 'Nível_de_instrução_mais_elevado_alcançado',
      'VD3005': 'Anos_de_estudo',
      'VD4001' : 'Condição_em_relação_à_força_de_trabalho',
      'VD4002' : 'Condição_de_ocupação',
      'VD4007' : 'Posição_na_ocupação_no_trabalho',
      'VD4013' : 'Faixa_das_horas_trabalhadas',
      'VD4019' : 'Rendimento_mensal',
      'VD4031' : 'Horas_trabalhadas_semana',
      'VD4036' : 'Faixa_horas_trabalhadas_semana',
      'VDI5012' : 'Faixa_de_rendimento_domiciliar_per_capita'
})
```

Analisar a alteração dos nomes das colunas: `df.columns`

Renomear Atributos

```
df=df.replace({ 
      'Situação_do_domicílio' : {1:'Urbana',2:'Rural'},
      'Condição_no_domicílio' : {7 : 'Genro ou nora', 8 : 'Pai, mãe, padrasto ou madrasta', 9 : 'Sogro(a)'},
      'Sexo' : {1:'Homem',2:'Mulher'},
      'Cor_ou_raça' : {1:  'Branca', 2: 'Preta', 3: 'Amarela', 4: 'Parda', 5: 'Indígena', 9: 'Ignorado'},
      'Sabe_ler_escrever' : {1:'Sim',2:'Não'},
      'Curso_mais_elevado_que_frequentou' : {1: 'Creche (disponível apenas no questionário anual de educação)', 2: 'Pré-escola', 3: 'Classe de alfabetização - CA', 4: 'Alfabetização de jovens e adultos', 5: 'Antigo primário (elementar)', 6: 'Antigo ginásio (médio 1º ciclo)', 7: 'Regular do ensino fundamental ou do 1º grau', 8: 'Educação de jovens e adultos (EJA) ou supletivo do 1º grau', 9: 'Antigo científico, clássico, etc. (médio 2º ciclo)',10: 'Regular do ensino médio ou do 2º grau',11: 'Educação de jovens e adultos (EJA) ou supletivo do 2º grau',12: 'Superior - graduação',13: 'Especialização de nível superior',14: 'Mestrado',15: 'Doutorado'},
      'Concluiu_este_curso' : {1:'Sim',2:'Não'},
      'Trabalhou_remunerado_dinheiro' : {1:'Sim',2:'Não'},
      'Quantos_trabalhos' : {1:'Um', 2:'Dois', 3 : 'Três ou mais'},
      'Domicílio_telefone_fixo' : {1:'Sim',2:'Não'},
      'Algum_morador_acesso_internet' : {1:'Sim',2:'Não'},
      'Nível_de_instrução_mais_elevado_alcançado' : {1: 'Sem instrução e menos de 1 ano de estudo',2: 'Fundamental incompleto ou equivalente',3: 'Fundamental completo ou equivalente',4: 'Médio incompleto ou equivalente',5: 'Médio completo ou equivalente',6: 'Superior incompleto ou equivalente',7: 'Superior completo'},
      'Condição_em_relação_à_força_de_trabalho': {1: 'Pessoas na força de trabalho',2: 'Pessoas fora da força de trabalho'},
      'Condição_de_ocupação': {1: 'Pessoas ocupadas',2: 'Pessoas desocupadas'},
      'Posição_na_ocupação_no_trabalho' : {1: 'Empregado (inclusive trabalhador doméstico)',2: 'Empregador',3: 'Conta própria',4: 'Trabalhador familiar auxiliar'},
      'Faixa_horas_trabalhadas_semana' : {1: 'Até 14 horas', 2: '15 a 39 horas', 3: '40 a 44 horas',4: '45 a 48 horas', 5: '49 horas ou mais'},
      'Faixa_de_rendimento_domiciliar_per_capita' : {1: 'Até ¼ salário mínimo', 2: 'Mais de ¼ até ½ salário mínimo', 3: 'Mais de ½ até 1 salário mínimo', 4: 'Mais de 1 até 2 salários mínimos',5: 'Mais de 2  até 3 salários mínimos',6: 'Mais de 3 até 5 salários mínimos',7: 'Mais de 5 salários mínimos',9: 'Ignorado'},
})
```

Analisar a alteração dos nomes dos atributos: `df['Sexo'].value_counts()`

Comando para ver o tipo de dados de cada coluna: `df.dtypes`

</details>

<details>
      <summary>
            <b><u><font size="+2"> Estrutura condicional e filtros </font></u></b>
      </summary>

Criar uma variável de filtro baseada em condições, por exemplo: Se na coluna X o valor for igual a 1 e na Y for igual a 2, a variável de nome Filtro marcará Verdade (True), se não, Falso.

Criar nova variável de acordo com outras instruções (Retorna true ou false)

```
df['Filtro'] = ((df['UF'] == 31) & (df['Condição_no_domicílio'] == 'Pai, mãe, padrasto ou madrasta') & ((df['Idade_do_morador'] >= 18) & (df['Idade_do_morador'] <= 80)))
```

Verificar se a nova coluna consta na lista: `df.columns`

Ver a distribuição da Filtro, por coluna

```
df[df['Filtro']==True][['Filtro','UF','Condição_no_domicílio', 'Idade_do_morador']]
```

Fazer Agrupamento utilizando o método [.loc](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html). É mais utilizado para definir rapidamente instruções lógicas simples em poucas linhas quando a condição tiver um resultado binário (tanto verdadeiro quanto falso).

```
df.loc[(df['Idade_do_morador'] >=18 ) & (df['Idade_do_morador'] <=20),  'Faixa_Etaria'] = '18 a 20 anos'
df.loc[(df['Idade_do_morador'] >=21 ) & (df['Idade_do_morador'] <=30),  'Faixa_Etaria'] = '21 a 30 anos'
df.loc[(df['Idade_do_morador'] >=31 ) & (df['Idade_do_morador'] <=40),  'Faixa_Etaria'] = '31 a 40 anos'
df.loc[(df['Idade_do_morador'] >=41 ) & (df['Idade_do_morador'] <=50),  'Faixa_Etaria'] = '41 a 50 anos'
df.loc[(df['Idade_do_morador'] >=51 ) & (df['Idade_do_morador'] <=60),  'Faixa_Etaria'] = '51 a 60 anos'
df.loc[df['Idade_do_morador'] >= 61,  'Faixa_Etaria'] = '61 anos ou mais'
```

Ver a distribuição da coluna Filtro em relação às outras coluna

```
df[df['Filtro']==True][['Idade_do_morador','Faixa_Etaria']]
```

Frequência/ Contagem da Coluna com rótulos ascendentes

```
df['Faixa_Etaria'].value_counts(ascending=True)
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Divisão de banco de dados </font></u></b>
      </summary>

"Criar" um novo banco de dados baseado na coluna Filtro

Filtrar DataFrame com base em condição da coluna e salvar em um nome DataFrame

```
df_filter = df.loc[df['Filtro'] == True]
```

Analisar o shape do banco: `df_filter.shape`

</details>

<details>
      <summary>
            <b><u><font size="+2"> Limpeza da base de dados </font></u></b>
      </summary>

Limpar a base de dados consiste em apagar colunas ou casos não desejados.

Apagar Colunas e salvar outro DataFrame

```
df_filter1 = df_filter.drop(['Ano', 'Trimestre', 'UF', 'Capital', 'RM_RIDE',
                'Sabe_ler_escrever', 'Curso_mais_elevado_que_frequentou', 'Concluiu_este_curso',
                'Domicílio_telefone_fixo','Quem_foi_o_informante_deste_módulo',
                'Anos_de_estudo', 'Faixa_horas_trabalhadas_semana'], axis=1)
```

Escolher Colunas e salvá-las em outro DataFrame

```
df_filter2=df_filter[['Ano', 'Trimestre', 'UF', 'Capital', 'RM_RIDE',
                'Sabe_ler_escrever', 'Curso_mais_elevado_que_frequentou', 'Concluiu_este_curso',
                'Domicílio_telefone_fixo','Quem_foi_o_informante_deste_módulo',
                'Anos_de_estudo', 'Faixa_horas_trabalhadas_semana']]
```

Mostrar missing values no banco de dados (Se na/null = True) : `df_filter1.isna()`

Loop para mostrar a quantidade de null por coluna

```
for i in df_filter1:
    print(i,df_filter1[i].isna().sum())
```

Trocar missings values por outro numero

```
df_filter1['Quantos_trabalhos'] = df_filter1['Quantos_trabalhos'].fillna(0)
```

Fazer cópia do DataFrame para fazer teste de apagar linhas: `dfteste = df_filter1`

Apagar uma linha de acordo com vazio na coluna

```
dfteste = dfteste[dfteste['Rendimento_mensal'].notna()]
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Juntar bases de dados </font></u></b>
      </summary>

Juntar / Agrupar bancos de dados, funções disponíveis: [.concat()](https://pandas.pydata.org/docs/reference/api/pandas.concat.html); [.join()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.join.html) e  [.merge()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html)

Juntar Bancos Filter 1 e 2 baseado na coluna index (comum entre os dois) 

```
df_concat = pd.concat([df_filter1, df_filter2], axis=1)
```

Analisar shpe do banco: `df_concat.shape`

</details>

<details>
      <summary>
            <b><u><font size="+2"> Exportação de base de dados </font></u></b>
      </summary>

A qualquer momento é possível salvar/ exportar o banco de dados para uso posterior e em praticamente qualquer formato/ extensão (excel, csv, txt). O que muda é a função do pandas utilizada

Definir colunas que ficam / ordem

```
df_final=df_filter1[['Sexo', 'Idade_do_morador', 'Faixa_Etaria', 'Cor_ou_raça',
  'Faixa_de_rendimento_domiciliar_per_capita','Situação_do_domicílio',
  'Quantos_moradores_celular', 'Algum_morador_acesso_internet',
  'Nível_de_instrução_mais_elevado_alcançado',
  'Trabalhou_remunerado_dinheiro','Quantos_trabalhos',
  'Condição_em_relação_à_força_de_trabalho', 'Condição_de_ocupação',
  'Posição_na_ocupação_no_trabalho', 'Faixa_das_horas_trabalhadas',
  'Rendimento_mensal', 'Horas_trabalhadas_semana']]
```

Exportar Base de dados em tabela do excel **JUPYTER**


```
df_filter.to_excel('C:/[caminho]/[arquivo].xlsx', index=False, sheet_name='base') 

```

Exportar Base de dados em tabela do excel **COLAB**

```
from google.colab import files

df_final.to_excel('df_FINAL_Minicurso.xlsx')
files.download('df_FINAL_Minicurso.xlsx', index=False)
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Visualização dos dados: Gráficos </font></u></b>
      </summary>

Para gerar gráficos, é necessário importar as bibliotecas: [Seaborn](https://seaborn.pydata.org/index.html) e 
[Matplotlib](https://https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.html). Vale ressaltar que é possível ajustar praticamente todos os aspectos visuais conforme consta nas respectivas documentações.

Obs: Para salvar os gráficos gerados como imagem (da extensão que preferir), o trecho de código é: fig.savefig('Nome do Arquivo.jpg'). Após esse processo, essa figura constará nos arquivos do colab e então basta clicar nos três pontinhos laterais e Fazer Download.

Importar bibliotecas

```
import matplotlib.pyplot as plt
import seaborn as sns
```

Relembrar colunas: `df_final.columns`


Plotar histograma do Matplotlib SEM formatação da distribuição por Sexo

```
plt.hist(df_final['Sexo'], 3)
plt.show()
```

Plotar histograma do Matplotlib COM formatação da distribuição por Sexo e salvá-lo

```
plt.title('Distribuição por Sexo', fontsize=12)
plt.xlabel('Sexo', fontsize=10)
plt.ylabel('Frequência Absoluta', fontsize=10)
plt.tick_params(labelsize=8)
plt.hist(df_final['Sexo'], 3, rwidth=0.9, color='#6fa8c7', alpha=0.7, edgecolor='black')
plt.savefig("Imagem5 - Distribuição Sexo.jpg")
plt.show()
```

Plotar Normal do Seaborn SEM formatação da distribuição por Idade

```
sns.distplot(df_final['Idade_do_morador'])

```

Plotar histograma do Seaborn SEM formatação da distribuição por Sexo e salvá-lo

```
sns.histplot(df_final['Sexo'])
fig = hist.get_figure()
fig.savefig('Imagem2 - Distribuição Sexo.png')
```

Plotar barplot do Seaborn COM formatação da distribuição de Cor/Raça por Sexo e salvá-lo (para as cores: usar atributo palette ou comando `sns.set_theme(style="darkgrid")´)

```
brplt = sns.barplot(x="Cor_ou_raça", y="Idade_do_morador", data=df_final,  palette="Greens_d");
fig = brplt.get_figure()
fig.savefig('Imagem2 - Distribuição Sexo.png')
```

Ver o tipo dos dados de cada coluna para avaliar adequação do gráfico: `df_pnad.dtypes`

Plotar boxplot do Seaborn COM formatação da distribuição de Condição de ocupação por Idade e salvá-lo

```
sns.set_theme(style="darkgrid")
boxplt = sns.boxplot(x ='Condição_de_ocupação', y ='Idade_do_morador', data = df)
fig = boxplt.get_figure()
fig.savefig('Imagem5 - Horas Trabalhadas vs Rendimento Mensal Sexo.jpg')
plt.show(boxplt)
```


Plotar scatterplot do Seaborn COM formatação da Distribuição de Horas trabalhadas por Rendimento Mensal e salvá-lo

```
scatt = sns.scatterplot(data=df_final, x='Horas_trabalhadas_semana', y='Rendimento_mensal', hue='Sexo', palette=['black', 'red'])
fig = scatt.get_figure()
fig.savefig('Imagem5 - Horas Trabalhadas vs Rendimento Mensal Sexo.jpg')
plt.show(scatt)
```

Plotar scatterplot do Seaborn COM formatação de elementos individuais da Distribuição de Horas trabalhadas por Rendimento Mensal e salvá-lo

```
scatt = sns.scatterplot(data=df_final, x='Horas_trabalhadas_semana', y='Rendimento_mensal', hue='Sexo', palette=['black', 'red'])
plt.title('Distribuição de Horas trabalhadas por Rendimento Mensal', fontsize=12)
plt.xlabel('Horas trabalhadas da semana', fontsize=10)
plt.ylabel('Rendimento Mensal', fontsize=10)
plt.tick_params(axis='both', which='major', labelsize=14)
fig = scatt.get_figure()
fig.savefig('Imagem6 - Horas Trabalhadas vs Rendimento Mensal Sexo.jpg')
plt.show(scatt)
```

</details>

<details>
      <summary>
            <b><u><font size="+2"> Relatório </font></u></b>
      </summary>

Já vimos como salvar os gráficos como imagem, agora, para salvar todo esse notebook (de extensão .ipynb), incluindo tópicos, textos, códigos e outputs (TUDO que aparece nele) em PDF, seguir o seguinte passo:

1. Clicar em Arquivos > Fazer Download > Fazer o download do .ipynb

2. Importar/ Fazer Upload desse arquivo para esse ambiente (conforme fizemos com a base de dados)

3. Rodar os trechos de código a seguir:

Fazer instalação de um pacote chamado Texlive, necessário nesse processo (duração de 60 segundos)

```
!sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-plain-generic
```

```
!jupyter nbconvert --to pdf /content/KNN.ipynb
```

</details>

## Finalização

Há diversas outras possibilidades de se chegar ao mesmo resultado, desde mais simples até as mais complexas e também outras linguagens podem ser utilizadas. Como exposto na introdução, o objeto deste minicurso foi de fazer um apanhado geral de algumas possibilidades de manipulação de banco de dados que proporcionam dados mais legíveis e de fácil análise. Espero que a missão tenha sido cumprida.

Se gostou desse conteúdo, faça um Fork para deixar guardado no seu repositório do GitHub e deixe uma estrelinha, pra ele brilhar hehe

Contato:
angelicabicegof@gmail.com
Presente nas mídias como Angélica Bicego