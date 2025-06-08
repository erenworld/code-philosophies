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

### 1.2.2 Ne soyez pas trop malin. YAGNI !

« Que pourrait-il arriver à mon logiciel dans le futur ? Oh oui, peut-être ceci ou cela. Autant tout implémenter maintenant tant qu’on travaille sur cette partie. Comme ça, ce sera à l’épreuve du futur. »

**You Aren’t Gonna Need It (YAGNI)** — Vous n’en aurez pas besoin ! Implémentez toujours les choses quand vous en avez *réellement* besoin, jamais juste parce que vous *pensez* en avoir besoin un jour. Moins il y a de code, mieux c’est !  
(Martin Fowler : YAGNI, C2 Wiki : [You Aren’t Gonna Need It](https://wiki.c2.com/?YouArentGonnaNeedIt))

Section liée : [2.4 Dupliquer coûte bien moins cher qu'une mauvaise abstraction](#24-la-duplication-coûte-moins-cher-quune-mauvaise-abstraction)

### 1.3 Laisse le code dans un meilleur état que tu ne l’as trouvé

**1.3.1 Détecte les "code smells" et agis si nécessaire**

Si tu remarques que quelque chose ne va pas, corrige-le immédiatement. Mais si ce n’est pas si simple à corriger ou si tu n’as pas le temps à ce moment-là, ajoute au minimum un commentaire (`FIXME` ou `TODO`) avec une explication concise du problème identifié. Assure-toi que tout le monde sache que c’est cassé. Cela montre que tu te soucies de la qualité du code, et incite les autres à faire de même lorsqu’ils rencontrent ce genre de choses.

<details>
    <summary><strong>🙈 Voir des exemples de "code smells" faciles à repérer</strong></summary>

<br/>

- ❌ Méthodes ou fonctions définies avec un grand nombre d’arguments  
- ❌ Logique booléenne difficile à comprendre  
- ❌ Trop de lignes de code dans un seul fichier  
- ❌ Code dupliqué qui est identique (mais potentiellement formaté différemment)  
- ❌ Fonctions ou méthodes difficiles à comprendre  
- ❌ Classes / composants avec un trop grand nombre de fonctions ou méthodes  
- ❌ Trop de lignes de code dans une seule fonction ou méthode  
- ❌ Fonctions ou méthodes avec un grand nombre de `return`  
- ❌ Code dupliqué qui n’est pas identique mais suit la même structure (ex. : seuls les noms de variables diffèrent)  

</details>

Garde en tête qu’un *code smell* ne signifie pas forcément que le code doit être changé. Il indique simplement que tu pourrais envisager une meilleure façon d’implémenter la même fonctionnalité.

**1.3.2 Refactoring impitoyable. Mieux vaut simple que complexe.**

> Le code de la pull request est-il plus complexe qu’il ne devrait l’être ? Posez-vous cette question à chaque niveau : les lignes individuelles sont-elles trop complexes ? Les fonctions ? Les classes ?  
> « Trop complexe » signifie généralement « difficile à comprendre rapidement pour les lecteurs du code ». Cela peut aussi vouloir dire que « les développeurs risquent d’introduire des bugs en appelant ou en modifiant ce code ».  
> – [Google Engineering Practices: Ce qu’il faut rechercher dans une revue de code](https://google.github.io/eng-practices/review/reviewer/looking-for.html)

**💁‍♀️ ASTUCE : Simplifiez les [conditions complexes](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Avoid_conditions.md) et sortez tôt des fonctions si possible.**

<details>
    <summary>🙈 Exemple d'utilisation de retours précoces (early returns)</summary>


```tsx
# ❌ MOINS BIEN

if (loading) {
  return <LoadingScreen />
} else if (error) {
  return <ErrorScreen />
} else if (data) {
  return <DataScreen />
} else {
  throw new Error('This should be impossible')
}

# ✅ MIEUX


if (loading) {
  return <LoadingScreen />
} 

if (error) {
  return <ErrorScreen />
}

if (data) {
  return <DataScreen />
}

throw new Error('This should be impossible')
```

</details>

**💁‍♀️ ASTUCE : Préférez les fonctions d’ordre supérieur enchaînées aux boucles**

S’il n’y a pas de différence de performance notable et si possible, remplacez les boucles traditionnelles par des fonctions d’ordre supérieur enchaînées (`map`, `filter`, `find`, `findIndex`, `some`, etc).  
[StackOverflow : Quel est l’avantage d’utiliser une fonction par rapport à une boucle ?](https://stackoverflow.com/questions/34402198/what-is-the-advantage-of-using-a-function-over-loops)

---

### 1.4 Vous pouvez faire mieux

**💁‍♀️ ASTUCE : Rappelez-vous que vous n’avez peut-être pas besoin de mettre votre `state` comme dépendance, car vous pouvez passer une fonction de rappel à la place.**

Vous n’avez pas besoin d’inclure `setState` (de `useState`) ou `dispatch` (de `useReducer`) dans le tableau de dépendances des hooks comme `useEffect` et `useCallback`. ESLint ne se plaindra pas, car React garantit leur stabilité.

<details>
    <summary>🙈 Voir un exemple</summary>

```tsx
❌ Moins bien
const decrement = useCallback(() => setCount(count - 1), [setCount, count])
const decrement = useCallback(() => setCount(count - 1), [count])

✅ MIEUX
const decrement = useCallback(() => setCount(count => (count - 1)), [])
```
</details>

**💁‍♀️ ASTUCE : Si votre `useMemo` ou `useCallback` n'a pas de dépendance, vous l'utilisez peut-être mal.**

<details>
    <summary>🙈 Voir l'exemple</summary>
 
 <br />
 
 ```tsx
 ❌ Pas terrible
const MyComponent = () => {
    const functionToCall = useCallback(x: string => `Hello ${x}!`,[])
    const iAmAConstant = useMemo(() => { return {x: 5, y: 2} }, [])
    /* Je vais utiliser functionToCall et iAmAConstant */
}
        
✅ MIEUX 
const I_AM_A_CONSTANT =  { x: 5, y: 2 }
const functionToCall = (x: string) => `Hello ${x}!`
const MyComponent = () => {
    /* Je vais utiliser functionToCall et I_AM_A_CONSTANT */ 
}
```

</details>

**💁‍♀️ ASTUCE : Envelopper votre contexte personnalisé dans un hook crée une API plus élégante**

Non seulement c'est plus joli, mais vous n'avez qu'une seule chose à importer au lieu de deux.

<details>
    <summary>🙈 Voir l'exemple</summary>
  
 <br />
 
❌ Pas terrible
```tsx
// vous devez importer deux choses à chaque fois
import { useContext } from "react"
import { SomethingContext } from "some-context-package"

function App() {
  const something = useContext(SomethingContext) // ça va, mais pourrait être mieux
  // blah
}
```

✅ Mieux
```tsx
// dans un fichier vous déclarez ce hook
function useSomething() {
  const context = useContext(SomethingContext)
  if (context === undefined) {
    throw new Error('useSomething must be used within a SomethingProvider')
  }
  return context
}

// vous n'avez besoin d'importer qu'une seule chose à chaque fois
import { useSomething } from "some-context-package"

function App() {
  const something = useSomething() // plus joli
  // blah
}
```

</details>

**💁‍♀️ ASTUCE : Réfléchissez à la façon dont votre composant sera utilisé avant de le coder**

[Écrire des APIs est difficile](http://sweng.the-davies.net/Home/rustys-api-design-manifesto). Le [`README Driven Development`](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) est une technique utile pour aider à concevoir de meilleures APIs.

Je ne dis pas qu'on devrait faire du [RDD](https://rathes.me/blog/en/readme-driven-development/) de manière religieuse, je dis juste que l'idée derrière est excellente. Je trouve que quand j'écris d'abord l'API (comment le composant sera utilisé) avant de l'implémenter, cela crée généralement un composant mieux conçu que quand je ne le fais pas.

## 🧘 2. Design pour le bonheur

> "N'importe quel imbécile peut écrire du code que l'ordinateur comprend. Les bons programmeurs écrivent du code que les humains comprennent." – Martin Fowler

> "Le rapport entre le temps passé à lire du code et celui passé à en écrire est largement supérieur à 10 pour 1. Nous passons notre temps à lire du vieux code dans le but d’en écrire du nouveau. Donc si vous voulez aller vite, si vous voulez finir rapidement, si vous voulez que votre code soit facile à écrire, rendez-le facile à lire." ― Robert C. Martin [(Je ne dis pas que je suis d'accord avec ses opinions politiques)](https://www.getrevue.co/profile/tech-bullshit/issues/tech-bullshit-explained-uncle-bob-830918)

**TL;DR**

1. Évitez la complexité de gestion d’état en supprimant les états redondants  
2. Passez la banane, pas le gorille qui tient la banane ni toute la jungle (privilégiez les primitives comme props)  
3. Gardez vos composants petits et simples – le principe de responsabilité unique !  
4. La duplication coûte bien moins cher que la mauvaise abstraction (évitez les généralisations prématurées/inappropriées)  
5. Évitez le *prop drilling* en utilisant la composition ([Michael Jackson](https://www.youtube.com/watch?v=3XaXKiXtNjw)). `Context` n’est pas la solution à tous les problèmes de partage d’état  
6. Divisez les énormes `useEffect` en effets plus petits et indépendants ([KCD : Myths about useEffect](https://epicreact.dev/myths-about-useeffect))  
7. Extrayez la logique dans des hooks ou des fonctions utilitaires  
8. Privilégiez des primitives comme dépendances dans `useCallback`, `useMemo` et `useEffect`  
9. N’ajoutez pas trop de dépendances dans `useCallback`, `useMemo` et `useEffect`  
10. Pour plus de simplicité, au lieu d’avoir plusieurs `useState`, envisagez `useReducer` si certaines valeurs dépendent d’autres ou d’états précédents  
11. Le `Context` n’a pas besoin d’être global à toute l’application. Placez-le aussi bas que possible dans l’arbre des composants, comme vous le feriez pour des variables, des commentaires, des états (et du code en général), aussi près que possible de l’endroit où ils sont utilisés.

### 💖 2.1 Évitez la complexité de gestion d’état en supprimant les états redondants

Lorsque vous avez des états redondants, certains peuvent se désynchroniser ; vous pourriez oublier de les mettre à jour après une séquence complexe d’interactions.  
En plus d’éviter les bugs de synchronisation, vous remarquerez que cela rend le raisonnement plus simple et nécessite moins de code.  
Voir aussi : [KCD: Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe](https://epic-react-exercises.vercel.app/react/hooks/1)

##### 🙈 Exemple 1
<details>
    <summary><strong> 📝🖊️ Voir l'exigence métier / énoncé du problème </strong></summary>


---

Votre tâche est d'afficher les propriétés d’un triangle rectangle :
- les longueurs des trois côtés
- le périmètre
- l’aire

Le triangle est un objet avec deux nombres `{a: number, b: number}` qui doivent être récupérés depuis une API.  
Les deux nombres représentent les deux côtés les plus courts d’un triangle rectangle.

---

</details>


<details>
 <summary> ❌ Voir une solution pas terrible </summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useState<{a: number, b: number} | null>(null)
  const [hypotenuse, setHypotenuse] = useState<number | null>(null)
  const [perimeter, setPerimeter] = useState<number | null>(null)
  const [areas, setArea] = useState<number | null>(null)

  useEffect(() => {
    fetchTriangle().then(t => setTriangleInfo(t))
  }, [])

  useEffect(() => {
    if(!triangleInfo) {
      return
    }
    
    const { a, b } = triangleInfo
    const h = computeHypotenuse(a, b)
    setHypotenuse(h)
    const newArea = computeArea(a, b)
    setArea(newArea)
    const p = computePerimeter(a, b, h)
    setPerimeter(p)

  }, [triangleInfo])

  if (!triangleInfo) {
    return null
  }

  /*** afficher les infos ici ****/
}
````
</details>


<details>
  <summary> ✅ Voir une "meilleure" solution</summary>

```tsx
const TriangleInfo = () => {
  const [triangleInfo, setTriangleInfo] = useState<{
    a: number;
    b: number;
  } | null>(null)

  useEffect(() => {
    fetchTriangle().then((r) => setTriangleInfo(r))
  }, []);

  if (!triangleInfo) {
    return
  }

  const { a, b } = triangeInfo
  const area = computeArea(a, b)
  const hypotenuse = computeHypotenuse(a, b)
  const perimeter = computePerimeter(a, b, hypotenuse)
 
  /*** show info here ****/
};
```

</details> 

##### 🙈 Example 2
<details>
    <summary><strong> 📝🖊️ Voir l'exigence métier / énoncé du problème </strong></summary>

---

Supposons que vous êtes chargé de concevoir un composant qui :

1. Récupère une liste de points uniques depuis une API  
2. Inclut un bouton pour trier soit par `x` soit par `y` (ordre croissant)  
3. Inclut un bouton pour modifier la `maxDistance` (augmenter de `10` à chaque fois, la valeur initiale doit être `100`)  
4. Affiche uniquement les points qui ne sont PAS plus éloignés que la `maxDistance` actuelle de l’origine `(0, 0)`  
5. Supposons que la liste ne contient que 100 éléments (vous n’avez donc pas à vous soucier de l’optimisation). Si vous travaillez avec de très grands ensembles de données, vous pouvez mémoriser certains calculs avec `useMemo`.

---

</details>

</details>

<details>
  <summary> ❌ Voir une solution pas terrible </summary>
  
```tsx
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [filteredPoints, setFilteredPoints] = useState<{x: number, y: number}[]>([])
  const [sortedPoints, setSortedPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')
  
  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  
  useEffect(() => {
    const sorted = sortPoints(points, sortBy)
    setSortedPoints(sorted)
  }, [sortBy, points])

  useEffect(() => {
    const filtered = sortedPoints.filter(p => getDistance(p.x, p.y) < maxDistance)
    setFilteredPoints(filtered)
  }, [sortedPoints, maxDistance])

  const otherSortBy = toggle(sortBy)
  const pointToDisplay = filteredPoints.map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy}
      <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}

````
</details>

<details>
  <summary> ✅ Voir une "meilleure" solution </summary>

```tsx

// NOTE: You can also use useReducer instead
type SortBy = 'x' | 'y'
const toggle = (current: SortBy): SortBy => current === 'x' ? : 'y' : 'x'

const Points = () => {
  const [points, setPoints] = useState<{x: number, y: number}[]>([])
  const [maxDistance, setMaxDistance] = useState<number>(100)
  const [sortBy, setSortBy] = useState<SortBy>('x')

  useEffect(() => {
    fetchPoints().then(r => setPoints(r))
  }, [])
  

  const otherSortBy = toggle(sortBy)
  const filtedPoints = points.filter(p => getDistance(p.x, p.y) < maxDistance)
  const pointToDisplay = sortPoints(filteredPoints, sortBy).map(
    p => <li key={`${p.x}|{p.y}`}>({p.x}, {p.y})</li>
  )

  return (
    <>
      <button onClick={() => setSortBy(otherSortBy)}>
        Sort by: {otherSortBy} <button>
      <button onClick={() => setMaxDistance(maxDistance + 10)}>
        Increase max distance
      <button>
      Showing only points that are less than {maxDistance} units away from origin (0, 0)
      Currently sorted by: '{sortBy}' (ascending)
      <ol>{pointToDisplay}</ol>
    </>
  )
}
````

</details>

### 💖 2.2 Passez la banane, pas le gorille qui tient la banane avec toute la jungle

> Vous vouliez une banane, mais ce que vous avez eu, c’est un gorille tenant la banane et toute la jungle. - Joe Armstrong

Pour éviter de tomber dans ce piège, il est conseillé de passer principalement des types primitifs (`boolean`, `string`, `number`, etc.) en tant que props. (Passer des primitifs est aussi recommandé si vous souhaitez utiliser `React.memo` pour l’optimisation)

> Un composant ne devrait connaître que ce qu’il lui faut pour faire son travail, et rien de plus. Autant que possible, les composants devraient pouvoir collaborer avec d’autres sans savoir ce qu’ils sont ni ce qu’ils font.

En procédant ainsi, les composants seront plus faiblement couplés, le degré de dépendance entre deux composants sera réduit. Un couplage faible rend plus facile la modification, le remplacement ou la suppression de composants sans impacter les autres. [stackoverflow:2832017](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)

##### 🙈 Exemple

<details>
    <summary><strong> 📝🖊️ Voir l'exigence métier / énoncé du problème </strong></summary>

---
