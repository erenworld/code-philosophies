# react-philosophies

## Table des matières

0. [Introduction](#-0-introduction)  
1. [Le strict minimum](#-1-le-strict-minimum)  
2. [Design pour le bonheur](#-2-concevoir-pour-le-bonheur)  
3. [Astuces de performance](#-3-astuces-de-performance)  
4. [Principes de test](#-4-principes-de-test)  
5. [Idées partagées par d'autres](#-5-idées-partagées-par-dautres)

<details>
    <summary>Comment ce document est organisé</summary>

<br/>
Il m’a été assez difficile de séparer mes réflexions en `design`, `performance` et `tests`. J’ai remarqué que beaucoup de conceptions pensées pour la maintenabilité rendent aussi votre application plus rapide et plus facile à tester. Désolé si la discussion semble parfois désorganisée.
<br/>

</details>

<details>
    <summary><strong>Merci pour tous les PR 🚜, les cafés ☕, les lectures recommandées 📚 et le partage d'idées 💡 (Voir les contributeurs)</strong></summary>

---

#### ❤️ Commentaires, suggestions, réactions vives ? J’aimerais les entendre !

Si vous pensez à quelque chose qui devrait faire partie de ma liste de lecture ou si vous avez de super idées à inclure ici, n’hésitez pas à soumettre un PR ou une issue. J’ai notamment inclus la section [`Idées partagées par d'autres`](#-5-idées-partagées-par-dautres) si vous souhaitez y ajouter vos propres idées 🙂. Les liens cassés, les fautes de grammaire, de mise en forme ou de typographie sont aussi les bienvenus. Toute contribution pour améliorer `react-philosophies`, petite ou grande, est toujours appréciée.

---

#### ❤️ Merci spécial à ceux qui ont pris le temps de contribuer !

_Note : la liste suivante n’est pas exhaustive. Si vous avez contribué à ce projet et que votre nom n’apparaît pas, n’hésitez pas à soumettre un PR pour l’ajouter ici. Merci !_

**💡 Commentaires et suggestions**

- La communauté [`r/reactjs`](https://www.reddit.com/r/reactjs/comments/pvwb6m/what_i_think_about_when_i_write_code_in_react)
- [Josh W Comeau](https://www.joshwcomeau.com/)
- [@unpunnyfuns](https://github.com/unpunnyfuns)
- [@cassidoo](https://github.com/cassidoo)

**☕ Café !**

- [Myles](https://github.com/myles-banner)
- [Daniel](https://Ko-fi.com/home/coffeeshop?txid=7d71404a-fa0c-419d-9808-46ea520c913f&mode=public&img=ogsomeoneboughtme)
- [Ankit](https://github.com/ankitwww)

**🚜 Pull Requests**

- [@fengzilong](https://github.com/fengzilong)
- [@ankitwww](https://github.com/ankitwww)
- [@dzakki](https://github.com/dzakki)
- [@metonym](https://github.com/metonym)
- [@sapegin](https://github.com/sapegin)

**📚 Lectures recommandées**

- [ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript), [3rs-of-software-architecture](https://github.com/ryanmcdermott/3rs-of-software-architecture), [ryanmcdermott/code-review-tips](https://github.com/ryanmcdermott/code-review-tips)
- [Ben Moseley et Peter Marks : Out of the Tar Pit (2006)](http://curtclifton.net/papers/MoseleyMarks06a.pdf), recommandé par [@icyjoseph](https://github.com/icyjoseph)
- [`goldbergyoni/nodebestpractices`](https://github.com/goldbergyoni/nodebestpractices), recommandé par [@rstacruz](https://github.com/rstacruz)
- [Dan Abramov : Writing Resilient Components](https://overreacted.io/writing-resilient-components/), recommandé par [Mon Quindoza](https://ph.linkedin.com/in/monquindoza)
- [Matthieu Kern : Stop checking if your component is mounted](https://medium.com/doctolib/react-stop-checking-if-your-component-is-mounted-3bb2568a4934), recommandé par [@Pierre-CLIND](https://github.com/Pierre-CLIND)

</details>

## 🧘 0. Introduction
`react-philosophies`, c’est :

- les choses auxquelles je pense quand j’écris du code `React`.
- en arrière-plan dans mon esprit lorsque je relis le code de quelqu’un d’autre ou le mien
- juste des lignes directrices, et NON des règles strictes
- un document vivant qui évoluera avec le temps à mesure que mon expérience grandit
- principalement des techniques qui sont des variantes de méthodes de [refactoring](https://fr.wikipedia.org/wiki/Remaniement_de_code), de principes [SOLID](https://fr.wikipedia.org/wiki/SOLID_(informatique)) et d’idées issues de la [programmation extrême](https://fr.wikipedia.org/wiki/Programmation_extr%C3%AAme)... simplement appliquées spécifiquement à `React` 🙂

`react-philosophies` s'inspire de différentes sources que j’ai croisées à divers moments de mon parcours de développement.

En voici quelques-unes :

- [Sandi Metz](https://sandimetz.com/)
- [Kent C Dodds](https://kentcdodds.com)
- [Zen of Python (PEP 20)](https://www.python.org/dev/peps/pep-0020/), [Zen of Go](https://dave.cheney.net/2020/02/23/the-zen-of-go)
- [trekhleb/state-of-the-art-shitcode](https://github.com/trekhleb/state-of-the-art-shitcode), [droogans/unmaintainable-code](https://github.com/Droogans/unmaintainable-code), [sapegin/washingcode-book](https://github.com/sapegin/washingcode-book/)

> En tant que développeur expérimenté, j’ai certaines habitudes, opinions et schémas que j’ai tendance à suivre. Devoir expliquer à quelqu’un pourquoi j’aborde un problème d’une certaine manière m’aide vraiment à briser mes mauvaises habitudes, à remettre en question mes présupposés ou à valider mes bonnes compétences en résolution de problèmes. - [Coraline Ada Ehmke](https://where.coraline.codes)

## 🧘 1. Le strict minimum

### 1.1 Reconnaître quand l’ordinateur est plus malin que vous

1. Analysez statiquement votre code avec [`ESLint`](https://eslint.org/). Activez la règle [`rule-of-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) ainsi que la règle `exhaustive-deps` pour détecter les erreurs spécifiques à `React`.
2. Activez le ["strict mode"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode). On est en 2022.
3. [Soyez honnête à propos de vos dépendances](https://overreacted.io/a-complete-guide-to-useeffect/#two-ways-to-be-honest-about-dependencies). Corrigez les avertissements/erreurs `exhaustive-deps` dans vos `useMemo`, `useCallback` et `useEffect`. Vous pouvez essayer ["The latest ref pattern"](https://epicreact.dev/the-latest-ref-pattern-in-react) pour garder vos callbacks à jour sans rerenders inutiles.
4. [Ajoutez toujours des clés](https://epicreact.dev/why-react-needs-a-key-prop) quand vous utilisez `map` pour afficher des composants.
5. [N’appelez les hooks qu’au niveau supérieur](https://reactjs.org/docs/hooks-rules.html). N’appelez pas de hooks dans des boucles, des conditions ou des fonctions imbriquées.
6. Comprenez l’avertissement "Can't perform state update on unmounted component". [facebook/react/pull/22114](https://github.com/facebook/react/pull/22114)
7. Évitez l’[“écran blanc de la mort”](https://kentcdodds.com/blog/use-react-error-boundary-to-handle-errors-in-react) en ajoutant plusieurs [error boundaries](https://reactjs.org/docs/error-boundaries.html) à différents niveaux de votre application. Vous pouvez aussi les utiliser pour envoyer des alertes à un service de monitoring comme [Sentry](https://sentry.io) si vous le souhaitez. ([Accounting for Failures In React](https://brandondail.com/posts/fault-tolerance-react))
8. Il y a une raison pour laquelle les erreurs et avertissements s’affichent dans la console.
9. N’oubliez pas le [`tree-shaking`](https://webpack.js.org/guides/tree-shaking/) !
10. [Prettier](https://prettier.io/) (ou une alternative) formate votre code automatiquement, assurant une mise en forme cohérente à chaque fois. Vous n’avez plus à y penser !
11. [`Typescript`](https://www.typescriptlang.org/) et des frameworks comme [`NextJS`](https://nextjs.org/) vous simplifient énormément la vie.
12. Je recommande vivement [Code Climate](https://codeclimate.com/quality/) (ou un équivalent) pour les dépôts open-source ou si vous avez le budget. Je trouve que les "code smells" détectés automatiquement me motivent vraiment à réduire la dette technique de l’application sur laquelle je travaille !

### 1.2 Le code est une douleur supplémentaire

> "Le meilleur code est celui qu’on n’écrit pas. Chaque ligne de code que vous introduisez volontairement dans le monde est une ligne qui devra être déboguée, lue, comprise et maintenue." - Jeff Atwood

> "L’un de mes jours les plus productifs a été celui où j’ai supprimé 1000 lignes de code." - Eric S. Raymond

Voir aussi : [Write Less Code - Rich Harris](https://svelte.dev/blog/write-less-code), [Code is evil - Artem Sapegin](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

#### 1.2.1 Réfléchir avant d’ajouter une dépendance

Inutile de rappeler que plus vous ajoutez de dépendances, plus vous envoyez de code au navigateur. Posez-vous la question : utilisez-vous réellement les fonctionnalités qui rendent cette bibliothèque intéressante ?

<details>
    <summary><strong><em>🙈 En avez-vous vraiment besoin ?</strong> Voir des exemples de dépendances / de code dont vous pourriez vous passer</em></summary>

<br/>

1. Avez-vous vraiment besoin de [`Redux`](https://redux.js.org/) ? C’est possible. Mais gardez en tête que React est déjà une [bibliothèque de gestion d’état](https://kentcdodds.com/blog/application-state-management-with-react).

2. Avez-vous vraiment besoin du [`Apollo client`](https://www.apollographql.com/docs/react/) ? Il offre beaucoup de fonctionnalités puissantes, comme la normalisation manuelle. Mais il augmentera fortement la taille de votre bundle. Si votre application n’utilise pas ses fonctionnalités avancées, envisagez une alternative plus légère comme [`react-query`](https://react-query.tanstack.com/comparison) ou [`SWR`](https://github.com/vercel/swr) (ou aucune).

3. [`Axios`](https://github.com/axios/axios) ? C’est une excellente bibliothèque avec des fonctionnalités difficilement réplicables avec `fetch`. Mais si la seule raison de l’utiliser est une API plus agréable, envisagez un simple wrapper autour de fetch (comme [`redaxios`](https://github.com/developit/redaxios) ou le vôtre). Demandez-vous si vous exploitez vraiment ses fonctionnalités uniques.

4. [`Decimal.js`](https://github.com/MikeMcl/decimal.js/) ? Peut-être que [Big.js](https://github.com/MikeMcl/big.js/) ou [d'autres bibliothèques plus légères](https://www.npmtrends.com/big.js-vs-bignumber.js-vs-decimal.js-vs-mathjs) suffisent.

5. [`Lodash`](https://lodash.com/) / [`UnderscoreJS`](https://underscorejs.org/) ? [you-dont-need/You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore)

6. [`MomentJS`](https://momentjs.com/) ? [you-dont-need/You-Dont-Need-Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs)

7. Vous n’avez peut-être pas besoin de `Context` pour le thème (`clair`/`sombre`) : envisagez plutôt l’utilisation de [`variables CSS`](https://epicreact.dev/css-variables).

8. Vous n’avez peut-être même pas besoin de `Javascript`. Le CSS est puissant. [you-dont-need/You-Dont-Need-JavaScript](https://github.com/you-dont-need/You-Dont-Need-JavaScript)

<br/>

</details>

