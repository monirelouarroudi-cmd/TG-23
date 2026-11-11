# Séance 3 — Loi binomiale (TG‑22) : espérance, variance, écart‑type

> **Terminale — Spécialité Mathématiques | Durée : 1h**
>
> **Prérequis :** loi binomiale, formule de $P(X=k)$, fonctions `loi` et `cumul` ; espérance, variance et écart‑type d'une variable aléatoire (Première).
>
> **Objectif :** connaître et utiliser $E(X)=np$, $V(X)=np(1-p)$ et $\sigma(X)=\sqrt{np(1-p)}$, savoir les interpréter (moyenne, dispersion) et comprendre pourquoi une moyenne « n'est pas sûre ».

---

## 1. Déroulement (1 heure)

| Temps | Activité |
|---|---|
| 0–5 min | Diagnostic rapide (rappels de Première) |
| 5–20 min | Cours : Bernoulli, binomiale, interprétation, démonstration |
| 20–30 min | 4 exercices faciles |
| 30–40 min | 3 exercices moyens |
| 40–50 min | 3 exercices difficiles |
| 50–55 min | 1 exercice très difficile (au choix, l'autre en travail personnel) |
| 55–60 min | Bilan oral + travail personnel |


---

## 2. Diagnostic — 5 min

### Question 1
Une variable $X$ prend les valeurs $0$, $1$ et $2$ avec les probabilités $0,2$ ; $0,5$ et $0,3$. Calculer $E(X)$, $V(X)$ et $\sigma(X)$.

### Question 2
Soit $X$ une variable de Bernoulli de paramètre $p=0,3$. Donner $E(X)$ et $V(X)$.

### Question 3
Rappeler la formule de $V(X)$ qui utilise $E(X^2)$.

### Question 4
Dans quelle unité s'exprime l'écart‑type ?

<details>
<summary>👉 Correction</summary>

**1.**

$$E(X)=0\times0,2+1\times0,5+2\times0,3=\boxed{1,1}$$

$$E(X^2)=0+1\times0,5+4\times0,3=1,7$$

$$V(X)=E(X^2)-E(X)^2=1,7-1,21=\boxed{0,49}\qquad\sigma(X)=\sqrt{0,49}=\boxed{0,7}$$

**2.** $E(X)=p=0,3$ et $V(X)=p(1-p)=0,3\times0,7=0,21$.

**3.** $$V(X)=E(X^2)-E(X)^2$$

**4.** Dans la même unité que $X$.

</details>

---

## 3. Résumé de cours

### 3.1 Rappel de Première

Si $X$ prend les valeurs $x_1,\dots,x_r$ :

$$E(X)=\sum_i x_i\,P(X=x_i)$$

$$V(X)=\sum_i P(X=x_i)\,\big(x_i-E(X)\big)^2=E(X^2)-E(X)^2$$

$$\sigma(X)=\sqrt{V(X)}$$

---

### 3.2 Loi de Bernoulli

Si $X$ suit la loi de Bernoulli de paramètre $p$ :

$$E(X)=p\qquad\text{et}\qquad V(X)=p(1-p)$$

**Démonstration.** $E(X)=1\times p+0\times(1-p)=p$ ; $E(X^2)=1^2\times p=p$ ; donc $V(X)=p-p^2=p(1-p)$.

---

### 3.3 Loi binomiale : espérance, variance, écart‑type

Si $X\sim\mathcal B(n;p)$ :

$$\boxed{E(X)=np}\qquad\boxed{V(X)=np(1-p)}\qquad\boxed{\sigma(X)=\sqrt{np(1-p)}}$$

**Idée :** $X$ est la somme de $n$ variables de Bernoulli indépendantes ; l'espérance d'une somme est la somme des espérances, et pour des variables indépendantes la variance d'une somme est la somme des variances.

---

### 3.4 Interprétation : le QCM au hasard

Pour $X\sim\mathcal B\!\left(10;\dfrac14\right)$ :

$$E(X)=10\times\frac14=2,5\qquad V(X)=10\times\frac14\times\frac34=1,875\qquad\sigma(X)\approx1,37$$

En moyenne, $2,5$ bonnes réponses, avec un écart typique d'environ une réponse et demie.

- $E(X)$ se comprend comme une **moyenne** sur un très grand nombre de répétitions de l'expérience ;
- $\sigma(X)$ mesure la **dispersion** autour de cette moyenne.

---

### 3.5 Attention : $E(X)$ n'est pas forcément une valeur prise

$E(X)=2,5$ alors que $X$ est entière : $P(X=2,5)=0$. Et la valeur **la plus probable** (ici $2$) n'est pas toujours l'espérance.

---

### 3.6 La variance est maximale pour $p=\frac12$

À $n$ fixé, $p(1-p)$ est maximal pour $p=\dfrac12$ :

$$p(1-p)\leq\frac14\qquad\text{donc}\qquad\sigma(X)\leq\frac{\sqrt n}{2}$$

---

### 3.7 Pour aller plus loin : la formule du capitaine

Pour $1\leq k\leq n$ :

$$k\binom{n}{k}=n\binom{n-1}{k-1}$$

*(Choisir une équipe de $k$ élèves avec un capitaine : soit on choisit d'abord l'équipe puis le capitaine, soit d'abord le capitaine puis ses $k-1$ coéquipiers.)*

**Démonstration de $E(X)=np$.** Le terme $k=0$ est nul, puis avec la formule du capitaine :

$$E(X)=\sum_{k=1}^{n}k\binom{n}{k}p^kq^{n-k}=np\sum_{k=1}^{n}\binom{n-1}{k-1}p^{k-1}q^{n-k}$$

En posant $j=k-1$, la dernière somme vaut $(p+q)^{n-1}=1$ avec $q=1-p$. Donc $E(X)=np$.

---

### 3.8 Contrôle en Python

```python
def esp_var(n, p):
    e = 0
    m2 = 0
    for k in range(n + 1):
        e = e + k * loi(n, p, k)
        m2 = m2 + k**2 * loi(n, p, k)
    return e, m2 - e**2
```

> **Réflexe :**
>
> $$\boxed{E(X)=np\qquad V(X)=np(1-p)\qquad\sigma(X)=\sqrt{np(1-p)}}$$

---

## 4. Exercices faciles

### Exercice 1 — Appliquer
Donner l'espérance, la variance et l'écart‑type (à $10^{-2}$ près) de $X\sim\mathcal B(50;0,2)$, puis de $Y\sim\mathcal B(400;0,5)$.

<details>
<summary>👉 Correction</summary>

**Pour $X\sim\mathcal B(50;0,2)$ :**

$$E(X)=50\times0,2=\boxed{10}\qquad V(X)=50\times0,2\times0,8=\boxed{8}\qquad\sigma(X)=\sqrt8\approx\boxed{2,83}$$

**Pour $Y\sim\mathcal B(400;0,5)$ :**

$$E(Y)=400\times0,5=\boxed{200}\qquad V(Y)=400\times0,5\times0,5=\boxed{100}\qquad\sigma(Y)=\sqrt{100}=\boxed{10}$$

</details>

---

### Exercice 2 — Remonter aux paramètres
$X$ suit une loi binomiale d'espérance $12$ et de variance $8,4$. Retrouver $n$ et $p$.

<details>
<summary>👉 Correction</summary>

$$np=12\qquad np(1-p)=8,4$$

En divisant la seconde égalité par la première :

$$1-p=\frac{8,4}{12}=0,7\quad\text{donc}\quad p=0,3$$

Puis $n=\dfrac{12}{0,3}=40$.

$$\boxed{n=40\qquad p=0,3}$$

</details>

---

### Exercice 3 — Un QCM de 20 questions
Un élève répond au hasard à un QCM de 20 questions, chacune à 4 réponses dont une seule correcte. $X$ est le nombre de bonnes réponses. Donner la loi de $X$, son espérance, sa variance et son écart‑type (à $10^{-2}$ près), puis interpréter.

<details>
<summary>👉 Correction</summary>

$$\boxed{X\sim\mathcal B(20;0,25)}$$

$$E(X)=20\times0,25=\boxed{5}\qquad V(X)=20\times0,25\times0,75=\boxed{3,75}\qquad\sigma(X)=\sqrt{3,75}\approx\boxed{1,94}$$

**Interprétation :** en répondant au hasard, on obtient en moyenne $5$ bonnes réponses sur $20$, avec un écart typique d'environ $2$ bonnes réponses.

</details>

---

### Exercice 4 — Une espérance qui n'est pas une valeur
Soit $X\sim\mathcal B(5;0,5)$.

a. Calculer $E(X)$. A‑t‑on $P(X=E(X))>0$ ?

b. Quelles sont les valeurs les plus probables de $X$ ?

<details>
<summary>👉 Correction</summary>

**a.**

$$E(X)=5\times0,5=2,5$$

$X$ ne prend que des valeurs entières, donc $P(X=2,5)=0$.

**b.** $P(X=2)=\dbinom52\dfrac{1}{32}=\dfrac{10}{32}$ et $P(X=3)=\dbinom53\dfrac{1}{32}=\dfrac{10}{32}$ :

$$\boxed{\text{les valeurs les plus probables sont }2\text{ et }3,\ \text{avec }\frac{10}{32}=0,3125\text{ chacune}}$$

L'espérance $2,5$ se trouve au milieu, sans être une valeur prise par $X$.

</details>

---

## 5. Exercices moyens

### Exercice 5 — Le jeu des trois dés
On mise $1$ € sur un numéro, puis on lance trois dés équilibrés. S'il n'apparaît sur aucun dé, on perd la mise ; s'il apparaît sur $k$ dés ($k\geq1$), on garde la mise et on gagne $k$ €. $X$ est le nombre de dés montrant le numéro, $G$ le gain.

a. Donner la loi de $X$ et $E(X)$.

b. Justifier que $E(G)=E(X)-P(X=0)$.

c. Calculer $P(X=0)$ puis $E(G)$. Le jeu est‑il équitable ?

<details>
<summary>👉 Correction</summary>

**a.** Succès = « le dé montre le numéro », $p=\dfrac16$, 3 lancers indépendants :

$$\boxed{X\sim\mathcal B\!\left(3;\frac16\right)}\qquad E(X)=3\times\frac16=\frac12$$

**b.** $G=k$ si $X=k\geq1$ et $G=-1$ si $X=0$. Donc :

$$E(G)=\sum_{k=1}^{3}k\,P(X=k)-P(X=0)=\Big(\sum_{k=0}^{3}k\,P(X=k)\Big)-P(X=0)=E(X)-P(X=0)$$

**c.**

$$P(X=0)=\left(\frac56\right)^3=\frac{125}{216}\approx0,5787$$

$$E(G)=\frac12-\frac{125}{216}=\frac{108-125}{216}=-\frac{17}{216}\approx\boxed{-0,0787}$$

$E(G)\neq0$ : le jeu n'est **pas équitable**. En moyenne, le joueur perd environ $0,08$ € par partie.

</details>

---

### Exercice 6 — Même moyenne, dispersions différentes
Soit $X\sim\mathcal B(10;0,5)$ et $Y\sim\mathcal B(100;0,05)$.

a. Comparer leurs espérances et leurs écarts‑types (à $10^{-2}$ près).

b. Calculer $P(X\geq8)$ et $P(Y\geq8)$ à $10^{-3}$ près (calculatrice). Commenter.

<details>
<summary>👉 Correction</summary>

**a.**

$$E(X)=10\times0,5=5\qquad E(Y)=100\times0,05=5$$

$$\sigma(X)=\sqrt{10\times0,5\times0,5}=\sqrt{2,5}\approx\boxed{1,58}\qquad\sigma(Y)=\sqrt{100\times0,05\times0,95}=\sqrt{4,75}\approx\boxed{2,18}$$

Même espérance, mais $Y$ est plus dispersée.

**b.**

$$P(X\geq8)=1-P(X\leq7)\approx\boxed{0,055}\qquad P(Y\geq8)=1-P(Y\leq7)\approx\boxed{0,128}$$

**Commentaire :** avec la même moyenne, $Y$ s'écarte plus souvent de sa moyenne, donc les grandes valeurs ($\geq8$) y sont plus probables. **Deux lois de même espérance peuvent être très différentes.**

</details>

---

### Exercice 7 — Un sondage
Dans une ville, $52\,\%$ des électeurs votent pour le candidat A. Un institut interroge $1\,000$ électeurs, assimilés à un tirage avec remise. $X$ compte ceux qui votent A.

a. Calculer $E(X)$ et $\sigma(X)$ à $0,1$ près.

b. Calculer $P(X\leq500)$ à $10^{-3}$ près. Interpréter pour le sondage.

<details>
<summary>👉 Correction</summary>

**a.** $X\sim\mathcal B(1000;0,52)$.

$$E(X)=1000\times0,52=\boxed{520}$$

$$V(X)=1000\times0,52\times0,48=249,6\qquad\sigma(X)=\sqrt{249,6}\approx\boxed{15,8}$$

**b.**

$$\boxed{P(X\leq500)\approx0,109}$$

**Interprétation :** même si $52\,\%$ des électeurs votent réellement pour A, il y a environ $11\,\%$ de chances que le sondage donne **au plus $500$** réponses pour A, c'est‑à‑dire pas de majorité visible. Un sondage de $1\,000$ personnes ne permet donc pas de conclure de façon sûre.

</details>

---

## 6. Exercices difficiles

### Exercice 8 — La dispersion la plus grande
On fixe $n$ et on note $f(p)=np(1-p)$ pour $p\in[0;1]$.

a. Étudier les variations de $f$. Pour quelle valeur de $p$ la variance est‑elle maximale ?

b. En déduire que $\sigma(X)\leq\dfrac{\sqrt n}{2}$.

c. Avec 100 lancers d'une pièce, l'écart‑type du nombre de « pile » peut‑il dépasser $5$ ?

<details>
<summary>👉 Correction</summary>

**a.** $f(p)=np-np^2$, donc :

$$f'(p)=n-2np=n(1-2p)$$

$f'(p)>0$ pour $p<\dfrac12$ et $f'(p)<0$ pour $p>\dfrac12$ : $f$ croît sur $\left[0;\dfrac12\right]$ puis décroît sur $\left[\dfrac12;1\right]$.

$$\boxed{\text{La variance est maximale pour }p=\frac12,\ \text{avec }f\!\left(\frac12\right)=\frac n4}$$

**b.** $\sigma(X)=\sqrt{f(p)}\leq\sqrt{\dfrac n4}=\boxed{\dfrac{\sqrt n}{2}}$.

**c.** Pour $n=100$ : $\sigma(X)\leq\dfrac{\sqrt{100}}{2}=5$. L'écart‑type **ne peut pas dépasser $5$** : il vaut exactement $5$ pour une pièce équilibrée ($p=0,5$), et il est plus petit pour une pièce déséquilibrée.

</details>

---

### Exercice 9 — En moyenne n'est pas sûrement
Une graine germe avec probabilité $0,85$, indépendamment des autres. On veut obtenir **en moyenne** au moins $100$ plants.

a. Combien de graines faut‑il semer au minimum ?

b. Avec ce nombre, calculer $P(X<100)$ à $10^{-2}$ près (calculatrice). Conclure.

<details>
<summary>👉 Correction</summary>

**a.** Si on sème $n$ graines, $X\sim\mathcal B(n;0,85)$ et $E(X)=0,85\,n$.

$$0,85\,n\geq100\Longleftrightarrow n\geq\frac{100}{0,85}\approx117,65$$

$$\boxed{n=118}$$

**b.** Pour $X\sim\mathcal B(118;0,85)$, $E(X)=100,3$ et :

$$P(X<100)=P(X\leq99)\approx\boxed{0,41}$$

**Conclusion :** bien que l'espérance soit supérieure à $100$, il y a environ **$41\,\%$ de chances** d'obtenir moins de $100$ plants. « Avoir 100 plants en moyenne » ne garantit pas d'avoir 100 plants sur une expérience donnée.

</details>

---

### Exercice 10 — Dériver pour calculer l'espérance
Soit $X\sim\mathcal B(n;p)$, $q=1-p$ et, pour $t\in\mathbb R$, $g(t)=(pt+q)^n$.

a. Justifier que $g(t)=\displaystyle\sum_{k=0}^{n}P(X=k)\,t^k$.

b. Calculer $g'(t)$ de deux façons, puis en $t=1$ : retrouver $E(X)=np$.

c. Que donne $g''(1)$ ? En déduire $V(X)$.

<details>
<summary>👉 Correction</summary>

**a.** Avec la formule du binôme :

$$g(t)=\sum_{k=0}^{n}\binom{n}{k}(pt)^kq^{n-k}=\sum_{k=0}^{n}\binom{n}{k}p^kq^{n-k}\,t^k=\sum_{k=0}^{n}P(X=k)\,t^k$$

**b.** En dérivant la somme :

$$g'(t)=\sum_{k=0}^{n}k\,P(X=k)\,t^{k-1}\quad\Longrightarrow\quad g'(1)=\sum_{k=0}^{n}k\,P(X=k)=E(X)$$

En dérivant la forme composée :

$$g'(t)=np\,(pt+q)^{n-1}\quad\Longrightarrow\quad g'(1)=np\,(p+q)^{n-1}=np$$

Donc $\boxed{E(X)=np}$.

**c.** En dérivant une seconde fois :

$$g''(t)=n(n-1)p^2(pt+q)^{n-2}\quad\Longrightarrow\quad g''(1)=n(n-1)p^2$$

D'autre part $g''(1)=\displaystyle\sum_{k=0}^{n}k(k-1)P(X=k)=E\big(X(X-1)\big)=E(X^2)-E(X)$.

Donc $E(X^2)=n(n-1)p^2+np$ et :

$$V(X)=E(X^2)-E(X)^2=n(n-1)p^2+np-n^2p^2=np-np^2$$

$$\boxed{V(X)=np(1-p)}$$

</details>

---

## 7. Exercices très difficiles / réflexion

*Faire l'un des deux en séance, laisser l'autre en travail personnel.*

### Exercice 11 — Contrôle en Python
On reprend la fonction `esp_var(n, p)` du cours (3.8).

a. Quelle formule de Première le programme utilise‑t‑il pour la variance ?

b. En appelant `esp_var(20, 0.3)`, on lit des valeurs comme $(5{,}999999999999993\ ;\ 4{,}200000000000053)$. Commenter.

c. Modifier la dernière ligne pour que la fonction renvoie aussi l'écart‑type.

<details>
<summary>👉 Correction</summary>

**a.** Le programme calcule $E(X)=\sum k\,P(X=k)$ et $E(X^2)=\sum k^2P(X=k)$, puis utilise :

$$V(X)=E(X^2)-E(X)^2$$

**b.** Les valeurs théoriques sont :

$$E(X)=20\times0,3=6\qquad V(X)=20\times0,3\times0,7=4,2$$

L'ordinateur trouve des valeurs très proches de $6$ et de $4,2$ : l'écart (de l'ordre de $10^{-14}$) vient des **arrondis des nombres décimaux** dans les sommes de nombreux termes. Les résultats sont cohérents avec les formules $np$ et $np(1-p)$. Les derniers chiffres peuvent varier d'une machine à l'autre.

**c.**

```python
from math import sqrt

def esp_var(n, p):
    e = 0
    m2 = 0
    for k in range(n + 1):
        e = e + k * loi(n, p, k)
        m2 = m2 + k**2 * loi(n, p, k)
    v = m2 - e**2
    return e, v, sqrt(v)
```

</details>

---

### Exercice 12 — Contrôle qualité
Une machine produit $2\,\%$ de pièces défectueuses, indépendamment les unes des autres. On prélève un lot de $200$ pièces ; $X$ est le nombre de pièces défectueuses.

a. Donner la loi de $X$, puis $E(X)$, $V(X)$ et $\sigma(X)$ (à $10^{-2}$ près).

b. On décide d'arrêter la machine si le lot contient **au moins $8$** pièces défectueuses. Calculer la probabilité d'arrêter la machine alors qu'elle fonctionne normalement (calculatrice, à $10^{-3}$ près).

c. Même question avec le seuil « au moins $10$ ». Que gagne‑t‑on, que risque‑t‑on avec ce seuil plus élevé ?

<details>
<summary>👉 Correction</summary>

**a.**

$$\boxed{X\sim\mathcal B(200;0,02)}$$

$$E(X)=200\times0,02=\boxed{4}\qquad V(X)=200\times0,02\times0,98=\boxed{3,92}\qquad\sigma(X)=\sqrt{3,92}\approx\boxed{1,98}$$

**b.**

$$P(X\geq8)=1-P(X\leq7)\approx\boxed{0,049}$$

Environ $4,9\,\%$ de risque d'arrêter la machine « pour rien ».

**c.**

$$P(X\geq10)=1-P(X\leq9)\approx\boxed{0,007}$$

Avec le seuil $10$, on n'arrête la machine à tort que dans environ $0,7\,\%$ des cas (moins de fausses alertes). En contrepartie, on tolère davantage de pièces défectueuses avant de réagir : si la machine se dérègle vraiment, on s'en apercevra plus tard.

</details>

---

## 8. Bilan de fin de séance (5 min)

### Les 4 réflexes à retenir

#### Réflexe 1 — Les formules
$$\boxed{E(X)=np\qquad V(X)=np(1-p)\qquad\sigma(X)=\sqrt{np(1-p)}}$$

#### Réflexe 2 — Avant d'appliquer
**Je vérifie d'abord que $X$ suit bien une loi binomiale (les quatre points de justification).**

#### Réflexe 3 — Interpréter
**$E(X)$ = moyenne sur un grand nombre de répétitions ; $\sigma(X)$ = dispersion autour de cette moyenne.**

#### Réflexe 4 — Méfiance
**Une moyenne peut coûter cher : $E(X)\geq100$ ne garantit pas $X\geq100$ (exercice 9).**

### Questions orales (sans regarder le cours)

1. Que valent $E(X)$ et $V(X)$ pour une variable de Bernoulli ?
2. Que valent $E(X)$, $V(X)$ et $\sigma(X)$ pour $X\sim\mathcal B(n;p)$ ?
3. Pourquoi $E(X)$ n'est‑elle pas toujours une valeur prise par $X$ ?
4. Pour quelle valeur de $p$ la dispersion est‑elle la plus grande, à $n$ fixé ?

---

## 9. Travail personnel

- refaire les exercices 2, 5, 6 et 7 sans regarder la correction ;
- refaire l'exercice 9 en insistant sur la conclusion rédigée ;
- l'exercice très difficile non traité en séance (11 ou 12) ;
- savoir démontrer, avec la formule du capitaine ou avec l'exercice 10, que $E(X)=np$.

### Pour le professeur

Noter à la fin de la séance :

- maîtrise des trois formules et de leur utilisation ;
- capacité à remonter aux paramètres $n$ et $p$ ;
- qualité de l'interprétation d'une espérance et d'un écart‑type ;
- compréhension que « en moyenne » ne veut pas dire « sûrement » ;
- aisance à lire un programme Python (`esp_var`).

> **Lien avec la suite :** la séance suivante portera sur $E(aX+b)$ et $V(aX+b)$, puis sur l'intervalle de fluctuation.
