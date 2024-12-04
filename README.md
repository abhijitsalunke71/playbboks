# playbook files 

A)  playbook to retrive and display the current date and time 

- name: Retrieve and display date and logged-in user
  hosts: production
  become: yes  # Use become to execute commands with sudo if necessary
  tasks:
    - name: Show current date
      command: date
      register: current_date

    - name: Display current date
      debug:
        msg: "Current date is {{ current_date.stdout }}"

    - name: Show logged-in user
      command: whoami
      register: logged_in_user

    - name: Display logged-in user
      debug:
        msg: "Logged-in user is {{ logged_in_user.stdout }}"


B)  playbook update the apt package manager install java 


- name: Update apt package manager, install Java, and display version
  hosts: production
  become: yes
  tasks:
    - name: Update apt package manager
      apt:
        update_cache: yes

    - name: Install Java 17
      apt:
        name: openjdk-17-jdk
        state: present

    - name: Display Java version
      command: java -version
      register: java_version

    - name: Show Java version
      debug:
        msg: "Java Version: {{ java_version.stderr }}"


C)  Install Nginx Web Server and Start the Service


---
- name: Install Nginx web server and start the service
  hosts: production
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes  # Ensure it starts on boot


D)   Copy a Shell Script from the Control Node to Managed Nodes and Execute It

---
- name: Copy shell script and execute it
  hosts: production
  become: yes
  tasks:
    - name: Copy the shell script to managed node
      copy:
        src: /path/to/your/script.sh
        dest: /home/ubuntu/script.sh
        mode: '0755'  # Make it executable

    - name: Execute the shell script
      command: /home/ubuntu/script.sh



E) Add Multiple Users on All Managed Nodes

---
- name: Add multiple users with home directories
  hosts: production
  become: yes
  tasks:
    - name: Add user1
      user:
        name: user1
        state: present
        create_home: yes

    - name: Add user2
      user:
        name: user2
        state: present
        create_home: yes

    - name: Add user3
      user:
        name: user3
        state: present
        create_home: yes







