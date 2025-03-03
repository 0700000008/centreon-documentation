---
id: unattended-install-poller
title: Installation silencieuse d'un collecteur
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Pour installer un collecteur plus rapidement, vous pouvez utiliser un script. Le script exécutera les étapes d'installation proprement dites. Vous devrez ensuite enregistrer le collecteur et le rattacher au serveur central ou au serveur distant.

## Procédure d'installation

1. Mettez votre système à jour :

<Tabs groupId="sync">
<TabItem value="RHEL 8" label="RHEL 8">

```shell
dnf update
subscription-manager register --username my_username --password my_password --auto-attach --force
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
```

> Remplacez **my_username** et **my_password** par les identifiants de votre compte RedHat.

</TabItem>

<TabItem value="Alma / Oracle Linux 8" label="Alma / Oracle Linux 8">

```shell
dnf update
```

</TabItem>
<TabItem value="RHEL 9" label="RHEL 9">

```shell
dnf update
subscription-manager register --username my_username --password my_password --auto-attach --force
subscription-manager repos --enable codeready-builder-for-rhel-9-x86_64-rpms
```

</TabItem>
<TabItem value="Alma / Oracle Linux 9" label="Alma / Oracle Linux 9">

```shell
dnf update
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
apt update && apt upgrade
```

</TabItem>
</Tabs>

2. Téléchargez le script à l'aide de la commande suivante :

```shell
curl -L https://raw.githubusercontent.com/centreon/centreon/23.10.x/centreon/unattended.sh -O /tmp/unattended
```

3. Exécutez la commande suivante en **root** :

```shell
bash unattended.sh install -t poller -v 23.10 -r stable -l DEBUG  2>&1 |tee -a /tmp/unattended-$(date +"%m-%d-%Y-%H%M%S").log
```

  Vous obtiendrez un fichier de log complet avec toutes les erreurs dans votre répertoire **tmp**, fichier nommé **unattended(date).log**.

4. Une fois le script exécuté, suivez les [étapes 3 à 5 de la procédure d'installation d'un collecteur](./using-packages.md#step-3-register-the-server).

## Aide

Pour obtenir de l'aide sur le script, utilisez la commande suivante :

```shell
bash unattended.sh -h
```
