FROM ubuntu

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install libc6-i386 -y
RUN apt-get install lib32gcc1 -y
RUN apt-get install wget -y
RUN apt-get install lib32stdc++6 -y
RUN mkdir ~/Steam
RUN cd ~/Steam && wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
RUN cd ~/Steam && tar -xvzf steamcmd_linux.tar.gz

RUN echo "login anonymous \n\
force_install_dir ./csgo-ds \n\
app_update 740 validate \n\
quit\n" > ~/Steam/script.txt

RUN ~/Steam/steamcmd.sh +runscript ~/Steam/script.txt

RUN echo 'hostname "eagulov"\n\
sv_password "server_password"\n\
sv_timeout 60\n\
rcon_password "rcon_password"\n\
mp_autoteambalance 1\n\
mp_limitteams 1\n\
writeid\n\
writeip\n' > ~/Steam/csgo-ds/csgo/cfg/server.cfg

RUN mkdir ~/.steam/sdk32/ && ln -s ~/Steam/linux32/steamclient.so ~/.steam/sdk32/steamclient.so

CMD cd ~/Steam/csgo-ds/ && ./srcds_run -game csgo -usercon +game_type 0 +game_mode 1 +mapgroup mg_bomb +map de_dust2  -net_port_try 1 
