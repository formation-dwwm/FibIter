# FibIter

On se propose ici de travailler l'algorithmique et la notion d'Itérable (ES6) à travers l'utilisation de la suite de Fibonnacci.

Mathématiquement cette suite se définit ainsi:

```
U[0] = 0; U[1] = 1;
U[n] = U[n-1] + U[n-2] pour n > 1
```

En langage naturel :
> Un terme de la suite de Fibonnacci représente la somme des deux termes précédents.

Les premières valeurs successives de cette suite sont donc:

```javascript
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...]
```

# Cheminement

## 1/ Un générateur de fibonnacci

Se créer une fonction `next` telle que :

```javascript
console.log(next());  // 1
console.log(next());  // 2
console.log(next());  // 3
console.log(next());  // 5
// ...
``` 

Vous pouvez baser votre structure comme suit :

```javascript
let prev = 0, curr = 0;
const next = () => {
  // ...
  return //...;
}
```

## 1-bis/ Intéraction DOM

Placer dans une page HTML un `label` ou `input[disabled]` qui affichera la dernière valeur calculée, et sera mis à jour à chaque fois que l'utilisateur cliquera sur un `button` next.


## 2/ Protocole Itérateur

[Documentation MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Les_protocoles_iteration)

Se préparer à l'utilisation du protocol *Itérateur*.
- La fonction `next` doit appartenir à un objet (function "membre"). Exemple: `FibIterateur.next()`
- `next()` renvoie un objet de la forme:
```javascript
{
    value: // La valeur de fib,
    done: false // Toujours false pour l'instant
}
```


## 3/ Protocole Itérable

Créer un objet FibIterable implémentant le protocole *Itérable*.

L'utiliser avec :

```javascript
for(let v of FibIterable){
    console.log(v);
    if(v > 50) break;
}
```


## 4/ Currying pour paramétrer notre suite

On se propose maintenant de transformer notre objet FibIterable en une fonction, qui servira alors à définir la valeur maximale accessible par l'itérateur.

Après transformations, on veut donc obtenir le même résultat que précédemment (sans boucle infinie !!) avec le code suivant :

```javascript
for(let v of FibIterable(50)){
    console.log(v);
}
```


## 5/ Représentation graphique

Une particularité remarquable de la suite de Fibonnacci est que le rapport entre deux termes successifs tend asymptotiquement vers le [Nombre d'Or (Phi, φ)](https://fr.wikipedia.org/wiki/Nombre_d%27or) :

```
U[n+1] / U[n] -> Phi
```

Le Nombre d'Or peut être utilisé pour réaliser la [Spirale d'Or](https://fr.wikipedia.org/wiki/Spirale_d%27or), dont la spécificité est de devenir plus large par un facteur de φ à chaque quart de tour.

Les valeurs successives générées par notre itérable pourront donc être utilisée en tant que rayons successifs pour notre spirale, une pour chaque quart de tour. Etant donné les propriétés de la suite de Fibonnacci, nous aurons ainsi une approximation assez juste de la Spirale d'Or.

Dans un premier temps nous représenteront cette spirale par des segments de droite pour chaque quart de tour.

### A - Graphisme en Javascript

En vous aidant d'Internet, repérer les différentes technologies ou API accessibles depuis JavaScript qui permettent de réaliser des représentations graphiques.

**Hints**:
- SVG et ici la balise path
- Canvas et son context2D

### B - Utilisation du SVG

**Hints**:
- Nous utiliserons la balise `path` de SVG
- Puisque nous avons choisi de représenter notre spirale par des segments, le path pourra ne comporter que des instructions `MoveTo` et `LineTo`.
- Nous partons ici de rayons est d'angles (coordonnées polaires) pour construire notre spirale, alors que SVG (comme canvas) utilisent des coordonnées x, y (coordonnées cartésiennes). La création d'une fonction transformant des coordonnées polaires en cartésiennes est donc chaudement recommandée.

<details>
 <summary>Proposition pour `polar2cart`</summary>

```javascript
const polar2cart = (radius, angle) => ({ x: radius*Math.cos(angle/180*Math.PI), y: radius*Math.sin(angle/180*Math.PI) });
```
</details>
