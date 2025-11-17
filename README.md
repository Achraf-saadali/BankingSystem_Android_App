# BankingSystem Android App

BankingSystem est une application Android de gestion bancaire permettant aux utilisateurs de consulter leur compte, effectuer des transactions (retraits, transferts) et suivre l’historique de leurs transactions. L’application communique avec un serveur backend via **REST API** et **SOAP** pour certaines opérations.

---

## Fonctionnalités

* **Connexion utilisateur** : Authentification avec `owner_name` et `password`.
* **Visualisation du compte** : Affiche le solde et les informations du compte.
* **Retrait de fonds** : Permet de retirer de l’argent en choisissant le montant.
* **Transfert d’argent** : Envoyer de l’argent à un autre compte via un identifiant ou RIB.
* **Historique des transactions** : Liste complète des transactions (retraits, dépôts, transferts) avec détails.
* **Support SOAP** : Certaines transactions utilisent des requêtes SOAP pour la communication avec le serveur.
* **Interface moderne** : Material Design, cartes, gradients, et boutons animés.

---

## Architecture

* **Frontend (Android)** :

  * Kotlin + Android Studio
  * RecyclerView pour l’historique des transactions
  * CardView et Material Components pour UI
  * Retrofit2 pour REST API
  * Gson pour sérialisation JSON

* **Backend (Python/Flask)** :

  * Base de données MySQL pour comptes et transactions
  * Routes REST (`/transactions`, `/login`, `/withdraw`, `/transfer`)
  * SOAP endpoints pour certaines opérations bancaires

---

## Modèles de données

### Account

```kotlin
@Serializable
data class Account(
    val Code: Int?,
    val account_id: Int?,
    var balance: Float,
    val message: String?,
    val owner_name: String?,
    val password: String?,
    val rib: String?,
    val status: String?
)
```

### Transaction

```kotlin
data class Transaction(
    val transaction_id: Int?,
    val from_account_Name: String?,
    val to_account_Name: String?,
    val amount: Float?,
    val type_transaction: String? // Deposit, Withdraw, Transfer
)
```

---

## Installation et Exécution

1. Cloner le dépôt :

```bash
git clone https://github.com/achraf-saadali/BankingSystem.git
```

2. Ouvrir le projet dans Android Studio.
3. Configurer le backend :

   * Installer Python 3.x et MySQL.
   * Créer la base de données `banking`.
   * Lancer le serveur Flask :

   ```bash
   python app.py
   ```
4. Configurer Retrofit `BASE_URL` dans Android :

```kotlin
object RetrofitClient {
    val instance: ApiService by lazy {
        Retrofit.Builder()
            .baseUrl("http://<SERVER_IP>:5000/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
            .create(ApiService::class.java)
    }
}
```

5. Lancer l’application sur un émulateur ou appareil physique Android.

---

## Screenshots

* Écran de connexion
* Dashboard avec solde
* Écran de retrait
* Écran de transfert
* Historique des transactions

*(Insérer des captures d’écran si disponible)*

---

## Dépendances

* Retrofit 2
* Gson
* RecyclerView
* Material Components
* CardView
* ConstraintLayout

---

## Structure du projet

```
BankingSystem/
│
├─ app/src/main/java/com/example/bankingapp
│   ├─ Activities/
│   │   ├─ DashboardActivity.kt
│   │   ├─ WithdrawActivity.kt
│   │   ├─ TransferActivity.kt
│   │   └─ TransactionsActivity.kt
│   ├─ Adapters/
│   │   └─ TransactionsAdapter.kt
│   ├─ Models/
│   │   ├─ Account.kt
│   │   ├─ Transaction.kt
│   │   └─ TransactionRequest.kt
│   └─ Network/
│       ├─ ApiService.kt
│       └─ RetrofitClient.kt
│
├─ app/src/main/res/
│   ├─ layout/ (XML layouts)
│   ├─ drawable/ (icônes et fonds)
│   └─ values/ (colors, strings, styles)
│
└─ backend/
    ├─ app.py
    └─ init_db.sql
```

---

## Auteurs

* **Achraf Saadali** – Étudiant ENSA El Jadida – 1ère année IITE
  Email: [achrafsaadalii@gmail.com](mailto:achrafsaadalii@gmail.com)
  GitHub: [https://github.com/achraf-saadali](https://github.com/achraf-saadali)

---

## Licence

Ce projet est sous licence MIT – voir le fichier LICENSE pour plus de détails.
