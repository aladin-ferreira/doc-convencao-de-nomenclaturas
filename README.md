
# Convenção de Nomenclaturas: Boas Práticas para Nomear Variáveis, Funções e Classes

Este documento é um guia de referência para boas práticas ao nomear suas variáveis, classes e funções no seu código.
Ter uma boa convenção de nomenclatura para suas variáveis, funções e classes é uma peça importante para o desenvolvimento de software, e ter essa habilidade afiada no seu _skillset_, vão te fazer um programador 3x melhor.


## Qual a importância de saber nomear bem o seu código? 

Aprender sobre um boa convenção de nomenclatura, é uma parte essencial para ter um código mais legível e entendível, facilitando a manutenção e colaboração no seu código. Fazer uma boa escolha na hora de nomear, é um fator importante e que facilmente pode diferenciar um código bom de um código ruim. Quer ver um exemplo?

#### Você consegue adivinhar o que essa função faz? 🤔

```kotlin
fun setValue(value: Int)
```

Essa função lógicamente atribui um valor a algo, mas *a o quê?*

Você como criador do código, provavelmente saberia exatamente do que essa função  ```setValue()``` se trata, mas muito provavelmente alguém que não esteja por dentro do escopo do seu projeto, **não saberia**.

É importante manter em mente de que em algum momento, o seu código será revisado por alguém ou outra pessoa precisará dar manutenção ao seu script no futuro. Quando alguém não está por dentro do contexto do projeto, é bem mais dificil tentar decifrar o que ```setValue()``` faz.

#### 📌 Dicas: 

Uma dica para saber se o nome da sua função está bom, é fazer as seguintes perguntas para você mesmo:\
**_daqui a uma semana, eu vou saber o que essa função faz só de ler o nome dela?_**\
ou\
**_se uma pessoa "leiga" ler essa função, ela teria uma ideia do que a função faz, ou ficaria boiando? 🤔_**

Isso vai te ajudar a refletir, e é um bom guia mental para te ajudar com a convenção de nomenclatura.



## ✅ Nomes bons vs Nomes ruins

Já foi discutido que ```setValue()``` definitivamente não seria um bom nome para sua função, _mas qual seria o nome mais adequado?_\
A jogada de mestre é evitar os nomes genéricos, e utilizar nomes mais específicos e que auto-expliquem a sua função. 

### Exemplo:

Vamos supor que a sua função seja responsável por _settar_ um valor de saldo bancário do usuário.\
Então, em vez de nomear como: 
```kotlin
fun setValue(value: Int)
```
Você deveria fazer algo como:
```kotlin 
fun setUserAccountBalance(value: Int)
```
Percebeu que mesmo sem estar tão por dentro do escopo do projeto, praticamente qualquer um entenderia o que essa função faz?\
Isso faz toda diferença, pois independentemente do conteúdo da sua função, qualquer pessoa consegue ao menos ter uma ideia do que a função faz, facilitando muito uma possível manutenção.

### **Importante**❗️

Não se preocupe com nomes grandes demais, eles **na maioria** dos casos são realmente mais descritivos, porém tenha cuidado com funções como   ```setUserAccountBalanceAndUpdateUserData()``` pois este tipo de função fere os princípios da responsabilidade única.

_(lembrando que não é interessante utilizar tipos Int ou Double para lidar com valores monetários. para mais informações acesse esta documentação aqui)_


### O mesmo vale para suas variáveis e classes!

As suas variáveis precisam ser descritivas e auto-explicativas, elas deveriam *literalmente* descrever a sua entidade. Seria o caso de você bater o olho, e saber exatamente do que tal coisa se trata.\
Por exemplo:
```kotlin
var x = 10
//nome ruim! não dá pra saber o que x representa
```
o snippet acima, é um exemplo de nome ruim. O ideal seria você bater o olho na variável e já saber do que ela se trata, e neste exemplo, isso é praticamente impossível. X poderia ser literalmente qualquer coisa, e seria necessário gastar umas boas horas tentando adivinhar o seu significado pelo contexto do código inteiro. 

```kotlin
var userAge = 10
//nome bom! sabemos exatamente do que se trata
```

**reparou que agora é fácil saber que essa variável representa a idade do usuário?**\
e este realmente é o intuito, saber do que algo se trata apenas batendo o olho, ou você gostaria de perder tempo tendo que ler e reler o código 10x para efetivamente entendê-lo? eu acredito que não.

### Como em qualquer cenário, esse também tem a sua excessão 👍

Foi dito anteriormente que o ideal seria evitar nomes genéricos e utilizar o máximo possível nomes específicos, mas analise esse caso: 

```kotlin
for(i in 0..10) {
    println("count: $i")
}
```
a variável foi nomeada apenas com um "i", e está tudo bem, mas por quê?\
A resposta para essa pergunta é muito simples: _você consegue saber **exatamente** o que esse código faz!_\
Esse trecho de código é comumente utilizado pela comunidade dev, logo qualquer um (com um mínimo de noção em desenvolvimento) consegue saber o que ele faz. 

outros exemplos:

```kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
// k, v são totalmente compreensíveis como chave e valor, pois estamos lidando diretamente com um map
```

```kotlin
val names = listOf("Barry", "Allen")
val upperNames = names.map { it.uppercase() }
//it é implícito e muito usado em lambdas simples (todo mundo entende)
```

