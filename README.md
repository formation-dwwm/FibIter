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
