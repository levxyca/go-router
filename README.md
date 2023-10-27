# GoRouter

[Projeto para explorar a navegação com o GoRouter no Flutter. 🚢](https://github.com/levxyca/go-router)

## **🤔 O que é?**

O GoRouter é uma biblioteca de navegação para o Flutter. No desenvolvimento de aplicativos, a navegação se refere à transição entre diferentes telas ou páginas. O GoRouter facilita a gestão dessa navegação, permitindo que os desenvolvedores controlem como e quando as transições entre telas ocorrem.

Ele opera em cima da estrutura de roteamento nativa do Flutter, adicionando uma camada de abstração para tornar o gerenciamento de rotas mais intuitivo e simplificado. Em vez de lidar diretamente com o roteamento e a navegação, os desenvolvedores podem usar o GoRouter para definir rotas e personalizar o comportamento de navegação.

O GoRouter oferece recursos como a capacidade de passar parâmetros entre telas, tratar rotas de maneira dinâmica e personalizar animações de transição. Ele também suporta a navegação para trás, permitindo que os usuários retornem à tela anterior.

## ✖ GoNamed vs PushNamed

### goNamed

- GoNamed no Flutter permite ir diretamente para uma rota nomeada em vez de percorrer todas as rotas intermediárias. Mas na hora de voltar, ele respeita a árvore de rotas e o contexto.

### pushNamed

- PushNamed no Flutter também me permite navegar para uma rota em específico, entretanto, eu empilho essa rota.

## 📒 Anotações

- A ideia do GoRouter é separar a navegação em árvores.
- Ele muda um pouco quando usamos a BottomNavigation, pois aí começamos a trabalhar com contextos de navegação também.
- Colocamos “/” no nome das rotas que são as top-level de cada contexto. Isso é obrigatório, caso contrário, teremos um erro.

## 🦴 Desmembrando o código

```dart
// Configuração necessária para usar o GoRouter
return MaterialApp.router(
    routerConfig: MobileRouter.router,
);
```

```dart
GoRoute(
    /// Obrigatório
    path: loginRoute,
    /// Vamos usar para trabalhar com a navegação nomeada
    name: loginRoute,
    /// Vai construir o que estiver aqui
    builder: (_, __) => const Login(),
    /// Uma lista de outras rotas
    routes: [
			///
    ],
  ),
)
```

```dart
GoRoute(
    path: profileRoute,
    name: profileRoute,
		/// Podemos usar o segundo parâmetro do builder para passar argumentos entre as telas.
    builder: (_, state) {
			/// Variável para receber o state usando o extra para passar os argumentos.
			/// Precisar usar o cast para converter o argumento para o tipo necessário.
			final arguments = state.extra as String;
			/// Passamos o argumento como parâmetro do construtor.
			const Profile(name: 'Leticia'),
		}
  ),
)
```

```dart
/// Com o pushNamed conseguimos realizar uma ação quando voltamos da tela.
/// O goNamed não tem isso, ele é void.
context.pushNamed('teste', extra: 1).then((value) => null);
```

## 🦴 BottomNavigation

```dart
			///Bottom Navigation
			/// O indexedStack fica no mobile router.
      StatefulShellRoute.indexedStack(
        builder: (_, __, navigationShell) {
					/// Constrói a bottomNavigation passando o navigationShell.
					/// Com ele vamos gerenciar a nossa bottomNavigation.
          return BottomNavigationFactory.bottomNavigation(navigationShell);
        },
        branches: [
					/// Cada StatefulShellBranch é uma aba da bottom.
          StatefulShellBranch(
            routes: [
              /// Home
              GoRoute(path: homeRoute, name: homeRoute, builder: (_, __) => const Home()),
            ],
          ),
        ],
      ),
```
