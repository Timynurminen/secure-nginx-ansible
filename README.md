# Secure Nginx Ansible

## Infrastructure as Code -projekti, joka asentaa ja koventaa web-palvelimen Ansiblella. Se ei ole vielä täydellinen production-tason security baseline.

# Quick start

```bash
sudo apt update
sudo apt install -y ansible git openssh-client
```

#### Ohjeet SSH yhteyden muodostamiseen Githubissa

**Luo SSH-avain**

```bash
ssh-keygen -t ed25519 -C "email@example.com"
```
Paina enteriä kaikkiin kysymyksiin

**Lisää avain githubiin**

```bash
cat ~/.ssh/id_ed25519.pub
```

- Githubista: Settings
- SSH and GPG keys
- New SSH key
- liitä avain

**Testaa yhteys**

```bash
ssh -T git@github.com
```

## Kloonaa projekti

```bash
git clone git@github.com:Timynurminen/secure-nginx-ansible.git
cd secure-nginx-ansible
```

## Aja Ansible

```bash
ansible-playbook site.yml -K
```

- Syötä sudo-salasana pyydettäessä

## Testaus

```bash
firefox http://localhost
```

**TAI**

```bash
curl http://localhost
```

# Mitä projekti tekee

- Asentaa Nginx
- Kopioi web-sivun
- Lisää security headerit
- Konfiguroi UFW palomuurin (SSH + HTTP)
- Asentaa Fail2Ban
- Koventaa SSH:n (root login pois)

## Miten projekti on rakennettu

- site.yml: pää-playbook
- roles/: Ansible-roolit:
  - nginx
  - firewall
  - fail2ban
  - ssh
- hosts.ini: localhost inventory
- ansible.cfg: Määrittää inventoryn automaattisesti


# Lopputulos

Yhdellä komennolla saat:

- valmiin web-palvelimen
- perus kovennuksen
- palomuurin
- brute force -suojauksen
