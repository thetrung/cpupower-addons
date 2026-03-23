cpupower Addons 
======================================
This small utility was done to customize `cpupower` tool.

### 1. Usecases
- `cpupower-set-range` : You want many-cores system to run at lower frequencies at once, for example : 400 ~ 600Mhz only in all cores. 

### 2. Setup 
- `git clone https://github.com/thetrung/cpupower-addons` to your `$HOME`.
- `mv bash_aliases .bash_aliases` (in case you don't have `.bash_aliases` yet)

      sudo chmod +x cpupower-set-range
      sudo mv cpupower-set* /usr/bin/
      sudo mv cpupower.service /etc/systemd/system/
      sudo systemctl daemon-reload
      sudo systemctl restart cpupower.service
   

### 3. Auto-Services
    
    cat << EOF | sudo tee /etc/systemd/system/cpupower.service
    [Unit]
    Description=CPU powersave
    [Service]
    Type=oneshot
    Restart=always
    ExecStart=usr/bin/cpupower-set-range 400 550
    [Install]
    WantedBy=multi-user.target
    EOF

Start Service :

    sudo systemctl daemon-reload && sudo systemctl enable cpupower.service

~ Enjoy ~
