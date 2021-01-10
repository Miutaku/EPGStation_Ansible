# RecServer_Ansible

Setup TV recorder server with Ansible.

Using repository: [l3tnun/docker-mirakurun-epgstation](https://github.com/l3tnun/docker-mirakurun-epgstation)

This Ansible support Ubuntu 20.04 LTS only.

## Needs

- Working Ubuntu20.04 on TV recorder server machine.
- If you want to play ansible from ssh client, server can ssh.
- Added 1 data disk on TV recorder server machine.
- Create a user who can use `sudo` on the TV recorder server machine.
- Installed `ansible` and `ansible-playbook` on ansible playing machine.

Install Ansible example:

```sh
macOS> $ brew install hudochenkov/sshpass/sshpass
macOS> $ brew install ansible ansible-lint
```


## By the way...

It may be a little helpful for you to run this playbook :)


### Production Server info

My private server's spec is here.
- CPU: core i5 4460
- RAM: 8GB
- OS Storage(`/dev/sda`): SSD 128GB
- Data Storage(`/dev/sdb`): HDD 500GB

### Test Server info

Tested by VirtualBox VM with Ubuntu VM Image.
Deploy time is **about 30 min. too long time.** So, you may wait too long time. Do with coffee :)

Used Image: [osboxes.org's Ubuntu 20.04](https://www.osboxes.org/ubuntu/#ubuntu-20-04-info)


## Ansible Player info

- Machine: MBA 2018
- OS: macOS 11 Big Sur 


## How to use

### 1. Replace slack's webhook url (optional)

Replace `roles/rec_server/docker_launch/vars/main.yml`.

```sh
$ echo "webhook: <your webhookurl>" > roles/rec_server/docker_launch/vars/main.yml
```

### 2. Using VAAPI (optional)

```sh
$ vim roles/rec_server/docker_launch/template/docker-compose.yml.j2
- #        devices:
+         devices:
- #            - /dev/dri:/dev/dri
+             - /dev/dri:/dev/dri
```

### 3. Change servername file

Add hostname `inventories/recserver`

* Servername

```sh
$ echo <your servername> >> inventories/recserver
```


### 4. Modfiy mirakurun config

Edit the following to suit your environment.
- roles/rec_server/docker_launch/template/tuners.yml.j2
- roles/rec_server/docker_launch/template/channels.yml.j2

see sample: https://github.com/l3tnun/docker-mirakurun-epgstation/tree/master/mirakurun/conf


### 5. Play ansible playbook

Play command is here.

```sh
$ git clone git@github.com:Miutaku/EPGStation_Ansible.git
$ cd EPGStation_Ansible
$ ansible-playbook -i inverntories/recserver deploy_recserver.yml -K 
```


## Thanks

- **EPGStation**
  - [l3tnun/docker-mirakurun-epgstation](https://github.com/l3tnun/docker-mirakurun-epgstation) : docker-mirakurun-epgstation
    - [MIT License](https://github.com/l3tnun/docker-mirakurun-epgstation/blob/master/LICENSE)


## LICENSE

[MIT License](https://github.com/collelog/tv-recorder/blob/master/LICENSE)
