# Lab 7 : Création d'une VM avec Nginx et montage de dossier partagé

🌟 **Objectif**

Ce laboratoire vise à :

- Créer une machine virtuelle avec **Vagrant** basée sur une image hébergée sur le **cloud HashiCorp**.
- Configurer un **partage de dossier** pour déployer un site statique sur **Nginx**.
- Vérifier l'accès au site depuis la machine hôte.

---

📊 **Prérequis**

- **Vagrant** installé sur votre machine.
- **VirtualBox** comme fournisseur de machines virtuelles.
- **Connexion Internet fonctionnelle**.
- Dossier local **`static-website-example/`** contenant les fichiers du site statique.

---

🚀 **Étapes du Lab**

### 1. **Configuration du Vagrantfile**

Utilisez le fichier suivant pour configurer la machine virtuelle :

```ruby
# Variables globales
RAM = 2048
CPU = 2
IP = "10.0.0.10"

Vagrant.configure("2") do |config|
  # Utilisation de la box nginx hébergée sur HashiCorp
  config.vm.box = "jak-devops/nginx"
  config.vm.box_version = "0"

  # Configuration réseau
  config.vm.hostname = "web-server"
  config.vm.network "private_network", ip: IP

  # Montage du dossier local vers Nginx
  config.vm.synced_folder "static-website-example/", "/usr/share/nginx/html"

  # Allocation des ressources VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.memory = RAM
    vb.cpus = CPU
  end
end
```

---

### 2. **Lancer la machine virtuelle**

- Démarrez la VM avec la commande :

   ```bash
   vagrant up
   ```

- Connectez-vous à la machine pour vérifier que **Nginx** fonctionne :

   ```bash
   vagrant ssh
   ```

- Redémarrez **Nginx** pour s'assurer qu'il prend en compte les fichiers :

   ```bash
   sudo service nginx restart
   ```

---

### 3. **Vérifier le montage du dossier**

Dans la machine virtuelle, assurez-vous que les fichiers de votre site sont présents dans **`/usr/share/nginx/html/`** :

```bash
ls -l /usr/share/nginx/html/
```

Vous devriez voir les fichiers contenus dans le dossier **`static-website-example/`** de votre machine hôte.

---

### 4. **Tester l'accès au site web**

Depuis votre **machine hôte**, ouvrez un navigateur et accédez à l'URL suivante :

```
http://10.0.0.10
```

Si tout est correctement configuré, votre site statique doit s'afficher. 🎉

---

🛠 **Commandes Utiles**

| Commande                                   | Description                                      |
|--------------------------------------------|--------------------------------------------------|
| `vagrant up`                               | Démarre la machine virtuelle.                   |
| `vagrant ssh`                              | Accède à la machine virtuelle via SSH.          |
| `vagrant reload`                           | Redémarre la machine avec la configuration mise à jour. |
| `vagrant halt`                             | Arrête la machine virtuelle.                    |
| `vagrant destroy`                          | Supprime la machine virtuelle.                  |
| `sudo service nginx restart`               | Redémarre le serveur Nginx dans la VM.          |

---

📊 **Résultat Attendu**

- La machine virtuelle est configurée avec :
  - **IP privée** : `10.0.0.10`.
  - **Nginx** installé et fonctionnel.
  - **Partage de dossier** : Les fichiers du site statique dans **`static-website-example/`** sont accessibles via **`/usr/share/nginx/html`** dans la VM.

- Le site statique est accessible depuis la machine hôte via :

   ```
   http://10.0.0.10
   ```

---

🌟 **Conclusion**

Ce laboratoire vous a permis de :

- Utiliser **Vagrant** pour déployer rapidement une machine virtuelle avec **Nginx**.
- Configurer un **partage de dossier** pour déployer un site statique.
- Tester l'accessibilité du site via une IP privée.

Félicitations pour la réussite de ce lab ! 🚀🎉
