For create nodes on Ansible, we do some steps:
1. Access to AWS console:
2. Open 3 instance: 1 master node, 2 worker nodes:
3. Work on AWS linux, 2t mikro and connect to them:
4. sudo yum install ansible =in master node we install Ansible:
5. ansible --version:
6. Copy private key from Downloads
7. in master node go to ansible folder (default)
9. vi ~/.ssh/id_rsa     and paste private key from Downloads
10. cd ..
11. cd ~
12. cd .ssh
13. chmod 400 id_rsa
14. ls
13. sudo vi hosts: [node1] private IP adreess.
15. ssh to private key of node 1 
16. echo '172.31.17.108' | sudo tee -a /etc/ansible/hosts  (inventory)
15. cat /etc/ansible/hosts
16. ansible all -m ping
17. vi nginx.setup.yml  put inside the task
   ---
---
- hosts: all
  become: true
  tasks:
    - name: Update all packages
      yum:
        name: "*"
        state: latest

    - name: Install Nginx
      yum:
        name: nginx
        state: present

    - name: Create a custom HTML page
      copy:
        dest: /usr/share/nginx/html/index.html
        content: |
          <html>
          <head>
              <title>Welcome to Nginx!</title>
          </head>
          <body>
              <h1>Nginx is running on the Worker Node!</h1>
          </body>
          </html>

    - name: Ensure Nginx is started and enabled
      service:
        name: nginx
        state: started
        enabled: true


    19. ansible-playbook -i /etc/ansible/hosts nginx_setup.yml

    20. copy public IP from master and check welcome page.
    We should see "Nginx is running on the Worker Node!"
