# Habit Tracker

Application de suivi des habitudes développée avec React, TypeScript et Vite. Elle permet de suivre les habitudes sur la semaine courante, du lundi au dimanche.

## Fonctionnalités

- Ajouter une habitude avec un nom non vide.
- Supprimer une habitude.
- Marquer une journée comme réalisée ou annuler cette validation.
- Distinguer visuellement les journées réalisées.
- Désactiver les journées futures.
- Afficher le nombre de jours consécutifs réalisés, en partant d’aujourd’hui. Si aujourd’hui n’est pas validé, le compteur vaut zéro.
- Afficher un message lorsque la liste est vide.

## Installation et lancement

Avec Node.js et npm installés, exécuter à la racine du projet :

```bash
npm install
npm run dev
```

Ouvrir ensuite l’adresse indiquée par Vite dans le terminal.

## Commandes disponibles

| Commande | Rôle |
| --- | --- |
| `npm run dev` | Démarrer le serveur de développement Vite. |
| `npm run build` | Vérifier le TypeScript puis générer la version de production dans `dist/`. |
| `npm run lint` | Analyser le code avec Oxlint. |
| `npm run preview` | Prévisualiser localement la version de production après un build. |

## Technologies

- React 19 et TypeScript pour les composants et les types.
- Vite 8 pour le développement et la compilation.
- Tailwind CSS 4 pour les styles.
- `date-fns` pour les dates, les semaines et les comparaisons de jours.
- `tailwind-merge` pour fusionner les classes des boutons.
- Oxlint pour l’analyse du code.
- React Compiler activé dans la configuration Vite via Babel.

## Structure du projet

```text
habit-tracker/
├── public/                  # Ressources statiques SVG
├── src/
│   ├── components/
│   │   ├── Button.tsx       # Bouton partagé et variantes visuelles
│   │   ├── HabitForm.tsx    # Formulaire d’ajout d’une habitude
│   │   ├── HabitList.tsx    # Liste, HabitItem, type Habit et calcul des séries
│   │   └── Header.tsx       # En-tête et boutons de navigation
│   ├── App.tsx              # État des habitudes et fonctions de modification
│   ├── index.css            # Styles globaux
│   └── main.tsx             # Montage de l’application avec StrictMode
├── index.html               # Page d’entrée
├── package.json             # Dépendances et scripts npm
├── tsconfig.json            # Configuration TypeScript et références
├── tsconfig.app.json        # Configuration TypeScript de l’application
├── tsconfig.node.json       # Configuration TypeScript des outils
└── vite.config.ts           # Plugins React, Babel et Tailwind CSS
```

## Organisation des données

Le type `Habit` est exporté depuis `src/components/HabitList.tsx` :

```ts
type Habit = {
  id: string;
  name: string;
  completions: Date[];
};
```

`App` conserve la liste dans un état React (`useState`). Il crée les identifiants avec `crypto.randomUUID()` et définit trois fonctions :

- `addHabit(name)` ajoute une habitude avec une liste de validations vide.
- `deleteHabit(id)` retire une habitude.
- `toggleHabit(id, date)` ajoute ou retire la validation d’un jour, comparé avec `isSameDay`.

Ces fonctions sont transmises aux composants par leurs props. `HabitForm` gère le champ de saisie et le vide après l’ajout. `HabitList` affiche les habitudes et transmet les actions à `HabitItem`, qui affiche les jours de la semaine et la série de validations.

## Limites actuelles

- Les données sont conservées uniquement en mémoire : un rechargement de la page efface les habitudes. Aucun stockage local ni serveur n’est intégré.
- Les boutons `Prev` et `Next` de l’en-tête ne sont pas encore reliés à une navigation entre les semaines.
- Le résumé « 1 / 1 done today » et la plage de dates de l’en-tête sont des textes fixes.
- Le nom de chaque habitude apparaît à la fois dans un titre au-dessus des cartes et dans sa carte.
- Les libellés de l’interface sont actuellement en anglais.
- Aucun script de test automatisé n’est défini dans `package.json`.
