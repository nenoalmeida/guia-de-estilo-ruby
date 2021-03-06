# Guia de estilo Ruby


	Guia para escrever códigos Ruby mais legíveis e limpos

	Tradução livre de acordo com a minha interpretação sobre o assunto

Originalmente postado [aqui](http://praxis.scholarslab.org/scratchpad/ruby-style-guide/)


##Guia de estilo


* Use espaços entre operadores, e pontos de interrogação ('{', '}') depois de virgulas e ponto e virgula

```sh
sum = 1 + 2
a, b = 1, 2
1 > 2 ? true : false; puts "hi"
[1, 2, 3].each { |e| puts e }
```

* Não use espaço depois de '(', ou entre parentesis ('[', ']').

```sh
some(arg).other
[1, 2, 3].length

* Identar o resultado do termo "when" 

when song.name == 'Tik Tok'
  puts "Not again!"
when song.duration > 120
  puts "That's really long"
when Time.now.hour > 21
  puts "It's time to start coding"
else
  song.play
end

epoch = case year
        when 1607..1777 then "Colonial Period"
        when 1778..1812 then "Early Republic"

* Use uma linha vazia depois de terornar o valor de um metodo
(a menos que seja apenas uma linha) e uma linha entre as declarações "def".      
        
    def some_method
  do_something
  do_something_else

  result
end

def do_something
  result
end
```

> Use RDoc como uma convenção da documentação (SDoc pode ser usado para gerar melhor mecanismo de busca na documentação).
> Use uma linha vazia para quebrar o metodo para um paragrafo logico
> Mantenha linhas abaixo de 80 caracteres

# Sintaxe

> use o def entre pasentesis quando houver argumentos. Omita os parenteses quando o metodo nao aceitar nenhum argumento

```sh
def some_method
  > payload
end
```

```sh
def method_with_arguments(arg1, arg2)
  > payload
end

```
> Nunca use "for", a menos que voce saiba exatamente o porque. Iteradores devem ser usados em seu lugar
arr = [1, 2, 3]

```sh
> errado
for elem in arr do
  puts elem
end
```
```sh
> correto
array.each { |elem| puts elem }
```
> nunca use-o para multiplas linhas if/unless

```sh
> errado
if some_condition then
  # payload
end

> correto
if some_condition
  # payload
end
```

>De preferencia aos seus operadores de construção ternaria no lugar de if/then/else/end.  É mais comum e conciso.

```sh
> errado
result = if some_condition then something else something_else end

> correto
result = some_condition ? something : something_else

> Use apenas uma expressão de operador ternario por branch. Isso significa que o operador ternario precisa estar anunhado. Prefira 
construçoes if/else neses casos.

> errado
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

> correto
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```
> Utilize && e || para expressoes booleanas. Use and ou for para o controle de fluxo

> expressão booleana
if some_condition && some_other_condition
  do_something
end

> fluxo de controle
document.saved? or document.save!

> Evite operadores ternarios de multiplas linas, use if/unless no lugar deles.
> De preferencia por modificar o uso de if/unless quando voce tiver uma linha apenas

```sh
> errado
if some_condition
  do_something
end

> correto
do_something if some_condition

> outra boa opção
some_condition and do_something
> De preferencia para o uso do if para conditionais negativas (ou a conditional or)
```


> Inibir parentesis superfulos quando chamamos os metodos, mas mante-lo quando chamamod "funçoes", i.e. Quando voce usa o retorno do valor 
na mesma linha

```sh
x = Math.sin(y)
array.delete e
```

> Prefira {...} no lugar de do...end em blocos de uma linha. Evite usar {...} para blocos de multiplas linhas.
Sempre use do...end para "controlar o fluxo" e "definir o metodo" (e.g no Rakefiles e certos DSLs.) Evite do...end quando estiver encadeando

> Evite "return" onde não for requisitado.

```sh
> errado
def some_method(some_arr)
  return some_arr.size
end

> correto
def some_method(some_arr)
  some_arr.size
end
```
> Evite  linha coninua (\) onde nao requisitado. Na pratica, evite o uso de linha continua como um todo.

```sh
> errado
result = 1 - \
         2

> correto (mais ainda tá muito feio)
result = 1 \
         - 2

> Use o retorno de valor = esta correto

if v = array.grep(/foo/) ...
Use ||= freely.

> set name to Bozhidar, only if it's nil or false
name ||= "Bozhidar"
```

> Evite o uso do estilo Perl em especial nas variaveis ( como $0-9, $, ...).
> A anotação de tecldo que é seguida por dois pointos e espaço, é entao uma nota que descreve um pronlema

> Se multiplas linhas forem requisitadas para descrever um problema, as linhas subsequentes deves ser identadas com 2 espaços
> apos o #

```sh
 def bar
   FIXME: This has crashed occasionally since v3.2.1. It may
     be related to the BarBazUtil upgrade.
  baz(:quux)
end


> Nos casos onde o problema é tao óbvio que a documentação poderia ser redundante, anotaçoes podem 
>ser feitas a esquerda da linha sem nota. Este jeito deve ser uma exceção a regra

def bar
  sleep 100 - OPTIMIZE
end
```

> Use TODO para notas de features perdidas ou funcionalidades que deveriam ser adicionadas depois da data

> Use FiXME para notas quebradas de código que precisam ser refeitas

> Use OPTIMIZE para nominar codigos lentos ou ineficientes que podem causar problemas de performance.

> Use HACK para nominar codigos que foram usados com praticas questionaveis e deveriam ser refatorados. 

> Use REVIEW para nominar tudo que deveria ser visto para confirmar sua intenção de trabalho. Por exemplo

> REVIEW: Are we sure this is how the client does X currently?

> Use outra anotação customizada se achar apropriado, mas tenha certeza de documenta-los em seu projeto no README ou similar.