Esses nomes curtos funcionam quando a intenção é óbvia pelo contexto. Em código complexo, sempre prefira nomes mais descritivos.

## Como Nomear no Cenário do Android?

Todos os tópicos abordados e discutidos servem para qualquer projeto, mas o desenvolvimento Android traz componentes específicos (como Activities, Fragments, ViewModels, Repositories, etc.) que exigem padronizações adicionais para manter a clareza, escalabilidade e consistência do código.
A seguir, definimos convenções voltadas exclusivamente ao ecossistema Android.

### 🧠 Erro mais comum: ViewModel ≠ Repository

É comum vermos casos onde as funções do ```ViewModel``` têm exatamente o mesmo nome que as funções do ```Repository```

```kotlin
//Repository 
fun getUser(id: Int): Flow<User>

//ViewModel
fun getUser(id: Int) {
    viewModelScope.launch {
        repository.getUser(id)
    }
}
```

Não necessariamente está errado, mas é uma boa prática diferenciar os nomes das funções de cada um, pois o ```ViewModel``` e o ```Repository``` tem **responsabilidades diferentes**.
## ✅ Guia Prático

📦 Repository: nomes mais diretos e descritivos da fonte de dados\
Foco: o que ele faz com os dados

🎯 ViewModel: nomes mais intencionais, voltados à UI ou ações\
Foco: intenção da tela / caso de uso

```kotlin
// Repository
fun getUser(id: Int): Flow<User>

// ViewModel
fun loadUserData(id: String) {
    viewModelScope.launch {
        repository.getUser(id)
    }
}
```
O mesmo serve para quando o ```Repository``` faz ações de POST/PUT/DELETE, a nomenclatura ainda segue o princípio de descrever claramente o que está sendo feito com os dados.

Use verbos como:
- ```send```
- ```post```
- ```submit```
- ```update```
- ```delete```
- ```save```

```kotlin
// Repository
suspend fun submitFeedback(feedback: Feedback)
suspend fun updateUserProfile(profile: Profile)
suspend fun deleteCartItem(itemId: String)

// ViewModel
fun onFeedbackSubmitted(feedback: Feedback) {
    viewModelScope.launch {
        repository.submitFeedback(feedback)
    }
}

fun confirmProfileUpdate(profile: Profile) {
    viewModelScope.launch {
        repository.updateUserProfile(profile)
    }
}
```

### 📌 Dica:
Pense no ViewModel como um intermediador entre a UI e os dados. O nome das funções dele devem refletir as ações da tela.

Em resumo:\
```Repository```: descreve o que acontece com os dados → ```submitFeedback```, ```sendOrder```, ```deleteItem```.\
```ViewModel```: descreve o que o usuário ou a tela está fazendo → ```onFeedbackSubmitted```, ```confirmOrder```, ```removeItemFromCart```.

## Na View:

O mesmo se aplica a camada de visualização do projeto (Fragment, Activities, Adapters), use nomes relacionados à ação visual ou de interação do usuário: 

 ```kotlin
 //exemplo ruim
fun fetchUser() // dentro de uma Activity

//é melhor usar
fun setupUserUi()
fun observeUser()
```

### 🥇 Regra de ouro
Nomeie com base na responsabilidade.\
View → **"o que mostrar"**\
ViewModel → **"o que executar"**\
Repository → **"o que buscar ou enviar"**

Abaixo, está uma tabela com boas práticas de **convenção de nomenclatura** para cada camada do Android
## Convenção de Nomes por Camada

| Camada       | Responsabilidade                           | Prefixos/Sufixos comuns                    | Exemplo de Funções                                      |
|--------------|--------------------------------------------|--------------------------------------------|---------------------------------------------------------|
| `View`       | Exibir dados e interações do usuário       | `setup`, `observe`, `show`, `navigateTo`   | `setupUserUi()`, `observeLoginState()`, `showError()`, `navigateToHome()` |
| `ViewModel`  | Lógica de UI, orquestrar ações             | `perform`, `load`, `handle`, `onX`, `fetchUiState` | `performLogin()`, `loadUserProfile()`, `handleSuccess()`, `onRetryClick()` |
| `Repository` | Comunicação com fontes de dados (API, DB)  | `get`, `fetch`, `send`, `update`, `create` | `getUserFromRemote()`, `fetchProfile()`, `sendLoginRequest()`, `updateUserData()` |
| `DataSource` | Acesso direto a API/DB                     | `apiCall`, `query`, `insert`, `post`       | `queryUserById()`, `insertNewUser()`, `postUserData()`, `apiCallLogin()` |


## Considerações Finais

Seguir convenções de nomenclatura claras e consistentes é essencial para garantir legibilidade, manutenção e colaboração eficiente em projetos Android. Ao nomear classes, funções e variáveis de acordo com a responsabilidade de cada camada, você facilita a compreensão do código e reduz a chance de ambiguidade.

Essa documentação serve como um guia de referência para mantermos um padrão comum dentro do time. Caso novas necessidades surjam ou padrões evoluam, este documento pode (e deve) ser atualizado para refletir as melhores práticas adotadas pelo time.

**Escrevemos código para pessoas lerem, e só depois para máquinas executarem.**

