# Tpp12
# LAB-12 | Contournement de la Détection de Root Android via Medusa & Frida

## 1. Introduction
Ce laboratoire est dédié à l'étude des mécanismes de détection de root au sein d'un environnement Android et à la mise en œuvre de techniques de contournement par instrumentation dynamique. 

L'application cible utilisée est **OWASP UnCrackable Level 2**, un binaire volontairement vulnérable conçu pour l'apprentissage du reverse engineering et de la sécurité mobile.

L'évaluation explore deux méthodologies distinctes :
1. **Approche manuelle :** Injection et hooking via **Frida**.
2. **Approche automatisée :** Orchestration et gestion des hooks via le framework **Medusa**.

> 💡 **Note clé :** Ce TP démontre qu'une sécurité reposant exclusivement sur des vérifications côté client (comme la détection de root ou de débogage) reste contournable à l'exécution si elle n'est pas consolidée par une logique de validation serveur ou des mécanismes d'obfuscation avancés.

---

## 2. Objectifs Pédagogiques
* Configurer et synchroniser le serveur `frida-server` sur l'émulateur Android et le client sur la machine hôte.
* Valider l'état de la communication inter-périphériques via le protocole ADB.
* Analyser le comportement initial et les routines de fermeture de l'application face à un appareil rooté.
* Intercepter et neutraliser les classes Java responsables du contrôle d'intégrité du système.
* Dissimuler la présence des binaires de su (SuperUser) et des indicateurs de root habituels.
* Contourner la logique de validation du code secret (Secret Key).
* Exploiter le framework **Medusa** pour automatiser et structurer l'exécution des scripts d'instrumentation.
* Documenter méthodiquement chaque phase de l'analyse avec des preuves visuelles.

---

## 3. Environnement Technique

| Composant | Spécification / Valeur |
| :--- | :--- |
| **Système Hôte** | Windows (PowerShell) |
| **Environnement de Test** | Émulateur Android (`emulator-5554`) |
| **Application Cible** | OWASP UnCrackable Level 2 |
| **Package ID** | `owasp.mstg.uncrackable2` |
| **Outil d'Instrumentation** | Frida |
| **Framework d'Automatisation** | Medusa |
| **Type de Rétro-ingénierie** | Analyse dynamique en mémoire |

---

## 4. Application Cible
L'application **OWASP UnCrackable Level 2** fait partie du projet *Mobile Application Security Verification Standard (MASVS)* de l'OWASP. Elle intègre des protections natives (anti-root, anti-debug, vérification de signature) qui en font un excellent cas d'étude pour la manipulation de runtimes Android.

---

## 5. Procédure Exécutive & Captures d'Écran

### Étape 1 — Validation de la liaison ADB
<img width="775" height="85" alt="Connexion ADB" src="https://github.com/user-attachments/assets/ccc88142-b46f-4ff7-93c2-da2ab6e58a88" />

*Vérification de la bonne détection du terminal Android virtuel par le démon ADB de la machine de travail.*

### Étape 2 — Énumération du processus cible par Frida
<img width="1208" height="736" alt="Détection Frida" src="https://github.com/user-attachments/assets/8366a68d-c02c-40dd-bdbc-1ed86d8d3210" />

*Cartographie des périphériques et identification formelle du package UnCrackable Level 2 actif sur l'émulateur.*

### Étape 3 — Injection du script de hooking (Frida)
<img width="1410" height="649" alt="Exécution script Frida" src="https://github.com/user-attachments/assets/07f90dc1-f647-4da0-8707-19ab34f67524" />

*Initialisation et chargement des hooks JavaScript personnalisés dans la mémoire du processus Android.*

### Étape 4 — Validation du contournement manuel
<img width="384" height="835" alt="Bypass réussi" src="https://github.com/user-attachments/assets/a849dded-8742-4aff-97c2-c2f52b00d206" />

*L'alerte de sécurité est neutralisée et l'application reste active : le premier niveau de protection est contourné.*

### Étape 5 — Initialisation du framework Medusa
<img width="1432" height="612" alt="Lancement Medusa" src="https://github.com/user-attachments/assets/4236371c-4a78-462c-8513-d2b0123bc5dd" />

*Lancement de la console Medusa et ciblage de l'instance de l'émulateur connecté.*

### Étape 6 — Configuration du script d'agent (`agent.js`)
<img width="1035" height="850" alt="Agent.js dans Medusa" src="https://github.com/user-attachments/assets/2413dab6-cbbe-4e45-8508-65a606c047ac" />

*Intégration et alignement de la logique d'instrumentation personnalisée au sein de l'environnement de Medusa.*

### Étape 7 — Exploration du catalogue de modules
<img width="802" height="265" alt="Modules Medusa" src="https://github.com/user-attachments/assets/3745ba8e-89fc-4fe5-b94a-4402a00a78b0" />

*Parcours des scripts et modules utilitaires mis à disposition par Medusa pour faciliter l'analyse à chaud.*

### Étape 8 — Exécution et Bypass final via Medusa
<img width="384" height="835" alt="Bypass final Medusa" src="https://github.com/user-attachments/assets/a849dded-8742-4aff-97c2-c2f52b00d206" />

*Lancement supervisé par Medusa : les routines anti-root sont interceptées et neutralisées automatiquement au démarrage.*
