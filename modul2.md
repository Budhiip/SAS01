# **Praktikum Modul 2**

### Fairuzrizqi Nugraharsanto (1202190044)
### Budhi Priambodo (1202192065)

---

1. Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

   * Cek lxc dengan menggunakan 

   ```markdown
    lxc-ls -f
   ```
   ![1](https://user-images.githubusercontent.com/92350603/144398558-b12ea29e-3d6f-4f9a-a1ce-e7dc203f084f.png)

   

   * Hapus ubuntu landing dengan menggunakan  command seperti dibawah ini, dan buat ubuntu focal baru dengan lxc-create

   ```markdown
    lxc-destroy ubuntu_landing
   ```
   ![2](https://user-images.githubusercontent.com/92350603/144399349-fd64ed4b-f22e-4861-92ed-7cde94e5c75c.png) 
   ![3](https://user-images.githubusercontent.com/92350603/144399542-90ebf4f8-130d-410c-8ff5-f4e9eec5861c.png) 


- Setelah membuat baru, gunakan command lxc-start untuk memulai ubuntu_landing dan gunakan command lxc-attach untuk membuka ubuntu_landing. Lalu gunakan install nano untuk mengedit config.
  
  ![4](https://user-images.githubusercontent.com/92350603/144399608-29608414-e7c8-40ee-bbca-594019c96509.png)

- Atur IP ubuntu_landing
  ```markdown
  sudo lxc-start -n ubuntu_landing
  sudo lxc-attach  -n ubuntu_landing
  nano /etc/netplan/10-lxc.yaml
  netplan apply
  ```
   ![5](https://user-images.githubusercontent.com/92350603/144399632-b3be7ef6-cb97-478f-b2a5-6569350ae8d5.png)
   ![6](https://user-images.githubusercontent.com/92350603/144399973-afa6e4d1-657b-4b79-9b8f-d5ba4e1b6488.png)

  - atur autostart lxc, seperti dibawah ini :
  
   ![7](https://user-images.githubusercontent.com/92350603/144399948-000a0297-e113-4f34-9942-a389c82e0d4e.png)

  - install ssh 
  
   ![8](https://user-images.githubusercontent.com/92350603/144400034-869b66b0-5004-4738-9d0b-ebcf27531ceb.png)

    ```markdown
    PermitRootLogin yes
    RSAAuthentication yes
    service sshd restart
    
    ```
    
    ![9](https://user-images.githubusercontent.com/92350603/144400117-af8adfc4-a4b3-435c-b9ec-23b8ba034a16.png)


  - cek ssh apakah sudah berjalan atau belum

    ![10](https://user-images.githubusercontent.com/92350603/144400147-0ff14676-95d9-4f69-8f92-82276b886c57.png)



2. Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)

   - Cek lxc dengan menggunakan 

   ```markdown
    lxc-ls -f
   ```

   * Hapus ubuntu landing dengan menggunakan  command seperti dibawah ini, dan buat ubuntu_php7.4 baru dengan menggunakan command lxc-create

   ```markdown
    lxc-destroy ubuntu_php7.4
   ```

   ![2 1](https://user-images.githubusercontent.com/92350603/144401209-e815c339-0fd8-41a8-a343-7ec871bd0088.png)


   - Setelah membuat baru, gunakan command lxc-start untuk memulai ubuntu_7.4 dan gunakan command lxc-attach untuk membuka ubuntu_7.4. Lalu gunakan install nano untuk mengedit config.

     ![2 2](https://user-images.githubusercontent.com/92350603/144401633-87337fe6-2330-4b78-b2c6-aba54872865c.png)

     
   
   - Atur IP ubuntu_php7.4
   
     Dengan Menggunakan

     ```markdown
     sudo lxc-start -n ubuntu_php7.4
     sudo lxc-attach  -n ubuntu_php7.4
     nano /etc/netplan/10-lxc.yaml
     netplan apply
     
     ```

    ![2 3](https://user-images.githubusercontent.com/92350603/144401820-d4254d7e-7214-4d9c-afcf-1523f8288f90.png)

    ![2 4](https://user-images.githubusercontent.com/92350603/144401841-0ab16777-12c0-46b4-94de-3edf69834578.png)

   
   - Hentikan ubuntu_php7.4 dengan menggunakan command dan auto start

     ```markdown
     lxc-stop ubuntu_php7.4
     ```

     ![2 5](https://user-images.githubusercontent.com/92350603/144402034-6889633f-5735-4637-b510-904f71223323.png)
 

   - Cek lxc dengan menggunakan 

   ```
    lxc-ls -f
   ```
   
   - install ssh
   
      ![2 6](https://user-images.githubusercontent.com/92350603/144402143-ff6b1bc7-c4ff-4aed-8b31-7495094a0a92.png)

      ![2 7](https://user-images.githubusercontent.com/92350603/144402153-066381a4-38e8-4aa1-b025-56457475a4c1.png)

   
   - Atur password baru
   
    
     ![2 8](https://user-images.githubusercontent.com/92350603/144402209-a2a69e6d-83cf-471e-ae27-d75b985b9762.png)

   
   - cek ssh apakah sudah berjalan atau belum
    
     <img width="325" alt="2 9" src="https://user-images.githubusercontent.com/92350603/144402245-1574b0ac-6ade-406b-935e-e2868882c826.PNG">

3. vm.local/

- Langkah pertama yang harus dilakukan yakni menginstall laravel  menggunakan ansible. Setelah menginstall, masuk ke ansible tersebut dan buatlah folder laravel

   ![20](https://user-images.githubusercontent.com/61863147/144441684-ff34a07b-69de-4753-99fc-6ffb6f93b3fe.PNG)

  
- Selanjutnya, buat host untuk lxc yang nanti akan di otomasi

  ![21](https://user-images.githubusercontent.com/61863147/144441808-d6454fc4-e5cd-4e05-8a34-71b11a902a11.PNG)


   

  ```markdown
  [landing]
  ubuntu_landing ansible_host=lxc_landing.dev ansible_ssh_user=root ansible_become_pass=sepasi
  
  ```

  * Buatlah directory serta apapun yang akan digunakan untuk menjalankan folder php dan lakukan instalasi
          	
    ![WhatsApp Image 2021-12-02 at 9 33 51 PM](https://user-images.githubusercontent.com/61863147/144442200-e1da5123-f90b-4f9e-99f6-d87a9c444b49.jpeg)

    

  ```
  ---
  - hosts: all
    become : yes
    tasks:
      - name: install nginx nginx extras
        apt:
         pkg:
           - nginx
           - nginx-extras
         state: latest
      - name: start nginx
        service:
         name: nginx
         state: started
      - name: menginstall tools
        apt:
         pkg:
           - curl
           - software-properties-common
           - unzip
         state: latest
      - name: "Repo PHP 7.4"
        apt_repository:
          repo="ppa:ondrej/php"
      - name: "Updating the repo"
        apt: update_cache=yes
      - name: Installation PHP 7.4
        apt: name=php7.4 state=present
      - name: install php untuk laravel
        apt:
         pkg:
            - php7.4-fpm
            - php7.4-mysql
            - php7.4-mbstring
            - php7.4-xml
            - php7.4-bcmath
            - php7.4-json
            - php7.4-zip
            - php7.4-common
         state: present
  ```

  

  - Jika instalasi telah selesai dilakukan, buat folder installcomposer.yml

    ![WhatsApp Image 2021-12-02 at 9 34 41 PM](https://user-images.githubusercontent.com/61863147/144442376-7d7268cd-0f60-4144-b554-7b5da7b4a3d2.jpeg)

    


  ```
  ---
   -hosts: all
    become : yes
    tasks:
     - name: Download and install Composer
       shell: curl -sS https://getcomposer.org/installer | php
       args:
        chdir: /usr/src/
        creates: /usr/local/bin/composer
        warn: false
     - name: Add Composer to global path
       copy:
        dest: /usr/local/bin/composer
        group: root
        mode: '0755'
        owner: root
        src: /usr/src/composer.phar
        remote_src: yes
     - name: Composer create project
       become_user: root
       composer:
        command: create-project
        arguments: laravel/laravel landing 
        working_dir: /var/www/html
        prefer_dist: yes
       environment:
          COMPOSER_NO_INTERACTION: "1"
     - name: mengkopi file .env.example jadi .env
       copy:
        dest: /var/www/html/landing/.env.example
        src: /var/www/html/landing/.env
        remote_src: yes
     - name: mengganti konfigurasi .env
       lineinfile:
        path: /var/www/html/landing/.env
        regexp: "{{ item.regexp }}"
        line: "{{ item.line }}"
        backrefs: yes
       loop:
        - { regexp: '^(.*)DB_HOST(.*)$', line: 'DB_HOST=10.0.3.200' }
        - { regexp: '^(.*)DB_DATABASE(.*)$', line: 'DB_DATABASE=landing' }
        - { regexp: '^(.*)DB_USERNAME(.*)$', line: 'DB_USERNAME=admin' }
        - { regexp: '^(.*)DB_PASSWORD(.*)$', line: 'DB_PASSWORD= ' }
        - { regexp: '^(.*)APP_URL(.*)$', line: 'APP_URL=http://vm.local' }
        - { regexp: '^(.*)APP_NAME=(.*)$', line: 'APP_NAME=landing' }
     - name: Composer install ke landing
       composer:
         command: install
         working_dir: /var/www/html/landing
       environment:
         COMPOSER_NO_INTERACTION: "1"
     - name: generate php artisan
       args:
        chdir: /var/www/html/landing
       shell: php artisan key:generate
     - name: mengganti permission storage
       file:
        path: /var/www/html/landing/storage
        mode: 0777
        recurse: yes
  
  ```

  

  

  - Lakukan instalasi kembali
  
      ![2021-11-30_6](https://user-images.githubusercontent.com/61863147/144442932-4960a69b-a892-4e5c-b4cd-1e532bfd4165.png)


  - Buatlah file lxc_landing.dev

       ![22](https://user-images.githubusercontent.com/61863147/144443067-3965ad39-c88f-4250-9035-0f9763871e9c.PNG)


    ```
    server {
            listen 80;
    
            root /var/www/html/landing/public;
            index index.php index.html index.htm;
            server_name lxc_landing.dev;
    
            error_log /var/log/nginx/landing_error.log;
            access_log /var/log/nginx/landing_access.log;
    
            client_max_body_size 100M;
            location / {
                    try_files $uri $uri/ /index.php$args;
            }
            location ~\.php$ {
                    include snippets/fastcgi-php.conf;
                    fastcgi_pass unix:run/php/php7.4-fpm.sock;
                    fastcgi_param SCRIPTFILENAME $document_root$fastcgi_script_name;
            }
    }
    ```

    

  - Buatlah file config.yml

   ![23](https://user-images.githubusercontent.com/61863147/144443120-2b2ad19d-4db6-4943-b5f3-62386ce1ad29.PNG)
 

    

    ```
    ---
    - hosts: all
      become : yes
      vars:
        domain: 'lxc_landing.dev'
      tasks:
       - name: stop apache2
         service:
          name: apache2
          state: stopped
          enabled: no
       - name: Write {{ domain }} to /etc/hosts
         lineinfile:
          dest: /etc/hosts
          regexp: '.*{{ domain }}$'
          line: "127.0.0.1 {{ domain }}"
          state: present
       - name: ensure nginx is at the latest version
         apt: name=nginx state=latest
       - name: start nginx
         service:
          name: nginx
          state: started
       - name: copy the nginx config file 
         copy:
          src: ~/ansible/laravel/lxc_landing.dev
          dest: /etc/nginx/sites-available/lxc_landing.dev
       - name: Symlink lxc_landing.dev
         command: ln -sfn /etc/nginx/sites-available/lxc_landing.dev /etc/nginx/sites-enabled/lxc_landing.dev
         args:
          warn: false
       - name: restart nginx
         service:
          name: nginx
          state: restarted
       - name: restart php7
         service:
          name: php7.4-fpm
          state: restarted
       - name: curl web
         command: curl -i http://lxc_landing.dev
         args:
          warn: false
    ```

    

  - Lakukan instalasi

       ![24](https://user-images.githubusercontent.com/61863147/144443261-e6ca8f84-3d87-4ec4-8db7-92eba8f2da3e.PNG)


    

    

  - Cek dengan cara membuka vm.local. Jika sukses, maka tampilannya akan seperti berikut ini :

  ![25](https://user-images.githubusercontent.com/61863147/144443323-1fe9ff51-0a6f-481e-8364-80974108f3dd.PNG)
      
    
    



4. vm.local/blog

   - Seperti pada nomor sebelumnya, langkah pertama dimulai dengan masuk pada folder ansible
   - 
           	![WhatsApp Image 2021-12-02 at 9 41 20 PM](https://user-images.githubusercontent.com/61863147/144443674-b3136603-7e6c-498d-bdbf-20c4a2c1ec7f.jpeg)

   
     
     
   - Buat host untuk lxc yang nanti akan di otomasi
    
       ![26](https://user-images.githubusercontent.com/61863147/144443579-52b51a5c-e728-4c9f-afa5-92634e001bda.PNG)


   
   ```
   [blog]
   ubuntu_php7.4 ansible_host=lxc_php7.dev ansible_ssh_user=root ansible_become_pass=sepasi
   ```
   
   
   
   - Buat direktori untuk tasks,templates dan handlers di folder wordpress. Lalu, masuk ke dalam folder tasks untuk menginstall paket
   
       ![27](https://user-images.githubusercontent.com/61863147/144443757-e268b7a1-7485-45cb-a8a8-4f2a4007d8dc.PNG)
   
   ```
   ---
   - hosts: all
     vars:
       domain: 'lxc_php7.dev'
     tasks:
      - name: delete apt chache
        become: yes
        become_user: root
        become_method: su
        command: rm -vf /var/lib/apt/lists/*
   
      - name: install requirement
        become: yes
        become_user: root
        become_method: su
        apt: name={{ item }} state=latest update_cache=true
        with_items:
         - nginx
         - nginx-extras
         - curl
         - wget
         - php7.4
         - php7.4-fpm
         - php7.4-curl
         - php7.4-xml
         - php7.4-gd
         - php7.4-opcache
         - php7.4-mbstring
         - php7.4-zip
         - php7.4-json
         - php7.4-cli
         - php7.4-mysqlnd
         - php7.4-xmlrpc
         - php7.4-curl
   
      - name: wget wordpress
        shell: wget -c http://wordpress.org/latest.tar.gz
   
      - name: tar latest.tar.gz
        shell: tar -xvzf latest.tar.gz
   
      - name: copy folder wordpress
        shell: cp -R wordpress /var/www/html/blog
   
      - name: chmod
        become: yes
        become_user: root
        become_method: su
        command: chmod 775 -R /var/www/html/blog/
   
      - name: copy .wp-config.conf
        copy:
         src=~/ansible/wordpress/wp.conf
         dest=/var/www/html/blog/wp-config.php
   
      - name: copy wordpress.conf
        copy:
         src=~/ansible/wordpress/wordpress.conf
         dest=/etc/nginx/sites-available/{{ domain }}
        vars:
         servername: '{{ domain }}'
   
      - name: Symlink wordpress.conf
        command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
      
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
   
      - name: Write {{ domain }} to /etc/hosts
        lineinfile:
         dest: /etc/hosts
         regexp: '.*{{ domain }}$'
         line: "127.0.0.1 {{ domain }}"
         state: present
   
      - name: enable module php mbstring
        command: phpenmod mbstring
   
      - name: restart php
        become: yes
        become_user: root
        become_method: su
        action: service name=php7.4-fpm state=restarted
   
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
   ```
   
   
   
   - Kemudian, masuk ke dalam templates wp.conf yang merupakan tempat configuration pada wordpress
  
       ![28](https://user-images.githubusercontent.com/61863147/144443813-d9b82e9c-98be-42f9-9c4a-d71751024e72.PNG)

  
   
     
   
     ```
     <?php
     /**
      * The base configuration for WordPress
      *
      * The wp-config.php creation script uses this file during the installation.
      * You don't have to use the web site, you can copy this file to "wp-config.php"
      * and fill in the values.
      *
      * This file contains the following configurations:
      *
      * * MySQL settings
      * * Secret keys
      * * Database table prefix
      * * ABSPATH
      *
      * @link https://wordpress.org/support/article/editing-wp-config-php/
      *
      * @package WordPress
      */
     
     define( 'WP_HOME', 'http://vm.local/blog' );
     define( 'WP_SITEURL', 'http://vm.local/blog' );
     
     // ** MySQL settings - You can get this info from your web host ** //
     /** The name of the database for WordPress */
     define( 'DB_NAME', 'blog' );
     
     /** MySQL database username */
     define( 'DB_USER', 'admin' );
     
     /** MySQL database password */
     define( 'DB_PASSWORD', 'SysAdminSas0102' );
     
     /** MySQL hostname */
     define( 'DB_HOST', '10.0.3.200:3306' );
     
     /** Database charset to use in creating database tables. */
     define( 'DB_CHARSET', 'utf8' );
     
     /** The database collate type. Don't change this if in doubt. */
     define( 'DB_COLLATE', '' );
     
     /**#@+
      * Authentication unique keys and salts.
      *
      * Change these to different unique phrases! You can generate these using
      * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
      *
      * You can change these at any point in time to invalidate all existing cookies.
      * This will force all users to have to log in again.
      *
      * @since 2.6.0
      */
     define( 'AUTH_KEY',         'put your unique phrase here' );
     define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
     define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
     define( 'NONCE_KEY',        'put your unique phrase here' );
     define( 'AUTH_SALT',        'put your unique phrase here' );
     define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
     define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
     define( 'NONCE_SALT',       'put your unique phrase here' );
     
     /**#@-*/
     
     /**
      * WordPress database table prefix.
      *
      * You can have multiple installations in one database if you give each
      * a unique prefix. Only numbers, letters, and underscores please!
      */
     $table_prefix = 'wp_';
     
     /**
      * For developers: WordPress debugging mode.
      *
      * Change this to true to enable the display of notices during development.
      * It is strongly recommended that plugin and theme developers use WP_DEBUG
      * in their development environments.
      *
      * For information on other constants that can be used for debugging,
      * visit the documentation.
      *
      * @link https://wordpress.org/support/article/debugging-in-wordpress/
      */
     define( 'WP_DEBUG', false );
     
     /* Add any custom values between this line and the "stop editing" line. */
     
     
     
     /* That's all, stop editing! Happy publishing. */
     
     /** Absolute path to the WordPress directory. */
     if ( ! defined( 'ABSPATH' ) ) {
             define( 'ABSPATH', __DIR__ . '/' );
     }
     
     /** Sets up WordPress vars and included files. */
     require_once ABSPATH . 'wp-settings.php';
     
     ```
   
     
   
   - Masuk ke dalam templates wordpress.conf
   
        ![29](https://user-images.githubusercontent.com/61863147/144443861-7c887fa6-a569-4dd2-8e22-1779d2bdb8d7.PNG)
   
     ```
     server {
          listen 80;
          listen [::]:80;
     
          # Log files for Debugging
          access_log /var/log/nginx/wordpress-access.log;
          error_log /var/log/nginx/wordpress-error.log;
     
          # Webroot Directory for Laravel project
          root /var/www/html/blog;
          index index.php index.html index.htm;
     
          # Your  Name
          server_name lxc_php7.dev;
     
          location / {
                  try_files $uri $uri/ /index.php?$query_string;
          }
     
          # PHP-FPM Configuration Nginx
          location ~ \.php$ {
                  try_files $uri =404;
                  fastcgi_split_path_info ^(.+\.php)(/.+)$;
                  fastcgi_pass unix:/run/php/php7.4-fpm.sock;
                  fastcgi_index index.php;
                  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                  include fastcgi_params;
          }
     }
     ```
   
     
   
     - Jalankan ansible kembali untuk menginstall
   
         ![30](https://user-images.githubusercontent.com/61863147/144443991-095f3c89-b039-430a-bf64-23d67a0110dd.PNG)
   
     
   
   - Buka vm.local/blog untuk melakukan checking apakah wordpressnya sudah dapat dijalankan atau belum. Jika sudah dapat dijalankan, maka tampilannya akan berubah menjadi berikut :
   

    	![31](https://user-images.githubusercontent.com/61863147/144444084-53581b08-4d22-4c88-8cb2-3b831c557c93.PNG)

   
      ![33](https://user-images.githubusercontent.com/61863147/144444144-670aee04-5810-4b06-9880-8492f3d8b10e.PNG)


      ![34](https://user-images.githubusercontent.com/61863147/144444175-fa8b4586-a069-46cc-b555-4bd0e239d916.PNG)

     
      ![35](https://user-images.githubusercontent.com/61863147/144444207-9370b548-f8a4-4091-b07e-bb8c83945cc2.PNG)