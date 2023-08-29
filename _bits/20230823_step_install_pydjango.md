---
title: Step by step - Install Python & Django
permalink: /bits/step_install_pydjango/
layout: single
author_profile: true
toc: true
toc_sticky: true
excerpt: "How to quickly install Python & Django on Windows and MacOS"
last_modified_at: 2023-08-29T20:48:05-04:00
---
**Note:** This bit is a basic step-by-step guide on how to install Python & Django on Windows and MacOS. It was realized as part of my studies and it is not meant to be a full tutorial on how to use Django. If you want to learn more about Django, I recommend you to check out the [official documentation](https://docs.djangoproject.com/en/3.2/).
{: .notice}


# Français

## Prérequis

-   Téléchargez le programme d'installation de [Python](https://www.python.org/downloads/) pour votre système d'exploitation (devrait être sélectionné automatiquement).
-   VS Code & VS Code extension “Python”

## Installer Python & Django sur Windows

1.  Ouvrez le logiciel d’installation et suivez les instructions à l'écran afin d'installer python. Vous devrez peut-être entrer votre mot de passe pour autoriser l'installation. Vous pouvez aussi installer la version proposée sur le microsoft store. Voilà, c'est fait !
    
    ![0-python.png](/assets/images/bits/0-python.png)
    
2.  Ouvrez powershell et saisissez cette commande afin d’installer Django
    

```powershell
python -m pip install Django
```

![1-installDjangoPS.png](/assets/images/bits/1-installDjangoPS.png)

1.  Si vous avez une erreur de variable d’environnement système du “PATH”, vous pouvez l’ajouter manuellement en lançant le logiciel “Modifier les variables d’environnement pour votre compte”

![MicrosoftTeams-image (1).png](/assets/images/bits/MicrosoftTeams-image_(1).png)

-   Dans la variable "Path" > modifier > nouveau > copier coller le chemin d'installation de Django qui est dans notre cas:

```
C:\\Users\\%user%\\AppData\\Local\\Packages\\PythonSoftwareFoundation.Python.3.11_qbz5n2kfra8p0\\LocalCache\\local-packages\\Python311\\Scripts
```

<aside> 💡 _**NOTE**_: il est possible que suite à une mise à jour de python, le chemin change, il faudra donc chercher le chemin correct en partant de “\Packages\”

</aside>

1.  dans power shell, utiliser la commande "cd" pour aller dans le repertoire de travail pour votre projet et tapez la commande "django-admin startproject NomDuProjet”

```powershell
django-admin startproject NomDuProjet
```

-   deplacer vous encore une fois dans le dossier du nom de projet et taper la commande suivante pour lancer le serveur local

```python
python [manage.py](<http://manage.py/>) runserver
```

![3-4-createProjectAndRun.png](/assets/images/bits/3-4-createProjectAndRun.png)

1.  Dans votre navigateur, tapez "localhost:8000" et constater la page par defaut de Django
    
    ![5-defaultPageDjango.png](/assets/images/bits/5-defaultPageDjango.png)
    

## Installer Python & Django sur MacOS

1.  Ouvrez le paquet d’installation et suivez les instructions à l'écran afin d'installer python. Vous devrez peut-être entrer votre mot de passe pour autoriser l'installation. Voilà, c'est fait !
2.  Installez le gestionnaire de paquets Python (pip) en collant cette ligne dans le terminal afin de pouvoir ajouter de nouveaux modules à nos projets python.

```bash
python3 -m pip install --upgrade pip
```

1.  Pour installer Django, il suffit de saisir la ligne ci-dessous dans le terminal. Ceci en utilisant le gestionnaire de paquets Python (voir l'étape précédente)

```bash
pip3 install Django
```

# English

# Requirements

-   Download the [Python](https://www.python.org/downloads/) installer for your current Operating System (Should automatically be selected)
-   VS Code & VS Code extension “Python”

## Install Python & Django on Windows

1.  Open the installation software and follow the on-screen instructions to install Python. You may need to enter your password to authorize the installation. You can also install the version offered on the Microsoft Store. And that's it!
    
    ![0-python.png](/assets/images/bits/0-python.png)
    
2.  Open PowerShell and enter this command to install Django:
    
    ```powershell
    python -m pip install Django
    ```
    
    ![1-installDjangoPS.png](/assets/images/bits/1-installDjangoPS.png)
    
3.  If you have a "PATH" system environment variable error, you can add it manually by running the "Change environment variables for your account" program
    
    ![MicrosoftTeams-image (1).png](/assets/images/bits/MicrosoftTeams-image+(1).png)
    

-   In the "Path" variable > modify > new > copy and paste the installation path of Django which in our case is:

```
C:\\Users\\%user%\\AppData\\Local\\Packages\\PythonSoftwareFoundation.Python.3.11_qbz5n2kfra8p0\\LocalCache\\local-packages\\Python311\\Scripts
```

<aside> 💡 NOTE: it is possible that following an update of python, the path changes, it will be necessary to seek the correct path starting from "\Packages\”

</aside>

1.  in power shell, use the command "cd" to go to the working directory of your project and type the command "django-admin startproject ProjectName

```powershell
django-admin startproject ProjectName
```

-   Navigate once again to the project directory and type the following command to start the local server

```python
python [manage.py](<http://manage.py/>) runserver
```

![3-4-createProjectAndRun.png](/assets/images/bits/3-4-createProjectAndRun.png)

1.  In your browser, type "localhost:8000" and see the default page of Django
    
    ![5-defaultPageDjango.png](/assets/images/bits/5-defaultPageDjango.png)
    

## Install Python & Django on MacOS

1.  Open the package and follow the instructions on screen in order to install python. You may have to enter your password to allow the installation. You’re done !
2.  Install the Python package manager (pip) by pasting this line in the terminal in order to add new modules to our python projects.

```bash
python3 -m pip install --upgrade pip
```

1.  To install Django, simply enter the line below in the terminal. This is using the Python Package Manager (See previous step)

```bash
pip3 install Django
```

# Sources

[Django #1 - introduction](https://www.youtube.com/watch?v=iBGhDHtysAA&list=PLrSOXFDHBtfED_VFTa6labxAOPh29RYiO&index=1)

[Installing-python-on-mac](https://www.dataquest.io/blog/installing-python-on-mac/)