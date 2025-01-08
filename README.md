# Guide-to-Install-Frappe-iVendNext-Using-Docker

A complete Guide to Install Frappe Bench in Windows 11 Using Docker and install Frappe/iVendNext Application

### Pre-requisites 

    Docker Desktop
    git
    Wnidows 11 
    VS Code

### STEP 1 Check Docker version
    docker version
    git version

### STEP 2  Clone frappe_docker and move to frappe_docker folder

    git clone https://github.com/frappe/frappe_docker.git
    cd frappe_docker

### STEP 3

   Copy example devcontainer config from 
    
    devcontainer-example folder to .devcontainer folder
    
   Copy example vscode config for devcontainer from 
    
    development/vscode-example folder to development/.vscode folder
   
### STEP 4 Install VSCode Remote Containers extension
    
    Open vscode and install 'Dev Containers' extension
    
###  STEP 5 After the extensions are installed, you can

  Open frappe_docker folder in VS Code.
  
  Launch the command, from Command Palette (Ctrl + Shift + P) Remote-Containers: Reopen in Container. You can also click in the bottom left corner to access the remote   container menu.
  
### Note: 
   if this error in running contaners try the below commnad in CMD
   
   Error starting userland proxy: listen tcp 0.0.0.0:80: bind: An attempt was made to access a socket in a way forbidden by its access permissions
	
    netsh http add iplisten ipaddress=::
                
   The development directory is ignored by git. It is mounted and available inside the container. Create all your benches (installations of bench, the tool that          manages frappe) inside this directory.
   Node v14 and v10 are installed. Check with nvm ls. Node v14 is used by default.
                
    
### STEP 6 Initilase frappe bench with frappe version 14 and Switch directory

    
    bench init --skip-redis-config-generation --frappe-branch version-15 ivend-bench
    cd ivend-bench

### STEP 7 Delete frappe folder from the ivend-bench app 
 
    Delete \development\ivend-bench\apps\frappe
    
### STEP 8 Install iVendFramework

    bench get-app --branch Release-1.0 --resolve-deps https://github.com/ivendnext/iVendFramework.git

### STEP 9 Setup hosts
    
   We need to tell bench to use the right containers instead of localhost. Run the following commands inside the container:

    bench set-config -g db_host mariadb
    bench set-config -g redis_cache redis://redis-cache:6379
    bench set-config -g redis_queue redis://redis-queue:6379
    bench set-config -g redis_socketio redis://redis-socketio:6379
  For any reason the above commands fail, set the values in common_site_config.json manually.

    {
	 "db_host": "mariadb",
	 "redis_cache": "redis://redis-cache:6379",
	 "redis_queue": "redis://redis-queue:6379",
	 "redis_socketio": "redis://redis-socketio:6379"
    }
    
### STEP 10 Create a new site
   sitename MUST end with .localhost for trying deployments locally.
   MariaDB root password: 123
    
    bench new-site cdivendnext.com --no-mariadb-socket  

### STEP 11 Set bench developer mode on the new site
    
    bench --site cdivendnext.com set-config developer_mode 1
    bench --site cdivendnext.com clear-cache 
       
### STEP 12 Install iVendNext
    
    bench get-app --branch Release-1.0 --resolve-deps https://github.com/ivendnext/iVendNext.git
    
### STEP 13 Install iVendNext app in site

    bench --site cdivendnext.com install-app erpnext
    
### STEP 14 Install iVend-POS
    
    bench get-app --branch develop --resolve-deps https://github.com/ivendnext/iVend-POS.git
    
### STEP 13 Install iVendNext app in site

    bench --site cdivendnext.com install-app ivendnext_pos   
    
### STEP 14 Start Frappe bench 
    
    bench start
    
You can now login with user Administrator and the password you choose when creating the site. Your website will now be accessible at location cdivendnext.com:8000
    
   
