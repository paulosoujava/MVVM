# MVVM
O padrão de projeto Model-View-ViewModel (MVVM) foi originalmente criado para aplicativos Windows Presentation Foundation (WPF) usando XAML para separar a interface do usuário (UI) da lógica de negócios e aproveitando ao máximo o data binding (a vinculação de dados).

Aplicações arquitetadas desta forma têm uma camada ViewModel distinta que não possui dependências de sua interface de usuário.

Esta arquitetura em si é otimizada para testes de unidade, bem como para o desenvolvimento multiplataforma.

Como as classes ViewModel de um aplicativo não têm dependências sobre a camada de interface do usuário, você pode facilmente trocar uma interface de usuário iOS por uma interface Android e escrever testes contra a camada ViewModel.
 
O padrão MVVM é composto basicamente dos seguintes elementos:

Model: A camada de modelo é a lógica de negócios que impulsiona a aplicação e quaisquer objetos de negócios;

View: Esta camada é a interface do usuário. No caso do desenvolvimento cross plataform, ela inclui qualquer código específico da plataforma para conduzir a interface do usuário da aplicação.

ViewModel: Esta camada age como a cola em aplicações MVVM. As camadas ViewModel coordenam as operações entre a view e as camadas model. Uma camada ViewModel irá conter propriedades que a View vai obter ou definir, e funções para cada operação que pode ser feita pelo usuário em cada view. A camada ViewModel também evocará operações sobre a camada Model, se necessário.

A figura abaixo mostra um esquema do padrão Model-View-ViewModel :
[![Android](http://www.macoratti.net/16/09/net_mvvm11.png)](https://github.com/paulosoujava/eyemobile/tree/master/app)




É importante notar que a interação entre as camadas View e ViewModel é  tradicionalmente criada pela ligação de dados ou databinding.

No entanto, o iOS e o Android não possuem um mecanismos de vinculação de dados embutidos, por isso a abordagem geral neste caso é feita manualmente chamando a camada ViewModel da camada View.

# LIVEDATA
[![Android](https://github.com/paulosoujava/MVVM/blob/master/image/Captura%20de%20Tela%202020-05-06%20%C3%A0s%2013.27.16.png)](https://github.com/paulosoujava/eyemobile/tree/master/app)


[![Android](https://github.com/paulosoujava/MVVM/blob/master/image/Captura%20de%20Tela%202020-05-06%20%C3%A0s%2013.53.12.png)](https://github.com/paulosoujava/eyemobile/tree/master/app)

Data Binding Library   
Parte do Android Jetpack.
A Data Binding Library é uma biblioteca de apoio que permite vincular componentes de IU dos seus layouts a fontes de dados do app usando um formato declarativo, em vez de programático.
Os layouts geralmente são definidos em atividades com código que chama métodos de framework da IU. Por exemplo, o código abaixo chama findViewById() para localizar um widget TextView e vinculá-lo à propriedade userName da variável viewModel


O pacote androidx.lifecycle fornece classes e interfaces que permitem criar componentes com reconhecimento de ciclo de vida, que são aqueles que podem ajustar automaticamente o próprio comportamento com base no estado atual do ciclo de vida de uma atividade ou um fragmento.

https://developer.android.com/topic/libraries/architecture/lifecycle


LiveData é uma classe armazenadora de dados observáveis. Diferente de um observável comum, o LiveData conta com reconhecimento de ciclo de vida, ou seja, ele respeita o ciclo de vida de outros componentes do app, como atividades, fragmentos ou serviços. Esse reconhecimento garante que o LiveData atualize apenas os observadores de componente do app que estão em um estado ativo no ciclo de vida.

https://developer.android.com/topic/libraries/architecture/livedata

Room
A biblioteca de persistência Room oferece uma camada de abstração sobre o SQLite para permitir um acesso mais robusto ao banco de dados, aproveitando toda a capacidade do SQLite.
A biblioteca ajuda você a criar um cache dos dados do seu app no dispositivo que o executa. Esse cache, que funciona como a única fonte da verdade do seu app, permite que os usuários vejam uma cópia consistente das informações importantes no app, independentemente dos usuários terem uma conexão de Internet.

FONTE:

https://developer.android.com/topic/libraries/architecture/room

ViewModel
A classe ViewModel foi projetada para armazenar e gerenciar dados relacionados à IU considerando o ciclo de vida. A classe ViewModel permite que os dados sobrevivam às mudanças de configuração, como a rotação da tela.
Observação: para importar o ViewModel para seu projeto Android, consulte as instruções de declaração de dependências nas notas da versão do Lifecycle.
O framework do Android gerencia os ciclos de vida dos controladores de IU, como atividades e fragmentos. O framework pode decidir destruir ou recriar um controlador de IU em resposta a determinadas ações do usuário ou eventos do dispositivo que estão completamente fora do seu controle.
Se o sistema destruir ou recriar um controlador de IU, todos os dados temporários relacionados à IU armazenados nele serão perdidos. Por exemplo, seu app pode incluir uma lista de usuários em uma das atividades dele. Quando a atividade for recriada para uma mudança de configuração, a nova atividade precisará buscar novamente a lista de usuários. Para dados simples, a atividade pode usar o método onSaveInstanceState() e restaurar os próprios dados a partir do pacote em onCreate(), mas essa abordagem é adequada apenas para pequenos volumes de dados que podem ser serializados e depois desserializados, não para volumes potencialmente grandes de dados. como uma lista de usuários ou bitmaps.
Outro problema é que os controladores de IU geralmente precisam fazer chamadas assíncronas que podem levar algum tempo para retornar. O controlador de IU precisa gerenciar essas chamadas e garantir que o sistema as limpe depois de ser destruído, para evitar possíveis vazamentos de memória. Esse gerenciamento requer muita manutenção e, caso o objeto seja recriado para uma mudança de configuração, representa um desperdício de recursos, porque o objeto pode precisar emitir novamente as chamadas já feitas.
Os controladores de IU, como atividades e fragmentos, têm como objetivo principal exibir dados da IU, reagir às ações do usuário ou lidar com a comunicação do sistema operacional, como solicitações de permissão. A exigência de que os controladores de IU também sejam responsáveis pelo carregamento de dados de um banco de dados ou de uma rede acaba tornando a classe pesada. Atribuir responsabilidades excessivas aos controladores de IU pode fazer com que uma única classe precise lidar sozinha com todo o trabalho de um app, em vez de delegar o trabalho para outras classes. Atribuir responsabilidades excessivas aos controladores de IU dessa maneira também dificulta muito os testes.
É mais fácil e eficiente separar a propriedade de dados de visualização da lógica do controlador de IU.

FONTE:

https://developer.android.com/topic/libraries/architecture/viewmodel

