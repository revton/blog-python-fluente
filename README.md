# blog-python-fluente
Blog sobre a leitura do Livro Python Fluente, Segunda Edição (2023) por Luciano Ramalho, que se encontra no link https://pythonfluente.com

Irei me guiar pelos capítulos para ir escrevendo.

## Índice
- [Modelo dos dados](#modelo-dos-dados)
    - [Coleções em Python](#coleções-em-python)
    - [Acessando Atributos](#acessando-atributos)

## [Modelo dos dados](#modelo-dos-dados)

Adentrar o universo Python é descobrir um ecossistema rico em funcionalidades, com uma sintaxe elegante e intuitiva. Este artigo se propõe a ser um mergulho profundo nesse universo, explorando desde as coleções até os meandros da programação assíncrona.

### [Coleções em Python](#coleções-em-python)

As coleções no Python são um conjunto robusto de tipos de dados que facilitam o armazenamento e a manipulação de conjuntos de valores. Vamos explorar algumas das principais coleções:

- **Listas**: São coleções ordenadas e mutáveis que podem conter itens de diferentes tipos.
````python
minha_lista = [1, 2, 3, "Python", [4, 5]]
````

- **Tuplas**: Semelhantes às listas, mas imutáveis.
````python
minha_tupla = (1, 2, 3, "Imutável")
````

- Dicionários: Estruturas de dados que armazenam pares chave-valor.
````python
meu_dicionario = {"chave": "valor", "nome": "Revton", "idade": 33}
````

- Conjuntos: Coleções desordenadas de itens únicos.
````python
meu_conjunto = {1, 2, 2, 3, 4}
````

Cada um desses tipos de coleção tem seus próprios métodos e propriedades, permitindo manipulá-los de maneiras específicas, dependendo das necessidades do seu programa.

### [Acessando Atributos](#acessando-atributos)

Em Python, os atributos de um objeto podem ser acessados de várias maneiras. Aqui estão algumas das formas comuns:

#### 1. Acesso Direto:

Você pode acessar os atributos diretamente usando o nome do atributo, se o atributo não for privado.
````python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

# Acessando e modificando atributos:
pessoa = Pessoa("Revton", 30)
print(pessoa.nome)  # Saída: Revton
pessoa.nome = "João"
print(pessoa.nome)  # Saída: João
````

#### 2. Acesso por Métodos:

Para atributos privados (aqueles que começam com `_` ou `__`), é uma prática comum usar métodos getter e setter para acessar e modificar esses atributos.
````python
class MinhaClasse:
    def __init__(self):
        self.__atributo_privado = "Olá"

    def get_atributo(self):
        return self.__atributo_privado

    def set_atributo(self, valor):
        self.__atributo_privado = valor

# Acessando e modificando atributos:
obj = MinhaClasse()
print(obj.get_atributo())  # Saída: Olá
obj.set_atributo("Oi")
print(obj.get_atributo())  # Saída: Oi
````

#### 3. Acesso pelo Nome do Atributo:

Você pode acessar os atributos de um objeto dinamicamente usando a função `getattr`.
````python
class MinhaClasse:
    def __init__(self):
        self.atributo = "Olá"

# Acessando o atributo:
obj = MinhaClasse()
print(getattr(obj, "atributo"))  # Saída: Olá
````

#### 4. Acesso via Atributos de Dicionário:

Os atributos de um objeto também podem ser acessados como um dicionário, usando o `__dict__`.
````python
class MinhaClasse:
    def __init__(self):
        self.atributo = "Olá"

# Acessando o atributo:
obj = MinhaClasse()
print(obj.__dict__["atributo"])  # Saída: Olá
````

#### 5. Acesso Personalizado com Métodos Especiais:

Python oferece métodos especiais que permitem personalizar o acesso, atribuição e deleção de atributos.
````python
class PessoaCustomizada:
    def __init__(self):
        self.__dict__['_data'] = {}

    def __getattr__(self, nome):
        return self._data.get(nome, f"Atributo {nome} não encontrado")
    
    def __setattr__(self, nome, valor):
        if nome not in ['nome', 'idade']:
            raise AttributeError(f"Atributo {nome} não permitido")
        self._data[nome] = valor
    
    def __delattr__(self, nome):
        if nome in self._data:
            del self._data[nome]

pessoa_c = PessoaCustomizada()
pessoa_c.nome = "Revton"
print(pessoa_c.nome)  # Saída: Revton
del pessoa_c.nome
print(pessoa_c.nome)  # Saída: Atributo nome não encontrado
````
Aqui, no construtor `__init__`, usamos `self.__dict__['_data']` para contornar o nosso próprio método `__setattr__` personalizado e inicializar diretamente o dicionário interno `_data`.

### Iteração

Existem várias formas de iterar sobre coleções ou iteráveis em Python, incluindo a iteração assíncrona. Aqui estão algumas delas:

#### 1. Iteração com for:

Você pode usar um loop `for` para iterar sobre uma coleção ou iterável.
````python
lista = [1, 2, 3, 4]
for item in lista:
    print(item)
````

#### 2. Iteração com while:

Usar um loop `while` com um iterador e o método `next()` para iterar manualmente.
````python
lista = [1, 2, 3, 4]
iterador = iter(lista)
while True:
    try:
        item = next(iterador)
        print(item)
    except StopIteration:
        break
````

#### 3. Iteração com Comprensões de Lista(List Comprehension):

Compreensões de lista fornece uma maneira concisa de criar uma lista.
````python
lista = [1, 2, 3, 4]
[print(item) for item in lista]
````

#### 4. Iteração com função map:

A função `map` aplica uma função para cada item da lista
````python
lista = [1, 2, 3, 4]
def exibir(item):
    print(item)

list(map(exibir, lista))
````

#### 5. Iteração Assíncrona com async for:

A iteração assíncrona pode ser realizada com `async for` em conjuntos de dados assíncronos, como objetos async generator.
````python
import asyncio

async def async_generator():
    for i in range(5):
        await asyncio.sleep(1)
        yield i

async def main():
    async for item in async_generator():
        print(item)

await main()
````

Estes são alguns métodos comuns para realizar iterações em Python, incluindo a iteração assíncrona que é especialmente útil em programação assíncrona para evitar o bloqueio enquanto aguarda por operações de E/S ou outras operações assíncronas.