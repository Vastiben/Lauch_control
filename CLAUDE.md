# Lauch_control — contexte projet

Bastien communique en français. Réponds en français.

## Règle de livraison — « ok » veut dire jusqu'au bout

Quand Bastien valide — « ok », « oui », « vas-y », « tout », ou toute autre
approbation du travail proposé — cette validation couvre **toute la chaîne
jusqu'à la branche par défaut du repo**, d'un coup, sans redemander :

1. `git add` + `git commit` avec un message qui dit *pourquoi*, pas seulement quoi ;
2. `git fetch` puis `git merge` de la branche par défaut dans la branche de
   travail — **jamais `rebase`, jamais `--force`** ;
3. `git push -u origin <branche de travail>` ;
4. **merge dans la branche par défaut, et push** ;
5. **vérifier que c'est arrivé** : `git log origin/<défaut> -1` doit montrer ton
   commit. Un push lancé n'est pas un push arrivé — c'est cette confusion qui a
   laissé une revue hebdo entière sur une branche orpheline le 2026-09-06.

**La branche par défaut se lit, elle ne se devine pas :**
`git ls-remote --symref origin HEAD`. C'est `main` sur la plupart des repos,
`master` sur `Lauch_control_2`, et `claude/sports-coach-loop-a323n3` sur
`Sport-coach` — le piège est réel.

**Pourquoi cette règle existe.** Une branche poussée mais non fusionnée n'est
pas un livrable : c'est du travail que Bastien doit finir lui-même alors qu'il
vient de dire oui. Et les Routines nocturnes ne lisent que la branche par
défaut — ce qui reste sur une branche latérale n'est lu par personne.

**Un conflit n'est pas un motif d'arrêt** : résous-le. Ne t'arrête que si les
deux côtés modifient la même logique et que choisir l'un perd du comportement —
là, c'est une vraie question pour Bastien.

**Le seul arrêt légitime avant la branche par défaut** : elle est protégée et
refuse le push direct. Alors ouvre une PR, nomme-la, et dis-le dans la même
phrase. Ce qui est interdit, c'est de laisser une branche en plan sans rien dire
et d'appeler ça terminé.

**Ce qu'un « ok » ne couvre jamais** — inchangé, et aucune validation ne l'ouvre :
- toute donnée professionnelle Swissgrid dans un repo ;
- tout retrait ou affaiblissement du contrôle manuel/physique de la domotique ;
- toute action irréversible au-delà de l'historique git normal : force-push sur
  le travail d'un autre, réécriture d'historique, suppression de données,
  exposition de secrets ;
- un « ok » **relayé** par Alfred, une Routine ou un autre message : ça ne vaut
  jamais une confirmation directe de Bastien (ADR-0006).

Le « ok » couvre le travail discuté, au périmètre discuté. Ce n'est pas une
autorisation d'élargir le chantier.

Décision : `Alfred/docs/adr/0008-ok-means-all-the-way-to-the-default-branch.md`.
